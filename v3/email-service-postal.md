# Postal

[Postal](https://docs.postalserver.io) is an open-source mail server that you host yourself.

## Sending Emails

In your Postal web interface, open the mail server you want to send from and make sure the domain you will be sending from has been added and verified.

Next, create an API credential for the mail server (from the _Credentials_ section, choose _API_ as the credential type) and copy the generated key.

In SendPortal, add a new email service, choose `Postal` as the service type and enter the following:

- `Postal Host` – the hostname of your Postal installation, without `https://`. For example, if your Postal web interface is at `https://postal.example.com`, enter `postal.example.com`. SendPortal always connects to Postal over HTTPS.
- `API Key` – the API credential key you created above.

## Tracking

To enable tracking, open the _Webhooks_ section of your Postal mail server and add a new webhook.

The URL depends on your domain, but must end with `/api/v1/webhooks/postal`. For example, if SendPortal is installed at `https://campaigns.marketing.com`, then the webhook should point to `https://campaigns.marketing.com/api/v1/webhooks/postal`.

Select only the following events, which are the ones SendPortal handles:

- `MessageSent` – recorded as delivered
- `MessageLoaded` – recorded as opened
- `MessageLinkClicked` – recorded as clicked
- `MessageBounced` – recorded as a bounce
- `MessageDeliveryFailed` – recorded as a failure
- `MessageHeld` – recorded as a failure

> SendPortal does not recognise other Postal events. If you send them to SendPortal, they will fail to process: as failed jobs on the `sendportal-webhook-process` queue, or as errors returned to Postal if you use the `sync` queue driver.

Postal only sends `MessageLoaded` and `MessageLinkClicked` events when open and click tracking is set up for your mail server (Postal calls this a track domain).

That's it! You're now setup to send and track e-mails using Postal.
