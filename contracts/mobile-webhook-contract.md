# Mobile Webhook Contract (JSON-only)

All mobile-triggered workflows accept JSON bodies only.

Required headers:
- Content-Type: application/json
- X-Mobile-Secret: <secret>

Canonical payload shape:
{
  "text": "optional",
  "url": "optional",
  "tags": ["optional"],
  "source": "ios-shortcut",
  "meta": {
    "device": "iphone",
    "sentAt": "2026-03-05T00:00:00Z"
  }
}

Recommended response shape:
{
  "ok": true,
  "runId": "<n8n execution id or generated id>",
  "receivedAt": "<ISO timestamp>"
}

Security gate:
Reject with HTTP 401 if X-Mobile-Secret is missing/incorrect.