# TextInput

The **\<TextInput>** component provides single-line text input.

>  **NOTE**
>
>  This component is supported since API version 7. Updates will be marked with a superscript to indicate their earliest API version.


## Child Components

Not supported


## APIs

TextInput(value?:{placeholder?: ResourceStr, text?: ResourceStr, controller?: TextInputController})

**Parameters**

| Name                    | Type                                    | Mandatory  | Description           |
| ----------------------- | ---------------------------------------- | ---- | --------------- |
| placeholder   | [ResourceStr](ts-types.md#resourcestr)       | No   | Text displayed when there is no input.     |
| text          | [ResourceStr](ts-types.md#resourcestr)       | No   | Current text input.<br>If the component has [stateStyles](ts-universal-attributes-polymorphic-style.md) or any other attribute that may trigger updating configured, you are advised to bind the state variable to the text in real time through the **onChange** event, so as to prevent display errors when the component is updated.<br>Since API version 10, this parameter supports two-way binding through [$$](../../quick-start/arkts-two-way-sync.md).|
| controller<sup>8+</sup> | [TextInputController](#textinputcontroller8) | No   | Text input controller.|


## Attributes

Among the [universal attributes](ts-universal-attributes-size.md) and [universal text attributes](ts-universal-attributes-text-style.md), **fontColor**, **fontSize**, **fontStyle**, **fontWeight**, and **fontFamily** are supported. In addition, the following attributes are supported.

| Name                      | Type                                    | Description                                      |
| ------------------------ | ---------------------------------------- | ---------------------------------------- |
| type                     | [InputType](#inputtype)     | Input box type.<br>Default value: **InputType.Normal**       |
| placeholderColor         | [ResourceColor](ts-types.md#resourcecolor)     | Placeholder text color.<br>The default value follows the theme.  |
| placeholderFont          | [Font](ts-types.md#font) | Placeholder text font.|
| enterKeyType             | [EnterKeyType](#enterkeytype) | Type of the Enter key. Currently, only the default value is supported.<br>Default value: **EnterKeyType.Done**|
| caretColor               | [ResourceColor](ts-types.md#resourcecolor)    | Color of the caret in the text box.<br>Default value: **'#007DFF'**                               |
| maxLength                | number                                   | Maximum number of characters in the text input.                           |
| inputFilter<sup>8+</sup> | {<br>value: [ResourceStr](ts-types.md#resourcestr),<br>error?: (value: string) =&gt; void<br>} | Regular expression for input filtering. Only inputs that comply with the regular expression can be displayed. Other inputs are filtered out. The regular expression can match single characters, but not strings.<br>- **value**: regular expression to set.<br>- **error**: filtered-out content to return when regular expression matching fails.|
| copyOption<sup>9+</sup>  | [CopyOptions](ts-appendix-enums.md#copyoptions9) | Whether copy and paste is allowed.<br>Default value: **CopyOptions.LocalDevice**<br>If this attribute is set to **CopyOptions.None**, the paste operation is allowed, but not the copy or cut operation.|
| showPasswordIcon<sup>9+</sup> | boolean | Whether to display the password icon at the end of the password text box.<br>Default value: **true**|
| style<sup>9+</sup> | [TextInputStyle](#textinputstyle9) \| [TextContentStyle](ts-appendix-enums.md#textcontentstyle10) | Text input style.<br>Default value: **TextInputStyle.Default**|
| textAlign<sup>9+</sup>   | [TextAlign](ts-appendix-enums.md#textalign) | Horizontal alignment of the text.<br>Default value: **TextAlign.Start**<br>**NOTE**<br>Available options are **TextAlign.Start**, **TextAlign.Center**, and **TextAlign.End**.<br>To set vertical alignment for the text, use the [align](ts-universal-attributes-location.md) attribute. The **align** attribute alone does not control the horizontal position of the text. In other words, **Alignment.TopStart**, **Alignment.Top**, and **Alignment.TopEnd** produce the same effect, top-aligning the text; **Alignment.Start**, **Alignment.Center**, and **Alignment.End** produce the same effect, centered-aligning the text vertically; **Alignment.BottomStart**, **Alignment.Bottom**, and **Alignment.BottomEnd** produce the same effect, bottom-aligning the text. |
| selectedBackgroundColor<sup>10+</sup> | [ResourceColor](ts-types.md#resourcecolor) | Background color of the selected text.<br>If the opacity is not set, the color is opaque. For example, **0x80000000** indicates black with 50% opacity.|
| caretStyle<sup>10+</sup> | {<br>width: [Length](ts-types.md#length)<br>} | Caret style.                                       |
| caretPosition<sup>10+</sup> | number | Caret position.|
| showUnit<sup>10+</sup>                |  [CustomBuilder](ts-types.md#CustomBuilder8)         | Unit for content in the component.<br>By default, there is no unit.|
| showError<sup>10+</sup> | string \| undefined | Error text displayed when an error occurs.<br>By default, no error text is displayed.|
| showUnderline<sup>10+</sup> | boolean | Whether to show an underline.<br>Default value: **false**|
| passwordIcon<sup>10+</sup> | [PasswordIcon](#passwordicon10) | Password icon to display at the end of the password text box.<br>By default, the system-provided icon is used.|
| enableKeyboardOnFocus<sup>10+</sup> | boolean | Whether to enable the input method when the component obtains focus.<br>Default value: **true**  |
| selectionMenuHidden<sup>10+</sup> | boolean | Whether to display the text selection menu when the text box is long-pressed or right-clicked.<br>Default value: **false**|

>  **NOTE**
>
>  The default value of the universal attribute [padding](ts-universal-attributes-size.md) is as follows: <br>{<br> top: 8 vp,<br> right: 16 vp,<br> bottom: 8 vp,<br> left: 16 vp<br> }

## EnterKeyType

| Name                 | Description       |
| ------------------- | --------- |
| Go     | The Enter key is labeled "Go."  |
| Search | The Enter key is labeled "Search." |
| Send   | The Enter key is labeled "Send." |
| Next   | The Enter key is labeled "Next."|
| Done   | The Enter key is labeled "Done."    |

## InputType

| Name                | Description           |
| ------------------ | ------------- |
| Normal   | Normal input mode.<br>The value can contain digits, letters, underscores (_), spaces, and special characters.|
| Password | Password input mode. The value can contain digits, letters, underscores (_), spaces, and special characters. An eye icon is used to show or hide the password, and the password is hidden behind dots by default.|
| Email    | Email address input mode. The value can contain digits, letters, underscores (_), and at signs (@). Only one at sign (@) is allowed.|
| Number   | Digit input mode.     |
| PhoneNumber<sup>9+</sup> | Phone number input mode.<br>The value can contain digits, plus signs (+), hyphens (-), asterisks (*), and number signs (#). The length is not limited.|

## TextInputStyle<sup>9+</sup>

| Name                | Description           |
| ------------------ | ------------- |
| Default   | Default style. The caret width is fixed at 1.5 vp, and the caret height is subject to the background height and font size of the selected text.  |
| Inline    | Inline input style. The background height of the selected text is the same as the height of the text box.     |

## PasswordIcon<sup>10+</sup>

| Name      | Type                                              | Mandatory| Description                                              |
| ---------- | -------------------------------------------------- | ---- | -------------------------------------------------- |
| onIconSrc  | string \|[Resource](ts-types.md#resource)| No  | Icon that can be used to hide the password in password input mode.|
| offIconSrc | string \|[Resource](ts-types.md#resource)| No  | Icon that can be used to show the password in password input mode.|

## Events

In addition to the [universal events](ts-universal-events-click.md), the following events are supported.

| Name                                                        | Description                                                    |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| onChange(callback: (value: string) =&gt; void) | Triggered when the input in the text box changes.<br>**value**: text content.<br>This event is triggered when any of the following conditions is met:<br>1. Keyboard input is received.<br>2. Paste and cut is performed.<br>3. Ctrl+V is pressed.|
| onSubmit(callback: (enterKey: EnterKeyType) =&gt; void) | Triggered when the Enter key on the keyboard is pressed. The return value is the current type of the Enter key.<br>**enterKeyType**: type of the Enter key. For details, see [EnterKeyType](#enterkeytype).|
| onEditChanged(callback: (isEditing: boolean) =&gt; void)<sup>(deprecated)</sup> | Triggered when the input status changes. Since API version 8, **onEditChange** is recommended.|
| onEditChange(callback: (isEditing: boolean) =&gt; void)<sup>8+</sup> | Triggered when the input status changes. When the cursor is placed in the text box, it is in the editing state. Otherwise, it is in the non-editing state. If the value of **isEditing** is **true**, text input is in progress.|
| onCopy(callback:(value: string) =&gt; void)<sup>8+</sup> | Triggered when the copy button on the pasteboard, which displays when the text box is long pressed, is clicked.<br>**value**: text to be copied.|
| onCut(callback:(value: string) =&gt; void)<sup>8+</sup> | Triggered when the cut button on the pasteboard, which displays when the text box is long pressed, is clicked.<br>**value**: text to be cut.|
| onPaste(callback:(value: string) =&gt; void)<sup>8+</sup> | Triggered when the paste button on the pasteboard, which displays when the text box is long pressed, is clicked.<br>**value**: text to be pasted.|
| onTextSelectionChange(callback: (selectionStart: number, selectionEnd: number) => void)<sup>10+</sup> | Triggered when the text selection position changes.<br>**selectionStart**: start position of the text selection area. The start position of text in the text box is **0**.<br>**selectionEnd**: end position of the text selection area.|
| onContentScroll(callback: (totalOffsetX: number, totalOffsetY: number) => void)<sup>10+</sup> | Triggered when the text content is scrolled.<br>**totalOffsetX**: X coordinate offset of the text in the content area.<br>**totalOffsetY**: Y coordinate offset of the text in the content area.|

## TextInputController<sup>8+</sup>

Implements the controller of the **\<TextInput>** component.

### Objects to Import
```
controller: TextInputController = new TextInputController()
```
### caretPosition<sup>8+</sup>

caretPosition(value: number): void

Sets the position of the caret.

**Parameters**

| Name| Type| Mandatory| Description                              |
| ------ | -------- | ---- | -------------------------------------- |
| value  | number   | Yes  | Length from the start of the string to the position where the caret is located.|
### setTextSelection<sup>10+</sup>

setTextSelection(selectionStart: number, selectionStart: number): void

Sets the text selection area, which will be highlighted.

**Parameters**

| Name        | Type| Mandatory| Description              |
| -------------- | -------- | ---- | ---------------------- |
| selectionStart | number   | Yes  | Start position of the text selection range. The start position of text in the text box is 0.|
| selectionEnd   | number   | Yes  | End position of the text selection range.|

### stopEditing<sup>10+</sup>

stopEditing(): void

Exits the editing state.

### getTextContentRect<sup>10+</sup>

getTextContentRect(): [RectResult](#rectresult10)

Obtains the position of the edited text area relative to the component and its size. The unit of the return value is pixel.

**Return value**

| Type      | Description      |
| -------------------  | -------- |
| [RectResult](#rectresult10) | Position of the edited text area relative to the component and its size.|

> **NOTE**
>
> - If no text is entered, the return value contains the position information, but the size is 0.
> - The position information is the offset of the first character relative to the editable area.

### RectResult<sup>10+</sup>

Describes the position and size.

| Parameter     | Type    | Description|
| ------- | ------ | ----------------------- |
| x     | number | X coordinate.|
| y     | number | Y coordinate.|
| width | number | Content width.|
| height | number | Content height.|


### getTextContentLineCount<sup>10+</sup>

getTextContentLineCount(): number

Obtains the number of lines of the edited text.

**Return value**

| Type | Description      |
| ----- | -------- |
| number| Number of lines of the edited text.|

## Example

```ts
// xxx.ets
@Entry
@Component
struct TextInputExample {
  @State text: string = ''
  controller: TextInputController = new TextInputController()

  build() {
    Column() {
      TextInput({ text: this.text, placeholder: 'input your word...', controller: this.controller })
        .placeholderColor(Color.Grey)
        .placeholderFont({ size: 14, weight: 400 })
        .caretColor(Color.Blue)
        .width(400)
        .height(40)
        .margin(20)
        .fontSize(14)
        .fontColor(Color.Black)
        .inputFilter('[a-z]', (e) => {
          console.log(JSON.stringify(e))
        })
        .onChange((value: string) => {
          this.text = value
        })
      Text(this.text)
      Button('Set caretPosition 1')
        .margin(15)
        .onClick(() => {
          // Move the caret to after the first entered character.
          this.controller.caretPosition(1)
        })
      // Password text box.
      TextInput({ placeholder: 'input your password...' })
        .width(400)
        .height(40)
        .margin(20)
        .type(InputType.Password)
        .maxLength(9)
        .showPasswordIcon(true)
      // Inline-style text box.
      TextInput({ placeholder: 'inline style' })
        .width(400)
        .height(50)
        .margin(20)
        .borderRadius(0)
        .style(TextInputStyle.Inline)
    }.width('100%')
  }
}
```

![textInput](figures/textInput.gif)
