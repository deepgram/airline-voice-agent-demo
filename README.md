# Airline Voice Agent Demo

A one-page site for calling an airline voice agent from the browser. Speech runs on Deepgram STT/TTS
and the call is handled by Amazon Connect, joined through the Amazon Chime SDK.

Live: https://d2e3t4f1ay5rue.cloudfront.net/

## How it works

`index.html` gets temporary AWS credentials from a Cognito identity pool, asks the API endpoint in
`CONFIG` to start a Connect contact, and joins the returned Chime meeting for the audio. There is no
build step.

## Run locally

```sh
python3 -m http.server 8000
```

Calls need the Cognito pool and API to accept the origin you serve from.

## Deploy

The site is static files on S3 behind CloudFront. Upload the files to the site bucket and invalidate
the distribution. Ask the Deepgram AppEng team for access.
