# A world of xAI Pan

Blog at https://blog.xaipan.net

Built with [Astro](https://astro.build/), content stored as Markdown in this repo, hosted for free on Cloudflare Pages.

## Write a post

Add a Markdown file in `src/content/blog/`, for example `src/content/blog/my-post.md`:

```md
---
title: 'My post title'
description: 'One sentence about the post.'
pubDate: 'Nov 17 2026'
---

Your post here.
```

Push to `main` and Cloudflare Pages rebuilds and deploys automatically.

## Run locally

```sh
npm install
npm run dev
```

## Build

```sh
npm run build
```

## Deploy

Cloudflare Pages project, connected to `pansue/xaiblog`:

- Framework preset: Astro
- Build command: `npm run build`
- Build output directory: `dist`
- Node version: 22 (see `.nvmrc`)
- Custom domain: `blog.xaipan.net`
