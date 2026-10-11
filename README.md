# nuxt-cloudinary-257-modern

Check of [nuxt-modules/cloudinary#257](https://github.com/nuxt-modules/cloudinary/issues/257) on the current stack:
the [current Nuxt v4 starter](https://github.com/nuxt/starter/tree/b7d8f8f8c952bd5a49d10126fc3c5285906b7ac8)
with `@nuxtjs/cloudinary` in `modules` and a `<CldImage>` on the page, TypeScript installed.

| Branch             | `@nuxtjs/cloudinary` | Result of `npm run dev`, `GET /`                     |
|--------------------|----------------------|------------------------------------------------------|
| `main`             | 4.1.0                | 200, `<CldImage>` rendered                           |
| `cloudinary-4.0.0` | 4.0.0                | 200, `<CldImage>` rendered                           |

Stack: Nuxt 4.6.1, Vue 3.5.43, Vite 8.3.4, TypeScript 5.9.3. `npm run build` also succeeds on `main`.

## Run

- StackBlitz, `main`: https://stackblitz.com/github/Jorgagu/nuxt-cloudinary-257-modern
- StackBlitz, `cloudinary-4.0.0`: https://stackblitz.com/github/Jorgagu/nuxt-cloudinary-257-modern/tree/cloudinary-4.0.0
- Locally: `npm install && npm run dev`, then open http://localhost:3000

## Why 4.0.0 also works here

The error came from `@vue/compiler-sfc` failing to resolve `ImageOptions`, whose declarations live in the
`.d.cts` file of `@cloudinary-util/url-loader`. Resolution of `.mts/.cts` files was added in
[vuejs/core#14402](https://github.com/vuejs/core/pull/14402), released in Vue 3.5.28. On older Vue versions,
4.1.0 is the fix: see [nuxt-cloudinary-257-repro](https://github.com/Jorgagu/nuxt-cloudinary-257-repro).
