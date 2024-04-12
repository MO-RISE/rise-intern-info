# Submitting timestamps to Deplide

## Login with keycloak

To authenticate with keycloak in order to submit timestamps, one need to gain an access token by using our keycloak instance at id.deplide.org. This is done a little differently for each platform but there is an android library available [here](https://github.com/openid/AppAuth-Android).

## Submitting messages

Once the token is aquired, timestamps can now be submitted to an endpoint. To submit a timestamp conforming to the TCMF, a POST-request needs to be sent to the address `https://arkady.deplide.org/cdm/update` with the header `Authorization: Bearer <token>`.

A curl request could look like this:

```
curl --location 'https://arkady.deplide.org/cdm/update' --header 'Content-Type: application/json' --header 'Authorization: Bearer eyJh...' --data-raw '{
  "payload": {
    "@type": "LocationState",
    "timeType": "planned",
    "referenceObject": "tcmf:reference_object:train:train_id:testtåget",
    "timeSequence": "departed_from",
    "location": "tcmf:location:station:Mgb:testspåret",
    "time": "2024-03-18T12:24:00.000Z"
  },
  "grouping": ["tcmf:grouping:train:train_id:testtåget"],
  "messageId": "tcmf:message:8463495a-027e-49c4-aaa3-4969f168f642",
  "reportedAt": "2024-03-18T08:25:00.797Z",
  "reportedBy": "tcmf:user:RISE:pontus_dev",
  "version": "0.0.7"
}'
```
