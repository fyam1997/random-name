# random-name

https://fyam1997.github.io/random-name/

## Project Setup

```sh
pnpm install
```

### Compile and Hot-Reload for Development

```sh
pnpm run dev
```

### Compile and Minify for Production

```sh
pnpm run build
```

### Deployment

```sh
pnpm install
pnpm run build
gh-pages -d dist -m "$(git rev-parse HEAD)"
```
