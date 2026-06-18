# Velocity VM Preview

Velocity VM Preview is a lightweight browser tool for testing Apache Velocity
templates without starting a backend service. Paste a `.vm` template, provide a
JSON context, render it, and inspect both the generated HTML and the visual
preview in one place.

It is especially useful for SAP Commerce Cloud teams that need to develop,
review, or explain Velocity-based email templates and storefront fragments.

## Highlights

- Render Velocity templates directly in the browser.
- Validate template output against editable JSON context data.
- Preview generated HTML side by side with rendered output.
- Load practical examples for email, product listing, segmentation, and cart
  recovery scenarios.
- Generate JSON context and template insights with OpenRouter AI integration.
- Run locally with no build step and no application server.

## Tech Stack

- [VelocityJS](https://github.com/shepherdwind/velocity.js) for Velocity parsing
  and rendering.
- [Bootstrap 5.3](https://getbootstrap.com/) for responsive UI components.
- [Bootstrap Icons](https://icons.getbootstrap.com/) for interface icons.
- Vanilla JavaScript for the application logic.
- [OpenRouter](https://openrouter.ai/) for optional AI-assisted context
  generation and review.

## Getting Started

Clone the repository and open `index.html` in a browser:

```bash
git clone https://github.com/andreescocard/velocityvmpreview.git
cd velocityvmpreview
start index.html
```

For development, you can also serve the directory through a local HTTP server:

```bash
npx http-server .
```

Then open:

```text
http://localhost:8080
```

Python is also fine if you already have it installed:

```bash
python -m http.server 8000
```

The app loads Bootstrap, Bootstrap Icons, and VelocityJS from CDNs. Internet
access is required unless those dependencies are vendored locally.

## How It Works

1. Paste or write a Velocity template in the template editor.
2. Add the matching JSON context in the context editor.
3. Click render to generate the final HTML.
4. Review the raw output and rendered preview.
5. Export the template, context, or generated HTML when needed.
6. Optionally use the AI tools to generate missing context or inspect the
   template for issues.

Example template:

```velocity
<h1>Hello, $customer.firstName!</h1>

#if($customer.isPremium)
  <p>You are a premium customer.</p>
#else
  <p>Join the loyalty program to unlock premium benefits.</p>
#end
```

Example context:

```json
{
  "customer": {
    "firstName": "Sarah",
    "isPremium": true
  }
}
```

## SAP Commerce Cloud Use Cases

SAP Commerce Cloud projects commonly use Velocity templates for generated
content. This preview tool helps teams test those templates before deploying
them into a commerce environment.

Common scenarios include:

- Transactional emails such as order confirmation, password reset, shipment
  updates, and abandoned cart reminders.
- CMS and storefront fragments that depend on dynamic context data.
- Personalized content based on customer segment, cart state, stock status, or
  promotion eligibility.
- Developer onboarding and chapter demos for Velocity syntax and SAP Commerce
  email flows.
- Code review sessions where template changes need to be shown visually.

## Example: Order Confirmation Email

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

#if($order.deliveryAddress)
  <h2>Delivery Address</h2>
  <p>
    $order.deliveryAddress.line1<br>
    $order.deliveryAddress.town,
    $order.deliveryAddress.region
    $order.deliveryAddress.postalCode
  </p>
#end
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
        "product": {
          "name": "Premium Wireless Headphones"
        },
        "quantity": 1,
        "totalPrice": "299.99"
      },
      {
        "product": {
          "name": "Smartphone Case"
        },
        "quantity": 2,
        "totalPrice": "49.98"
      }
    ],
    "deliveryAddress": {
      "line1": "123 Main Street",
      "town": "San Francisco",
      "region": "CA",
      "postalCode": "94102"
    }
  }
}
```

## AI Features

The OpenRouter integration is optional. When configured with an API key, it can:

- Generate a complete JSON context from the variables found in a template.
- Suggest improvements for template structure and readability.
- Flag likely syntax issues.
- Highlight security concerns such as unsafe HTML injection.
- Provide SAP Commerce-oriented review notes.

The API key is kept in browser memory for the current session only. It is not
written to disk by this application.

## Project Structure

```text
.
|-- index.html      # Complete single-file application
|-- README.md       # Project documentation
|-- LICENSE         # MIT license
|-- .gitignore      # Local ignore rules
|-- .editorconfig   # Shared editor defaults
|-- .gitattributes  # Text and encoding normalization
`-- tasks/          # Local task notes and scratch work, ignored by Git
```

## Roadmap

- Template library with save and load support.
- Export and import for `.vm` templates and `.json` context files.
- Shareable links with compressed template and context data.
- Template history stored locally in the browser.
- Syntax highlighting for Velocity and JSON editors.
- Light and dark themes.
- SAP Commerce impex import helpers.
- Automated regression tests for critical templates.

## Contributing

1. Fork the repository.
2. Create a feature branch.
3. Make a focused change.
4. Test the application in a browser.
5. Update this README when behavior or setup changes.
6. Open a pull request with a concise description and screenshots when useful.

Please keep the project simple: no build step, no backend dependency, and no
heavy framework unless the project direction changes intentionally.

## License

This project is licensed under the MIT License. See `LICENSE` for details.

## Acknowledgments

- [Apache Velocity](https://velocity.apache.org/)
- [VelocityJS](https://github.com/shepherdwind/velocity.js)
- [Bootstrap](https://getbootstrap.com/)
- [OpenRouter](https://openrouter.ai/)
