# Facebook Conversion API for Next.js

A lightweight, type-safe implementation of the Facebook Conversion API for Next.js applications.

## Features

- Server-side event tracking for Facebook Pixel
- Compatible with Next.js App Router and Pages Router
- TypeScript support
- Easy-to-use React components
- Automatic event deduplication
- GDPR-friendly implementation

## Installation

```bash
npm install @microdeft/facebook-conversion-api-nextjs
```

or

```bash
yarn add @microdeft/facebook-conversion-api-nextjs
```

## Setup

### 1. Create a Facebook Pixel

If you don't already have a Facebook Pixel set up, create one in your [Meta Business Manager](https://business.facebook.com/events_manager/).

### 2. Configure environment variables

Add these environment variables to your `.env.local` file:

```
FACEBOOK_PIXEL_ID=your_pixel_id
FACEBOOK_ACCESS_TOKEN=your_access_token
```

You can obtain your access token from the [Facebook Business Manager](https://business.facebook.com/events_manager/) under your Pixel's settings.

## Usage

### Basic Server Component (App Router)

```tsx
// app/page.tsx
import { trackPageView } from '@microdeft/facebook-conversion-api-nextjs';

export default async function Page() {
  // Track page view server-side
  await trackPageView();
  
  return <div>My Page Content</div>;
}
```

### API Route (Pages Router)

```tsx
// pages/api/track-event.js
import { createFacebookConversionApiHandler } from '@microdeft/facebook-conversion-api-nextjs/handlers';

export default createFacebookConversionApiHandler({
  // Optional configuration
  debug: process.env.NODE_ENV === 'development',
});
```

### Client-side Component

```tsx
// components/AddToCart.tsx
import { TrackEvent } from '@microdeft/facebook-conversion-api-nextjs/components';

export function AddToCartButton({ product }) {
  return (
    <TrackEvent 
      event="AddToCart" 
      data={{
        content_ids: [product.id],
        content_name: product.name,
        value: product.price,
        currency: 'USD'
      }}
    >
      <button>Add to Cart</button>
    </TrackEvent>
  );
}
```

## API Reference

### Server-side functions

- `trackPageView(options?: PageViewOptions)` - Track a page view event
- `trackEvent(eventName: string, eventData: EventData)` - Track a custom event
- `trackPurchase(purchaseData: PurchaseData)` - Track a purchase event

### Components

- `<TrackEvent />` - React component to track events on user interactions
- `<TrackPageView />` - React component to track page views client-side

### Handler Creators

- `createFacebookConversionApiHandler(config)` - Create an API route handler for Pages Router
- `createFacebookConversionApiRoute(config)` - Create a route handler for App Router

## License

MIT © [Microdeft](https://github.com/microdeft)