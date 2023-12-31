# ArkTS Syntax Usage

## How do I dynamically create components using code in ArkUI?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

ArkUI uses the ArkTS declarative development paradigm. Developers cannot hold component instances. During declaration, you can control component creation by rendering control syntax and dynamically building UI elements.

**Example**

```
// Create a component using the if statement.
if(this.isTrue) {
  Text ("Create Text Component").fontSize (30)
}
// Create a component using the ForEach statement.
ForEach(this.nums,(item) => {
  Text(item + '').fontSize(30)
},item => JSON.stringify(item))
```

**Reference**

[Overview of Rendering Control](../quick-start/arkts-rendering-control-overview.md)

## What is the difference between an @Builder decorated method and a regular method?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

The @Builder decorated method allows for use of a custom component, while regular methods do not. If a custom component is used in an @Builder decorated method, it is re-created each time the method is called.

**Reference**

[@BuilderParam](../quick-start/arkts-builderparam.md)

## How do I define @BuilderParam decorated attributes?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

-   Without parameters

    If no parameter is passed when assigning a value to the **@BuilderParam** decorated attribute (for example, **content: this.specificParam**), define the type of the attribute as a function without a return value (for example, **@BuilderParam content: \(\) =\> void**).

-   With parameters

    If any parameter is passed when assigning a value to the **@BuilderParam** decorated attribute (for example, **callContent: this.specificParam1\("111"\)**), define the type of the attribute as **any** (for example, **@BuilderParam callContent: any**).


**Reference**

[@BuilderParam](../quick-start/arkts-builderparam.md)

## How do I listen for object changes in an array?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

To listen for object changes in an array, use the @Observed and @ObjectLink decorators. **@Observed** applies to classes, and **@ObjectLink** applies to variables.

**Example**

1.  Use @Observed on a class.

    ```
    @Observed
    class ClassA {
      public name: string
      public c: number
      public id: number
    
      constructor(c: number, name: string = 'OK') {
        this.name = name
        this.c = c
      }
    }
    ```

2.  Use @ObjectLink on a component variable.

    ```
    @Component
    struct ViewA {
      label: string = 'ViewA1'
      @ObjectLink a: ClassA
    
      build() {
        Row() {
          Button(`ViewA [${this.label}] this.a.c= ${this.a.c} +1`)
            .onClick(() => {
              this.a.c += 1
            })
        }.margin({ top: 10 })
      }
    }
    ```


**Reference**

[\@Observed and \@ObjectLink: Observing Attribute Changes in Nested Class Objects](../quick-start/arkts-observed-and-objectlink.md)

## How do I transfer values through the parent component to @Link decorated varaibles in a child component?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

To enable a child component to receive the value from the parent component through @Link, '**\$**' must be used to first establish a reference relationship between variables in the child and parent components.  

**Example**

The **@Link** semantics are derived from the '**$**' operator. In other words, **\$isPlaying** is the two-way binding of the internal state **this.isPlaying**. When the button in the **PlayButton** child component is touched, the value of the @Link decorated variable is changed, and **PlayButton** together with the **\<Image>** and **\<Text>** components of the parent component is refreshed. Similarly, when the button in the parent component is touched, the value of **this.isPlaying** is changed, and **PlayButton** together with the **\<Text>** and **\<Button>** components of the parent component is refreshed.

1.  Use the @State decorator in the parent component and use the '**\$**' operator to create a reference for transferring data.

    ```
    @Entry
    @Component
    struct Player {
      @State isPlaying: boolean = false
      build() {
        Column() {
          PlayButton({ buttonPlaying: $isPlaying })
          Text(`Player is ${this.isPlaying ? '' : 'not'} playing`).fontSize(18)
          Button('Parent:' + this.isPlaying)
            .margin(15)
            .onClick(() => {
              this.isPlaying = !this.isPlaying
            })
        }
      }
    }
    
    
    ```

2.  Use @Link in the child component to receive data.

    ```
    @Component
    struct PlayButton {
      @Link buttonPlaying: boolean
    
      build() {
        Column() {
          Button(this.buttonPlaying ? 'pause' : 'play')
            .margin(20)
            .onClick(() => {
              this.buttonPlaying = !this.buttonPlaying
            })
        }
      }
    }
    ```


