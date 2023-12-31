# ExtensionAbility组件概述


ExtensionAbility组件是基于特定场景（例如服务卡片、输入法等）提供的应用组件，以便满足更多的使用场景。


每一个具体场景对应一个[ExtensionAbilityType](../reference/apis/js-apis-bundleManager.md#extensionabilitytype)，开发者只能使用（包括实现和访问）系统已定义的类型。各类型的ExtensionAbility组件均由相应的系统服务统一管理，例如InputMethodExtensionAbility组件由输入法管理服务统一管理。

当前系统已定义的ExtensionAbility类型如下表所示。
说明：
- “是否允许三方应用实现”是指：对于一类ExtensionAbility，三方应用能否继承该ExtensionAbility父类实现自己的业务逻辑。
- “是否允许三方应用访问”是指：有些ExtensionAbility会对外提供一些服务，这些ExtensionAbility可能允许三方访问，也可能不允许。“Y”表示允许，“N”表示不允许，“NA”表示不涉及对外服务。

对于系统应用，不受下表约束，允许实现系统已定义的各类ExtensionAbility，也允许访问提供的各类对外服务。

| 已支持ExtensionAbility类型                 | 功能描述 | 是否允许三方应用实现                  | 是否允许三方应用访问                                                 |
| ------------------------ | -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [FormExtensionAbility](../reference/apis/js-apis-app-form-formExtensionAbility.md)                 | FORM类型的ExtensionAbility组件，用于提供服务卡片场景相关能力。      | Y | N |
| [WorkSchedulerExtensionAbility](../reference/apis/js-apis-WorkSchedulerExtensionAbility.md) | WORK_SCHEDULER类型的ExtensionAbility组件，用于提供延迟任务回调实现的能力。      | Y | NA |
| [InputMethodExtensionAbility](../reference/apis/js-apis-inputmethod.md) | INPUT_METHOD类型的ExtensionAbility组件，用于开发输入法应用。      | Y | Y |
|[AccessibilityExtensionAbility](../reference/apis/js-apis-application-accessibilityExtensionAbility.md) | ACCESSIBILITY类型的ExtensionAbility组件，用于提供辅助功能业务的能力。      | Y | NA |
|[ServiceExtensionAbility](../reference/apis/js-apis-app-ability-serviceExtensionAbility.md) | SERVICE类型的ExtensionAbility组件，用于提供后台服务场景相关能力。如果三方开发者想要实现后台处理相关事务的功能，无法使用ServiceExtensionAbility，可以使用后台任务，具体请参见[后台任务](../task-management/background-task-overview.md)。      | N | Y |
|[DataShareExtensionAbility](../reference/apis/js-apis-application-dataShareExtensionAbility.md) | DATA_SHARE类型的ExtensionAbility组件，用于提供支持数据共享业务的能力。      | N | Y |
|[StaticSubscriberExtensionAbility](../reference/apis/js-apis-application-staticSubscriberExtensionAbility.md) | STATIC_SUBSCRIBER类型的ExtensionAbility组件，用于提供静态广播的能力。      | N | NA |
|[WindowExtensionAbility](../reference/apis/js-apis-application-windowExtensionAbility.md) | WINDOW类型的ExtensionAbility组件，用于提供界面组合扩展能力，允许系统应用进行跨应用的界面拉起和嵌入。      | N | NA |
| [EnterpriseAdminExtensionAbility](../reference/apis/js-apis-EnterpriseAdminExtensionAbility.md)            | ENTERPRISE_ADMIN类型的ExtensionAbility组件，用于提供企业管理时处理管理事件的能力，比如设备上应用安装事件、锁屏密码输入错误次数过多事件等。      | N | NA



## 访问指定类型的ExtensionAbility组件

所有类型的ExtensionAbility组件均不能被应用直接启动，而是由相应的系统管理服务拉起，以确保其生命周期受系统管控，使用时拉起，使用完销毁。ExtensionAbility组件的调用方无需关心目标ExtensionAbility组件的生命周期。

  以[InputMethodExtensionAbility](../reference/apis/js-apis-inputmethod.md)组件为例进行说明，如下图所示，调用方应用发起对InputMethodExtensionAbility组件的调用，此时将先调用输入法管理服务，由输入法管理服务拉起[InputMethodExtensionAbility](../reference/apis/js-apis-inputmethod.md)组件，返回给调用方，同时开始管理其生命周期。

**图1** 使用InputMethodExtensionAbility组件
![ExtensionAbility-start](figures/ExtensionAbility-start.png)


## 实现指定类型的ExtensionAbility组件

以实现卡片[FormExtensionAbility](../reference/apis/js-apis-app-form-formExtensionAbility.md)为例进行说明。卡片框架提供了[FormExtensionAbility](../reference/apis/js-apis-app-form-formExtensionAbility.md)基类，开发者通过派生此基类（如MyFormExtensionAbility），实现回调（如创建卡片的onCreate()回调、更新卡片的onUpdateForm()回调等）来实现具体卡片功能，具体见开发指导见[服务卡片FormExtensionAbility](service-widget-overview.md)。

卡片FormExtensionAbility实现方不用关心使用方何时去请求添加、删除卡片，FormExtensionAbility实例及其所在的ExtensionAbility进程的整个生命周期，都是由卡片管理系统服务FormManagerService进行调度管理。
![form_extension](figures/form_extension.png)


> **说明：**
> 同一应用内的所有同类型的ExtensionAbility运行在同一独立进程（除ServiceExtensionAbility、DataShareExtensionAbility外），跟UIAbility组件不在同一进程，Stage模型的进程模型请参见[进程模型](process-model-stage.md)。
