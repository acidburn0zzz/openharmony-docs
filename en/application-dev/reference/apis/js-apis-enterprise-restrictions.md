# @ohos.enterprise.restrictions (Restrictions)

This **restrictions** module provides APIs for setting general restriction policies, including disabling or enabling device printing and HDC.

> **NOTE**
> 
> The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> The APIs provided by this module can be called only by a [device administrator application](enterpriseDeviceManagement-overview.md#basic-concepts) that is [enabled](js-apis-enterprise-adminManager.md#adminmanagerenableadmin).

## Modules to Import

```js
import restrictions from '@ohos.enterprise.restrictions'
```

## restrictions.setPrinterDisabled

setPrinterDisabled(admin: Want, disabled: boolean, callback: AsyncCallback\<void>): void

Enables or disables device printing through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| disabled  | boolean | Yes| Whether to disable device printing. The value **true** means to disable device printing; the value **false** means the opposite.|
| callback | AsyncCallback\<void> | Yes| Callback invoked to return the result.<br> If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.setPrinterDisabled(wantTemp, true, (err) => {
  if (err) {
    console.error(`Failed to set printer disabled. Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info('Succeeded in setting printer disabled');
})
```

## restrictions.setPrinterDisabled

setPrinterDisabled(admin: Want, disabled: boolean): Promise\<void>

Enables or disables device printing through the specified device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| disabled  | boolean | Yes| Whether to disable device printing. The value **true** means to disable device printing; the value **false** means the opposite.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | Promise that returns no value. An error object will be thrown if the specified device administrator application fails to disable or enable the device printing function.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.setPrinterDisabled(wantTemp, true).then(() => {
  console.info('Succeeded in setting printer disabled');
}).catch((err) => {
  console.error(`Failed to set printer disabled. Code is ${err.code}, message is ${err.message}`);
})
```

## restrictions.isPrinterDisabled

isPrinterDisabled(admin: Want, callback: AsyncCallback\<boolean>): void

Checks whether printing is disabled for devices through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| callback | AsyncCallback\<boolean> | Yes| Callback invoked to return the result. The value **true** means that device printing is disabled; the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.isPrinterDisabled(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to query is the printing function disabled or not. Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying is the printing function disabled : ${result}`);
})
```

## restrictions.isPrinterDisabled

isPrinterDisabled(admin: Want): Promise\<boolean>

Checks whether printing is disabled for devices through the specified device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<boolean> | Promise used to return the result. The value **true** means that device printing is disabled; the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.isPrinterDisabled(wantTemp).then((result) => {
  console.info(`Succeeded in querying is the printing function disabled : ${result}`);
}).catch((err) => {
  console.error(`Failed to query is the printing function disabled or not. Code is ${err.code}, message is ${err.message}`);
})
```

## restrictions.setHdcDisabled

setHdcDisabled(admin: Want, disabled: boolean, callback: AsyncCallback\<void>): void

Enables or disables HDC through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| disabled  | boolean | Yes| Whether to disable HDC. The value **true** means to disable HDC; the value **false** means the opposite.|
| callback | AsyncCallback\<void> | Yes| Callback invoked to return the result.<br> If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.setHdcDisabled(wantTemp, true, (err) => {
  if (err) {
    console.error(`Failed to set hdc disabled. Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info('Succeeded in setting hdc disabled');
})
```

## restrictions.setHdcDisabled

setHdcDisabled(admin: Want, disabled: boolean): Promise\<void>

Enables or disables HDC through the specified device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| disabled  | boolean | Yes| Whether to disable HDC. The value **true** means to disable HDC; the value **false** means the opposite.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | Promise that returns no value. An error object will be thrown if the specified device administrator application fails to disable or enable HDC.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.setHdcDisabled(wantTemp, true).then(() => {
  console.info('Succeeded in setting hdc disabled');
}).catch((err) => {
  console.error(`Failed to set hdc disabled. Code is ${err.code}, message is ${err.message}`);
})
```

## restrictions.isHdcDisabled

isHdcDisabled(admin: Want, callback: AsyncCallback\<boolean>): void

Checks whether HDC is disabled through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| callback | AsyncCallback\<boolean> | Yes| Callback invoked to return the result. The value **true** means HDC is disabled; the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                       |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.isHdcDisabled(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to query is hdc disabled or not. Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying is hdc disabled : ${result}`);
})
```

## restrictions.isHdcDisabled

isHdcDisabled(admin: Want): Promise\<boolean>

Checks whether HDC is disabled through the specified device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESTRICT_POLICY

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<boolean> | Promise used to return the result. The value **true** means HDC is disabled; the value **false** means the opposite.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                                     |
| ------- | ---------------------------------------------------------------------------- |
| 9200001 | the application is not an administrator of the device.                        |
| 9200002 | the administrator application does not have permission to manage the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

restrictions.isHdcDisabled(wantTemp).then((result) => {
  console.info(`Succeeded in querying is hdc disabled : ${result}`);
}).catch((err) => {
  console.error(`Failed to query is hdc disabled or not. Code is ${err.code}, message is ${err.message}`);
})
```
