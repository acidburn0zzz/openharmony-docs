# @ohos.file.cloudSyncManager (端云同步管理能力)

该模块向云空间应用提供端云同步管理能力，包括使能/去使能端云协同能力、修改应用同步开关，云端数据变化通知以及帐号退出清理/保留云相关文件等。

> **说明：**
>
> - 本模块首批接口从API version 10开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。
> - 本模块接口为系统接口，三方应用不支持调用。

## 导入模块

```js
import cloudSyncManager from '@ohos.file.cloudSyncManager'
```

## cloudSyncManager.changeAppCloudSwitch

changeAppCloudSwitch(accountId: string, bundleName: string, status: boolean): Promise&lt;void&gt;

异步方法修改应用的端云文件同步开关，以Promise形式返回结果。

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id |
| bundleName | string | 是   | 应用包名|
| status | boolean | 是   | 修改的应用云同步开关状态，true为打开，false为关闭|

**返回值：**

| 类型                  | 说明             |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | 使用Promise形式返回修改应用的端云文件同步开关的结果 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.changeAppCloudSwitch(accountId, bundleName, true).then(function() {
      console.info("changeAppCloudSwitch successfully");
  }).catch(function(err) {
      console.info("changeAppCloudSwitch failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.changeAppCloudSwitch

changeAppCloudSwitch(accountId: string, bundleName: string, status: boolean, callback: AsyncCallback&lt;void&gt;): void

异步方法修改应用的端云文件同步开关，以callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| bundleName | string | 是   | 应用包名|
| status | boolean | 是   | 修改的应用云同步开关状态，true为打开，false为关闭|
| callback | AsyncCallback&lt;void&gt; | 是   | 异步修改应用的端云文件同步开关之后的回调 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.changeAppCloudSwitch(accountId, bundleName, true, (err) => {
    if (err) {
      console.info("changeAppCloudSwitch failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("changeAppCloudSwitch successfully");
    }
  });
  ```

## cloudSyncManager.notifyDataChange

notifyDataChange(accountId: string, bundleName: string): Promise&lt;void&gt;

异步方法通知端云服务应用的云数据变更，以Promise形式返回结果。

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| bundleName | string | 是   | 应用包名|

**返回值：**

| 类型                  | 说明             |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | 使用Promise形式返回通知端云服务应用的云数据变更的结果 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.notifyDataChange(accountId, bundleName).then(function() {
      console.info("notifyDataChange successfully");
  }).catch(function(err) {
      console.info("notifyDataChange failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.notifyDataChange

notifyDataChange(accountId: string, bundleName: string, callback: AsyncCallback&lt;void&gt;): void

异步方法通知端云服务应用的云数据变更，以callback形式返回结果。

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| bundleName | string | 是   | 应用包名|
| callback | AsyncCallback&lt;void&gt; | 是   | 异步通知端云服务应用的云数据变更之后的回调 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let bundleName = "com.example.bundle";
  cloudSyncManager.notifyDataChange(accountId, bundleName, (err) => {
    if (err) {
      console.info("notifyDataChange failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("notifyDataChange successfully");
    }
  });
  ```

## cloudSyncManager.enableCloud

enableCloud(accountId: string, switches: { [bundleName: string]: boolean }): Promise&lt;void&gt;

异步方法使能端云协同能力，以Promise形式返回结果。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| switches | object | 是   | 应用的端云协同特性使能开关，bundleName为应用包名，开关状态是个boolean类型|

**返回值：**

| 类型                  | 说明             |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | 使用Promise形式返回使能端云协同能力的结果 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let switches = {"com.example.bundleName1": true, "com.example.bundleName2": false};
  cloudSyncManager.enableCloud(accountId, switches).then(function() {
      console.info("enableCloud successfully");
  }).catch(function(err) {
      console.info("enableCloud failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.enableCloud

enableCloud(accountId: string, switches: { [bundleName: string]: boolean }, callback: AsyncCallback&lt;void&gt;): void

异步方法使能端云协同能力，以callback形式返回结果。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| switches | object | 是   | 应用的端云协同特性使能开关，bundleName为应用包名，开关状态是个boolean类型|
| callback | AsyncCallback&lt;void&gt; | 是   | 异步使能端云协同能力之后的回调 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let switches = {"com.example.bundleName1": true, "com.example.bundleName2": false};
  cloudSyncManager.enableCloud(accountId, switches, (err) => {
    if (err) {
      console.info("enableCloud failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("enableCloud successfully");
    }
  });
  ```

## cloudSyncManager.disableCloud

disableCloud(accountId: string): Promise&lt;void&gt;

异步方法去使能端云协同能力，以Promise形式返回结果。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|

**返回值：**

| 类型                  | 说明             |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | 使用Promise形式返回去使能端云协同能力的结果 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  cloudSyncManager.disableCloud(accountId).then(function() {
      console.info("disableCloud successfully");
  }).catch(function(err) {
      console.info("disableCloud failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.disableCloud

disableCloud(accountId: string, callback: AsyncCallback&lt;void&gt;): void

异步方法去使能端云协同能力，以callback形式返回结果。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| callback | AsyncCallback&lt;void&gt; | 是   | 异步去使能端云协同能力之后的回调 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  cloudSyncManager.disableCloud(accountId, (err) => {
    if (err) {
      console.info("disableCloud failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("disableCloud successfully");
    }
  });
  ```

## Action

清理本地云相关数据时的Action，为枚举类型。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**: SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

| 名称 |  值|  说明 |
| ----- |  ---- |  ---- |
| RETAIN_DATA |  0 |  仅清除云端标识，保留本地缓存文件|
| CLEAR_DATA |  1 |  清除云端标识信息，若存在本地缓存文件，一并删除|

## cloudSyncManager.clean

clean(accountId: string, appActions: { [bundleName: string]: Action }): Promise&lt;void&gt;

异步方法清理本地云相关数据，以Promise形式返回结果。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| appActions | object | 是   | 清理动作类型，bundleName为待清理应用包名, [Action](#action)为清理动作类型|

**返回值：**

| 类型                  | 说明             |
| --------------------- | ---------------- |
| Promise&lt;void&gt; | 使用Promise形式返回清理本地云相关数据的结果 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let appActions = {"com.example.bundleName1": cloudSyncManager.Action.RETAIN_DATA,
                    "com.example.bundleName2": cloudSyncManager.Action.CLEAR_DATA};
  cloudSyncManager.clean(accountId, appActions).then(function() {
      console.info("clean successfully");
  }).catch(function(err) {
      console.info("clean failed with error message: " + err.message + ", error code: " + err.code);
  });
  ```

## cloudSyncManager.clean

clean(accountId: string, appActions: { [bundleName: string]: Action }, callback: AsyncCallback&lt;void&gt;): void

异步方法清理本地云相关数据，以callback形式返回结果。

**需要权限**：ohos.permission.CLOUDFILE_SYNC_MANAGER

**系统能力**：SystemCapability.FileManagement.DistributedFileService.CloudSyncManager

**参数：**

| 参数名     | 类型   | 必填 | 说明 |
| ---------- | ------ | ---- | ---- |
| accountId | string | 是   | 帐号Id|
| appActions | object | 是   | 清理动作类型，bundleName为待清理应用包名, [Action](#action)为清理动作类型|
| callback | AsyncCallback&lt;void&gt; | 是   | 异步方法清理本地云相关数据 |

**错误码：**

以下错误码的详细介绍请参见[文件管理子系统错误码](../errorcodes/errorcode-filemanagement.md)。

| 错误码ID                     | 错误信息        |
| ---------------------------- | ---------- |
| 201 | Permission verification failed. |
| 202 | The caller is not a system application. |
| 401 | The input parameter is invalid. |

**示例：**

  ```js
  let accountId = "testAccount";
  let appActions = {"com.example.bundleName1": cloudSyncManager.Action.RETAIN_DATA,
                    "com.example.bundleName2": cloudSyncManager.Action.CLEAR_DATA};
  cloudSyncManager.clean(accountId, appActions, (err) => {
    if (err) {
      console.info("clean failed with error message: " + err.message + ", error code: " + err.code);
    } else {
      console.info("clean successfully");
    }
  });
  ```
