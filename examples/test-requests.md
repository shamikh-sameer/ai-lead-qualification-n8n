# Test requests

Replace `YOUR_WEBHOOK_URL` with the Test or Production URL shown in the **Lead Webhook** node.
Use your own email address so you can see the lead-facing emails arrive.

## Hot lead

**PowerShell**
```powershell
Invoke-RestMethod -Method Post -Uri "YOUR_WEBHOOK_URL" -ContentType "application/json" -Body '{"name":"Sara Khan","email":"you@example.com","phone":"+14045550123","service":"Emergency AC repair","message":"AC died today, it is 95 degrees and I need someone out ASAP. Happy to pay for same-day service."}'
```

**bash / curl**
```bash
curl -X POST "YOUR_WEBHOOK_URL" -H "Content-Type: application/json" -d '{
  "name": "Sara Khan", "email": "you@example.com", "phone": "+14045550123",
  "service": "Emergency AC repair",
  "message": "AC died today, it is 95 degrees and I need someone out ASAP. Happy to pay for same-day service."
}'
```

Expected: score 8-10, category `hot`; row logged; instant follow-up email to the lead and an alert email to the owner.

## Cold lead

```bash
curl -X POST "YOUR_WEBHOOK_URL" -H "Content-Type: application/json" -d '{
  "name": "Tom Reed", "email": "you@example.com", "phone": "",
  "service": "Not sure", "message": "just looking at prices, maybe next year"
}'
```

Expected: score 1-3, category `cold`; row logged; nurture email only.
