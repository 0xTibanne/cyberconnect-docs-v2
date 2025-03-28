---
id: user-login
title: User Login
slug: /guides/authentication/user-login
sidebar_label: User Login
sidebar_position: 2
description: Authentication - User Login
---

CyberConnect uses sign in with ethereum (SIWE) login flow for users to

1. send the on-chain transaction thru relay service. In this way, users would not need to pay for gas.
2. It’s also used while registering signing key for storing data offchain (follow).

## Login Flow

1. Send `loginGetMessage` request with following fields.

import ApolloCard from "@site/src/components/ApolloCard";

<ApolloCard queryName="loginGetMessage" />

2. Sign this message with the wallet you specified. Remember to replace \n with new lines. ([unescape json](https://www.freeformatter.com/json-escape.html#before-output)) Use the following tools to sign the message with your ETH wallet.

   1. Use [Etherscan tool](https://etherscan.io/verifiedSignatures#)
      ![siwe.png](/img/v2/siwe.png)
   2. Your familiar Ether.js, web3.js and other package

3. Verify the signature with gateway and save the token.

<ApolloCard queryName="loginVerify" />

## Next Step

The following `mutations` require `Authorization` header:

1. `registerSigningKey`
2. `createRegisterEssenceTypedData`
3. `createCollectEssenceTypedData`
4. `createSetEssenceDataTypedData`
5. `createSubscribeTypedData`
6. `createSetSubscribeDataTypedData`
7. `relay`

Use this personal access token in HTTP header `Authorization` . Don’t miss the `bearer` in front.

```json
{
  "Authorization": "bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJjaGFpbl9pZCI6MSwiZG9tYWluIjoiY3liZXJjb25uZWN0Lm1lIiwiYWRkcmVzcyI6IjB4OTI3ZjM1NTExNzcyMWUwRThBN2I1ZUEyMDAwMmI2NUI4YTU1MTg5MCIsImlzcyI6IkN5YmVyQ29ubmVjdCIsImV4cCI6MTY2NTA4NDU2MywiaWF0IjoxNjYyNDkyNTYzfQ.X3Y-gTTnsmpNRqkZ3vAAv3UOnHBb5WH5EZ2sOcJRPnw"
}
```
