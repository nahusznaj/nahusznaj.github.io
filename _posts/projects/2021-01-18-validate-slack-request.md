---
layout: article
title: Validate Slack requests
categories: projects
modified: 2021-01-01T16:28:11-04:00
tags: [python, slack]
comments: true
share: true
read_time: true
---

You can build a Slack app, but you should make it secure. See how to validate Slack's requests.

Slack's requests are signed. In the repo mentioned below, I show how to build the signature using the request's payload plus the signing key; and how to compare it with the signature that Slack sends in the request's headers.

I wrote this here because it took me a little while to figure out how to do it right: <https://github.com/nahusznaj/validate_slack_requests>