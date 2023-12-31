# ServiceExtensionContext

The **ServiceExtensionContext** module, inherited from **ExtensionContext**, provides context for ServiceExtensionAbilities.

You can use the APIs of this module to start, terminate, connect, and disconnect abilities.

> **NOTE**
> 
>  - The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.
>  - The APIs of this module can be used only in the stage model.

## Modules to Import

```ts
import common from '@ohos.app.ability.common';
```

## Usage

Before using the **ServiceExtensionContext** module, you must define a child class that inherits from **ServiceExtensionAbility**.

```ts
  import ServiceExtensionAbility from '@ohos.app.ability.ServiceExtensionAbility';

  let context;
  let commRemote; // Release the instance when the connection is disconnected.
  class EntryAbility extends ServiceExtensionAbility {
    onCreate() {
      context = this.context; // Obtain a ServiceExtensionContext instance.
    }
  }
```

## ServiceExtensionContext.startAbility

startAbility(want: Want, callback: AsyncCallback&lt;void&gt;): void;

Starts an ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };

  try {
    this.context.startAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbility failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startAbility

startAbility(want: Want, options?: StartOptions): Promise\<void>;

Starts an ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | No| Parameters used for starting the ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };
  let options = {
  	windowMode: 0,
  };

  try {
    this.context.startAbility(want, options)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startAbility failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startAbility

startAbility(want: Want, options: StartOptions, callback: AsyncCallback&lt;void&gt;): void

Starts an ability with the start options specified. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability.|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | Yes| Parameters used for starting the ability.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbility(want, options, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbility failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Starts an ability with the account ID specified. This API uses an asynchronous callback to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.startAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbilityWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options: StartOptions, callback: AsyncCallback\<void\>): void;

Starts an ability with the account ID and start options specified. This API uses an asynchronous callback to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | Yes| Parameters used for starting the ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startAbilityWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('startAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```


## ServiceExtensionContext.startAbilityWithAccount

startAbilityWithAccount(want: Want, accountId: number, options?: StartOptions): Promise\<void>;

Starts an ability with the account ID specified. This API uses a promise to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | No| Parameters used for starting the ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden.        |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;
  let options = {
    windowMode: 0
  };

  try {
    this.context.startAbilityWithAccount(want, accountId, options)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startAbilityWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

Starts a new ServiceExtensionAbility. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.startServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startServiceExtensionAbility failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('startServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbility

startServiceExtensionAbility(want: Want): Promise\<void>;

Starts a new ServiceExtensionAbility. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.startServiceExtensionAbility(want)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startServiceExtensionAbility failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Starts a new ServiceExtensionAbility with the account ID specified. This API uses an asynchronous callback to return the result.

> **NOTE**
> 
> The **ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS** permission is not required when **accountId** specifies the current user.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).


**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('startServiceExtensionAbilityWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('startServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startServiceExtensionAbilityWithAccount

startServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

Starts a new ServiceExtensionAbility with the account ID specified. This API uses a promise to return the result.

> **NOTE**
> 
> The **ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS** permission is not required when **accountId** specifies the current user.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist.        |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.startServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // Carry out normal service processing.
        console.log('startServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('startServiceExtensionAbilityWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want, callback: AsyncCallback\<void>): void;

Stops a ServiceExtensionAbility in the same application. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.stopServiceExtensionAbility(want, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('stopServiceExtensionAbility failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('stopServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbility

stopServiceExtensionAbility(want: Want): Promise\<void>;

Stops a ServiceExtensionAbility in the same application. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };

  try {
    this.context.stopServiceExtensionAbility(want)
      .then((data) => {
        // Carry out normal service processing.
        console.log('stopServiceExtensionAbility succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('stopServiceExtensionAbility failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number, callback: AsyncCallback\<void>): void;

Stops a ServiceExtensionAbility in the same application with the account ID specified. This API uses an asynchronous callback to return the result.

> **NOTE**
> 
> The **ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS** permission is not required when **accountId** specifies the current user.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| callback | AsyncCallback\<void\> | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId, (error) => {
      if (error.code) {
        // Process service logic errors.
        console.error('stopServiceExtensionAbilityWithAccount failed, error.code: ${error.code, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('stopServiceExtensionAbilityWithAccount succeed');
    });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.stopServiceExtensionAbilityWithAccount

stopServiceExtensionAbilityWithAccount(want: Want, accountId: number): Promise\<void>;

Stops a ServiceExtensionAbility in the same application with the account ID specified. This API uses a promise to return the result.

> **NOTE**
> 
> The **ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS** permission is not required when **accountId** specifies the current user.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |
| 16200001 | The caller has been released. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;

  try {
    this.context.stopServiceExtensionAbilityWithAccount(want, accountId)
      .then((data) => {
        // Carry out normal service processing.
        console.log('stopServiceExtensionAbilityWithAccount succeed');
      })
      .catch((error) => {
        // Process service logic errors.
        console.error('stopServiceExtensionAbilityWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.terminateSelf

terminateSelf(callback: AsyncCallback&lt;void&gt;): void;

Terminates this ability. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  this.context.terminateSelf((error) => {
    if (error.code) {
      // Process service logic errors.
      console.error('terminateSelf failed, error.code: ${error.code}, error.message: ${error.message}');
      return;
    }
    // Carry out normal service processing.
    console.log('terminateSelf succeed');
  });
  ```

## ServiceExtensionContext.terminateSelf

terminateSelf(): Promise&lt;void&gt;;

Terminates this ability. This API uses a promise to return the result.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  this.context.terminateSelf().then((data) => {
    // Carry out normal service processing.
    console.log('terminateSelf succeed');
  }).catch((error) => {
    // Process service logic errors.
    console.error('terminateSelf failed, error.code: ${error.code}, error.message: ${error.message}');
  });
  ```

## ServiceExtensionContext.connectServiceExtensionAbility

connectServiceExtensionAbility(want: Want, options: ConnectOptions): number;

Connects this ability to a ServiceExtensionAbility.

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md)  | Yes| Want information about the target ability, such as the ability name and bundle name.|
| options | [ConnectOptions](js-apis-inner-ability-connectOptions.md) | Yes| Callback used to return the information indicating that the connection is successful, interrupted, or failed.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | A number, based on which the connection will be interrupted.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    bundleName: 'com.example.myapp',
    abilityName: 'MyAbility'
  };
  let options = {
    onConnect(elementName, remote) { 
      commRemote = remote;
      console.log('----------- onConnect -----------'); 
    },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------') },
    onFailed(code) { console.error('----------- onFailed -----------') }
  };

  let connection = null;
  try {
    connection = this.context.connectServiceExtensionAbility(want, options);
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.connectServiceExtensionAbilityWithAccount

connectServiceExtensionAbilityWithAccount(want: Want, accountId: number, options: ConnectOptions): number;

Uses the **AbilityInfo.AbilityType.SERVICE** template and account ID to connect this ability to another ability.

**Required permissions**: ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| accountId | number | Yes| ID of a system account. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|
| options | ConnectOptions | Yes| Remote object instance.|

**Return value**

| Type| Description|
| -------- | -------- |
| number | Result code of the ability connection.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  let want = {
    deviceId: '',
    bundleName: 'com.example.myapplication',
    abilityName: 'EntryAbility'
  };
  let accountId = 100;
  let options = {
    onConnect(elementName, remote) { 
      commRemote = remote;
      console.log('----------- onConnect -----------');
    },
    onDisconnect(elementName) { console.log('----------- onDisconnect -----------'); },
    onFailed(code) { console.log('----------- onFailed -----------'); }
  };

  let connection = null;
  try {
    connection = this.context.connectServiceExtensionAbilityWithAccount(want, accountId, options);
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number, callback:AsyncCallback&lt;void&gt;): void;

Disconnects this ability from a ServiceExtensionAbility and after the successful disconnection, sets the remote object returned upon the connection to void. This API uses an asynchronous callback to return the result. 

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| connection | number | Yes| Number returned after **connectServiceExtensionAbility** is called.|
| callback | AsyncCallback&lt;void&gt; | Yes| Callback used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  // connection is the return value of connectServiceExtensionAbility.
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection, (error) => {
      commRemote = null;
      if (error.code) {
        // Process service logic errors.
        console.error('disconnectServiceExtensionAbility failed, error.code: ${error.code}, error.message: ${error.message}');
        return;
      }
      // Carry out normal service processing.
      console.log('disconnectServiceExtensionAbility succeed');
    });
  } catch (paramError) {
    commRemote = null;
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.disconnectServiceExtensionAbility

disconnectServiceExtensionAbility(connection: number): Promise&lt;void&gt;;

Disconnects this ability from a ServiceExtensionAbility and after the successful disconnection, sets the remote object returned upon the connection to void. This API uses a promise to return the result. 

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| connection | number | Yes| Number returned after **connectServiceExtensionAbility** is called.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000011 | The context does not exist.        |
| 16000050 | Internal error. |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  ```ts
  // connection is the return value of connectServiceExtensionAbility.
  let connection = 1;

  try {
    this.context.disconnectServiceExtensionAbility(connection)
      .then((data) => {
        commRemote = null;
        // Carry out normal service processing.
        console.log('disconnectServiceExtensionAbility succeed');
      })
      .catch((error) => {
        commRemote = null;
        // Process service logic errors.
        console.error('disconnectServiceExtensionAbility failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    commRemote = null;
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

## ServiceExtensionContext.startAbilityByCall

startAbilityByCall(want: Want): Promise&lt;Caller&gt;;

Starts an ability in the foreground or background and obtains the caller object for communicating with the ability.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - The rules for using this API in the same-device and cross-device scenarios are different. For details, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Information about the ability to start, including **abilityName**, **moduleName**, **bundleName**, **deviceId** (optional), and **parameters** (optional). If **deviceId** is left blank or null, the local ability is started. If **parameters** is left blank or null, the ability is started in the background.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Caller&gt; | Promise used to return the caller object to communicate with.|

**Error codes**

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16200001 | The caller has been released.        |

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

**Example**

  Start an ability in the background.

  ```ts
  let caller;

  // Start an ability in the background by not passing parameters.
  let wantBackground = {
      bundleName: 'com.example.myservice',
      moduleName: 'entry',
      abilityName: 'EntryAbility',
      deviceId: ''
  };

  try {
    this.context.startAbilityByCall(wantBackground)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.error('startAbilityByCall failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```

  Start an ability in the foreground.

  ```ts
  let caller;

  // Start an ability in the foreground with 'ohos.aafwk.param.callAbilityToForeground' in parameters set to true.
  let wantForeground = {
      bundleName: 'com.example.myservice',
      moduleName: 'entry',
      abilityName: 'EntryAbility',
      deviceId: '',
      parameters: {
        'ohos.aafwk.param.callAbilityToForeground': true
      }
  };

  try {
    this.context.startAbilityByCall(wantForeground)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCall succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.error('startAbilityByCall failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```
## ServiceExtensionContext.startRecentAbility

startRecentAbility(want: Want, callback: AsyncCallback\<void>): void;

Starts an ability. If the ability has multiple instances, the latest instance is started. This API uses an asynchronous callback to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**Example**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};

try {
  this.context.startRecentAbility(want, (err) => {
    if (err.code) {
      // Process service logic errors.
      console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // Carry out normal service processing.
    console.info('startRecentAbility succeed');
  });
} catch (err) {
  // Process input parameter errors.
  console.error(`startRecentAbility failed failed, code is ${err.code}, message is ${err.message}`);
}
  ```
## ServiceExtensionContext.startRecentAbility

startRecentAbility(want: Want, options: StartOptions, callback: AsyncCallback\<void>): void;

Starts an ability with the start options specified. If the ability has multiple instances, the latest instance is started. This API uses an asynchronous callback to return the result.
You can use this API to carry start options.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | Yes| Parameters used for starting the ability.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**Example**

  ```ts
let want = {
  deviceId: '',
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0
};

try {
  this.context.startRecentAbility(want, options, (err) => {
    if (err.code) {
      // Process service logic errors.
      console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
      return;
    }
    // Carry out normal service processing.
    console.info('startRecentAbility succeed');
  });
} catch (err) {
  // Process input parameter errors.
  console.error(`startRecentAbility failed failed, code is ${err.code}, message is ${err.message}`);
}
  ```
## ServiceExtensionContext.startRecentAbility

startRecentAbility(want: Want, options?: StartOptions): Promise\<void>;

Starts an ability. If the ability has multiple instances, the latest instance is started.
This API uses a promise to return the result.

Observe the following when using this API:
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - For details about the startup rules for the components in the stage model, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Want information about the target ability.|
| options | [StartOptions](js-apis-app-ability-startOptions.md) | No| Parameters used for starting the ability.|

**Error codes**

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000009 | An ability cannot be started or stopped in Wukong mode. |
| 16000010 | The call with the continuation flag is forbidden. |
| 16000011 | The context does not exist. |
| 16000050 | Internal error. |
| 16000053 | The ability is not on the top of the UI. |
| 16000055 | Installation-free timed out. |
| 16200001 | The caller has been released. |

**Example**

  ```ts
let want = {
  bundleName: 'com.example.myapplication',
  abilityName: 'EntryAbility'
};
let options = {
  windowMode: 0,
};

try {
  this.context.startRecentAbility(want, options)
    .then(() => {
      // Carry out normal service processing.
      console.info('startRecentAbility succeed');
    })
    .catch((err) => {
      // Process service logic errors.
      console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
    });
} catch (err) {
  // Process input parameter errors.
  console.error(`startRecentAbility failed, code is ${err.code}, message is ${err.message}`);
}
  ```

## ServiceExtensionContext.startAbilityByCallWithAccount<sup>10+</sup>

startAbilityByCallWithAccount(want: Want, accountId: number): Promise&lt;Caller&gt;;

Starts an ability with the account ID specified and obtains the caller object for communicating with the ability.

Observe the following when using this API:
 - If an application needs to call this API to start an ability that belongs to another user, it must have the **ohos.permission.ABILITY_BACKGROUND_COMMUNICATION** and **ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS** permissions.
 - If an application running in the background needs to call this API to start an ability, it must have the **ohos.permission.START_ABILITIES_FROM_BACKGROUND** permission.
 - If **exported** of the target ability is **false** in cross-application scenarios, the caller must have the **ohos.permission.START_INVISIBLE_ABILITY** permission.
 - The rules for using this API in the same-device and cross-device scenarios are different. For details, see [Component Startup Rules (Stage Model)](../../application-models/component-startup-rules.md).

**Required permissions**: ohos.permission.NOTIFICATION_CONTROLLER and ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

**System capability**: SystemCapability.Ability.AbilityRuntime.Core

**System API**: This is a system API and cannot be called by third-party applications.

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| want | [Want](js-apis-application-want.md) | Yes| Information about the ability to start, including **abilityName**, **moduleName**, **bundleName**, **deviceId** (optional), and **parameters** (optional). If **deviceId** is left blank or null, the local ability is started. If **parameters** is left blank or null, the ability is started in the background.|
| accountId | number | Yes| ID of a system account. The value **-1** indicates the current user. For details, see [getCreatedOsAccountsCount](js-apis-osAccount.md#getosaccountlocalidfromprocess).|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise&lt;Caller&gt; | Promise used to return the caller object to communicate with.|

**Error codes**

For details about the error codes, see [Ability Error Codes](../errorcodes/errorcode-ability.md).

| ID| Error Message|
| ------- | -------------------------------- |
| 16000001 | The specified ability does not exist. |
| 16000002 | Incorrect ability type. |
| 16000004 | Can not start invisible component. |
| 16000005 | Static permission denied. The specified process does not have the permission. |
| 16000006 | Cross-user operations are not allowed. |
| 16000008 | The crowdtesting application expires. |
| 16000011 | The context does not exist. |
| 16000012 | The application is controlled.        |
| 16000013 | The application is controlled by EDM.       |
| 16000050 | Internal error. |
| 16200001 | The caller has been released.        |

**Example**

  ```ts
  let caller;

  // ID of a system account. The value -1 indicates the current user.
  let accountId = -1;

  // Specify the ability to start.
  let want = {
      bundleName: 'com.acts.actscalleeabilityrely',
      moduleName: 'entry',
      abilityName: 'EntryAbility',
      deviceId: '',
      parameters: {
        // If the value of 'ohos.aafwk.param.callAbilityToForeground' is true, the ability is started in the foreground. If the value is false or not set, the ability is started in the background.
        'ohos.aafwk.param.callAbilityToForeground': true
      }
  };

  try {
    this.context.startAbilityByCallWithAccount(want, accountId)
      .then((obj) => {
        // Carry out normal service processing.
        caller = obj;
        console.log('startAbilityByCallWithAccount succeed');
      }).catch((error) => {
        // Process service logic errors.
        console.error('startAbilityByCallWithAccount failed, error.code: ${error.code}, error.message: ${error.message}');
      });
  } catch (paramError) {
    // Process input parameter errors.
    console.error('error.code: ${paramError.code}, error.message: ${paramError.message}');
  }
  ```
