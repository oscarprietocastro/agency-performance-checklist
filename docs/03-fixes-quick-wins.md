# 03 - Quick Wins

High-impact, low-effort fixes that can be applied quickly.

## Images

- [ ] Compress all images with lossy compression (mozjpeg, oxipng, squoosh)
- [ ] Convert to WebP or AVIF
- [ ] Add `width` and `height` attributes to all `<img>` tags (prevents CLS)
- [ ] Add `loading="lazy"` to below-the-fold images
- [ ] Add `fetchpriority="high"` to the LCP image
- [ ] Use `srcset` for responsive images

## Fonts

- [ ] Add `font-display: swap` or `optional` to all @font-face rules
- [ ] Preload the most critical font file
- [ ] Subset fonts to remove unused characters
- [ ] Self-host fonts instead of loading from Google Fonts or Adobe

## JavaScript

- [ ] Defer or async non-critical scripts
- [ ] Remove unused JavaScript (check with Coverage in DevTools)
- [ ] Move third-party scripts to load after user interaction (facade pattern)
- [ ] Enable tree shaking in the build tool

## CSS

- [ ] Inline critical CSS
- [ ] Defer non-critical CSS with `<link rel="preload" as="style">`
- [ ] Remove unused CSS (PurgeCSS, UnCSS)

## Caching

- [ ] Set long `Cache-Control` headers on static assets (`max-age=31536000, immutable`)
- [ ] Enable gzip or Brotli compression on the web server
- [ ] Warm the cache after deploys

## HTTP

- [ ] Enable HTTP/2 or HTTP/3
- [ ] Add `<link rel="preconnect">` for critical third-party origins
- [ ] Add `<link rel="dns-prefetch">` for secondary third-party origins

## Server

- [ ] Enable OPcache (PHP)
- [ ] Increase PHP memory limit if under pressure
- [ ] Enable keep-alive connections on the web server
