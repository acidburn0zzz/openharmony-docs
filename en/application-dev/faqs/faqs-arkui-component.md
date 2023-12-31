# ArkUI Component Development (ArkTS)

## Can custom dialog boxes be defined or used in .ts files?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

Unfortunately, no. ArkTS syntax is required for defining and initializing custom dialog boxes. Therefore, they can be defined and used only in .ets files.

**Reference**

[Custom Dialog Box](../reference/arkui-ts/ts-methods-custom-dialog-box.md)

## How do I transfer variables in a custom dialog box to a page?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

The variable defined in a custom dialog box needs to be transferred to the page when the dialog box is closed or the variable changes.

**Solution**

-   Method 1: Define the variable as a state variable of the custom dialog box.
-   Method 2: During initialization of the custom dialog box, pass to it a method, which is triggered in the custom dialog box and accepts the variable in the custom dialog box as a parameter.
-   Method 3: Use AppStorage or LocalStorage to manage page state and implement state sharing between the custom dialog box and page.

**Example**

-   Method 1:

    ```
    @CustomDialog
    struct CustomDialog01 {
      @Link inputValue: string
      controller: CustomDialogController
      build() {
        Column() {
          Text('Change text').fontSize(20).margin({ top: 10, bottom: 10 })
          TextInput({ placeholder: '', text: this.inputValue }).height(60).width('90%')
            .onChange((value: string) => {
              this.inputValue = value
            })
        }
      }
    }
    
    @Entry
    @Component
    struct DialogDemo01 {
      @State inputValue: string = 'click me'
      dialogController: CustomDialogController = new CustomDialogController({
        builder: CustomDialog01({
          inputValue: $inputValue
        })
      })
    
      build() {
        Column() {
          Button(this.inputValue)
            .onClick(() => {
              this.dialogController.open()
            }).backgroundColor(0x317aff)
        }.width('100%').margin({ top: 5 })
      }
    }
    
    ```

-   Method 2:

    ```
    @CustomDialog
    struct CustomDialog02 {
      private inputValue: string
      changeInputValue: (val: string) => void
      controller: CustomDialogController
      build() {
        Column() {
          Text('Change text').fontSize(20).margin({ top: 10, bottom: 10 })
          TextInput({ placeholder: '', text: this.inputValue }).height(60).width('90%')
            .onChange((value: string) => {
              this.changeInputValue(value)
            })
        }
      }
    }
    
    @Entry
    @Component
    struct DialogDemo02 {
      @State inputValue: string = 'click me'
      dialogController: CustomDialogController = new CustomDialogController({
        builder: CustomDialog02({
          inputValue: this.inputValue,
          changeInputValue: (val: string) => {
            this.inputValue = val
          }
        })
      })
    
      build() {
        Column() {
          Button(this.inputValue)
            .onClick(() => {
              this.dialogController.open()
            }).backgroundColor(0x317aff)
        }.width('100%').margin({ top: 5 })
      }
    }
    
    ```

-   Method 3:

    ```
    let storage = LocalStorage.GetShared()
    @CustomDialog
    struct CustomDialog03 {
      @LocalStorageLink('inputVal')  inputValue: string = ''
      controller: CustomDialogController
      build() {
        Column() {
          Text('Change text').fontSize(20).margin({ top: 10, bottom: 10 })
          TextInput({ placeholder: '', text: this.inputValue }).height(60).width('90%')
            .onChange((value: string) => {
              this.inputValue = value;
            })
        }
      }
    }
    
    @Entry(storage)
    @Component
    struct DialogDemo03 {
      @LocalStorageLink('inputVal') inputValue: string = ''
      dialogController: CustomDialogController = new CustomDialogController({
        builder: CustomDialog03()
      })
    
      build() {
        Column() {
          Button(this.inputValue)
            .onClick(() => {
              this.dialogController.open()
            }).backgroundColor(0x317aff)
        }.width('100%').margin({ top: 5 })
      }
    }
    
    ```


## How do I obtain the width and height of a component?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

The width and height of a component need to be obtained to calculate the size and offset of the layout area.

**Solution**

-   Method 1: Use the **onAreaChange** event of the component, which is triggered when the component is initialized or the component size changes.
-   Manner 2: Use the callback in the click or touch event, which provides the area information of the target element.

**Reference**

[Component Area Change Event](../reference/arkui-ts/ts-universal-component-area-change-event.md), [Click Event](../reference/arkui-ts/ts-universal-events-click.md), [Touch Event](../reference/arkui-ts/ts-universal-events-touch.md)

## How do I clear the content of the \<TextInput> and \<TextArea> components by one click?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

