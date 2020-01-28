[@ew-did-registry/claims](../README.md) › [Globals](../globals.md) › [ClaimsUser](claimsuser.md)

# Class: ClaimsUser

## Hierarchy

* [Claims](claims.md)

  ↳ **ClaimsUser**

## Implements

* [IClaims](../interfaces/iclaims.md)
* [IClaimsUser](../interfaces/iclaimsuser.md)

## Index

### Constructors

* [constructor](claimsuser.md#constructor)

### Properties

* [curve](claimsuser.md#curve)
* [did](claimsuser.md#did)
* [g](claimsuser.md#g)
* [jwt](claimsuser.md#jwt)
* [keys](claimsuser.md#keys)
* [paranoia](claimsuser.md#paranoia)
* [q](claimsuser.md#q)

### Methods

* [createPrivateClaim](claimsuser.md#createprivateclaim)
* [createProofClaim](claimsuser.md#createproofclaim)
* [createPublicClaim](claimsuser.md#createpublicclaim)
* [getDocument](claimsuser.md#getdocument)
* [verifyPrivateClaim](claimsuser.md#verifyprivateclaim)
* [verifyPublicClaim](claimsuser.md#verifypublicclaim)
* [verifySignature](claimsuser.md#verifysignature)

## Constructors

###  constructor

\+ **new ClaimsUser**(`keys`: IKeys, `resolver`: IResolver): *[ClaimsUser](claimsuser.md)*

*Inherited from [Claims](claims.md).[constructor](claims.md#constructor)*

Defined in claims/src/claims/claims.ts:29

**`constructor`** 

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`keys` | IKeys | user key pair |
`resolver` | IResolver |   |

**Returns:** *[ClaimsUser](claimsuser.md)*

## Properties

###  curve

• **curve**: *sjcl.SjclEllipticalCurve* =  sjcl.ecc.curves.k256

Defined in claims/src/claimsUser/claimsUser.ts:21

___

###  did

• **did**: *string*

*Implementation of [IClaimsUser](../interfaces/iclaimsuser.md).[did](../interfaces/iclaimsuser.md#did)*

*Inherited from [Claims](claims.md).[did](claims.md#did)*

Defined in claims/src/claims/claims.ts:29

___

###  g

• **g**: *any* =  this.curve.G

Defined in claims/src/claimsUser/claimsUser.ts:25

___

###  jwt

• **jwt**: *IJWT*

*Implementation of [IClaimsUser](../interfaces/iclaimsuser.md).[jwt](../interfaces/iclaimsuser.md#jwt)*

*Inherited from [Claims](claims.md).[jwt](claims.md#jwt)*

Defined in claims/src/claims/claims.ts:22

jwt stores the JWT to manage web tokens

___

###  keys

• **keys**: *IKeys*

*Implementation of [IClaimsUser](../interfaces/iclaimsuser.md).[keys](../interfaces/iclaimsuser.md#keys)*

*Inherited from [Claims](claims.md).[keys](claims.md#keys)*

Defined in claims/src/claims/claims.ts:27

Key pair represents the implementation of key management interface

___

###  paranoia

• **paranoia**: *number* = 6

Defined in claims/src/claimsUser/claimsUser.ts:27

___

###  q

• **q**: *any* =  this.curve.r

Defined in claims/src/claimsUser/claimsUser.ts:23

## Methods

###  createPrivateClaim

▸ **createPrivateClaim**(`publicData`: [IClaimData](../interfaces/iclaimdata.md), `privateData`: [IClaimData](../interfaces/iclaimdata.md), `issuer`: string): *Promise‹object›*

*Implementation of [IClaimsUser](../interfaces/iclaimsuser.md)*

Defined in claims/src/claimsUser/claimsUser.ts:84

Used by the claim subject to create token with subject encrypted
private data and public data which afterwards will be sent to the issuer.
Salted private fields will be saved in the `saltedFields` argument

**`example`** 
```typescript
import { ClaimsUser } from '@ew-did-registry/claims';
import { Keys } from '@ew-did-registry/keys';

const user = new Keys();
const claims = new ClaimsUser(user);
const privateData = {
    licence: 'abc123'
};
const publicData = {
    name: 'John'
};
const claim = await claims.createPrivateClaim(publicData, privateData, issuer);
```

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`publicData` | [IClaimData](../interfaces/iclaimdata.md) | subject public data |
`privateData` | [IClaimData](../interfaces/iclaimdata.md) | subject private data |
`issuer` | string |   |

**Returns:** *Promise‹object›*

> } token with private data encrypted by issuer key

___

###  createProofClaim

▸ **createProofClaim**(`claimUrl`: string, `saltedFields`: object): *Promise‹string›*

Defined in claims/src/claimsUser/claimsUser.ts:134

Used by the claim subject based on the salted values calculated
when creating private claim

**`example`** 
```typescript
import { ClaimsUser } from '@ew-did-registry/claims';
import { Keys } from '@ew-did-registry/keys';

const user = new Keys();
const claims = new ClaimsUser(user);
const claimUrl = 'http://example.com';
const saltedFields = {
   secret: '123abc'
};
const claim = await claims.createProofClaim(claimUrl, saltedFields);
```

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`claimUrl` | string | url of previously saved token |
`saltedFields` | object | - |

**Returns:** *Promise‹string›*

___

###  createPublicClaim

▸ **createPublicClaim**(`publicData`: [IClaimData](../interfaces/iclaimdata.md)): *Promise‹string›*

*Implementation of [IClaimsUser](../interfaces/iclaimsuser.md)*

Defined in claims/src/claimsUser/claimsUser.ts:49

Creates token with data about subject provided in claimData

**`example`** 
```typescript
import { ClaimsUser } from '@ew-did-registry/claims';
import { Keys } from '@ew-did-registry/keys';

const user = new Keys();
const claims = new ClaimsUser(user);
const claimData = {
    name: 'John'
};
const token = await claims.createPublicClaim(claimData);
```

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`publicData` | [IClaimData](../interfaces/iclaimdata.md) |   |

**Returns:** *Promise‹string›*

___

###  getDocument

▸ **getDocument**(`did`: string): *Promise‹IDIDDocument›*

*Inherited from [Claims](claims.md).[getDocument](claims.md#getdocument)*

Defined in claims/src/claims/claims.ts:61

Fetches DID document of the corresponding DID

**`example`** 
```typescript
import { Keys } from '@ew-did-registry/keys';
import { Claims } from '@ew-did-registry/claims';

const user = new Keys();
const claims = new Claims(user);
const did = `did:${Networks.Ethereum}:user_id`;
const document = await claims.getDocument(did);
```

**Parameters:**

Name | Type |
------ | ------ |
`did` | string |

**Returns:** *Promise‹IDIDDocument›*

___

###  verifyPrivateClaim

▸ **verifyPrivateClaim**(`token`: string, `saltedFields`: object, `publicData`: [IClaimData](../interfaces/iclaimdata.md)): *Promise‹void›*

Defined in claims/src/claimsUser/claimsUser.ts:213

Verifies token with private data received from issuer

**`example`** 
```typescript
import { ClaimsUser } from '@ew-did-registry/claims';
import { Keys } from '@ew-did-registry/keys';

const user = new Keys();
const claims = new UserClaims(user);
const verified = await claims.verifyPrivateToken(issuedToken);
```

**`throw`** if the proof failed

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`token` | string | issued token |
`saltedFields` | object | - |
`publicData` | [IClaimData](../interfaces/iclaimdata.md) | - |

**Returns:** *Promise‹void›*

___

###  verifyPublicClaim

▸ **verifyPublicClaim**(`token`: string, `verifyData`: [IClaimData](../interfaces/iclaimdata.md)): *Promise‹void›*

*Implementation of [IClaimsUser](../interfaces/iclaimsuser.md)*

Defined in claims/src/claimsUser/claimsUser.ts:176

Verifies token received from issuer

**`example`** 
```typescript
import { ClaimsUser } from '@ew-did-registry/claims';
import { Keys } from '@ew-did-registry/keys';

const user = new Keys();
const claims = new UserClaims(user);
const verified = await claims.verifyPublicToken(issuedToken);
```

**`throws`** if the proof failed

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`token` | string | issued token |
`verifyData` | [IClaimData](../interfaces/iclaimdata.md) | - |

**Returns:** *Promise‹void›*

___

###  verifySignature

▸ **verifySignature**(`token`: string, `signer`: string): *Promise‹boolean›*

*Inherited from [Claims](claims.md).[verifySignature](claims.md#verifysignature)*

Defined in claims/src/claims/claims.ts:83

Verifies signers signature on received token

**`example`** 
```typescript
import { Keys } from '@ew-did-registry/keys';
import { Claims } from '@ew-did-registry/claims';

const user = new Keys();
const claims = new Claims(user);
const verified = claims.verifySignature(token, userDid);
```

**Parameters:**

Name | Type | Description |
------ | ------ | ------ |
`token` | string | token signature on which you want to check |
`signer` | string | did of the signer  |

**Returns:** *Promise‹boolean›*