**Reference**

[@Link](../quick-start/arkts-link.md)

## How does a component synchronize state with its grandchild components?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

-   Method 1 (recommended): Use the @Provide and @Consume decorators. Specifically, use @Provide in the component and @Consume in the grandchild component to implement two-way data binding between the components.

-   Method 2: Use the @State and @Link decorators. Specifically, use @State in the parent component and @Link in each layer of child components (child and grandchild components).

**Example 1**

1.  Include a child component in the component. Employ @Provide in the component to provide the **reviewVote** parameter to its grandchild component.

    ```
    @Entry
    @Component
    struct Father{
      @Provide("reviewVote") reviewVotes: number = 0;
    
      build() {
        Column() {
          Son()
          Button(`Father: ${this.reviewVotes}`)
            ...
        }
      }
    }
    ```

2.  Include the grandchild component in the child component.

    ```
    @Component
    struct Son{
      build() {
        Column() {
          GrandSon()
        }
      }
    }
    ```

3.  Employ @Consume in the grandchild component to receive the **reviewVote** parameter.

    ```
    @Component
    struct GrandSon{
      @Consume("reviewVote") reviewVotes: number
    
      build() {
        Column() {
          Button(`GrandSon: ${this.reviewVotes}`)
            ...
        }.width('100%')
      }
    }
    ```


**Example 2**

1.  Employ @State in the component **Father** to decorate **reviewVote**.

    ```
    @Entry
    @Component
    struct Father {
      @State reviewVotes: number = 0;
    
      build() {
        Column() {
          Son({reviewVotes:$reviewVotes})
          Button(`Father: ${this.reviewVotes}`)
            ...
        }
      }
    }
    ```

2.  Employ @Link in the child component **Son** to receive the **reviewVote** parameter passed from **Father**.

    ```
    @Component
    struct Son{
      @Link reviewVotes: number;
      build() {
        Column() {
          Grandson({reviewVotes:$reviewVotes})
        }
      }
    }
    
    
    ```

3.  Employ @Link in the grandchild component **GrandSon** to receive the **reviewVote** parameter passed from **Son**.

    ```
    @Component
    struct Grandson{
      @Link reviewVotes: number;
    
      build() {
        Column() {
          Button(`Grandson: ${this.reviewVotes}`)
            ...
        }.width('100%')
      }
    }
    ```


## How is a callback function defined in JS?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

The following is an example to illustrate how to define a callback function:

1.  Define the callback function.

    ```
    // Define a callback function that contains two parameters and returns void.
    myCallback: (a:number,b:string) => void
    ```

2.  Initialize the callback function by assigning values.

    ```
    aboutToAppear() {
      // Initialize the callback function.
      this.myCallback= (a,b)=>{
        console.info(`handle myCallback a=${a},b=${b}`)
      }}
    ```


## How do I maximize performance in cases when a component needs to be updated for multiple times?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

Use the state management module for the purpose. Currently, the minimum update is supported. When the data dependency changes, instead of updating the entire custom component, only the view content that depends on the data is updated.

## How does this of a function in an object point to the outer layer?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

You can use the arrow function for this purpose.

**Example**

```
const obj = {
  start:() => {
    return this.num
  }
}
```

## How do I obtain data through an API before page loading?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

Data needs to be obtained before page rendering so as to be rendered when needed.

**Solution**

In the **aboutToAppear** function, use an asynchronous API to obtain page data and @State to decorate related variables. After the data is obtained, the page is automatically refreshed based on the variables.

**Example**

