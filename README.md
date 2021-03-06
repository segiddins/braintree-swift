# Braintree Swift

Braintree v.zero for Swift apps on iOS and OS X.

## Features

* Tokenize credit cards to create `payment_method_nonces`
* Tokenize Apple Pay `PKPayment`s to create `payment_method_nonces` (iOS only)
* Vault credit cards from raw credit card details

## Integration

* Add this repo as a git submodule
* Add Braintree to your app target:
  * Either add `Braintree.swift` to your app's compiled sources;
  * Or add `Braintree-Swift.xcodeproj` to your Xcode Project
    * Add `Braintree-Swift.framework` as a `Target Dependency`;
    * and add `Braintree-Swift.framework` under a `Link Binary with Libraries`

## Usage

```swift
let braintree = Braintree.Client(clientTokenProvider)
let card = Braintree.PaymentMethodDetails.Card(number: "4111111111111111", expiration: Braintree.Expiration(expirationMonth: 12, expirationYear: 2015))
braintree.tokenize(card) { result in
    switch result {
    case let .RequestError(message):
        println("Got a validation error: \(message)")
    case let .BraintreeError(message):
        println("Got a Braintree error: \(message)")
    case let .PaymentMethodNonce(nonce):
        println("Got a nonce: \(nonce)")
    }
}
```

See [Braintree Playground](BraintreeUsage.playground/section-1.swift).

Read [Braintree's developer documentation](https://developers.braintreepayments.com/ios/sdk/overview/how-it-works) for more information about the processing payments with Braintree.

## Minimum Requirements

* Xcode 6.1
* iOS 8.1 or OS X 10.10 Base SDK
* iOS 8.0-8.1 or OS X 10.10 Deployment Target
* Braintree server-side integration, using the latest client libraries as of 11/14/14
  * An authenticated endpoint on your server that generates `client_tokens`
  * Another authenticated endpoint on your server that accepts `payment_method_nonce`s

## Project Status

:warning: Under Construction :warning: - This library is not officially supported by Braintree; use it at your own risk. [braintree_ios](https://github.com/braintre/braintree_ios), which is written in Objective-C, is fully supported and interoperable with Swift apps.

### Missing Features

* [Security] SSL Certificate Pinning
* [Functionality] Support for credit card verification data, like CVV or Postal Code
* [Functionality] Support for some alternative payment methods, like PayPal and Venmo
* [UI] UI Bindings
* [UI] Drop In

## License

```
Copyright (c) 2014 Braintree, a division of PayPal, Inc.

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
```
