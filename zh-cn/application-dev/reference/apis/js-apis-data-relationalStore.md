# @ohos.data.relationalStore (关系型数据库)

关系型数据库（Relational Database，RDB）是一种基于关系模型来管理数据的数据库。关系型数据库基于SQLite组件提供了一套完整的对本地数据库进行管理的机制，对外提供了一系列的增、删、改、查等接口，也可以直接运行用户输入的SQL语句来满足复杂的场景需要。不支持Worker线程。

该模块提供以下关系型数据库相关的常用功能：

- [RdbPredicates](#rdbpredicates)： 数据库中用来代表数据实体的性质、特征或者数据实体之间关系的词项，主要用来定义数据库的操作条件。
- [RdbStore](#rdbstore)：提供管理关系数据库(RDB)方法的接口。
- [ResultSet](#resultset)：提供用户调用关系型数据库查询接口之后返回的结果集合。

> **说明：**
> 
> 本模块首批接口从API version 9开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import relationalStore from '@ohos.data.relationalStore'
```

## relationalStore.getRdbStore

getRdbStore(context: Context, config: StoreConfig, callback: AsyncCallback&lt;RdbStore&gt;): void

获得一个相关的RdbStore，操作关系型数据库，用户可以根据自己的需求配置RdbStore的参数，然后通过RdbStore调用相关接口可以执行相关的数据操作，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                           | 必填 | 说明                                                         |
| -------- | ---------------------------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                                        | 是   | 应用的上下文。 <br>FA模型的应用Context定义见[Context](js-apis-inner-app-context.md)。<br>Stage模型的应用Context定义见[Context](js-apis-inner-application-uiAbilityContext.md)。 |
| config   | [StoreConfig](#storeconfig)               | 是   | 与此RDB存储相关的数据库配置。                                |
| callback | AsyncCallback&lt;[RdbStore](#rdbstore)&gt; | 是   | 指定callback回调函数，返回RdbStore对象。                   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                |
| ------------ | ----------------------------------------------------------- |
| 14800010     | Failed to open or delete database by invalid database path. |
| 14800011     | Failed to open database by database corrupted.              |
| 14800000     | Inner error.                                                |

**示例：**

FA模型示例：

```js

import featureAbility from '@ohos.ability.featureAbility'

var store;

// 获取context
let context = featureAbility.getContext();

const STORE_CONFIG = {
  name: "RdbTest.db",
  securityLevel: relationalStore.SecurityLevel.S1
};

relationalStore.getRdbStore(context, STORE_CONFIG, function (err, rdbStore) {
  store = rdbStore;
  if (err) {
    console.error(`Get RdbStore failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Get RdbStore successfully.`);
})
```

Stage模型示例：

```ts
import UIAbility from '@ohos.app.ability.UIAbility'

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage) {
    var store;
    const STORE_CONFIG = {
      name: "RdbTest.db",
      securityLevel: relationalStore.SecurityLevel.S1
    };
        
    relationalStore.getRdbStore(this.context, STORE_CONFIG, function (err, rdbStore) {
      store = rdbStore;
      if (err) {
        console.error(`Get RdbStore failed, code is ${err.code},message is ${err.message}`);
        return;
      }
      console.info(`Get RdbStore successfully.`);
    })
  }
}
```

## relationalStore.getRdbStore

getRdbStore(context: Context, config: StoreConfig): Promise&lt;RdbStore&gt;

获得一个相关的RdbStore，操作关系型数据库，用户可以根据自己的需求配置RdbStore的参数，然后通过RdbStore调用相关接口可以执行相关的数据操作，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名  | 类型                             | 必填 | 说明                                                         |
| ------- | -------------------------------- | ---- | ------------------------------------------------------------ |
| context | Context                          | 是   | 应用的上下文。 <br>FA模型的应用Context定义见[Context](js-apis-inner-app-context.md)。<br>Stage模型的应用Context定义见[Context](js-apis-inner-application-uiAbilityContext.md)。 |
| config  | [StoreConfig](#storeconfig) | 是   | 与此RDB存储相关的数据库配置。                                |

**返回值**：

| 类型                                      | 说明                              |
| ----------------------------------------- | --------------------------------- |
| Promise&lt;[RdbStore](#rdbstore)&gt; | Promise对象。返回RdbStore对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                |
| ------------ | ----------------------------------------------------------- |
| 14800010     | Failed to open or delete database by invalid database path. |
| 14800011     | Failed to open database by database corrupted.              |
| 14800000     | Inner error.                                                |

**示例：**

FA模型示例：

```js
import featureAbility from '@ohos.ability.featureAbility'

var store;

// 获取context
let context = featureAbility.getContext();

const STORE_CONFIG = {
  name: "RdbTest.db",
  securityLevel: relationalStore.SecurityLevel.S1
};

let promise = relationalStore.getRdbStore(context, STORE_CONFIG);
promise.then(async (rdbStore) => {
  store = rdbStore;
  console.info(`Get RdbStore successfully.`);
}).catch((err) => {
  console.error(`Get RdbStore failed, code is ${err.code},message is ${err.message}`);
})
```

Stage模型示例：

```ts
import UIAbility from '@ohos.app.ability.UIAbility'

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage) {
    var store;
    const STORE_CONFIG = {
      name: "RdbTest.db",
      securityLevel: relationalStore.SecurityLevel.S1
    };
        
    let promise = relationalStore.getRdbStore(this.context, STORE_CONFIG);
    promise.then(async (rdbStore) => {
      store = rdbStore;
      console.info(`Get RdbStore successfully.`)
    }).catch((err) => {
      console.error(`Get RdbStore failed, code is ${err.code},message is ${err.message}`);
    })
  }
}
```

## relationalStore.deleteRdbStore

deleteRdbStore(context: Context, name: string, callback: AsyncCallback&lt;void&gt;): void

删除数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                                                         |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| context  | Context                   | 是   | 应用的上下文。 <br>FA模型的应用Context定义见[Context](js-apis-inner-app-context.md)。<br>Stage模型的应用Context定义见[Context](js-apis-inner-application-uiAbilityContext.md)。 |
| name     | string                    | 是   | 数据库名称。                                                 |
| callback | AsyncCallback&lt;void&gt; | 是   | 指定callback回调函数。                                       |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                |
| ------------ | ----------------------------------------------------------- |
| 14800010     | Failed to open or delete database by invalid database path. |
| 14800000     | Inner error.                                                |

**示例：**

FA模型示例：

```js
import featureAbility from '@ohos.ability.featureAbility'

// 获取context
let context = featureAbility.getContext()

relationalStore.deleteRdbStore(context, "RdbTest.db", function (err) {
  if (err) {
    console.error(`Delete RdbStore failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Delete RdbStore successfully.`);
})
```

Stage模型示例：

```ts
import UIAbility from '@ohos.app.ability.UIAbility'

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage){
    relationalStore.deleteRdbStore(this.context, "RdbTest.db", function (err) {
      if (err) {
        console.error(`Delete RdbStore failed, code is ${err.code},message is ${err.message}`);
        return;
      }
      console.info(`Delete RdbStore successfully.`);
    })
  }
}
```

## relationalStore.deleteRdbStore

deleteRdbStore(context: Context, name: string): Promise&lt;void&gt;

使用指定的数据库文件配置删除数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数**

| 参数名  | 类型    | 必填 | 说明                                                         |
| ------- | ------- | ---- | ------------------------------------------------------------ |
| context | Context | 是   | 应用的上下文。 <br>FA模型的应用Context定义见[Context](js-apis-inner-app-context.md)。<br>Stage模型的应用Context定义见[Context](js-apis-inner-application-uiAbilityContext.md)。 |
| name    | string  | 是   | 数据库名称。                                                 |

**返回值**：

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                |
| ------------ | ----------------------------------------------------------- |
| 14800010     | Failed to open or delete database by invalid database path. |
| 14800000     | Inner error.                                                |

**示例：**

FA模型示例：

```js
import featureAbility from '@ohos.ability.featureAbility'

// 获取context
let context = featureAbility.getContext();

let promise = relationalStore.deleteRdbStore(context, "RdbTest.db");
promise.then(()=>{
  console.info(`Delete RdbStore successfully.`);
}).catch((err) => {
  console.error(`Delete RdbStore failed, code is ${err.code},message is ${err.message}`);
})
```

Stage模型示例：

```ts
import UIAbility from '@ohos.app.ability.UIAbility'

