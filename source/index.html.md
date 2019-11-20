---
title: Inspetor Docs

language_tabs: # must be one of https://git.io/vQNgJ
  - sh

includes:
  - using
  - collection-api.md.erb

search: true
---

# Introduction

Inspetor protects your company from losses due to fraud and chargebacks, all while maximizing revenue from valid purchases and maintaining the simple payment flow that your customers love. We accomplish this by making predictions based on past and present user behavior to evaluate the likelihood that a transaction is fraudulent. 

But we can't collect this information on our own--we need *you*, the user, to integrate our library into your code base so we can capture sufficient information to train our models. The more information we receive, the better the decision we can make, and the better we can protect your platform from fraud. Events like logins, profile updates, or even unrelated purchases on the same account all contribute to our assessment of a given transaction.

What follows is a general guide of how to integrate Inspetor's Client Library into your product. It should be sufficient for you to start with your Inspetor product integration. Should you find yourself in need of further assistance, do not hesitate to reach out to the Inspetor team--we will be happy to help!


