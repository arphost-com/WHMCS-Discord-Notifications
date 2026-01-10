# WHMCS Discord Notification Hook
Want instant Discord notifications? Need to know when you've received a ticket reply without waiting for emails to give you a notification? This hook will allow just that! It's **free**, open-source and customisable - offering a range of instant notifications within your Discord server. 

## Brought To You For Free By Zare.com - Updated by arphost.com

## Installation Instructions
1. Download a free copy of this GitHub repo or release version; you should end up with a `.zip` file.
2. Extract the file and upload the `includes` folder within the zip to your base WHMCS directory (we'd recommend doing so on a development environment first).
3. Open up the file you have just uploaded, which will be within the `includes/hooks` directory. The full path is `includes/hooks/WHMCS-Discord-Notifications.php`
4. Modify lines `11-41` to enter your Discord configuration. Comments are provided below each option to assist you in understanding what data is needed for each.
5. Modify lines `42-74` to your liking to enable or disable which notifications are sent by the hook to your Discord server.
6. Give it a test! Check to make sure it sends through to the channel configured within your Discord server; if it doesn't work, double-check your config options! **Enjoy!**

## Configuration Options
* Set a specific rank depending on the notification type to get pinged to deal with it.
* Automatically generated link to instantly navigate to the page the notification is relating to.
* Configurable name of the bot sending messages.
* Configurable avatar profile image (allowing the same webhook to be used by multiple installs).
* Configurable message colours.

## Notification Types
### Ticket Notifications
* New Ticket Opened
* New Ticket Reply Received
* New Ticket Note
* Ticket Flagged To Staff Member  

### Invoice Notifications
* Invoice Payment Received
* Invoice Refunded
* Invoice Late Fee Added  

### Order Notifications
* Order Marked as Pending
* Order Paid
* Order Accepted
* Order Marked As Fraudulent
* Order Cancelled
* Order Cancelled and Refunded  

### Network Issue Notifications
* New Network Issue
* Network Issue Modified
* Network Issue Closed

### Misc Notifications
* Cancellation Request Received

## 🔐 Security, Stability, and Best Practice Improvements

The following issues were identified and resolved in  
`includes/hooks/WHMCS-Discord-Notifications.php`.

---

## 🚨 Critical Security Fix

### 1. SSL Certificate Verification (lines 618–619)
SSL verification was previously disabled and has now been properly enabled:

- `CURLOPT_SSL_VERIFYHOST` set to **2** (verifies the hostname matches the certificate)
- `CURLOPT_SSL_VERIFYPEER` set to **true** (verifies the certificate chain)

**Impact:**  
This change prevents man-in-the-middle (MITM) attacks when communicating with Discord’s webhook API.

---

## 🛠️ Error Handling Improvements

### 2. `InvoicePaid` Hook (lines 89–98)
- Added validation for `GetInvoice` API call
- Added validation for `GetClientsDetails` API call
- Implemented proper logging when either API call fails

---

### 3. `OrderPaid` Hook (lines 277–300)
Enhancements include:

- Validation for `GetOrders` API call
- Null check for order data:
  ```php
  empty($orders['orders']['order'][0])