class EntryAbility extends UIAbility {
  onWindowStageCreate(windowStage){
    let promise = relationalStore.deleteRdbStore(this.context, "RdbTest.db");
    promise.then(()=>{
      console.info(`Delete RdbStore successfully.`);
    }).catch((err) => {
      console.error(`Delete RdbStore failed, code is ${err.code},message is ${err.message}`);
    })
  }
}
```

## StoreConfig

管理关系数据库配置。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称        | 类型          | 必填 | 说明                                                      |
| ------------- | ------------- | ---- | --------------------------------------------------------- |
| name          | string        | 是   | 数据库文件名。                                            |
| securityLevel | [SecurityLevel](#securitylevel) | 是   | 设置数据库安全级别                                        |
| encrypt       | boolean       | 否   | 指定数据库是否加密，默认不加密。<br/> true:加密。<br/> false:非加密。 |

## SecurityLevel

数据库的安全级别枚举。

> **说明：**
>
> 若需要进行同步操作，数据库安全等级应不高于对端设备安全等级，具体可见[跨设备同步访问控制机制](../../database/sync-app-data-across-devices-overview.md#跨设备同步访问控制机制)。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称 | 值   | 说明                                                         |
| ---- | ---- | ------------------------------------------------------------ |
| S1   | 1    | 表示数据库的安全级别为低级别，当数据泄露时会产生较低影响。例如，包含壁纸等系统数据的数据库。 |
| S2   | 2    | 表示数据库的安全级别为中级别，当数据泄露时会产生较大影响。例如，包含录音、视频等用户生成数据或通话记录等信息的数据库。 |
| S3   | 3    | 表示数据库的安全级别为高级别，当数据泄露时会产生重大影响。例如，包含用户运动、健康、位置等信息的数据库。 |
| S4   | 4    | 表示数据库的安全级别为关键级别，当数据泄露时会产生严重影响。例如，包含认证凭据、财务数据等信息的数据库。 |

## AssetStatus<sup>10+</sup>

描述资产附件的状态枚举。请使用枚举名称而非枚举值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称                              | 值   | 说明             |
| ------------------------------- | --- | -------------- |
| ASSET_NORMAL     | -   | 表示资产状态正常。      |
| ASSET_INSERT | - | 表示资产需要插入到云端。 |
| ASSET_UPDATE | - | 表示资产需要更新到云端。 |
| ASSET_DELETE | - | 表示资产需要在云端删除。 |
| ASSET_ABNORMAL    | -   | 表示资产状态异常。      |
| ASSET_DOWNLOADING | -   | 表示资产正在下载到本地设备。 |

## Asset<sup>10+</sup>

记录资产附件（文件、图片、视频等类型文件）的相关信息。资产类型的相关接口暂不支持Datashare。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称          | 类型                          | 必填  | 说明           |
| ----------- | --------------------------- | --- | ------------ |
| name        | string                      | 是   | 资产的名称。       |
| uri         | string                      | 是   | 资产的uri，在系统里的绝对路径。       |
| path        | string                      | 是   | 资产在应用沙箱里的路径。       |
| createTime  | string                      | 是   | 资产被创建出来的时间。   |
| modifyTime  | string                      | 是   | 资产最后一次被修改的时间。 |
| size        | string                      | 是   | 资产占用空间的大小。    |
| status      | [AssetStatus](#assetstatus10) | 否   | 资产的状态，默认值为ASSET_NORMAL。        |

## Assets<sup>10+</sup>

表示[Asset](#asset10)类型的数组。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 类型    | 说明                 |
| ------- | -------------------- |
| [Asset](#asset10)[] | 表示Asset类型的数组。   |

## ValueType

用于表示允许的数据字段类型。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 类型    | 说明                 |
| ------- | -------------------- |
| null<sup>10+</sup>    | 表示值类型为空。   |
| number  | 表示值类型为数字。   |
| string  | 表示值类型为字符。   |
| boolean | 表示值类型为布尔值。 |
| Uint8Array<sup>10+</sup>           | 表示值类型为Uint8类型的数组。            |
| Asset<sup>10+</sup>  | 表示值类型为附件[Asset](#asset10)。     |
| Assets<sup>10+</sup> | 表示值类型为附件数组[Assets](#assets10)。 |

## ValuesBucket

用于存储键值对的类型。该类型不是多线程安全的，如果应用中存在多线程同时操作该类派生出的实例，注意加锁保护。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 键类型 | 值类型                   |
| ------ | ----------------------- |
| string | [ValueType](#valuetype) |

## PRIKeyType<sup>10+</sup> 

用于表示数据库表某一行主键的数据类型。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 类型             | 说明                               |
| ---------------- | ---------------------------------- |
| number \| string | 主键的类型可以是number或者string。 |

## UTCTime<sup>10+</sup>

用于表示UTC类型时间的数据类型。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 类型 | 说明            |
| ---- | --------------- |
| Date | UTC类型的时间。 |

## ModifyTime<sup>10+</sup> 

用于存储数据库表的主键和修改时间的数据类型。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 类型                                                    | 说明                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| Map<[PRIKeyType](#prikeytype10), [UTCTime](#utctime10)> | 键表示是数据库表某一行的主键，值表示该行的最后修改时间，用UTC格式表示。 |

## SyncMode

指数据库同步模式。

| 名称           | 值   | 说明                               |
| -------------- | ---- | ---------------------------------- |
| SYNC_MODE_PUSH                       | 0   | 表示数据从本地设备推送到远程设备。<br>**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core                     |
| SYNC_MODE_PULL                       | 1   | 表示数据从远程设备拉至本地设备。<br>**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core                      |
| SYNC_MODE_TIME_FIRST<sup>10+</sup>   | -   | 表示数据从修改时间较近的一端同步到修改时间较远的一端。请使用枚举名称而非枚举值。<br>**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client |
| SYNC_MODE_NATIVE_FIRST<sup>10+</sup> | -   | 表示数据从本地设备同步到云端。请使用枚举名称而非枚举值。<br>**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client             |
| SYNC_MODE_CLOUD_FIRST<sup>10+</sup>  | -   | 表示数据从云端同步到本地设备。请使用枚举名称而非枚举值。<br>**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client             |

## SubscribeType

描述订阅类型。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

| 名称                  | 值   | 说明               |
| --------------------- | ---- | ------------------ |
| SUBSCRIBE_TYPE_REMOTE | 0    | 订阅远程数据更改。<br>**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core |
| SUBSCRIBE_TYPE_CLOUD<sup>10+</sup> | -  | 订阅云端数据更改。请使用枚举名称而非枚举值。<br>**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client |
| SUBSCRIBE_TYPE_CLOUD_DETAILS<sup>10+</sup> | -  | 订阅云端数据更改详情。请使用枚举名称而非枚举值。<br>**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client |

## ChangeType<sup>10+</sup>

描述数据变更类型的枚举。请使用枚举名称而非枚举值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

| 名称                         | 值   | 说明                         |
| -------------------------- | --- | -------------------------- |
| DATA_CHANGE  | -   | 表示是数据发生变更。   |
| ASSET_CHANGE | -   | 表示是资产附件发生了变更。 |

## ChangeInfo<sup>10+</sup>

记录端云同步过程详情。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称     | 类型                               | 必填 | 说明                                                         |
| -------- | ---------------------------------- | ---- | ------------------------------------------------------------ |
| table    | string                             | 是   | 表示发生变化的表的名称。                                     |
| type     | [ChangeType](#changetype10)        | 是   | 表示发生变化的数据的类型，数据或者资产附件发生变化。         |
| inserted | Array\<string\> \| Array\<number\> | 是   | 记录插入数据的位置，如果该表的主键是string类型，该值是主键的值，否则该值表示插入数据的行号。 |
| updated  | Array\<string\> \| Array\<number\> | 是   | 记录更新数据的位置，如果该表的主键是string类型，该值是主键的值，否则该值表示更新数据的行号。 |
| deleted  | Array\<string\> \| Array\<number\> | 是   | 记录删除数据的位置，如果该表的主键是string类型，该值是主键的值，否则该值表示删除数据的行号。 |

## DistributedType<sup>10+</sup>

描述表的分布式类型的枚举。请使用枚举名称而非枚举值。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

| 名称                | 值   | 说明                                                                                                 |
| ------------------ | --- | -------------------------------------------------------------------------------------------------- |
| DISTRIBUTED_DEVICE | -  | 表示在不同设备之间分布式的数据库表。<br>**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core               |
| DISTRIBUTED_CLOUD  | -   | 表示在设备和云端之间分布式的数据库表。<br>**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client |

## DistributedConfig<sup>10+</sup>

记录表的分布式配置信息。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称     | 类型    | 必填 | 说明                                                         |
| -------- | ------- | ---- | ------------------------------------------------------------ |
| autoSync | boolean | 是   | 该值为true时，表示该表支持自动同步和手动同步；该值为false时，表示该表只支持手动同步，不支持自动同步。 |

## ConflictResolution<sup>10+</sup>

插入和修改接口的冲突解决方式。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称                 | 值   | 说明                                                         |
| -------------------- | ---- | ------------------------------------------------------------ |
| ON_CONFLICT_NONE | 0 | 表示当冲突发生时，不做任何处理。 |
| ON_CONFLICT_ROLLBACK | 1    | 表示当冲突发生时，中止SQL语句并回滚当前事务。                |
| ON_CONFLICT_ABORT    | 2    | 表示当冲突发生时，中止当前SQL语句，并撤销当前 SQL 语句所做的任何更改，但是由同一事务中先前的 SQL 语句引起的更改被保留并且事务保持活动状态。 |
| ON_CONFLICT_FAIL     | 3    | 表示当冲突发生时，中止当前 SQL 语句。但它不会撤销失败的 SQL 语句的先前更改，也不会结束事务。 |
| ON_CONFLICT_IGNORE   | 4    | 表示当冲突发生时，跳过包含违反约束的行并继续处理 SQL 语句的后续行。 |
| ON_CONFLICT_REPLACE  | 5    | 表示当冲突发生时，在插入或更新当前行之前删除导致约束违例的预先存在的行，并且命令会继续正常执行。 |

## Progress<sup>10+</sup>

描述端云同步过程的枚举。请使用枚举名称而非枚举值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称             | 值   | 说明                     |
| ---------------- | ---- | ------------------------ |
| SYNC_BEGIN       | -    | 表示端云同步过程开始。   |
| SYNC_IN_PROGRESS | -    | 表示正在端云同步过程中。 |
| SYNC_FINISH      | -    | 表示端云同步过程已完成。 |

## Statistic<sup>10+</sup>

描述数据库表的端云同步过程的统计信息。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称     | 类型   | 必填 | 说明                                     |
| -------- | ------ | ---- | ---------------------------------------- |
| total    | number | 是   | 表示数据库表中需要端云同步的总行数。     |
| success  | number | 是   | 表示数据库表中端云同步成功的行数。       |
| failed   | number | 是   | 表示数据库表中端云同步失败的行数。       |
| remained | number | 是   | 表示数据库表中端云同步剩余未执行的行数。 |

## TableDetails<sup>10+</sup>

描述数据库表执行端云同步任务上传和下载的统计信息。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称     | 类型                      | 必填 | 说明                                       |
| -------- | ------------------------- | ---- | ------------------------------------------ |
| upload   | [Statistic](#statistic10) | 是   | 表示数据库表中端云同步上传过程的统计信息。 |
| download | [Statistic](#statistic10) | 是   | 表示数据库表中端云同步下载过程的统计信息。 |

## ProgressCode<sup>10+</sup>

表示端云同步过程的状态。请使用枚举名称而非枚举值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称                  | 值   | 说明                                                         |
| --------------------- | ---- | ------------------------------------------------------------ |
| SUCCESS               | -    | 表示端云同步过程成功。                                       |
| UNKNOWN_ERROR         | -    | 表示端云同步过程遇到未知错误。                               |
| NETWORK_ERROR         | -    | 表示端云同步过程遇到网络错误。                               |
| CLOUD_DISABLED        | -    | 表示云端不可用。                                             |
| LOCKED_BY_OTHERS      | -    | 表示有其他设备正在端云同步，本设备无法进行端云同步。<br>请确保无其他设备占用云端资源后，再使用本设备进行端云同步任务。 |
| RECORD_LIMIT_EXCEEDED | -    | 表示本次端云同步需要同步的条目或大小超出最大值。由云端配置最大值。 |
| NO_SPACE_FOR_ASSET    | -    | 表示云空间剩余空间小于待同步的资产大小。                     |

## ProgressDetails<sup>10+</sup>

描述数据库整体执行端云同步任务上传和下载的统计信息。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称     | 类型                                              | 必填 | 说明                                                         |
| -------- | ------------------------------------------------- | ---- | ------------------------------------------------------------ |
| schedule | [Progress](#progress10)                           | 是   | 表示端云同步过程。                                           |
| code     | [ProgressCode](#progresscode10)                   | 是   | 表示端云同步过程的状态。                                     |
| details  | [table: string] : [TableDetails](#tabledetails10) | 是   | 表示端云同步各表的统计信息。<br>键表示表名，值表示该表的端云同步过程统计信息。 |

## RdbPredicates

表示关系型数据库（RDB）的谓词。该类确定RDB中条件表达式的值是true还是false。该类型不是多线程安全的，如果应用中存在多线程同时操作该类派生出的实例，注意加锁保护。

### constructor

constructor(name: string)

构造函数。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明         |
| ------ | ------ | ---- | ------------ |
| name   | string | 是   | 数据库表名。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
```

### inDevices

inDevices(devices: Array&lt;string&gt;): RdbPredicates

同步分布式数据库时连接到组网内指定的远程设备。

> **说明：**
>
> 其中devices通过调用[deviceManager.getTrustedDeviceListSync](js-apis-device-manager.md#gettrusteddevicelistsync)方法得到。deviceManager模块的接口均为系统接口，仅系统应用可用。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名  | 类型                | 必填 | 说明                       |
| ------- | ------------------- | ---- | -------------------------- |
| devices | Array&lt;string&gt; | 是   | 指定的组网内的远程设备ID。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceIds = [];

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    for (var i = 0; i < devices.length; i++) {
        deviceIds[i] = devices[i].deviceId;
    }
})
                                  
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.inDevices(deviceIds);
```

### inAllDevices

inAllDevices(): RdbPredicates


同步分布式数据库时连接到组网内所有的远程设备。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.inAllDevices();
```

### equalTo

equalTo(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为ValueType且值等于指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                   |
| ------ | ----------------------- | ---- | ---------------------- |
| field  | string                  | 是   | 数据库表中的列名。     |
| value  | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "lisi");
```


### notEqualTo

notEqualTo(field: string, value: ValueType): RdbPredicates


配置谓词以匹配数据字段为ValueType且值不等于指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                   |
| ------ | ----------------------- | ---- | ---------------------- |
| field  | string                  | 是   | 数据库表中的列名。     |
| value  | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.notEqualTo("NAME", "lisi");
```


### beginWrap

beginWrap(): RdbPredicates


向谓词添加左括号。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值**：

| 类型                                 | 说明                      |
| ------------------------------------ | ------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回带有左括号的Rdb谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "lisi")
    .beginWrap()
    .equalTo("AGE", 18)
    .or()
    .equalTo("SALARY", 200.5)
    .endWrap()
```

### endWrap

endWrap(): RdbPredicates

向谓词添加右括号。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值**：

| 类型                                 | 说明                      |
| ------------------------------------ | ------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回带有右括号的Rdb谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "lisi")
    .beginWrap()
    .equalTo("AGE", 18)
    .or()
    .equalTo("SALARY", 200.5)
    .endWrap()
```

### or

or(): RdbPredicates

将或条件添加到谓词中。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值**：

| 类型                                 | 说明                      |
| ------------------------------------ | ------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回带有或条件的Rdb谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa")
    .or()
    .equalTo("NAME", "Rose")
```

### and

and(): RdbPredicates

向谓词添加和条件。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值**：

| 类型                                 | 说明                      |
| ------------------------------------ | ------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回带有和条件的Rdb谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa")
    .and()
    .equalTo("SALARY", 200.5)
```

