# Solid on Sapper

## Process

- npx degit "sveltejs/sapper-template#rollup" solid-box
- cd solid-box
- npm install @inrupt/solid-client
- npm run dev

In the browser console (on http://localhost:3000), I got `require is not defined` related to `solid-client`:

```js
const fetch = (resource, init) => {
  let fetch;
  try {
    fetch = require("solid-auth-client").fetch;
  } catch (e) {
    fetch = require("cross-fetch"); // <- Because of this.
  }
  return fetch(resource, init);
};
```

I tried to configure rollup with:

```js
commonjs({
  transformMixedEsModules: true,
});
```

But it didn't work.
