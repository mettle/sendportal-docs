# Mailgun

## Sending Emails

When you first begin, Mailgun will automatically create a sandbox domain that you can use for sending, but to send using your own domain you'll need to create a custom domain. Select _Sending_ then _Domains_ from the menu on the left hand side, then click _Add New Domain_ (you'll need to add credit card details before this button appears).

![https://sendportal.io/img/docs/providers/mailgun/mailgun-1.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-1.png)

Enter the domain name, choose whichever region makes the most sense for you and click _Add Domain_.

![https://sendportal.io/img/docs/providers/mailgun/mailgun-2.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-2.png)

You'll now need to visit the site that you use to manage DNS for the domain provided (usually the domain registrar). The steps to do this are beyond the scope of this documentation as they vary from provider to provider, but you will need to create a `TXT` entry for the relevant domain and paste in the strings from the `Hostname` and `Enter This Value` columns. Once you've added these, click _Verify DNS Settings_.

![https://sendportal.io/img/docs/providers/mailgun/mailgun-3.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-3.png)

You'll now need to copy the `Private API Key` from _Settings_ > _API Keys_

![https://sendportal.io/img/docs/providers/mailgun/mailgun-4.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-4.png)

Then paste this into your SendPortal provider configuration.

![https://sendportal.io/img/docs/providers/mailgun/mailgun-5.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-5.png)

## Tracking

To enable tracking, select _Sending_ then _Webhooks_ from the menu and click the _Add Webhook_ button.

![https://sendportal.io/img/docs/providers/mailgun/mailgun-6.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-6.png)

The URL depends on your domain, but must end with `/api/v1/webhooks/mailgun`. For example, if SendPortal is installed at `https://campaigns.marketing.com`, then each webhook should point to `https://campaigns.marketing.com/api/v1/webhooks/mailgun`.

![https://sendportal.io/img/docs/providers/mailgun/mailgun-7.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-7.png)

You'll need to add an entry for each type of event you want to track, but the URL is the same for each of them.

![https://sendportal.io/img/docs/providers/mailgun/mailgun-8.png](https://sendportal.io/img/docs/providers/mailgun/mailgun-8.png)

That's it! You're now setup to send and track e-mails using Mailgun.
