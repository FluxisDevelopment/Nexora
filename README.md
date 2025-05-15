# Nexora

**Nexora** is an open-source, high-performance client area for the Pterodactyl Panel, developed and maintained by the Fluxis team. Built for simplicity and speed, Nexora empowers your users to create, manage, monitor, and upgrade game servers through a sleek, modern interface.

---

## 🚀 Key Features

- **Intuitive Dashboard**: Streamlined server creation, status overview, and management controls.
- **Real-Time Monitoring**: Live CPU, memory, disk, and network usage graphs.
- **One-Click Operations**: Start, stop, restart, reinstall, and backup servers instantly.
- **Theming Support**: Choose dark, light, or custom themes via `config.toml`.
- **Plugin Architecture**: Extend functionality with community-driven modules.
- **Localization**: Multi-language support with easy JSON-based translations.
- **Responsive Layout**: Optimized for desktops, tablets, and mobile devices.
- **Webhook & API Integrations**: Connect billing, notifications, and automations seamlessly.
- **Security Best Practices**: JWT authentication, CSRF protection, and strict CSP by default.

---

## 📦 Prerequisites

Ensure your environment meets these requirements before installing Nexora:

- **Node.js** v16+ and **npm** v8+ (or **yarn**)
- A running **Pterodactyl Panel** (v1.12 or newer)
- SSL certificate for HTTPS (Let's Encrypt, Cloudflare, etc.)
- Modern web browser (Chrome, Firefox, Edge, Safari)

---

## ⚙️ Installation & Setup

1. **Clone the Repo**
   ```bash
   git clone https://github.com/fluxis/nexora.git
   cd nexora
````

2. **Install Dependencies**

   ```bash
   npm install
   # or yarn install
   ```

3. **Configure Nexora**

   * Duplicate the example config:

     ```bash
     cp config.example.toml config.toml
     ```
   * Edit `config.toml` with your settings:

     ```toml
     [app]
     name = "Nexora"
     panel_url = "https://panel.yourdomain.com"
     theme = "dark"

     [auth]
     jwt_secret = "YOUR_JWT_SECRET"
     ```

4. **SSL & Reverse Proxy**

   * Sample NGINX config:

     ```nginx
     server {
       listen 80;
       server_name client.yourdomain.com;
       return 301 https://$host$request_uri;
     }

     server {
       listen 443 ssl;
       server_name client.yourdomain.com;

       ssl_certificate /etc/letsencrypt/live/yourdomain.com/fullchain.pem;
       ssl_certificate_key /etc/letsencrypt/live/yourdomain.com/privkey.pem;

       location / {
         proxy_pass http://localhost:3000;
         proxy_set_header Host $host;
         proxy_set_header X-Real-IP $remote_addr;
       }
     }
     ```

5. **Start Nexora**

   ```bash
   npm run start
   # or yarn start
   ```

6. **Access Client Area**
   Open `https://client.yourdomain.com` in your browser.

---

## 🎨 Theming & Customization

Customize Nexora’s look with built‑in and custom themes:

1. **Default Themes**: `light`, `dark`.

2. **Custom Theme**:

   * Define CSS variables in `src/styles/theme.css`:

     ```css
     :root {
       --background: #121212;
       --accent: #00d8ff;
       --text: #e0e0e0;
     }
     ```
   * Activate in `config.toml`:

     ```toml
     theme = "custom"
     ```

3. **Branding Assets**:

   * Swap `/public/assets/logo.svg`, `/public/assets/favicon.ico`, and `/public/assets/showcase.png`.

---

## 🖼️ Screenshots Gallery

![Server List](https://your-cdn.com/nexora-gallery-1.png)
*Server overview with status indicators and quick actions.*

![Server Details](https://your-cdn.com/nexora-gallery-2.png)
*Detailed server view with console, file manager, and settings.*

![Usage Charts](https://your-cdn.com/nexora-gallery-3.png)
*Interactive CPU, memory, and network graphs.*

![User Settings](https://your-cdn.com/nexora-gallery-4.png)
*Account preferences and profile management.*

---

## 🔧 Troubleshooting

* **Startup Errors**: Verify `config.toml` syntax and environment variables.
* **CORS Denied**: Ensure `panel_url` in config matches the Pterodactyl Panel URL.
* **Missing Media**: Confirm assets exist under `/public/assets/`.
* **Auth Failures**: Regenerate `jwt_secret` and restart the application.

---

## 🤝 Contributing

Nexora thrives thanks to community contributions. To get involved:

1. Fork the repository and create a branch:

   ```bash
   git checkout -b feature/awesome-addition
   ```
2. Implement your changes, add relevant tests, and run linting.
3. Open a Pull Request with a clear description.

Read our [CONTRIBUTING.md](CONTRIBUTING.md) for detailed guidelines.

---

## 📅 Roadmap

* [ ] Plugin Marketplace
* [ ] Billing Integrations (Stripe, PayPal)
* [ ] Automated Backups & Snapshots
* [ ] Role-Based Access Control
* [ ] Dynamic Theme Switcher

---

## 📜 License

Nexora is licensed under MIT. See the [LICENSE](LICENSE) file for details.

---

*Made with ❤️ by Fluxis*
