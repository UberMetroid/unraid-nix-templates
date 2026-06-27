# Unraid Nix Templates

This repository serves as the official preset template library for the **[Unraid Nix Plugin](https://github.com/UberMetroid/unraid-nix)**. It stores declarative JSON definitions for deploying over 165+ self-hosted applications natively on Unraid without Docker container or VM overhead.

---

## 📂 Repository Structure

The template registry is split into two directories:
* **`/presets`**: Templates for standard single-process applications (e.g. Radarr, Caddy, Jellyfin).
* **`/presets_composed`**: Multi-process stack templates that run multiple dependent binaries inside a single supervisor environment (e.g. Jellyfin + Caddy).

---

## 🛠️ Template Schema (How to write a template)

All templates are simple, structured JSON files named after their service identifier (e.g., `presets/jellyfin.json`). Below is the standard schema:

```json
{
  "name": "jellyfin",
  "display_name": "Jellyfin",
  "description": "Jellyfin is a Free Software Media System that puts you in control of managing and streaming your media.",
  "url": "https://jellyfin.org/",
  "command": "exec nix run nixpkgs#jellyfin -- --datadir /config",
  "default_ports": [
    {
      "host": 8096,
      "container": 8096,
      "label": "HTTP WebGUI"
    }
  ],
  "icon": "fa-television"
}
```

### Field Descriptions:
* **`name`** *(string, required)*: The unique slug identifier for the service (alphanumeric and dashes only).
* **`display_name`** *(string, required)*: The friendly title shown in the WebGUI store.
* **`description`** *(string, required)*: A short description of the application.
* **`url`** *(string, optional)*: Link to the application's homepage.
* **`command`** *(string, required)*: The launch command. Usually begins with `exec nix run nixpkgs#[package-name]`.
* **`default_ports`** *(array, required)*: Port mappings for the service. Each entry requires a `host` port, a `container` port (inside the chroot namespace), and a friendly descriptive `label`.
* **`icon`** *(string, optional)*: A FontAwesome 4 class name (without the `fa-` prefix, or standard icon name) used to style the store card.

---

## 🔄 Syncing Mechanics

* **Background Sync**: Unraid Nix plugin automatically queries and downloads the latest main zip of this repository in the background every time the Unraid storage array is mounted.
* **Manual Refresh**: You can force an instant refresh of your local template cache by going to the **Settings** subtab of the Nix tab in your Unraid WebGUI and clicking **Force Sync Templates**.

---

## 🤝 Contributing New Templates

We welcome community contributions for new templates!
1. **Fork** this repository.
2. Create a new `.json` file inside the `/presets` directory matching the schema above.
3. Submit a **Pull Request** to the `main` branch.

Alternatively, if you're not comfortable writing JSON, feel free to open a template request on the **[GitHub Issues](https://github.com/UberMetroid/unraid-nix/issues)** page!
