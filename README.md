# Mini QR

[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

An app to create beautiful QR codes and scan various QR code types.

<div style="display:flex; flex-direction:row; flex-wrap:wrap; justify-content:center; gap:8px;">
    <a href="https://esteetey.dev"><img width="100" src="public/presets/lyqht.svg" /></a>
    <a href="https://www.padlet.com"><img width="100" src="public/presets/padlet.svg" /></a>
    <a href="https://www.uilicious.com">
    <img width="100" src="public/presets/uilicious.svg" />
    </a>
    <a href="https://www.supabase.com"><img width="100" src="public/presets/supabase-green.svg" /></a>
    <a href="https://www.vercel.com"><img width="100" src="public/presets/vercel-dark.svg" /></a>
    <a href="https://viteconf.org/"><img width="100" src="public/presets/viteconf2023.svg" /></a>
</div>

## Features

- ✅ Accessible: minimally WCAG A compliant
- 🎨 Customizable colors and styles
- 🖼️ Export to PNG, JPG & SVG
- 📋 Copy to clipboard
- 🌓 Light/dark/system-preference mode toggle
- 🎲 Randomize style button
- 🌐 Available in 30+ languages
- 💾 Save & Load QR Code config
- 🖼️ Upload custom image for logo
- 🎭 Presets: Pre-crafted QR code styles
- 🖌️ Frame customization: Add text labels and style the frame around your QR code
- 🛡️ Error correction level: affects the size of the QR code and logo within. Use lower correction levels for bigger pieces of data to ensure that it can be read.
- 📱 QR Code Scanner: Scan QR codes using your camera or by uploading images, with intelligent detection for URLs, emails, phone numbers, WiFi credentials, and more
- 📦 Batch data export: Import a CSV file with multiple data strings and export QR codes for them all at once.
- 📲 PWA Support: Install MiniQR as a desktop or mobile app
- 📝 Data templates: Support for various data types including text, URLs, emails, phone numbers, SMS, WiFi credentials, vCards, locations, and calendar events

### Installation as PWA

<details>
<summary>MiniQR can also be installed as a Progressive Web App (PWA) on your device</summary>

1. **Desktop (Chrome/Edge)**:

   - Visit [mini-qr.vercel.app](https://mini-qr.vercel.app)
   - Click the install icon (➕) in the address bar
   - Click "Install" in the prompt

2. **Mobile (Android)**:

   - Visit [mini-qr.vercel.app](https://mini-qr.vercel.app)
   - Tap the "Add to Home Screen" option in your browser menu
   - Tap "Install" or "Add"

3. **iOS (Safari)**:
   - Visit [mini-qr.vercel.app](https://mini-qr.vercel.app)
   - Tap the Share button
   - Scroll down and tap "Add to Home Screen"
   - Tap "Add"

Once installed, MiniQR will work offline and provide a native app-like experience.

</details>

## Demo

Try it out [here](https://mini-qr.vercel.app/) ✨

<details>

<summary>Frame text included in batch export (added in v0.17.0)</summary>

https://github.com/user-attachments/assets/c6db8fd5-ec36-43be-b6e3-a42e1b7dc3cb

</details>

<details>
<summary>Data templates (added in v0.16.0)</summary>

https://github.com/user-attachments/assets/863f9330-2645-4d23-88aa-04f5f5beaa67

</details>

<details>
<summary>Basic frame settings (added in v0.15.0)</summary>

https://github.com/user-attachments/assets/e160d60d-3c7f-4bbb-908c-efd11fec20e8

</details>

<details>
<summary>Scanning QR code (added in v0.13.0)</summary>

https://github.com/user-attachments/assets/5ad58b35-0a16-43a4-839a-e2197bfc273a

</details>

<details>
<summary>Batch data export (added in v0.9.0)</summary>

https://github.com/user-attachments/assets/fef17e6a-c226-4136-9501-8d3e951671e0

</details>

<details>

<summary>MVP - presets, languages, dark/light mode (v0.3.0)</summary>

https://github.com/lyqht/mini-qr/assets/35736525/991b2d7e-f168-4354-9091-1678d2c1bddb

</details>

## Self-hosting with Docker 🐋

Mini-QR can easily be self-hosted using Docker. We provide a [docker-compose.yml](docker-compose.yml) file and a production-ready multi-stage [Dockerfile](Dockerfile).

### Quick Start (using prebuilt image)

```bash
wget https://github.com/lyqht/mini-qr/raw/main/docker-compose.yml

docker compose up -d
```

This will pull the latest production image from GitHub Container Registry and start the app at [http://localhost:8081](http://localhost:8081).

### Build and run locally (for development or custom builds)

```bash
docker compose up -d --build
```

Or build and run manually:

```bash
docker build -t mini-qr .
docker run -d -p 8081:8080 mini-qr
```

### Customization

#### Environment Variables

| Variable                      | Description                                                                        | Default   |
| ----------------------------- | ---------------------------------------------------------------------------------- | --------- |
| `BASE_PATH`                   | Base path for deployment                                                           | `/`       |
| `VITE_HIDE_CREDITS`           | Set to `"true"` to hide credits in the footer                                      | `"false"` |
| `VITE_DEFAULT_PRESET`         | Name of the default QR code preset to load (e.g., `"lyqht"`)                       | `""`      |
| `VITE_DEFAULT_DATA_TO_ENCODE` | Default data to encode when the app first loads                                    | `""`      |
| `VITE_QR_CODE_PRESETS`        | JSON string defining custom QR code presets. E.g., `'[{"name":"c1","data":"hi"}]'` | `"[]"`    |
| `VITE_FRAME_PRESET`           | Name of the default frame preset to load (e.g., `"default"`)                       | `""`      |
| `VITE_FRAME_PRESETS`          | JSON string defining custom frame presets. E.g., `'[{"name":"fA","text":"QR"}]'`   | `"[]"`    |
| `VITE_DISABLE_LOCAL_STORAGE`  | Set to `"true"` to disable loading saved settings from local storage on startup    | `"false"` |

### Docker configuration

- You can edit `nginx.conf` or mount your own static files by uncommenting the `volumes` section in `docker-compose.yml`.
- The production image uses Nginx for optimal static file serving.
- The `.dockerignore` file is included for smaller, faster builds.
- Set `BASE_PATH=/your-path` to deploy the app under a subdirectory (e.g., for hosting at `domain.com/your-path`).
- If you want to have a default preset to be fixed, you should set `VITE_DISABLE_LOCAL_STORAGE=true`

#### Examples

Deploy at root path (default):

```bash
docker compose up -d
```

Deploy at subdirectory `/mini-qr`:

```bash
BASE_PATH=/mini-qr docker compose up -d
```

For custom builds with specific BASE_PATH:

```bash
docker build --build-arg BASE_PATH=/mini-qr -t mini-qr .
docker run -d -p 8081:8080 mini-qr
```

## Contributing

[![All Contributors](https://img.shields.io/github/all-contributors/lyqht/mini-qr?color=ee8449&style=flat-square)](#contributors) [![Crowdin](https://badges.crowdin.net/miniqr/localized.svg)](https://crowdin.com/project/miniqr)

Translations and bug fixes are welcome!

> [!NOTE]
> For other issues, please create an issue/ raise it on the discussion board before working on them, as they may be rejected if they are not aligned with @lyqht's goals for this project.

See [CONTRIBUTING.md](CONTRIBUTING.md) for more details.

## Contributors

Thank you for everyone here for taking their time out to improve MiniQR 🧡

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->


<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->
