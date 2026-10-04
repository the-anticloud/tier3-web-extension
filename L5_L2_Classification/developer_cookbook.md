# Developer Cookbook — web-extension
**Stack:** TypeScript, WebExtension API (Chrome/Firefox), WebSocket (LAN only), AIOSS_FORMAT
**Domain:** Sovereign browser extension: local AI assistant powered by PAX 27B via LAN API
**License:** Apache-2.0 | **IP:** USPTO pending 2026, Anticloud FZ LLE

## Core Usage

```typescript
// Background service worker
chrome.runtime.onMessage.addListener(async (msg, sender, reply) => {
  if (msg.type === 'pax_query') {
    const ws = new WebSocket('ws://localhost:8081/chat');
    ws.onopen = () => ws.send(JSON.stringify({ message: msg.text }));
    ws.onmessage = (e) => {
      const resp = JSON.parse(e.data);
      reply({ text: resp.text, chainHash: resp.chain_hash });
    };
  }
});

// Content script: highlight + explain
document.addEventListener('mouseup', async () => {
  const selection = window.getSelection()?.toString();
  if (selection) showPAXExplanation(selection);
});
```

## AIOSS Chain Append

```python
import hashlib, time

def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

# After every web-extension output:
chain_hash = aioss_append("./web_extension.aioss",
                           result_bytes, "web-extension")
```

## Performance & Integration

Performance: profile with api-oss-devtools. Benchmark with api-oss-analytics. Integration: all web-extension operations are logged to api-oss-logging and audited by api-oss-compliance.