### contains

contains(field: string, value: string): RdbPredicates

配置谓词以匹配数据字段为string且value包含指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                   |
| ------ | ------ | ---- | ---------------------- |
| field  | string | 是   | 数据库表中的列名。     |
| value  | string | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.contains("NAME", "os");
```

### beginsWith

beginsWith(field: string, value: string): RdbPredicates

配置谓词以匹配数据字段为string且值以指定字符串开头的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                   |
| ------ | ------ | ---- | ---------------------- |
| field  | string | 是   | 数据库表中的列名。     |
| value  | string | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.beginsWith("NAME", "os");
```

### endsWith

endsWith(field: string, value: string): RdbPredicates

配置谓词以匹配数据字段为string且值以指定字符串结尾的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                   |
| ------ | ------ | ---- | ---------------------- |
| field  | string | 是   | 数据库表中的列名。     |
| value  | string | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.endsWith("NAME", "se");
```

### isNull

isNull(field: string): RdbPredicates

配置谓词以匹配值为null的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| field  | string | 是   | 数据库表中的列名。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例**：

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.isNull("NAME");
```

### isNotNull

isNotNull(field: string): RdbPredicates

配置谓词以匹配值不为null的指定字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| field  | string | 是   | 数据库表中的列名。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.isNotNull("NAME");
```

### like

like(field: string, value: string): RdbPredicates

配置谓词以匹配数据字段为string且值类似于指定字符串的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                   |
| ------ | ------ | ---- | ---------------------- |
| field  | string | 是   | 数据库表中的列名。     |
| value  | string | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.like("NAME", "%os%");
```

### glob

glob(field: string, value: string): RdbPredicates

配置RdbPredicates匹配数据字段为string的指定字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                                                         |
| ------ | ------ | ---- | ------------------------------------------------------------ |
| field  | string | 是   | 数据库表中的列名。                                           |
| value  | string | 是   | 指示要与谓词匹配的值。<br>支持通配符，*表示0个、1个或多个数字或字符，?表示1个数字或字符。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.glob("NAME", "?h*g");
```

### between

between(field: string, low: ValueType, high: ValueType): RdbPredicates

将谓词配置为匹配数据字段为ValueType且value在给定范围内的指定字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                       |
| ------ | ----------------------- | ---- | -------------------------- |
| field  | string                  | 是   | 数据库表中的列名。         |
| low    | [ValueType](#valuetype) | 是   | 指示与谓词匹配的最小值。   |
| high   | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的最大值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.between("AGE", 10, 50);
```

### notBetween

notBetween(field: string, low: ValueType, high: ValueType): RdbPredicates

