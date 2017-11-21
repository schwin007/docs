---
title: Associate a New Authenticator for Use with Multifactor Authentication
description: How to associate a new authenticator for use with MFA using the new MFA API endpoints
---
# Multifactor Authentication Challenges

You can, at any point, trigger MFA challenges for authenticators that you've enrolled by calling the `/mfa/challenges` endpoint.

## OTP Challenges

To trigger an OTP challenge, make the appropriate `POST` call to `mfa/challenge`.

```har
{
	"method": "POST",
	"url": "https://${account.namespace}/mfa/challenge",
	"postData": {
		"mimeType": "application/json",
		"text": "{ \"client_id\": \"YOUR_CLIENT_ID\", \"challenge_type\": \"otp\", \"mfa_token\": \"Fe26.2**05...\" }"
	}
}
```

If successful, you'll receive the following response: 

```json
{
  "challenge_type": "otp"
}
```

Proceed with the authentication process as usual.

## OOB Challenges

To trigger an OOB challenge, make the appropriate `POST` call to `mfa/challenge`.

```har
{
	"method": "POST",
	"url": "https://${account.namespace}/mfa/challenge",
	"postData": {
		"mimeType": "application/json",
		"text": "{ \"client_id\": \"YOUR_CLIENT_ID\", \"challenge_type\": \"oob\", \"authenticator_id\": \"sms|dev_s...O\", \"mfa_token\": \"Fe26.2**05...\" }"
	}
}
```

If successful, you'll receive the following response, as well as an SMS message containing the required six-digit code:

```json
{
  "challenge_type": "oob",
  "oob_code": "asdae35fdt5...oob_code_redacted",
  "binding_method": "prompt"
}
```

Proceed with the authentication process as usual.

## Posting the MFA Responses

You can post MFA OTP or MFA OOB responses using the `/oauth/token` endpoint.