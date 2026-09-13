# Aligner Tracker website

Static features, support, and privacy pages for Aligner Tracker, published at
<https://aligner-tracker.alecbytes.com/>.

## Local preview

From the repository root, run:

```sh
python3 -m http.server 8000
```

Then open <http://localhost:8000/>.

## Deployment

See [DEPLOYMENT.md](DEPLOYMENT.md) for the first-publish steps, GitHub Pages
settings, custom-domain checks, HTTPS setup, and App Store Connect URLs.

## Public URLs

- Features: <https://aligner-tracker.alecbytes.com/features/>
- Support: <https://aligner-tracker.alecbytes.com/support/>
- Privacy: <https://aligner-tracker.alecbytes.com/privacy/>

GitHub Pages should publish from the root of the `main` branch. Keep the custom
domain and **Enforce HTTPS** enabled in the repository's Pages settings.

Before an App Store release, review the privacy wording against the final
production archive, privacy manifests, enabled dependencies, observed network
behavior, and App Store privacy answers.
