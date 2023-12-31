# @ohos.enterprise.adminManager (Enterprise Device Management)

The **adminManager** module provides enterprise device management capabilities so that devices have the custom capabilities required in enterprise settings.

> **NOTE**
>
> - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>
> - The APIs provided by this module can be called only by a [device administrator application](enterpriseDeviceManagement-overview.md#basic-concepts).

## Modules to Import

```js
import adminManager from '@ohos.enterprise.adminManager';
```

## adminManager.enableAdmin

enableAdmin(admin: Want, enterpriseInfo: EnterpriseInfo, type: AdminType, callback: AsyncCallback\<void>): void

Enables a device administrator application of the current user. This API uses an asynchronous callback to return the result. The super administrator application can be enabled only by the administrator.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name           | Type                                 | Mandatory  | Description                |
| -------------- | ----------------------------------- | ---- | ------------------ |
| admin          | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.           |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | Yes   | Enterprise information of the device administrator application.     |
| type           | [AdminType](#admintype)             | Yes   | Type of the device administrator to enable.        |
| callback       | AsyncCallback\<void>                | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                        |
| ------- | --------------------------------------------------------------- |
| 9200003 | the administrator ability component is invalid.                 |
| 9200004 | failed to enable the administrator application of the device.   |
| 9200007 | the system ability work abnormally.                             |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.enableAdmin(wantTemp, enterpriseInfo, adminManager.AdminType.ADMIN_TYPE_SUPER, (err) => {
  if (err) {
    console.error(`Failed to enable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in enabling admin');
});
```

## adminManager.enableAdmin

enableAdmin(admin: Want, enterpriseInfo: EnterpriseInfo, type: AdminType, userId: number, callback: AsyncCallback\<void>): void

Enables a device administrator application of the user specified by **userId**. This API uses an asynchronous callback to return the result. The super administrator application can be enabled only by the administrator.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name           | Type                                 | Mandatory  | Description                          |
| -------------- | ----------------------------------- | ---- | ---------------------------- |
| admin          | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.                     |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | Yes   | Enterprise information of the device administrator application.                |
| type           | [AdminType](#admintype)             | Yes   | Type of the device administrator to enable.                  |
| userId         | number                              | Yes   | User ID. The default value is the user ID of the caller. The user ID must be greater than or equal to **0**.|
| callback       | AsyncCallback\<void>                | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.      |

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                        |
| ------- | --------------------------------------------------------------- |
| 9200003 | the administrator ability component is invalid.                 |
| 9200004 | failed to enable the administrator application of the device.   |
| 9200007 | the system ability work abnormally.                             |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.enableAdmin(wantTemp, enterpriseInfo, adminManager.AdminType.ADMIN_TYPE_NORMAL, 100, (err) => {
  if (err) {
    console.error(`Failed to enable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in enabling admin');
});
```

## adminManager.enableAdmin

enableAdmin(admin: Want, enterpriseInfo: EnterpriseInfo, type: AdminType, userId?: number): Promise\<void>

Enables a device administrator application of the specified user (if **userId** is passed in) or the current user (if **userId** is not passed in). This API uses a promise to return the result. The super administrator application can be enabled only by the administrator.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name           | Type                                 | Mandatory  | Description                          |
| -------------- | ----------------------------------- | ---- | ---------------------------- |
| admin          | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.                     |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | Yes   | Enterprise information of the device administrator application.                |
| type           | [AdminType](#admintype)             | Yes   | Type of the device administrator to enable.                  |
| userId         | number                              | No   | User ID. The default value is the user ID of the caller. The user ID must be greater than or equal to **0**.|

**Return value**

| Type               | Description               |
| ----------------- | ----------------- |
| Promise\<void>    | Promise that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                        |
| ------- | --------------------------------------------------------------- |
| 9200003 | the administrator ability component is invalid.                 |
| 9200004 | failed to enable the administrator application of the device.   |
| 9200007 | the system ability work abnormally.                             |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.enableAdmin(wantTemp, enterpriseInfo, adminManager.AdminType.ADMIN_TYPE_NORMAL, 100).catch((err) => {
  console.error(`Failed to enable admin. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.disableAdmin

disableAdmin(admin: Want, callback: AsyncCallback\<void>): void

Disables a device administrator application of the current user. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name     | Type                                 | Mandatory  | Description                 |
| -------- | ----------------------------------- | ---- | ------------------- |
| admin    | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.          |
| callback | AsyncCallback\<void>                | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                          |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.disableAdmin(wantTemp, (err) => {
  if (err) {
    console.error(`Failed to disable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disabling admin');
});
```

## adminManager.disableAdmin

disableAdmin(admin: Want, userId: number, callback: AsyncCallback\<void>): void

Disables a device administrator application of the user specified by **userId**. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name     | Type                                 | Mandatory  | Description                          |
| -------- | ----------------------------------- | ---- | ---------------------------- |
| admin    | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.                   |
| userId   | number                              | Yes   | User ID. The default value is the user ID of the caller. The user ID must be greater than or equal to **0**.|
| callback | AsyncCallback\<void>                | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.       |

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                          |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.disableAdmin(wantTemp, 100, (err) => {
  if (err) {
    console.error(`Failed to disable admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disabling admin');
});
```

## adminManager.disableAdmin

disableAdmin(admin: Want, userId?: number): Promise\<void>

Disables a device administrator application of the specified user (if **userId** is passed in) or the current user (if **userId** is not passed in). This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name   | Type                                 | Mandatory  | Description                          |
| ------ | ----------------------------------- | ---- | ---------------------------- |
| admin  | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.                   |
| userId | number                              | No   | User ID. The default value is the user ID of the caller. The user ID must be greater than or equal to **0**.|

**Return value**

| Type               | Description               |
| ----------------- | ----------------- |
| Promise\<void>    | Promise that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                          |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.disableAdmin(wantTemp, 100).catch((err) => {
  console.error(`Failed to disable admin. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.disableSuperAdmin

disableSuperAdmin(bundleName: String, callback: AsyncCallback\<void>): void

Disables a super device administrator application based on the specified bundle name. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name       | Type                     | Mandatory  | Description                 |
| ---------- | ----------------------- | ---- | ------------------- |
| bundleName | String                  | Yes   | Bundle name of the super device administrator application.       |
| callback   | AsyncCallback\<void>    | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                          |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**Example**

```js
let bundleName = 'com.example.myapplication';

adminManager.disableSuperAdmin(bundleName, (err) => {
  if (err) {
    console.error(`Failed to disable super admin. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in disabling super admin');
});
```

## adminManager.disableSuperAdmin

disableSuperAdmin(bundleName: String): Promise\<void>

Disables a super device administrator application based on the specified bundle name. This API uses a promise to return the result.

**Required permissions**: ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name       | Type    | Mandatory  | Description          |
| ---------- | ------ | ---- | ------------ |
| bundleName | String | Yes   | Bundle name of the super device administrator application.|

**Return value**

| Type               | Description               |
| ----------------- | ----------------- |
| Promise\<void>    | Promise that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                                          |
| ------- | ----------------------------------------------------------------- |
| 9200005 | failed to disable the administrator application of the device.    |

**Example**

```js
let bundleName = 'com.example.myapplication';

adminManager.disableSuperAdmin(bundleName).catch((err) => {
  console.error(`Failed to disable super admin. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.isAdminEnabled

isAdminEnabled(admin: Want, callback: AsyncCallback\<boolean>): void

Checks whether a device administrator application of the current user is enabled. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name     | Type                                 | Mandatory  | Description                  |
| -------- | ----------------------------------- | ---- | -------------------- |
| admin    | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.            |
| callback | AsyncCallback\<boolean>             | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null** and **data** is a Boolean value (**true** means that the device administrator application is enabled; and **false** means the opposite). If the operation fails, **err** is an error object.|

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.isAdminEnabled(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to query admin is enabled or not. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying admin is enabled or not, result : ${result}`);
});
```

## adminManager.isAdminEnabled

isAdminEnabled(admin: Want, userId: number, callback: AsyncCallback\<boolean>): void

Checks whether a device administrator application of the user specified by **userId** is enabled. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name     | Type                                 | Mandatory  | Description                          |
| -------- | ----------------------------------- | ---- | ---------------------------- |
| admin    | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.                     |
| userId   | number                              | Yes   | User ID. The default value is the user ID of the caller. The user ID must be greater than or equal to **0**.|
| callback | AsyncCallback\<boolean>             | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null** and **data** is a Boolean value (**true** means that the device administrator application is enabled; and **false** means the opposite). If the operation fails, **err** is an error object.     |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.isAdminEnabled(wantTemp, 100, (err, result) => {
  if (err) {
    console.error(`Failed to query admin is enabled. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying admin is enabled or not, result : ${result}`);
});
```

## adminManager.isAdminEnabled

isAdminEnabled(admin: Want, userId?: number): Promise\<boolean>

Checks whether a device administrator application of the specified user (if **userId** is passed in) or the current user (if **userId** is not passed in) is enabled. This API uses a promise to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name   | Type                                 | Mandatory  | Description                          |
| ------ | ----------------------------------- | ---- | ---------------------------- |
| admin  | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.                     |
| userId | number                              | No   | User ID. The default value is the user ID of the caller. The user ID must be greater than or equal to **0**.|

**Return value**

| Type              | Description               |
| ----------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result. If **true** is returned, the device administrator application is enabled. If **false** is returned, the device administrator application is not enabled.|

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};

adminManager.isAdminEnabled(wantTemp, 100).then((result) => {
  console.info(`Succeeded in querying admin is enabled or not, result : ${result}`);
}).catch((err) => {
  console.error(`Failed to query admin is enabled or not. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.isSuperAdmin

isSuperAdmin(bundleName: String, callback: AsyncCallback\<boolean>): void

Checks whether a super device administrator application is enabled based on the specified bundle name. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name       | Type                     | Mandatory  | Description                  |
| ---------- | ----------------------- | ---- | -------------------- |
| bundleName | String                  | Yes   | Device administrator application.             |
| callback   | AsyncCallback\<boolean> | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null** and **data** is a Boolean value (**true** means that the super device administrator application is enabled; and **false** means the opposite). If the operation fails, **err** is an error object.|

**Example**

```js
let bundleName = 'com.example.myapplication';

adminManager.isSuperAdmin(bundleName, (err, result) => {
  if (err) {
    console.error(`Failed to query admin is super admin or not. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in querying admin is super admin or not, result : ${result}`);
});
```

## adminManager.isSuperAdmin

isSuperAdmin(bundleName: String): Promise\<boolean>

Checks whether a super device administrator application is enabled based on the specified bundle name. This API uses a promise to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name       | Type    | Mandatory  | Description       |
| ---------- | ------ | ---- | --------- |
| bundleName | String | Yes   | Super device administrator application.|

**Return value**

| ID          | Error Message              |
| ----------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result. If **true** is returned, the super device administrator application is enabled. If **false** is returned, the super device administrator application is not enabled.|

**Example**

```js
let bundleName = 'com.example.myapplication';

adminManager.isSuperAdmin(bundleName).then((result) => {
  console.info(`Succeeded in querying admin is super admin or not, result : ${result}`);
}).catch((err) => {
  console.error(`Failed to query admin is super admin or not. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.setEnterpriseInfo

setEnterpriseInfo(admin: Want, enterpriseInfo: EnterpriseInfo, callback: AsyncCallback\<void>;): void

Sets the enterprise information of a device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.SET_ENTERPRISE_INFO

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name           | Type                                 | Mandatory  | Description                    |
| -------------- | ----------------------------------- | ---- | ---------------------- |
| admin          | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.               |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | Yes   | Enterprise information of the device administrator application.          |
| callback       | AsyncCallback\<void>;               | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.setEnterpriseInfo(wantTemp, enterpriseInfo, (err) => {
  if (err) {
    console.error(`Failed to set enterprise info. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in setting enterprise info');
});
```

## adminManager.setEnterpriseInfo

setEnterpriseInfo(admin: Want, enterpriseInfo: EnterpriseInfo): Promise\<void>;

Sets the enterprise information of a device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.SET_ENTERPRISE_INFO

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name           | Type                                 | Mandatory  | Description          |
| -------------- | ----------------------------------- | ---- | ------------ |
| admin          | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.     |
| enterpriseInfo | [EnterpriseInfo](#enterpriseinfo)   | Yes   | Enterprise information of the device administrator application.|

**Return value**

| Type               | Description                   |
| ----------------- | --------------------- |
| Promise\<void>    | Promise that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};
let enterpriseInfo = {
  name: 'enterprise name',
  description: 'enterprise description'
}

adminManager.setEnterpriseInfo(wantTemp, enterpriseInfo).catch((err) => {
  console.error(`Failed to set enterprise info. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.getEnterpriseInfo

getEnterpriseInfo(admin: Want, callback: AsyncCallback&lt;EnterpriseInfo&gt;): void

Obtains the enterprise information of a device administrator application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name     | Type                                      | Mandatory  | Description                      |
| -------- | ---------------------------------------- | ---- | ------------------------ |
| admin    | [Want](js-apis-app-ability-want.md)      | Yes   | Device administrator application.                 |
| callback | AsyncCallback&lt;[EnterpriseInfo](#enterpriseinfo)&gt; | Yes   | Callback invoked to return the result. If the operation is successful, **err** is **null** and **data** is the enterprise information of the device administrator application obtained. If the operation fails, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

adminManager.getEnterpriseInfo(wantTemp, (err, result) => {
  if (err) {
    console.error(`Failed to get enterprise info. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info(`Succeeded in getting enterprise info, enterprise name : ${result.name}, enterprise description : ${result.description}`);
});
```

## adminManager.getEnterpriseInfo

getEnterpriseInfo(admin: Want): Promise&lt;EnterpriseInfo&gt;

Obtains the enterprise information of a device administrator application. This API uses a promise to return the result.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|

**Return value**

| Type                                      | Description                       |
| ---------------------------------------- | ------------------------- |
| Promise&lt;[EnterpriseInfo](#enterpriseinfo)&gt; | Promise used to return the enterprise information of the specified device administrator application obtained.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |

**Example**

```js
let wantTemp = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility',
};

adminManager.getEnterpriseInfo(wantTemp).then((result) => {
  console.info(`Succeeded in getting enterprise info, enterprise name : ${result.name}, enterprise description : ${result.description}`);
}).catch((err) => {
  console.error(`Failed to get enterprise info. Code: ${err.code}, message: ${err.message}`);
});
```

## adminManager.subscribeManagedEvent

subscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>, callback: AsyncCallback\<void>): void

Subscribes to system management events through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | Yes| Array of events to subscribe to.|
| callback | AsyncCallback\<void> | Yes| Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

|ID| Error Message                                               |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events = [0, 1];

adminManager.subscribeManagedEvent(wantTemp, events, (err) => {
  if (err) {
    console.error(`Failed to subscribe managed event. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in subscribe managed event');
});
```

## adminManager.subscribeManagedEvent

subscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>): Promise\<void>

Subscribes to system management events through the specified device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | Yes| Array of events to subscribe to.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | Promise that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events = [0, 1];

adminManager.subscribeManagedEvent(wantTemp, events).then(() => {
}).catch((err) => {
  console.error(`Failed to subscribe managed event. Code: ${err.code}, message: ${err.message}`);
})
```

## adminManager.unsubscribeManagedEvent

unsubscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>, callback: AsyncCallback\<void>): void

Unsubscribes from system management events through the specified device administrator application. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | Yes| Array of events to unsubscribe from.|
| callback | AsyncCallback\<void> | Yes| Callback invoked to return the result. If the operation is successful, **err** is **null**. Otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events = [0, 1];

adminManager.unsubscribeManagedEvent(wantTemp, events, (err) => {
  if (err) {
    console.error(`Failed to unsubscribe managed event. Code: ${err.code}, message: ${err.message}`);
    return;
  }
  console.info('Succeeded in unsubscribe managed event');
});
```

## adminManager.unsubscribeManagedEvent

unsubscribeManagedEvent(admin: Want, managedEvents: Array\<ManagedEvent>): Promise\<void>

Unsubscribes from system management events through the specified device administrator application. This API uses a promise to return the result.

**Required permissions**: ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

**Parameters**

| Name  | Type                                 | Mandatory  | Description     |
| ----- | ----------------------------------- | ---- | ------- |
| admin | [Want](js-apis-app-ability-want.md) | Yes   | Device administrator application.|
| managedEvents  | Array\<[ManagedEvent](#managedevent)> | Yes| Array of events to unsubscribe from.|

**Return value**

| Type  | Description                                 |
| ----- | ----------------------------------- |
| Promise\<void> | Promise that returns no value. If the operation fails, an error object is thrown.|

**Error codes**

For details about the error codes, see [Enterprise Device Management Error Codes](../errorcodes/errorcode-enterpriseDeviceManager.md).

| ID| Error Message                                              |
| ------- | ----------------------------------------------------- |
| 9200001 | the application is not an administrator of the device. |
| 9200008 | the specified system events enum is invalid.          |

**Example**

```js
let wantTemp = {
  bundleName: 'bundleName',
  abilityName: 'abilityName',
};
let events = [0, 1];

adminManager.unsubscribeManagedEvent(wantTemp, events).then(() => {
}).catch((err) => {
  console.error(`Failed to unsubscribe managed event. Code: ${err.code}, message: ${err.message}`);
})
```

## EnterpriseInfo

Defines the enterprise information of a device administrator application.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

| Name        | Type    | Mandatory| Description                           |
| ----------- | --------| ---- | ------------------------------- |
| name        | string   | Yes  | Name of the enterprise to which the device administrator application belongs.|
| description | string   | Yes  | Description of the enterprise to which the device administrator application belongs.|

## AdminType

Enumerates the administrator types of the device administrator application.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

| Name               | Value | Description   |
| ----------------- | ---- | ----- |
| ADMIN_TYPE_NORMAL | 0x00 | Common administrator.|
| ADMIN_TYPE_SUPER  | 0x01 | Super administrator.|

## ManagedEvent

Enumerates the system management events that can be subscribed to.

**System capability**: SystemCapability.Customization.EnterpriseDeviceManager

**System API**: This is a system API.

| Name                       | Value | Description          |
| -------------------------- | ---- | ------------- |
| MANAGED_EVENT_BUNDLE_ADDED | 0    | Application installed.|
| MANAGED_EVENT_BUNDLE_REMOVED | 1  | Application uninstalled.|
| MANAGED_EVENT_APP_START<sup>10+</sup> | 2    | Application started.|
| MANAGED_EVENT_APP_STOP<sup>10+</sup> | 3  | Application stopped.|
