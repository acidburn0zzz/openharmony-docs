# arkui子系统ChangeLog

## cl.arkui.1 通用事件参数支持undefined

通用事件（点击事件、触摸事件、挂载卸载事件、按键事件、焦点事件、鼠标事件、组件区域变化事件）参数支持undefined。

**示例：**

```ts
// xxx.ets
@Entry
@Component
struct Example {
  build() {
    Button("test")
    .onClick(()=>{
      console.log("click");
    })
    .onClick(undefined)
  }
}
```

**变更影响**

如果事件回调参数为undefined，那么将不再响应已经设置的事件回调。


**关键的接口/组件变更**

不涉及。

**适配指导**

当事件参数设置为undefined，将会禁用该事件，依据实际应用开发场景进行参数设置即可。


## cl.arkui.2 @Prop/@BuilderParam 状态变量需要初始化或从父组件传值

**示例：**

```ts
// xxx.ets
@Entry
@Component
struct Parent {
  @State message: string = 'Parent'
  build() {
    Column() {
      Child()   // 编译报错
    }
  }
}

@Component
struct Child {
  @Prop message: string
  build() {
    Column() {
      
    }
  }
}
```

**变更影响**

当@Prop/@BuilderParam 状态变量未初始化且未从父组件传值时，编译无法通过。


**关键的接口/组件变更**

不涉及。

**适配指导**

对@Prop/@BuilderParam 状态变量做初始化赋值或从父组件调用子组件时传入。


## cl.arkui.3 @BuilderParam 状态变量初始化赋值必须为@Builder函数/方法

**示例：**

```ts
// xxx.ets
@Builder
function builderFunction() {
  Text('Hello Builder')
}

function normal () {

}

@Component
struct Index {
  @BuilderParam builderParam: ()=>void = builderFunction
  @BuilderParam builderParam2: ()=>void = normal   // 编译报错
  build() {
    Column() {

    }
  }
}
```

**变更影响**

@BuilderParam 状态变量初始化赋值非@Builder方法时，编译无法通过。


**关键的接口/组件变更**

不涉及。

**适配指导**

@BuilderParam 状态变量初始化赋值传入@Builder方法。

## cl.arkui.4 Search组件的searchButton属性中SearchButtonOption修改为SearchButtonOptions

**变更影响**

如果显式地使用了SearchButtonOption类型，编译无法通过。

**关键的接口/组件变更**

searchButton属性中类型SearchButtonOption修改为SearchButtonOptions。

**适配指导**

SearchButtonOption修改为SearchButtonOptions。
