# Mailgun

## Sending Emails

When you first begin, Mailgun will automatically create a sandbox domain that you can use for sending, but to send using your own domain you'll need to create a custom domain. Select _Sending_ then _Domains_ from the menu on the left hand side, then click _Add New Domain_ (you'll need to add credit card details before this button appears).

[image:B56A1364-FF45-4A3F-AF0C-A6DE5CC5B2BD-999-000012D784DC4783/mailgun-1.png]

Enter the domain name, choose whichever region makes the most sense for you and click _Add Domain_.

[image:59FB1B8E-0DF9-476F-B524-1D45637F9B70-999-000012F173AEFB32/mailgun-2.png]

You'll now need to visit the site that you use to manage DNS for the domain provided (usually the domain registrar). The steps to do this are beyond the scope of this documentation as they vary from provider to provider, but you will need to create a `TXT` entry for the relevant domain and paste in the strings from the `Hostname` and `Enter This Value` columns. Once you've added these, click _Verify DNS Settings_.

[image:9F80D702-B38C-4C9B-9222-12AAE1F63A6D-999-0000138FB22A8931/mailgun-3.png]

You'll now need to copy the `Private API Key` from _Settings_ > _API Keys_

[image:06BA5E7D-91B8-4532-B531-582769E0DB59-999-0000148D840A90E9/mailgun-4.png]

Then paste this into your SendPortal provider configuration.

[image:2062680F-7A5B-437B-B51B-DC83F870E368-999-000014A4AF0A35A5/mailgun-5.png]

## Tracking

To enable tracking, select _Sending_ then _Webhooks_ from the menu and click the _Add Webhook_ button.

[image:64AF2CDB-ECCE-4089-B09F-69F0D590877E-999-000014ED8037B418/mailgun-6.png]

The URL depends on your domain, but must end with `/api/webhooks/mailgun`. For example, if SendPortal is installed at `https://campaigns.marketing.com`, then each webhook should point to `https://campaigns.marketing.com/api/webhooks/mailgun`.

[image:F45A3A77-F883-41EB-942C-ADC4D702E48F-999-0000152E08A127F5/mailgun-7.png]

You'll need to add an entry for each type of event you want to track, but the URL is the same for each of them.

[image:4857A0D9-9C85-43F9-B996-425495547C92-999-0000152F05591490/mailgun-8.png]

That's it! You're now setup to send and track e-mails using Mailgun.
