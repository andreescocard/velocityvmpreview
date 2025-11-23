# Velocity VM Preview

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Version](https://img.shields.io/badge/version-1.0.0-green.svg)]()

## 🎯 Overview

**Velocity VM Preview** is an interactive web tool for testing and visualizing Velocity templates (.vm) in real-time. With an intuitive interface, you can insert Velocity templates, provide context data in JSON format, and immediately see the generated HTML, both as code and visually rendered.

This project was created to facilitate the development and testing of Velocity templates without the need to configure a server or complex environment - just open the HTML file in your browser!

> 💡 **Perfect for**: Developers working with SAP Commerce Cloud (Hybris), teams using Velocity templates for emails, CMS, or storefront, and for technical chapter presentations.

## 🚀 Project Objectives

### Problems it Solves:
- **Slow development**: Testing Velocity templates usually requires server deployment, application restart, etc.
- **Lack of immediate feedback**: Hard to know if the template works until you see it in the final environment.
- **Learning curve**: Developers new to Velocity need a safe environment to experiment.

### Solutions:
- ✅ Instant preview of Velocity templates
- ✅ Fast testing without backend server requirements
- ✅ Syntax validation and error visualization
- ✅ Automatic context generation with AI (optional)
- ✅ Educational tool for onboarding and technical chapters

## 🛠️ Technologies Used

- **[VelocityJS](https://github.com/shepherdwind/velocity.js) 2.0.6** - Velocity rendering engine in JavaScript
- **[Bootstrap 5.3](https://getbootstrap.com/)** - CSS framework for modern and responsive UI (via CDN)
- **Vanilla JavaScript (ES6+)** - Application logic without heavy dependencies
- **[OpenRouter API](https://openrouter.ai/)** - Optional integration with AI models for context generation and insights
- **HTML5 + CSS3** - Structure and styling

**No build step required!** Everything works directly in the browser via CDN.

## 📦 How to Run Locally

### Option 1: Directly in browser (simplest)
```bash
# 1. Clone the repository
git clone https://github.com/your-username/velocityvmpreview.git
cd velocityvmpreview

# 2. Open the file in browser
# Windows:
start index.html
# Mac:
open index.html
# Linux:
xdg-open index.html
```

### Option 2: With Live Server (recommended for development)
```bash
# If you use VS Code with Live Server extension
# Right-click on index.html > "Open with Live Server"

# OR use any local HTTP server:
npx http-server .
# or
python -m http.server 8000
```

Access: `http://localhost:8000`

## 📖 How to Use

### Basic Step-by-Step:

1. **Insert Velocity Template**
   - In the left textarea, type or paste your .vm template
   - Example:
   ```velocity
   <h1>Hello, $customer.firstName!</h1>
   #if($customer.isPremium)
     <p>You are a premium customer!</p>
   #end
   ```

2. **Insert JSON Context**
   - In the right textarea, provide the data in JSON format
   - Example:
   ```json
   {
     "customer": {
       "firstName": "John",
       "isPremium": true
     }
   }
   ```

3. **Render**
   - Click the "Renderizar" button
   - See the generated HTML in the bottom left panel
   - See the rendered result in the iframe on the right

4. **Use AI Features (Optional)**
   - Insert your OpenRouter API Key
   - Select an AI model
   - Click "Gerar Contexto" to automatically create JSON
   - Click "Obter Insights" to receive improvement suggestions

### Pre-loaded Examples:

Click "Carregar Exemplo" and choose from:
- **📧 Order Confirmation Email**: Transactional email template (SAP Commerce real use case)
- **🛒 Product Listing**: Loop with product array and stock conditionals
- **🔀 Customer Segmentation**: Conditional content based on customer type
- **📦 Cart Abandoned Email**: Reminder email with cart items

## 🔗 Connection with SAP Commerce Cloud / Commerce Storefront

### Where Velocity is Used:

**SAP Commerce Cloud** (formerly Hybris) uses Velocity templates in several areas:

1. **Email Templates**
   - Transactional emails (order confirmation, password recovery, abandoned cart, etc.)
   - Newsletters and marketing campaigns
   - Location: `/resources/impex/projectdata-email-content.impex`
   - Real example: Order confirmation emails sent via `EmailService`

2. **CMS Components**
   - Dynamic component rendering in storefront
   - Content personalization based on user context
   - Example: Product tiles, promotional banners with customer-specific data

3. **Page Renderers**
   - Custom page templates
   - Dynamic HTML generation on server-side
   - Integration with CMS cockpit

4. **Reports and Exports**
   - Formatted document generation
   - Data export templates
   - Invoice generation

### How This Preview Tool Helps:

| Real Scenario | How the Tool Helps |
|--------------|-------------------|
| Create new email template | Quickly test variables like `$customer.firstName`, `$order.code`, `$product.price` |
| Debug broken template | Isolate issues with controlled context |
| Developer onboarding | Experiment with Velocity syntax without affecting environments |
| Document templates | Generate visual examples for technical documentation |
| Code review | Present template changes visually before deployment |
| Test data structures | Validate that context objects match expected template structure |

### Real Example - SAP Commerce Order Confirmation Email:

```velocity
<!DOCTYPE html>
<html>
<head>
  <style>
    body { font-family: Arial, sans-serif; color: #333; }
    .header { background: #0070d2; color: white; padding: 20px; text-align: center; }
    .content { padding: 20px; }
    .order-summary { border: 1px solid #ddd; padding: 15px; margin: 20px 0; }
    .item { border-bottom: 1px solid #eee; padding: 10px 0; }
    .total { font-size: 20px; font-weight: bold; color: #0070d2; }
  </style>
</head>
<body>
  <div class="header">
    <h1>Order Confirmed</h1>
  </div>
  
  <div class="content">
    <p>Hello $customer.firstName $customer.lastName,</p>
    
    <p>Thank you for your order! Your order <strong>#$order.code</strong> has been confirmed.</p>
    
    <div class="order-summary">
      <h2>Order Summary</h2>
      
      #foreach($entry in $order.entries)
        <div class="item">
          <strong>$entry.product.name</strong> (SKU: $entry.product.code)<br>
          Quantity: $entry.quantity | Unit Price: $$entry.basePrice<br>
          <strong>Subtotal: $$entry.totalPrice</strong>
        </div>
      #end
      
      <p class="total">Order Total: $$order.totalPrice</p>
      
      #if($order.appliedPromotions)
        <p style="color: green;">
          ✓ Promotions applied: $order.appliedPromotions.size()
        </p>
      #end
    </div>
    
    #if($order.deliveryAddress)
      <h3>Delivery Address</h3>
      <p>
        $order.deliveryAddress.firstName $order.deliveryAddress.lastName<br>
        $order.deliveryAddress.line1<br>
        #if($order.deliveryAddress.line2)
          $order.deliveryAddress.line2<br>
        #end
        $order.deliveryAddress.town, $order.deliveryAddress.region $order.deliveryAddress.postalCode<br>
        $order.deliveryAddress.country.name
      </p>
    #end
    
    <p>Estimated delivery: $order.deliveryMode.name - $order.estimatedDeliveryDate</p>
    
    <hr>
    <small>Questions? Contact us at support@example.com</small>
  </div>
</body>
</html>
```

**Corresponding JSON Context (matching SAP Commerce Cloud data model):**
```json
{
  "customer": {
    "firstName": "Sarah",
    "lastName": "Johnson",
    "uid": "sarah.johnson@example.com"
  },
  "order": {
    "code": "00001234",
    "created": "2024-11-23T10:30:00Z",
    "totalPrice": "1,299.98",
    "currency": { "isocode": "USD", "symbol": "$" },
    "entries": [
      {
        "product": {
          "code": "123456",
          "name": "Premium Wireless Headphones",
          "description": "Noise-canceling, 30-hour battery"
        },
        "quantity": 1,
        "basePrice": "299.99",
        "totalPrice": "299.99"
      },
      {
        "product": {
          "code": "789012",
          "name": "Smartphone Case - Black",
          "description": "Protective case with card slots"
        },
        "quantity": 2,
        "basePrice": "24.99",
        "totalPrice": "49.98"
      }
    ],
    "deliveryAddress": {
      "firstName": "Sarah",
      "lastName": "Johnson",
      "line1": "123 Main Street",
      "line2": "Apt 4B",
      "town": "San Francisco",
      "region": "CA",
      "postalCode": "94102",
      "country": { "isocode": "US", "name": "United States" }
    },
    "deliveryMode": {
      "code": "standard",
      "name": "Standard Delivery (3-5 business days)"
    },
    "estimatedDeliveryDate": "Nov 28, 2024",
    "appliedPromotions": [
      { "code": "WELCOME10", "description": "10% off first order" }
    ]
  }
}
```

## 🤖 AI Integration (OpenRouter)

### How to Configure:

1. **Get API Key:**
   - Visit [OpenRouter.ai](https://openrouter.ai/)
   - Create an account (if needed)
   - Generate an API Key at [keys](https://openrouter.ai/keys)
   - Free tier available with rate limits

2. **Configure in Application:**
   - Expand the "🤖 Assistente IA" section
   - Paste your API Key in the field (never saved, memory only)
   - Select your desired model

3. **Supported Models** (ranked by OpenRouter performance):
   - `google/gemini-2.0-flash-exp:free` - Gemini 2.0 Flash (FREE, excellent performance)
   - `anthropic/claude-3.5-sonnet` - Claude 3.5 Sonnet (top tier, recommended)
   - `openai/gpt-4-turbo` - GPT-4 Turbo (excellent quality)
   - `google/gemini-pro-1.5` - Gemini 1.5 Pro (great balance)
   - `qwen/qwen-2.5-72b-instruct` - Qwen 2.5 72B (good cost-benefit)
   - `meta-llama/llama-3.3-70b-instruct` - Llama 3.3 70B (open-source option)

### Available Features:

#### 1. Generate JSON Context
- **What it does**: Analyzes your template and automatically generates a JSON with all necessary variables
- **When to use**: When you have the template but don't want to create context manually
- **Example**: Template with `$customer.firstName`, `$order.code` → generates complete JSON structure

#### 2. Get Template Insights
- **What it does**: Analyzes template + context and provides:
  - ✅ Potential syntax errors
  - 💡 Improvement suggestions
  - 🛡️ Security validations (XSS, injection risks)
  - 📚 Best practices not followed
  - 🎯 SAP Commerce Cloud specific recommendations
- **When to use**: Code review, refactoring, learning, before deployment

### Security:
⚠️ **Important**: The API Key is NEVER saved to disk or sent to any server other than OpenRouter. It's kept only in memory during the browser session.

## 📚 Usage Examples

### Example 1: Password Recovery Email (SAP Commerce)
**Template:**
```velocity
<h1>Password Reset Request</h1>
<p>Hello $customer.firstName,</p>
<p>We received a request to reset your password for account: <strong>$customer.uid</strong></p>
<p>Click the link below to reset your password:</p>
<a href="$resetLink">Reset Password</a>
<p>This link expires in $expiryHours hours.</p>
<p><small>If you didn't request this, please ignore this email.</small></p>
```

**Context:**
```json
{
  "customer": {
    "firstName": "John",
    "uid": "john.doe@example.com"
  },
  "resetLink": "https://shop.example.com/reset?token=abc123",
  "expiryHours": 24
}
```

### Example 2: Product Catalog with Stock Status
**Template:**
```velocity
<h2>Featured Products</h2>
<div class="product-grid">
  #foreach($product in $products)
    <div class="product-card">
      <h3>$product.name</h3>
      <p class="sku">SKU: $product.code</p>
      <p class="price">$$product.price.value</p>
      
      #if($product.stock.stockLevelStatus == "inStock")
        <span class="badge badge-success">In Stock</span>
      #elseif($product.stock.stockLevelStatus == "lowStock")
        <span class="badge badge-warning">Only $product.stock.stockLevel left!</span>
      #else
        <span class="badge badge-danger">Out of Stock</span>
      #end
      
      #if($product.promotions && $product.promotions.size() > 0)
        <p class="promo">🎉 $product.promotions.get(0).description</p>
      #end
    </div>
  #end
</div>
```

**Context:**
```json
{
  "products": [
    {
      "code": "123456",
      "name": "Premium Laptop",
      "price": { "value": "1299.99", "currencyIso": "USD" },
      "stock": { "stockLevelStatus": "inStock", "stockLevel": 50 },
      "promotions": [
        { "code": "SAVE20", "description": "Save 20% today!" }
      ]
    },
    {
      "code": "789012",
      "name": "Wireless Mouse",
      "price": { "value": "29.99", "currencyIso": "USD" },
      "stock": { "stockLevelStatus": "lowStock", "stockLevel": 3 },
      "promotions": []
    }
  ]
}
```

### Example 3: Customer Segmentation Email
**Template:**
```velocity
#if($customer.segment == "VIP" && $customer.loyaltyPoints > 5000)
  <div class="vip-exclusive">
    <h2>🌟 VIP Exclusive Offer</h2>
    <p>Dear $customer.title $customer.lastName,</p>
    <p>You have <strong>$customer.loyaltyPoints points</strong>. Redeem now for exclusive rewards!</p>
    <a href="$rewardsLink" class="btn-gold">View VIP Rewards</a>
  </div>
#elseif($customer.segment == "Premium")
  <div class="premium-offer">
    <h2>⭐ Premium Member Benefits</h2>
    <p>Hi $customer.firstName,</p>
    <p>Earn more points to unlock VIP status. Current: $customer.loyaltyPoints points</p>
  </div>
#else
  <div class="standard-offer">
    <h2>Join Our Loyalty Program</h2>
    <p>Hello $customer.firstName,</p>
    <p>Sign up today and start earning rewards on every purchase!</p>
  </div>
#end
```

**Context:**
```json
{
  "customer": {
    "title": "Ms.",
    "firstName": "Emily",
    "lastName": "Chen",
    "segment": "VIP",
    "loyaltyPoints": 7500
  },
  "rewardsLink": "https://shop.example.com/rewards"
}
```

## 🗺️ Roadmap / Next Steps

### Planned Features:

- [ ] **Template Library**: Save and load favorite templates
- [ ] **Export/Import**: Export templates as `.vm` and contexts as `.json`
- [ ] **Sharing**: Generate shareable link with template + context (URL encoding)
- [ ] **History**: Navigate through previous versions (using localStorage)
- [ ] **Syntax Highlighting**: Color-coded editor for better readability
- [ ] **Advanced Validation**: Lint templates with inline suggestions
- [ ] **Themes**: Light/dark mode
- [ ] **Multi-language**: Interface in English and Portuguese
- [ ] **Comparison**: Visual diff between two template versions
- [ ] **Automated Testing**: Test suite for critical templates
- [ ] **SAP Commerce Integration**: Direct import from impex files

### Technical Improvements:

- [ ] PWA (Progressive Web App) for offline use
- [ ] Service Worker for asset caching
- [ ] Data compression for sharing
- [ ] GitHub Gist integration for cloud storage
- [ ] VS Code plugin/extension
- [ ] Real-time collaboration (multiplayer mode)

## 🤝 How to Contribute

Contributions are welcome! To contribute:

1. Fork this repository
2. Create a branch for your feature (`git checkout -b feature/MyFeature`)
3. Commit your changes (`git commit -m 'Add: MyFeature'`)
4. Push to the branch (`git push origin feature/MyFeature`)
5. Open a Pull Request

### Guidelines:
- Keep the project without build step (CDN only)
- Write clean and commented code
- Test across different browsers
- Update this README if adding features
- Follow existing code style

## 📄 License

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

**MIT License Summary:**
- ✅ Commercial use allowed
- ✅ Modification allowed
- ✅ Distribution allowed
- ✅ Private use allowed
- ⚠️ No warranty (use at your own risk)

---

## 📞 Contact and Support

**Questions or suggestions?**
- Open an [Issue](https://github.com/your-username/velocityvmpreview/issues)
- Contact via internal Slack (channel #chapter-frontend)

---

## 🙏 Acknowledgments

- [Apache Velocity](https://velocity.apache.org/) - The original template engine
- [VelocityJS](https://github.com/shepherdwind/velocity.js) - JavaScript implementation
- [Bootstrap](https://getbootstrap.com/) - UI framework
- [OpenRouter](https://openrouter.ai/) - AI integration platform

---

**Developed with ❤️ to make working with Velocity Templates easier**

*Last updated: November 2024*