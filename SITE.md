# dtwinscentralfork.app

A static landing page for the DtwinsCentral Wick Editor fork.

## Local preview

Because this is a static site, serve it from the repository root:

```bash
python3 -m http.server 8080
```

Then open <http://localhost:8080>.

## Deployment

The site can be published with GitHub Pages from the `main` branch. Configure the custom domain `dtwinscentralfork.app` in the Pages settings and add the required DNS records at your domain provider.

The site includes a restrictive meta Content Security Policy. For production, configure the equivalent policy as an HTTP response header at the hosting layer.
