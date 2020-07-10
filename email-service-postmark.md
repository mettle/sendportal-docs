# Postmark

## Sending Email

To send e-mails using the Postmark provider, you will need a Postmark account. If you don't already have an account, visit the [Postmark website](https://postmarkapp.com/) and click the _Start Free Trial_ button in the top right corner of the screen.

Postmark will automatically create a server for you, called `My First Server`. Click on the server and select the _API Tokens_ tab.

![https://sendportal.io/img/docs/providers/postmark/postmark-1.png](https://sendportal.io/img/docs/providers/postmark/postmark-1.png)

Copy the string from `Server API tokens` and create a provider within SendPortal.

![https://sendportal.io/img/docs/providers/postmark/postmark-2.png](https://sendportal.io/img/docs/providers/postmark/postmark-2.png)

Next, navigate to _Sender Signatures_ and select the option to _Add Domain_.

![https://sendportal.io/img/docs/providers/postmark/postmark-3.png](https://sendportal.io/img/docs/providers/postmark/postmark-3.png)

Enter your domain name and click _Verify domain_.

![https://sendportal.io/img/docs/providers/postmark/postmark-4.png](https://sendportal.io/img/docs/providers/postmark/postmark-4.png)

You'll now need to visit the site that you use to manage DNS for the domain provided (usually the domain registrar). The steps to do this are beyond the scope of this documentation as they vary from provider to provider, but you will need to create a `TXT` entry for the relevant domain and paste in the strings from the `Hostname` and `Add this value` columns.

![https://sendportal.io/img/docs/providers/postmark/postmark-5.png](https://sendportal.io/img/docs/providers/postmark/postmark-5.png)

Once you've added the entry with your DNS provider, click the _Verify_ button and the DKIM status should transition to `Verified`. It can take some time to make this transition, but if it doesn't work ensure you didn't accidentally copy and paste any whitespace at the beginning or end of either string.

![https://sendportal.io/img/docs/providers/postmark/postmark-6.png](https://sendportal.io/img/docs/providers/postmark/postmark-6.png)

To configure e-mail tracking, select the server from the `Servers` page, select the `Transactional` (`Default Transactional Stream`) stream from the list of `Message Streams`.

![https://sendportal.io/img/docs/providers/postmark/postmark-7.png](https://sendportal.io/img/docs/providers/postmark/postmark-7.png)

Select the _Webhooks_ tab and click _Add webhook_.

![https://sendportal.io/img/docs/providers/postmark/postmark-8.png](https://sendportal.io/img/docs/providers/postmark/postmark-8.png)

The `Webhook URL` depends on your domain, but must end with `/api/v1/webhooks/postmark`. For example, if SendPortal is installed at `https://campaigns.marketing.com`, then each webhook should point to `https://campaigns.marketing.com/api/v1/webhooks/postmark`.

![https://sendportal.io/img/docs/providers/postmark/postmark-9.png](https://sendportal.io/img/docs/providers/postmark/postmark-9.png)

You'll also need to enable open tracking and link tracking from the stream settings.

![https://sendportal.io/img/docs/providers/postmark/postmark-10.png](https://sendportal.io/img/docs/providers/postmark/postmark-10.png)

That's it! You're now setup to send and track e-mails using Postmark.