配置RdbPredicates以匹配数据字段为ValueType且value超出给定范围的指定字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                       |
| ------ | ----------------------- | ---- | -------------------------- |
| field  | string                  | 是   | 数据库表中的列名。         |
| low    | [ValueType](#valuetype) | 是   | 指示与谓词匹配的最小值。   |
| high   | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的最大值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.notBetween("AGE", 10, 50);
```

### greaterThan

greaterThan(field: string, value: ValueType): RdbPredicates

配置谓词以匹配数据字段为ValueType且值大于指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                   |
| ------ | ----------------------- | ---- | ---------------------- |
| field  | string                  | 是   | 数据库表中的列名。     |
| value  | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.greaterThan("AGE", 18);
```

### lessThan

lessThan(field: string, value: ValueType): RdbPredicates

配置谓词以匹配数据字段为valueType且value小于指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                   |
| ------ | ----------------------- | ---- | ---------------------- |
| field  | string                  | 是   | 数据库表中的列名。     |
| value  | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.lessThan("AGE", 20);
```

### greaterThanOrEqualTo

greaterThanOrEqualTo(field: string, value: ValueType): RdbPredicates

配置谓词以匹配数据字段为ValueType且value大于或等于指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                   |
| ------ | ----------------------- | ---- | ---------------------- |
| field  | string                  | 是   | 数据库表中的列名。     |
| value  | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.greaterThanOrEqualTo("AGE", 18);
```

### lessThanOrEqualTo

lessThanOrEqualTo(field: string, value: ValueType): RdbPredicates

配置谓词以匹配数据字段为ValueType且value小于或等于指定值的字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                    | 必填 | 说明                   |
| ------ | ----------------------- | ---- | ---------------------- |
| field  | string                  | 是   | 数据库表中的列名。     |
| value  | [ValueType](#valuetype) | 是   | 指示要与谓词匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.lessThanOrEqualTo("AGE", 20);
```

### orderByAsc

orderByAsc(field: string): RdbPredicates

配置谓词以匹配其值按升序排序的列。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| field  | string | 是   | 数据库表中的列名。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.orderByAsc("NAME");
```

### orderByDesc

orderByDesc(field: string): RdbPredicates

配置谓词以匹配其值按降序排序的列。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明               |
| ------ | ------ | ---- | ------------------ |
| field  | string | 是   | 数据库表中的列名。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.orderByDesc("AGE");
```

### distinct

distinct(): RdbPredicates

配置谓词以过滤重复记录并仅保留其中一个。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值**：

| 类型                                 | 说明                           |
| ------------------------------------ | ------------------------------ |
| [RdbPredicates](#rdbpredicates) | 返回可用于过滤重复记录的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Rose").distinct();
```

### limitAs

limitAs(value: number): RdbPredicates

设置最大数据记录数的谓词。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明             |
| ------ | ------ | ---- | ---------------- |
| value  | number | 是   | 最大数据记录数。 |

**返回值**：

| 类型                                 | 说明                                 |
| ------------------------------------ | ------------------------------------ |
| [RdbPredicates](#rdbpredicates) | 返回可用于设置最大数据记录数的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Rose").limitAs(3);
```

### offsetAs

offsetAs(rowOffset: number): RdbPredicates

配置RdbPredicates以指定返回结果的起始位置。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名    | 类型   | 必填 | 说明                               |
| --------- | ------ | ---- | ---------------------------------- |
| rowOffset | number | 是   | 返回结果的起始位置，取值为正整数。 |

**返回值**：

| 类型                                 | 说明                                 |
| ------------------------------------ | ------------------------------------ |
| [RdbPredicates](#rdbpredicates) | 返回具有指定返回结果起始位置的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Rose").offsetAs(3);
```

### groupBy

groupBy(fields: Array&lt;string&gt;): RdbPredicates

配置RdbPredicates按指定列分组查询结果。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                | 必填 | 说明                 |
| ------ | ------------------- | ---- | -------------------- |
| fields | Array&lt;string&gt; | 是   | 指定分组依赖的列名。 |

**返回值**：

| 类型                                 | 说明                   |
| ------------------------------------ | ---------------------- |
| [RdbPredicates](#rdbpredicates) | 返回分组查询列的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.groupBy(["AGE", "NAME"]);
```

### indexedBy

indexedBy(field: string): RdbPredicates

配置RdbPredicates以指定索引列。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明           |
| ------ | ------ | ---- | -------------- |
| field  | string | 是   | 索引列的名称。 |

**返回值**：


| 类型                                 | 说明                                  |
| ------------------------------------ | ------------------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回具有指定索引列的RdbPredicates。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.indexedBy("SALARY_INDEX");
```

### in

in(field: string, value: Array&lt;ValueType&gt;): RdbPredicates

配置RdbPredicates以匹配数据字段为ValueType数组且值在给定范围内的指定字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                                 | 必填 | 说明                                    |
| ------ | ------------------------------------ | ---- | --------------------------------------- |
| field  | string                               | 是   | 数据库表中的列名。                      |
| value  | Array&lt;[ValueType](#valuetype)&gt; | 是   | 以ValueType型数组形式指定的要匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.in("AGE", [18, 20]);
```

### notIn

notIn(field: string, value: Array&lt;ValueType&gt;): RdbPredicates

将RdbPredicates配置为匹配数据字段为ValueType且值超出给定范围的指定字段。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                                 | 必填 | 说明                                  |
| ------ | ------------------------------------ | ---- | ------------------------------------- |
| field  | string                               | 是   | 数据库表中的列名。                    |
| value  | Array&lt;[ValueType](#valuetype)&gt; | 是   | 以ValueType数组形式指定的要匹配的值。 |

**返回值**：

| 类型                                 | 说明                       |
| ------------------------------------ | -------------------------- |
| [RdbPredicates](#rdbpredicates) | 返回与指定字段匹配的谓词。 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.notIn("NAME", ["Lisa", "Rose"]);
```

## RdbStore

提供管理关系数据库(RDB)方法的接口。

在使用以下相关接口前，请使用[executeSql](#executesql)接口初始化数据库表结构和相关数据。

### 属性<sup>10+</sup>

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称         | 类型            | 必填 | 说明                             |
| ------------ | ----------- | ---- | -------------------------------- |
| version<sup>10+</sup>  | number | 是   | 设置和获取数据库版本，值为大于0的正整数。       |

**示例：**

```js
// 设置数据库版本
store.version = 3;
// 获取数据库版本
console.info(`RdbStore version is ${store.version}`);
```

### insert

insert(table: string, values: ValuesBucket, callback: AsyncCallback&lt;number&gt;):void

向目标表中插入一行数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                          | 必填 | 说明                                                       |
| -------- | ----------------------------- | ---- | ---------------------------------------------------------- |
| table    | string                        | 是   | 指定的目标表名。                                           |
| values   | [ValuesBucket](#valuesbucket) | 是   | 表示要插入到表中的数据行。                                 |
| callback | AsyncCallback&lt;number&gt;   | 是   | 指定callback回调函数。如果操作成功，返回行ID；否则返回-1。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Lisa",
  "AGE": 18,
  "SALARY": 100.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
store.insert("EMPLOYEE", valueBucket, function (err, rowId) {
  if (err) {
    console.error(`Insert is failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Insert is successful, rowId = ${rowId}`);
})
```

### insert<sup>10+</sup>

insert(table: string, values: ValuesBucket,  conflict: ConflictResolution, callback: AsyncCallback&lt;number&gt;):void

向目标表中插入一行数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                        | 必填 | 说明                                                       |
| -------- | ------------------------------------------- | ---- | ---------------------------------------------------------- |
| table    | string                                      | 是   | 指定的目标表名。                                           |
| values   | [ValuesBucket](#valuesbucket)               | 是   | 表示要插入到表中的数据行。                                 |
| conflict | [ConflictResolution](#conflictresolution10) | 是   | 指定冲突解决方式。                                         |
| callback | AsyncCallback&lt;number&gt;                 | 是   | 指定callback回调函数。如果操作成功，返回行ID；否则返回-1。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Lisa",
  "AGE": 18,
  "SALARY": 100.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
store.insert("EMPLOYEE", valueBucket, relationalStore.ConflictResolution.ON_CONFLICT_REPLACE, function (err, rowId) {
  if (err) {
    console.error(`Insert is failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Insert is successful, rowId = ${rowId}`);
})
```

### insert

insert(table: string, values: ValuesBucket):Promise&lt;number&gt;

向目标表中插入一行数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                          | 必填 | 说明                       |
| ------ | ----------------------------- | ---- | -------------------------- |
| table  | string                        | 是   | 指定的目标表名。           |
| values | [ValuesBucket](#valuesbucket) | 是   | 表示要插入到表中的数据行。 |

**返回值**：

| 类型                  | 说明                                              |
| --------------------- | ------------------------------------------------- |
| Promise&lt;number&gt; | Promise对象。如果操作成功，返回行ID；否则返回-1。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Lisa",
  "AGE": 18,
  "SALARY": 100.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let promise = store.insert("EMPLOYEE", valueBucket);
promise.then((rowId) => {
  console.info(`Insert is successful, rowId = ${rowId}`);
}).catch((err) => {
  console.error(`Insert is failed, code is ${err.code},message is ${err.message}`);
})
```

### insert<sup>10+</sup>

insert(table: string, values: ValuesBucket,  conflict: ConflictResolution):Promise&lt;number&gt;

向目标表中插入一行数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                        | 必填 | 说明                       |
| -------- | ------------------------------------------- | ---- | -------------------------- |
| table    | string                                      | 是   | 指定的目标表名。           |
| values   | [ValuesBucket](#valuesbucket)               | 是   | 表示要插入到表中的数据行。 |
| conflict | [ConflictResolution](#conflictresolution10) | 是   | 指定冲突解决方式。         |

**返回值**：

| 类型                  | 说明                                              |
| --------------------- | ------------------------------------------------- |
| Promise&lt;number&gt; | Promise对象。如果操作成功，返回行ID；否则返回-1。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Lisa",
  "AGE": 18,
  "SALARY": 100.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let promise = store.insert("EMPLOYEE", valueBucket, relationalStore.ConflictResolution.ON_CONFLICT_REPLACE);
promise.then((rowId) => {
  console.info(`Insert is successful, rowId = ${rowId}`);
}).catch((err) => {
  console.error(`Insert is failed, code is ${err.code},message is ${err.message}`);
})
```

### batchInsert

batchInsert(table: string, values: Array&lt;ValuesBucket&gt;, callback: AsyncCallback&lt;number&gt;):void

向目标表中插入一组数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                       | 必填 | 说明                                                         |
| -------- | ------------------------------------------ | ---- | ------------------------------------------------------------ |
| table    | string                                     | 是   | 指定的目标表名。                                             |
| values   | Array&lt;[ValuesBucket](#valuesbucket)&gt; | 是   | 表示要插入到表中的一组数据。                                 |
| callback | AsyncCallback&lt;number&gt;                | 是   | 指定callback回调函数。如果操作成功，返回插入的数据个数，否则返回-1。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket1 = {
  "NAME": "Lisa",
  "AGE": 18,
  "SALARY": 100.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5])
};
const valueBucket2 = {
  "NAME": "Jack",
  "AGE": 19,
  "SALARY": 101.5,
  "CODES": new Uint8Array([6, 7, 8, 9, 10])
};
const valueBucket3 = {
  "NAME": "Tom",
  "AGE": 20,
  "SALARY": 102.5,
  "CODES": new Uint8Array([11, 12, 13, 14, 15])
};

let valueBuckets = new Array(valueBucket1, valueBucket2, valueBucket3);
store.batchInsert("EMPLOYEE", valueBuckets, function(err, insertNum) {
  if (err) {
    console.error(`batchInsert is failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`batchInsert is successful, the number of values that were inserted = ${insertNum}`);
})
```

### batchInsert

batchInsert(table: string, values: Array&lt;ValuesBucket&gt;):Promise&lt;number&gt;

向目标表中插入一组数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                                       | 必填 | 说明                         |
| ------ | ------------------------------------------ | ---- | ---------------------------- |
| table  | string                                     | 是   | 指定的目标表名。             |
| values | Array&lt;[ValuesBucket](#valuesbucket)&gt; | 是   | 表示要插入到表中的一组数据。 |

**返回值**：

| 类型                  | 说明                                                        |
| --------------------- | ----------------------------------------------------------- |
| Promise&lt;number&gt; | Promise对象。如果操作成功，返回插入的数据个数，否则返回-1。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket1 = {
  "NAME": "Lisa",
  "AGE": 18,
  "SALARY": 100.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5])
};
const valueBucket2 = {
  "NAME": "Jack",
  "AGE": 19,
  "SALARY": 101.5,
  "CODES": new Uint8Array([6, 7, 8, 9, 10])
};
const valueBucket3 = {
  "NAME": "Tom",
  "AGE": 20,
  "SALARY": 102.5,
  "CODES": new Uint8Array([11, 12, 13, 14, 15])
};

let valueBuckets = new Array(valueBucket1, valueBucket2, valueBucket3);
let promise = store.batchInsert("EMPLOYEE", valueBuckets);
promise.then((insertNum) => {
  console.info(`batchInsert is successful, the number of values that were inserted = ${insertNum}`);
}).catch((err) => {
  console.error(`batchInsert is failed, code is ${err.code},message is ${err.message}`);
})
```

### update

update(values: ValuesBucket, predicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void

根据RdbPredicates的指定实例对象更新数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                 | 必填 | 说明                                                         |
| ---------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| values     | [ValuesBucket](#valuesbucket)        | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | RdbPredicates的实例对象指定的更新条件。                    |
| callback   | AsyncCallback&lt;number&gt;          | 是   | 指定的callback回调方法。返回受影响的行数。                   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Rose",
  "AGE": 22,
  "SALARY": 200.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa");
store.update(valueBucket, predicates, function (err, rows) {
  if (err) {
    console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Updated row count: ${rows}`);
})
```

### update<sup>10+</sup>

update(values: ValuesBucket, predicates: RdbPredicates, conflict: ConflictResolution, callback: AsyncCallback&lt;number&gt;):void

根据RdbPredicates的指定实例对象更新数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                        | 必填 | 说明                                                         |
| ---------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| values     | [ValuesBucket](#valuesbucket)               | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [RdbPredicates](#rdbpredicates)            | 是   | RdbPredicates的实例对象指定的更新条件。                      |
| conflict   | [ConflictResolution](#conflictresolution10) | 是   | 指定冲突解决方式。                                           |
| callback   | AsyncCallback&lt;number&gt;                 | 是   | 指定的callback回调方法。返回受影响的行数。                   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Rose",
  "AGE": 22,
  "SALARY": 200.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa");
store.update(valueBucket, predicates, relationalStore.ConflictResolution.ON_CONFLICT_REPLACE, function (err, rows) {
  if (err) {
    console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Updated row count: ${rows}`);
})
```

### update

update(values: ValuesBucket, predicates: RdbPredicates):Promise&lt;number&gt;

根据RdbPredicates的指定实例对象更新数据库中的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名       | 类型                                 | 必填 | 说明                                                         |
| ------------ | ------------------------------------ | ---- | ------------------------------------------------------------ |
| values       | [ValuesBucket](#valuesbucket)        | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | RdbPredicates的实例对象指定的更新条件。                    |

**返回值**：

| 类型                  | 说明                                      |
| --------------------- | ----------------------------------------- |
| Promise&lt;number&gt; | 指定的Promise回调方法。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Rose",
  "AGE": 22,
  "SALARY": 200.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa");
let promise = store.update(valueBucket, predicates);
promise.then(async (rows) => {
  console.info(`Updated row count: ${rows}`);
}).catch((err) => {
  console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
})
```

### update<sup>10+</sup>

update(values: ValuesBucket, predicates: RdbPredicates, conflict: ConflictResolution):Promise&lt;number&gt;

根据RdbPredicates的指定实例对象更新数据库中的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                        | 必填 | 说明                                                         |
| ---------- | ------------------------------------------- | ---- | ------------------------------------------------------------ |
| values     | [ValuesBucket](#valuesbucket)               | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [RdbPredicates](#rdbpredicates)            | 是   | RdbPredicates的实例对象指定的更新条件。                      |
| conflict   | [ConflictResolution](#conflictresolution10) | 是   | 指定冲突解决方式。                                           |

**返回值**：

| 类型                  | 说明                                      |
| --------------------- | ----------------------------------------- |
| Promise&lt;number&gt; | 指定的Promise回调方法。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const valueBucket = {
  "NAME": "Rose",
  "AGE": 22,
  "SALARY": 200.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa");
let promise = store.update(valueBucket, predicates, relationalStore.ConflictResolution.ON_CONFLICT_REPLACE);
promise.then(async (rows) => {
  console.info(`Updated row count: ${rows}`);
}).catch((err) => {
  console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
})
```

### update

update(table: string, values: ValuesBucket, predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;number&gt;):void

根据DataSharePredicates的指定实例对象更新数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| table      | string                                                       | 是   | 指定的目标表名。                                             |
| values     | [ValuesBucket](#valuesbucket)                                | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的更新条件。                |
| callback   | AsyncCallback&lt;number&gt;                                  | 是   | 指定的callback回调方法。返回受影响的行数。                   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
import dataSharePredicates from '@ohos.data.dataSharePredicates'
const valueBucket = {
    "NAME": "Rose",
    "AGE": 22,
    "SALARY": 200.5,
    "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
store.update("EMPLOYEE", valueBucket, predicates, function (err, rows) {
  if (err) {
    console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Updated row count: ${rows}`);
})
```

### update

update(table: string, values: ValuesBucket, predicates: dataSharePredicates.DataSharePredicates):Promise&lt;number&gt;

根据DataSharePredicates的指定实例对象更新数据库中的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                         |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| table      | string                                                       | 是   | 指定的目标表名。                                             |
| values     | [ValuesBucket](#valuesbucket)                                | 是   | values指示数据库中要更新的数据行。键值对与数据库表的列名相关联。 |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的更新条件。                |

**返回值**：

| 类型                  | 说明                                      |
| --------------------- | ----------------------------------------- |
| Promise&lt;number&gt; | 指定的Promise回调方法。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
import dataSharePredicates from '@ohos.data.dataSharePredicates'
const valueBucket = {
  "NAME": "Rose",
  "AGE": 22,
  "SALARY": 200.5,
  "CODES": new Uint8Array([1, 2, 3, 4, 5]),
};
let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
let promise = store.update("EMPLOYEE", valueBucket, predicates);
promise.then(async (rows) => {
  console.info(`Updated row count: ${rows}`);
}).catch((err) => {
  console.error(`Updated failed, code is ${err.code},message is ${err.message}`);
})
```

### delete

delete(predicates: RdbPredicates, callback: AsyncCallback&lt;number&gt;):void

根据RdbPredicates的指定实例对象从数据库中删除数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                 | 必填 | 说明                                      |
| ---------- | ------------------------------------ | ---- | ----------------------------------------- |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | RdbPredicates的实例对象指定的删除条件。 |
| callback   | AsyncCallback&lt;number&gt;          | 是   | 指定callback回调函数。返回受影响的行数。  |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa");
store.delete(predicates, function (err, rows) {
  if (err) {
    console.error(`Delete failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Delete rows: ${rows}`);
})
```

### delete

delete(predicates: RdbPredicates):Promise&lt;number&gt;

根据RdbPredicates的指定实例对象从数据库中删除数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                 | 必填 | 说明                                      |
| ---------- | ------------------------------------ | ---- | ----------------------------------------- |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | RdbPredicates的实例对象指定的删除条件。 |

**返回值**：

| 类型                  | 说明                            |
| --------------------- | ------------------------------- |
| Promise&lt;number&gt; | Promise对象。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Lisa");
let promise = store.delete(predicates);
promise.then((rows) => {
  console.info(`Delete rows: ${rows}`);
}).catch((err) => {
  console.error(`Delete failed, code is ${err.code},message is ${err.message}`);
})
```

### delete

delete(table: string, predicates: dataSharePredicates.DataSharePredicates, callback: AsyncCallback&lt;number&gt;):void

根据DataSharePredicates的指定实例对象从数据库中删除数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                          |
| ---------- | ------------------------------------------------------------ | ---- | --------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                              |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的删除条件。 |
| callback   | AsyncCallback&lt;number&gt;                                  | 是   | 指定callback回调函数。返回受影响的行数。      |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
import dataSharePredicates from '@ohos.data.dataSharePredicates'
let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
store.delete("EMPLOYEE", predicates, function (err, rows) {
  if (err) {
    console.error(`Delete failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Delete rows: ${rows}`);
})
```

### delete

delete(table: string, predicates: dataSharePredicates.DataSharePredicates):Promise&lt;number&gt;

根据DataSharePredicates的指定实例对象从数据库中删除数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                          |
| ---------- | ------------------------------------------------------------ | ---- | --------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                              |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的删除条件。 |

**返回值**：

| 类型                  | 说明                            |
| --------------------- | ------------------------------- |
| Promise&lt;number&gt; | Promise对象。返回受影响的行数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
import dataSharePredicates from '@ohos.data.dataSharePredicates'
let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Lisa");
let promise = store.delete("EMPLOYEE", predicates);
promise.then((rows) => {
  console.info(`Delete rows: ${rows}`);
}).catch((err) => {
  console.error(`Delete failed, code is ${err.code},message is ${err.message}`);
})
```

### query

query(predicates: RdbPredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定条件查询数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------------- |
| predicates | [RdbPredicates](#rdbpredicates)                         | 是   | RdbPredicates的实例对象指定的查询条件。                   |
| columns    | Array&lt;string&gt;                                          | 是   | 表示要查询的列。如果值为空，则查询应用于所有列。            |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Rose");
store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"], function (err, resultSet) {
  if (err) {
    console.error(`Query failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
})
```

### query

query(predicates: RdbPredicates, columns?: Array&lt;string&gt;):Promise&lt;ResultSet&gt;

根据指定条件查询数据库中的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                 | 必填 | 说明                                             |
| ---------- | ------------------------------------ | ---- | ------------------------------------------------ |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | RdbPredicates的实例对象指定的查询条件。        |
| columns    | Array&lt;string&gt;                  | 否   | 表示要查询的列。如果值为空，则查询应用于所有列。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**返回值**：

| 类型                                                    | 说明                                               |
| ------------------------------------------------------- | -------------------------------------------------- |
| Promise&lt;[ResultSet](#resultset)&gt; | Promise对象。如果操作成功，则返回ResultSet对象。 |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("NAME", "Rose");
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
}).catch((err) => {
  console.error(`Query failed, code is ${err.code},message is ${err.message}`);
})
  ```

### query

query(table: string, predicates: dataSharePredicates.DataSharePredicates, columns: Array&lt;string&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定条件查询数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                                        |
| ---------- | ------------------------------------------------------------ | ---- | ----------------------------------------------------------- |
| table      | string                                                       | 是   | 指定的目标表名。                                            |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的查询条件。               |
| columns    | Array&lt;string&gt;                                          | 是   | 表示要查询的列。如果值为空，则查询应用于所有列。            |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import dataSharePredicates from '@ohos.data.dataSharePredicates'
let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Rose");
store.query("EMPLOYEE", predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"], function (err, resultSet) {
  if (err) {
    console.error(`Query failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
})
```

### query

query(table: string, predicates: dataSharePredicates.DataSharePredicates, columns?: Array&lt;string&gt;):Promise&lt;ResultSet&gt;

根据指定条件查询数据库中的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**模型约束：** 此接口仅可在Stage模型下可用。

**系统接口：** 此接口为系统接口。

**参数：**

| 参数名     | 类型                                                         | 必填 | 说明                                             |
| ---------- | ------------------------------------------------------------ | ---- | ------------------------------------------------ |
| table      | string                                                       | 是   | 指定的目标表名。                                 |
| predicates | [dataSharePredicates.DataSharePredicates](js-apis-data-dataSharePredicates.md#datasharepredicates) | 是   | DataSharePredicates的实例对象指定的查询条件。    |
| columns    | Array&lt;string&gt;                                          | 否   | 表示要查询的列。如果值为空，则查询应用于所有列。 |

**返回值**：

| 类型                                                    | 说明                                               |
| ------------------------------------------------------- | -------------------------------------------------- |
| Promise&lt;[ResultSet](#resultset)&gt; | Promise对象。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import dataSharePredicates from '@ohos.data.dataSharePredicates'
let predicates = new dataSharePredicates.DataSharePredicates();
predicates.equalTo("NAME", "Rose");
let promise = store.query("EMPLOYEE", predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
}).catch((err) => {
  console.error(`Query failed, code is ${err.code},message is ${err.message}`);
})
```

### remoteQuery

remoteQuery(device: string, table: string, predicates: RdbPredicates, columns: Array&lt;string&gt; , callback: AsyncCallback&lt;ResultSet&gt;): void

根据指定条件查询远程设备数据库中的数据。使用callback异步回调。

> **说明：**
>
> 其中device通过调用[deviceManager.getTrustedDeviceListSync](js-apis-device-manager.md#gettrusteddevicelistsync)方法得到。deviceManager模块的接口均为系统接口，仅系统应用可用。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                         | 必填 | 说明                                                      |
| ---------- | -------------------------------------------- | ---- | --------------------------------------------------------- |
| device     | string                                       | 是   | 指定的远程设备ID。                                        |
| table      | string                                       | 是   | 指定的目标表名。                                          |
| predicates | [RdbPredicates](#rdbpredicates)              | 是   | RdbPredicates的实例对象，指定查询的条件。                 |
| columns    | Array&lt;string&gt;                          | 是   | 表示要查询的列。如果值为空，则查询应用于所有列。          |
| callback   | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceId = null;

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    deviceId = devices[0].deviceId;
})

let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
predicates.greaterThan("id", 0);
store.remoteQuery(deviceId, "EMPLOYEE", predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"],
  function(err, resultSet) {
    if (err) {
      console.error(`Failed to remoteQuery, code is ${err.code},message is ${err.message}`);
      return;
    }
    console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
    // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
    while(resultSet.goToNextRow()) {
      const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
      const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
      const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
      const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
      console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
    }
    // 释放数据集的内存
    resultSet.close();
  }
)
```

### remoteQuery

remoteQuery(device: string, table: string, predicates: RdbPredicates, columns: Array&lt;string&gt;): Promise&lt;ResultSet&gt;

根据指定条件查询远程设备数据库中的数据。使用Promise异步回调。

> **说明：**
>
> 其中device通过调用[deviceManager.getTrustedDeviceListSync](js-apis-device-manager.md#gettrusteddevicelistsync)方法得到。deviceManager模块的接口均为系统接口，仅系统应用可用。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                 | 必填 | 说明                                             |
| ---------- | ------------------------------------ | ---- | ------------------------------------------------ |
| device     | string                               | 是   | 指定的远程设备ID。                   |
| table      | string                               | 是   | 指定的目标表名。                                 |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | RdbPredicates的实例对象，指定查询的条件。      |
| columns    | Array&lt;string&gt;                  | 是   | 表示要查询的列。如果值为空，则查询应用于所有列。 |

**返回值**：

| 类型                                                         | 说明                                               |
| ------------------------------------------------------------ | -------------------------------------------------- |
| Promise&lt;[ResultSet](#resultset)&gt; | Promise对象。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceId = null;

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    deviceId = devices[0].deviceId;
})

let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
predicates.greaterThan("id", 0);
let promise = store.remoteQuery(deviceId, "EMPLOYEE", predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
}).catch((err) => {
  console.error(`Failed to remoteQuery, code is ${err.code},message is ${err.message}`);
})
```

### querySql<sup>10+</sup>

querySql(sql: string, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定SQL语句查询数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                                         |
| -------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| sql      | string                                       | 是   | 指定要执行的SQL语句。                                        |
| callback | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。    |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
store.querySql("SELECT * FROM EMPLOYEE CROSS JOIN BOOK WHERE BOOK.NAME = 'sanguo'", function (err, resultSet) {
  if (err) {
    console.error(`Query failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
})
```

### querySql

querySql(sql: string, bindArgs: Array&lt;ValueType&gt;, callback: AsyncCallback&lt;ResultSet&gt;):void

根据指定SQL语句查询数据库中的数据，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                         | 必填 | 说明                                                         |
| -------- | -------------------------------------------- | ---- | ------------------------------------------------------------ |
| sql      | string                                       | 是   | 指定要执行的SQL语句。                                        |
| bindArgs | Array&lt;[ValueType](#valuetype)&gt;         | 是   | SQL语句中参数的值。该值与sql参数语句中的占位符相对应。当sql参数语句完整时，该参数需为空数组。 |
| callback | AsyncCallback&lt;[ResultSet](#resultset)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ResultSet对象。    |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
store.querySql("SELECT * FROM EMPLOYEE CROSS JOIN BOOK WHERE BOOK.NAME = ?", ['sanguo'], function (err, resultSet) {
  if (err) {
    console.error(`Query failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
})
```

### querySql

querySql(sql: string, bindArgs?: Array&lt;ValueType&gt;):Promise&lt;ResultSet&gt;

根据指定SQL语句查询数据库中的数据，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                 | 必填 | 说明                                                         |
| -------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| sql      | string                               | 是   | 指定要执行的SQL语句。                                        |
| bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 否   | SQL语句中参数的值。该值与sql参数语句中的占位符相对应。当sql参数语句完整时，该参数不填。 |

**返回值**：

| 类型                                                    | 说明                                               |
| ------------------------------------------------------- | -------------------------------------------------- |
| Promise&lt;[ResultSet](#resultset)&gt; | Promise对象。如果操作成功，则返回ResultSet对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
let promise = store.querySql("SELECT * FROM EMPLOYEE CROSS JOIN BOOK WHERE BOOK.NAME = 'sanguo'");
promise.then((resultSet) => {
  console.info(`ResultSet column names: ${resultSet.columnNames}, column count: ${resultSet.columnCount}`);
  // resultSet是一个数据集合的游标，默认指向第-1个记录，有效的数据从0开始。
  while(resultSet.goToNextRow()) {
    const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
    const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
    const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
    const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
    console.info(`id=${id}, name=${name}, age=${age}, salary=${salary}`);
  }
  // 释放数据集的内存
  resultSet.close();
}).catch((err) => {
  console.error(`Query failed, code is ${err.code},message is ${err.message}`);
})
```

### executeSql<sup>10+</sup>

executeSql(sql: string, callback: AsyncCallback&lt;void&gt;):void

执行包含指定参数但不返回值的SQL语句，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                 | 必填 | 说明                                                         |
| -------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| sql      | string                               | 是   | 指定要执行的SQL语句。                                        |
| callback | AsyncCallback&lt;void&gt;            | 是   | 指定callback回调函数。                                       |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const SQL_DELETE_TABLE = "DELETE FROM test WHERE name = 'zhangsan'"
store.executeSql(SQL_DELETE_TABLE, function(err) {
  if (err) {
    console.error(`ExecuteSql failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Delete table done.`);
})
```

### executeSql

executeSql(sql: string, bindArgs: Array&lt;ValueType&gt;, callback: AsyncCallback&lt;void&gt;):void

执行包含指定参数但不返回值的SQL语句，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                 | 必填 | 说明                                                         |
| -------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| sql      | string                               | 是   | 指定要执行的SQL语句。                                        |
| bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 是   | SQL语句中参数的值。该值与sql参数语句中的占位符相对应。当sql参数语句完整时，该参数需为空数组。 |
| callback | AsyncCallback&lt;void&gt;            | 是   | 指定callback回调函数。                                       |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const SQL_DELETE_TABLE = "DELETE FROM test WHERE name = ?"
store.executeSql(SQL_DELETE_TABLE, ['zhangsan'], function(err) {
  if (err) {
    console.error(`ExecuteSql failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Delete table done.`);
})
```

### executeSql

executeSql(sql: string, bindArgs?: Array&lt;ValueType&gt;):Promise&lt;void&gt;

执行包含指定参数但不返回值的SQL语句，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                 | 必填 | 说明                                                         |
| -------- | ------------------------------------ | ---- | ------------------------------------------------------------ |
| sql      | string                               | 是   | 指定要执行的SQL语句。                                        |
| bindArgs | Array&lt;[ValueType](#valuetype)&gt; | 否   | SQL语句中参数的值。该值与sql参数语句中的占位符相对应。当sql参数语句完整时，该参数不填。 |

**返回值**：

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
const SQL_DELETE_TABLE = "DELETE FROM test WHERE name = 'zhangsan'"
let promise = store.executeSql(SQL_DELETE_TABLE);
promise.then(() => {
    console.info(`Delete table done.`);
}).catch((err) => {
    console.error(`ExecuteSql failed, code is ${err.code},message is ${err.message}`);
})
```

### getModifyTime<sup>10+</sup>

getModifyTime(table: string, columnName: string, primaryKeys: PRIKeyType[], callback: AsyncCallback&lt;ModifyTime&gt;): void

获取数据库表中数据的最后修改时间，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型                                             | 必填 | 说明                                                         |
| ----------- | ------------------------------------------------ | ---- | ------------------------------------------------------------ |
| table       | string                                           | 是   | 指定要查询的数据库表的表名。                                 |
| columnName  | string                                           | 是   | 指定要查询的数据库表的列名。                                 |
| primaryKeys | [PRIKeyType](#prikeytype10)[]                    | 是   | 指定要查询的行的主键。<br>如果数据库表无主键，参数columnName需传入"rowid"，此时primaryKeys为要查询的数据库表的行号。<br>如果数据库表无主键，参数columnName传入不为"rowid"，返回对应的错误码。 |
| callback    | AsyncCallback&lt;[ModifyTime](#modifytime10)&gt; | 是   | 指定callback回调函数。如果操作成功，则返回ModifyTime对象，表示数据的最后修改时间。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息** |
| ------------ | ------------ |
| 14800000     | Inner error. |

**示例：**

```js
let PRIKey = [1, 4, 2, 3];
store.getModifyTime("cloud_tasks", "uuid", PRIKey, function (err, modifyTime) {
    if (err) {
        console.error(`getModifyTime failed, code is ${err.code},message is ${err.message}`);
        return;
    }
    let size = modifyTime.size();
});
```

### getModifyTime<sup>10+</sup>

getModifyTime(table: string, columnName: string, primaryKeys: PRIKeyType[]): Promise&lt;ModifyTime&gt;

获取数据库表中数据的最后修改时间，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型                          | 必填 | 说明                                                         |
| ----------- | ----------------------------- | ---- | ------------------------------------------------------------ |
| table       | string                        | 是   | 指定要查询的数据库表的表名。                                 |
| columnName  | string                        | 是   | 指定要查询的数据库表的列名。                                 |
| primaryKeys | [PRIKeyType](#prikeytype10)[] | 是   | 指定要查询的行的主键。<br>如果数据库表无主键，参数columnName需传入"rowid"，此时primaryKeys为要查询的数据库表的行号。<br>如果数据库表无主键，参数columnName传入不为"rowid"，返回对应的错误码。 |

**返回值**：

| 类型                                       | 说明                                                      |
| ------------------------------------------ | --------------------------------------------------------- |
| Promise&lt;[ModifyTime](#modifytime10)&gt; | 返回ModifyTime类型的Promise对象，表示数据最后的修改时间。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息** |
| ------------ | ------------ |
| 14800000     | Inner error. |

**示例：**

```js
let PRIKey = [1, 2, 3];
store.getModifyTime("cloud_tasks", "uuid", PRIKey).then((modifyTime) => {
    let size = modifyTime.size();
}).catch((err) => {
    console.error(`getModifyTime failed, code is ${err.code},message is ${err.message}`);
});
```

### beginTransaction

beginTransaction():void

在开始执行SQL语句之前，开始事务。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                 |
| ------------ | -------------------------------------------- |
| 14800047     | The WAL file size exceeds the default limit. |
| 14800000     | Inner error.                                 |

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility'
let context = featureAbility.getContext();
const STORE_CONFIG = { 
  name: "RdbTest.db",
  securityLevel: relationalStore.SecurityLevel.S1
};
relationalStore.getRdbStore(context, STORE_CONFIG, async function (err, store) {
  if (err) {
    console.error(`GetRdbStore failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  store.beginTransaction();
  const valueBucket = {
    "name": "lisi",
	"age": 18,
	"salary": 100.5,
	"blobType": new Uint8Array([1, 2, 3]),
  };
  await store.insert("test", valueBucket);
  store.commit();
})
```

### commit

commit():void

提交已执行的SQL语句。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility'
let context = featureAbility.getContext();
const STORE_CONFIG = { 
  name: "RdbTest.db",
  securityLevel: relationalStore.SecurityLevel.S1
};
relationalStore.getRdbStore(context, STORE_CONFIG, async function (err, store) {
  if (err) {
     console.error(`GetRdbStore failed, code is ${err.code},message is ${err.message}`);
     return;
  }
  store.beginTransaction();
  const valueBucket = {
	"name": "lisi",
	"age": 18,
	"salary": 100.5,
	"blobType": new Uint8Array([1, 2, 3]),
  };
  await store.insert("test", valueBucket);
  store.commit();
})
```

### rollBack

rollBack():void

回滚已经执行的SQL语句。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**示例：**

```js
import featureAbility from '@ohos.ability.featureAbility'
let context = featureAbility.getContext();
const STORE_CONFIG = { 
  name: "RdbTest.db",
  securityLevel: relationalStore.SecurityLevel.S1
};
relationalStore.getRdbStore(context, STORE_CONFIG, async function (err, store) {
  if (err) {
    console.error(`GetRdbStore failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  try {
    store.beginTransaction()
    const valueBucket = {
	  "id": 1,
	  "name": "lisi",
	  "age": 18,
	  "salary": 100.5,
	  "blobType": new Uint8Array([1, 2, 3]),
	};
	await store.insert("test", valueBucket);
    store.commit();
  } catch (err) {
    console.error(`Transaction failed, code is ${err.code},message is ${err.message}`);
    store.rollBack();
  }
})
```

### backup

backup(destName:string, callback: AsyncCallback&lt;void&gt;):void

以指定名称备份数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                     |
| -------- | ------------------------- | ---- | ------------------------ |
| destName | string                    | 是   | 指定数据库的备份文件名。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 指定callback回调函数。   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
store.backup("dbBackup.db", function(err) {
  if (err) {
    console.error(`Backup failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Backup success.`);
})
```

### backup

backup(destName:string): Promise&lt;void&gt;

以指定名称备份数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型   | 必填 | 说明                     |
| -------- | ------ | ---- | ------------------------ |
| destName | string | 是   | 指定数据库的备份文件名。 |

**返回值**：

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
let promiseBackup = store.backup("dbBackup.db");
promiseBackup.then(()=>{
  console.info(`Backup success.`);
}).catch((err)=>{
  console.error(`Backup failed, code is ${err.code},message is ${err.message}`);
})
```

### restore

restore(srcName:string, callback: AsyncCallback&lt;void&gt;):void

从指定的数据库备份文件恢复数据库，使用callback异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                     |
| -------- | ------------------------- | ---- | ------------------------ |
| srcName  | string                    | 是   | 指定数据库的备份文件名。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 指定callback回调函数。   |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
store.restore("dbBackup.db", function(err) {
  if (err) {
    console.error(`Restore failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Restore success.`);
})
```

### restore

restore(srcName:string): Promise&lt;void&gt;

从指定的数据库备份文件恢复数据库，使用Promise异步回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名  | 类型   | 必填 | 说明                     |
| ------- | ------ | ---- | ------------------------ |
| srcName | string | 是   | 指定数据库的备份文件名。 |

**返回值**：

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
let promiseRestore = store.restore("dbBackup.db");
promiseRestore.then(()=>{
  console.info(`Restore success.`);
}).catch((err)=>{
  console.error(`Restore failed, code is ${err.code},message is ${err.message}`);
})
```

### setDistributedTables

setDistributedTables(tables: Array&lt;string&gt;, callback: AsyncCallback&lt;void&gt;): void

设置分布式数据库表，使用callback异步回调。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                      | 必填 | 说明                   |
| -------- | ------------------------- | ---- | ---------------------- |
| tables   | Array&lt;string&gt;       | 是   | 要设置的分布式数据库表表名。 |
| callback | AsyncCallback&lt;void&gt; | 是   | 指定callback回调函数。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
store.setDistributedTables(["EMPLOYEE"], function (err) {
  if (err) {
    console.error(`SetDistributedTables failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`SetDistributedTables successfully.`);
})
```

### setDistributedTables

 setDistributedTables(tables: Array&lt;string&gt;): Promise&lt;void&gt;

设置分布式数据库表，使用Promise异步回调。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                     | 必填 | 说明                     |
| ------ | ------------------------ | ---- | ------------------------ |
| tables | ArrayArray&lt;string&gt; | 是   | 要设置的分布式数据库表表名。 |

**返回值**：

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息** |
| ------------ | ------------ |
| 14800000     | Inner error. |

**示例：**

```js
let promise = store.setDistributedTables(["EMPLOYEE"]);
promise.then(() => {
  console.info(`SetDistributedTables successfully.`);
}).catch((err) => {
  console.error(`SetDistributedTables failed, code is ${err.code},message is ${err.message}`);
})
```

### setDistributedTables<sup>10+</sup>

setDistributedTables(tables: Array&lt;string&gt;, type: number, config: DistributedConfig, callback: AsyncCallback&lt;void&gt;): void

设置分布式数据库表，使用callback异步回调。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型                                  | 必填  | 说明              |
| -------- | ----------------------------------- | --- | --------------- |
| tables   | Array&lt;string&gt;                 | 是   | 要设置的分布式数据库表表名。     |
| type     | number | 是   | 表的分布式类型。目前支持的入参值为: relationalStore.DistributedType.DISTRIBUTED_DEVICE、relationalStore.DistributedType.DISTRIBUTED_CLOUD。<br> 当type为relationalStore.DistributedType.DISTRIBUTED_DEVICE时，表示表在不同设备之间分布式。<br> 当type为relationalStore.DistributedType.DISTRIBUTED_CLOUD时，表示表在设备和云端之间分布式。 |
| config | [DistributedConfig](#distributedconfig10) | 是 | 表的分布式配置信息。 |
| callback | AsyncCallback&lt;void&gt;           | 是   | 指定callback回调函数。 |

**示例：**

```js
let config = new relationalStore.DistributedConfig();
config.autoSync = true;
store.setDistributedTables(["EMPLOYEE"], relationalStore.DistributedType.DISTRIBUTED_CLOUD, config, function (err) {
  if (err) {
    console.error(`SetDistributedTables failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`SetDistributedTables successfully.`);
})
```

### setDistributedTables<sup>10+</sup>

 setDistributedTables(tables: Array&lt;string>, type?: number, config?: DistributedConfig): Promise&lt;void>

设置分布式数据库表，使用Promise异步回调。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型                                      | 必填 | 说明                                                         |
| ------ | ----------------------------------------- | ---- | ------------------------------------------------------------ |
| tables | Array&lt;string&gt;                       | 是   | 要设置的分布式数据库表表名。                                     |
| type   | number                                    | 否   | 表的分布式类型。默认值是relationalStore.DistributedType.DISTRIBUTED_DEVICE。<br> 目前支持的入参值为: relationalStore.DistributedType.DISTRIBUTED_DEVICE、relationalStore.DistributedType.DISTRIBUTED_CLOUD。<br/> 当type为relationalStore.DistributedType.DISTRIBUTED_DEVICE时，表示表在不同设备之间分布式。<br/> 当type为relationalStore.DistributedType.DISTRIBUTED_CLOUD时，表示表在设备和云端之间分布式。 |
| config | [DistributedConfig](#distributedconfig10) | 否   | 表的分布式配置信息。不传入时默认autoSync为false，即只支持手动同步。 |

**返回值**：

| 类型                | 说明                      |
| ------------------- | ------------------------- |
| Promise&lt;void&gt; | 无返回结果的Promise对象。 |

**示例：**

```js
let config = new relationalStore.DistributedConfig();
config.autoSync = true;
let promise = store.setDistributedTables(["EMPLOYEE"], relationalStore.DistributedType.DISTRIBUTED_CLOUD, config);
promise.then(() => {
  console.info(`SetDistributedTables successfully.`);
}).catch((err) => {
  console.error(`SetDistributedTables failed, code is ${err.code},message is ${err.message}`);
})
```

### obtainDistributedTableName

obtainDistributedTableName(device: string, table: string, callback: AsyncCallback&lt;string&gt;): void

根据远程设备的本地表名获取指定远程设备的分布式表名。在查询远程设备数据库时，需要使用分布式表名, 使用callback异步回调。

> **说明：**
>
> 其中device通过调用[deviceManager.getTrustedDeviceListSync](js-apis-device-manager.md#gettrusteddevicelistsync)方法得到。deviceManager模块的接口均为系统接口，仅系统应用可用。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                        | 必填 | 说明                                                         |
| -------- | --------------------------- | ---- | ------------------------------------------------------------ |
| device   | string                      | 是   | 远程设备ID 。                                                |
| table    | string                      | 是   | 远程设备的本地表名。                                         |
| callback | AsyncCallback&lt;string&gt; | 是   | 指定的callback回调函数。如果操作成功，返回远程设备的分布式表名。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceId = null;

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    deviceId = devices[0].deviceId;
})

store.obtainDistributedTableName(deviceId, "EMPLOYEE", function (err, tableName) {
    if (err) {
        console.error(`ObtainDistributedTableName failed, code is ${err.code},message is ${err.message}`);
        return;
    }
    console.info(`ObtainDistributedTableName successfully, tableName= ${tableName}`);
})
```

### obtainDistributedTableName

 obtainDistributedTableName(device: string, table: string): Promise&lt;string&gt;

根据远程设备的本地表名获取指定远程设备的分布式表名。在查询远程设备数据库时，需要使用分布式表名，使用Promise异步回调。

> **说明：**
>
> 其中device通过调用[deviceManager.getTrustedDeviceListSync](js-apis-device-manager.md#gettrusteddevicelistsync)方法得到。deviceManager模块的接口均为系统接口，仅系统应用可用。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                 |
| ------ | ------ | ---- | -------------------- |
| device | string | 是   | 远程设备ID。         |
| table  | string | 是   | 远程设备的本地表名。 |

**返回值**：

| 类型                  | 说明                                                  |
| --------------------- | ----------------------------------------------------- |
| Promise&lt;string&gt; | Promise对象。如果操作成功，返回远程设备的分布式表名。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceId = null;

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    deviceId = devices[0].deviceId;
})

let promise = store.obtainDistributedTableName(deviceId, "EMPLOYEE");
promise.then((tableName) => {
  console.info(`ObtainDistributedTableName successfully, tableName= ${tableName}`);
}).catch((err) => {
  console.error(`ObtainDistributedTableName failed, code is ${err.code},message is ${err.message}`);
})
```

### sync

sync(mode: SyncMode, predicates: RdbPredicates, callback: AsyncCallback&lt;Array&lt;[string, number]&gt;&gt;): void

在设备之间同步数据, 使用callback异步回调。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                               | 必填 | 说明                                                         |
| ---------- | -------------------------------------------------- | ---- | ------------------------------------------------------------ |
| mode       | [SyncMode](#syncmode)                             | 是   | 指同步模式。该值可以是relationalStore.SyncMode.SYNC_MODE_PUSH、relationalStore.SyncMode.SYNC_MODE_PULL。                               |
| predicates | [RdbPredicates](#rdbpredicates)               | 是   | 约束同步数据和设备。                                         |
| callback   | AsyncCallback&lt;Array&lt;[string, number]&gt;&gt; | 是   | 指定的callback回调函数，用于向调用者发送同步结果。string：设备ID；number：每个设备同步状态，0表示成功，其他值表示失败。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceIds = [];

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    for (var i = 0; i < devices.length; i++) {
        deviceIds[i] = devices[i].deviceId;
    }
})

let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
predicates.inDevices(deviceIds);
store.sync(relationalStore.SyncMode.SYNC_MODE_PUSH, predicates, function (err, result) {
  if (err) {
    console.error(`Sync failed, code is ${err.code},message is ${err.message}`);
    return;
  }
  console.info(`Sync done.`);
  for (let i = 0; i < result.length; i++) {
    console.info(`device= ${result[i][0]}, status= ${result[i][1]}`);
  }
})
```

### sync

 sync(mode: SyncMode, predicates: RdbPredicates): Promise&lt;Array&lt;[string, number]&gt;&gt;

在设备之间同步数据，使用Promise异步回调。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型                                 | 必填 | 说明                           |
| ---------- | ------------------------------------ | ---- | ------------------------------ |
| mode       | [SyncMode](#syncmode)               | 是   | 指同步模式。该值可以是relationalStore.SyncMode.SYNC_MODE_PUSH、relationalStore.SyncMode.SYNC_MODE_PULL。 |
| predicates | [RdbPredicates](#rdbpredicates) | 是   | 约束同步数据和设备。           |

**返回值**：

| 类型                                         | 说明                                                         |
| -------------------------------------------- | ------------------------------------------------------------ |
| Promise&lt;Array&lt;[string, number]&gt;&gt; | Promise对象，用于向调用者发送同步结果。string：设备ID；number：每个设备同步状态，0表示成功，其他值表示失败。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                 |
| ------------ | ---------------------------- |
| 14800000     | Inner error.                 |

**示例：**

```js
import deviceManager from '@ohos.distributedHardware.deviceManager';
let dmInstance = null;
let deviceIds = [];

deviceManager.createDeviceManager("com.example.appdatamgrverify", (err, manager) => {
    if (err) {
        console.log("create device manager failed, err=" + err);
        return;
    }
    dmInstance = manager;
    let devices = dmInstance.getTrustedDeviceListSync();
    for (var i = 0; i < devices.length; i++) {
        deviceIds[i] = devices[i].deviceId;
    }
})

let predicates = new relationalStore.RdbPredicates('EMPLOYEE');
predicates.inDevices(deviceIds);
let promise = store.sync(relationalStore.SyncMode.SYNC_MODE_PUSH, predicates);
promise.then((result) =>{
  console.info(`Sync done.`);
  for (let i = 0; i < result.length; i++) {
    console.info(`device= ${result[i][0]}, status= ${result[i][1]}`);
  }
}).catch((err) => {
  console.error(`Sync failed, code is ${err.code},message is ${err.message}`);
})
```

### cloudSync<sup>10+</sup>

cloudSync(mode: SyncMode, progress: Callback&lt;ProgressDetails&gt;, callback: AsyncCallback&lt;void&gt;): void

手动执行对所有分布式表的端云同步，使用callback异步回调。使用该接口需要实现云服务功能。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                               |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------------------- |
| mode     | [SyncMode](#syncmode)                                 | 是   | 表示数据库的同步模式。                             |
| progress | Callback&lt;[ProgressDetails](#progressdetails10)&gt; | 是   | 用来处理数据库同步详细信息的回调函数。             |
| callback | AsyncCallback&lt;void&gt;                             | 是   | 指定的callback回调函数，用于向调用者发送同步结果。 |

**示例：**

```js
relationalStore.cloudSync(relationalStore.SyncMode.SYNC_MODE_CLOUD_FIRST, function (progressDetails) {
    console.info(`Progess: ${progressDetails}`);
}, function (err) {
     if (err) {
         console.error(`Cloud sync failed, code is ${err.code},message is ${err.message}`);
         return;
     }
     console.info('Cloud sync succeeded');
});
```

### cloudSync<sup>10+</sup>

cloudSync(mode: SyncMode, progress: Callback&lt;ProgressDetails&gt;): Promise&lt;void&gt;

手动执行对所有分布式表的端云同步，使用Promise异步回调。使用该接口需要实现云服务功能。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                   |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| mode     | [SyncMode](#syncmode)                                 | 是   | 表示数据库的同步模式。                 |
| progress | Callback&lt;[ProgressDetails](#progressdetails10)&gt; | 是   | 用来处理数据库同步详细信息的回调函数。 |

**返回值**：

| 类型                | 说明                                    |
| ------------------- | --------------------------------------- |
| Promise&lt;void&gt; | Promise对象，用于向调用者发送同步结果。 |

**示例：**

```js
function progress(progressDetail) {
    console.info(`progress: ${progressDetail}`);
}

relationalStore.cloudSync(relationalStore.SyncMode.SYNC_MODE_CLOUD_FIRST, progress).then(() => {
    console.info('Cloud sync succeeded');
}).catch((err) => {
    console.error(`cloudSync failed, code is ${err.code},message is ${err.message}`);
});
```

### cloudSync<sup>10+</sup>

cloudSync(mode: SyncMode, tables: string[], progress: Callback&lt;ProgressDetails&gt;, callback: AsyncCallback&lt;void&gt;): void

手动执行对指定表的端云同步，使用callback异步回调。使用该接口需要实现云服务功能。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                               |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------------------- |
| mode     | [SyncMode](#syncmode)                                 | 是   | 表示数据库的同步模式。                             |
| tables   | string[]                                              | 是   | 指定同步的表名。                                   |
| progress | Callback&lt;[ProgressDetails](#progressdetails10)&gt; | 是   | 用来处理数据库同步详细信息的回调函数。             |
| callback | AsyncCallback&lt;void&gt;                             | 是   | 指定的callback回调函数，用于向调用者发送同步结果。 |

**示例：**

```js
const tables = ["table1", "table2"];
relationalStore.cloudSync(relationalStore.SyncMode.SYNC_MODE_CLOUD_FIRST, tables, function (progressDetails) {
    console.info(`Progess: ${progressDetails}`);
}, function (err) {
     if (err) {
         console.error(`Cloud sync failed, code is ${err.code},message is ${err.message}`);
         return;
     }
     console.info('Cloud sync succeeded');
});
```

### cloudSync<sup>10+</sup>

cloudSync(mode: SyncMode, tables: string[], progress: Callback&lt;ProgressDetails&gt;): Promise&lt;void&gt;

手动执行对指定表的端云同步，使用Promise异步回调。使用该接口需要实现云服务功能。

**需要权限：** ohos.permission.DISTRIBUTED_DATASYNC

**系统能力：** SystemCapability.DistributedDataManager.CloudSync.Client

**参数：**

| 参数名   | 类型                                                  | 必填 | 说明                                   |
| -------- | ----------------------------------------------------- | ---- | -------------------------------------- |
| mode     | [SyncMode](#syncmode)                                 | 是   | 表示数据库的同步模式。                 |
| tables   | string[]                                              | 是   | 指定同步的表名。                       |
| progress | Callback&lt;[ProgressDetails](#progressdetails10)&gt; | 是   | 用来处理数据库同步详细信息的回调函数。 |

**返回值**：

| 类型                | 说明                                    |
| ------------------- | --------------------------------------- |
| Promise&lt;void&gt; | Promise对象，用于向调用者发送同步结果。 |

**示例：**

```js
const tables = ["table1", "table2"];
function progress(progressDetail) {
    console.info(`progress: ${progressDetail}`);
}

relationalStore.cloudSync(relationalStore.SyncMode.SYNC_MODE_CLOUD_FIRST, tables, progress).then(() => {
    console.info('Cloud sync succeeded');
}).catch((err) => {
    console.error(`cloudSync failed, code is ${err.code},message is ${err.message}`);
});
```

### on('dataChange')

on(event: 'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;): void

注册数据库的数据变更的事件监听。当分布式数据库中的数据发生更改时，将调用回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| event    | string                                                       | 是   | 取值为'dataChange'，表示数据更改。                           |
| type     | [SubscribeType](#subscribetype) | 是   | 订阅类型。                                                   |
| observer | Callback&lt;Array&lt;string&gt;&gt;                          | 是   | 指分布式数据库中数据更改事件的观察者。Array&lt;string&gt;为数据库中的数据发生改变的对端设备ID。 |

**示例：**

```js
function storeObserver(devices) {
  for (let i = 0; i < devices.length; i++) {
    console.info(`device= ${devices[i]} data changed`);
  }
}
try {
  store.on('dataChange', relationalStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver);
} catch (err) {
  console.error(`Register observer failed, code is ${err.code},message is ${err.message}`);
}
```

### on('dataChange')<sup>10+</sup>

on(event: 'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;\| Callback&lt;Array&lt;ChangeInfo&gt;&gt;): void

注册数据库的数据变更的事件监听。当分布式数据库中的数据发生更改时，将调用回调。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                | 必填 | 说明                                        |
| -------- | ----------------------------------- | ---- | ------------------------------------------- |
| event    | string                              | 是   | 取值为'dataChange'，表示数据更改。          |
| type     | [SubscribeType](#subscribetype)    | 是   | 订阅类型。 |
| observer | Callback&lt;Array&lt;string&gt;&gt; \| Callback&lt;Array&lt;[ChangeInfo](#changeinfo10)&gt;&gt; | 是   | 回调函数。<br>当type为SUBSCRIBE_TYPE_REMOTE，observer类型需为Callback&lt;Array&lt;string&gt;&gt;，其中Array&lt;string&gt;为数据库中的数据发生改变的对端设备ID。<br> 当type为SUBSCRIBE_TYPE_CLOUD，observer类型需为Callback&lt;Array&lt;string&gt;&gt;，其中Array&lt;string&gt;为数据库中的数据发生改变的云端帐号。 <br> 当type为SUBSCRIBE_TYPE_CLOUD_DETAILS，observer类型需为Callback&lt;Array&lt;ChangeInfo&gt;&gt;，其中Array&lt;ChangeInfo&gt;为数据库端云同步过程的详情。 |

**示例：**

```js
function storeObserver(devices) {
  for (let i = 0; i < devices.length; i++) {
    console.info(`device= ${devices[i]} data changed`);
  }
}
try {
  store.on('dataChange', relationalStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver);
} catch (err) {
  console.error(`Register observer failed, code is ${err.code},message is ${err.message}`);
}
```

### off('dataChange')

off(event:'dataChange', type: SubscribeType, observer: Callback&lt;Array&lt;string&gt;&gt;): void

取消数据变更的事件监听。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                                         | 必填 | 说明                                                         |
| -------- | ------------------------------------------------------------ | ---- | ------------------------------------------------------------ |
| event    | string                                                       | 是   | 取值为'dataChange'，表示数据更改。                           |
| type     | [SubscribeType](#subscribetype) | 是   | 订阅类型。                                                   |
| observer | Callback&lt;Array&lt;string&gt;&gt;                          | 是   | 指已注册的数据更改观察者。Array&lt;string&gt;为数据库中的数据发生改变的对端设备ID。 |

**示例：**

```
function storeObserver(devices) {
  for (let i = 0; i < devices.length; i++) {
    console.info(`device= ${devices[i]} data changed`);
  }
}
try {
  store.off('dataChange', relationalStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver);
} catch (err) {
  console.error(`Unregister observer failed, code is ${err.code},message is ${err.message}`);
}
```

### off('dataChange')<sup>10+</sup>

off(event:'dataChange', type: SubscribeType, observer?: Callback&lt;Array&lt;string&gt;&gt;\| Callback&lt;Array&lt;ChangeInfo&gt;&gt;): void

取消数据变更的事件监听。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型                                | 必填 | 说明                                        |
| -------- | ---------------------------------- | ---- | ------------------------------------------ |
| event    | string                              | 是   | 取值为'dataChange'，表示数据更改。          |
| type     | [SubscribeType](#subscribetype)     | 是   | 订阅类型。                                 |
| observer | Callback&lt;Array&lt;string&gt;&gt;\| Callback&lt;Array&lt;[ChangeInfo](#changeinfo10)&gt;&gt; | 否 | 回调函数。<br/>当type为SUBSCRIBE_TYPE_REMOTE，observer类型需为Callback&lt;Array&lt;string&gt;&gt;，其中Array&lt;string&gt;为数据库中的数据发生改变的对端设备ID。<br/> 当type为SUBSCRIBE_TYPE_CLOUD，observer类型需为Callback&lt;Array&lt;string&gt;&gt;，其中Array&lt;string&gt;为数据库中的数据发生改变的云端帐号。 <br/> 当type为SUBSCRIBE_TYPE_CLOUD_DETAILS，observer类型需为Callback&lt;Array&lt;ChangeInfo&gt;&gt;，其中Array&lt;ChangeInfo&gt;为数据库端云同步过程的详情。<br> 当observer没有传入时，表示取消当前type类型下所有数据变更的事件监听。 |

**示例：**

```js
function storeObserver(devices) {
  for (let i = 0; i < devices.length; i++) {
    console.info(`device= ${devices[i]} data changed`);
  }
}
try {
  store.off('dataChange', relationalStore.SubscribeType.SUBSCRIBE_TYPE_REMOTE, storeObserver);
} catch (err) {
  console.error(`Unregister observer failed, code is ${err.code},message is ${err.message}`);
}
```

## ResultSet

提供通过查询数据库生成的数据库结果集的访问方法。结果集是指用户调用关系型数据库查询接口之后返回的结果集合，提供了多种灵活的数据访问方式，以便用户获取各项数据。

### 使用说明

首先需要获取resultSet对象。

```js
let resultSet = null;
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
predicates.equalTo("AGE", 18);
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((result) => {
  resultSet = result;
  console.info(`resultSet columnNames: ${resultSet.columnNames}`);
  console.info(`resultSet columnCount: ${resultSet.columnCount}`);
});
```

### 属性

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

| 名称         | 类型            | 必填 | 说明                             |
| ------------ | ------------------- | ---- | -------------------------------- |
| columnNames  | Array&lt;string&gt; | 是   | 获取结果集中所有列的名称。       |
| columnCount  | number              | 是   | 获取结果集中的列数。             |
| rowCount     | number              | 是   | 获取结果集中的行数。             |
| rowIndex     | number              | 是   | 获取结果集当前行的索引。         |
| isAtFirstRow | boolean             | 是   | 检查结果集是否位于第一行。       |
| isAtLastRow  | boolean             | 是   | 检查结果集是否位于最后一行。     |
| isEnded      | boolean             | 是   | 检查结果集是否位于最后一行之后。 |
| isStarted    | boolean             | 是   | 检查指针是否移动过。             |
| isClosed     | boolean             | 是   | 检查当前结果集是否关闭。         |

### getColumnIndex

getColumnIndex(columnName: string): number

根据指定的列名获取列索引。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名     | 类型   | 必填 | 说明                       |
| ---------- | ------ | ---- | -------------------------- |
| columnName | string | 是   | 表示结果集中指定列的名称。 |

**返回值：**

| 类型   | 说明               |
| ------ | ------------------ |
| number | 返回指定列的索引。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
resultSet.goToFirstRow();
const id = resultSet.getLong(resultSet.getColumnIndex("ID"));
const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
  ```

### getColumnName

getColumnName(columnIndex: number): string

根据指定的列索引获取列名。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明                       |
| ----------- | ------ | ---- | -------------------------- |
| columnIndex | number | 是   | 表示结果集中指定列的索引。 |

**返回值：**

| 类型   | 说明               |
| ------ | ------------------ |
| string | 返回指定列的名称。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
const id = resultSet.getColumnName(0);
const name = resultSet.getColumnName(1);
const age = resultSet.getColumnName(2);
  ```

### goTo

goTo(offset:number): boolean

向前或向后转至结果集的指定行，相对于其当前位置偏移。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名 | 类型   | 必填 | 说明                         |
| ------ | ------ | ---- | ---------------------------- |
| offset | number | 是   | 表示相对于当前位置的偏移量。 |

**返回值：**

| 类型    | 说明                                          |
| ------- | --------------------------------------------- |
| boolean | 如果成功移动结果集，则为true；否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
let promise= store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  resultSet.goTo(1);
  resultSet.close();
}).catch((err) => {
  console.error(`query failed, code is ${err.code},message is ${err.message}`);
});
  ```

### goToRow

goToRow(position: number): boolean

转到结果集的指定行。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名   | 类型   | 必填 | 说明                     |
| -------- | ------ | ---- | ------------------------ |
| position | number | 是   | 表示要移动到的指定位置。 |

**返回值：**

| 类型    | 说明                                          |
| ------- | --------------------------------------------- |
| boolean | 如果成功移动结果集，则为true；否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  resultSet.goToRow(5);
  resultSet.close();
}).catch((err) => {
  console.error(`query failed, code is ${err.code},message is ${err.message}`);
});
  ```

### goToFirstRow

goToFirstRow(): boolean


转到结果集的第一行。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值：**

| 类型    | 说明                                          |
| ------- | --------------------------------------------- |
| boolean | 如果成功移动结果集，则为true；否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  resultSet.goToFirstRow();
  resultSet.close();
}).catch((err) => {
  console.error(`query failed, code is ${err.code},message is ${err.message}`);
});
  ```

### goToLastRow

goToLastRow(): boolean

转到结果集的最后一行。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值：**

| 类型    | 说明                                          |
| ------- | --------------------------------------------- |
| boolean | 如果成功移动结果集，则为true；否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  resultSet.goToLastRow();
  resultSet.close();
}).catch((err) => {
  console.error(`query failed, code is ${err.code},message is ${err.message}`);
});
  ```

### goToNextRow

goToNextRow(): boolean

转到结果集的下一行。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值：**

| 类型    | 说明                                          |
| ------- | --------------------------------------------- |
| boolean | 如果成功移动结果集，则为true；否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  resultSet.goToNextRow();
  resultSet.close();
}).catch((err) => {
  console.error(`query failed, code is ${err.code},message is ${err.message}`);
});
  ```

### goToPreviousRow

goToPreviousRow(): boolean

转到结果集的上一行。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**返回值：**

| 类型    | 说明                                          |
| ------- | --------------------------------------------- |
| boolean | 如果成功移动结果集，则为true；否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |

**示例：**

  ```js
let predicates = new relationalStore.RdbPredicates("EMPLOYEE");
let promise = store.query(predicates, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promise.then((resultSet) => {
  resultSet.goToPreviousRow();
  resultSet.close();
}).catch((err) => {
  console.error(`query failed, code is ${err.code},message is ${err.message}`);
});
  ```

### getBlob

getBlob(columnIndex: number): Uint8Array

以字节数组的形式获取当前行中指定列的值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明                    |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型       | 说明                             |
| ---------- | -------------------------------- |
| Uint8Array | 以字节数组的形式返回指定列的值。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
const codes = resultSet.getBlob(resultSet.getColumnIndex("CODES"));
  ```

### getString

getString(columnIndex: number): string

以字符串形式获取当前行中指定列的值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明                    |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型   | 说明                         |
| ------ | ---------------------------- |
| string | 以字符串形式返回指定列的值。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
const name = resultSet.getString(resultSet.getColumnIndex("NAME"));
  ```

### getLong

getLong(columnIndex: number): number

以Long形式获取当前行中指定列的值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明                    |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| number | 以Long形式返回指定列的值。<br>该接口支持的数据范围是：Number.MIN_SAFE_INTEGER ~ Number.MAX_SAFE_INTEGER，若超出该范围，建议使用[getDouble](#getdouble)。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
const age = resultSet.getLong(resultSet.getColumnIndex("AGE"));
  ```

### getDouble

getDouble(columnIndex: number): number

以double形式获取当前行中指定列的值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明                    |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型   | 说明                         |
| ------ | ---------------------------- |
| number | 以double形式返回指定列的值。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
const salary = resultSet.getDouble(resultSet.getColumnIndex("SALARY"));
  ```

### getAsset<sup>10+</sup>

getAsset(columnIndex: number): Asset

以[Asset](#asset10)形式获取当前行中指定列的值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名         | 类型     | 必填  | 说明           |
| ----------- | ------ | --- | ------------ |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型              | 说明                         |
| --------------- | -------------------------- |
| [Asset](#asset10) | 以Asset形式返回指定列的值。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                     |
| --------- | ------------------------------------------------------------ |
| 14800013  | The column value is null or the column type is incompatible. |

**示例：**

```js
const doc = resultSet.getAsset(resultSet.getColumnIndex("DOC"));
```

### getAssets<sup>10+</sup>

getAssets(columnIndex: number): Assets

以[Assets](#assets10)形式获取当前行中指定列的值。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名         | 类型     | 必填  | 说明           |
| ----------- | ------ | --- | ------------ |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型              | 说明                           |
| ---------------- | ---------------------------- |
| [Assets](#assets10)| 以Assets形式返回指定列的值。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

```js
const docs = resultSet.getAssets(resultSet.getColumnIndex("DOCS"));
```


### isColumnNull

isColumnNull(columnIndex: number): boolean

检查当前行中指定列的值是否为null。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**参数：**

| 参数名      | 类型   | 必填 | 说明                    |
| ----------- | ------ | ---- | ----------------------- |
| columnIndex | number | 是   | 指定的列索引，从0开始。 |

**返回值：**

| 类型    | 说明                                                      |
| ------- | --------------------------------------------------------- |
| boolean | 如果当前行中指定列的值为null，则返回true，否则返回false。 |

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800013     | The column value is null or the column type is incompatible. |

**示例：**

  ```js
const isColumnNull = resultSet.isColumnNull(resultSet.getColumnIndex("CODES"));
  ```

### close

close(): void

关闭结果集。

**系统能力：** SystemCapability.DistributedDataManager.RelationalStore.Core

**示例：**

  ```js
let predicatesClose = new relationalStore.RdbPredicates("EMPLOYEE");
let promiseClose = store.query(predicatesClose, ["ID", "NAME", "AGE", "SALARY", "CODES"]);
promiseClose.then((resultSet) => {
  resultSet.close();
}).catch((err) => {
  console.error(`resultset close failed, code is ${err.code},message is ${err.message}`);
});
  ```

**错误码：**

以下错误码的详细介绍请参见[关系型数据库错误码](../errorcodes/errorcode-data-rdb.md)。

| **错误码ID** | **错误信息**                                                 |
| ------------ | ------------------------------------------------------------ |
| 14800012     | The result set is empty or the specified location is invalid. |
