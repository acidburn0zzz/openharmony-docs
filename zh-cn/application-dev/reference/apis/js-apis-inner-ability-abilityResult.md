# AbilityResult

定义Ability被拉起并退出后返回的结果码和数据，可以通过[startAbilityForResult](js-apis-ability-featureAbility.md#featureabilitystartabilityforresult7)获取被拉起Ability退出后返回的AbilityResult对象，被startAbilityForResult拉起的Ability对象可以通过[terminateSelfWithResult](js-apis-ability-featureAbility.md#featureabilityterminateselfwithresult7)返回AbilityResult对象。

> **说明：**
>
> 本模块首批接口从API version 7开始支持。后续版本的新增接口，采用上角标单独标记接口的起始版本。

## 导入模块

```ts
import ability from '@ohos.ability.ability';
```

## 属性

**系统能力**：以下各项对应的系统能力均为SystemCapability.Ability.AbilityBase

| 名称        |  类型                 | 必填 | 说明                                                         |
| ----------- | -------------------- | ---- | ------------------------------------------------------------ |
| resultCode  | number               | 是   | 表示Ability被拉起并退出后返回的结果码。                                |
| want  | [Want](./js-apis-app-ability-want.md)               | 否   | 表示Ability被拉起并退出后返回的数据。 |

