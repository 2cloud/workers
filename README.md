## 2cloud Workers

These are workers written to run on [IronWorker](http://www.iron.io/products/worker), though they could, hypothetically, be slightly modified to run on any system.

Each worker represents tasks that will be kicked off via a webhook or on a schedule. Each task is standalone and simply interacts with the [2cloud API](/2cloud/api/wiki).

## Workers

The following workers are necessary for the operation of the system:

### StripeCallback

This worker handles callbacks from the [Stripe API](https://www.stripe.com/docs/webhooks) and translates them into [2cloud Subscription requests](/2cloud/api/wiki/Subscriptions).

### ExpiredSubscriptionEmailer

This worker runs daily to let users know when there's an error with their Subscription. It retrieves a list of subscriptions that are in the grace period, and emails the user associated with the subscription to let them know they need to update their subscription or lose access to the service.

### EmailVerifier

This worker runs every minute to check an [IronMQ](http://www.iron.io/products/mq) queue for messages. For each message, it retrieves the payload, then emails the email address specified in the payload with the verification code specified in the payload.