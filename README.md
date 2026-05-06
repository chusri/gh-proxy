# gh-proxy

A lightweight HTTP proxy for GitHub files and web content, built with Go and Gin.

## Features

- **Download** files from GitHub repositories
- **Show** any remote URL content
- **Blog** proxy with automatic URL rewriting for fully rendered pages

## Endpoints

### `GET /download/<owner>/<repo>/...`

Proxy download files from GitHub.

```
/download/plutonyx/gh-proxy/releases/download/v0.0.4/gh-proxy-linux-amd64
```

### `GET /show/<url>`

Fetch and return raw content from any URL.

```
/show/https://example.com/data.json
```

### `GET /blog/<url>`

Proxy a web page with all assets rewritten so it renders correctly. Ideal for GitHub Pages blogs and static sites.

```
/blog/https://karpathy.github.io/2026/02/12/microgpt/
```

HTML `src`/`href` attributes and CSS `url()` references pointing to the same origin are rewritten through the proxy. Cross-origin resources are left untouched.

### `GET /install.sh`

Returns the install script.

## Install

```sh
curl -sSL <your-host>/install.sh | sh
```

Or specify a custom directory:

```sh
curl -sSL <your-host>/install.sh | INSTALL_DIR=~/.local/bin sh
```

## Run

```sh
gh-proxy
```

Listens on `:8080` by default. Set `ENV=dev` to enable Gin debug mode.

## Docker

```sh
docker build -t gh-proxy .
docker run -p 8080:8080 gh-proxy
```

## Build from source

```sh
make build
```

Cross-compile for all platforms:

```sh
make release
```

## License

MIT
