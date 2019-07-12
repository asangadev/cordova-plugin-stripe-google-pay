# cordova-plugin-stripe-google-pay

Cordova plugin for Stripe Google pay integration

## Notes

This plugin only supports Android.

This plugin will add these dependencies to your build.gradle file:

    com.stripe:stripe-android:6.1.2
    com.google.android.gms:play-services-wallet:16.0.0
    com.android.support:support-v4:27.0.2
    com.android.support:appcompat-v7:24.1.1

## Installation

    cordova plugin add cordova-plugin-stripe-google-pay

## Quick Example

Run below on onDeviceReady function

```javascript
sgap.setKey('pk_test_Ldy7TLYtmnsv1VrI4ULriWSd').then(function(output) {
  sgap.isReadyToPay().then(function() {
    sgap.requestPayment(1000, 'AUD').then(function(token) {
      alert(token);
    }).catch(function(err) {
      alert(err);
    });
  }).catch(function(err) {
    alert(err);
  });
}).catch(function(err) {
  alert(err);
});
```

## Usage

This plugin puts the functions into `window.sgap`.
All functions return a promise.

```javascript
sgap.setKey('pk_test_d34db33f')
```

-   Used to set the Stripe publishable key
-   Required to request payments
-   If test key is provided, then payments are completed in `ENVIRONMENT_TEST` mode, and `ENVIRONMENT_PRODUCTION` mode if the live key is given
-   If you attempt any of the below functions without calling this first, they will throw an error

```javascript
sgap.isReadyToPay()
```

-   Used to test if the appropriate payment method is available on the current device.
-   Resolves if appropriate payment method is available
-   Rejects if not, or if it encounters an error

```javascript
sgap.requestPayment(totalPrice, currency)
```

-   Initiates the payment journey for the user to complete.
-   `totalPrice` must be a string representation of the total price - e.g. for £10.78, it would be `10.78`
-   `currency` must be a valid ISO 4217 currency code for the transaction
-   Resolves when the journey is complete, with the stripe token
-   Rejects if an error occurs

## Switch to PRODUCTION

You need to request for production access before test on production environment. Carefully go through the [CHECK LIST](https://developers.google.com/pay/api/android/guides/test-and-deploy/integration-checklist) mentioned in this [LINK](https://developers.google.com/pay/api/android/guides/test-and-deploy/integration-checklist) and [REQUEST PRODUCTION ACCESS](https://services.google.com/fb/forms/googlepayAPIenable)

## Why this error after switching to PRODUCTION?

#### Request Failed

Make sure you check the APK on a real device and not on an emulator.


## License

MIT