```
@Entry
@Component
struct Test6Page {
  // After the data is obtained, the page is automatically refreshed.
  @State message: string = 'loading.....'
  aboutToAppear(){
    // Simulate an asynchronous API to obtain data.
    setTimeout(()=>{
      this.message = 'new msg'
    },3000)
  }
  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

## How do I display sensor data in the \<Text> component on the UI in real time?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

The type of data returned by the sensor is double. To display it in the \<Text> component, first convert the data from double to string.

## How do I listen for screen rotation events?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

To listen for screen rotation events, use the **mediaquery** API.

```
import mediaquery from '@ohos.mediaquery'
let listener = mediaquery.matchMediaSync('(orientation: landscape)'); // Listen for landscape events.
function onPortrait(mediaQueryResult) {
  if (mediaQueryResult.matches) {
   // do something here
  } else {
   // do something here
  }
}
listener.on('change', onPortrait) // Register a callback.
listener.off('change', onPortrait) // Deregister a callback.
```

**Reference**

[@ohos.mediaquery (Media Query)](../reference/apis/js-apis-mediaquery.md)

## What should I do if a singleton does not take effect after the page is changed?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

A singleton works only in the same page. It becomes **undefined** when the page changes.

**Solution**

A JS file is generated for each page, and a defined singleton is generated in each JS file. Therefore, the singleton in applicable only to the owning page.

To share an instance across pages, it must be created at the UIAbility or application level.

## How do I convert a string in time format to a date object?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

If the string is in the yyyy-MM-dd format, you can convert it to a date object by calling **new Date\("yyyy-MM-dd"\)**.

```
new Date("2021-05-23");
new Date("2020/2/29");
new Date("2020-14-03");
new Date("14-02-2021");
```

If the string is in other formats, you can convert it to a date object by calling **new Date\(year:number,month:number,day?:number,hour?:number,minute?:number,second?:number,ms?:number\)**.

```
// Syntax for creating a date based on parameters:
new Date(yearValue, IndexOfMonth, dayValue, hours, minutes, seconds)
```

Pass the date parameters as arguments.

-   **yearValue**: the year in the ISO 8061 YYYY format, for example, **2021**. If we specify a value in YY format, it will be incorrectly accepted. For example, the value **21** would be considered the year 1921 rather than 2021.
-   **IndexOfMonth**: index of the month, which starts from 0. It is obtained by subtracting 1 from the month value. For example, for March, the month value is 3, but the value of **IndexOfMonth** will be 2 (that is, 3 – 1 = 2). The value should typically be within the 0–11 range.
-   **dayValue**: day of the month. It should range from 1 to 31 depending on the number of days in the month. For example, for 21-05-2021, the day value is **21**.
-   **hours**: hour of the day. For example, **10** for 10 o'clock.
-   **minutes**: number of minutes that have elapsed in the hour.
-   **seconds**: number of seconds past a minute.

## How do I convert a string to a byte array in ArkTS?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

Refer to the following code:

```
stringToArray(str:string) {
  var arr = [];
  for(var i = 0,j = str.length;i<j;++i) {
 arr.push(str.charCodeAt(i))
  }
  return arr;
}
```

## How do I implement string encoding and decoding in ArkTS?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

You can use **TextEncoder** and **TextDecoder** provided by the **util** module.

**Reference**

[TextEncoder](../reference/apis/js-apis-util.md#textencoder), [TextDecoder](../reference/apis/js-apis-util.md#textdecoder)

## How do I import and export namespaces?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

Use **import** and **export** statements.

-   Exporting namespaces from the database:

    ```
    namespace Util{
        export function getTime(){
            return Date.now()
        }
    }
    export default Util
    ```

-   Importing namespaces

    ```
    import Util from './util'
    Util.getTime()
    ```

## Can relational database operations be performed in the Worker thread?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

Currently, the relational database (RDB) object in the UI main thread cannot be sent to the Worker thread for operations. To use the RDB in the Worker thread, you must obtain a new RDB object.

## How do I obtain files in the resource directory of an application?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

-   Method 1: Use **\$r** or **\$rawfile**. This method applies to static access, during which the **resource** directory remains unchanged when the application is running.
-   Method 2: Use **ResourceManager**. This method applies to dynamic access, during which the **resource** directory dynamically changes when the application is running.

**Reference**

[Resource Categories and Access](../quick-start/resource-categories-and-access.md) and [@ohos.resourceManager (Resource Manager)](../reference/apis/js-apis-resource-manager.md)

## How do I convert the XML format to the JSON format?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

The data returned by the server is encoded using Base64 in XML format and needs to be converted to the JSON format for subsequent processing.

**Solution**

Use the Base64-related APIs in the **util** module to decode data, and then use the **convertxml** module to parse data in XML format.

**Example**

```
import convertxml from '@ohos.convertxml';
import util from '@ohos.util';

