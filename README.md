# Fastly CBI Upload

## What it does

This policy will poll the Fastly APIs, download the invoice, service and usage data from the last *n* days within the current month, convert the data to the CBI CSV format, and upload them to the CBI Bill Upload API.

## Input Parameters

This policy has the following input parameters required when launching the policy:

- *Bill Connect ID* - The ID of the CBI Bill Connect for uploading bills (format: `cbi-oi-optima-*`)
- *Email Addresses* - The list of email addresses to notify

## Policy Actions

The following policy actions are taken on any resources found to be out of compliance:

- Upload Bill to Optima endpoint
- Send an email report

## Prerequisites

This policy uses [credentials](https://docs.flexera.com/flexera/EN/Automation/CredentialsIntro.htm)
for connecting to the cloud API -- in order to apply this policy you must have a credential
registered in the system that is compatible with this policy. If there are no credentials listed
when you apply the policy, please contact your cloud admin and ask them to register a credential
that is compatible with this policy. The information below should be consulted when creating the
credentials.

### Credentials

- Fastly API key with *Organization Member* and *Organization Read Only* permissions
  - Credential Type: *API Key*
  - Location: *Header*
  - Type: this should be left empty. If leaving this field empty does not allow you to 'Validate' the credential, enter a string into this field to 'Validate', then edit the credential again to remove the string.
  - Key: value of Fastly *API Key*
  - Provider: `fastly`
- Flexera One client credentials (for Service Account) or refresh token with `csm_bill_upload_admin` role
  - Credential Type: *OAuth2*
  - Grant Type: *Client Credentials* or *Refresh Token*
  - Token URL: `https://login.flexera.com/oidc/token` or `https://login.flexera.eu/oidc/token`
  - When grant type is *Client Credentials*:
    - Client Authentication Method: *Client ID & Secret*
    - Client ID: value of Flexera One Service Account client ID
    - Client Secret: value of Flexera One Service Account client secret
  - When grant type is *Refresh Token*:
    - Client Authentication Method: *Token*
    - Token: value of Flexera One refresh token
  - Provider: `flexera`

## Supported Clouds

- Fastly

## Cost

This Policy Template does not launch any instances, and so does not incur any cloud costs.
