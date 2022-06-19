---
date: 2022-05-15T08:48:08+01:00
description: "SOLID by example"
featured_image: "/images/compare-fibre-jlrnBE3Jn3o-unsplash.jpg"
images:
- /images/pascal-swier-7de474KZIbs-unsplash.jpg
tags: ["SOLID", "PDV", "Distributed Web"]
title: "A quick look on how the SOLID protocol works"
draft: true
---

### How does the SOLID protocol work ?

This is a research question currently at hand and I'd like to take you along in the journey.

SOLID is a set of protocols that allows people to create a distributed web. Content remains at its owner inside a "POD" and it is possible to combine data in different PODs into a sinlge web applicaton. 

### OK, so what do I need to know ?

Next to the POD, it is handy to know that you access a POD based on a WebID, for PODs that is your unique identity. Luckily it is possible to use OIDC (Open ID Connect) to login in order to the WebID as a token of your identity. 

And the other important thing is that the contents inside a POD is structured according to the [Linked Data](https://www.w3.org/TR/ldp/) and [RDF](https://www.w3.org/TR/rdf11-concepts/) specifications. 

### Lets start with the examples

For these samples, the [Solid community server](https://github.com/solid/community-server) is used. 

#### Intial things that happen 

Registered:

https://olger.solidweb.org/

WebID: https://olger.solidweb.org/profile/card#me

Inside the app these headers are passed to the solid server

Request to olger.solidweb.org -> returns a turtle file
```
Authorization: DPoP eyJhbGciOiJSUzI1NiIsImtpZCI6IjZENjVERmtuQk0wIn0.eyJpc3MiOiJodHRwczovL3NvbGlkd2ViLm9yZyIsImF1ZCI6InNvbGlkIiwic3ViIjoiaHR0cHM6Ly9vbGdlci5zb2xpZHdlYi5vcmcvcHJvZmlsZS9jYXJkI21lIiwiZXhwIjoxNjQzNDg5NDc4LCJpYXQiOjE2NDIyNzk4NzgsImp0aSI6ImY2YmYzMGRlZTBiNWJjZjIiLCJjbmYiOnsiamt0IjoiTnNKenVoWk54Q01UT0dOQjgteHh0VDFpcklrWTFNVWU0U3Y3ajFkLUw4ZyJ9LCJjbGllbnRfaWQiOiI0NTEwZWM4YzY0Y2ZiNTZlYWVhMGUyNmQ0Y2I1YzNiZSIsIndlYmlkIjoiaHR0cHM6Ly9vbGdlci5zb2xpZHdlYi5vcmcvcHJvZmlsZS9jYXJkI21lIn0.iJkx63wVqnPKak3sq_i7Fa15lumI7un0t5kmekdL4T4C0ORP-RnlJfYyF3KmsZ9DjQnoQFNkhUzEo3C93m09LvUInqd0DzHM0sTwgxM3QKgLySqgpMHIX107Q0buu8OaIJnJIOKcJKxjBUbIugiqwA49KO1NY6QK9gckKK0VRIqOchJC6B2aaA7fla1KKp5x2EVX4I5bhAZripkGgxdKrVxsw_SpCe_fweoZLIgJeLQ7EjyGr_GgaTbIp-RTbMPyxKu2Q6X8BQ2eVp9RTv7HLbVnJybbherT2iGDu3E4QvM2A8uihnqr8rT_2-KgtvHdKKxVi1Avs-ozELAacK4qfg

{
  "iss": "https://solidweb.org",
  "aud": "solid",
  "sub": "https://olger.solidweb.org/profile/card#me",
  "exp": 1643489478,
  "iat": 1642279878,
  "jti": "f6bf30dee0b5bcf2",
  "cnf": {
    "jkt": "NsJzuhZNxCMTOGNB8-xxtT1irIkY1MUe4Sv7j1d-L8g"
  },
  "client_id": "4510ec8c64cfb56eaea0e26d4cb5c3be",
  "webid": "https://olger.solidweb.org/profile/card#me"
}
```

```
dpop: eyJhbGciOiJFUzI1NiIsImp3ayI6eyJjcnYiOiJQLTI1NiIsImt0eSI6IkVDIiwieCI6IllrdzVIc2lUMVoyRXU4dDVHU01VdmRxNWhuTU5DN0RwYW84dWlwcE5pNkEiLCJ5IjoiejctalVkQXZBNzVOdExxTG1LX2VjMVZ4RUVkdlN4N0dETFNyNlhRVUp6dyIsImFsZyI6IkVTMjU2In0sInR5cCI6ImRwb3Arand0In0.eyJodHUiOiJodHRwczovL29sZ2VyLnNvbGlkd2ViLm9yZy8iLCJodG0iOiJHRVQiLCJqdGkiOiJhNTk1MzViZS03NDc5LTRiMDctYWFkZS00ZGEwYTJmNzNkMmQiLCJpYXQiOjE2NDIyNzk4Nzh9.UxknEkuQ6EKKXn7eYCV6xDkJpLJJWyTcIMHBdNJnxUjFZ9zjiEViZhe0J0C5SwiZ0wd4gz-wF9uVPICJxZ-XpA

{
  "alg": "ES256",
  "jwk": {
    "crv": "P-256",
    "kty": "EC",
    "x": "Ykw5HsiT1Z2Eu8t5GSMUvdq5hnMNC7Dpao8uippNi6A",
    "y": "z7-jUdAvA75NtLqLmK_ec1VxEEdvSx7GDLSr6XQUJzw",
    "alg": "ES256"
  },
  "typ": "dpop+jwt"
}
{
  "htu": "https://olger.solidweb.org/",
  "htm": "GET",
  "jti": "a59535be-7479-4b07-aade-4da0a2f73d2d",
  "iat": 1642279878
}
```

Request to privateTypeIndex.ttl give different dpop

```
{
  "alg": "ES256",
  "jwk": {
    "crv": "P-256",
    "kty": "EC",
    "x": "Ykw5HsiT1Z2Eu8t5GSMUvdq5hnMNC7Dpao8uippNi6A",
    "y": "z7-jUdAvA75NtLqLmK_ec1VxEEdvSx7GDLSr6XQUJzw",
    "alg": "ES256"
  },
  "typ": "dpop+jwt"
}
{
  "htu": "https://olger.solidweb.org/settings/privateTypeIndex.ttl",
  "htm": "GET",
  "jti": "77e97713-38e8-48ab-9e77-bc0a4f628279",
  "iat": 1642279879
}
```


#### The WebID required to access a POD



  
Photo by [Compare Fibre](hhttps://unsplash.com/@comparefibre) on Unsplash
