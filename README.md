# groundedtechco.com

Static site for Grounded Tech Co. No build step — plain HTML and one stylesheet,
served by GitHub Pages from `main`.

```
index.html                  studio home
gridlock/index.html         app page, doubles as the App Store support URL
gridlock/privacy/index.html privacy policy filed with Apple
assets/                     stylesheet and app icon
CNAME                       custom domain for GitHub Pages
```

## Hosting

Cloudflare Pages, deploying from `main` in this repo. Cloudflare is the
registrar, the DNS, and the host, so there is one dashboard and no records to
wire up by hand.

Push to `main` and Cloudflare rebuilds automatically. There is no build step —
the repo is served as-is.

**Pages project settings**

| Setting                | Value  |
|------------------------|--------|
| Framework preset       | None   |
| Build command          | *empty* |
| Build output directory | `/`    |
| Production branch      | `main` |

The custom domain is attached in **Pages → the project → Custom domains**,
which writes the DNS record itself. No `CNAME` file is needed — that file is a
GitHub Pages mechanism and was removed when this moved to Cloudflare.

GitHub Pages is disabled for this repo. Running both would have the two
services fighting over the same domain.

## Editing

Push to `main`; Pages redeploys in under a minute. To preview locally:

```
python3 -m http.server 8787
```

then open <http://localhost:8787/>. Use a server rather than opening the files
directly — asset paths are absolute and will not resolve over `file://`.

## Email

Every page links `hello@groundedtechco.com`. That address must actually receive
mail before the app is submitted; App Review does sometimes check that a
support contact is reachable. Cloudflare Email Routing forwards a custom-domain
address to an existing inbox for free and is the quickest way to set it up.
