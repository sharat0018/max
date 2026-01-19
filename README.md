# 🛍️ CLIQTRIX - E-Commerce Zobot for Zoho SalesIQ

**CLIQTRIX** (also known as **MAX**) is a complete e-commerce conversational assistant built for Zoho SalesIQ using Deluge scripting. It provides end-to-end shopping experience from product discovery to order fulfillment and returns.

## 🌟 Features

### 1. **Deals & Offers Browser**
- Dynamically fetches discounted products from Shopify
- Calculates and displays discount percentages
- Filters products by specific discount rates (e.g., "20% OFF")
- Shows original price vs. sale price comparison

### 2. **Product Catalog**
- Browse complete product inventory
- View detailed product information with images
- Real-time stock availability checking
- Direct links to product pages

### 3. **Shopping Cart**
- Add products to cart with custom quantities
- Real-time inventory validation
- Automatic price calculation
- Stateless architecture (no session dependencies)

### 4. **Checkout & Order Creation**
- Email collection during checkout
- Order confirmation with order ID
- Direct integration with Shopify Admin API
- Automatic email notifications to customers

### 5. **Order Tracking**
- Track orders by email address
- View order status (dispatched/pending)
- Display all historical orders
- Real-time fulfillment status updates

### 6. **Return & Cancellation**
- Return non-dispatched orders
- Two-step confirmation process
- Automatic refund initiation
- Prevents returns for shipped orders

## 🚀 Live Demo

- **Website**: https://max-cypher.zohosites.com/
- **Zobot Name**: MAX - CLIQTRIX E-Commerce Assistant
- **Platform**: Zoho SalesIQ

## 🔧 Technical Architecture

