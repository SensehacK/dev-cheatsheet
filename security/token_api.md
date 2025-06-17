
# Token API

## Intro


## Best practices

### Secure Storage

Utilize apple [keychain](keychain.md) on apple ecosystem to persist the token with encryption.
Different techniques could be utilized for [secret_keys](secret_keys.md) in your application.


### Eager Initialization

On app launch, check for early fetch tokens, cache to improve quick network calls.
Make sure the expirations are checked so that you can renew / refresh your tokens.



### Timeout & Retry

### Cache & Refresh

### Scopes/Capabilities Usage

### Secret Rotation

### Environments

### Query Parameters

