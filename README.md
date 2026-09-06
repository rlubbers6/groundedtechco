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

## DNS setup in Cloudflare

The domain is registered at Cloudflare; the site is hosted by GitHub Pages.
In the Cloudflare dashboard, under **DNS → Records**, add:

| Type  | Name | Content                 | Proxy    |
|-------|------|-------------------------|----------|
| A     | @    | 185.199.108.153         | DNS only |
| A     | @    | 185.199.109.153         | DNS only |
| A     | @    | 185.199.110.153         | DNS only |
| A     | @    | 185.199.111.153         | DNS only |
| CNAME | www  | rlubbers6.github.io     | DNS only |

**Set the proxy to DNS only (grey cloud), not proxied (orange cloud).** GitHub
issues the TLS certificate itself, and it cannot complete that challenge while
Cloudflare is terminating the connection. Leaving the orange cloud on is the
usual reason a custom domain sits stuck on "certificate provisioning".

If you later want Cloudflare's proxy in front, turn it on only after the
certificate has issued, and set **SSL/TLS → Overview** to **Full**. Leaving it
on *Flexible* causes an infinite redirect loop with GitHub Pages.

Then in the GitHub repo: **Settings → Pages → Custom domain** should already
read `groundedtechco.com` from the `CNAME` file. Tick **Enforce HTTPS** once
the certificate has issued — usually within an hour, sometimes minutes.

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
