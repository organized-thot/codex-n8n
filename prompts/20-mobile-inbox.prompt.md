Generate a baseline workflow named "Mobile Inbox".

Trigger:
Webhook POST /mobile/inbox

Security:
- Require X-Mobile-Secret header, compare to secret stored in n8n variables/credentials.
- Reject with 401 if invalid.

Payload (JSON-only):
{
  "text": "optional",
  "url": "optional",
  "tags": ["optional"],
  "source": "ios-shortcut",
  "meta": { "sentAt": "<iso>", "device": "iphone" }
}

Behavior:
1) Validate secret
2) Normalize fields (ensure tags is always an array; fill source if missing)
3) Store to a simple log (e.g., write to static data or append to a file if permitted)
4) Respond JSON:
{ "ok": true, "receivedAt": "<iso>", "echo": { "text":..., "url":..., "tags":..., "source":... } }

Mandatory upgrades:
- Include validation report
- Include test harness
- Provide Admin Upsert deploy payload