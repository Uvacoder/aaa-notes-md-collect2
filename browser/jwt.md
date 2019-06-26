# JWT

https://jwt.io/introduction/

- Header(x)
- Payload(y)
- Signature (z)


xxxxx.yyyyy.zzzzz

## Header
header typically consists of two parts: 
- the type of the token
- hashing algorithm being used,
```
{
  "alg": "HS256",
  "typ": "JWT"
}
```
Encode with base64

## Payload
contains the claims.
- registered
- public
- private claims.

```
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```
Encode with base64

## Signature

```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```


The final will be
`
base64(header).base64(PAyload).base64(signature)
`