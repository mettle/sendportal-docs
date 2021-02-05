# Email Services

## Introduction
SendPortal must be integrated with at least one email service provider in order for your emails to be dispatched. You can have multiple email services configured at one given time. For example, you may wish to send newsletters via SES and transactional emails via Postmark.

> The credentials for each email service is stored in an encrypted format in the database. If the `APP_KEY` in your `.env` field is changed or lost, you will need to re-enter the credentials for each email service again.

SendPortal currently integrates with the following five email service providers:

- [AWS SES](/docs/v2/email-services/aws)
- [Postmark](/docs/v2/email-services/postmark)
- [Sendgrid](/docs/v2/email-services/sendgrid)
- [Mailgun](/docs/v2/email-services/mailgun)
- [Mailjet](/docs/v2/email-services/mailjet)

## Testing

You can test if an Email Service has been correctly configured by clicking on the `Test` button in the page that lists all of your Email Services.  

![/img/docs/providers/testing.png](/img/docs/providers/testing.png)

In order to test an Email Service you will have to provide the email address from which the email will be sent - this must be a verified email address or domain.
