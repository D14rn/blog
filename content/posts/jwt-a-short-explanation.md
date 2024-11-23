+++
date = '2024-11-23T11:21:08+01:00'
draft = false
title = 'JWT: A Short Explanation'
+++

## Introduction
This article aims to be a short explanation of the three parts (header, payload, signature) of a JSON Web Token, how they are generated and validated.

## Anatomy Overview
A JWT consists of three parts, each delimited by a "." (dot) like the following:\
`header.payload.signature`

## Basic overview of the three parts

### Header
The header of a JWT usually contains the signing algorithm that was used, the type of the token, in this case "JWT" and optionally, if signed, a "Key ID" (kid).

Base64url-decoding the JWT header produces the following:
```json
{
    "typ": "JWT",
    "alg": "HS256"
}
```

### Payload
The payload of a JWT contains a set of claims being made.
Different types of claims:
- [Registered claims](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1): standardised and recommended, like 'iss', 'sub', 'exp'.
- [Public claims](https://datatracker.ietf.org/doc/html/rfc7519#section-4.2): non-registered claims that should be collision-resistant, like 'preferred_username', 'roles', 'email'.
    - Some are defined in the [IANA "JSON Web Token Claims" registry](https://www.iana.org/assignments/jwt/jwt.xhtml).
- [Private claims](https://datatracker.ietf.org/doc/html/rfc7519#section-4.3): non-registered claims without care for collisions.

Base64url-decoding the JWT payload produces the following:
```json
{
    "iss": "joe",
    "exp": 1300819380,
    "http://example.com/is_root": true
}
```

### Signature
The signature of a JWT ensures the token hasn't been tampered with, and, if signed, can be used to verify the identity of the JWT's sender.

Example base64url-encoded signature:
```
dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```

### Everything put together
Payload, Header and signature base64url-encoded:
```
eyJ0eXAiOiJKV1QiLA0KICJhbGciOiJIUzI1NiJ9
.
eyJpc3MiOiJqb2UiLA0KICJleHAiOjEzMDA4MTkzODAsDQogImh0dHA6Ly9leGFtcGxlLmNvbS9pc19yb290Ijp0cnVlfQ
.
dBjftJeZ4CVP-mB92K27uhbUJU1p1r_wW1gFWFOEjXk
```

## Generating the token
### Header & Payload
The header and payload are each encoded using [base64url encoding](https://datatracker.ietf.org/doc/html/rfc4648#section-5) and then joined together with a "." (dot) (**JWS Signing Input**).

(header)
```json
{
    "typ": "JWT",
    "alg": "HS256"
}
```
\+ (payload)
```json
{
    "iss": "joe",
    "exp": 1300819380,
    "http://example.com/is_root": true
}
```
becomes
```
eyJ0eXAiOiJKV1QiLA0KICJhbGciOiJIUzI1NiJ9.eyJpc3MiOiJqb2UiLA0KICJleHAiOjEzMDA4MTkzODAsDQogImh0dHA6Ly9leGFtcGxlLmNvbS9pc19yb290Ijp0cnVlfQ
```

### Signature creation
[RFC reference](https://datatracker.ietf.org/doc/html/rfc7515#section-5.1)

The signature is generated using the following (simplified) process:
1. Join the base64url-encoded header and base64url-encoded payload with a "." (dot) (**JWS Signing Input**).
2. Compute the MAC of the previous value by applying the specified algorithm (ex: HS256, RS256) with the secret or private key.
3. Base64url-encode the resulting signature from the previous step.

Examples:
- ex: base64url(HS256(base64url(header) + "." + base64url(payload), secret_key))
- ex: base64url(RS256(base64url(header) + "." + base64url(payload), private_key))

## Verifying the token
[RFC reference](https://datatracker.ietf.org/doc/html/rfc7515#section-5.2)

The JWT is verified using the following (simplified) process:
1. Extract all three parts of the JWT.
2. Base64url-decode the header and retrieve the "alg" to use.
3. Join the base64url-encoded header and base64url-encoded payload with a "." (dot) (JWS Signing Input).
4. Use the validation method defined for the algorithm being used.
    - HS256 (symmetric):
        - The signature is **reproduced** by hashing the JWS Signing Input with the shared secret key.
        - The reproduced signature is then **compared** to the signature in the JWT.
    - RS256 (asymmetric):
        - The JWT's signature is **decrypted** using the public key, exposing a SHA256 hash.
        - A **new** SHA256 hash is **computed** from the JWS Signing Input of the JWT.
        - If both hashes **match**, the token is **validated**.

## Conclusion
I hope this article provided a clear and helpful introduction to the basic principles of JSON Web Tokens.
For a deeper understanding and to verify the information yourself, I recommend you to experiment with JWT and read the relevant RFC standards.

## Quick references

### Links
- [RFC 4648 (base64url encoding)](https://datatracker.ietf.org/doc/html/rfc4648#section-5)
- [RFC 7515 / JSON Web Signature (JWS)](https://datatracker.ietf.org/doc/html/rfc7515)
- [RFC 7519 / JSON Web Token (JWT)](https://datatracker.ietf.org/doc/html/rfc7519)
- [Introduction to JWT](https://jwt.io/introduction)
- [JWT Debugger](https://jwt.io/#debugger-io)