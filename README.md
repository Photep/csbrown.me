# csbrown.me

Public personal one-pager for Christopher Brown. Static HTML and CSS only.

## Deploy

GitHub Actions copies `index.html` and `styles.css` into `./public` and runs `wrangler deploy` on push to `main` and on pull requests. Cloudflare Workers serves that folder as static assets. There is no Worker script.

Required GitHub Actions secrets:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

Deploy will fail until those secrets exist. That is expected.
