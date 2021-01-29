# Quickstart Guide

## Introduction

The following guide will walk you through sending out your first campaign. It assumes that you have:

- successfully installed and configured SendPortal; and
- created your first user; and
- that you are logged in.

For more detailed instructions for each feature, refer to the relevant article in the Features section.

## Create An Email Service

SendPortal integrates with [Mailgun](/docs/email-services/mailgun), [Amazon SES](/docs/email-services/aws), [Sendgrid](/docs/email-services/sendgrid) and [Postmark](/docs/email-services/postmark).

> As per their [Terms of Service](https://postmarkapp.com/terms-of-service#email-types-that-we-dont-allow-on-postmark), Postmark should only be used for transactional mail, and not for marketing messages.

Click on the _Email Services_ link in the sidebar and then click the _Add Email Service_ button.

The required information will vary between each service. Full instructions on how to set up each service can be found in the [email service documentation](/docs/email-services/introduction).

## Add Or Import Subscribers

In order for SendPortal to send emails, you need to set up lists of [subscribers](/docs/features/subscribers). These subscribers can be added in 3 ways:

- Manually
- Through the API
- CSV Import

To add a single subscriber manually, click the _Subscribers_ link in the sidebar, and then click _New Subscriber_. You will need to provide an email address for the subscriber and ensure that `Subscribed` is checked. Once you are happy with your subscriber, click _Save_.

Refer to the [subscriber documentation](/docs/features/subscribers) for more information.

## Create A Template

A [template](/docs/features/templates) allows you to create consistent branding for all your campaigns, so that you only need to create new content for each campaign.

> Campaigns can be created without a template as well, if desired.

To create a template, click on the _Templates_ link in the sidebar and then click the _Add Template_ button. Templates should contain valid HTML and must include at least a `{{content}}` tag.

Refer to the [templates documentation](/docs/features/templates) for more information.

## Create A Campaign

To create a campaign, click on the _Campaigns_ link in the sidebar and then click the _New Campaign_ button.

If you have created a template in the previous step, you can select it here. The content will be placed into the `{{content}}` tag in the template.

Refer to the [campaign documentation](/docs/features/campaigns) for more information.

## Send The Campaign

After your campaign has been created, you will have a chance to review it before sending.

### Test Email

You can test the email by entering an address in the Test Email section and clicking _Send Test Email_.

### Recipients

Specify who the campaign should be sent to; either **All Subscribers,** or one or more **tags**.

### Schedule

Choose to dispatch the campaign immediately or at a specific and date and time.

### Sending Behaviour

Finally, you can choose to save each individual email as a draft message, or send it out immediately.

Choosing to save the message as a draft means you will will need to review and send each individual message before it is sent out.

Choosing to send the messages immediately will dispatch each message as soon as SendPortal is ready to do so.

## Next Steps

This covers the basics of how to set up your email services, templates, subscribers and campaigns.

For more detailed information on each of these items, please refer to the relevant Features section of the documentation.
