# ezwup

Terminal-style CTF writeup generator. Single HTML file, no dependencies, no API.

Fill in your recon, exploits, privesc and flags — ezwup formats everything into clean markdown. Missing fields are marked as `[TODO]`. Export as `.md` or copy to clipboard.

## Features

- Machine info, enumeration, web enum, exploitation, privesc, flags, lessons learned
- Live markdown preview (collapsible)
- Commands and outputs auto-wrapped in code blocks
- Missing fields marked as `[TODO]`
- Export as `.md` file
- Copy to clipboard
- All data persisted in `localStorage`

## Usage

Just open `ezwup.html` in a browser. No build step, no install.

## Nginx (port 1337)

```nginx
server {
    listen 1337;
    server_name _;

    root /opt/ezwup/frontend;
    index index.html;

    access_log /var/log/ezwup/access.log;
    error_log  /var/log/ezwup/error.log;

    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

```bash
sudo mkdir -p /opt/ezwup/frontend /var/log/ezwup
sudo cp ezwup.html /opt/ezwup/frontend/index.html
sudo chown -R www-data:www-data /opt/ezwup /var/log/ezwup
sudo ln -s /etc/nginx/sites-available/ezwup /etc/nginx/sites-enabled/
sudo nginx -t && sudo systemctl reload nginx
```
