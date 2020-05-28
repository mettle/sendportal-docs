# Email Services

## Introduction
SendPortal must be integrated with at least one email service provider in order for your emails to be dispatched. You can have multiple email services configured at one given time. For example, you may wish to send newsletters via SES and transactional emails via Postmark.

> The credentials for each email service is stored in an encrypted format in the database. If the `APP_KEY` in your `.env` field is changed or lost, you will need to re-enter the credentials for each email service again.

SendPortal currently integrates with the following four email service providers:

- [AWS SES](/docs/email-services/email-service-ses)
- [Postmark](/docs/email-services/email-service-postmark)
- [Sendgrid](/docs/email-services/email-service-sendgrid)
- [Mailgun](/docs/email-services/email-service-mailgun)
