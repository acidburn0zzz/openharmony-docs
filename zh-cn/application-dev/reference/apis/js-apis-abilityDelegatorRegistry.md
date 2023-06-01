# AbilityDelegatorRegistry

> **说明**
>
> 本模块首批接口从API version 8开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```js
import AbilityDelegatorRegistry from '@ohos.application.abilityDelegatorRegistry'
```



## AbilityLifecycleState

Ability生命周期状态。

**系统能力** ：以下各项对应的系统能力均为SystemCapability.Ability.AbilityRuntime.Core

| 名称          | 值   | 说明                        |
| ------------- | ---- | --------------------------- |
| UNINITIALIZED | 0    | 表示无效状态。              |
| CREATE        | 1    | 表示Ability处于已创建状态。 |
| FOREGROUND    | 2    | 表示Ability处于前台状态。   |
| BACKGROUND    | 3    | 表示Ability处于后台状态。   |
| DESTROY       | 4    | 表示Ability处于已销毁状态。 |



## AbilityDelegatorRegistry.getAbilityDelegator

getAbilityDelegator(): AbilityDelegator

获取应用程序的AbilityDelegator对象

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [AbilityDelegator](js-apis-application-abilityDelegator.md#AbilityDelegator) | [AbilityDelegator](js-apis-application-abilityDelegator.md#AbilityDelegator)对象。可以用来调度测试框架相关功能。 |

**示例：**

```js
var abilityDelegator;

abilityDelegator = AbilityDelegatorRegistry.getAbilityDelegator();
```



## AbilityDelegatorRegistry.getArguments

getArguments(): AbilityDelegatorArgs

获取单元测试参数AbilityDelegatorArgs对象

**系统能力：** SystemCapability.Ability.AbilityRuntime.Core

**返回值：**

| 类型                                                         | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [AbilityDelegatorArgs](js-apis-application-abilityDelegatorArgs.md#AbilityDelegatorArgs) | [AbilityDelegatorArgs](js-apis-application-abilityDelegatorArgs.md#AbilityDelegatorArgs)对象。可以用来获取测试参数。 |

**示例：**

```js
var args = AbilityDelegatorRegistry.getArguments();
console.info("getArguments bundleName:" + args.bundleName);
console.info("getArguments testCaseNames:" + args.testCaseNames);
console.info("getArguments testRunnerClassName:" + args.testRunnerClassName);
```