# @ohos.security.cryptoFramework (Crypto Framework)

The **cryptoFramework** module shields underlying hardware and algorithm libraries and provides unified APIs for cryptographic operations.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9.

## Modules to Import

```js
import cryptoFramework from "@ohos.security.cryptoFramework"
```

## Result

 Enumerates the operation results.

 **System capability**: SystemCapability.Security.CryptoFramework

| Name                                 |    Value  |   Description                        |
| ------------------------------------- | -------- | ---------------------------- |
| INVALID_PARAMS                        | 401      | Invalid parameter.                  |
| NOT_SUPPORT                           | 801      | Unsupported operation.                |
| ERR_OUT_OF_MEMORY                     | 17620001 | Memory error.                  |
| ERR_RUNTIME_ERROR                     | 17620002 | Runtime error.            |
| ERR_CRYPTO_OPERATION                  | 17630001 | Failed to invoke the third-party cryptographic API.    |

## DataBlob

Defines a binary data array.

 **System capability**: SystemCapability.Security.CryptoFramework

| Name| Type      | Readable| Writable| Description  |
| ---- | ---------- | ---- | ---- | ------ |
| data | Uint8Array | Yes  | Yes  | Binary data array. |

## ParamsSpec

Defines the parameters used for encryption and decryption. <br>For the symmetric encryption and decryption modes that require parameters such as the initialization vector (IV), you need to construct a child class object and pass it to [init()](#init-2). If the IV is not required (for example, the ECB mode), pass in **null** in [init()](#init-2).

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Yes  | Symmetric encryption and decryption parameters. Options:<br>- **IvParamsSpec**: applicable to the CBC, CTR, OFB, and CFB modes.<br>- **GcmParamsSpec**: applicable to the GCM mode.<br>- **CcmParamsSpec**: applicable to the CCM mode.|

> **NOTE**
>
> The **params** parameter in [init()](#init-2) is of the **ParamsSpec** type (parent class). However, a specific child class object (such as **IvParamsSpec**) needs to be passed in. When constructing the child class object, you need to set **algName** for the parent class **ParamsSpec** to specify the child class object in **init()**.

## IvParamsSpec

Defines the child class of [ParamsSpec](#paramsspec). It is used as the parameters of [init()](#init-2) during symmetric encryption and decryption. <br>**IvParamsSpec** applies to the encryption and decryption modes such as CBC, CTR, OFB, and CFB, which use only the IV.

**System capability**: SystemCapability.Security.CryptoFramework

| Name| Type                 | Readable| Writable| Description                                                        |
| ---- | --------------------- | ---- | ---- | ------------------------------------------------------------ |
| iv   | [DataBlob](#datablob) | Yes  | Yes  | IV for encryption and decryption. Options:<br>- AES CBC, CTR, OFB, or CFB mode: 16-byte IV<br>- 3DES CBC, OFB, or CFB mode: 8-byte IV<br>- SM4<sup>10+</sup>CBC, CTR, OFB, or CFB mode: 16-byte IV|

> **NOTE**
>
> Before passing [init()](#init-2), specify **algName** for its parent class [ParamsSpec](#paramsspec).

## GcmParamsSpec

Defines the child class of [ParamsSpec](#paramsspec). It is used as the parameters of [init()](#init-2) during symmetric encryption and decryption. <br>**GcmParamsSpec** applies to the GCM mode.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type                 | Readable| Writable| Description                                                        |
| ------- | --------------------- | ---- | ---- | ------------------------------------------------------------ |
| iv      | [DataBlob](#datablob) | Yes  | Yes  | IV, which is of 12 bytes.                            |
| aad     | [DataBlob](#datablob) | Yes  | Yes  | Additional authentication data (AAD), which is of 8 bytes.                            |
| authTag | [DataBlob](#datablob) | Yes  | Yes  | Authentication tag, which is of 16 bytes.<br>When the GCM mode is used for encryption, the last 16 bytes of the [DataBlob](#datablob) output by [doFinal()](#dofinal-2) are used as the **authTag** in [GcmParamsSpec](#gcmparamsspec) of [init()](#init-2). |

> **NOTE**
>
> Before passing [init()](#init-2), specify **algName** for its parent class [ParamsSpec](#paramsspec).

## CcmParamsSpec

Defines the child class of [ParamsSpec](#paramsspec). It is used as the parameters of [init()](#init-2) during symmetric encryption and decryption. <br>**CcmParamsSpec** applies to the CCM mode.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type                 | Readable| Writable| Description                                                        |
| ------- | --------------------- | ---- | ---- | ------------------------------------------------------------ |
| iv      | [DataBlob](#datablob) | Yes  | Yes  | IV, which is of 7 bytes.                             |
| aad     | [DataBlob](#datablob) | Yes  | Yes  | Additional authentication data (AAD), which is of 8 bytes.                            |
| authTag | [DataBlob](#datablob) | Yes  | Yes  | Authentication tag, which is of 12 bytes.<br>When the CCM mode is used for encryption, the last 12 bytes of the [DataBlob](#datablob) output by [doFinal()](#dofinal-2) are used as the **authTag** in [CcmParamsSpec](#ccmparamsspec) of [init()](#init-2).|

> **NOTE**
>
> Before passing [init()](#init-2), specify **algName** for its parent class [ParamsSpec](#paramsspec).

## CryptoMode

Enumerates the cryptographic operations.

**System capability**: SystemCapability.Security.CryptoFramework

| Name        | Value  | Description              |
| ------------ | ---- | ------------------ |
| ENCRYPT_MODE | 0    | Encryption.|
| DECRYPT_MODE | 1    | Decryption.|

## AsyKeySpecItem<sup>10+</sup>

Enumerates the key parameters.

**System capability**: SystemCapability.Security.CryptoFramework

| Name        | Value  | Description            |
| ------------ | ---- | ---------------- |
| DSA_P_BN | 101 | Prime modulus **p** in the DSA algorithm.|
| DSA_Q_BN | 102 | Parameter **q** (prime factor of p – 1) in the DSA algorithm.|
| DSA_G_BN | 103 | Parameter **g** in the DSA algorithm.|
| DSA_SK_BN | 104 | Private key **sk** in the DSA algorithm.|
| DSA_PK_BN | 105 | Public key **pk** in the DSA algorithm.|
| ECC_FP_P_BN | 201 | Prime number **p** in the **Fp** fields of the elliptic curve in the DSA algorithm.|
| ECC_A_BN | 202 | First coefficient **a** of the elliptic curve in the DSA algorithm.|
| ECC_B_BN | 203 | Second coefficient **b** of the elliptic curve in the DSA algorithm.|
| ECC_G_X_BN | 204 | X coordinate of the base point **g** in the ECC algorithm.|
| ECC_G_Y_BN | 205 | Y coordinate of the base point **g** in the ECC algorithm.|
| ECC_N_BN | 206 | Order **n** of the base point **g** in the ECC algorithm.|
| ECC_H_NUM | 207 | Cofactor **h** in the ECC algorithm.|
| ECC_SK_BN | 208 | Private key **sk** in the ECC algorithm.|
| ECC_PK_X_BN | 209 | X coordinate of the public key **pk** (a point on the elliptic curve) in the ECC algorithm.|
| ECC_PK_Y_BN | 210 | Y coordinate of the public key **pk** (a point on the elliptic curve) in the ECC algorithm.|
| ECC_FIELD_TYPE_STR | 211 | Elliptic curve field type in the ECC algorithm. Currently, only the **Fp** field is supported.|
| ECC_FIELD_SIZE_NUM | 212 | Size of the field in the ECC algorithm, in bits.<br>**NOTE**<br>For the **Fp** field, the field size is the length of the prime **p**, in bits. |
| ECC_CURVE_NAME_STR | 213 | SECG curve name in the ECC algorithm.|
| RSA_N_BN | 301 | Modulus **n** in the RSA algorithm.|
| RSA_SK_BN | 302 | Private key **sk** (private key exponent **d**) in the RSA algorithm.|
| RSA_PK_BN | 303 | Public key **pk** (public key exponent **e**) in the RSA algorithm.|

## AsyKeySpecType<sup>10+</sup>

Enumerates the key parameter types.

**System capability**: SystemCapability.Security.CryptoFramework

| Name        | Value  | Description            |
| ------------ | ---- | ---------------- |
| COMMON_PARAMS_SPEC | 0 | Common parameters contained in the public and private keys. You can use [generateKeyPair()](#generatekeypair-2) to randomly generate a key pair based on the parameters of this type.|
| PRIVATE_KEY_SPEC | 1 | Parameter contained in the private key. You can use [generatePriKey()](#generateprikey) to generate a private key based on the parameters of this type.|
| PUBLIC_KEY_SPEC | 2 | Parameter contained in the public key. You can use [generatePubKey()](#generatepubkey) to generate a public key based on the parameters of this type.|
| KEY_PAIR_SPEC | 3 | All parameters contained in the public and private keys. You can use [generateKeyPair](#generatekeypair-2) to generate a key pair based on the parameters of this type.|

## CipherSpecItem<sup>10+</sup>

Enumerates the cipher parameters. You can use [setCipherSpec](#setcipherspec10) to set cipher parameters, and use [getCipherSpec](#getcipherspec10) to obtain cipher parameters. <br>Currently, only the RSA is supported. For details, see [Encryption and Decryption Specifications](../../security/cryptoFramework-overview.md#encryption-and-decryption-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

| Name        | Value  | Description            |
| ------------ | ---- | ---------------- |
| OAEP_MD_NAME_STR | 100 | Name of the message digest algorithm when the PKCS1_OAEP padding mode is used in the RSA.|
| OAEP_MGF_NAME_STR | 101 | Mask generation algorithm when the PKCS1_OAEP padding mode is used in the RSA. Currently, only MGF1 is supported.|
| OAEP_MGF1_MD_STR | 102 | Message digest algorithm for the MGF1 mask generation when the PKCS1_OAEP padding mode is used in the RSA.|
| OAEP_MGF1_PSRC_UINT8ARR | 103 | **pSource** byte stream when the PKCS1_OAEP padding mode is used in the RSA.|

## SignSpecItem<sup>10+</sup>

Enumerates the parameters for signing and signature verification. You can use [setSignSpec](#setsignspec10) and [setVerifySpec](#setverifyspec10) to set these parameters, and use [getSignSpec](#getsignspec10) and [getVerifySpec](#getverifyspec10) to obtain the parameters. <br>Currently, only the RSA is supported. For details, see [Encryption and Decryption Specifications](../../security/cryptoFramework-overview.md#encryption-and-decryption-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

| Name        | Value  | Description            |
| ------------ | ---- | ---------------- |
| PSS_MD_NAME_STR | 100 | Name of the message digest algorithm when the PSS padding mode is used in the RSA.|
| PSS_MGF_NAME_STR | 101 | Mask generation algorithm when the PSS padding mode is used in the RSA. Currently, only MGF1 is supported.|
| PSS_MGF1_MD_STR | 102 | Message digest parameters for the MGF1 mask generation when the PSS padding mode is used in the RSA.|
| PSS_SALT_LEN_NUM | 103 | Length of the salt in bytes when the PSS padding mode is used in the RSA.|
| PSS_TRAILER_FIELD_NUM | 104 | Integer used for encoding when the PSS padding mode is used in the RSA. The value is **1**.|

## AsyKeySpec<sup>10+</sup>

Defines the asymmetric key parameters for creating a key generator. You need to construct a child class object and pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator. All the parameters of the bigint type in the child class object must be integers in big-endian format.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Yes  | Algorithm of the asymmetric key pair, for example, **RSA**, **DSA**, or **ECC**.|
| specType | [AsyKeySpecType](#asykeyspectype10) | Yes  | Yes| Key parameter type, which is used to distinguish public and private key parameters.|

## DSACommonParamsSpec<sup>10+</sup>

Defines the common parameters contained in the public and private keys in the DSA algorithm. It is a child class of [AsyKeySpec](#asykeyspec10) and can be used to randomly generate public or private keys. <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| p | bigint | Yes  | Yes  | Prime modulus **p** in the DSA algorithm.|
| q | bigint | Yes  | Yes  | Parameter **q** (prime factor of **p** – 1) in the DSA algorithm.|
| g | bigint | Yes  | Yes  | Parameter **g** in the DSA algorithm.|

## DSAPubKeySpec<sup>10+</sup>

Defines the parameters contained in the public key in the DSA algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [DSACommonParamsSpec](#dsacommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the DSA algorithm.|
| pk | bigint | Yes  | Yes  | Public key of the DSA algorithm.|

## DSAKeyPairSpec<sup>10+</sup>

Defines full parameters contained in the public and private keys in the DSA algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [DSACommonParamsSpec](#dsacommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the DSA algorithm.|
| sk | bigint | Yes  | Yes  | Private key **sk** in the DSA algorithm.|
| pk | bigint | Yes  | Yes  | Public key **pk** in the DSA algorithm.|

## ECField<sup>10+</sup>

Defines the elliptic curve field. Currently, only the **Fp** field is supported.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| fieldType | string | Yes  | Yes  | Type of the elliptic curve field. Currently, only **Fp** is supported.|

## ECFieldFp<sup>10+</sup>

Defines the prime field of the elliptic curve. It is a child class of [ECField](#ecfield10).

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| p | bigint | Yes  | Yes  | Prime **p**.|

## Point<sup>10+</sup>

Defines a point on the elliptic curve.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| x | bigint | Yes  | Yes  | X coordinate of the point on an elliptic curve.|
| y | bigint | Yes  | Yes  | Y coordinate of the point on an elliptic curve.|

## ECCCommonParamsSpec<sup>10+</sup>

Defines the common parameters contained in the public and private keys in the ECC algorithm. It is a child class of [AsyKeySpec](#asykeyspec10) and can be used to randomly generate public or private keys. <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| field | [ECField](#ecfield10) | Yes  | Yes  | Field of the elliptic curve. Currently, only the **Fp** field is supported.|
| a | bigint | Yes  | Yes  | First coefficient **a** of the elliptic curve.|
| b | bigint | Yes  | Yes  | Second coefficient **b** of the elliptic curve.|
| g | [Point](#point10) | Yes  | Yes  | Base point g.|
| n | bigint | Yes  | Yes  | Order **n** of the base point **g**.|
| h | number | Yes  | Yes  | Cofactor **h**.|

## ECCPriKeySpec<sup>10+</sup>

Defines the parameters contained in the private key in the ECC algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [ECCCommonParamsSpec](#ecccommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the ECC algorithm.|
| sk | bigint | Yes  | Yes  | Private key **sk** in the ECC algorithm.|

## ECCPubKeySpec<sup>10+</sup>

Defines the parameters contained in the public key in the ECC algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [ECCCommonParamsSpec](#ecccommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the ECC algorithm.|
| pk | [Point](#point10) | Yes  | Yes  | Public key **pk** in the ECC algorithm.|

## ECCKeyPairSpec<sup>10+</sup>

Defines full parameters contained in the public and private keys in the ECC algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [ECCCommonParamsSpec](#ecccommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the ECC algorithm.|
| sk | bigint | Yes  | Yes  | Private key **sk** in the ECC algorithm.|
| pk | [Point](#point10) | Yes  | Yes  | Public key **pk** in the ECC algorithm.|

## RSACommonParamsSpec<sup>10+</sup>

Defines the common parameters contained in the public and private keys in the RSA algorithm. It is a child class of [AsyKeySpec](#asykeyspec10) and can be used to randomly generate public or private keys. <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| n | bigint | Yes  | Yes  | Modulus **n**.|

## RSAPubKeySpec<sup>10+</sup>

Defines the parameters contained in the public key in the RSA algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [RSACommonParamsSpec](#rsacommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the RSA algorithm.|
| pk | bigint | Yes  | Yes  | Public key **pk** in the RSA algorithm.|

## RSAKeyPairSpec<sup>10+</sup>

Defines full parameters contained in the public and private keys in the RSA algorithm. It is a child class of [AsyKeySpec](#asykeyspec10). <br>When key parameters are used to generate a key, you can pass it to [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create a key generator.

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                                                        |
| ------- | ------ | ---- | ---- | ------------------------------------------------------------ |
| params | [RSACommonParamsSpec](#rsacommonparamsspec10) | Yes  | Yes  | Common parameters contained in both public and private keys in the RSA algorithm.|
| sk | bigint | Yes  | Yes  | Private key **sk** in the RSA algorithm.|
| pk | bigint | Yes  | Yes  | Public key **pk** in the RSA algorithm.|

## Key

Provides APIs for key operations. Before performing cryptographic operations (such as encryption and decryption), you need to construct a child class object of **Key** and pass it to [init()](#init-2) of the [Cipher](#cipher) instance. <br>Keys can be generated by a key generator.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| format  | string | Yes  | No  | Format of the key.                |
| algName | string | Yes  | No  | Algorithm name (including the key length).|

### getEncoded

getEncoded(): DataBlob

Obtains the byte stream of the key data synchronously. The key can be a symmetric key, public key, or private key. The public key must be in DER encoding format and comply with the ASN.1 syntax and X.509 specifications. The private key must be in DER encoding format and comply with the ASN.1 syntax and PKCS#8 specifications.

> **NOTE**
>
> When key parameters are used to generate an RSA private key, the private key object does not support **getEncoded()**.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type                 | Description                    |
| --------------------- | ------------------------ |
| [DataBlob](#datablob) | Key obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 801 | this operation is not supported. |
| 17620001 | memory error. |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"
function uint8ArrayToShowStr(uint8Array) {
  return Array.prototype.map
    .call(uint8Array, (x) => ('00' + x.toString(16)).slice(-2))
    .join('');
}

let key;    // The key is generated by a key generator. The generation process is omitted here.
let encodedKey = key.getEncoded();
console.info("key hex:" + uint8ArrayToShowStr(encodedKey.data));
```

## SymKey

Provides APIs for symmetric key operations. It is a child class of [Key](#key). Its objects need to be passed to [init()](#init-2) of the [Cipher](#cipher) instance in symmetric encryption and decryption. <br>Symmetric keys can be generated by a [SymKeyGenerator](#symkeygenerator).

### clearMem

clearMem(): void

Clears the keys in the memory. This API returns the result synchronously. You are advised to use this API when symmetric key instances are no longer used.

**System capability**: SystemCapability.Security.CryptoFramework

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"
function uint8ArrayToShowStr(uint8Array) {
  return Array.prototype.map
    .call(uint8Array, (x) => ('00' + x.toString(16)).slice(-2))
    .join('');
}

let key;    // The key is generated by a symKeyGenerator. The generation process is omitted here.
let encodedKey = key.getEncoded();
console.info("key hex: "+ uint8ArrayToShowStr(encodedKey.data));    // Display key content.
key.clearMem();
encodedKey = key.getEncoded();
console.info("key hex:" + uint8ArrayToShowStr(encodedKey.data));    // Display all 0s.
```

## PubKey

Provides APIs for public key operations. It is a child class of [Key](#key). Its objects need to be passed in during asymmetric encryption and decryption, signature verification, and key agreement. <br>The public key can be generated by using the asymmetric key generator [AsyKeyGenerator](#asykeygenerator) or [AsyKeyGeneratorBySpec](#asykeygeneratorbyspec10).

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| format  | string | Yes  | No  | Format of the key.                |
| algName | string | Yes  | No  | Algorithm name (including the key length).|

### getAsyKeySpec<sup>10+</sup>

getAsyKeySpec(itemType: AsyKeySpecItem): bigint | string | number

Obtains a key parameter synchronously.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type                 | Mandatory| Description                |
| ---- | --------------------- | ---- | -------------------- |
| item  | [AsyKeySpecItem](#asykeyspecitem10) | Yes  | Key parameter to obtain.|

**Return value**

| Type                       | Description                             |
| --------------------------- | --------------------------------- |
| bigint\|string\|number | Content of the key parameter obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters. |
| 17620001 | memory error. |
| 17630001 | crypto operation error. |

**Example**

```js
let key; // key is a public key object. The generation process is omitted here.
let p = key.getAsyKeySpec(cryptoFramework.AsyKeySpecItem.ECC_FP_P_BN);
console.info("ecc item --- p: " + p.toString(16));
```

## PriKey

Provides APIs for private key operations. It is a child class of [Key](#key). Its objects need to be passed in during asymmetric encryption and decryption, signing, and key agreement. <br>The public key can be generated by using the asymmetric key generator [AsyKeyGenerator](#asykeygenerator) or [AsyKeyGeneratorBySpec](#asykeygeneratorbyspec10).

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| format  | string | Yes  | No  | Format of the key.                |
| algName | string | Yes  | No  | Algorithm name (including the key length).|

### clearMem

clearMem(): void

Clears the keys in the memory. This API returns the result synchronously.

**System capability**: SystemCapability.Security.CryptoFramework

**Example**

```js
let key; // The key is a private key generated by the asymmetric key generator. The generation process is omitted here.
key.clearMem(); // For the asymmetric private key, clearMem() releases the internal key struct. After clearMem is executed, getEncoded() is not supported.
```

### getAsyKeySpec<sup>10+</sup>

getAsyKeySpec(itemType: AsyKeySpecItem): bigint | string | number

Obtains a key parameter synchronously.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type                 | Mandatory| Description                |
| ---- | --------------------- | ---- | -------------------- |
| item  | [AsyKeySpecItem](#asykeyspecitem10) | Yes  | Key parameter to obtain.|

**Return value**

| Type                       | Description                             |
| --------------------------- | --------------------------------- |
| bigint\|string\|number | Content of the key parameter obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters. |
| 17620001 | memory error. |
| 17630001 | crypto operation error. |

**Example**

```js
let key; // key is a private key object. The generation process is omitted here.
let p = key.getAsyKeySpec(cryptoFramework.AsyKeySpecItem.ECC_FP_P_BN);
console.info("ecc item --- p: " + p.toString(16));
```

## KeyPair

Defines an asymmetric key pair, which includes a public key and a private key. <br>The asymmetric key pair can be generated by using the asymmetric key generator [AsyKeyGenerator](#asykeygenerator) or [AsyKeyGeneratorBySpec](#asykeygeneratorbyspec10).

> **NOTE**
>
> The **pubKey** and **priKey** objects in the **KeyPair** object exist as one parameter in the **KeyPair** object. When **KeyPair** leaves the scope, its internal objects can be destructed.
> The service must reference the **KeyPair** object instead of the internal **pubKey** or **priKey** object.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description          |
| ------- | ------ | ---- | ---- | ------------ |
| priKey  | [PriKey](#prikey) | Yes  | No  | Private key.     |
| pubKey | [PubKey](#pubkey) | Yes  | No  | Public key.      |


## cryptoFramework.createSymKeyGenerator

createSymKeyGenerator(algName: string): SymKeyGenerator

Creates a **symKeyGenerator** instance based on the specified algorithm. <br>For details about the supported specifications, see [Key Generation Specifications](../../security/cryptoFramework-overview.md#key-generation-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                                                        |
| ------- | ------ | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Algorithm used to create the **symKeyGenerator** instance.<br>For details, see "String Parameter" in [Key Generation Specifications](../../security/cryptoFramework-overview.md#key-generation-specifications).|

**Return value**

| Type                               | Description                      |
| ----------------------------------- | -------------------------- |
| [SymKeyGenerator](#symkeygenerator) | **symKeyGenerator** instance created.|

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters. |
| 801 | this operation is not supported. |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';
let symKeyGenerator = cryptoFramework.createSymKeyGenerator('3DES192');
```

## SymKeyGenerator

Provides APIs for using the **symKeyGenerator**. <br>Before using any API of the **SymKeyGenerator** class, you must create a **symKeyGenerator** instance by using [createSymKeyGenerator](#cryptoframeworkcreatesymkeygenerator).

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                          |
| ------- | ------ | ---- | ---- | ------------------------------ |
| algName | string | Yes  | No  | Algorithm used by the **symKeyGenerator**.|

### generateSymKey

generateSymKey(callback: AsyncCallback\<SymKey>): void

Generates a key randomly. This API uses an asynchronous callback to return the result. <br>This API can be used only after a **symKeyGenerator** instance is created by using [createSymKeyGenerator](#cryptoframeworkcreatesymkeygenerator). <br>**RAND_priv_bytes()** of OpenSSL can be used to generate random keys.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                             | Mandatory| Description                                                        |
| -------- | --------------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback\<[SymKey](#symkey)> | Yes  | Callback invoked to return the result. If the operation is successful, **err** is **undefined** and **data** is the symmetric key generated. Otherwise, **err** is an error object.|

**Error codes**

| ID| Error Message     |
| -------- | ------------- |
| 17620001 | memory error. |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';
let symAlgName = '3DES192';
let symKeyGenerator = cryptoFramework.createSymKeyGenerator(symAlgName);
symKeyGenerator.generateSymKey((err, symKey) => {
  if (err) {
    console.error(`Generate symKey failed, ${err.code}, ${err.message}`);
  } else {
    console.info(`Generate symKey success, algName: ${symKey.algName}`);
  }
})
```

### generateSymKey

generateSymKey(): Promise\<SymKey>

Generates a key randomly. This API uses a promise to return the result. <br>This API can be used only after a **symKeyGenerator** instance is created by using [createSymKeyGenerator](#cryptoframeworkcreatesymkeygenerator). <br>**RAND_priv_bytes()** of OpenSSL can be used to generate random keys.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type                       | Description                             |
| --------------------------- | --------------------------------- |
| Promise\<[SymKey](#symkey)> | Promise used to return the symmetric key generated.|

**Error codes**

| ID| Error Message     |
| -------- | ------------- |
| 17620001 | memory error. |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';
let symAlgName = 'AES128';
let symKeyGenerator = cryptoFramework.createSymKeyGenerator(symAlgName);
symKeyGenerator.generateSymKey()
.then(symKey => {
  console.info(`Generate symKey success, algName: ${symKey.algName}`);
}, error => {
  console.error(`Generate symKey failed, ${error.code}, ${error.message}`);
})
```

### convertKey

convertKey(key: DataBlob, callback: AsyncCallback\<SymKey>): void

Converts data into a symmetric key. This API uses an asynchronous callback to return the result. <br>This API can be used only after a **symKeyGenerator** instance is created by using [createSymKeyGenerator](#cryptoframeworkcreatesymkeygenerator).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                             | Mandatory| Description                                                        |
| -------- | --------------------------------- | ---- | ------------------------------------------------------------ |
| key      | [DataBlob](#datablob)             | Yes  | Data to convert.                                        |
| callback | AsyncCallback\<[SymKey](#symkey)> | Yes  | Callback invoked to return the result. If the operation is successful, **err** is **undefined** and **data** is the symmetric key generated. Otherwise, **err** is an error object.|

**Error codes**

| ID| Error Message                                              |
| -------- | --------------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                                       |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

function genKeyMaterialBlob() {
  let arr = [
    0xba, 0x3d, 0xc2, 0x71, 0x21, 0x1e, 0x30, 0x56,
    0xad, 0x47, 0xfc, 0x5a, 0x46, 0x39, 0xee, 0x7c,
    0xba, 0x3b, 0xc2, 0x71, 0xab, 0xa0, 0x30, 0x72];    // keyLen = 192 (24 bytes)
  let keyMaterial = new Uint8Array(arr);
  return {data: keyMaterial};
}

let symAlgName = '3DES192';
let symKeyGenerator = cryptoFramework.createSymKeyGenerator(symAlgName);
let keyMaterialBlob = genKeyMaterialBlob();
symKeyGenerator.convertKey(keyMaterialBlob, (err, symKey) => {
  if (err) {
    console.error(`Convert symKey failed, ${err.code}, ${err.message}`);
  } else {
    console.info(`Convert symKey success, algName: ${symKey.algName}`);
  }
})
```

### convertKey

convertKey(key: DataBlob): Promise\<SymKey>

Converts data into a symmetric key. This API uses a promise to return the result. <br>This API can be used only after a **symKeyGenerator** instance is created by using [createSymKeyGenerator](#cryptoframeworkcreatesymkeygenerator).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type                 | Mandatory| Description                |
| ---- | --------------------- | ---- | -------------------- |
| key  | [DataBlob](#datablob) | Yes  | Data to convert.|

**Return value**

| Type                       | Description                             |
| --------------------------- | --------------------------------- |
| Promise\<[SymKey](#symkey)> | Promise used to return the symmetric key generated.|

**Error codes**

| ID| Error Message                                         |
| -------- | --------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                                |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

function genKeyMaterialBlob() {
  let arr = [
    0xba, 0x3d, 0xc2, 0x71, 0x21, 0x1e, 0x30, 0x56,
    0xad, 0x47, 0xfc, 0x5a, 0x46, 0x39, 0xee, 0x7c,
    0xba, 0x3b, 0xc2, 0x71, 0xab, 0xa0, 0x30, 0x72];    // keyLen = 192 (24 bytes)
  let keyMaterial = new Uint8Array(arr);
  return {data: keyMaterial};
}

let symAlgName = '3DES192';
let symKeyGenerator = cryptoFramework.createSymKeyGenerator(symAlgName);
let keyMaterialBlob = genKeyMaterialBlob();
symKeyGenerator.convertKey(keyMaterialBlob)
.then(symKey => {
  console.info(`Convert symKey success, algName: ${symKey.algName}`);
}, error => {
  console.error(`Convert symKey failed, ${error.code}, ${error.message}`);
})
```

## cryptoFramework.createAsyKeyGenerator

createAsyKeyGenerator(algName: string): AsyKeyGenerator

Creates an **AsyKeyGenerator** instance based on the specified algorithm. <br>For details about the supported specifications, see [Key Generation Specifications](../../security/cryptoFramework-overview.md#key-generation-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                            |
| ------- | ------ | ---- | -------------------------------- |
| algName | string | Yes  | Algorithm used to create the **symkeyGenerator**.|

**Return value**

| Type           | Description                        |
| --------------- | ---------------------------- |
| [AsyKeyGenerator](#asykeygenerator) | **AsyKeyGenerator** instance created.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters. |
| 801 | this operation is not supported. |
| 17620001 | memory error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyGenerator = cryptoFramework.createAsyKeyGenerator("ECC256");
```

## AsyKeyGenerator

Provides APIs for using the **AsKeyGenerator**. Before using any API of the **AsKeyGenerator** class, you must create an **AsyKeyGenerator** instance by using **createAsyKeyGenerator()**.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                            |
| ------- | ------ | ---- | ---- | -------------------------------- |
| algName | string | Yes  | No  | Algorithm used by the **AsKeyGenerator**.|

### generateKeyPair

generateKeyPair(callback: AsyncCallback\<KeyPair>): void

Generates a key pair randomly. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                   | Mandatory| Description                          |
| -------- | ----------------------- | ---- | ------------------------------ |
| callback | AsyncCallback\<[KeyPair](#keypair)> | Yes  | Callback invoked to return the key pair obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyGenerator = cryptoFramework.createAsyKeyGenerator("ECC256");
asyKeyGenerator.generateKeyPair((err, keyPair) => {
  if (err) {
    console.error("generateKeyPair: error.");
    return;
  }
  console.info("generateKeyPair: success.");
})
```

### generateKeyPair

generateKeyPair(): Promise\<KeyPair>

Generates a key pair randomly. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type             | Description                             |
| ----------------- | --------------------------------- |
| Promise\<[KeyPair](#keypair)> | Promise used to return the key pair generated.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyGenerator = cryptoFramework.createAsyKeyGenerator("ECC256");
let keyGenPromise = asyKeyGenerator.generateKeyPair();
keyGenPromise.then( keyPair => {
  console.info("generateKeyPair success.");
}).catch(error => {
  console.error("generateKeyPair error.");
});
```

### convertKey

convertKey(pubKey: DataBlob, priKey: DataBlob, callback: AsyncCallback\<KeyPair\>): void

Converts data into an asymmetric key. This API uses an asynchronous callback to return the result. For details, see **Key Conversion**.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type      | Mandatory| Description                          |
| -------- | ----------- | ---- | ------------------------------ |
| pubKey   | [DataBlob](#datablob)     | Yes  | Public key material to convert. If no public key is required, set this parameter to **null**.       |
| priKey   | [DataBlob](#datablob)     | Yes  | Private key material to convert. If no private key is required, set this parameter to **null**.       |
| callback | AsyncCallback\<[KeyPair](#keypair)> | Yes  | Callback invoked to return the key pair obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let pubKeyArray = new Uint8Array([48, 89, 48, 19, 6, 7, 42, 134, 72, 206, 61, 2, 1, 6, 8, 42, 134, 72, 206, 61, 3, 1, 7, 3, 66, 0, 4, 83, 96, 142, 9, 86, 214, 126, 106, 247, 233, 92, 125, 4, 128, 138, 105, 246, 162, 215, 71, 81, 58, 202, 121, 26, 105, 211, 55, 130, 45, 236, 143, 55, 16, 248, 75, 167, 160, 167, 106, 2, 152, 243, 44, 68, 66, 0, 167, 99, 92, 235, 215, 159, 239, 28, 106, 124, 171, 34, 145, 124, 174, 57, 92]);
let priKeyArray = new Uint8Array([48, 49, 2, 1, 1, 4, 32, 115, 56, 137, 35, 207, 0, 60, 191, 90, 61, 136, 105, 210, 16, 27, 4, 171, 57, 10, 61, 123, 40, 189, 28, 34, 207, 236, 22, 45, 223, 10, 189, 160, 10, 6, 8, 42, 134, 72, 206, 61, 3, 1, 7]);
let pubKeyBlob = {data: pubKeyArray}; // Data of the public key.
let priKeyBlob = {data: priKeyArray}; // Data of the private key.
let asyKeyGenerator = cryptoFramework.createAsyKeyGenerator("ECC256");
asyKeyGenerator.convertKey(pubKeyBlob, priKeyBlob, (err, keyPair) => {
  if (err) {
    console.error("convertKey: error.");
    return;
  }
  console.info("convertKey: success.");
})
```

### convertKey

convertKey(pubKey: DataBlob, priKey: DataBlob): Promise\<KeyPair>

Converts data into an asymmetric key. This API uses a promise to return the result. For details, see **Key Conversion**.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type   | Mandatory| Description            |
| ------ | -------- | ---- | ---------------- |
| pubKey | DataBlob | Yes  | Public key material to convert. If no public key is required, set this parameter to **null**.|
| priKey | DataBlob | Yes  | Private key material to convert. If no private key is required, set this parameter to **null**.|

**Return value**

| Type             | Description                             |
| ----------------- | --------------------------------- |
| Promise\<[KeyPair](#keypair)> | Promise used to return the key pair generated.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let pubKeyArray = new Uint8Array([48, 89, 48, 19, 6, 7, 42, 134, 72, 206, 61, 2, 1, 6, 8, 42, 134, 72, 206, 61, 3, 1, 7, 3, 66, 0, 4, 83, 96, 142, 9, 86, 214, 126, 106, 247, 233, 92, 125, 4, 128, 138, 105, 246, 162, 215, 71, 81, 58, 202, 121, 26, 105, 211, 55, 130, 45, 236, 143, 55, 16, 248, 75, 167, 160, 167, 106, 2, 152, 243, 44, 68, 66, 0, 167, 99, 92, 235, 215, 159, 239, 28, 106, 124, 171, 34, 145, 124, 174, 57, 92]);
let priKeyArray = new Uint8Array([48, 49, 2, 1, 1, 4, 32, 115, 56, 137, 35, 207, 0, 60, 191, 90, 61, 136, 105, 210, 16, 27, 4, 171, 57, 10, 61, 123, 40, 189, 28, 34, 207, 236, 22, 45, 223, 10, 189, 160, 10, 6, 8, 42, 134, 72, 206, 61, 3, 1, 7]);
let pubKeyBlob = {data: pubKeyArray}; // Data of the public key.
let priKeyBlob = {data: priKeyArray}; // Data of the private key.
let asyKeyGenerator = cryptoFramework.createAsyKeyGenerator("ECC256");
let keyGenPromise = asyKeyGenerator.convertKey(pubKeyBlob, priKeyBlob);
keyGenPromise.then( keyPair => {
  console.info("convertKey success.");
}).catch(error => {
  console.error("convertKey error.");
});
```

**Key Conversion**

1. After **getEncoded()** is called for the asymmetric (RSA, ECC, or DSA) public and private keys, binary data in X.509 format and binary data in PKCS #8 format are returned, respectively. The binary data can be used for cross-application transfer or persistent storage.
2. The public key returned by **convertKey()** must comply with the ASN.1 syntax, X.509 specifications, and DER encoding format, and the private key must comply with the ASN.1 syntax, PKCS #8 specifications, and DER encoding format.
3. In **convertKey()**, you can pass in either **pubKey** or **priKey**, or both of them. If one of them is passed in, the returned **KeyPair** instance contains only the key converted from the data you passed in.

## cryptoFramework.createAsyKeyGeneratorBySpec<sup>10+</sup>

createAsyKeyGeneratorBySpec(asyKeySpec: AsyKeySpec): AsyKeyGeneratorBySpec

Creates an **AsyKeyGenerator** instance based on the key parameters. <br>For details about the supported specifications, see [Key Generation Specifications](../../security/cryptoFramework-overview.md#key-generation-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                            |
| ------- | ------ | ---- | -------------------------------- |
| asyKeySpec | [AsyKeySpec](#asykeyspec10) | Yes  | Key parameters. The **AsyKeyGenerator** generates the public/private key based on the specified parameters.|

**Return value**

| Type                                           | Description                      |
| ----------------------------------------------- | -------------------------- |
| [AsyKeyGeneratorBySpec](#asykeygeneratorbyspec10) | Returns the **AsyKeyGenerator** instance created.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters. |
| 801 | this operation is not supported. |
| 17620001 | memory error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

// Set the common parameters contained in both the DSA1024 public and private keys.
function genDsa1024CommonSpecBigE() {
  let dsaCommonSpec = {
    algName : "DSA",
    specType : cryptoFramework.AsyKeySpecType.COMMON_PARAMS_SPEC,
    p : BigInt("0xed1501551b8ab3547f6355ffdc2913856ddeca198833dbd04f020e5f25e47c50e0b3894f7690a0d2ea5ed3a7be25c54292a698e1f086eb3a97deb4dbf04fcad2dafd94a9f35c3ae338ab35477e16981ded6a5b13d5ff20bf55f1b262303ad3a80af71aa6aa2354d20e9c82647664bdb6b333b7bea0a5f49d55ca40bc312a1729"),
    q : BigInt("0xd23304044019d5d382cfeabf351636c7ab219694ac845051f60b047b"),
    g : BigInt("0x2cc266d8bd33c3009bd67f285a257ba74f0c3a7e12b722864632a0ac3f2c17c91c2f3f67eb2d57071ef47aaa8f8e17a21ad2c1072ee1ce281362aad01dcbcd3876455cd17e1dd55d4ed36fa011db40f0bbb8cba01d066f392b5eaa9404bfcb775f2196a6bc20eeec3db32d54e94d87ecdb7a0310a5a017c5cdb8ac78597778bd"),
  }
  return dsaCommonSpec;
}
// Set full parameters contained in the DSA1024 public and private keys.
function genDsa1024KeyPairSpecBigE() {
  let dsaCommonSpec = genDsa1024CommonSpecBigE();
  let dsaKeyPairSpec = {
    algName : "DSA",
    specType : cryptoFramework.AsyKeySpecType.KEY_PAIR_SPEC,
    params : dsaCommonSpec,
    sk : BigInt("0xa2dd2adb2d11392c2541930f61f1165c370aabd2d78d00342e0a2fd9"),
    pk : BigInt("0xae6b5d5042e758f3fc9a02d009d896df115811a75b5f7b382d8526270dbb3c029403fafb8573ba4ef0314ea86f09d01e82a14d1ebb67b0c331f41049bd6b1842658b0592e706a5e4d20c14b67977e17df7bdd464cce14b5f13bae6607760fcdf394e0b73ac70aaf141fa4dafd736bd0364b1d6e6c0d7683a5de6b9221e7f2d6b"),
  }
  return dsaKeyPairSpec;
}

let asyKeyPairSpec = genDsa1024KeyPairSpecBigE(); // The JS input must be a positive number in big-endian format.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
```

## AsyKeyGeneratorBySpec<sup>10+</sup>

Provides APIs for using the **AsKeyGenerator**. Before using the APIs of this class, you need to use [createAsyKeyGeneratorBySpec()](#cryptoframeworkcreateasykeygeneratorbyspec10) to create an **AsyKeyGeneratorBySpec** instance.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                      |
| ------- | ------ | ---- | ---- | -------------------------- |
| algName | string | Yes  | No  | Algorithm used by the asymmetric key generator.|

### generateKeyPair

generateKeyPair(callback: AsyncCallback\<KeyPair>): void

Generates an asymmetric key pair. This API uses an asynchronous callback to return the result. When you use key parameters of the **COMMON_PARAMS_SPEC** type to create the key generator, you can obtain a key pair randomly generated. When you use **KEY_PAIR_SPEC** to create the key generator, you can obtain a key pair that matches the key parameters.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                   | Mandatory| Description                          |
| -------- | ----------------------- | ---- | ------------------------------ |
| callback | AsyncCallback\<[KeyPair](#keypair)> | Yes  | Callback invoked to return the key pair obtained.|

**Error codes**

| ID| Error Message               |
| -------- | ----------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyPairSpec; // asyKeyPairSpec specifies full parameters contained in the private and public keys. The generation process is omitted here.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
asyKeyGeneratorBySpec.generateKeyPair((err, keyPair) => {
  if (err) {
    console.error("generateKeyPair: error.");
    return;
  }
  console.info("generateKeyPair: success.");
})
```

### generateKeyPair

generateKeyPair(): Promise\<KeyPair>

Generates an asymmetric key pair. This API uses a promise to return the result. When you use key parameters of the **COMMON_PARAMS_SPEC** type to create the key generator, you can obtain a key pair randomly generated. When you use **KEY_PAIR_SPEC** to create the key generator, you can obtain a key pair that matches the key parameters.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type             | Description                             |
| ----------------- | --------------------------------- |
| Promise\<[KeyPair](#keypair)> | Promise used to return the key pair generated.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyPairSpec; // asyKeyPairSpec specifies full parameters contained in the private and public keys. The generation process is omitted here.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
let keyGenPromise = asyKeyGeneratorBySpec.generateKeyPair();
keyGenPromise.then( keyPair => {
  console.info("generateKeyPair success.");
}).catch(error => {
  console.error("generateKeyPair error.");
});
```

### generatePriKey

generatePriKey(callback: AsyncCallback\<PriKey>): void

Generates a private key. This API uses an asynchronous callback to return the result. If you use key parameters of the **PRIVATE_KEY_SPEC** type to create the key generator, you can obtain the specified private key. If you use **KEY_PAIR_SPEC** to create the key generator, you can obtain the private key from the generated key pair.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                   | Mandatory| Description                          |
| -------- | ----------------------- | ---- | ------------------------------ |
| callback | AsyncCallback\<[PriKey](#prikey)> | Yes  | Callback invoked to return the key pair obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyPairSpec; // asyKeyPairSpec specifies full parameters contained in the private and public keys.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
asyKeyGeneratorBySpec.generatePriKey((err, prikey) => {
  if (err) {
    console.error("generatePriKey: error.");
    return;
  }
  console.info("generatePriKey: success.");
})
```

### generatePriKey

generatePriKey(): Promise\<PriKey>

Generates a private key. This API uses a promise to return the result. If you use key parameters of the **PRIVATE_KEY_SPEC** type to create the key generator, you can obtain the specified private key. If you use **KEY_PAIR_SPEC** to create the key generator, you can obtain the private key from the generated key pair.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type             | Description                             |
| ----------------- | --------------------------------- |
| Promise\<[PriKey](#prikey)> | Promise used to return the key generated.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyPairSpec; // asyKeyPairSpec specifies full parameters contained in the private and public keys.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
let keyGenPromise = asyKeyGeneratorBySpec.generatePriKey();
keyGenPromise.then( priKey => {
  console.info("generatePriKey success.");
}).catch(error => {
  console.error("generatePriKey error.");
});
```

### generatePubKey

generatePubKey(callback: AsyncCallback\<PubKey>): void

Generates a public key. This API uses an asynchronous callback to return the result. If you use key parameters of the **PUBLIC_KEY_SPEC** type to create the key generator, you can obtain the specified public key. If you use **KEY_PAIR_SPEC** to create the key generator, you can obtain the public key from the generated key pair.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                   | Mandatory| Description                          |
| -------- | ----------------------- | ---- | ------------------------------ |
| callback | AsyncCallback\<[PubKey](#pubkey)> | Yes  | Callback invoked to return the key pair obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyPairSpec; // asyKeyPairSpec specifies full parameters contained in the private and public keys. The generation process is omitted here.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
asyKeyGeneratorBySpec.generateKeyPair((err, pubKey) => {
  if (err) {
    console.error("generatePubKey: error.");
    return;
  }
  console.info("generatePubKey: success.");
})
```

### generatePubKey

generatePubKey(): Promise\<PubKey>

Generates a public key. This API uses a promise to return the result. If you use key parameters of the **PUBLIC_KEY_SPEC** type to create the key generator, you can obtain the specified public key. If you use **KEY_PAIR_SPEC** to create the key generator, you can obtain the public key from the generated key pair.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type             | Description                             |
| ----------------- | --------------------------------- |
| Promise\<[PubKey](#pubkey)> | Promise used to return the key pair generated.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let asyKeyPairSpec; // asyKeyPairSpec specifies full parameters contained in the private and public keys. The generation process is omitted here.
let asyKeyGeneratorBySpec = cryptoFramework.createAsyKeyGeneratorBySpec(asyKeyPairSpec);
let keyGenPromise = asyKeyGeneratorBySpec.generatePubKey();
keyGenPromise.then( pubKey => {
  console.info("generatePubKey success.");
}).catch(error => {
  console.error("generatePubKey error.");
});
```

## cryptoFramework.createCipher

createCipher(transformation: string): Cipher

Creates a [Cipher](#cipher) instance based on the specified algorithm. <br>For details about the supported specifications, see [Encryption and Decryption Specifications](../../security/cryptoFramework-overview.md#encryption-and-decryption-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name        | Type  | Mandatory| Description                                                        |
| -------------- | ------ | ---- | ------------------------------------------------------------ |
| transformation | string | Yes  | Combination of the algorithm name (including the key length), encryption mode, and padding algorithm of the **Cipher** instance to create.<br>For details, see **String Parameter** in [Encryption and Decryption Specifications](../../security/cryptoFramework-overview.md#encryption-and-decryption-specifications).|

> **NOTE**
>
> 1. In symmetric encryption and decryption, the implementation of PKCS #5 is the same as that of PKCS #7. PKCS #5 and PKCS #7 use the same padding length and block length. That is, data is padded with 8 bytes in 3DES and 16 bytes in AES. **noPadding** indicates that no padding is performed. <br>You need to understand the differences between different block cipher modes and use the correct parameter specifications. For example, padding is required for ECB and CBC. Otherwise, ensure that the plaintext length is an integer multiple of the block size. No padding is recommended for other modes. In this case, the ciphertext length is the same as the plaintext length.
> 2. When RSA or SM2 are used for asymmetric encryption and decryption, create a **Cipher** instance for encryption and decryption respectively. Do not use the same **Cipher** instance for encryption and decryption. For symmetric encryption and decryption, one **cipher** object can be used to perform both encryption and decryption as long as the algorithm specifications are the same.

**Return value**

| Type             | Description                    |
| ----------------- | ------------------------ |
| [Cipher](#cipher) | [Cipher](#cipher) instance created.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported. |
| 17620001 | memory error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let cipherAlgName = '3DES192|ECB|PKCS7';
var cipher;
try {
  cipher = cryptoFramework.createCipher(cipherAlgName);
  console.info(`cipher algName: ${cipher.algName}`);
} catch (error) {
  console.error(`createCipher failed, ${error.code}, ${error.message}`);
}
```

## Cipher

Provides APIs for cipher operations. The [init()](#init-2), [update()](#update-4), and [doFinal()](#dofinal-2) APIs in this class are called in sequence to implement symmetric encryption or decryption and asymmetric encryption or decryption. <br>For details about the complete encryption and decryption process, see [Encryption and Decryption](../../security/cryptoFramework-guidelines.md#encryption-and-decryption).

A complete symmetric encryption/decryption process is slightly different from the asymmetric encryption/decryption process.

- Symmetric encryption and decryption: **init()** and **doFinal()** are mandatory. **update()** is optional and can be called multiple times to encrypt or decrypt big data. After **doFinal()** is called to complete an encryption or decryption operation, **init()** can be called to start a new encryption or decryption operation.
- RSA or SM2 asymmetric encryption and decryption: **init()** and **doFinal()** are mandatory, and **update()** is not supported. **doFinal()** can be called multiple times to encrypt or decrypt big data. **init()** cannot be called repeatedly. If the encryption/decryption mode or padding mode is changed, a new **Cipher** object must be created.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework


| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| algName | string | Yes  | No  | Algorithm.|

### init

init(opMode: CryptoMode, key: Key, params: ParamsSpec, callback: AsyncCallback\<void>): void

Initializes a [cipher](#cipher) instance. This API uses an asynchronous callback to return the result. <br>This API can be used only after a [Cipher](#cipher) instance is created by using [createCipher](#cryptoframeworkcreatecipher).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| opMode   | [CryptoMode](#cryptomode) | Yes  | Operation (encryption or decryption) to perform.                                          |
| key      | [Key](#key)               | Yes  | Key for encryption or decryption.                                      |
| params   | [ParamsSpec](#paramsspec) | Yes  | Parameters for encryption or decryption. For algorithm modes without parameters (such as ECB), **null** can be passed in.|
| callback | AsyncCallback\<void>      | Yes  | Callback invoked to return the result. If the initialization is successful, **err** is **undefined**. Otherwise, **err** is an error object.    |

**Error codes**

| ID| Error Message                                                |
| -------- | --------------------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                                            |
| 17620002 | runtime error.                                           |
| 17630001 | crypto operation error.|

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';
let symKey;     // The process of generating the symmetric key is omitted here.
let cipher;        // The process of creating a Cipher instance is omitted here.

cipher.init(cryptoFramework.CryptoMode.ENCRYPT_MODE, symKey, null, (err, ) => {
  if (err) {
    console.error(`Failed to init cipher, ${err.code}, ${err.message}`);
  } else {
    console.info(`Init cipher success`);
    // Perform subsequent operations such as update.
  }
})
```

### init

init(opMode: CryptoMode, key: Key, params: ParamsSpec): Promise\<void>

Initializes a [cipher](#cipher) instance. This API uses a promise to return the result. <br>This API can be used only after a [Cipher](#cipher) instance is created by using [createCipher](#cryptoframeworkcreatecipher).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| ------ | ------------------------- | ---- | ------------------------------------------------------------ |
| opMode | [CryptoMode](#cryptomode) | Yes  | Operation (encryption or decryption) to perform.                                          |
| key    | [Key](#key)               | Yes  | Key for encryption or decryption.                                      |
| params | [ParamsSpec](#paramsspec) | Yes  | Parameters for encryption or decryption. For algorithm modes without parameters (such as ECB), **null** can be passed in.|

**Return value**

| Type          | Description                                  |
| -------------- | -------------------------------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message                                         |
| -------- | ------------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                                     |
| 17620002 | runtime error.                                    |
| 17630001 | crypto operation error.|

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';
let symKey;     // The process of generating the symmetric key is omitted here.
let cipher;        // The process of creating a Cipher instance is omitted here.
cipher.init(cryptoFramework.CryptoMode.ENCRYPT_MODE, symKey, null)
.then(() => {
  console.info(`Init cipher success`);
  // Perform subsequent operations such as update.
}, error => {
  console.error(`Failed to init cipher, ${error.code}, ${error.message}`);
})
```

### update

update(data: DataBlob, callback: AsyncCallback\<DataBlob>): void

Updates the data to encrypt or decrypt by segment. This API uses an asynchronous callback to return the encrypted or decrypted data. <br>This API can be called only after the [Cipher](#cipher) instance is initialized by using [init()](init-2).

> **NOTE**
>
> 1. If you are not familiar with the block modes for symmetric encryption and decryption, add a judgment to determine whether the result of each **update()** and **doFinal()** is null. If the result is not null, obtain the data to concatenate the complete ciphertext or plaintext. The reason is the block mode and the related specifications affect the **update()** and [doFinal()](#dofinal-2) results. <br>For example, in ECB and CBC modes, data is encrypted or decrypted by block no matter whether the data passed in by **update()** is an integer multiple of the block length, and the encrypted/decrypted block data generated by this **update()** is output. <br>That is, encrypted/decrypted data is returned as long as the data passed in by **update()** reaches the size of a block. Otherwise, **null** is returned and the data will be retained until a block is formed in the next **update()**/**doFinal()**. <br>When **doFinal()** is called, the data that has not been encrypted or decrypted will be padded based on the padding mode set in [createCipher](#cryptoframeworkcreatecipher) to an integer multiple of the block length, and then encrypted or decrypted. <br>For a mode in which a block cipher can be converted into a stream cipher, the length of the ciphertext may be the same as that of the plaintext.
> 2. **update()** may be called multiple times or may not be called ([doFinal()](#dofinal-2) is called after [init](#init-2)), depending on the size of the data to encrypt or decrypt.
>    The algorithm library does not set a limit on the amount of data that can be passed in by **updated()** (once or accumulatively). For symmetric encryption and decryption of a large amount of data, you are advised to call **update()** multiple times to pass in the data by segment.
>    For details about the sample code for calling **update()** multiple times in AES, see [Encryption and Decryption](../../security/cryptoFramework-guidelines.md#encryption-and-decryption).
> 3. RSA or SM2 asymmetric encryption and decryption do not support **update()**.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| data     | [DataBlob](#datablob)                 | Yes  | Data to encrypt or decrypt. It cannot be **null** or {data:Uint8Array (empty)}.          |
| callback | AsyncCallback\<[DataBlob](#datablob)> | Yes  | Callback invoked to return the result. If the operation is successful, **err** is **undefined**, and **data** is **DataBlob** (containing the encrypted or decrypted data). Otherwise, **err** is an error object.|

**Error codes**

| ID| Error Message                                   |
| -------- | ------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                               |
| 17620002 | runtime error.                              |
| 17630001 | crypto operation error.                     |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

function stringToUint8Array(str) {
  let arr = [];
  for (let i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  return new Uint8Array(arr);
}

let cipher;        // The process of creating a Cipher instance is omitted here.
// The init() process is omitted here.
let plainText = {data: stringToUint8Array('this is test!')};
cipher.update(plainText, (err, output) => {       // Example of the encryption process.
  if (err) {
    console.error(`Failed to update cipher`);
  } else {
    console.info(`Update cipher success`);
    if (output != null) {
      // Concatenate output.data to the ciphertext.
    }
    // Perform subsequent operations such as doFinal().
  }
})
```

### update

update(data: DataBlob): Promise\<DataBlob>

Updates the data to encrypt or decrypt by segment. This API uses a promise to return the encrypted or decrypted data. <br>This API can be called only after the [Cipher](#cipher) instance is initialized by using [init()](init-2).

> **NOTE**
>
> 1. If you are not familiar with the block modes for symmetric encryption and decryption, add a judgment to determine whether the result of each **update()** and **doFinal()** is null. If the result is not null, obtain the data to concatenate the complete ciphertext or plaintext. The reason is the block mode and the related specifications affect the **update()** and [doFinal()](#dofinal-2) results. <br>For example, in ECB and CBC modes, data is encrypted or decrypted by block no matter whether the data passed in by **update()** is an integer multiple of the block length, and the encrypted/decrypted block data generated by this **update()** is output. <br>That is, encrypted/decrypted data is returned as long as the data passed in by **update()** reaches the size of a block. Otherwise, **null** is returned and the data will be retained until a block is formed in the next **update()**/**doFinal()**. <br>When **doFinal()** is called, the data that has not been encrypted or decrypted will be padded based on the padding mode set in [createCipher](#cryptoframeworkcreatecipher) to an integer multiple of the block length, and then encrypted or decrypted. <br>For a mode in which a block cipher can be converted into a stream cipher, the length of the ciphertext may be the same as that of the plaintext.
> 2. **update()** may be called multiple times or may not be called ([doFinal()](#dofinal-2) is called after [init](#init-2)), depending on the size of the data to encrypt or decrypt.
>    The algorithm library does not set a limit on the amount of data that can be passed in by **updated()** (once or accumulatively). For symmetric encryption and decryption of a large amount of data, you are advised to call **update()** multiple times to pass in the data by segment.
>    For details about the sample code for calling **update()** multiple times in AES, see [Encryption and Decryption](../../security/cryptoFramework-guidelines.md#encryption-and-decryption).
> 3. RSA or SM2 asymmetric encryption and decryption do not support **update()**.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type                 | Mandatory| Description                |
| ---- | --------------------- | ---- | -------------------- |
| data | [DataBlob](#datablob) | Yes  | Data to encrypt or decrypt. It cannot be **null** or {data:Uint8Array (empty)}.|

**Return value**

| Type                           | Description                                            |
| ------------------------------- | ------------------------------------------------ |
| Promise\<[DataBlob](#datablob)> | Promise used to return the **DataBlob** (containing the encrypted or decrypted data).|

**Error codes**

| ID| Error Message                                    |
| -------- | -------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                                |
| 17620002 | runtime error.                               |
| 17630001 | crypto operation error.                      |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

function stringToUint8Array(str) {
  let arr = [];
  for (let i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  return new Uint8Array(arr);
}

let cipher;        // The process of creating a Cipher instance is omitted here.
// The init() process is omitted here.
let plainText = {data: stringToUint8Array('this is test!')};
cipher.update(plainText)
.then((output) => {
  console.info(`Update cipher success.`);
  if (output != null) {
    // Concatenate output.data to the ciphertext.
  }
  // Perform subsequent operations such as doFinal().
}, error => {
  console.info(`Update cipher failed.`);
})
```

### doFinal

doFinal(data: DataBlob, callback: AsyncCallback\<DataBlob>): void

 (1) Encrypts or decrypts the remaining data (generated by the block cipher mode) and the data passed in by **doFinal()** to finalize the symmetric encryption or decryption. This API uses an asynchronous callback to return the encrypted or decrypted data. <br>If a small amount of data needs to be encrypted or decrypted, you can use **doFinal()** to pass in data without using **update()**. If all the data has been passed in by [update()](#update-4), you can pass in **null** in **data** of **doFinal()**. <br>The output of **doFinal()** varies with the symmetric encryption/decryption mode in use.

- Symmetric encryption in GCM and CCM mode: The result consists of the ciphertext and **authTag** (the last 16 bytes for GCM and the last 12 bytes for CCM). If **null** is passed in by **data** of **doFinal()**, the result of **doFinal()** is **authTag**. <br>**authTag** must be [GcmParamsSpec](#gcmparamsspec) or [CcmParamsSpec](#ccmparamsspec) used for decryption. The ciphertext is the **data** passed in for decryption.
- Symmetric encryption and decryption in other modes and symmetric decryption in GCM and CCM modes: The result is the complete plaintext/ciphertext.

 (2) Encrypts or decrypts the input data for RSA or SM2 asymmetric encryption/decryption. This API uses an asynchronous callback to return the result. If a large amount of data needs to be encrypted/decrypted, call **doFinal()** multiple times and concatenate the result of each **doFinal()** to obtain the complete plaintext/ciphertext.

> **NOTE**
>
>  1. In symmetric encryption or decryption, calling **doFinal()** means the end of an  encryption or decryption process, and the [Cipher](#cipher) instance state will be cleared. To start a new encryption or decryption operation, you must call [init()](#init-2) to pass in a complete parameter list for initialization. <br>For example, if the same symmetric key is used for a **Cipher** instance to perform encryption and then decryption. After the encryption is complete, the **params** in **init** for decryption must be set instead of being **null**.
>  2. If a decryption fails, check whether the data to be encrypted and decrypted matches the parameters in **[init](#init-2)**. For the GCM mode, check whether the **authTag** obtained after encryption is obtained from the **GcmParamsSpec** for decryption.
>  3. The result of **doFinal()** may be **null**. To avoid exceptions, determine whether the result is **null** before using the **.data** field to access the **doFinal()** result.
>  4. For details about the sample code for calling **doFinal()** multiple times during RSA or SM2 asymmetric encryption and decryption, see [Encryption and Decryption](../../security/cryptoFramework-guidelines.md#encryption-and-decryption).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name    | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| data     | [DataBlob](#datablob)                 | Yes  | Data to encrypt or decrypt. It can be **null** in symmetric encryption or decryption, but cannot be {data:Uint8Array(empty)}.      |
| callback | AsyncCallback\<[DataBlob](#datablob)> | Yes  | Callback invoked to return the result. If the data is successfully encrypted or decrypted, **err** is **undefined**, and **data** is the **DataBlob** (encryption or decryption result of the remaining data). Otherwise, **err** is an error object.|

**Error codes**

| ID| Error Message               |
| -------- | ----------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.           |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

let cipher;        // The process of creating a Cipher instance is omitted here.
let data;           // The process of preparing the data to encrypt or decrypt is omitted here.
// The init() and update() processes are omitted here.
cipher.doFinal(data, (err, output) => {
  if (err) {
    console.error(`Failed to finalize cipher, ${err.code}, ${err.message}`);
  } else {
    console.info(`Finalize cipher success`);
    if (output != null) {
      // Concatenate output.data to obtain the complete plaintext/ciphertext (and authTag).
    }
  }
})
```

### doFinal

doFinal(data: DataBlob): Promise\<DataBlob>

 (1) Encrypts or decrypts the remaining data (generated by the block cipher mode) and the data passed in by **doFinal()** to finalize the symmetric encryption or decryption. This API uses a promise to return the encrypted or decrypted data. <br>If a small amount of data needs to be encrypted or decrypted, you can use **doFinal()** to pass in data without using **update()**. If all the data has been passed in by [update()](#update-4), you can pass in **null** in **data** of **doFinal()**. <br>The output of **doFinal()** varies with the symmetric encryption/decryption mode in use.

- Symmetric encryption in GCM and CCM mode: The result consists of the ciphertext and **authTag** (the last 16 bytes for GCM and the last 12 bytes for CCM). If **null** is passed in by **data** of **doFinal()**, the result of **doFinal()** is **authTag**. <br>**authTag** must be [GcmParamsSpec](#gcmparamsspec) or [CcmParamsSpec](#ccmparamsspec) used for decryption. The ciphertext is the **data** passed in for decryption.
- Symmetric encryption and decryption in other modes and symmetric decryption in GCM and CCM modes: The result is the complete plaintext/ciphertext.

 (2) Encrypts or decrypts the input data for RSA or SM2 asymmetric encryption/decryption. This API uses a promise to return the result. If a large amount of data needs to be encrypted/decrypted, call **doFinal()** multiple times and concatenate the result of each **doFinal()** to obtain the complete plaintext/ciphertext.

> **NOTE**
>
>  1. In symmetric encryption or decryption, calling **doFinal()** means the end of an  encryption or decryption process, and the [Cipher](#cipher) instance state will be cleared. To start a new encryption or decryption operation, you must call [init()](#init-2) to pass in a complete parameter list for initialization. <br>For example, if the same symmetric key is used for a **Cipher** instance to perform encryption and then decryption. After the encryption is complete, the **params** in **init** for decryption must be set instead of being **null**.
>  2. If a decryption fails, check whether the data to be encrypted and decrypted matches the parameters in **[init](#init-2)**. For the GCM mode, check whether the **authTag** obtained after encryption is obtained from the **GcmParamsSpec** for decryption.
>  3. The result of **doFinal()** may be **null**. To avoid exceptions, determine whether the result is **null** before using the **.data** field to access the **doFinal()** result.
>  4. For details about the sample code for calling **doFinal()** multiple times during RSA or SM2 asymmetric encryption and decryption, see [Encrypting and Decrypting Data](../../security/cryptoFramework-guidelines.md#encryption-and-decryption).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type                 | Mandatory| Description                |
| ---- | --------------------- | ---- | -------------------- |
| data | [DataBlob](#datablob) | Yes  | Data to encrypt or decrypt. It can be **null**, but cannot be {data:Uint8Array(empty)}.|

**Return value**

| Type                           | Description                                            |
| ------------------------------- | ------------------------------------------------ |
| Promise\<[DataBlob](#datablob)> | Promise used to return the **DataBlob**, which is the encryption or decryption result of the remaining data.|

**Error codes**

| ID| Error Message                                    |
| -------- | -------------------------------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.                                |
| 17620002 | runtime error.                               |
| 17630001 | crypto operation error.                      |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

let cipher;        // The process of creating a Cipher instance is omitted here.
let data;           // The process of preparing the data to encrypt or decrypt is omitted here.
// The init() and update() processes are omitted here.
cipher.doFinal(data)
.then(output => {
  console.info(`Finalize cipher success`);
    if (output != null) {
    // Concatenate output.data to obtain the complete plaintext/ciphertext (and authTag).
  }
}, error => {
  console.error(`Failed to finalize cipher, ${error.code}, ${error.message}`);
})
```

**RSA encryption example (callback)**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

function stringToUint8Array(str) {
  let arr = [];
  for (let i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  return new Uint8Array(arr);
}

let rsaGenerator = cryptoFramework.createAsyKeyGenerator("RSA1024|PRIMES_2");
let cipher = cryptoFramework.createCipher("RSA1024|PKCS1");
rsaGenerator.generateKeyPair(function (err, keyPair) {
  let pubKey = keyPair.pubKey;
  cipher.init(cryptoFramework.CryptoMode.ENCRYPT_MODE, pubKey, null, function (err, data) {
    let plainText = "this is cipher text";
    let input = {data: stringToUint8Array(plainText) };
    cipher.doFinal(input, function (err, data) {
      AlertDialog.show({ message: "EncryptOutPut is " + data.data} );
    });
  });
});
```

**RSA encryption example (promise)**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

function stringToUint8Array(str) {
  let arr = [];
  for (let i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  return new Uint8Array(arr);
}

let rsaGenerator = cryptoFramework.createAsyKeyGenerator("RSA1024|PRIMES_2");
let cipher = cryptoFramework.createCipher("RSA1024|PKCS1");
let keyGenPromise = rsaGenerator.generateKeyPair();
keyGenPromise.then(rsaKeyPair => {
  let pubKey = rsaKeyPair.pubKey;
  return cipher.init(cryptoFramework.CryptoMode.ENCRYPT_MODE, pubKey, null); // Pass in the private key and DECRYPT_MODE to initialize the decryption mode.
}).then(() => {
  let plainText = "this is cipher text";
  let input = { data: stringToUint8Array(plainText) };
  return cipher.doFinal(input);
}).then(dataBlob => {
  console.info("EncryptOutPut is " + dataBlob.data);
});
```

> **NOTE**
>
> For more encryption and decryption examples, see [Encryption and Decryption](../../security/cryptoFramework-guidelines.md#encryption-and-decryption).

### setCipherSpec<sup>10+</sup>

setCipherSpec(itemType: CipherSpecItem, itemValue: Uint8Array): void

Sets cipher specifications. You can use this API to set cipher specifications that cannot be set by [createCipher](#cryptoframeworkcreatecipher). Currently, only the RSA is supported.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description      |
| -------- | -------------------- | ---- | ---------- |
| itemType     | [CipherSpecItem](#cipherspecitem10)           | Yes  | Cipher parameter to set.|
| itemValue | Uint8Array | Yes  | Value of the parameter to set.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

let cipher; // The process of generating the Cipher instance is omitted here.
let pSource = new Uint8Array([1,2,3,4]);
cipher.setCipherSpec(cryptoFramework.CipherSpecItem.OAEP_MGF1_PSRC_UINT8ARR, pSource);
```

### getCipherSpec<sup>10+</sup>

getCipherSpec(itemType: CipherSpecItem): string | Uint8Array

Obtains cipher specifications. Currently, only the RSA is supported.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| itemType   | [CipherSpecItem](#cipherspecitem10) | Yes  | Cipher parameter to obtain.|

**Return value**

| Type          | Description       |
| -------------- | ----------- |
| string\|Uint8Array | Returns the value of the cipher parameter obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from '@ohos.security.cryptoFramework';

let cipher; // The process of generating the Cipher instance is omitted here.
let mdName = cipher.getCipherSpec(cryptoFramework.CipherSpecItem.OAEP_MD_NAME_STR);
```

## cryptoFramework.createSign

createSign(algName: string): Sign

Creates a **Sign** instance.<br>For details about the supported specifications, see [Signing and Signature Verification Specifications](../../security/cryptoFramework-overview.md#signing-and-signature-verification-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                                                        |
| ------- | ------ | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Signing algorithm, which can be RSA, ECC, DSA, or SM2<sup>10+</sup>. If the RSA PKCS1 mode is used, you need to set the digest. If the RSA PSS mode is used, you need to set the digest and mask digest.|

**Return value**

| Type| Description                              |
| ---- | ---------------------------------- |
| Sign | Returns the **Sign** instance created.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let signer1 = cryptoFramework.createSign("RSA1024|PKCS1|SHA256");

let signer2 = cryptoFramework.createSign("RSA1024|PSS|SHA256|MGF1_SHA256");

let signer3 = cryptoFramework.createSign("ECC224|SHA256");

let signer4 = cryptoFramework.createSign("DSA2048|SHA256");
```

## Sign

Provides APIs for signing. Before using any API of the **Sign** class, you must create a **Sign** instance by using **createSign(algName: string): Sign**. Invoke **init()**, **update()**, and **sign()** in this class in sequence to complete the signing operation. For details about the sample code, see [Signing and Signature Verification](../../security/cryptoFramework-guidelines.md#signing-and-signature-verification).

The **Sign** class does not support repeated initialization. When a new key is used for signing, you must create a new **Sign** object and call **init()** for initialization.

The signing mode is determined in **createSign()**, and the key is set by **init()**.

If the data to be signed is short, you can directly call **sign()** to pass in the original data for signing after **init()**. That is, you do not need to use **update()**.

If the data to be signed is long, you can use **update()** to pass in the data by segment, and then use **sign()** to sign the entire data.

If **update()** is used to pass in data by segment, **data** of **sign()** can be **null**.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| algName | string | Yes  | No  | Algorithm to use.|

### init

init(priKey: PriKey, callback: AsyncCallback\<void>): void

Initializes a **Sign** object using a private key. This API uses an asynchronous callback to return the result. The **Sign** class does not support repeated calling of **init()**.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description            |
| -------- | -------------------- | ---- | ---------------- |
| priKey   | [PriKey](#prikey)    | Yes  | Private key used for the initialization.|
| callback | AsyncCallback\<void> | Yes  | Callback invoked to return the result.     |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### init

init(priKey: PriKey): Promise\<void>

Initializes a **Sign** object using a private key. This API uses a promise to return the result. The **Sign** class does not support repeated calling of **init()**.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type| Mandatory| Description            |
| ------ | ---- | ---- | ---------------- |
| priKey | [PriKey](#prikey)  | Yes  | Private key used for the initialization.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### update

update(data: DataBlob, callback: AsyncCallback\<void>): void

Updates the data to be signed. This API uses a callback to complete the update. <br>This API can be called only after the [Sign](#sign) instance is initialized by using [init()](init-2).

> **NOTE**
>
> **update()** may be called multiple times or may not be called (call [sign](#sign-1) after [init](#init-2)), depending on the size of the data.
> The algorithm library does not set a limit on the amount of data to be updated (once or accumulatively). If a large amount of data needs to be signed, you are advised to use **update()** multiple times to pass in data. This can prevent too much memory from being requested at a time.
> For details about the sample code for calling **update()** multiple times, see [Signing and Signature verification](../../security/cryptoFramework-guidelines.md#signing-and-signature-verification).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                 | Mandatory| Description        |
| -------- | --------------------- | ---- | ------------ |
| data     | [DataBlob](#datablob) | Yes  | Data to pass in.|
| callback | AsyncCallback\<void>  | Yes  | Callback invoked to return the result.  |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### update

update(data: DataBlob): Promise\<void>

Updates the data to be signed. This API uses a promise to return the result. <br>This API can be called only after the [Sign](#sign) instance is initialized by using [init()](#init-3).

> **NOTE**
>
> **update()** may be called multiple times or may not be called (call [sign](#sign-2) after [init](#init-3)), depending on the size of the data.<br>
> The algorithm library does not set a limit on the amount of data to be updated (once or accumulatively). If a large amount of data needs to be signed, you are advised to use **update()** multiple times to pass in data. This can prevent too much memory from being requested at a time.<br>
> For details about the sample code for calling **update()** multiple times, see [Signing and Signature verification](../../security/cryptoFramework-guidelines.md#signing-and-signature-verification).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| data   | [DataBlob](#datablob)  | Yes  | Data to pass in.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### sign

sign(data: DataBlob, callback: AsyncCallback\<DataBlob>): void

Signs the data. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description      |
| -------- | -------------------- | ---- | ---------- |
| data     | [DataBlob](#datablob)              | Yes  | Data to pass in.|
| callback | AsyncCallback\<[DataBlob](#datablob) > | Yes  | Callback invoked to return the result. |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### sign

sign(data: DataBlob): Promise\<DataBlob>

Signs the data. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| data   | [DataBlob](#datablob)  | Yes  | Data to pass in.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

**Callback example**:

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

function stringToUint8Array(str) {
  var arr = [];
  for (var i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  var tmpArray = new Uint8Array(arr);
  return tmpArray;
}

let globalKeyPair;
let SignMessageBlob;
let plan1 = "This is Sign test plan1"; // The first segment of the data.
let plan2 = "This is Sign test plan2"; // The second segment of the data.
let input1 = { data: stringToUint8Array(plan1) };
let input2 = { data: stringToUint8Array(plan2) };

function signMessageCallback() {
  let rsaGenerator = cryptoFramework.createAsyKeyGenerator("RSA1024|PRIMES_2");
  let signer = cryptoFramework.createSign("RSA1024|PKCS1|SHA256");
  rsaGenerator.generateKeyPair(function (err, keyPair) {
    globalKeyPair = keyPair;
    let priKey = globalKeyPair.priKey;
    signer.init(priKey, err => {
      signer.update(input1, err => { // add first segment of data
        signer.sign(input2, function (err, data) { // add second segment of data, sign input1 and input2
          SignMessageBlob = data;
          AlertDialog.show({message: "res" +  SignMessageBlob.data});
        });
      });
    });
  });
}
```

**Promise example**:

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

function stringToUint8Array(str) {
  var arr = [];
  for (var i = 0, j = str.length; i < j; ++i) {
    arr.push(str.charCodeAt(i));
  }
  var tmpArray = new Uint8Array(arr);
  return tmpArray;
}

let globalKeyPair;
let SignMessageBlob;
let plan1 = "This is Sign test plan1"; // The first segment of the data.
let plan2 = "This is Sign test plan2"; // The second segment of the data.
let input1 = { data: stringToUint8Array(plan1) };
let input2 = { data: stringToUint8Array(plan2) };

function signMessagePromise() {
  let rsaGenerator = cryptoFramework.createAsyKeyGenerator("RSA1024|PRIMES_2");
  let signer = cryptoFramework.createSign("RSA1024|PKCS1|SHA256");
  let keyGenPromise = rsaGenerator.generateKeyPair();
  keyGenPromise.then( keyPair => {
    globalKeyPair = keyPair;
    let priKey = globalKeyPair.priKey;
    return signer.init(priKey);
  }).then(() => {
    return signer.update(input1); // Add the first segment of the data.
  }).then(() => {
    return signer.sign(input2); // Add the second segment of the data, and sign input1 and input2.
  }).then(dataBlob => {
    SignMessageBlob = dataBlob;
    console.info("sign output is " + SignMessageBlob.data);
    AlertDialog.show({message: "output" +  SignMessageBlob.data});
  });
}
```

### setSignSpec<sup>10+</sup>

setSignSpec(itemType: SignSpecItem, itemValue: number): void

Sets signing specifications. You can use this API to set signing parameters that cannot be set by [createSign](#cryptoframeworkcreatesign). Currently, only the RSA is supported.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description      |
| -------- | -------------------- | ---- | ---------- |
| itemType     | [SignSpecItem](#signspecitem10)              | Yes  | Signing parameter to set.|
| itemValue | number | Yes  | Value of the signing parameter to set.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let signer; // The process of generating the Sign instance is omitted here.
let setN = 20;
signer.setSignSpec(cryptoFramework.SignSpecItem.PSS_SALT_LEN_NUM, setN);
```

### getSignSpec<sup>10+</sup>

getSignSpec(itemType: SignSpecItem): string | number

Obtains signing specifications. Currently, only the RSA is supported.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| itemType | [SignSpecItem](#signspecitem)  | Yes  | Signing parameter to obtain.|

**Return value**

| Type          | Description       |
| -------------- | ----------- |
| string\|number | Returns the value of the signing parameter obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let signer; // The process of generating the Sign instance is omitted here.
let saltLen = signer.getSignSpec(cryptoFramework.SignSpecItem.PSS_SALT_LEN_NUM);
```

## cryptoFramework.createVerify

createVerify(algName: string): Verify

Creates a **Verify** instance. <br>For details about the supported specifications, see [Signing and Signature Verification Specifications](../../security/cryptoFramework-overview.md#signing-and-signature-verification-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                                                        |
| ------- | ------ | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Signing algorithm, which can be RSA, ECC, DSA, or SM2<sup>10+</sup>. If the RSA PKCS1 mode is used, you need to set the digest. If the RSA PSS mode is used, you need to set the digest and mask digest.|

**Return value**

| Type  | Description                                |
| ------ | ------------------------------------ |
| Verify | Returns the **Verify** instance created.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let verifyer1 = cryptoFramework.createVerify("RSA1024|PKCS1|SHA256");

let verifyer2 = cryptoFramework.createVerify("RSA1024|PSS|SHA256|MGF1_SHA256")
```

## Verify

Provides APIs for signature verification. Before using any API of the **Verify** class, you must create a **Verify** instance by using **createVerify(algName: string): Verify**. Invoke **init()**, **update()**, and **sign()** in this class in sequence to complete the signature verification. For details about the sample code, see [Signing and Signature Verification](../../security/cryptoFramework-guidelines.md#signing-and-signature-verification).

The **Verify** class does not support repeated initialization. When a new key is used for signature verification, you must create a new **Verify** object and call **init()** for initialization.

The signature verification mode is determined in **createVerify()**, and key is set by **init()**.

If the signed message is short, you can call **verify()** to pass in the signed message and signature (**signatureData**) for signature verification after **init()**. That is, you do not need to use **update()**.

If the signed message is too long, you can call **update()** multiple times to pass in the signed message by segment, and then call **verify()** to verify the full text of the message. The **data** parameter of **verify()** can be null. The service can call **update()** multiple times in the loop. When the loop ends, the service calls **verify()** to pass in the signature (**signatureData**) for signature verification.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| algName | string | Yes  | No  | Algorithm to be used for signature verification.|

### init

init(pubKey: PubKey, callback: AsyncCallback\<void>): void

Initializes the **Verify** instance using a public key. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description                          |
| -------- | -------------------- | ---- | ------------------------------ |
| pubKey   | [PubKey](#pubkey)    | Yes  | Public key used to initialize the **Verify** instance.|
| callback | AsyncCallback\<void> | Yes  | Callback invoked to return the result.                    |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### init

init(pubKey: PubKey): Promise\<void>

Initializes the **Verify** instance using a public key. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type| Mandatory| Description                        |
| ------ | ---- | ---- | ---------------------------- |
| pubKey | [PubKey](#pubkey)  | Yes  | Public key used to initialize the **Verify** instance.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### update

update(data: DataBlob, callback: AsyncCallback\<void>): void

Updates the data for signature verification. This API uses an asynchronous callback to return the result. <br>This API can be called only after the [Verify](#verify) instance is initialized using [init()](#init-4).

> **NOTE**
>
> **update()** may be called multiple times or may not be called (call [verify](#verify-1) after [init](#init-4)), depending on the size of the data.<br>
> The algorithm library does not set a limit on the amount of data to be updated (once or accumulatively). If a large amount of data is involved in signature verification, you are advised to use **update()** multiple times to pass in data. This can prevent too much memory from being requested at a time.<br>
> For details about the sample code for calling **update()** multiple times, see [Signing and Signature verification](../../security/cryptoFramework-guidelines.md#signing-and-signature-verification).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                 | Mandatory| Description        |
| -------- | --------------------- | ---- | ------------ |
| data     | [DataBlob](#datablob) | Yes  | Data to pass in.|
| callback | AsyncCallback\<void>  | Yes  | Callback invoked to return the result.  |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### update

update(data: DataBlob): Promise\<void>

Updates the data for signature verification. This API uses a promise to return the result. <br>This API can be called only after the [Verify](#verify) instance is initialized using [init()](#init-5).

> **NOTE**
>
> **update()** may be called multiple times or may not be called (call [verify](#verify-2) after [init](#init-5)), depending on the size of the data.
> The algorithm library does not set a limit on the amount of data to be updated (once or accumulatively). If a large amount of data is involved in signature verification, you are advised to use **update()** multiple times to pass in data. This can prevent too much memory from being requested at a time.<br>
> For details about the sample code for calling **update()** multiple times, see [Signing and Signature verification](../../security/cryptoFramework-guidelines.md#signing-and-signature-verification).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| data   | [DataBlob](#datablob)  | Yes  | Data to pass in.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### verify

verify(data: DataBlob, signatureData: DataBlob, callback: AsyncCallback\<boolean>): void

Verifies the signature. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name       | Type                | Mandatory| Description      |
| ------------- | -------------------- | ---- | ---------- |
| data          | [DataBlob](#datablob)              | Yes  | Data to pass in.|
| signatureData | [DataBlob](#datablob)              | Yes  | Signature data. |
| callback      | AsyncCallback\<boolean> | Yes  | Callback invoked to return the result. |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### verify

verify(data: DataBlob, signatureData: DataBlob): Promise\<boolean>

Verifies the signature. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name       | Type    | Mandatory| Description      |
| ------------- | -------- | ---- | ---------- |
| data          | [DataBlob](#datablob)  | Yes  | Data to pass in.|
| signatureData | [DataBlob](#datablob)  | Yes  | Signature data. |

**Return value**

| Type             | Description                          |
| ----------------- | ------------------------------ |
| Promise\<boolean> | Promise used to return the result.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

**Callback example**:

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let globalKeyPair; // globalKeyPair is an asymmetric key object generated by the asymmetric key generator. The generation process is omitted here.
let input1 = null;
let input2 = null;
let signMessageBlob = null; // Signed data, which is omitted here.
let verifyer = cryptoFramework.createVerify("RSA1024|PKCS1|SHA25");
verifyer.init(globalKeyPair.pubKey, function (err, data) {
  verifyer.update(input1, function(err, data) {
    verifyer.verify(input2, signMessageBlob, function(err, data) {
      console.info("verify result is " + data);
    })
  });
})
```

**Promise example**:

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let globalKeyPair; // globalKeyPair is an asymmetric key object generated by the asymmetric key generator. The generation process is omitted here.
let verifyer = cryptoFramework.createVerify("RSA1024|PKCS1|SHA256");
let verifyInitPromise = verifyer.init(globalKeyPair.pubKey);
let input1 = null;
let input2 = null;
let signMessageBlob = null; // Signed data, which is omitted here.
verifyInitPromise.then(() => {
  return verifyer.update(input1);
}).then(() => {
  return verifyer.verify(input2, signMessageBlob);
}).then(res => {
  console.log("Verify result is " + res);
});
```

### setVerifySpec<sup>10+</sup>

setVerifySpec(itemType: SignSpecItem, itemValue: number): void

Set signature verification specifications. You can use this API to set signature verification parameters that cannot be set by [createVerify](#cryptoframeworkcreateverify). Currently, only the RSA is supported.

The parameters for signature verification must be the same as those for signing.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description      |
| -------- | -------------------- | ---- | ---------- |
| itemType     | [SignSpecItem](#signspecitem10)              | Yes  | Signature verification parameter to set.|
| itemValue | number | Yes  | Value of the signature verification parameter to set.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let verifyer; //The process of generating the Verify instance is omitted here.
let setN = 20;
verifyer.setVerifySpec(cryptoFramework.SignSpecItem.PSS_SALT_LEN_NUM, setN);
```

### getVerifySpec<sup>10+</sup>

getVerifySpec(itemType: SignSpecItem): string | number

Obtains signature verification specifications. Currently, only the RSA is supported.

The parameters for signature verification must be the same as those for signing.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| itemType   | [SignSpecItem](#signspecitem10)  | Yes  | Signature verification parameter to obtain.|

**Return value**

| Type          | Description       |
| -------------- | ----------- |
| string\|number | Returns the value of the parameter obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let verifyer; //The process of generating the Verify instance is omitted here.
let saltLen = verifyer.getSignSpec(cryptoFramework.SignSpecItem.PSS_SALT_LEN_NUM);
```

## cryptoFramework.createKeyAgreement

createKeyAgreement(algName: string): KeyAgreement

Creates a **KeyAgreement** instance. <br>For details about the supported specifications, see [Key Agreement Specifications](../../security/cryptoFramework-overview.md#key-agreement-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                             |
| ------- | ------ | ---- | --------------------------------- |
| algName | string | Yes  | Key agreement algorithm to use. Currently, only the ECC is supported.|

**Return value**

| Type        | Description                                      |
| ------------ | ------------------------------------------ |
| KeyAgreement | Returns the **KeyAgreement** instance created.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 801 | this operation is not supported.          |
| 17620001 | memory error.          |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let keyAgreement = cryptoFramework.createKeyAgreement("ECC256");

```

## KeyAgreement

Provides APIs for key agreement operations. Before using any API of the **KeyAgreement** class, you must create a **KeyAgreement** instance by using **createKeyAgreement(algName: string): KeyAgreement**.

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                        |
| ------- | ------ | ---- | ---- | ---------------------------- |
| algName | string | Yes  | No  | Algorithm used for key agreement.|

### generateSecret

generateSecret(priKey: PriKey, pubKey: PubKey, callback: AsyncCallback\<DataBlob>): void

Generates a shared secret. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                    | Mandatory| Description                  |
| -------- | ------------------------ | ---- | ---------------------- |
| priKey   | [PriKey](#prikey)        | Yes  | Private key used for key agreement.|
| pubKey   | [PubKey](#pubkey)        | Yes  | Public key used for key agreement.|
| callback | AsyncCallback\<[DataBlob](#datablob)> | Yes  | Callback invoked to return the shared secret.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

### generateSecret

generateSecret(priKey: PriKey, pubKey: PubKey): Promise\<DataBlob>

Generates a shared secret. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type  | Mandatory| Description                  |
| ------ | ------ | ---- | ---------------------- |
| priKey | [PriKey](#prikey) | Yes  | Private key used for key agreement.|
| pubKey | [PubKey](#pubkey) | Yes  | Public key used for key agreement.|

**Return value**

| Type              | Description    |
| ------------------ | -------- |
| Promise\<[DataBlob](#datablob)> | Promise used to return the shared secret.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17620002 | runtime error.          |
| 17630001 | crypto operation error. |

**Callback example**:

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let globalKeyPair; // globalKeyPair is an asymmetric key object generated by the asymmetric key generator. The generation process is omitted here.
let keyAgreement = cryptoFramework.createKeyAgreement("ECC256");
keyAgreement.generateSecret(globalKeyPair.priKey, globalKeyPair.pubKey, function (err, secret) {
  if (err) {
    console.error("keyAgreement error.");
    return;
  }
  console.info("keyAgreement output is " + secret.data);
});
```

**Promise example**:

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

let globalKeyPair; // globalKeyPair is an asymmetric key object generated by the asymmetric key generator. The generation process is omitted here.
let keyAgreement = cryptoFramework.createKeyAgreement("ECC256");
let keyAgreementPromise = keyAgreement.generateSecret(globalKeyPair.priKey, globalKeyPair.pubKey);
keyAgreementPromise.then((secret) => {
  console.info("keyAgreement output is " + secret.data);
}).catch((error) => {
  console.error("keyAgreement error.");
});
```

## cryptoFramework.createMd

createMd(algName: string): Md

Creates an **Md** instance for message digest operations. <br>For details about the supported specifications, see [MD Algorithm Specifications](../../security/cryptoFramework-overview.md#md-algorithm-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                                                        |
| ------- | ------ | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Digest algorithm. For details about the supported algorithms, see [MD Algorithm Specifications](../../security/cryptoFramework-overview.md#md-algorithm-specifications).|

**Return value**

| Type| Description                                   |
| ---- | --------------------------------------- |
| Md   | Returns the [Md](#md) instance created.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 401 | invalid parameters.       |
| 17620001 | memory error.       |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var md;
try {
    // Set algName based on the algorithm supported.
    md = cryptoFramework.createMd("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
```

## Md

Provides APIs for message digest operations. Before using any API of the **Md** class, you must create an **Md** instance by using [createMd](#cryptoframeworkcreatemd).

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                  |
| ------- | ------ | ---- | ---- | ---------------------- |
| algName | string | Yes  | No  | Digest algorithm.|

### update

update(input: DataBlob, callback: AsyncCallback\<void>): void

Updates the message digest data. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> For details about the sample code for calling **update()** multiple times, see [Generating a Digest](../../security/cryptoFramework-guidelines.md#generating-a-digest).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                 | Mandatory| Description        |
| -------- | --------------------- | ---- | ------------ |
| input    | [DataBlob](#datablob) | Yes  | Data to pass in.|
| callback | AsyncCallback\<void>  | Yes  | Callback invoked to return the result.  |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.       |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var md;
try {
    md = cryptoFramework.createMd("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Md algName is: " + md.algName);

let blob;
md.update(blob, (err,) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    }
});
```

### update

update(input: DataBlob): Promise\<void>

Updates the message digest data. This API uses a promise to return the result.

> **NOTE**
>
> For details about the sample code for calling **update()** multiple times, see [Generating a Digest](../../security/cryptoFramework-guidelines.md#generating-a-digest).

**System capability**: SystemCapability.Security.CryptoFramework

| Name| Type    | Mandatory| Description        |
| ------ | -------- | ---- | ------------ |
| input  | DataBlob | Yes  | Data to pass in.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.       |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var md;
try {
    md = cryptoFramework.createMd("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Md algName is: " + md.algName);

let blob;
var promiseMdUpdate = md.update(blob);
promiseMdUpdate.then(() => {
    // do something
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});
```

### digest

digest(callback: AsyncCallback\<DataBlob>): void

Generates a message digest. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

| Name  | Type                    | Mandatory| Description      |
| -------- | ------------------------ | ---- | ---------- |
| callback | AsyncCallback\<DataBlob> | Yes  | Callback invoked to return the result.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var md;
try {
    md = cryptoFramework.createMd("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Md algName is: " + md.algName);

let blob;
md.update(blob, (err,) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    }
    md.digest((err1, mdOutput) => {
		if (err1) {
            console.error("[Callback] err: " + err1.code);
        } else {
            console.error("[Callback]: MD result: " + mdOutput);
        }
    });
});
```

### digest

digest(): Promise\<DataBlob>

Generates a message digest. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type              | Description       |
| ------------------ | ----------- |
| Promise\<[DataBlob](#datablob)> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var md;
try {
    md = cryptoFramework.createMd("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Md algName is: " + md.algName);

let blob;
var promiseMdUpdate = md.update(blob);
promiseMdUpdate.then(() => {
    var PromiseMdDigest = md.digest();
    return PromiseMdDigest;
}).then(mdOutput => {
    console.error("[Promise]: MD result: " + mdOutput.data);
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});
```

### getMdLength

getMdLength(): number

Obtains the message digest length, in bytes.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type  | Description                      |
| ------ | -------------------------- |
| number | Returns the length of the message digest obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var md;
try {
    md = cryptoFramework.createMd("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Md algName is: " + md.algName);

let blob;
var promiseMdUpdate = md.update(blob);
promiseMdUpdate.then(() => {
    var PromiseMdDigest = md.digest();
    return PromiseMdDigest;
}).then(mdOutput => {
    console.error("[Promise]: MD result: " + mdOutput.data);
    let mdLen = md.getMdLength();
	console.error("MD len: " + mdLen);
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});
```

## cryptoFramework.createMac

createMac(algName: string): Mac

Creates a **Mac** instance for message authentication code (MAC) operations. For details about the supported specifications, see [HMAC Algorithm Specifications](../../security/cryptoFramework-overview.md#hmac-algorithm-specifications).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name | Type  | Mandatory| Description                                                        |
| ------- | ------ | ---- | ------------------------------------------------------------ |
| algName | string | Yes  | Digest algorithm. For details about the supported algorithms, see [HMAC Algorithm Specifications](../../security/cryptoFramework-overview.md#hmac-algorithm-specifications).|

**Return value**

| Type| Description                                     |
| ---- | ----------------------------------------- |
| Mac  | Returns the [Mac](#mac) instance created.|

**Error codes**

| ID| Error Message          |
| -------- | ------------------ |
| 401 | invalid parameters.       |
| 17620001 | memory error.       |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var mac;
try {
    // Set algName based on the algorithm supported.
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
```

## Mac

Provides APIs for MAC operations. Before using any API of the **Mac** class, you must create a **Mac** instance by using [createMac](#cryptoframeworkcreatemac).

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                  |
| ------- | ------ | ---- | ---- | ---------------------- |
| algName | string | Yes  | No  | Digest algorithm.|

### init

init(key: SymKey, callback: AsyncCallback\<void>): void

Initializes the MAC computation using a symmetric key. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                | Mandatory| Description          |
| -------- | -------------------- | ---- | -------------- |
| key      | [SymKey](#symkey)    | Yes  | Shared symmetric key.|
| callback | AsyncCallback\<void> | Yes  | Callback invoked to return the result.    |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.       |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
var KeyBlob;
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
symKeyGenerator.convertKey(KeyBlob, (err, symKey) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    }
    mac.init(symKey, (err1, ) => {
        if (err1) {
            console.error("[Callback] err: " + err1.code);
        }
    });
});
```

### init

init(key: SymKey): Promise\<void>

Initializes the MAC computation using a symmetric key. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type  | Mandatory| Description        |
| ------ | ------ | ---- | ------------ |
| key    | [SymKey](#symkey) | Yes  | Shared symmetric key.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.       |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Mac algName is: " + mac.algName);

var KeyBlob;
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
var promiseConvertKey = symKeyGenerator.convertKey(KeyBlob);
promiseConvertKey.then(symKey => {
    var promiseMacInit = mac.init(symKey);
    return promiseMacInit;
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});

```

### update

update(input: DataBlob, callback: AsyncCallback\<void>): void

Updates the MAC computation data. This API uses an asynchronous callback to return the result.

> **NOTE**
>
> For details about the sample code for calling **update()** multiple times, see [Generating a MAC](../../security/cryptoFramework-guidelines.md#generating-a-mac).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                 | Mandatory| Description        |
| -------- | --------------------- | ---- | ------------ |
| input    | [DataBlob](#datablob) | Yes  | Data to pass in.|
| callback | AsyncCallback\<void>  | Yes  | Callback invoked to return the result.  |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.       |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var KeyBlob;
var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
symKeyGenerator.convertKey(KeyBlob, (err, symKey) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    }
    mac.init(symKey, (err1, ) => {
        if (err1) {
            console.error("[Callback] err: " + err1.code);
        }
        let blob;
      	mac.update(blob, (err2, data) => {
        	if (err2) {
            console.error("[Callback] err: " + err2.code);
        	}
      	});
    });
});
```

### update

update(input: DataBlob): Promise\<void>

Updates the MAC computation data. This API uses a promise to return the result.

> **NOTE**
>
> For details about the sample code for calling **update()** multiple times, see [Generating a MAC](../../security/cryptoFramework-guidelines.md#generating-a-mac).

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type    | Mandatory| Description      |
| ------ | -------- | ---- | ---------- |
| input  | [DataBlob](#datablob) | Yes  | Data to pass in.|

**Return value**

| Type          | Description         |
| -------------- | ------------- |
| Promise\<void> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.       |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Mac algName is: " + mac.algName);

var KeyBlob;
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
var promiseConvertKey = symKeyGenerator.convertKey(KeyBlob);
promiseConvertKey.then(symKey => {
    var promiseMacInit = mac.init(symKey);
    return promiseMacInit;
}).then(() => {
    let blob;
    var promiseMacUpdate = mac.update(blob);
    return promiseMacUpdate;
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});

```

### doFinal

doFinal(callback: AsyncCallback\<DataBlob>): void

Finalizes the MAC computation. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                    | Mandatory| Description    |
| -------- | ------------------------ | ---- | -------- |
| callback | AsyncCallback\<[DataBlob](#datablob)> | Yes  | Callback invoked to return the result.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var KeyBlob;
var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
symKeyGenerator.convertKey(KeyBlob, (err, symKey) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    }
    mac.init(symKey, (err1, ) => {
        if (err1) {
            console.error("[Callback] err: " + err1.code);
        }
        let blob;
        mac.update(blob, (err2, ) => {
            if (err2) {
                console.error("[Callback] err: " + err2.code);
            }
            mac.doFinal((err3, macOutput) => {
                if (err3) {
                    console.error("[Callback] err: " + err3.code);
                } else {
                    console.error("[Promise]: HMAC result: " + macOutput);
                }
            });
        });
    });
});
```

### doFinal

doFinal(): Promise\<DataBlob>

Finalizes the MAC computation. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type              | Description       |
| ------------------ | ----------- |
| Promise\<[DataBlob](#datablob)> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Mac algName is: " + mac.algName);

var KeyBlob;
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
var promiseConvertKey = symKeyGenerator.convertKey(KeyBlob);
promiseConvertKey.then(symKey => {
    var promiseMacInit = mac.init(symKey);
    return promiseMacInit;
}).then(() => {
    let blob;
    var promiseMacUpdate = mac.update(blob);
    return promiseMacUpdate;
}).then(() => {
    var PromiseMacDoFinal = mac.doFinal();
    return PromiseMacDoFinal;
}).then(macOutput => {
    console.error("[Promise]: HMAC result: " + macOutput.data);
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});
```

### getMacLength

getMacLength(): number

Obtains the MAC length, in bytes.

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type  | Description                       |
| ------ | --------------------------- |
| number | Returns the MAC length obtained.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var mac;
try {
    mac = cryptoFramework.createMac("SHA256");
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
console.error("Mac algName is: " + mac.algName);

var KeyBlob;
var symKeyGenerator = cryptoFramework.createSymKeyGenerator("AES128");
var promiseConvertKey = symKeyGenerator.convertKey(KeyBlob);
promiseConvertKey.then(symKey => {
    var promiseMacInit = mac.init(symKey);
    return promiseMacInit;
}).then(() => {
    let blob;
    var promiseMacUpdate = mac.update(blob);
    return promiseMacUpdate;
}).then(() => {
    var PromiseMacDoFinal = mac.doFinal();
    return PromiseMacDoFinal;
}).then(macOutput => {
    console.error("[Promise]: HMAC result: " + macOutput.data);
    let macLen = mac.getMacLength();
	console.error("MAC len: " + macLen);
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});
```

## cryptoFramework.createRandom

createRandom(): Random

Creates a **Random** instance for generating random numbers and setting seeds. <br>For details about the supported specifications, see [Random Number](../../security/cryptoFramework-overview.md#random-number).

**System capability**: SystemCapability.Security.CryptoFramework

**Return value**

| Type  | Description                                           |
| ------ | ----------------------------------------------- |
| Random | Returns the [Random](#random) instance created.|

**Error codes**

| ID| Error Message    |
| -------- | ------------ |
| 17620001 | memory error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

try {
    var rand = cryptoFramework.createRandom();
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
```

## Random

Provides APIs for computing random numbers and setting seeds. Before using any API of the **Random** class, you must create a **Random** instance by using [createRandom](#cryptoframeworkcreaterandom).

### Attributes

**System capability**: SystemCapability.Security.CryptoFramework

| Name   | Type  | Readable| Writable| Description                |
| ------- | ------ | ---- | ---- | -------------------- |
| algName<sup>10+</sup> | string | Yes  | No  | Algorithm used to generate the random number. Currently, only **CTR_DRBG** is supported.|

### generateRandom

generateRandom(len: number, callback: AsyncCallback\<DataBlob>): void

Generates a random number of the specified length. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name  | Type                    | Mandatory| Description                |
| -------- | ------------------------ | ---- | -------------------- |
| len      | number                   | Yes  | Length of the random number to generate, in bytes. The value range is [1, INT_MAX].|
| callback | AsyncCallback\<[DataBlob](#datablob)> | Yes  | Callback invoked to return the result.           |

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.          |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var rand;
try {
    rand = cryptoFramework.createRandom();
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}
rand.generateRandom(12, (err, randData) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    } else {
        console.error("[Callback]: generate random result: " + randData.data);
    }
});
```

### generateRandom

generateRandom(len: number): Promise\<DataBlob>

Generates a random number of the specified length. This API uses a promise to return the result.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type  | Mandatory| Description                                                  |
| ------ | ------ | ---- | ------------------------------------------------------ |
| len    | number | Yes  | Length of the random number to generate, in bytes. The value range is [1, INT_MAX].|

**Return value**

| Type              | Description       |
| ------------------ | ----------- |
| Promise\<[DataBlob](#datablob)> | Promise that returns no value.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var rand;
try {
    rand = cryptoFramework.createRandom();
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}

var promiseGenerateRand = rand.generateRandom(12);
promiseGenerateRand.then(randData => {
    console.error("[Promise]: rand result: " + randData.data);
}).catch(error => {
    console.error("[Promise]: error: " + error.message);
});
```

### generateRandomSync<sup>10+</sup>

generateRandomSync(len: number): DataBlob

Generates a random number of the specified length synchronously.

**System capability**: SystemCapability.Security.CryptoFramework

**Parameters**

| Name| Type  | Mandatory| Description                |
| ------ | ------ | ---- | -------------------- |
| len    | number | Yes  | Length of the random number to generate, in bytes. The value range is [1, INT_MAX].|

**Return value**

| Type              | Description       |
| ------------------ | ----------- |
|[DataBlob](#datablob) | Returns the generated random number.|

**Error codes**

| ID| Error Message              |
| -------- | ---------------------- |
| 401 | invalid parameters.          |
| 17620001 | memory error.           |
| 17630001 | crypto operation error. |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var rand;
try {
    rand = cryptoFramework.createRandom();
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}

try {
  let randData = rand.generateRandomSync(12);
  if (randData != null) {
    console.info("[Sync]: rand result: " + randData.data);
  } else {
    console.error("[Sync]: get rand result fail!");
  }
} catch (error) {
  console.error("[Sync]: error: " + error.message);
}
```

### setSeed

setSeed(seed: DataBlob): void

Sets a seed.

**System capability**: SystemCapability.Security.CryptoFramework

| Name| Type    | Mandatory| Description        |
| ------ | -------- | ---- | ------------ |
| seed   | DataBlob | Yes  | Seed to set.|

**Error codes**

| ID| Error Message          |
| -------- | ----------------- |
| 17620001 | memory error.      |

**Example**

```js
import cryptoFramework from "@ohos.security.cryptoFramework"

var rand;
try {
    rand = cryptoFramework.createRandom();
} catch (error) {
    console.error("[Sync]: error code: " + error.code + ", message is: " + error.message);
}

rand.generateRandom(12, (err, randData) => {
    if (err) {
        console.error("[Callback] err: " + err.code);
    } else {
        console.info("[Callback]: generate random result: " + randData.data);
        try {
            rand.setSeed(randData);
        } catch (error) {
            console.error("setSeed failed, errCode: " + error.code + ", errMsg: " + error.message);
        }
    }
});
```
