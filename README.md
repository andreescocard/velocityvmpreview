<div align="center">

# ⚡ Velocity VM Preview

[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![No build step](https://img.shields.io/badge/build-none-brightgreen.svg)](#quick-start)
[![Single file app](https://img.shields.io/badge/app-single--file-lightgrey.svg)](index.html)
[![Buy Me a Coffee](https://img.shields.io/badge/Buy%20Me%20a%20Coffee-support-FFDD00?logo=buymeacoffee&logoColor=000)](https://buymeacoffee.com/andreescocard)

**Preview, test, and review Apache Velocity `.vm` templates — directly in the browser.**

No backend. No build step. One HTML file.

[Quick Start](#quick-start) · [Features](#features) · [Usage](#usage) · [AI Assistant](#ai-assistant) · [Roadmap](#roadmap)

</div>

---

Paste a template, provide a JSON context, render the output, and inspect both the generated HTML and the visual preview side by side.

Built for **SAP Commerce Cloud** teams working with email templates, CMS fragments, personalization logic, and other Velocity-backed content.

---

## ✨ Features

| Area | What you can do |
|------|-----------------|
| 🖼️ Template preview | Render Velocity templates locally in the browser |
| 📦 JSON context | Edit and validate the data model used by the template |
| 🔍 Output review | Compare generated HTML with the rendered iframe preview |
| 📚 Examples | Load practical examples for orders, products, segmentation, and password reset |
| 📤 Import / Export | Export `.vm`, `.json`, and rendered `.html`; import template and context files |
| 🤖 AI support | Use OpenRouter to generate context data or review template quality |
| ⚙️ Zero setup | Run as a single HTML file — no backend, no build pipeline |

---

## 🚀 Quick Start

```bash
git clone https://github.com/andreescocard/velocityvmpreview.git
cd velocityvmpreview
```

**Open directly:**
```bash
start index.html
```

**Or serve locally:**
```bash
npx http-server .
# → http://localhost:8080
```

```bash
python -m http.server 8000
# → http://localhost:8000
```

> **Note:** The app loads Bootstrap, Bootstrap Icons, and VelocityJS from CDNs. Internet access required unless those are vendored locally.

---

## 📖 Usage

1. Paste a Velocity template in the template editor
2. Add the matching JSON context in the context editor
3. Click **Render**
4. Review the generated HTML and iframe preview
5. Export the template, context, or generated HTML when needed
6. Optionally use the AI assistant to generate context or review the template

**Example template:**

```velocity
<h1>Hello, $customer.firstName!</h1>

#if($customer.isPremium)
  <p>You are a premium customer.</p>
#else
  <p>Join the loyalty program to unlock premium benefits.</p>
#end
```

**Example context:**

```json
{
  "customer": {
    "firstName": "Sarah",
    "isPremium": true
  }
}
```

---

## 🏢 SAP Commerce Cloud

SAP Commerce Cloud projects use Velocity templates for generated content. This tool lets teams test and review those templates without deploying to a commerce environment.

**Common uses:**

- Order confirmation, password reset, shipment, and abandoned cart emails
- CMS or storefront fragments that depend on dynamic context data
- Personalized content based on segment, cart state, stock status, or promotion
- Developer onboarding and chapter demos for Velocity syntax
- Visual code review for template changes before deployment

<details>
<summary><strong>Example: Order Confirmation</strong></summary>

```velocity
<h1>Order Confirmed</h1>

<p>Hello $customer.firstName $customer.lastName,</p>
<p>Your order <strong>#$order.code</strong> has been confirmed.</p>

<h2>Order Summary</h2>

#foreach($entry in $order.entries)
  <div class="item">
    <strong>$entry.product.name</strong><br>
    Quantity: $entry.quantity<br>
    Subtotal: $$entry.totalPrice
  </div>
#end

<p><strong>Total:</strong> $$order.totalPrice</p>
```

```json
{
  "customer": {
    "firstName": "Sarah",
    "lastName": "Johnson"
  },
  "order": {
    "code": "00001234",
    "totalPrice": "349.97",
    "entries": [
      {
        "product": { "name": "Premium Wireless Headphones" },
        "quantity": 1,
        "totalPrice": "299.99"
      }
    ]
  }
}
```

</details>

---

## 🤖 AI Assistant

OpenRouter integration is optional. When an API key is configured, the assistant can:

- Generate JSON context from variables found in a template
- Suggest readability and structure improvements
- Flag likely syntax problems
- Highlight security concerns such as unsafe HTML injection
- Provide SAP Commerce-oriented review notes

> The API key is kept in browser memory for the current session only — never written to disk.

---

## 🔒 Security Notes

- Template output rendered in a **sandboxed iframe**
- AI insight output displayed as text, not injected as HTML
- Dynamic alert values escaped before insertion into Bootstrap alert markup
- Intended for **local preview and developer workflows**, not as a hosted public execution service

---

## 🛠️ Tech Stack

| Dependency | Purpose |
|------------|---------|
| [VelocityJS](https://github.com/shepherdwind/velocity.js) | Velocity parsing and rendering |
| [Bootstrap 5.3](https://getbootstrap.com/) | Layout and UI components |
| [Bootstrap Icons](https://icons.getbootstrap.com/) | Interface icons |
| Vanilla JavaScript | Application logic |
| [OpenRouter](https://openrouter.ai/) | Optional AI-assisted context and review |

---

## 📁 Project Structure

```text
.
├── index.html       # Complete single-file application
├── README.md        # Project documentation
├── LICENSE          # MIT license
├── .gitignore       # Local ignore rules
├── .editorconfig    # Shared editor defaults
├── .gitattributes   # Text normalization
└── tasks/           # Local task notes and scratch work (git-ignored)
```

---

## 🗺️ Roadmap

- [ ] Template library with save and load support
- [ ] Shareable links with compressed template and context data
- [ ] Local template history
- [ ] Syntax highlighting for Velocity and JSON editors
- [ ] Light and dark themes
- [ ] SAP Commerce impex import helpers
- [ ] Automated browser smoke tests

---

## 🤝 Contributing

1. Fork the repository
2. Create a focused feature branch
3. Test the app in a browser
4. Update this README when behavior or setup changes
5. Open a pull request with a concise description and screenshots when useful

Keep it simple: **no backend, no required build step, no heavy framework.**

---

## 📄 License

Licensed under the [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- [Apache Velocity](https://velocity.apache.org/)
- [VelocityJS](https://github.com/shepherdwind/velocity.js)
- [Bootstrap](https://getbootstrap.com/)
- [OpenRouter](https://openrouter.ai/)
