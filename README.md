# Contentful Cloudflare Webhook Purge

Guide for setting up a [Contentful](https://www.contentful.com/) webhook to purge [Cloudflare](https://www.cloudflare.com/) cache via payload customization.

## Contentful

[Contentful](https://www.contentful.com/) provides a content infrastructure for digital teams to power content in websites, apps, and devices. Unlike a CMS, Contentful was built to integrate with the modern software stack. It offers a central hub for structured content, powerful management and delivery APIs, and a customizable web app that enable developers and content creators to ship digital products faster.

Contentful is registered trademark of Contentful GmbH.

## Author

**Teemu Tammela**

* [teemu.tammela@auralcandy.net](mailto:teemu.tammela@auralcandy.net)
* [www.auralcandy.net](https://www.auralcandy.net/)
* [github.com/teemutammela](https://github.com/teemutammela)
* [t.me/teemutammela](http://t.me/teemutammela)

## Disclaimer

This guide comes with ABSOLUTELY NO WARRANTY. The author assumes no responsibility of data loss or any other unintended side-effect. This guide is based on [Cloudflare API V4](https://api.cloudflare.com/) and as such is subject to change.

## Prequisites

This guide assumes you have already created a [Cloudflare](https://www.cloudflare.com/) account and configured at least one domain.

**1)** Login to your Cloudflare account and select the domain you wish to apply the cache purge.

**2)** Select the _Overview_ page and find your _Zone ID_ under the section _API_.

**3)** Click the link _Get your API key_ under the section _API_ on the _Overview_ page.

**4)** Find _Global API Key_ under the section _API Keys_ and click the _View_ button.

## Installation

**1)** Install [Contentful CLI](https://github.com/contentful/contentful-cli).

**2)** Login to Contentful CLI and select the target space.

```shell
contentful login
contentful space use
```

**3)** Import webhook to target space.

```shell
contentful space import --content-file webhook.json
```

**4)** Go to _Space settings → Webhooks_ in your target space and confirm a webhook called _Purge Cloudflare Cache_ has been installed.

**5)** Select _View details → Webhook settings_.

**6)** Look for the URL `https://api.cloudflare.com/client/v4/zones/CLOUDFLARE_ZONE_ID/purge_cache` and replace the string `CLOUDFLARE_ZONE_ID` with your _Zoned ID_.

**7)** Look for the fields _X-Auth-Email_ and _X-Auth-Key_ under the section _Headers_ and replace them with Cloudflare account e-mail address and _API Key_.

**8)** Click _Save_ and test the webhook by publishing any entry. Verify the webhook is working as intended under the section _Activity log_.


**NOTE!** By default the webhook is configured to engage when an entry is updated. If you wish to change that behavior, you may edit the settings under the  

- by default master

**NOTE!** If you are delivering content from Contentful to multiple Cloudflare-enabled domains, you need to install a webhook for each domain that have unique _Zone IDs_ and _API Keys_. If you are installing multiple webhooks to the same space, it's highly recommend to change their names from _Purge Cloudflare Cache_ to e.g. _Purge Cloudflare Cache (Site Name)_ after installation.