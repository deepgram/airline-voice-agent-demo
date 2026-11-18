# Larkspur Air voice agent demo

A one-page site for calling Larkspur Air's support line from the browser. Larkspur Air is a fictional
airline: the travelers and bookings are made up. Speech runs on Deepgram speech-to-text and
text-to-speech, and the call is handled by Amazon Connect, joined through the Amazon Chime SDK.

Live: https://d2e3t4f1ay5rue.cloudfront.net/

## How it works

`index.html` gets temporary AWS credentials from a Cognito identity pool, asks the API endpoint in
`CONFIG` to start a Connect contact, and joins the returned Chime meeting for the audio. There is no
build step.

## Brand

- Name: Larkspur Air. Tagline: Airline · Customer care.
- Mark: an airplane window with two streaks, inline in `index.html` and in `favicon/larkspur.svg`.
- Design: follows Deepgram's Voice Demo UI kit. The landing is the kit's `HeroLanding` (an
  airplane-over-clouds photo, `images/landing-hero.jpg`, under Off-black scrims, one magenta Call button, a traveler toggle); on the call, the page switches to the
  stage (`stage-glow`) with a violet voice session panel, or a dock below 1024px wide. The kit's
  tokens are written out as plain CSS at the top of `index.html`, since there's no build step.
- Demo callers: Lisa Chen (booking 847291, Tokyo, seat 15A) and Carlos Martinez (booking 531068,
  first class upgrade). These must match the agent's data in Amazon Connect.
- The agent's greeting should name the brand: "Thanks for calling Larkspur Air. What's your booking
  number?" The greeting and prompts live in Amazon Connect, not in this repo.

## Run locally

```sh
python3 -m http.server 8000
```

Calls need the Cognito pool and API to accept the origin you serve from.

## Deploy

The site is static files on S3 behind CloudFront. Upload the files to the site bucket and invalidate
the distribution. Ask the Deepgram AppEng team for access.
