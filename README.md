# next-styled-jsx-pnpm-warning

Minimal reproduction: a Pages Router app that uses `<style jsx>`, installed
with pnpm, gets a Turbopack `Module not found` warning on every `next build`.

## Steps

```sh
pnpm install
pnpm build
```

## Actual

The build succeeds but prints:

```
Turbopack build encountered 1 warning:
./_
Warning: Module not found: Can't resolve 'styled-jsx/style.js'

https://nextjs.org/docs/messages/module-not-found
```

## Expected

No warning. The app doesn't declare `styled-jsx` (it uses the copy that ships
with `next`), and the file is traced correctly anyway:
`.next/server/pages/index.js.nft.json` lists
`node_modules/.pnpm/styled-jsx@5.1.6_react@19.3.0/node_modules/styled-jsx/style.js`.

## Notes

- Installing with npm instead of pnpm: no warning.
- Removing the `<style jsx>` from `pages/_app.js`: no warning.
- Symlinking `node_modules/styled-jsx` to the copy under `node_modules/.pnpm`:
  no warning.
- Reproduces on next 16.2.12, 16.3.2, 16.3.5 and 16.3.8.
