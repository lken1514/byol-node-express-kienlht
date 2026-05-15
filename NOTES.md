# BYOL Node.js Express Deployment Notes

## Strategy Selected
**Strategy A: serverless-http adapter**

## Reasoning
This strategy was chosen because it adds the fewest changes while keeping the Express app Lambda-unaware.
- **Minimal code changes:** only a small Lambda entrypoint file plus one dependency.
- **App stays clean:** `app.js` remains framework-pure and reusable.
- **Predictable behavior:** widely used adapter with known behavior for Express.

## Cold Start Measurement
Based on CloudWatch logs (`REPORT` line):
- **Init Duration:** 295.33 ms

## Deployment Details
- **Tooling:** AWS SAM CLI
- **Runtime:** Node.js 22.x
- **Architecture:** arm64
- **API URL:** https://ucs99ioq44.execute-api.us-west-2.amazonaws.com

## Testing
- **Home:**
	```bash
	curl https://ucs99ioq44.execute-api.us-west-2.amazonaws.com/
	```
- **Hello API:**
	```bash
	curl https://ucs99ioq44.execute-api.us-west-2.amazonaws.com/api/hello/Lan
	```
- **Echo API (POST):**
	```bash
	curl -X POST https://ucs99ioq44.execute-api.us-west-2.amazonaws.com/api/echo -H 'Content-Type: application/json' -d '{"hi":"there"}'
	```

## Terminal Evidence
```text
2026/05/15/[$LATEST]2079e8a6266242739c97d84985cd5ce8 2026-05-15T08:47:00.722000+00:00 INIT_START Runtime Version: nodejs:22.v78   Runtime Version ARN: arn:aws:lambda:us-west-2::runtime:4347240e377e6d9179a8724a4c38e9d6805124c642ee77eb18178f0fd1f3bc09
2026/05/15/[$LATEST]2079e8a6266242739c97d84985cd5ce8 2026-05-15T08:47:01.020000+00:00 START RequestId: a5102125-3a8b-4dad-9c72-e73cde7334a6 Version: $LATEST
2026/05/15/[$LATEST]2079e8a6266242739c97d84985cd5ce8 2026-05-15T08:47:01.034000+00:00 END RequestId: a5102125-3a8b-4dad-9c72-e73cde7334a6
2026/05/15/[$LATEST]2079e8a6266242739c97d84985cd5ce8 2026-05-15T08:47:01.034000+00:00 REPORT RequestId: a5102125-3a8b-4dad-9c72-e73cde7334a6      Duration: 12.68 ms      Billed Duration: 309 ms Memory Size: 512 MB       Max Memory Used: 93 MB  Init Duration: 295.33 ms
```
