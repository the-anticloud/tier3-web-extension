# Deploy Guide — web-extension
**Platform:** Anticloud sovereign infrastructure | Air-gap capable
**Stack:** TypeScript, WebExtension API (Chrome/Firefox), WebSocket (LAN only), AIOSS_FORMAT

## Prerequisites
Python 3.11+. See stack: TypeScript, WebExtension API (Chrome/Firefox), WebSocket (LAN only), AIOSS_FORMAT. AIOSS_FORMAT required. PAX 27B weights for AI-assisted features.

## AIOSS Integration
```bash
aioss init --module web-extension --output ./web_extension.aioss
aioss append --chain ./web_extension.aioss --payload ./output.bin --module web-extension
aioss verify --chain ./web_extension.aioss
```

## Air-Gap Deployment
```bash
# On networked machine:
pip download -r requirements.txt -d ./wheels/
# Transfer wheels/ to air-gap host, then:
pip install --no-index --find-links ./wheels/ -r requirements.txt
```

## PAX 27B Harness Wiring
```python
from anticloud_pax import PAXHarness
harness = PAXHarness(
    model_path="./pax-27b-q4.gguf",
    module="web-extension",
    aioss_chain="./web_extension.aioss",
    classification="L5_NARROW_L2_GENERAL"
)
result = harness.process(input_data)
```

## Verification
```bash
aioss verify --chain ./web_extension.aioss --verbose
python -m web_extension.tests.smoke
```
