# @ohos.reminderAgentManager (reminderAgentManager)

The **reminderAgentManager** module provides APIs for publishing scheduled reminders through the reminder agent.

You can use the APIs to create scheduled reminders for countdown timers, calendar events, and alarm clocks. When the created reminders are published, the timing and pop-up notification functions of your application will be taken over by the reminder agent in the background when your application is frozen or exits.

> **NOTE**
>
> The initial APIs of this module are supported since API version 9. Newly added APIs will be marked with a superscript to indicate their earliest API version.


## Modules to Import

```ts
import reminderAgentManager from'@ohos.reminderAgentManager';
```


## reminderAgentManager.publishReminder

publishReminder(reminderReq: ReminderRequest, callback: AsyncCallback\<number>): void

Publishes a reminder through the reminder agent. This API uses an asynchronous callback to return the result. It can be called only when notification is enabled for the application through [Notification.requestEnableNotification](js-apis-notification.md#notificationrequestenablenotification8).

**Required permissions**: ohos.permission.PUBLISH_AGENT_REMINDER

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | reminderReq | [ReminderRequest](#reminderrequest) | Yes| Reminder to be published.|
  | callback | AsyncCallback\<number> | Yes| Callback used to return the published reminder's ID.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700001    | Notification is not enabled. |
| 1700002    | The number of reminders exceeds the limit. |

**Example**
```ts
let timer = {
    reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_TIMER,
    triggerTimeInSeconds: 10
}

try {
    reminderAgentManager.publishReminder(timer, (err, reminderId) => {
        if (err) {
            console.log("callback err code:" + err.code + " message:" + err.message);
        } else {
            console.log("callback, reminderId = " + reminderId);
        }
    });
} catch (error) {
    console.log("publishReminder code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.publishReminder

publishReminder(reminderReq: ReminderRequest): Promise\<number>

Publishes a reminder through the reminder agent. This API uses a promise to return the result. It can be called only when notification is enabled for the application through [Notification.requestEnableNotification](js-apis-notification.md#notificationrequestenablenotification8).

**Required permissions**: ohos.permission.PUBLISH_AGENT_REMINDER

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**
  | Name| Type| Mandatory| Description|
  | -------- | -------- | -------- | -------- |
  | reminderReq | [ReminderRequest](#reminderrequest) | Yes| Reminder to be published.|

**Return value**
  | Type| Description|
  | -------- | -------- |
  | Promise\<number> | Promise used to return the published reminder's ID.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700001    | Notification is not enabled. |
| 1700002    | The number of reminders exceeds the limit. |

**Example**
```ts
let timer = {
    reminderType: reminderAgentManager.ReminderType.REMINDER_TYPE_TIMER,
    triggerTimeInSeconds: 10
}

try {
    reminderAgentManager.publishReminder(timer).then((reminderId) => {
        console.log("promise, reminderId = " + reminderId);
    }).catch(err => {
        console.log("promise err code:" + err.code + " message:" + err.message);
    });
} catch (error) {
    console.log("publishReminder code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.cancelReminder

cancelReminder(reminderId: number, callback: AsyncCallback\<void>): void

Cancels the reminder with the specified ID. This API uses an asynchronous callback to return the cancellation result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| reminderId | number | Yes| ID of the reminder to cancel.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700003    | The reminder does not exist. |
| 1700004    | The bundle name does not exist. |

**Example**

```ts
try {
    reminderAgentManager.cancelReminder(1, (err, data) => {
        if (err) {
            console.log("callback err code:" + err.code + " message:" + err.message);
        } else {
            console.log("cancelReminder callback");
        }
    });
} catch (error) {
    console.log("cancelReminder code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.cancelReminder

cancelReminder(reminderId: number): Promise\<void>

Cancels the reminder with the specified ID. This API uses a promise to return the cancellation result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| reminderId | number | Yes| ID of the reminder to cancel.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void>	 | Promise used to return the result.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700003    | The reminder does not exist. |
| 1700004    | The bundle name does not exist. |

**Example**

```ts
try {
    reminderAgentManager.cancelReminder(1).then(() => {
        console.log("cancelReminder promise");
    }).catch(err => {
        console.log("promise err code:" + err.code + " message:" + err.message);
    });
} catch (error) {
    console.log("cancelReminder code:" + error.code + " message:" + error.message);
};
```

## reminderAgentManager.getValidReminders

getValidReminders(callback: AsyncCallback<Array\<ReminderRequest>>): void


Obtains all valid (not yet expired) reminders set by the current application. This API uses an asynchronous callback to return the reminders.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback\<Array\<[ReminderRequest](#reminderrequest)>> | Yes| Asynchronous callback used to return an array of all valid reminders set by the current application.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700004    | The bundle name does not exist. |

**Example**

```ts
try {
    reminderAgentManager.getValidReminders((err, reminders) => {
        if (err) {
            console.log("callback err code:" + err.code + " message:" + err.message);
        } else {
            console.log("callback, getValidReminders length = " + reminders.length);
            for (let i = 0; i < reminders.length; i++) {
                console.log("getValidReminders = " + reminders[i]);
                console.log("getValidReminders, reminderType = " + reminders[i].reminderType);
                for (let j = 0; j < reminders[i].actionButton.length; j++) {
                    console.log("getValidReminders, actionButton.title = " + reminders[i].actionButton[j].title);
                    console.log("getValidReminders, actionButton.type = " + reminders[i].actionButton[j].type);
                }
                console.log("getValidReminders, wantAgent.pkgName = " + reminders[i].wantAgent.pkgName);
                console.log("getValidReminders, wantAgent.abilityName = " + reminders[i].wantAgent.abilityName);
                console.log("getValidReminders, maxScreenWantAgent.pkgName = " + reminders[i].maxScreenWantAgent.pkgName);
                console.log("getValidReminders, maxScreenWantAgent.abilityName = " + reminders[i].maxScreenWantAgent.abilityName);
                console.log("getValidReminders, ringDuration = " + reminders[i].ringDuration);
                console.log("getValidReminders, snoozeTimes = " + reminders[i].snoozeTimes);
                console.log("getValidReminders, timeInterval = " + reminders[i].timeInterval);
                console.log("getValidReminders, title = " + reminders[i].title);
                console.log("getValidReminders, content = " + reminders[i].content);
                console.log("getValidReminders, expiredContent = " + reminders[i].expiredContent);
                console.log("getValidReminders, snoozeContent = " + reminders[i].snoozeContent);
                console.log("getValidReminders, notificationId = " + reminders[i].notificationId);
                console.log("getValidReminders, slotType = " + reminders[i].slotType);
            }
        }
    })
} catch (error) {
    console.log("getValidReminders code:" + error.code + " message:" + error.message);
};
```

## reminderAgentManager.getValidReminders

getValidReminders(): Promise\<Array\<ReminderRequest>>

Obtains all valid (not yet expired) reminders set by the current application. This API uses a promise to return the reminders.

**System capability**: SystemCapability.Notification.ReminderAgent

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<Array\<[ReminderRequest](#reminderrequest)>> | Promise used to return an array of all valid reminders set by the current application.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700004    | The bundle name does not exist. |

**Example**

```ts
try {
    reminderAgentManager.getValidReminders().then((reminders) => {
        console.log("promise, getValidReminders length = " + reminders.length);
        for (let i = 0; i < reminders.length; i++) {
            console.log("getValidReminders = " + reminders[i]);
            console.log("getValidReminders, reminderType = " + reminders[i].reminderType);
            for (let j = 0; j < reminders[i].actionButton.length; j++) {
                console.log("getValidReminders, actionButton.title = " + reminders[i].actionButton[j].title);
                console.log("getValidReminders, actionButton.type = " + reminders[i].actionButton[j].type);
            }
            console.log("getValidReminders, wantAgent.pkgName = " + reminders[i].wantAgent.pkgName);
            console.log("getValidReminders, wantAgent.abilityName = " + reminders[i].wantAgent.abilityName);
            console.log("getValidReminders, maxScreenWantAgent.pkgName = " + reminders[i].maxScreenWantAgent.pkgName);
            console.log("getValidReminders, maxScreenWantAgent.abilityName = " + reminders[i].maxScreenWantAgent.abilityName);
            console.log("getValidReminders, ringDuration = " + reminders[i].ringDuration);
            console.log("getValidReminders, snoozeTimes = " + reminders[i].snoozeTimes);
            console.log("getValidReminders, timeInterval = " + reminders[i].timeInterval);
            console.log("getValidReminders, title = " + reminders[i].title);
            console.log("getValidReminders, content = " + reminders[i].content);
            console.log("getValidReminders, expiredContent = " + reminders[i].expiredContent);
            console.log("getValidReminders, snoozeContent = " + reminders[i].snoozeContent);
            console.log("getValidReminders, notificationId = " + reminders[i].notificationId);
            console.log("getValidReminders, slotType = " + reminders[i].slotType);
        }
    }).catch(err => {
        console.log("promise err code:" + err.code + " message:" + err.message);
    });
} catch (error) {
    console.log("getValidReminders code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.cancelAllReminders

cancelAllReminders(callback: AsyncCallback\<void>): void

Cancels all reminders set by the current application. This API uses an asynchronous callback to return the cancellation result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700004    | The bundle name does not exist. |

**Example**

```ts
try {
    reminderAgentManager.cancelAllReminders((err, data) =>{
        if (err) {
            console.log("callback err code:" + err.code + " message:" + err.message);
        } else {
            console.log("cancelAllReminders callback")
        }
    })
} catch (error) {
    console.log("cancelAllReminders code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.cancelAllReminders

cancelAllReminders(): Promise\<void>

Cancels all reminders set by the current application. This API uses a promise to return the cancellation result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Error codes**

For details about the error codes, see [reminderAgentManager Error Codes](../errorcodes/errorcode-reminderAgentManager.md).

| ID  | Error Message|
| --------- | ------- |
| 1700004    | The bundle name does not exist. |

**Example**

```ts
try {
    reminderAgentManager.cancelAllReminders().then(() => {
        console.log("cancelAllReminders promise")
    }).catch(err => {
        console.log("promise err code:" + err.code + " message:" + err.message);
    });
} catch (error) {
    console.log("cancelAllReminders code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.addNotificationSlot

addNotificationSlot(slot: NotificationSlot, callback: AsyncCallback\<void>): void

Adds a notification slot. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| slot | [NotificationSlot](js-apis-notification.md#notificationslot) | Yes| Notification slot, whose type can be set.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Example**

```ts
import notification from '@ohos.notification'

let mySlot = {
    type: notification.SlotType.SOCIAL_COMMUNICATION
}
try {
    reminderAgentManager.addNotificationSlot(mySlot, (err, data) => {
        if (err) {
            console.log("callback err code:" + err.code + " message:" + err.message);
        } else {
            console.log("addNotificationSlot callback");
        }
    });
} catch (error) {
    console.log("addNotificationSlot code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.addNotificationSlot

addNotificationSlot(slot: NotificationSlot): Promise\<void>

Adds a notification slot. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| slot | [NotificationSlot](js-apis-notification.md#notificationslot) | Yes| Notification slot, whose type can be set.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```ts
import notification from '@ohos.notification'

let mySlot = {
    type: notification.SlotType.SOCIAL_COMMUNICATION
}
try {
    reminderAgentManager.addNotificationSlot(mySlot).then(() => {
        console.log("addNotificationSlot promise");
    }).catch(err => {
        console.log("promise err code:" + err.code + " message:" + err.message);
    });
} catch (error) {
    console.log("addNotificationSlot code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.removeNotificationSlot

removeNotificationSlot(slotType: notification.SlotType, callback: AsyncCallback\<void>): void

Removes a notification slot of a specified type. This API uses an asynchronous callback to return the result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| slotType | [notification.SlotType](js-apis-notification.md#slottype) | Yes| Type of the notification slot to remove.|
| callback | AsyncCallback\<void> | Yes| Callback used to return the result.|

**Example**

```ts
import notification from '@ohos.notification'

try {
    reminderAgentManager.removeNotificationSlot(notification.SlotType.CONTENT_INFORMATION, (err, data) => {
        if (err) {
            console.log("callback err code:" + err.code + " message:" + err.message);
        } else {
            console.log("removeNotificationSlot callback");
        }
    });
} catch (error) {
    console.log("removeNotificationSlot code:" + error.code + " message:" + error.message);
};
```


## reminderAgentManager.removeNotificationSlot

removeNotificationSlot(slotType: notification.SlotType): Promise\<void>

Removes a notification slot of a specified type. This API uses a promise to return the result.

**System capability**: SystemCapability.Notification.ReminderAgent

**Parameters**

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| slotType | [notification.SlotType](js-apis-notification.md#slottype) | Yes| Type of the notification slot to remove.|

**Return value**

| Type| Description|
| -------- | -------- |
| Promise\<void> | Promise used to return the result.|

**Example**

```ts
import notification from '@ohos.notification'

try {
    reminderAgentManager.removeNotificationSlot(notification.SlotType.CONTENT_INFORMATION).then(() => {
        console.log("removeNotificationSlot promise");
    }).catch(err => {
        console.log("promise err code:" + err.code + " message:" + err.message);
    });
} catch (error) {
    console.log("removeNotificationSlot code:" + error.code + " message:" + error.message);
};
```

## ActionButtonType

Enumerates button types.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Value| Description|
| -------- | -------- | -------- |
| ACTION_BUTTON_TYPE_CLOSE | 0 | Button for closing the reminder.|
| ACTION_BUTTON_TYPE_SNOOZE | 1 | Button for snoozing the reminder.|
| ACTION_BUTTON_TYPE_CUSTOM<sup>10+</sup>  | 2 | Custom button.<br>**System API**: This is a system API and cannot be called by third-party applications.|


## ReminderType

Enumerates reminder types.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Value| Description|
| -------- | -------- | -------- |
| REMINDER_TYPE_TIMER | 0 | Countdown reminder.|
| REMINDER_TYPE_CALENDAR | 1 | Calendar reminder.|
| REMINDER_TYPE_ALARM | 2 | Alarm reminder.|


## ActionButton

Defines a button displayed for the reminder in the notification panel.


**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| title | string | Yes| Text on the button.|
| type | [ActionButtonType](#actionbuttontype) | Yes| Button type.|
| wantAgent<sup>10+</sup> | [WantAgent](#wantagent) | No| Ability information that is displayed after the button is clicked.<br>**System API**: This is a system API and cannot be called by third-party applications.|


## WantAgent

Defines the information about the redirected-to ability.

**System capability**: SystemCapability.Notification.ReminderAgent


| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| pkgName | string | Yes| Name of the target package.|
| abilityName | string | Yes| Name of the target ability.|
| uri<sup>10+</sup> | string | No| URI of the target ability.<br>**System API**: This is a system API and cannot be called by third-party applications.|


## MaxScreenWantAgent

Provides the information about the target package and ability to start automatically when the reminder is displayed in full-screen mode. This API is reserved.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| pkgName | string | Yes| Name of the package that is automatically started when the reminder arrives and the device is not in use.|
| abilityName | string | Yes| Name of the ability that is automatically started when the reminder arrives and the device is not in use.|


## ReminderRequest

Defines the reminder to publish.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| reminderType | [ReminderType](#remindertype) | Yes| Type of the reminder.|
| actionButton<sup></sup> | [ActionButton](#actionbutton) | No| Buttons displayed for the reminder in the notification panel.<br>- For common applications, a maximum of two buttons are supported.<br>- For system applications, a maximum of two buttons are supported in API version 9, and a maximum of three buttons are supported in API version 10 and later versions.|
| wantAgent | [WantAgent](#wantagent) | No| Information about the ability that is redirected to when the reminder is clicked.|
| maxScreenWantAgent | [MaxScreenWantAgent](#maxscreenwantagent) | No| Information about the ability that is automatically started when the reminder arrives. If the device is in use, a notification will be displayed.|
| ringDuration | number | No| Ringing duration, in seconds. The default value is **1**.|
| snoozeTimes | number | No| Number of reminder snooze times. The default value is **0**.|
| timeInterval | number | No| Reminder snooze interval, in seconds. The minimum value is 5 minutes.|
| title | string | No| Reminder title.|
| content | string | No| Reminder content.|
| expiredContent | string | No| Content to be displayed after the reminder expires.|
| snoozeContent | string | No| Content to be displayed when the reminder is snoozing.|
| notificationId | number | No| Notification ID used by the reminder. If there are reminders with the same notification ID, the later one will overwrite the earlier one.|
| slotType | [notification.SlotType](js-apis-notificationManager.md#slottype) | No| Type of the slot used by the reminder.|
| tapDismissed<sup>10+</sup> | boolean | No| Whether the notification is automatically cleared. The value is the same as that of [NotificationRequest.tapDismissed](js-apis-inner-notification-notificationRequest.md#notificationrequest).|
| autoDeletedTime<sup>10+</sup> | number | No| Time when the notification is automatically cleared. The value is the same as that of [NotificationRequest.autoDeletedTime](js-apis-inner-notification-notificationRequest.md#notificationrequest).|


## ReminderRequestCalendar

ReminderRequestCalendar extends ReminderRequest

Defines a reminder for a calendar event.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| dateTime | [LocalDateTime](#localdatetime) | Yes| Reminder time.|
| repeatMonths | Array\<number> | No| Month in which the reminder repeats.|
| repeatDays | Array\<number> | No| Date on which the reminder repeats.|


## ReminderRequestAlarm

ReminderRequestAlarm extends ReminderRequest

Defines a reminder for an alarm.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| hour | number | Yes| Hour portion of the reminder time.|
| minute | number | Yes| Minute portion of the reminder time.|
| daysOfWeek | Array\<number> | No| Days of a week when the reminder repeats. The value ranges from 1 to 7, corresponding to the data from Monday to Sunday.|


## ReminderRequestTimer

ReminderRequestTimer extends ReminderRequest

Defines a reminder for a scheduled timer.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| triggerTimeInSeconds | number | Yes| Number of seconds in the countdown timer.|


## LocalDateTime

Sets the time information for a calendar reminder.

**System capability**: SystemCapability.Notification.ReminderAgent

| Name| Type| Mandatory| Description|
| -------- | -------- | -------- | -------- |
| year | number | Yes| Year.|
| month | number | Yes| Month. The value ranges from 1 to 12.|
| day | number | Yes| Day. The value ranges from 1 to 31.|
| hour | number | Yes| Hour. The value ranges from 0 to 23.|
| minute | number | Yes| Minute. The value ranges from 0 to 59.|
| second | number | No| Second. The value ranges from 0 to 59.|