A click-to-clear feature is required to remove all characters in the **\<TextInput>** and **\<TextArea>** component at once.

**Solution**

Convert the **text** attribute of the **\<TextInput>** and **\<TextArea>** component to a state variable. Assign an empty string to the state variable when the click-to-clear event is performed.

**Example**

```
struct Index {
@State text: string = 'Hello World'
controller: TextInputController = new TextInputController()
  build() {
    Row() {
      Column() {
        TextInput({ placeholder: 'Please input your words.', text: this.text,
          controller:this.controller}).onChange((value) => {
            this.text = value
          })
        Button("Clear TextInput").onClick(() => {
          this.text = "";
        })
      }
      .width('100%')
    }
    .height('100%')
  }
}
```

## How do I set the position of a custom dialog box?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

By default, a custom dialog box is displayed in the center of the window. In some cases, it needs to be aligned with the window border.

**Solution**

During initialization of the custom dialog box, set the **alignment** and **offset** parameters.

**Reference**

[Custom Dialog Box](../reference/arkui-ts/ts-methods-custom-dialog-box.md)

## How do I hide the overflow content of a container component?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

When content overflows in a container component, that is, the child component does not fit in the container component, the overflow content needs to be processed.

**Solution**

To clip and hide overflow content, set the **clip** universal attribute to **true**. By default, this attribute is set to **false**.

**Reference**

[Shape Clipping](../reference/arkui-ts/ts-universal-attributes-sharp-clipping.md)

## How do I set a custom dialog box to automatically adapt its size to content?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

When a custom dialog box contains a child component whose area size can be changed, it needs to automatically adjust its size.

**Solution**

-   Method 1: Use the default style of the custom dialog box. In this case, the dialog box automatically adapts its width to the grid system and its height to the child components; the maximum height is 90% of the container height.
-   Method 2: Use a custom style of the custom dialog box. In this case, the dialog box automatically adapts its width and height to the child components.

**Reference**

[Custom Dialog Box](../reference/arkui-ts/ts-methods-custom-dialog-box.md)

## What is the function of the gridCount parameter in the custom dialog box?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

The **gridCount** parameter indicates the number of grid columns occupied by the dialog box. The system divides the window width into equal regions. The number of equal regions is the number of grid columns, which varies by device. For example, if the screen density of a device is 320 vp <= horizontal width < 600 vp, the number of grid columns is 4, and the valid value of **gridCount** is \[1, 4\].

Note: This parameter is valid only when the custom dialog box is in the default style.

**Reference**

[Custom Dialog Box](../reference/arkui-ts/ts-methods-custom-dialog-box.md)

## How do I remove the white background of a custom dialog box?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

When in the default style a custom dialog box comes with a white background.

**Solution**

To remove the white background, set the custom dialog box to a custom style.

1.  During initialization of the custom dialog box, set **customStyle** to **true**.
2.  During initialization of the custom dialog box, set **backgroundColor** to the color you prefer.

**Reference**

[Custom Dialog Box](../reference/arkui-ts/ts-methods-custom-dialog-box.md)

## How do I customize the eye icon for the password input mode of the \<TextInput> component?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

The eye icon for the password input mode (with the **type** attribute of the **\<TextInput>** component set to **InputType.Password**) cannot be customized.

**Solution**

The eye icon itself cannot be customized. You can use set the **showPasswordIcon** attribute of the **\<TextInput>** component to **false** to hide the icon, and use the **\<Image>** component to control the type of the **\<TextInput>** component.

**Reference**

[TextInput](../reference/arkui-ts/ts-basic-components-textinput.md)

## How do I use the onSubmit event of the \<TextInput> component?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

The **onSubmit** event is triggered when a user presses **Enter** on the (physical or soft) keyboard. The callback parameter in the event is the current Enter key type. The Enter key type can be set through the **enterKeyType** attribute of the **\<TextInput>** component. Setting the key style of the soft keyboard requires support by the input method.

**Reference**

[TextInput](../reference/arkui-ts/ts-basic-components-textinput.md)

## How do I set the caret position to the start point for when the \<TextInput> component obtains focus?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

When the **\<TextInput>** component obtains focus, the caret automatically moves to the position of the touch point, instead of the start position.

**Solution**

1.  Bind the **\<TextInput>** component to the **onEditChange** event, which is triggered when the component enters the input state.
2.  Call the **setTimeout** API for asynchronous processing. Then call the **TextInputController.caretPosition** API in the event callback to set the caret position.

**Example**

```
@Entry
@Component
struct TextInputDemo {
  controller: TextInputController = new TextInputController()

  build() {
    Column() {
      TextInput({ controller: this.controller })
        .onEditChange((isEditing: boolean) => {
          if (isEditing) {
            setTimeout(() => {
              this.controller.caretPosition(0)
            }, 100)
          }
        })
    }
  }
}
```

