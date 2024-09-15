# Stripe

Receive payments on your Medusa commerce application using Stripe.

[Stripe Plugin Documentation](https://docs.medusajs.com/plugins/payment/stripe) | [Medusa Website](https://medusajs.com/) | [Medusa Repository](https://github.com/medusajs/medusa)


## Prerequisites

- [Stripe account](https://stripe.com/)
- For businesses such as marketplaces and software platforms use [Stripe Connect](https://docs.stripe.com/connect) to manage and route payments and payouts between sellers, customers, service providers, and other entities.
- [Sandbox for testing](https://dashboard.stripe.com/sandboxes)

### Prerequisites for testing

- In sandbox dashboard, select More -> Connect -> Get started
- Create a connect account with `Express` type.
- After creating a account, you will receive a link. Go to the link and setup your account info.
- In your sandbox dashboard menu, click `Connected account`, you will see newly created account
  ![alt text](<Screenshot 2024-09-15 at 3.17.46 PM.png>)
  Account name is `CONNECTED_ACCOUNT_ID`

## Getting Started

### Medusa Backend

1\. After creating a sandbox, you will retrieve API keys in welcome screen. Set the following environment variables in `.env`:

```bash
STRIPE_API_KEY=sk_...
# only necessary for production
STRIPE_WEBHOOK_SECRET=whsec_...
```

2\. In `plugins/medusa-payment-stripe/src/core/stripe-base.ts` update your `CONNECTED_ACCOUNT_ID` at `stripeAccount` field

### Storefront Setup

1\. In your `.env.local` file (or the file you’re using for your environment variables), add the following variable:

```bash
NEXT_PUBLIC_STRIPE_KEY=<YOUR_PUBLISHABLE_KEY>
```

2\. In `src/modules/checkout/components/payment-wrapper/index.tsx`, replace `stripePromise` with below code:

```
const stripePromise = stripeKey
  ? loadStripe(stripeKey, { stripeAccount: CONNECTED_ACCOUNT_ID })
  : null
```
