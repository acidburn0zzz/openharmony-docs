# HuksKeyApi


## Overview

Describes the OpenHarmony Universal KeyStore (HUKS) capabilities, including key management and cryptography operations, provided for applications. The keys managed by HUKS can be imported by applications or generated by calling the HUKS APIs.

\@syscap SystemCapability.Security.Huks

**Since:**
9


## Summary


### Files

| Name | Description | 
| -------- | -------- |
| [native_huks_api.h](native__huks__api_8h.md) | Declares the APIs used to access the HUKS. <br>File to Include: <huks/native_huks/api.h> | 


### Functions

| Name | Description | 
| -------- | -------- |
| [OH_Huks_GetSdkVersion](#oh_huks_getsdkversion) (struct [OH_Huks_Blob](_o_h___huks___blob.md) \*sdkVersion) | Obtains the current HUKS SDK version.  | 
| [OH_Huks_GenerateKeyItem](#oh_huks_generatekeyitem) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSetIn, struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSetOut) | Generates a key.  | 
| [OH_Huks_ImportKeyItem](#oh_huks_importkeyitem) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*key) | Imports a key in plaintext.  | 
| [OH_Huks_ImportWrappedKeyItem](#oh_huks_importwrappedkeyitem) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*wrappingKeyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*wrappedKeyData) | Imports a wrapped key.  | 
| [OH_Huks_ExportPublicKeyItem](#oh_huks_exportpublickeyitem) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, struct [OH_Huks_Blob](_o_h___huks___blob.md) \*key) | Exports a public key.  | 
| [OH_Huks_DeleteKeyItem](#oh_huks_deletekeyitem) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet) | Deletes a key.  | 
| [OH_Huks_GetKeyItemParamSet](#oh_huks_getkeyitemparamset) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSetIn, struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSetOut) | Obtains the attributes of a key.  | 
| [OH_Huks_IsKeyItemExist](#oh_huks_iskeyitemexist) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet) | Checks whether a key exists.  | 
| [OH_Huks_AttestKeyItem](#oh_huks_attestkeyitem) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, struct [OH_Huks_CertChain](_o_h___huks___cert_chain.md) \*certChain) | Obtain the key certificate chain.  | 
| [OH_Huks_InitSession](#oh_huks_initsession) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*keyAlias, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, struct [OH_Huks_Blob](_o_h___huks___blob.md) \*handle, struct [OH_Huks_Blob](_o_h___huks___blob.md) \*challenge) | Initializes the key session interface and obtains a handle (mandatory) and challenge value (optional).  | 
| [OH_Huks_UpdateSession](#oh_huks_updatesession) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*handle, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*inData, struct [OH_Huks_Blob](_o_h___huks___blob.md) \*outData) | Adds data by segment for the key operation, performs the related key operation, and outputs the processed data.  | 
| [OH_Huks_FinishSession](#oh_huks_finishsession) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*handle, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet, const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*inData, struct [OH_Huks_Blob](_o_h___huks___blob.md) \*outData) | Ends the key session.  | 
| [OH_Huks_AbortSession](#oh_huks_abortsession) (const struct [OH_Huks_Blob](_o_h___huks___blob.md) \*handle, const struct [OH_Huks_ParamSet](_o_h___huks___param_set.md) \*paramSet) | Aborts a key session.  | 


## Function Description


### OH_Huks_AbortSession()

  
```
struct OH_Huks_Result OH_Huks_AbortSession (const struct OH_Huks_Blob * handle, const struct OH_Huks_ParamSet * paramSet )
```
**Description**<br>
Aborts a key session.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| handle | Indicates the pointer to the key session handle, which is generated by [OH_Huks_InitSession](#oh_huks_initsession).  | 
| paramSet | Indicates the pointer to the parameters required for aborting the key session. By default, this parameter is a null pointer.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.

 **See**

[OH_Huks_InitSession](#oh_huks_initsession)

[OH_Huks_UpdateSession](#oh_huks_updatesession)

[OH_Huks_FinishSession](#oh_huks_finishsession)


### OH_Huks_AttestKeyItem()

  
```
struct OH_Huks_Result OH_Huks_AttestKeyItem (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSet, struct OH_Huks_CertChain * certChain )
```
**Description**<br>
Obtain the key certificate chain.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the target key.  | 
| paramSet | Indicates the pointer to the parameters required for obtaining the key certificate.  | 
| certChain | Indicates the pointer to the key certificate chain obtained.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_DeleteKeyItem()

  
```
struct OH_Huks_Result OH_Huks_DeleteKeyItem (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSet )
```
**Description**<br>
Deletes a key.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the key to delete. The alias must be the same as the alias for the key generated.  | 
| paramSet | Indicates the pointer to the parameters required for deleting the key. By default, this parameter is a null pointer.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_ExportPublicKeyItem()

  
```
struct OH_Huks_Result OH_Huks_ExportPublicKeyItem (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSet, struct OH_Huks_Blob * key )
```
**Description**<br>
Exports a public key.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the public key to export. The alias must be the same as the alias for the key generated.  | 
| paramSet | Indicates the pointer to the parameters required for exporting the public key.  | 
| key | Indicates the pointer to the public key exported.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_FinishSession()

  
```
struct OH_Huks_Result OH_Huks_FinishSession (const struct OH_Huks_Blob * handle, const struct OH_Huks_ParamSet * paramSet, const struct OH_Huks_Blob * inData, struct OH_Huks_Blob * outData )
```
**Description**<br>
Ends the key session.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| handle | Indicates the pointer to the key session handle, which is generated by [OH_Huks_InitSession](#oh_huks_initsession).  | 
| paramSet | Indicates the pointer to the parameters required for the key operation.  | 
| inData | Indicates the pointer to the data to be processed.  | 
| outData | Indicates the pointer to the output data.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.

 **See**

[OH_Huks_InitSession](#oh_huks_initsession)

[OH_Huks_UpdateSession](#oh_huks_updatesession)

[OH_Huks_AbortSession](#oh_huks_abortsession)


### OH_Huks_GenerateKeyItem()

  
```
struct OH_Huks_Result OH_Huks_GenerateKeyItem (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSetIn, struct OH_Huks_ParamSet * paramSetOut )
```
**Description**<br>
Generates a key.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the key to generate. The alias must be unique in the process of the service. Otherwise, the key will be overwritten.  | 
| paramSetIn | Indicates the pointer to the parameter set for generating the key.  | 
| paramSetOut | Indicates the pointer to a temporary key generated. If the generated key is not of a temporary type, this parameter is a null pointer.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_GetKeyItemParamSet()

  
```
struct OH_Huks_Result OH_Huks_GetKeyItemParamSet (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSetIn, struct OH_Huks_ParamSet * paramSetOut )
```
**Description**<br>
Obtains the attributes of a key.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the target key.  | 
| paramSetIn | Indicates the pointer to the attribute tag required for obtaining the attributes. By default, this parameter is a null pointer.  | 
| paramSetOut | Indicates the pointer to the attributes obtained.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_GetSdkVersion()

  
```
struct OH_Huks_Result OH_Huks_GetSdkVersion (struct OH_Huks_Blob * sdkVersion)
```
**Description**<br>
Obtains the current HUKS SDK version.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| sdkVersion | Indicates the pointer to the SDK version (in string format) obtained.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_ImportKeyItem()

  
```
struct OH_Huks_Result OH_Huks_ImportKeyItem (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSet, const struct OH_Huks_Blob * key )
```
**Description**<br>
Imports a key in plaintext.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the key to import. The alias must be unique in the process of the service. Otherwise, the key will be overwritten.  | 
| paramSet | Indicates the pointer to the parameters of the key to import.  | 
| key | Indicates the pointer to the key to import. The key must be in the format required by the HUKS. For details, see [HuksTypeApi](_huks_type_api.md).  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_ImportWrappedKeyItem()

  
```
struct OH_Huks_Result OH_Huks_ImportWrappedKeyItem (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_Blob * wrappingKeyAlias, const struct OH_Huks_ParamSet * paramSet, const struct OH_Huks_Blob * wrappedKeyData )
```
**Description**<br>
Imports a wrapped key.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the key to import. The alias must be unique in the process of the service. Otherwise, the key will be overwritten.  | 
| wrappingKeyAlias | Indicates the pointer to the alias of the wrapping key, which is obtained through key agreement and used to decrypt the key to import.  | 
| paramSet | Indicates the pointer to the parameters of the wrapped key to import.  | 
| wrappedKeyData | Indicates the pointer to the wrapped key to import. The key must be in the format required by the HUKS. For details, see [OH_Huks_AlgSuite](_huks_type_api.md#oh_huks_algsuite).  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.


### OH_Huks_InitSession()

  
```
struct OH_Huks_Result OH_Huks_InitSession (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSet, struct OH_Huks_Blob * handle, struct OH_Huks_Blob * challenge )
```
**Description**<br>
Initializes the key session interface and obtains a handle (mandatory) and challenge value (optional).

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the target key.  | 
| paramSet | Indicates the pointer to the parameters for the initialization operation.  | 
| handle | Indicates the pointer to the handle of the key session obtained. This handle is required for subsequent operations, including [OH_Huks_UpdateSession](#oh_huks_updatesession), [OH_Huks_FinishSession](#oh_huks_finishsession), and [OH_Huks_AbortSession](#oh_huks_abortsession).  | 
| challenge | Indicates the pointer to the challenge value obtained.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.

 **See**

[OH_Huks_UpdateSession](#oh_huks_updatesession)

[OH_Huks_FinishSession](#oh_huks_finishsession)

[OH_Huks_AbortSession](#oh_huks_abortsession)


### OH_Huks_IsKeyItemExist()

  
```
struct OH_Huks_Result OH_Huks_IsKeyItemExist (const struct OH_Huks_Blob * keyAlias, const struct OH_Huks_ParamSet * paramSet )
```
**Description**<br>
Checks whether a key exists.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| keyAlias | Indicates the pointer to the alias of the target key.  | 
| paramSet | Indicates the pointer to the attribute tag required for checking the key. By default, this parameter is a null pointer.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the key exists.

Returns [OH_Huks_ErrCode#OH_HUKS_ERR_CODE_ITEM_NOT_EXIST](_huks_type_api.md) if the key does not exist.

Returns any other error code for other cases.


### OH_Huks_UpdateSession()

  
```
struct OH_Huks_Result OH_Huks_UpdateSession (const struct OH_Huks_Blob * handle, const struct OH_Huks_ParamSet * paramSet, const struct OH_Huks_Blob * inData, struct OH_Huks_Blob * outData )
```
**Description**<br>
Adds data by segment for the key operation, performs the related key operation, and outputs the processed data.

 **Parameters**

| Name | Description | 
| -------- | -------- |
| handle | Indicates the pointer to the key session handle, which is generated by [OH_Huks_InitSession](#oh_huks_initsession).  | 
| paramSet | Indicates the pointer to the parameters required for the key operation.  | 
| inData | Indicates the pointer to the data to be processed. This API can be called multiples time to process large data by segment.  | 
| outData | Indicates the pointer to the output data.  | 

**Returns**

Returns [OH_Huks_ErrCode#OH_HUKS_SUCCESS](_huks_type_api.md) if the operation is successful; returns an error code otherwise.

 **See**

[OH_Huks_InitSession](#oh_huks_initsession)

[OH_Huks_FinishSession](#oh_huks_finishsession)

[OH_Huks_AbortSession](#oh_huks_abortsession)