# Deployment guide

The site is published with GitHub Pages from the root of the `main` branch.
There is no build command, package installation, or deployment workflow.

Public URLs:

- Home: <https://aligner-tracker.alecbytes.com/>
- Support: <https://aligner-tracker.alecbytes.com/support/>
- Privacy: <https://aligner-tracker.alecbytes.com/privacy/>

## Current setup

The repository already contains the two files GitHub Pages needs for the custom
domain:

- `CNAME` contains `aligner-tracker.alecbytes.com`.
- `.nojekyll` tells GitHub Pages to serve the static files directly.

The public DNS record is also already correct:

```text
aligner-tracker.alecbytes.com CNAME alecbytes.github.io
```

Do not change the hosting or routes for `alecbytes.com` or
`www.alecbytes.com`. Those belong to the separate portfolio site on Vercel.

## First deployment

### 1. Sign in to GitHub from the command line

The GitHub CLI credentials currently saved on this computer are expired. From
the website repository, run:

```sh
gh auth login --hostname github.com --git-protocol https --web
gh auth setup-git
gh auth status
```

Complete the browser sign-in as the `AlecBytes` account. If more than one GitHub
account is configured, select the correct active account with:

```sh
gh auth switch --hostname github.com --user AlecBytes
```

### 2. Push the site

The initial site commit is already on the local `main` branch. Push it to the
empty GitHub repository:

```sh
git push --set-upstream origin main
```

Future deployments only require:

```sh
git push
```

### 3. Select the Pages publishing source

On GitHub:

1. Open <https://github.com/AlecBytes/aligner-tracker-website>.
2. Select **Settings**.
3. In the left sidebar, select **Pages** under **Code and automation**.
4. Under **Build and deployment**, set **Source** to **Deploy from a branch**.
5. Select the `main` branch and the `/(root)` folder.
6. Select **Save**.

GitHub will start the first Pages deployment. Its status appears on the
repository's **Actions** tab. Wait for the deployment to finish successfully
before testing the public URLs.

### 4. Confirm the custom domain

Return to **Settings > Pages**. Under **Custom domain**, confirm that the value
is exactly:

```text
aligner-tracker.alecbytes.com
```

If the field is empty, enter that value and select **Save**. Do not include
`https://`, a path, or a trailing slash.

The matching `CNAME` file is committed in the repository, and the matching DNS
record already points to `alecbytes.github.io`, so no DNS edit should be needed.

### 5. Enable HTTPS

In **Settings > Pages**, enable **Enforce HTTPS**. GitHub may need time to issue
the first certificate; according to GitHub, the option can take up to 24 hours
to become available after configuring a custom domain.

Do not enter the URLs in App Store Connect until all three pages load directly
over HTTPS without a certificate warning.

## Verify the deployment

Open these URLs in a private browser window and on an iPhone:

```text
https://aligner-tracker.alecbytes.com/
https://aligner-tracker.alecbytes.com/support/
https://aligner-tracker.alecbytes.com/privacy/
```

Confirm that:

- each URL loads without authentication or a certificate warning;
- Support and Privacy link to one another;
- the support email opens a message to `support@alecbytes.com`;
- the pages remain readable at phone width and in light and dark appearance;
- disabling JavaScript does not affect the site; and
- reloading `/support/` and `/privacy/` directly does not return a 404.

Optional command-line verification:

```sh
curl --fail --head https://aligner-tracker.alecbytes.com/
curl --fail --head https://aligner-tracker.alecbytes.com/support/
curl --fail --head https://aligner-tracker.alecbytes.com/privacy/
```

Each command should report a successful `2xx` status.

## App Store Connect

After the privacy wording has been reviewed against the final production
archive and the public pages pass verification, use:

- **Support URL:** `https://aligner-tracker.alecbytes.com/support/`
- **Privacy Policy URL:** `https://aligner-tracker.alecbytes.com/privacy/`
- **Marketing URL:** leave blank for version 1.0

## Recommended domain security

GitHub recommends verifying the domain at the account level to prevent another
GitHub user from claiming it for Pages. In the `AlecBytes` GitHub account:

1. Open account **Settings > Pages**.
2. Add `alecbytes.com` as a verified domain.
3. Copy the TXT record GitHub provides into the domain's DNS settings.
4. Leave the TXT record in place after verification.

Verifying the apex domain protects its subdomains, including
`aligner-tracker.alecbytes.com`.

## Troubleshooting

### The site still shows GitHub's 404 page

- Confirm that the initial push succeeded and the files appear on `main`.
- Confirm **Settings > Pages** uses `main` and `/(root)`.
- Check the **Actions** tab for a failed Pages deployment.
- Wait a few minutes after a successful first deployment, then try a private
  browser window.

### The default GitHub Pages URL works but the custom domain does not

- Confirm the Pages custom-domain field and repository `CNAME` both contain
  `aligner-tracker.alecbytes.com`.
- Confirm the DNS CNAME still points directly to `alecbytes.github.io`.
- Allow up to 24 hours for a recent DNS change to propagate.

### Enforce HTTPS is unavailable

- Confirm the custom-domain DNS check passes in **Settings > Pages**.
- Wait for GitHub to provision the certificate, which can take up to 24 hours.
- Do not delete and repeatedly recreate the custom-domain setting while the
  certificate is being provisioned.

## Publishing later updates

1. Edit and review the site locally.
2. Update the displayed effective/last-updated date when policy content changes
   materially.
3. Commit the changes.
4. Run `git push`.
5. Wait for the Pages deployment to pass, then verify the affected public URLs.

Keep `/support/` and `/privacy/` stable. If either page ever moves, retain a
redirect from its existing URL.