**Reference**

[TextInput](../reference/arkui-ts/ts-basic-components-textinput.md)


## How do I obtain the current scrolling offset of a scrollable component?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

1.  During initialization of the scrollable component, such as **\<List>**, **\<Grid>**, and **\<Scroll>**, set the **scroller** parameter to bind the component to a scroll controller.
2.  Call the **currentOffset** API of the controller to obtain the horizontal and vertical scrolling offsets.

**Reference**

[Scroll](../reference/arkui-ts/ts-container-scroll.md#currentoffset)

## How do I align text vertically?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Symptom**

Text cannot be aligned vertically in the **\<Text>** component.

**Solution**

Text is aligned horizontally in the **\<Text>** component. To enable text to align vertically, you can split the file, include it in a **\<Flex>** container, and set the container's main axis direction to vertical.

**Example**

```
@Entry
@Component
struct Index15 {
  private message: string = 'This document is intended for novices in developing applications. It introduces you to the application development process and main files in the project director, by walking you through the building of a simple application with the page redirection/return feature.';
  build() {
    Flex({ direction: FlexDirection.Column, wrap: FlexWrap.Wrap }) {
      ForEach(this.message.split(''), (item, index) => {
        Text(item)
          .fontSize(30)
          .flexShrink(0)
      })
    }
  }
}
```

## How do I set the UI of an ability to transparent?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9)

**Solution**

Set the background color of the top container component to transparent, and then set the **opacity** attribute of the XComponent to **0.01**.

**Example**

```
build() {
  Stack() {
    XComponent({
    id: 'componentId',
    type: 'surface',
    })
    .width('100%')
    .height('100%')
    .opacity(0.01)
    // Page content
  }
  .width('100%')
  .height('100%')
  .backgroundColor('rgba(255,255,255, 0)')
}
```

## Why do the constraintSize settings fail to take effect?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9, stage model)

**Symptom**

If **constraintSize** is set for a component and the width of its child component is set to a percentage, for example, **width\('100%'\)**, **constraintSize** takes effect by multiplying the maximum width by the percentage. As a result, the child component may overflow, in which case it looks like the **constraintSize** settings fail to take effect.

**Solution**

You can use the **\<Scroll>** component at the outer layer. In this way, when **constraintSize** is set and the space occupied by a child component exceeds the specified constraint value, a scrollbar will be displayed.

## How do I set the background color to transparent?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

Set **backgroundColor** to **'\#00000000'**.

## What should I do if the \<Scroll> component cannot scroll to the bottom?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9, stage model)

**Symptom**

Unless otherwise specified, the height of the **\<Scroll>** component is equal to the window height. In this case, the component's bottom area will be blocked by components (if any) outside of it.

**Solution**

Set the height of the **\<Scroll>** component or use the flex layout to limit this height.

## How do I customize the control bar style of the \<Video> component?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9, stage model)

**Solution**

1. Set **controls** to **false** to disable the default control bar.

2. Sets **controller** for the **\<Video>** component.

3. Implement a custom control bar in ArkTS and use **VideoController** to control video playback.

**Example**

```
// xxx.ets
@Entry@Componentstruct VideoCreateComponent {
  @State videoSrc: Resource = $rawfile('video1.mp4')
  @State previewUri: Resource = $r('app.media.poster1')
  @State curRate: PlaybackSpeed = PlaybackSpeed.Speed_Forward_1_00_X
  @State isAutoPlay: boolean = false
  @State showControls: boolean = true
  controller: VideoController = new VideoController()
   build() {
    Column() {
      Video({
        src: this.videoSrc,
        previewUri: this.previewUri,
        currentProgressRate: this.curRate,
        controller: this.controller
      }).width('100%').height(600)
        .autoPlay(this.isAutoPlay)
        .controls(this.showControls)
        .onStart(() => {
          console.info('onStart')
        })
        .onPause(() => {
          console.info('onPause')
        })
        .onFinish(() => {
          console.info('onFinish')
        })
        .onError(() => {
          console.info('onError')
        })
        .onPrepared((e) => {
          console.info('onPrepared is ' + e.duration)
        })
        .onSeeking((e) => {
          console.info('onSeeking is ' + e.time)
        })
        .onSeeked((e) => {
          console.info('onSeeked is ' + e.time)
        })
        .onUpdate((e) => {
          console.info('onUpdate is ' + e.time)
        })
             Row() {
        Button('src').onClick(() => {
          this.videoSrc = $rawfile('video2.mp4') // Switch the video source.
        }).margin(5)
        Button('previewUri').onClick(() => {
          this.previewUri = $r('app.media.poster2') // Switch the preview image.
        }).margin(5)

        Button('controls').onClick(() => {
          this.showControls =! this.showControls // Specify whether to show the control bar.
        }).margin(5)
      }
       Row() {
        Button('start').onClick(() => {
          this.controller.start() // Start playback.
        }).margin(5)
        Button('pause').onClick(() => {
          this.controller.pause() // Pause playback.
        }).margin(5)
        Button('stop').onClick(() => {
          this.controller.stop() // Stop playback.
        }).margin(5)
        Button('setTime').onClick(() => {
          this.controller.setCurrentTime(10, SeekMode.Accurate) // Seek to the 10s position of the video.
        }).margin(5)
      }
       Row() {
        Button('rate 0.75').onClick(() => {
          this.curRate = PlaybackSpeed.Speed_Forward_0_75_X // Play the video at the 0.75x speed.
        }).margin(5)
        Button('rate 1').onClick(() => {
          this.curRate = PlaybackSpeed.Speed_Forward_1_00_X // Play the video at the 1x speed.
        }).margin(5)
        Button('rate 2').onClick(() => {
          this.curRate = PlaybackSpeed.Speed_Forward_2_00_X // Play the video at the 2x speed.
        }).margin(5)
      }
    }
  }}
```

**Reference**

[Video](../reference/arkui-ts/ts-media-components-video.md#start)

## How do I set state-specific styles for a component?

**Solution**

You can use the **stateStyles** attribute to set styles of a component for different states (stateless, pressed, disabled, focused, or clicked).

**Example**

```
//xxx.ts
@Entry
@Component
struct StyleExample {
  @State isEnable: boolean = true;

  @Styles pressedStyles() {
    .backgroundColor("#ED6F21")
    .borderRadius(10)
    .borderStyle(BorderStyle.Dashed)
    .borderWidth(2)
    .borderColor('#33000000')
    .width(120)
    .height(30)
    .opacity(1)
  }
  build() {
    Flex({direction: FlexDirection.Column, alignItems: ItemAlign.Center}) {
      Text("pressed")
        .backgroundColor('#0A59F7')
        .borderRadius(20)
        .borderStyle(BorderStyle.Dotted)
        .borderWidth(2)
        .borderColor(Color.Red)
        .width(100)
        .height(25)
        .opacity(1)
        .fontSize(14)
        .fontColor(Color.White)
        .stateStyles({
          pressed: this.pressedStyles
        })
        .margin({
          bottom: 20
        })
        .textAlign(TextAlign.Center)
    }
    .width(350)
    .height(300)
  }
}
```

**Reference**

[Polymorphic Style](../reference/arkui-ts/ts-universal-attributes-polymorphic-style.md)

## What should I do if the flex width and height in the \<Scroll> component conflicts with the scrolling?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9, stage model)

**Symptom**

When a container component with a fixed size is added to the **\<Scroll>** component, a scrolling error occurs.

**Solution**

Do not set a size for any container component in the **\<Scroll>** component. In this way, the **\<Scroll>** component can adapt its size to the content.

## How does a component process click events in its child components?

Applicable to: OpenHarmony 3.2 Beta5 (API version 9, stage model)

When a child component is initialized in the parent component, the method defined in the parent component is transferred to and invoked in the child component. This process is similar to variable transfer.

**Example**

```
class Model {
  value: string
}
@Entry
@Component
struct EntryComponent {
  test() {
    console.log('testTag test in my component');
  }
  build() {
    Column() {
      MyComponent({ title: { value: 'Hello World 2' }, count: 7, onClick: this.test }) // The defined method is transferred during initialization.
    }
  }
}

@Component
struct MyComponent {
  @State title: Model = { value: 'Hello World' }
  @State count: number = 0
  onClick: any;
  private toggle: string = 'Hello World'
  private increaseBy: number = 1

  build() {
    Column() {
      Text(`${this.title.value}`).fontSize(30)
      Button(`Click to increase count=${this.count}`)
        .margin(20)
        .onClick(() => {
          // Change the count value of the internal state variable.
          this.count += this.increaseBy
          this.onClick.call();
        })
    }
  }
}
```

## How do I implement a text input box that automatically brings up the soft keyboard?

Applicable to: OpenHarmony 3.2 Beta 5 (API version 9)

**Solution**

You can use **focusControl.requestFocus** to control the focus of the text input box. When the text input box is in focus, it automatically brings up the soft keyboard.

**Reference**

[Focus Control](../reference/arkui-ts/ts-universal-attributes-focus.md)
