# @ohos.enterprise.deviceControl (Device Control)

The **deviceControl** module provides APIs for device control, which can be called only by device administrator applications.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 10. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
>
> - The APIs provided by this module can be called only by a [device administrator application](enterpriseDeviceManagement-overview.md#basic-concepts) that is [enabled](js-apis-enterprise-adminManager.md#adminmanagerenableadmin).

## Modules to Import

```js
import deviceControl from '@ohos.enterprise.deviceControl'
```

## deviceControl.resetFactory

resetFactory(admin: Want, callback: AsyncCallback\<void>): void

Restores factory settings through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESET_DEVICE

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application used to restore the factory settings.|
| callback | AsyncCallback\<void> | Yes| Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

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

deviceControl.resetFactory(wantTemp, (err) => {
  if (err) {
    console.error(`Failed to reset factory. Code is ${err.code}, message is ${err.message}`);
    return;
  }
  console.log('Succeeded in resetting factory');
})
```

## deviceControl.resetFactory

resetFactory(admin: Want): Promise\<void>

Restores factory settings. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_RESET_DEVICE

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application used to restore the factory settings.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | Promise that returns no value. If the operation fails, an error object will be thrown.|

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

deviceControl.resetFactory(wantTemp).then(() => {
}).catch((err) => {
  console.error(`Failed to reset factory. Code is ${err.code}, message is ${err.message}`);
})
```
