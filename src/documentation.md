# LeadsCalendar Documentation

Welcome to the official documentation for LeadsCalendar, a web application designed to streamline event creation and payment processing. This comprehensive guide will walk you through integrating the Google Calendar API, PayPal REST API, and Binance Pay API into the LeadsCalendar project. By following this documentation, you'll be able to understand the project's functionality, access code samples, and deploy the application successfully.

## Project Overview

LeadsCalendar integrates three main functionalities:

1. **Event Creation**: Users can create events directly on their Google Calendar through the LeadsCalendar interface.
2. **Payment Processing**: Upon event creation, users are prompted to make a payment of 1 USD or its equivalent in cryptocurrency.
3. **Confirmation**: Events are confirmed only after successful payment processing.

## Technical Requirements

To integrate the required APIs, you'll need to understand their technical aspects:

1. [Google Calendar API](https://developers.google.com/calendar/api/guides/overview)
2. [PayPal REST API](https://developer.paypal.com/api/rest/)
3. [Binance Pay API](https://developers.binance.com/docs/binance-pay/introduction)

## Functionality

### Event Creation

To create events on Google Calendar via LeadsCalendar:

1. Log in to LeadsCalendar.
2. Navigate to the "Create Event" section.
3. Fill in the event details such as title, date, time, and location.
4. Click "Create" to initiate event creation on Google Calendar.

### Payment Processing

After event details are filled:

1. Users are prompted to make a payment of 1 USD or equivalent in cryptocurrency.
2. Select the preferred payment method (PayPal or Binance Pay).
3. Complete the payment process.

### Confirmation

Events are confirmed upon successful payment processing. Confirmation includes adding the event to the user's Google Calendar.

## Code Samples and Configurations

### Google Calendar API Integration

```python
# Sample Python code to create an event using Google Calendar API
import google.oauth2.credentials
from googleapiclient.discovery import build

# Initialize credentials
credentials = google.oauth2.credentials.Credentials(
    YOUR_ACCESS_TOKEN
)

# Build the service
service = build('calendar', 'v3', credentials=credentials)

# Define event details
event = {
  'summary': 'New Event',
  'location': 'Sample Location',
  'start': {
    'dateTime': '2024-04-11T10:00:00',
    'timeZone': 'America/New_York',
  },
  'end': {
    'dateTime': '2024-04-11T12:00:00',
    'timeZone': 'America/New_York',
  },
}

# Insert event
event = service.events().insert(calendarId='primary', body=event).execute()
print('Event created: %s' % (event.get('htmlLink')))
```

### PayPal REST API Integration

```python
# Sample Python code to initiate payment using PayPal REST API
import requests

# PayPal API endpoint
url = "https://api.paypal.com/v1/payments/payment"

# Payload
payload = {
  "intent": "sale",
  "payer": {
    "payment_method": "paypal"
  },
  "transactions": [{
    "amount": {
      "total": "1.00",
      "currency": "USD"
    }
  }],
  "redirect_urls": {
    "return_url": "https://example.com/return",
    "cancel_url": "https://example.com/cancel"
  }
}

# Make POST request
response = requests.post(url, json=payload)
print(response.json())
```

### Binance Pay API Integration

```python
# Sample Python code to initiate payment using Binance Pay API
import requests

# Binance Pay API endpoint
url = "https://api.binance.com/api/v1/payments"

# Payload
payload = {
  "coin": "BTC",
  "amount": "0.0001",
  "product_id": "123456",
  "order_id": "abc123",
  "title": "Sample Payment"
}

# Make POST request
response = requests.post(url, json=payload)
print(response.json())
```
