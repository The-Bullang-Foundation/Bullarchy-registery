# Bullarchy Registry

The official package registry for the [Bullang](https://github.com/The-Bullang-Foundation/Bullang) ecosystem.

Packages listed here are installable via:

```
add <name>
add <name>@<version>
```

from within [Bullarchy](https://github.com/The-Bullang-Foundation/Bullarchy) or [Bullarchy-gui](https://github.com/The-Bullang-Foundation/Bullarchy-gui).

---

## Registry format

All packages are listed in [`registry.json`](./registry.json) as a flat JSON object:

```json
{
  "package-name": {
    "description": "A short description shown in the package list.",
    "version":     "v1.0.0",
    "git":         "https://github.com/The-Bullang-Foundation/bull-package-name"
  }
}
```

| Field         | Required | Description                                               |
|---------------|----------|-----------------------------------------------------------|
| `description` | yes      | One-line description shown when the user runs `add`       |
| `version`     | yes      | Latest stable release tag (must match a git tag exactly)  |
| `git`         | yes      | HTTPS URL of the package git repository                   |

---

## Publishing a package

1. **Create a public git repository** containing your Bullang package — a folder of `.bu` source files with an `inventory.bu` at the root.

2. **Tag a release** using semantic versioning:
   ```bash
   git tag v1.0.0
   git push origin v1.0.0
   ```

3. **Open a pull request** to this repository adding your entry to `registry.json`:
   ```json
   "your-package": {
     "description": "What your package does.",
     "version":     "v1.0.0",
     "git":         "https://github.com/your-org/your-package"
   }
   ```

4. Once merged, your package is immediately available to all Bullarchy users.

---

## Package prerequisites

If your package depends on external system tools (e.g. `ssh`, `curl`, `nmap`), list them clearly in your package's own `README.md`. Bullarchy does not install system tools — users are responsible for installing prerequisites themselves.

---

## Versioning

Packages follow [Semantic Versioning](https://semver.org): `vMAJOR.MINOR.PATCH`.

- `MAJOR` — breaking changes to the public bullet interface
- `MINOR` — new bullets, backwards compatible
- `PATCH` — bug fixes

Users can pin to a specific version with `add <name>@<version>`. If no version is specified, the latest tagged release is installed.
