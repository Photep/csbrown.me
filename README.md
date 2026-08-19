# csbrown.me

Public personal one-pager for Christopher Brown. Static HTML and CSS only.

## Workers

Two Cloudflare Workers serve the same static assets from `./public`:

| Environment | Worker name | URL | How it deploys |
| --- | --- | --- | --- |
| test | `csbrown-me` | https://csbrown-me.csbrown.workers.dev | Automatic on push to `main` and on pull requests |
| production | `csbrown-me-prod` | csbrown.me | Manual promote only |

There is no Worker script. Production is a separate worker so a promote can succeed before the csbrown.me zone is attached. `main` never deploys to production automatically. Production custom domains are csbrown.me and www.csbrown.me via wrangler `custom_domain`.

## Deploy

GitHub Actions copies `index.html` and `styles.css` into `./public`.

- **Test:** `wrangler deploy` with no `--env`. That publishes worker `csbrown-me` and keeps https://csbrown-me.csbrown.workers.dev as the live test URL.
- **Production:** Actions → Deploy → Run workflow (**Promote to production**). That job runs `wrangler deploy --env production` only and publishes worker `csbrown-me-prod`. It does not run on push or pull request.

Required GitHub Actions secrets:

- `CLOUDFLARE_API_TOKEN`
- `CLOUDFLARE_ACCOUNT_ID`

Deploy will fail until those secrets exist. That is expected.
