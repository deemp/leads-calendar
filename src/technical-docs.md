# Technical documentation

The following section demonstrates the code used for integration with the APIs.

1. [Google Calendar API](https://developers.google.com/calendar/api/guides/overview)
2. [PayPal REST API](https://developer.paypal.com/api/rest/)
3. [Binance Pay API](https://developers.binance.com/docs/binance-pay/introduction)

## Google Calendar API Integration (JavaScript)

```javascript
// Sample JavaScript code to create an event using Google Calendar API
const { google } = require('googleapis');

// Initialize OAuth2 client
const oauth2Client = new google.auth.OAuth2(
  YOUR_CLIENT_ID,
  YOUR_CLIENT_SECRET,
  YOUR_REDIRECT_URL
);

// Set access token
oauth2Client.setCredentials({
  access_token: YOUR_ACCESS_TOKEN,
  refresh_token: YOUR_REFRESH_TOKEN,
  // Optionally, set expiry_date if available
});

// Create calendar event
const calendar = google.calendar({ version: 'v3', auth: oauth2Client });
const event = {
  summary: 'New Event',
  location: 'Sample Location',
  start: {
    dateTime: '2024-04-11T10:00:00',
    timeZone: 'America/New_York',
  },
  end: {
    dateTime: '2024-04-11T12:00:00',
    timeZone: 'America/New_York',
  },
};

calendar.events.insert({
  calendarId: 'primary',
  resource: event,
}, (err, res) => {
  if (err) {
    console.error('Error creating event:', err);
    return;
  }
  console.log('Event created:', res.data.htmlLink);
});
```

## PayPal REST API Integration (JavaScript)

```javascript
// Sample JavaScript code to initiate payment using PayPal REST API
const request = require('request');

// PayPal API endpoint
const url = 'https://api.paypal.com/v1/payments/payment';

// Request payload
const payload = {
  intent: 'sale',
  payer: {
    payment_method: 'paypal'
  },
  transactions: [{
    amount: {
      total: '1.00',
      currency: 'USD'
    }
  }],
  redirect_urls: {
    return_url: 'https://example.com/return',
    cancel_url: 'https://example.com/cancel'
  }
};

// Make POST request
request.post({
  url: url,
  headers: {
    'Content-Type': 'application/json',
    'Authorization': 'Bearer ' + YOUR_ACCESS_TOKEN // Replace with your access token
  },
  body: JSON.stringify(payload)
}, function(err, response, body) {
  if (err) {
    console.error('Error:', err);
    return;
  }
  console.log('Payment initiated:', body);
});
```

## Binance Pay API Integration (JavaScript)

```javascript
// Sample JavaScript code to initiate payment using Binance Pay API
const request = require('request');

// Binance Pay API endpoint
const url = 'https://api.binance.com/api/v1/payments';

// Request payload
const payload = {
  coin: 'BTC',
  amount: '0.0001',
  product_id: '123456',
  order_id: 'abc123',
  title: 'Sample Payment'
};

// Make POST request
request.post({
  url: url,
  headers: {
    'Content-Type': 'application/json',
    'X-MBX-APIKEY': YOUR_API_KEY // Replace with your API key
  },
  body: JSON.stringify(payload)
}, function(err, response, body) {
  if (err) {
    console.error('Error:', err);
    return;
  }
  console.log('Payment initiated:', body);
});
```
