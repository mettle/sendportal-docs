# Sendgrid

## Sending Emails

To send e-mails using the Twilio Sendgrid provider, you will need a Sendgrid account. If you don't already have one, [visit the Sendgrid website](https://sendgrid.com/) and sign up. No credit card is required and you can get up to 100 free emails per month.

Once registered, open the `Setup Guide`, choose the `Web API` integration and select the PHP language option.

![https://sendportal.io/img/docs/providers/sendgrid/sendgrid-1.png](https://sendportal.io/img/docs/providers/sendgrid/sendgrid-1.png)

Generate an API key and copy it to your SendPortal configuration.

![https://sendportal.io/img/docs/providers/sendgrid/sendgrid-2.png](https://sendportal.io/img/docs/providers/sendgrid/sendgrid-2.png)

Check the `I've integrated the code above` box and click Next.

Send a test e-mail from SendPortal and if it works successfully click _Verify integration_.

## Tracking

![https://sendportal.io/img/docs/providers/sendgrid/sendgrid-3.png](https://sendportal.io/img/docs/providers/sendgrid/sendgrid-3.png)

Open and click tracking is enabled by default in SendGrid, but if you'd like to check the settings you'll find them under _Settings_ > _Tracking_.

![https://sendportal.io/img/docs/providers/sendgrid/sendgrid-4.png](https://sendportal.io/img/docs/providers/sendgrid/sendgrid-4.png)

You can also enable subscription tracking from this page. If enabled, SendGrid will automatically add unsubscribe links to the bottom of every e-mail you send.

![https://sendportal.io/img/docs/providers/sendgrid/sendgrid-5.png](https://sendportal.io/img/docs/providers/sendgrid/sendgrid-5.png)

To enable tracking within SendPortal you'll need to enable event notifications from _Settings_ > _Mail Settings_.

The `HTTP POST URL` depends on your domain, but must end with `/api/v1/webhooks/sendgrid`. For example, if SendPortal is installed at `https://campaigns.marketing.com`, then each webhook should point to `https://campaigns.marketing.com/api/v1/webhooks/sendgrid`.

That's it! You're now setup to send and track e-mails using SendGrid.
