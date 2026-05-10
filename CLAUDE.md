# repository

HA app catalog for hass-cortex. Metadata-only — no Dockerfiles, no `run.sh`, no `rootfs/`.

## Structure

Each top-level subdirectory with a `config.yaml` is an HA app. HA Supervisor auto-discovers them. App source code and build logic live in separate `app-*` source repos (see root `CLAUDE.md`).

```
repository/
├── repository.yaml           # Supervisor catalog metadata
├── .apps.yml                 # repository-updater config (source repo mapping)
├── .github/workflows/
│   └── repository-updater.yaml
├── cortex-stt/               # currently the only stable app
│   ├── config.yaml           # image: ghcr.io/hass-cortex/cortex_stt/{arch}
│   ├── DOCS.md
│   ├── CHANGELOG.md          # auto-generated
│   ├── icon.png
│   ├── logo.png
│   └── translations/en.yaml
```

## Updates

Source repos dispatch `repository_dispatch` events on release; `repository-updater.yaml` runs `hassio-addons/repository-updater@v1` to refresh the catalog.

## DO NOT Edit Manually

Files like `config.yaml` version, `CHANGELOG.md`, and `DOCS.md` are overwritten by the updater. To change an app, edit its **source repo** and cut a new release. To add a new app, add its entry to `.apps.yml` and create its subdirectory here.
