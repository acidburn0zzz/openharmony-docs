# @ohos.multimodalInput.pointer (Mouse Pointer)

The **pointer** module provides APIs related to pointer attribute management.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.

## Modules to Import

```js
import pointer from '@ohos.multimodalInput.pointer';
```

## pointer.setPointerVisible<sup>9+</sup>

setPointerVisible(visible: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets the visible status of the mouse pointer. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name      | Type                       | Mandatory  | Description                                      |
| -------- | ------------------------- | ---- | ---------------------------------------- |
| visible  | boolean                   | Yes   | Whether the mouse pointer is visible.|
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setPointerVisible(true, (error) => {
    if (error) {
      console.log(`Set pointer visible failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set pointer visible success`);
  });
} catch (error) {
  console.log(`Set pointer visible failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerVisible<sup>9+</sup>

setPointerVisible(visible: boolean): Promise&lt;void&gt;

Sets the visible status of the mouse pointer. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name     | Type     | Mandatory  | Description                                      |
| ------- | ------- | ---- | ---------------------------------------- |
| visible | boolean | Yes   | Whether the mouse pointer is visible.|

**Return value**

| Name                 | Description                 |
| ------------------- | ------------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.setPointerVisible(false).then(() => {
    console.log(`Set pointer visible success`);
  });
} catch (error) {
  console.log(`Set pointer visible failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.isPointerVisible<sup>9+</sup>

isPointerVisible(callback: AsyncCallback&lt;boolean&gt;): void

Checks the visible status of the mouse pointer. This API uses an asynchronous callback to return the result. 

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name      | Type                          | Mandatory  | Description            |
| -------- | ---------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;boolean&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.isPointerVisible((error, visible) => {
    if (error) {
      console.log(`Get pointer visible failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Get pointer visible success, visible: ${JSON.stringify(visible)}`);
  });
} catch (error) {
  console.log(`Get pointer visible failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.isPointerVisible<sup>9+</sup>

isPointerVisible(): Promise&lt;boolean&gt;

Checks the visible status of the mouse pointer. This API uses a promise to return the result. 

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Return value**

| Name                    | Description                 |
| ---------------------- | ------------------- |
| Promise&lt;boolean&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.isPointerVisible().then((visible) => {
    console.log(`Get pointer visible success, visible: ${JSON.stringify(visible)}`);
  });
} catch (error) {
  console.log(`Get pointer visible failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSpeed<sup>9+</sup>

setPointerSpeed(speed: number, callback: AsyncCallback&lt;void&gt;): void

Sets the mouse movement speed. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| speed    | number                    | Yes   | Mouse movement speed. The value ranges from **1** to **11**. The default value is **5**.  |
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setPointerSpeed(5, (error) => {
    if (error) {
      console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set pointer speed success`);
  });
} catch (error) {
  console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setPointerSpeed<sup>9+</sup>

setPointerSpeed(speed: number): Promise&lt;void&gt;

Sets the mouse movement speed. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| speed | number | Yes   | Mouse movement speed. The value ranges from **1** to **11**. The default value is **5**.|

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.setPointerSpeed(5).then(() => {
    console.log(`Set pointer speed success`);
  });
} catch (error) {
  console.log(`Set pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSpeed<sup>9+</sup>

getPointerSpeed(callback: AsyncCallback&lt;number&gt;): void

Obtains the mouse movement speed. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getPointerSpeed((error, speed) => {
    if (error) {
      console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Get pointer speed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerSpeed<sup>9+</sup>

getPointerSpeed(): Promise&lt;number&gt;

Obtains the mouse movement speed. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.getPointerSpeed().then(speed => {
    console.log(`Get pointer speed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`Get pointer speed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setHoverScrollState<sup>10+</sup>

setHoverScrollState(state: boolean, callback: AsyncCallback&lt;void&gt;): void

Sets the status of the mouse hover scroll switch. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state    | boolean                    | Yes   | Status of the mouse hover scroll switch.  |
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setHoverScrollState(true, (error) => {
    if (error) {
      console.log(`Set the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set the mouse hover scroll success`);
  });
} catch (error) {
  console.log(`Set the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setHoverScrollState<sup>10+</sup>

setHoverScrollState(state: boolean): Promise&lt;void&gt;

Sets the status of the mouse hover scroll switch. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean | Yes   | Status of the mouse hover scroll switch.|

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.setHoverScrollState(true).then(() => {
    console.log(`Set the mouse hover scroll success`);
  });
} catch (error) {
  console.log(`Set the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getHoverScrollState<sup>10+</sup>

getHoverScrollState(callback: AsyncCallback&lt;boolean&gt;): void

Obtains the status of the mouse hover scroll switch. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;boolean&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getHoverScrollState((error, state) => {
    console.log(`Get the mouse hover scroll success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`Get the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getHoverScrollState<sup>10+</sup>

getHoverScrollState(): Promise&lt;boolean&gt;

Obtains the status of the mouse hover scroll switch. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise&lt;boolean&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.getHoverScrollState().then((state) => {
    console.log(`Get the mouse hover scroll success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`Get the mouse hover scroll failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMousePrimaryButton<sup>10+</sup>

setMousePrimaryButton(primary: PrimaryButton, callback: AsyncCallback&lt;void&gt;): void

Sets the primary button of the mouse. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type                     | Mandatory | Description                                   |
| -------- | ------------------------- | ----  | ------------------------------------- |
| primary  | [PrimaryButton](#primarybutton10)   | Yes   | ID of the primary mouse button.  |
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setMousePrimaryButton(pointer.PrimaryButton.RIGHT, (error) => {
    if (error) {
      console.log(`Set mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`Set mouse primary button success`);
  });
} catch (error) {
  console.log(`Set mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMousePrimaryButton<sup>10+</sup>

setMousePrimaryButton(primary: PrimaryButton): Promise&lt;void&gt;

Sets the primary button of the mouse. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| primary | [PrimaryButton](#primarybutton10) | Yes   | ID of the primary mouse button.|

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.setMousePrimaryButton(pointer.PrimaryButton.RIGHT).then(() => {
    console.log(`Set mouse primary button success`);
  });
} catch (error) {
  console.log(`Set mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMousePrimaryButton<sup>10+</sup>

getMousePrimaryButton(callback: AsyncCallback&lt;PrimaryButton&gt;): void

Obtains the primary button of the mouse. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;[PrimaryButton](#primarybutton10)&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getMousePrimaryButton((error, primary) => {
    console.log(`Get mouse primary button success, primary: ${JSON.stringify(primary)}`);
  });
} catch (error) {
  console.log(`Get mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMousePrimaryButton<sup>10+</sup>

getMousePrimaryButton(): Promise&lt;PrimaryButton&gt;

Obtains the primary button of the mouse. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise&lt;[PrimaryButton](#primarybutton10)&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.getMousePrimaryButton().then((primary) => {
    console.log(`Get mouse primary button success, primary: ${JSON.stringify(primary)}`);
  });
} catch (error) {
  console.log(`Get mouse primary button failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## PrimaryButton<sup>10+</sup>

Type of the primary mouse button.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

| Name                              | Value   | Description    |
| -------------------------------- | ---- | ------ |
| LEFT                          | 0    | Left mouse button.    |
| RIGHT                             | 1    | Right mouse button.  |

## pointer.setMouseScrollRows<sup>10+</sup>

setMouseScrollRows(rows: number, callback: AsyncCallback&lt;void&gt;): void

Sets the number of mouse scroll rows. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| rows     | number                    | Yes   | Number of mouse scroll rows. The value ranges from 1 to 100. The default value is **3**.  |
| callback | AsyncCallback&lt;void&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setMouseScrollRows(1, (error) => {
    if (error) {
      console.log(`setMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setMouseScrollRows success`);
  });
} catch (error) {
  console.log(`setMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setMouseScrollRows<sup>10+</sup>

setMouseScrollRows(rows: number): Promise&lt;void&gt;

Sets the number of mouse scroll rows. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| rows  | number | Yes   | Number of mouse scroll rows. The value ranges from 1 to 100. The default value is **3**.|

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise&lt;void&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.setMouseScrollRows(20).then(() => {
    console.log(`setMouseScrollRows success`);
  });
} catch (error) {
  console.log(`setMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMouseScrollRows<sup>10+</sup>

getMouseScrollRows(callback: AsyncCallback&lt;number&gt;): void

Obtains the number of mouse scroll rows. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback&lt;number&gt; | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getMouseScrollRows((error, rows) => {
    console.log(`getMouseScrollRows success, rows: ${JSON.stringify(rows)}`);
  });
} catch (error) {
  console.log(`getMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getMouseScrollRows<sup>10+</sup>

getMouseScrollRows(): Promise&lt;number&gt;

Obtains the mouse movement speed. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise&lt;number&gt; | Promise used to return the result.|

**Example**

```js
try {
  pointer.getMouseScrollRows().then((rows) => {
    console.log(`getMouseScrollRows success, rows: ${JSON.stringify(rows)}`);
  });
} catch (error) {
  console.log(`getMouseScrollRows failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getPointerStyle<sup>9+</sup>

getPointerStyle(windowId: number, callback: AsyncCallback&lt;PointerStyle&gt;): void

Obtains the mouse pointer style. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name      | Type                                      | Mandatory  | Description            |
| -------- | ---------------------------------------- | ---- | -------------- |
| windowId | number                                   | Yes   | Window ID.   |
| callback | AsyncCallback&lt;[PointerStyle](#pointerstyle9)&gt; | Yes   | Callback used to return the result.|

**Example**

```js
import window from '@ohos.window';

window.getLastWindow(this.context, (error, win) => {
  if (error.code) {
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    return;
  }
  let windowId = win.getWindowProperties().id;
  if (windowId < 0) {
    console.log(`Invalid windowId`);
    return;
  }
  try {
    pointer.getPointerStyle(windowId, (error, style) => {
      console.log(`Get pointer style success, style: ${JSON.stringify(style)}`);
    });
  } catch (error) {
    console.log(`Get pointer style failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
  }
});
```

## pointer.getPointerStyle<sup>9+</sup>

getPointerStyle(windowId: number): Promise&lt;PointerStyle&gt;

Obtains the mouse pointer style. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name    | Type  | Mandatory| Description    |
| -------- | ------ | ---- | -------- |
| windowId | number | Yes  | Window ID.|

**Return value**

| Name                                      | Description                 |
| ---------------------------------------- | ------------------- |
| Promise&lt;[PointerStyle](#pointerstyle9)&gt; | Promise used to return the result.|

**Example**

```js
import window from '@ohos.window';

window.getLastWindow(this.context, (error, win) => {
  if (error.code) {
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    return;
  }
  let windowId = win.getWindowProperties().id;
  if (windowId < 0) {
    console.log(`Invalid windowId`);
    return;
  }
  try {
    pointer.getPointerStyle(windowId).then((style) => {
      console.log(`Get pointer style success, style: ${JSON.stringify(style)}`);
    });
  } catch (error) {
    console.log(`Get pointer style failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
  }
});
```

## pointer.setPointerStyle<sup>9+</sup>

setPointerStyle(windowId: number, pointerStyle: PointerStyle, callback: AsyncCallback&lt;void&gt;): void

Sets the mouse pointer style. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name          | Type                            | Mandatory  | Description                                 |
| ------------ | ------------------------------ | ---- | ----------------------------------- |
| windowId     | number                         | Yes   | Window ID.                         |
| pointerStyle | [PointerStyle](#pointerstyle9) | Yes   | Mouse pointer style ID.                            |
| callback     | AsyncCallback&lt;void&gt;      | Yes   | Callback used to return the result.|

**Example**

```js
import window from '@ohos.window';

window.getLastWindow(this.context, (error, win) => {
  if (error.code) {
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    return;
  }
  let windowId = win.getWindowProperties().id;
  if (windowId < 0) {
    console.log(`Invalid windowId`);
    return;
  }
  try {
    pointer.setPointerStyle(windowId, pointer.PointerStyle.CROSS, error => {
      console.log(`Set pointer style success`);
    });
  } catch (error) {
    console.log(`Set pointer style failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
  }
});
```
## pointer.setPointerStyle<sup>9+</sup>

setPointerStyle(windowId: number, pointerStyle: PointerStyle): Promise&lt;void&gt;

Sets the mouse pointer style. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**Parameters**

| Name                 | Type                            | Mandatory  | Description              |
| ------------------- | ------------------------------ | ---- | ---------------- |
| windowId            | number                         | Yes   | Window ID.      |
| pointerStyle        | [PointerStyle](#pointerstyle9) | Yes   | Mouse pointer style ID.         |
| Promise&lt;void&gt; | void                           | Yes   | Promise used to return the result.|

**Example**

```js
import window from '@ohos.window';

window.getLastWindow(this.context, (error, win) => {
  if (error.code) {
    console.error('Failed to obtain the top window. Cause: ' + JSON.stringify(error));
    return;
  }
  let windowId = win.getWindowProperties().id;
  if (windowId < 0) {
    console.log(`Invalid windowId`);
    return;
  }
  try {
    pointer.setPointerStyle(windowId, pointer.PointerStyle.CROSS).then(() => {
      console.log(`Set pointer style success`);
    });
  } catch (error) {
    console.log(`Set pointer style failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
  }
});
```
## PointerStyle<sup>9+</sup>

Enumerates mouse pointer styles.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

| Name                              | Value   | Description    |Legend|
| -------------------------------- | ---- | ------ |------ |
| DEFAULT                          | 0    | Default     |![Default.png](./figures/Default.png)|
| EAST                             | 1    | East arrow  |![East.png](./figures/East.png)|
| WEST                             | 2    | West arrow  |![West.png](./figures/West.png)|
| SOUTH                            | 3    | South arrow  |![South.png](./figures/South.png)|
| NORTH                            | 4    | North arrow  |![North.png](./figures/North.png)|
| WEST_EAST                        | 5    | West-east arrow |![West_East.png](./figures/West_East.png)|
| NORTH_SOUTH                      | 6    | North-south arrow |![North_South.png](./figures/North_South.png)|
| NORTH_EAST                       | 7    | North-east arrow |![North_East.png](./figures/North_East.png)|
| NORTH_WEST                       | 8    | North-west arrow |![North_West.png](./figures/North_West.png)|
| SOUTH_EAST                       | 9    | South-east arrow |![South_East.png](./figures/South_East.png)|
| SOUTH_WEST                       | 10   | South-west arrow |![South_West.png](./figures/South_West.png)|
| NORTH_EAST_SOUTH_WEST            | 11   | North-east and south-west adjustment|![North_East_South_West.png](./figures/North_East_South_West.png)|
| NORTH_WEST_SOUTH_EAST            | 12   | North-west and south-east adjustment|![North_West_South_East.png](./figures/North_West_South_East.png)|
| CROSS                            | 13   | Cross (accurate selection)  |![Cross.png](./figures/Cross.png)|
| CURSOR_COPY                      | 14   | Copy cursor    |![Copy.png](./figures/Copy.png)|
| CURSOR_FORBID                    | 15   | Forbid cursor   |![Forbid.png](./figures/Forbid.png)|
| COLOR_SUCKER                     | 16   | Sucker    |![Colorsucker.png](./figures/Colorsucker.png)|
| HAND_GRABBING                    | 17   | Grabbing hand  |![Hand_Grabbing.png](./figures/Hand_Grabbing.png)|
| HAND_OPEN                        | 18   | Opening hand  |![Hand_Open.png](./figures/Hand_Open.png)|
| HAND_POINTING                    | 19   | Hand-shaped pointer  |![Hand_Poniting.png](./figures/Hand_Pointing.png)|
| HELP                             | 20   | Help   |![Help.png](./figures/Help.png)|
| MOVE                             | 21   | Move    |![Move.png](./figures/Move.png)|
| RESIZE_LEFT_RIGHT                | 22   | Left and right resizing|![Resize_Left_Right.png](./figures/Resize_Left_Right.png)|
| RESIZE_UP_DOWN                   | 23   | Up and down resizing|![Resize_Up_Down.png](./figures/Resize_Up_Down.png)|
| SCREENSHOT_CHOOSE                | 24   | Screenshot crosshair|![Screenshot_Cross.png](./figures/Screenshot_Cross.png)|
| SCREENSHOT_CURSOR                | 25   | Screenshot cursor    |![Screenshot_Cursor.png](./figures/Screenshot_Cursor.png)|
| TEXT_CURSOR                      | 26   | Text cursor  |![Text_Cursor.png](./figures/Text_Cursor.png)|
| ZOOM_IN                          | 27   | Zoom in    |![Zoom_In.png](./figures/Zoom_In.png)|
| ZOOM_OUT                         | 28   | Zoom out    |![Zoom_Out.png](./figures/Zoom_Out.png)|
| MIDDLE_BTN_EAST                  | 29   | Scrolling east  |![MID_Btn_East.png](./figures/MID_Btn_East.png)|
| MIDDLE_BTN_WEST                  | 30   | Scrolling west  |![MID_Btn_West.png](./figures/MID_Btn_West.png)|
| MIDDLE_BTN_SOUTH                 | 31   | Scrolling south  | ![MID_Btn_South.png](./figures/MID_Btn_South.png)            |
| MIDDLE_BTN_NORTH                 | 32   | Scrolling north  |![MID_Btn_North.png](./figures/MID_Btn_North.png)|
| MIDDLE_BTN_NORTH_SOUTH           | 33   | Scrolling north-south |![MID_Btn_North_South.png](./figures/MID_Btn_North_South.png)|
| MIDDLE_BTN_NORTH_EAST            | 34   | Scrolling north-east |![MID_Btn_North_East.png](./figures/MID_Btn_North_East.png)|
| MIDDLE_BTN_NORTH_WEST            | 35   | Scrolling north-west |![MID_Btn_North_West.png](./figures/MID_Btn_North_West.png)|
| MIDDLE_BTN_SOUTH_EAST            | 36   | Scrolling south-east |![MID_Btn_South_East.png](./figures/MID_Btn_South_East.png)|
| MIDDLE_BTN_SOUTH_WEST            | 37   | Scrolling south-west |![MID_Btn_South_West.png](./figures/MID_Btn_South_West.png)|
| MIDDLE_BTN_NORTH_SOUTH_WEST_EAST | 38   | Moving as a cone in four directions|![MID_Btn_North_South_West_East.png](./figures/MID_Btn_North_South_West_East.png)|
| HORIZONTAL_TEXT_CURSOR<sup>10+</sup> | 39 | Horizontal text selection|![Horizontal_Text_Cursor.png](./figures/Horizontal_Text_Cursor.png)|
| CURSOR_CROSS<sup>10+</sup> | 40 | Cross cursor|![Cursor_Cross.png](./figures/Cursor_Cross.png)|
| CURSOR_CIRCLE<sup>10+</sup> | 41 | Circular cursor|![Cursor_Circle.png](./figures/Cursor_Circle.png)|

## pointer.setTouchpadScrollSwitch<sup>10+</sup>

setTouchpadScrollSwitch(state: boolean, callback: AsyncCallback\<void>): void

Sets the scroll switch of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | Yes   | Scroll switch status. The value **true** indicates that the scroll switch is enabled, and the value **false** indicates the opposite. The default value is **true**.  |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadScrollSwitch(true, (error) => {
    if (error) {
      console.log(`setTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadScrollSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollSwitch<sup>10+</sup>

setTouchpadScrollSwitch(state: boolean): Promise\<void>

Sets the scroll switch of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| Yes   |  Scroll switch status. The value **true** indicates that the scroll switch is enabled, and the value **false** indicates the opposite. The default value is **true**.|

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadScrollSwitch(false).then(() => {
    console.log(`setTouchpadScrollSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollSwitch<sup>10+</sup>

getTouchpadScrollSwitch(callback:  AsyncCallback\<boolean>): void

Obtains the scroll switch status of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadScrollSwitch ((error, state) => {
    console.log(`getTouchpadScrollSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollSwitch<sup>10+</sup>

getTouchpadScrollSwitch(): Promise\<boolean>

Obtains the scroll switch status of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadScrollSwitch().then((state) => {
    console.log(`getTouchpadScrollSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollDirection<sup>10+</sup>

setTouchpadScrollDirection(state: boolean, callback: AsyncCallback\<void>): void

Sets the scroll direction of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | Yes   | Scroll direction of the touchpad. The value **true** indicates that the scroll direction is the same as the finger moving direction, and the value **false** indicates the opposite. The default value is **true**.  |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadScrollDirection(true, (error) => {
    if (error) {
      console.log(`setTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadScrollDirection success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadScrollDirection<sup>10+</sup>

setTouchpadScrollDirection(state: boolean): Promise\<void>

Sets the scroll direction of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| Yes   |  Scroll direction of the touchpad. The value **true** indicates that the scroll direction is the same as the finger moving direction, and the value **false** indicates the opposite. The default value is **true**.    |

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadScrollDirection (false).then(() => {
    console.log(`setTouchpadScrollDirection success`);
  });
} catch (error) {
  console.log(`setTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollDirection<sup>10+</sup>

getTouchpadScrollDirection(callback:  AsyncCallback\<boolean>): void

Obtains the scroll direction of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadScrollSwitch ((error, state) => {
    console.log(`getTouchpadScrollDirection success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadScrollDirection<sup>10+</sup>

getTouchpadScrollDirection(): Promise\<boolean>

Obtains the scroll direction of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadScrollDirection().then((state) => {
    console.log(`getTouchpadScrollDirection success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadScrollDirection failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadTapSwitch<sup>10+</sup>

setTouchpadTapSwitch(state: boolean, callback: AsyncCallback\<void>): void

Sets the tap switch of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | Yes   |Tap switch status of the touchpad The value **true** indicates that the tap switch is enabled, and the value **false** indicates the opposite. The default value is **true**.  |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadTapSwitch(true, (error) => {
    if (error) {
      console.log(`setTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadTapSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadTapSwitch <sup>10+</sup>

setTouchpadTapSwitch(state: boolean): Promise\<void>

Sets the tap switch of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| Yes   |  Tap switch status of the touchpad The value **true** indicates that the tap switch is enabled, and the value **false** indicates the opposite. The default value is **true**. |

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadTapSwitch(false).then(() => {
    console.log(`setTouchpadTapSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadTapSwitch<sup>10+</sup>

getTouchpadTapSwitch(callback:  AsyncCallback\<boolean>): void

Obtains the tap switch status of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadTapSwitch((error, state) => {
    console.log(`getTouchpadTapSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadTapSwitch<sup>10+</sup>

getTouchpadTapSwitch(): Promise\<boolean>

Obtains the tap switch status of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadTapSwitch().then((state) => {
    console.log(`getTouchpadTapSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadTapSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPointerSpeed<sup>10+</sup>

setTouchpadPointerSpeed(speed: number, callback: AsyncCallback\<void>): void

Sets the cursor moving speed of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| speed | number                    | Yes   |Cursor moving speed of the touchpad. The value range is [1,11]. The default value is **5**. |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadPointerSpeed(1, (error) => {
    if (error) {
      console.log(`setTouchpadPointerSpeedfailed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadPointerSpeed success`);
  });
} catch (error) {
  console.log(`setTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPointerSpeed<sup>10+</sup>

setTouchpadPointerSpeed(speed: number): Promise\<void>

Sets the cursor moving speed of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| speed| number | Yes   | Cursor moving speed of the touchpad. The value range is [1,11]. The default value is **5**.   |

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadPointerSpeed(10).then(() => {
    console.log(`setTouchpadPointerSpeed success`);
  });
} catch (error) {
  console.log(`setTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPointerSpeed<sup>10+</sup>

getTouchpadPointerSpeed(callback: AsyncCallback\<number>): void

Obtains the cursor moving speed of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<number> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadPointerSpeed((error, speed) => {
    console.log(`getTouchpadPointerSpeed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`getTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPointerSpeed<sup>10+</sup>

getTouchpadPointerSpeed(): Promise\<number>

Obtains the cursor moving speed of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<number> | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadPointerSpeed().then((speed) => {
    console.log(`getTouchpadPointerSpeed success, speed: ${JSON.stringify(speed)}`);
  });
} catch (error) {
  console.log(`getTouchpadPointerSpeed failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPinchSwitch<sup>10+</sup>

setTouchpadPinchSwitch(state: boolean, callback: AsyncCallback\<void>): void

Sets the pinch switch of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | Yes   |Pinch switch status of the touchpad. The value **true** indicates that the pinch switch is enabled, and the value **false** indicates the opposite. The default value is **true**.  |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadTapSwitch(true, (error) => {
    if (error) {
      console.log(`setTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadPinchSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadPinchSwitch<sup>10+</sup>

setTouchpadPinchSwitch(state: boolean): Promise\<void>

Sets the pinch switch of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| Yes   |  Pinch switch status of the touchpad. The value **true** indicates that the pinch switch is enabled, and the value **false** indicates the opposite. The default value is **true**. |

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadPinchSwitch(false).then(() => {
    console.log(`setTouchpadPinchSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPinchSwitch<sup>10+</sup>

getTouchpadPinchSwitch(callback:  AsyncCallback\<boolean>): void

Obtains the pinch switch status of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadPinchSwitch((error, state) => {
    console.log(`getTouchpadPinchSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadPinchSwitch<sup>10+</sup>

getTouchpadPinchSwitch(): Promise\<boolean>

Obtains the pinch switch status of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadPinchSwitch().then((state) => {
    console.log(`getTouchpadPinchSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadPinchSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadSwipeSwitch<sup>10+</sup>

setTouchpadSwipeSwitch(state: boolean, callback: AsyncCallback\<void>): void

Sets the multi-finger swipe switch of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| state | boolean | Yes   |Swipe switch status of the touchpad. The value **true** indicates that the swipe switch is enabled, and the value **false** indicates the opposite. The default value is **true**.  |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadSwipeSwitch(true, (error) => {
    if (error) {
      console.log(`setTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadSwipeSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadSwipeSwitch<sup>10+</sup>

setTouchpadSwipeSwitch(state: boolean): Promise\<void>

Sets the swipe switch of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| state | boolean| Yes   |  Swipe switch status of the touchpad. The value **true** indicates that the swipe switch is enabled, and the value **false** indicates the opposite. The default value is **true**. |

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadSwipeSwitch(false).then(() => {
    console.log(`setTouchpadSwipeSwitch success`);
  });
} catch (error) {
  console.log(`setTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadSwipeSwitch<sup>10+</sup>

getTouchpadSwipeSwitch(callback:  AsyncCallback\<boolean>): void

Obtains the multi-finger swipe switch status of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<boolean> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadSwipeSwitch((error, state) => {
    console.log(`getTouchpadSwipeSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadSwipeSwitch<sup>10+</sup>

getTouchpadSwipeSwitch(): Promise\<boolean>

Obtains the multi-finger swipe switch status of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<boolean> | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadSwipeSwitch().then((state) => {
    console.log(`getTouchpadSwipeSwitch success, state: ${JSON.stringify(state)}`);
  });
} catch (error) {
  console.log(`getTouchpadSwipeSwitch failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## RightClickType<sup>10+</sup>

Enumerates shortcut menu triggering modes.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

| Name                              | Value   | Description    |
| -------------------------------- | ---- | ------ |
| TOUCHPAD_RIGHT_BUTTON            | 1    |Tapping the right-button area of the touchpad.|
| TOUCHPAD_LEFT_BUTTON            | 2    |Tapping the left-button area of the touchpad.|
| TOUCHPAD_TWO_FINGER_TAP         | 3    |Tapping or pressing the touchpad with two fingers.|

## pointer.setTouchpadRightClickType<sup>10+</sup>

setTouchpadRightClickType(type: RightClickType, callback: AsyncCallback\<void>): void

Sets the shortcut menu type of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                       | Mandatory  | Description                                   |
| -------- | ------------------------- | ---- | ------------------------------------- |
| type| RightClickType| Yes   |Shortcut menu type of the touchpad.<br>- TOUCHPAD_RIGHT_BUTTON: tapping the right-button area of the touchpad.<br>- TOUCHPAD_LEFT_BUTTON: tapping the left-button area of the touchpad.<br>- TOUCHPAD_TWO_FINGER_TAP: tapping or pressing the touchpad with two fingers.<br>The default value is **TOUCHPAD_RIGHT_BUTTON**. |
| callback | AsyncCallback\<void> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadRightClickType(RightClickType::TOUCHPAD_RIGHT_BUTTON , (error) => {
    if (error) {
      console.log(`setTouchpadRightClickType, error: ${JSON.stringify(error, [`code`, `message`])}`);
      return;
    }
    console.log(`setTouchpadRightClickType success`);
  });
} catch (error) {
  console.log(`setTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.setTouchpadRightClickType<sup>10+</sup>

setTouchpadRightClickType(type: RightClickType): Promise\<void>

Sets the shortcut menu type of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name   | Type    | Mandatory  | Description                                 |
| ----- | ------ | ---- | ----------------------------------- |
| type| RightClickType| Yes   | Shortcut menu type of the touchpad.<br>- TOUCHPAD_RIGHT_BUTTON: tapping the right-button area of the touchpad.<br>- TOUCHPAD_LEFT_BUTTON: tapping the left-button area of the touchpad.<br>- TOUCHPAD_TWO_FINGER_TAP: tapping or pressing the touchpad with two fingers.<br>The default value is **TOUCHPAD_RIGHT_BUTTON**.|

**Return value**

| Name                 | Description              |
| ------------------- | ---------------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```js
try {
  pointer.setTouchpadRightClickType(RightClickType::TOUCHPAD_RIGHT_BUTTON ).then(() => {
    console.log(`setTouchpadRightClickType success`);
  });
} catch (error) {
  console.log(`setTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadRightClickType<sup>10+</sup>

getTouchpadRightClickType(callback: AsyncCallback\<RightClickType>): void

Obtains the shortcut menu type of the touchpad. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Parameters**

| Name      | Type                         | Mandatory  | Description            |
| -------- | --------------------------- | ---- | -------------- |
| callback | AsyncCallback\<RightClickType> | Yes   | Callback used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadRightClickType((error, type) => {
    console.log(`getTouchpadRightClickType success, type: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`getTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```

## pointer.getTouchpadRightClickType<sup>10+</sup>

getTouchpadRightClickType(): Promise\<RightClickType>

Obtains the shortcut menu type of the touchpad. This API uses a promise to return the result.

**System capability**: SystemCapability.MultimodalInput.Input.Pointer

**System API**: This is a system API.

**Return value**

| Name                   | Description                 |
| --------------------- | ------------------- |
| Promise\<RightClickType > | Promise used to return the result.|

**Example**

```js
try {
  pointer.getTouchpadRightClickType().then((type) => {
    console.log(`getTouchpadRightClickType success, typeed: ${JSON.stringify(type)}`);
  });
} catch (error) {
  console.log(`getTouchpadRightClickType failed, error: ${JSON.stringify(error, [`code`, `message`])}`);
}
```
