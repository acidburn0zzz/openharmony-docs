# @ohos.vibrator (Vibrator)

The **vibrator** module provides APIs for starting or stopping vibration.

> **NOTE**
>
> The initial APIs of this module are supported since API version 8. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import vibrator from '@ohos.vibrator';
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute, callback: AsyncCallback&lt;void&gt;): void

Starts vibration with the specified effect and attribute. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name   | Type                                  | Mandatory| Description                                                      |
| --------- | -------------------------------------- | ---- | :--------------------------------------------------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | Yes  | Vibration effect.                                            |
| attribute | [VibrateAttribute](#vibrateattribute9) | Yes  | Vibration attribute.                                            |
| callback  | AsyncCallback&lt;void&gt;              | Yes  | Callback used to return the result. If the vibration starts, **err** is **undefined**; otherwise, **err** is an error object.|

**Error codes**

For details about the error codes, see [Vibrator Error Codes](../errorcodes/errorcode-vibrator.md).

| ID| Error Message                |
| -------- | ------------------------ |
| 14600101 | Device operation failed. |

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm'
  }, (error) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.startVibration<sup>9+</sup>

startVibration(effect: VibrateEffect, attribute: VibrateAttribute): Promise&lt;void&gt;

Starts vibration with the specified effect and attribute. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name   | Type                                  | Mandatory| Description          |
| --------- | -------------------------------------- | ---- | -------------- |
| effect    | [VibrateEffect](#vibrateeffect9)       | Yes  | Vibration effect.|
| attribute | [VibrateAttribute](#vibrateattribute9) | Yes  | Vibration attribute.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Error codes**

For details about the error codes, see [Vibrator Error Codes](../errorcodes/errorcode-vibrator.md).

| ID| Error Message                |
| -------- | ------------------------ |
| 14600101 | Device operation failed. |

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm'
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode, callback: AsyncCallback&lt;void&gt;): void

Stops vibration in the specified mode. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.                                    |
| callback | AsyncCallback&lt;void&gt;             | Yes  | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  // Start vibration at a fixed duration.
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm'
  }, (error) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}