### Integration
- **E-Commerce Platform**: Shopify
- **API**: Shopify Admin REST API (2023-10)
- **Authentication**: OAuth 2.0 via Access Token
- **Scripting Language**: Deluge (Zoho's proprietary language)

### Key Technical Features
- **Stateless Design**: No visitor variable dependencies
- **Real-time API Calls**: Live product and order data
- **Error Handling**: Graceful fallbacks for API failures
- **Intent Recognition**: Natural language processing for user commands
- **Dynamic Suggestions**: Context-aware button recommendations

## 📋 Setup Instructions

### Prerequisites
1. Zoho SalesIQ account
2. Shopify store with Admin API access
3. Shopify Admin API Access Token

### Step 1: Shopify Configuration

1. **Create Shopify Store** (if you don't have one)
   - Go to https://www.shopify.com/
   - Sign up for a free trial or use existing store

2. **Generate Admin API Access Token**
   - Go to Shopify Admin → Settings → Apps and sales channels
   - Click "Develop apps" → "Create an app"
   - Name your app (e.g., "CLIQTRIX Bot")
   - Go to "API credentials" tab
   - Under "Admin API access token", click "Install app"
   - Copy the Access Token (starts with `shpat_`)

3. **Configure API Permissions**
   Required scopes:
   - `read_products` - Read product catalog
   - `write_orders` - Create and cancel orders
   - `read_orders` - Track order status

### Step 2: Zoho SalesIQ Setup

1. **Create Zobot**
   - Login to Zoho SalesIQ
   - Go to Settings → Bots → Add Bot
   - Choose "SalesIQ Scripts" as bot type
   - Name your bot (e.g., "MAX" or "CLIQTRIX")

2. **Upload Bot Script**
   - Open `FINAL_COMPETITION_BOT.deluge` file
   - Replace the following variables at the top:
     ```deluge
     shopifyDomain = "your-store.myshopify.com";
     shopifyAccessToken = "your_shopify_admin_api_token";
     ```
   - Copy the entire script
   - Paste into Zoho SalesIQ bot editor
   - Click "Save" and "Publish"

3. **Configure Bot Settings**
   - Bot works on: All visitors
   - Bot typing status: Enabled (2 sec delay)
   - Allow handoff: During offline hours
   - Bot initiates: When visitors click chat widget

### Step 3: Website Integration

1. **Get SalesIQ Widget Code**
   - Go to Settings → Installation → Embed Code
   - Copy your widget code (format: `siq[code]`)

2. **Add to Website**
   ```html
   <script>
   var $zoho=$zoho || {};
   $zoho.salesiq = $zoho.salesiq || {
     widgetcode: "your_widget_code_here",
     values:{},ready:function(){}
   };
   var d=document;
   s=d.createElement("script");
   s.type="text/javascript";
   s.id="zsiqscript";
   s.defer=true;
   s.src="https://salesiq.zoho.com/widget";
   t=d.getElementsByTagName("script")[0];
   t.parentNode.insertBefore(s,t);
   </script>
   ```

## 🧪 Testing Guide

### Test Flow 1: Browse and Purchase
1. Open website → Chat widget appears
2. Type **"Deals"** → See discounted products
3. Click **"20% OFF"** → Filter by discount
4. Click product name (e.g., "Laptop Stand") → View details
5. Click **"Add to Cart"** → Product added
6. Type **"2 Laptop Stand"** → Set quantity to 2
7. Type **"Checkout 2 Laptop Stand demo@example.com"** → Review order
8. Click **"Confirm"** button → Order created
9. Check email for confirmation

### Test Flow 2: Track Orders
1. Type **"My Orders"** → Prompt for email
2. Enter **"demo@example.com"** → View all orders
3. See order list with status (dispatched/pending)

### Test Flow 3: Return Order
1. Type **"My Orders"** → Enter email
2. Click **"Return #1009"** → Initiate return
3. Click **"Cancel 1009"** → Confirm cancellation
4. Order cancelled, refund initiated

## 📝 User Commands Reference

| Command | Description |
|---------|-------------|
| `Deals` | Show discounted products |
| `Products` | Browse catalog |
| `20% OFF` | Filter by discount percentage |
| `[Product Name]` | View product details (e.g., "Laptop Stand") |
| `Add [Product] to Cart` | Start cart flow |
| `[Qty] [Product]` | Set quantity (e.g., "2 Laptop Stand") |
| `Checkout [Qty] [Product] [Email]` | Place order |
| `My Orders` | Track orders |
| `[Email]` | View orders for email |
| `Return #[OrderNum]` | Initiate return |
| `Cancel [OrderNum]` | Confirm cancellation |

## 🏗️ Project Structure

```
cliqtrix/
├── FINAL_COMPETITION_BOT.deluge  # Main bot script (production-ready)
├── README.md                      # This file
└── .gitignore                     # Git ignore rules
```

## 🔐 Security Notes

- **API Credentials**: Never commit actual API tokens to public repositories
- **OAuth 2.0**: Uses Shopify Admin API with secure token authentication
- **Email Validation**: Basic format checking (contains @ and .)
- **Order Verification**: Validates order ownership before cancellation

## 🎯 Competition Requirements Checklist

✅ **E-Commerce Integration**: Shopify Admin API  
✅ **OAuth 2.0 Authentication**: X-Shopify-Access-Token header  
✅ **Product Catalog**: Real-time product fetching  
✅ **Deals & Discounts**: Dynamic discount calculation  
✅ **Shopping Cart**: Quantity management with validation  
✅ **Checkout Flow**: Email collection and order creation  
✅ **Order Tracking**: Email-based order lookup  
✅ **Returns/Cancellations**: Non-dispatched order returns  
✅ **Email Notifications**: Automatic order confirmations  
✅ **Conversational UI**: Natural language intent recognition  
✅ **Error Handling**: Graceful API failure management  

## 🛠️ Troubleshooting

### Bot not responding
- Check if bot is published in Zoho SalesIQ
- Verify widget code is correctly embedded
- Check browser console for JavaScript errors

### Products not loading
- Verify Shopify API credentials are correct
- Check API token has required permissions
- Ensure Shopify store has products with inventory

### Orders not creating
- Verify `write_orders` permission is enabled
- Check product variant IDs are valid
- Ensure email format is correct

### Returns not working
- Verify order is not already dispatched
- Check order number format (#1009)
- Ensure API token has order cancellation permission

## 📞 Support

For issues or questions:
- Check Zoho SalesIQ documentation: https://www.zoho.com/salesiq/help/
- Shopify API docs: https://shopify.dev/docs/api/admin-rest
- Deluge scripting guide: https://www.zoho.com/deluge/

## 📄 License

This project is created for the Zoho SalesIQ Bot Competition.

## 👨‍💻 Author

**Team CLIQTRIX**  
Built with ❤️ using Zoho SalesIQ and Shopify

---

**Note**: Replace placeholder credentials with your actual Shopify store details before deployment.