@Entry
@Component
struct Faq_4_31 {
  @State message: string = 'base64 to JSON'

  build() {
    Row() {
      Column() {
        Text(this.message)
          .fontSize(50)
          .fontWeight(FontWeight.Bold)
          .onClick(() => {
            / *Original data in GBK encoding
            <?xml version="1.0" encoding="GBK"?>
            <data>
            <asset_no>xxxxx</asset_no>
            <machine_sn>xxxx</machine_sn>
            <bios_id>xxxx</bios_id>
            <responsible_emp_name><![CDATA[xxxx]]></responsible_emp_name>
            <responsible_account><![CDATA[xxxx xxxx]]></responsible_account>
            <responsible_emp_no>xxxx</responsible_emp_no>
            <responsible_dept><![CDATA[xxxx]]></responsible_dept>
            <user_dept><![CDATA[xxxx]]></user_dept>
            <user_name><![CDATA[xxx]]></user_name>
            <cur_domain_account>xxxx</cur_domain_account>
            <asset_loc><![CDATA[--]]></asset_loc>
            <asset_loc_cur><![CDATA[]]></asset_loc_cur>
            <asset_type>1</asset_type>
            <asset_use>For Outsourcing Staff/xxxx</asset_use>
            <overdue_date></overdue_date>
            <asset_status>xxxx</asset_status>
            <asset_period>xxxx</asset_period>
            <license></license>
            </data>
             */
            let src = 'PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iR0JLIj8+CjxkYXRhPgo8YXNzZXRfbm8+eHh4eHg8L2Fzc2V0X25vPgo8bWFjaGluZV9zbj54eHh4PC9tYWNoaW5lX3NuPgo8Ymlvc19pZD54eHh4PC9iaW9zX2lkPgo8cmVzcG9uc2libGVfZW1wX25hbWU+PCFbQ0RBVEFbeHh4eF1dPjwvcmVzcG9uc2libGVfZW1wX25hbWU+CjxyZXNwb25zaWJsZV9hY2NvdW50PjwhW0NEQVRBW3h4eHggeHh4eF1dPjwvcmVzcG9uc2libGVfYWNjb3VudD4KPHJlc3BvbnNpYmxlX2VtcF9ubz54eHh4PC9yZXNwb25zaWJsZV9lbXBfbm8+CjxyZXNwb25zaWJsZV9kZXB0PjwhW0NEQVRBW3h4eHhdXT48L3Jlc3BvbnNpYmxlX2RlcHQ+Cjx1c2VyX2RlcHQ+PCFbQ0RBVEFbeHh4eF1dPjwvdXNlcl9kZXB0Pgo8dXNlcl9uYW1lPjwhW0NEQVRBW3h4eF1dPjwvdXNlcl9uYW1lPgo8Y3VyX2RvbWFpbl9hY2NvdW50Pnh4eHg8L2N1cl9kb21haW5fYWNjb3VudD4KPGFzc2V0X2xvYz48IVtDREFUQVstLV1dPjwvYXNzZXRfbG9jPgo8YXNzZXRfbG9jX2N1cj48IVtDREFUQVtdXT48L2Fzc2V0X2xvY19jdXI+Cjxhc3NldF90eXBlPjE8L2Fzc2V0X3R5cGU+Cjxhc3NldF91c2U+Rm9yIE91dHNvdXJjaW5nIFN0YWZmL3h4eHg8L2Fzc2V0X3VzZT4KPG92ZXJkdWVfZGF0ZT48L292ZXJkdWVfZGF0ZT4KPGFzc2V0X3N0YXR1cz54eHh4PC9hc3NldF9zdGF0dXM+Cjxhc3NldF9wZXJpb2Q+eHh4eDwvYXNzZXRfcGVyaW9kPgo8bGljZW5zZT48L2xpY2Vuc2U+CjwvZGF0YT4='
            let base64 = new util.Base64Helper();
            // base64 decoding
            let src_uint8Array = base64.decodeSync(src);
            // Decode the string into a UTF-8 string.
            let textDecoder = util.TextDecoder.create("utf-8",{ignoreBOM: true})
            let src_str = textDecoder.decodeWithStream(src_uint8Array)
            // Replace the encoding field.
            src_str = src_str.replace("GBK","utf-8")
            console.log('Test src_str: ' + JSON.stringify(src_str));
            //Convert XML format to JSON format.
            let conv = new convertxml.ConvertXML();
            let options = {trim : false, declarationKey:"_declaration",
              instructionKey : "_instruction", attributesKey : "_attributes",
              textKey : "_text", cdataKey:"_cdata", doctypeKey : "_doctype",
              commentKey : "_comment", parentKey : "_parent", typeKey : "_type",
              nameKey : "_name", elementsKey : "_elements"}
            let src_json = JSON.stringify(conv.convertToJSObject(src_str, options));
            console.log('Test json: ' + JSON.stringify(src_json));
          })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

## What are the restrictions on using generator functions in TypeScript?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

Below are the restrictions on using generator functions in TypeScript:

-   Expressions can be used only in character strings (in the \(\$\{expression\}\) format), **if** conditions, **ForEach** parameters, and component parameters.
-   No expressions should cause any application state variables (**@State**, **@Link**, and **@Prop**) to change. Otherwise, undefined and potentially unstable framework behavior may occur.
-   The generator function cannot contain local variables.

None of the above restrictions apply to anonymous function implementations of event handlers (such as **onClick**).

## How do I set a badge for each of the four corners of an image?

Applicable to: OpenHarmony 3.2 Beta5

**Solution**

You can use absolute positioning to set the offset of the element anchor relative to the top start point of the parent container. In the layout container, setting this attribute does not affect the layout of the parent container.

**Example**

```
@Entry
@Component
struct PositionExample2 {
  build() {
    Column({ space: 20 }) {
      Stack({ alignContent: Alignment.TopStart }) {
        Row()
          .size({ width: '100', height: '100' })
          .backgroundColor(0xdeb887)
        Image($r('app.media.app_icon'))
          .size({ width: 25, height: 25 })
          .markAnchor({ x: 0, y: 0 })
        Image($r('app.media.app_icon'))
          .size({ width: 25, height: 25 })
          .markAnchor({ x: 25, y: 25 })
          .position({ x: '100%', y: '100%' }) 
      }.margin({ top: 25 }).width('100').height('100')
    }
    .width('100%').margin({ top: 25 })
  }
}
```

## How do I use the util.generateRandomUUID parameter?

Applicable to: OpenHarmony 3.2 Beta5

**Solution**

The bottom layer of **generateRandomUUID** uses the **Node.js crypto.randomUUID\(\)** API. If the parameter passed in is **false**, a new UUID is generated and cached in the system. If the parameter passed in is **true**, the existing cached UUID is used.

**Reference**

[util.generateRandomUUID](../reference/apis/js-apis-util.md#utilgeneraterandomuuid9)

## Do the Worker thread and the main thread run in the same global context?

Applicable to: OpenHarmony 3.2 Beta5

**Solution**

No. The Worker thread and the main thread are not in the same context. They interact with each other in data communication mode.

**Reference**

[@ohos.worker (Worker Startup)](../reference/apis/js-apis-worker.md)

## How do I set one application icon for different device types?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

To configure your application icon to show on different device types, use resource qualifiers.

**Example**

1. Create a resource directory and add resource files to the directory. In this example, a **tablet** resource directory is created in **src/main/resources** and a **media** resource folder in the **tablet** directory.

```
├─base
│  ├─element
│  ├─media
│  └─profile
├─rawfile
├─tablet
│  ├─element
│  └─media
```

2. Add the icon file to be displayed when the device type is tablet to the **media** folder. Reference the icon file on the UI.

```
@Entry @Component struct Index { build() {
   Flex({ direction: FlexDirection.Column, alignItems: ItemAlign.Center, justifyContent: FlexAlign.Center }) {
     Text($r("app.string.my_string"))
       .fontSize($r("app.float.my_float"))
       .fontColor($r("app.color.my_color"))
     Image($r("app.media.my_image"))
       .width(100)
       .height(100)
   }
   .width('100%')
   .height('100%') } }
```

## How do I prevent "this" in a method from changing to "undefined" when the method is called?

Applicable to: OpenHarmony 3.2 (API version 9)

**Solution**

Method 1: Add **.bind\(this\)** when calling the method.

Method 2: Use the arrow function.

## Is there any difference between the systemTime.getCurrentTime\(\) API of OpenHarmony and the new Date\(\).getTime\(\) API of JS?

Applicable to: OpenHarmony 3.2 (API version 9)

**Solution**

**systemTime.getCurrentTime\(false\)** is equivalent to **new Date\(\).getTime\(\)**, returning the number of milliseconds since January 1, 1970. **systemTime.getCurrentTime\(true\)** returns the number of nanoseconds since January 1, 1970. The system time is used in both APIs.

## How do I implement the ArkTS counterpart of the JS slot feature?

Applicable to: OpenHarmony 3.2 (API version 9)

**Solution**

Applicable to: OpenHarmony SDK 3.2.5.5, stage model of API version 9

Use @Build and @BuilderParam in ArkTS.

**Reference**

[\@BuilderParam: @Builder Function Reference](../quick-start/arkts-builderparam.md).

## Why is the text not centered vertically when lineHeight is set?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Cause**

Text in the **\<Text>** component is centered by default. You do not need to set the **lineHeight** attribute. As the text is drawn from the bottom, an appropriate line height can have the text centered. However, if the line height is too large, the text appears aligned toward the bottom. In general cases, use the **lineHeight** attribute together with the **padding** attribute to adjust the line spacing.

**Reference**

[Text](../reference/arkui-ts/ts-basic-components-text.md#example-1)

## How do I set the controlButton attribute for the \<SideBarContainer> component?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

The sample code is as follows:

```
@Entry
@Component
struct SideBarContainerExample {
  normalIcon : Resource = $r("app.media.icon")
  selectedIcon: Resource = $r("app.media.icon")
  @State arr: number[] = [1, 2, 3]
  @State current: number = 1

  build() {
    SideBarContainer(SideBarContainerType.Embed)
    {
      Column() {
        ForEach(this.arr, (item, index) => {
          Column({ space: 5 }) {
            Image(this.current === item ? this.selectedIcon : this.normalIcon).width(64).height(64)
            Text("Index0" + item)
              .fontSize(25)
              .fontColor(this.current === item ? '#0A59F7' : '#999')
              .fontFamily('source-sans-pro,cursive,sans-serif')
          }
          .onClick(() => {
            this.current = item
          })
        }, item => item)
      }.width('100%')
      .justifyContent(FlexAlign.SpaceEvenly)
      .backgroundColor('#19000000')


      Column() {
        Text('SideBarContainer content text1').fontSize(25)
        Text('SideBarContainer content text2').fontSize(25)
      }
      .margin({ top: 50, left: 20, right: 30 })
    }
    .sideBarWidth(150)
    .minSideBarWidth(50)
    .controlButton({left:32,
      top:32,
      width:32,
      height:32, 
      icons:{shown: $r("app.media.icon"),
        hidden: $r("app.media.icon"),
        switching: $r("app.media.icon")}})
    .maxSideBarWidth(300)
    .onChange((value: boolean) => {
      console.info('status:' + value)
    })
  }
}
```

## How do I implement the dragging feature for the \<Grid> component?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

1.  Set the **editMode\(true\)** attribute of the **\<Grid>** component to specify whether the component enters the editing mode. In the editing mode, you can drag grid items.
2.  Set the image displayed during dragging in the [onItemDragStart](../reference/arkui-ts/ts-container-grid.md#events) callback.
3.  Obtain the drag start position and drag insertion position from the [onItemDrop](../reference/arkui-ts/ts-container-grid.md#events) callback, and complete the array position exchange logic in the [onDrag](../reference/arkui-ts/ts-universal-events-drag-drop.md#events) callback. The sample code is as follows:

    ```
    @Entry
    @Component
    struct GridExample {
      @State numbers: String[] = []
      scroller: Scroller = new Scroller()
      @State text: string = 'drag'
    
      @Builder pixelMapBuilder () { // Drag style
        Column() {
          Text(this.text)
            .fontSize(16)
            .backgroundColor(0xF9CF93)
            .width(80)
            .height(80)
            .textAlign(TextAlign.Center)
        }
      }
    
      aboutToAppear() {
        for (let i = 1;i <= 15; i++) {
          this.numbers.push(i + '')
        }
      }
    
      changeIndex(index1: number, index2: number) {// Exchange the array item position.
        [this.numbers[index1], this.numbers[index2]] = [this.numbers[index2], this.numbers[index1]];
      }
    
      build() {
        Column({ space: 5 }) {
          Grid(this.scroller) {
            ForEach(this.numbers, (day: string) => {
              GridItem() {
                Text(day)
                  .fontSize(16)
                  .backgroundColor(0xF9CF93)
                  .width(80)
                  .height(80)
                  .textAlign(TextAlign.Center)
                  .onTouch((event: TouchEvent) => {
                    if (event.type === TouchType.Up) {
                      this.text = day
                    }
                  })
              }
            })
          }
          .columnsTemplate('1fr 1fr 1fr')
          .columnsGap(10)
          .rowsGap(10)
          .onScrollIndex((first: number) => {
            console.info(first.toString())
          })
          .width('90%')
          .backgroundColor(0xFAEEE0)
          .height(300)
          .editMode(true) // Set whether the grid enters the editing mode. In the editing mode, you can drag grid items.
          .onItemDragStart((event: ItemDragInfo, itemIndex: number) => { // Triggered when a grid item starts to be dragged.
            return this.pixelMapBuilder() // Set the image displayed during dragging.
          })
          .onItemDrop((event: ItemDragInfo, itemIndex: number, insertIndex: number, isSuccess: boolean) => { // Triggered when the dragged item is dropped on the drop target of the grid.
            console.info('beixiang' + itemIndex + '', insertIndex + '') // itemIndex indicates the initial position of the dragged item; insertIndex indicates the index of the position to which the dragged item will be dropped.
            this.changeIndex(itemIndex, insertIndex)
          })
        }.width('100%').margin({ top: 5 })
      }
    }
    ```


## Which API is used for URL encoding?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

Use the global function **encodeURI** for encoding and **decodeURI** for decoding. For example, the space character ""is encoded as %20.

```
let a = encodeURI(" ")
console.log(a) // %20
```

## How do I parse XML files?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

You can use the **convert** API of the **ConvertXML** module to parse XML text into JS objects.

**Reference**

[@ohos.convertxml (XML-to-JavaScript Conversion)](../reference/apis/js-apis-convertxml.md)

## What should I do if the .stateStyles doesn't conform standard error is reported with the use of the @Styles decorator?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Cause**

The @Styles decorator is used for non-universal attributes.

**Solution**

Use the @Styles decorator only for non-universal attributes. Alternatively, use Builder to extract common components.

## How do I use \$\$ for the \<Radio> component?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

When the **\<Radio>** component uses a variable bound to **\$\$**, changes to the variable trigger re-render of only the owning component, improving the rendering speed.

When the state of the **\<Radio>** component changes, the bound variable is not automatically updated.

**Reference**

[$ Syntax: Two-Way Synchronization of Built-in Components](../quick-start/arkts-two-way-sync.md)

## What should I do if ForEach does not work on a real device?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Symptom**

**ForEach** works in the previewer, but not on a real device.

**Cause**

If the system version on the real device is 3.2 beta5 or later, the minimum update policy is enabled by default.

However, minimum update is not enabled in DevEco Studio of an earlier version. As a result, components run abnormally.

**Solution**

Add the **metadata** configuration item to the **module.json5** file.

```
{
  "module": {
    "metadata": [
      {
        "name": "ArkTSPartialUpdate",
        "value": "true"
      }
  }
}
```
