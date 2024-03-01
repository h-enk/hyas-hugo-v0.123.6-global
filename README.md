# hyas-hugo-v0.123.6-global

Hugo v0.123.6 breaks build. 

Module mounts behavior of the `assets` directory changed with Hugo v0.123.0 and later.

Known inpact: all [Doks](https://github.com/gethyas/doks) and [Hyas](https://github.com/gethyas/hyas) users.

## Replicate

Clone repository

```bash
git clone https://github.com/h-enk/hyas-hugo-v0.123.6-global.git
```

Install dependencies

```bash
cd hyas-hugo-v0.123.6-global && npm install
```

Run development server

```bash
hugo server
```

## Module mounts (default settings)

`config/_default/module.toml`

```toml
## assets
[[mounts]]
  source = "node_modules/@hyas/core/assets"
  target = "assets"

[[mounts]]
  source = "assets"
  target = "assets"
```

Result: NOK

```bash
execute of template failed: template: partials/head/libsass.html:9:36: executing "partials/head/libsass.html" at <$css.Permalink>: error calling Permalink: operation not supported on directory ""
```

## Module mounts (temporary fix)

`config/_default/module.toml`

```toml
## assets
[[mounts]]
  source = "node_modules/@hyas/core/assets"
  target = "assets"
  excludeFiles = ["scss/app.scss"]

[[mounts]]
  source = "assets"
  target = "assets"
```

Result: OK

## Resources

- [hyas-hugo-v0.122.0](https://github.com/h-enk/hyas-hugo-v0.122.0)
- [hyas-hugo-v0.123.6](https://github.com/h-enk/hyas-hugo-v0.123.6)
- [hyas-hugo-v0.123.6-global](https://github.com/h-enk/hyas-hugo-v0.123.6-global)