try {
  // Stop vibration in VIBRATOR_STOP_MODE_TIME mode.
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_TIME, function (error) {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.stopVibration<sup>9+</sup>

stopVibration(stopMode: VibratorStopMode): Promise&lt;void&gt;

Stops vibration in the specified mode. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                    |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  // Start vibration at a fixed duration.
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm'
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}

try {
  // Stop vibration in VIBRATOR_STOP_MODE_TIME mode.
  vibrator.stopVibration(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(() => {
    console.info('Succeed in stopping vibration');
  }, (error) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (err) {
  console.error(`An unexpected error occurred. Code: ${err.code}, message: ${err.message}`);
}
```

## vibrator.stopVibration<sup>10+</sup>

stopVibration(callback: AsyncCallback&lt;void&gt;): void

Stops vibration in all modes. This API uses an asynchronous callback to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                        |
| -------- | ------------------------- | ---- | ------------------------------------------------------------ |
| callback | AsyncCallback&lt;void&gt; | Yes  | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  // Start vibration at a fixed duration.
  vibrator.startVibration({
    type: 'time',
    duration: 1000,
  }, {
    id: 0,
    usage: 'alarm'
  }, (error) => {
    if (error) {
      console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in starting vibration');
  });
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}

try {
  // Stop vibration in all modes.
  vibrator.stopVibration(function (error) {
    if (error) {
      console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
      return;
    }
    console.info('Succeed in stopping vibration');
  })
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## vibrator.stopVibration<sup>10+</sup>

stopVibration(): Promise&lt;void&gt;

Stops vibration in all modes. This API uses a promise to return the result.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Return value**

| Type               | Description         |
| ------------------- | ------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  // Start vibration at a fixed duration.
  vibrator.startVibration({
    type: 'time',
    duration: 1000
  }, {
    id: 0,
    usage: 'alarm'
  }).then(() => {
    console.info('Succeed in starting vibration');
  }, (error) => {
    console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}

try {
  // Stop vibration in all modes.
  vibrator.stopVibration().then(() => {
    console.info('Succeed in stopping vibration');
  }, (error) => {
    console.error(`Failed to stop vibration. Code: ${error.code}, message: ${error.message}`);
  });
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## vibrator.isSupportEffect<sup>10+</sup>

isSupportEffect(effectId: string, callback: AsyncCallback&lt;boolean&gt;): void

Checks whether the passed effect ID is supported. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                        | Mandatory| Description                                                  |
| -------- | ---------------------------- | ---- | ------------------------------------------------------ |
| effectId | string                       | Yes  | Vibration effect ID.                                            |
| callback | AsyncCallback&lt;boolean&gt; | Yes  | Callback used to return the result. The value **true** means that the passed effect ID is supported, and **false** means the opposite.|

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  // Check whether 'haptic.clock.timer' is supported.
  vibrator.isSupportEffect('haptic.clock.timer', function (err, state) {
    if (err) {
      console.error(`Failed to query effect. Code: ${err.code}, message: ${err.message}`);
      return;
    }
    console.info('Succeed in querying effect');
    if (state) {
      try {
        vibrator.startVibration({ // To use startVibration, you must configure the ohos.permission.VIBRATE permission.
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'unknown'
        }, (error) => {
          if (error) {
            console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
          } else {
            console.info('Succeed in starting vibration');
          }
        });
      } catch (error) {
        console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
      }
    }
  })
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## vibrator.isSupportEffect<sup>10+</sup>

isSupportEffect(effectId: string): Promise&lt;boolean&gt;

Checks whether the passed effect ID is supported. This API uses a promise to return the result.

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type  | Mandatory| Description        |
| -------- | ------ | ---- | ------------ |
| effectId | string | Yes  | Vibration effect ID.|

**Return value**

| Type                  | Description                                                     |
| ---------------------- | --------------------------------------------------------- |
| Promise&lt;boolean&gt; | Promise that returns the result. The value **true** means that the passed effect ID is supported, and **false** means the opposite.|

**Example**

```ts
import vibrator from '@ohos.vibrator';

try {
  // Check whether 'haptic.clock.timer' is supported.
  vibrator.isSupportEffect('haptic.clock.timer').then((state) => {
    console.info(`The query result is ${state}`);
    if (state) {
      try {
        vibrator.startVibration({
          type: 'preset',
          effectId: 'haptic.clock.timer',
          count: 1,
        }, {
          usage: 'unknown'
        }).then(() => {
          console.info('Succeed in starting vibration');
        }).catch((error) => {
          console.error(`Failed to start vibration. Code: ${error.code}, message: ${error.message}`);
        });
      } catch (error) {
        console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
      }
    }
  }, (error) => {
    console.error(`Failed to query effect. Code: ${error.code}, message: ${error.message}`);
  })
} catch (error) {
  console.error(`An unexpected error occurred. Code: ${error.code}, message: ${error.message}`);
}
```

## EffectId

Describes the preset vibration effect ID.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name              | Value                  | Description                            |
| ------------------ | -------------------- | -------------------------------- |
| EFFECT_CLOCK_TIMER | "haptic.clock.timer" | Vibration effect of the vibrator when a user adjusts the timer.|


## VibratorStopMode

Enumerates the modes available to stop the vibration.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name                     | Value      | Description                          |
| ------------------------- | -------- | ------------------------------ |
| VIBRATOR_STOP_MODE_TIME   | "time"   | The vibration to stop is in **duration** mode.|
| VIBRATOR_STOP_MODE_PRESET | "preset" | The vibration to stop is in **EffectId** mode.|

## VibrateEffect<sup>9+</sup>

Describes the vibration effect.

**System capability**: SystemCapability.Sensors.MiscDevice

| Type                            | Description                          |
| -------------------------------- | ------------------------------ |
| [VibrateTime](#vibratetime9)     | Vibration with the specified duration.|
| [VibratePreset](#vibratepreset9) | Vibration with a preset effect.|
| [VibrateFromFile<sup>10+</sup>](#vibratefromfile10) | Vibration according to a custom vibration configuration file.|

## VibrateTime<sup>9+</sup>

Describes the vibration with the specified duration.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Type   | Mandatory| Description                          |
| -------- | ------ | ----- | ------------------------------ |
| type     | string |  Yes  | The value **time** means vibration with the specified duration.|
| duration | number |  Yes  | Vibration duration, in ms.        |

## VibratePreset<sup>9+</sup>

Describes the vibration with a preset effect.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Type     | Mandatory| Description                          |
| -------- | -------- | ---- |------------------------------ |
| type     | string   |  Yes | The value **preset** means vibration with the specified effect.|
| effectId | string   |  Yes | Preset vibration effect ID.            |
| count    | number   |  Yes | Number of vibrations to repeat.              |

## VibrateFromFile<sup>10+</sup>

Describes the custom vibration type, which is supported only by certain devices. If a device does not support this vibration type, [an error code indicating unsupported device](../errorcodes/errorcode-universal.md) is returned.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Type      | Mandatory| Description                          |
| -------- | --------  | ---- | ------------------------------ |
| type     | string    |  Yes | The value **file** means vibration according to a vibration configuration file.|
| hapticFd | [HapticFileDescriptor](#hapticfiledescriptor10) | Yes| File descriptor (FD) of the vibration configuration file.|

## HapticFileDescriptor<sup>10+</sup>

Describes the FD of a custom vibration configuration file. Ensure that the file is available, and the parameters in it can be obtained from the sandbox path through the [file management API](js-apis-file-fs.md#fsopen) or from the HAP resource through the [resource management API](js-apis-resource-manager.md#getrawfd9). The use case is as follows: The system triggers vibration according to the sequence set in a configuration file, based on the specified offset and length. For details about the storage format of the vibration sequence, see [Custom Vibration Format](../../device/vibrator-guidelines.md#custom-vibration-format).

**System capability**: SystemCapability.Sensors.MiscDevice

| Name    | Type     |  Mandatory | Description                          |
| -------- | -------- |--------| ------------------------------|
| fd       | number   |  Yes   | FD of the custom vibration configuration file.               |
| offset   | number   |  No   | Offset from the start position of the file, in bytes. The default value is the start position of the file, and the value cannot exceed the valid range of the file.|
| length   | number   |  No   | Resource length, in bytes. The default value is the length from the offset position to the end of the file, and the value cannot exceed the valid range of the file.|

## VibrateAttribute<sup>9+</sup>

Describes the vibration attribute.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name | Type| Mandatory| Description          |
| ----- | ------ | ---- | -------------- |
| id    | number      |  No| Vibrator ID. The default value is 0.    |
| usage | [Usage](#usage9)      | Yes| Vibration scenario.|

## Usage<sup>9+</sup>

Enumerates the vibration scenarios.

**System capability**: SystemCapability.Sensors.MiscDevice

| Name            | Type  | Description                          |
| ---------------- | ------ | ------------------------------ |
| unknown          | string | Unknown scenario, with the lowest priority.|
| alarm            | string | Vibration for alarms.          |
| ring             | string | Vibration for incoming calls.          |
| notification     | string | Vibration for notifications.          |
| communication    | string | Vibration for communication.          |
| touch            | string | Touch vibration scenario.          |
| media            | string | Multimedia vibration scenario.        |
| physicalFeedback | string | Physical feedback vibration scenario.      |
| simulateReality  | string | Simulated reality vibration scenario.      |

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number): Promise&lt;void&gt;

Triggers vibration with the specified duration. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9-1) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type  | Mandatory| Description                  |
| -------- | ------ | ---- | ---------------------- |
| duration | number | Yes  | Vibration duration, in ms.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
vibrator.vibrate(1000).then(() => {
  console.info('Succeed in vibrating');
}, (error) => {
  console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
});
```

## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(duration: number, callback?: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified duration. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                      |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| duration | number                    | Yes  | Vibration duration, in ms.                                    |
| callback | AsyncCallback&lt;void&gt; | No  | Callback used to return the result. If the vibration starts, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
vibrator.vibrate(1000, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId): Promise&lt;void&gt;

Triggers vibration with the specified effect. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9-1) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                 | Mandatory| Description              |
| -------- | --------------------- | ---- | ------------------ |
| effectId | [EffectId](#effectid) | Yes  | Preset vibration effect ID.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER).then(() => {
  console.info('Succeed in vibrating');
}, (error) => {
  console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
});
```


## vibrator.vibrate<sup>(deprecated)</sup>

vibrate(effectId: EffectId, callback?: AsyncCallback&lt;void&gt;): void

Triggers vibration with the specified effect. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.startVibration](#vibratorstartvibration9) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                     | Mandatory| Description                                                      |
| -------- | ------------------------- | ---- | ---------------------------------------------------------- |
| effectId | [EffectId](#effectid)     | Yes  | Preset vibration effect ID.                                        |
| callback | AsyncCallback&lt;void&gt; | No  | Callback used to return the result. If the vibration starts, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
```

## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode): Promise&lt;void&gt;

Stops vibration in the specified mode. This API uses a promise to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.stopVibration](#vibratorstopvibration9-1) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                    |
| -------- | ------------------------------------- | ---- | ------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.|

**Return value**

| Type               | Description                                  |
| ------------------- | -------------------------------------- |
| Promise&lt;void&gt; | Promise that returns no value.|

**Example**

```ts
// Start vibration based on the specified effect ID.
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
// Stop vibration in VIBRATOR_STOP_MODE_PRESET mode.
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET).then(() => {
  console.info('Succeed in stopping');
}, (error) => {
  console.error(`Failed to stop. Code: ${error.code}, message: ${error.message}`);
});
```


## vibrator.stop<sup>(deprecated)</sup>

stop(stopMode: VibratorStopMode, callback?: AsyncCallback&lt;void&gt;): void

Stops vibration in the specified mode. This API uses an asynchronous callback to return the result.

This API is deprecated since API version 9. You are advised to use [vibrator.stopVibration](#vibratorstopvibration9) instead.

**Required permissions**: ohos.permission.VIBRATE

**System capability**: SystemCapability.Sensors.MiscDevice

**Parameters**

| Name  | Type                                 | Mandatory| Description                                                        |
| -------- | ------------------------------------- | ---- | ------------------------------------------------------------ |
| stopMode | [VibratorStopMode](#vibratorstopmode) | Yes  | Mode to stop the vibration.                                    |
| callback | AsyncCallback&lt;void&gt;             | No  | Callback used to return the result. If the vibration stops, **err** is **undefined**; otherwise, **err** is an error object.|

**Example**

```ts
// Start vibration based on the specified effect ID.
vibrator.vibrate(vibrator.EffectId.EFFECT_CLOCK_TIMER, function (error) {
  if (error) {
    console.error(`Failed to vibrate. Code: ${error.code}, message: ${error.message}`);
  } else {
    console.info('Succeed in vibrating');
  }
})
// Stop vibration in VIBRATOR_STOP_MODE_PRESET mode.
vibrator.stop(vibrator.VibratorStopMode.VIBRATOR_STOP_MODE_PRESET, function (error) {
  if (error) {
    console.error(`Failed to stop. Code: ${error.code}, message: ${error.message}`);
  } else {
    onsole.info('Succeed in stopping');
  }
})
```
