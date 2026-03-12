# halden-city

Static site for Halden City.

## Deploy with GitHub Actions (GitHub Pages)

This repository is configured to deploy `index.html` to GitHub Pages automatically on every push to `main`.

### One-time setup in GitHub

1. Go to **Settings → Pages** in this repository.
2. Under **Build and deployment**, set **Source** to **GitHub Actions**.

After that, each push to `main` will trigger the deployment workflow.

## Custom Domain

This project is configured to use `haldencity.com` via the `CNAME` file.

### DNS records to add

At your DNS provider, configure:

- `A` record for `@` → `185.199.108.153`
- `A` record for `@` → `185.199.109.153`
- `A` record for `@` → `185.199.110.153`
- `A` record for `@` → `185.199.111.153`
- `CNAME` record for `www` → `triursa.github.io`

### GitHub Pages settings

1. Go to **Settings → Pages**.
2. Set **Custom domain** to `haldencity.com`.
3. Enable **Enforce HTTPS** (once DNS has propagated and certificate is issued).

### DNS verification checklist

Run these commands locally to verify DNS propagation:

- `dig +short haldencity.com A`
	- Expected: the four GitHub Pages IPs (`185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`) in any order.
- `dig +short www.haldencity.com CNAME`
	- Expected: `triursa.github.io.`
- `nslookup haldencity.com`
	- Expected: answer section includes the same `185.199.108.153/109.153/110.153/111.153` addresses.
- `nslookup www.haldencity.com`
	- Expected: canonical name resolves to `triursa.github.io`.

Once DNS is correct:

1. Re-open **Settings → Pages** and confirm the custom domain is still `haldencity.com`.
2. Wait for certificate provisioning (can take several minutes to a few hours).
3. Enable **Enforce HTTPS**.