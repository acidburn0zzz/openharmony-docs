# Application Permission List

Before applying for required permissions, read and understand the [permission workflows](accesstoken-overview.md#permission-workflows). Then, determine the permissions required for your application.

For details about how to apply for required permissions, see [Permission Application Guide](accesstoken-guidelines.md).

## ohos.permission.USE_BLUETOOTH

Allows an application to access Bluetooth configurations.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.DISCOVER_BLUETOOTH

Allows an application to configure Bluetooth on a device, initiate or cancel a scan for Bluetooth devices, and pair with Bluetooth devices.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_BLUETOOTH

Allows an application to pair with a Bluetooth device and access the Contacts or messages of the device.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_BLUETOOTH

Allows an application to access Bluetooth and use Bluetooth capabilities, such as pairing and connecting to peripheral devices.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable ACL**: FALSE

## ohos.permission.INTERNET

Allows an application to access the Internet.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MODIFY_AUDIO_SETTINGS

Allows an application to modify audio settings.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_NOTIFICATION_POLICY

Allows an application to access the notification policy on the device.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.GET_TELEPHONY_STATE

Allows an application to read telephony information. 

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.REQUIRE_FORM

Allows an application to obtain the Ability Form.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_NETWORK_INFO

Allows an application to obtain network information.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PLACE_CALL

Allows an application to make calls without starting the dialer.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_NETWORK_INFO

Allows an application to set data network information.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.REMOVE_CACHE_FILES

Allows the cache of the specified application to be cleared.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.REBOOT

Allows an application to restart the device.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.RUNNING_LOCK

Allows an application to obtain a running lock.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_TIME

Allows an application to set the system time.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_TIME_ZONE

Allows an application to set the system time zone.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.DOWNLOAD_SESSION_MANAGER

Allows an application to manage the download sessions.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.COMMONEVENT_STICKY

Allows an application to publish sticky common events.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SYSTEM_FLOAT_WINDOW

Allows an application to be displayed in a floating window on top of other applications.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PRIVACY_WINDOW

Allows an application to set screens that cannot be captured or recorded.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.POWER_MANAGER

Allows an application to hibernate or wake up the device by calling an API.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.REFRESH_USER_ACTION

Allows an application to reset the screen timeout counter when a user input event occurs, such as pressing a key or touching the screen.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.POWER_OPTIMIZATION

Allows an application to set power saving mode, obtain configuration of the power saving mode, and receive notifications of the configuration changes.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.REBOOT_RECOVERY

Allows an application to restart the device and enter Recovery mode.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_LOCAL_ACCOUNTS

Allows an application to manage local user accounts.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS

Allows access between multiple OS accounts.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.VIBRATE

Allows an application to control vibration.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CONNECT_IME_ABILITY

Allows an application to bind the InputMethodAbility.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CONNECT_SCREEN_SAVER_ABILITY

Allows an application to bind the ScreenSaverAbility.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_SCREEN_SAVER

Allows an application to read the screen saver information, such as the list of screen savers that have been installed and the activated one.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_SCREEN_SAVER

Allows an application to modify the screen saver information, such as activating and previewing a screen saver.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_WALLPAPER

Allows an application to set a static wallpaper.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_WALLPAPER

Allows an application to read wallpaper files.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CHANGE_ABILITY_ENABLED_STATE

Allows an application to enable or disable an application or component.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_MISSIONS

Allows an application to obtain information about running processes and mission in a mission stack.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CLEAN_BACKGROUND_PROCESSES

Allows an application to clear background processes based on their bundle names.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.KEEP_BACKGROUND_RUNNING

Allows a Service ability to keep running in the background.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.UPDATE_CONFIGURATION

Allows an application to modify system settings.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.UPDATE_SYSTEM

Allows an application to call the update APIs.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.UPDATE_MIGRATE

Allows data migration during the update process.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.FACTORY_RESET

Allows an application to call the API for restoring factory settings.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GRANT_SENSITIVE_PERMISSIONS

Allows an application to grant sensitive permissions to other applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.REVOKE_SENSITIVE_PERMISSIONS

Allows an application to revoke sensitive permissions granted to other applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_SENSITIVE_PERMISSIONS

Allows an application to obtain the sensitive permissions that have been granted to other applications.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INTERACT_ACROSS_LOCAL_ACCOUNTS_EXTENSION

Allows an application to set the attributes of applications of other users.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.LISTEN_BUNDLE_CHANGE

Allows an application to listen for changes in other applications, when they are installed, updated, or uninstalled.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_BUNDLE_INFO

Allows an application to query information about another application. This permission applies only to third-party applications.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_BUNDLE_INFO_PRIVILEGED

Allows an application to query information about other applications at the same time.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCELEROMETER

Allows an application to read data from an acceleration sensor, uncalibrated acceleration sensor, or linear acceleration sensor.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GYROSCOPE

Allows an application to read data from a gyroscope sensor or uncalibrated gyroscope sensor.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INSTALL_BUNDLE

Allows an application to install and uninstall other applications except enterprise applications, including enterprise InHouse, mobile device management (MDM), and Normal applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_SHORTCUTS

Allows an application to query and start shortcuts of other applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.radio.ACCESS_FM_AM

Allows an application to access radio services.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_TELEPHONY_STATE

Allows an application to change the telephone state.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.START_ABILITIES_FROM_BACKGROUND

Allows an application to start or access other components from the background.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.BUNDLE_ACTIVE_INFO

Allows an application to obtain how long other applications have been running in the foreground or background.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.START_INVISIBLE_ABILITY

Allows an application to start an invisible ability.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.sec.ACCESS_UDID

Allows an application to obtain the Unified Device ID (UDID).

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.LAUNCH_DATA_PRIVACY_CENTER

Allows an application to switch from its privacy statement page to the <b>Data & privacy</b> page.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_MEDIA_RESOURCES

Allows an application to obtain and manage the media resources that are being played on the device.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PUBLISH_AGENT_REMINDER

Allows an application to use agent-powered reminders.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CONTROL_TASK_SYNC_ANIMATOR

Allows an application to use sync task animations.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INPUT_MONITORING

Allows an application to listen for input events. Only the system signed applications can apply for this permission.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_MISSIONS

Allows an application to manage ability mission stacks.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.NOTIFICATION_CONTROLLER

Allows an application to manage and subscribe to notifications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CONNECTIVITY_INTERNAL

Allows an application to obtain network information or modify network settings.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_VPN

Allows an application to start or stop the VPN.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.MANAGE_NET_STRATEGY

Allows an application to obtain network strategy information or modify network strategy settings.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_NETWORK_STATS

Allows an application to obtain historical traffic information and listen for traffic changes.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.SET_ABILITY_CONTROLLER

Allows an application to set the start and stop of an ability.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.USE_USER_IDM

Allows an application to access the system identity credential information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.MANAGE_USER_IDM

Allows an application to use the system identity credential management capability to enroll, modify, and delete PINs, face images, and fingerprints.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_BIOMETRIC

Allows an application to use biometric recognition for identity authentication.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_USER_AUTH_INTERNAL

Allows an application to use the system identity authentication capability to authenticate or identify users.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_PIN_AUTH

Allows a system application to call the PIN input APIs to present a password input dialog box for users.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.GET_RUNNING_INFO

Allows an application to obtain running status information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CLEAN_APPLICATION_DATA

Allows an application to clear application data.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.RUNNING_STATE_OBSERVER

Allows an application to observe the application status.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CAPTURE_SCREEN

Allows an application to take screenshots.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_WIFI_INFO

Allows an application to obtain WLAN information.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_WIFI_INFO_INTERNAL

Allows an application to obtain WLAN information.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_WIFI_INFO

Allows an application to set WLAN devices.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_WIFI_PEERS_MAC

Allows an application to obtain the MAC address of the peer WLAN or Bluetooth device.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_WIFI_LOCAL_MAC

Allows an application to obtain the MAC address of the local WLAN or Bluetooth device.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_WIFI_CONFIG

Allows an application to obtain the WLAN configuration.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_WIFI_CONFIG

Allows an application to set WLAN information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_WIFI_CONNECTION

Allows an application to manage WLAN connections.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_WIFI_HOTSPOT

Allows an application to enable or disable Wi-Fi hotspots.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_ALL_APP_ACCOUNTS

Allows an application to obtain all application account information.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.MANAGE_SECURE_SETTINGS

Allows an application to modify security settings.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_DFX_SYSEVENT

Allows an application to access system event logging data.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_ENTERPRISE_DEVICE_ADMIN

Allows an application to activate the device administrator app.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_ENTERPRISE_INFO

Allows the device administrator application to set enterprise information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SUBSCRIBE_MANAGED_EVENT

Allows the device administrator application to subscribe to management events.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_DATETIME

Allows the device administrator application to set the system time.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_GET_DEVICE_INFO

Allows the device administrator application to obtain device information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_RESET_DEVICE

Allows the device administrator to restore factory settings of the device.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_WIFI

Allows a device administrator application to set and query Wi-Fi information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_GET_NETWORK_INFO

Allows a device administrator application to query network information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_ACCOUNT_POLICY

Allows the device administrator to set account management policies.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_BUNDLE_INSTALL_POLICY

Allows the device administrator to set bundle installation policies.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_NETWORK

Allows the device administrator application to set network information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_MANAGE_SET_APP_RUNNING_POLICY

Allows the device administrator application to set application running policies.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_SCREENOFF_TIME

Allows the device administrator application to set the screen off time.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_INSTALL_BUNDLE

Allows a device administrator application to install and uninstall bundles.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_GET_SETTINGS

Allows a device administrator application to obtain the **Settings** application data.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_MANAGE_CERTIFICATE

Allows a device administrator application to manage certificates.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_RESTRICT_POLICY

Allows a device administrator application to deliver and obtain restriction policies.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_MANAGE_USB

Allows a device administrator application to manage the USB.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_MANAGE_NETWORK

Allows a device administrator application to manage the network.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ENTERPRISE_SET_BROWSER_POLICY

Allows the device to set or cancel browser policies.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.NFC_TAG

Allows an application to read NFC tag information.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.NFC_CARD_EMULATION

Allows an application to implement card emulation.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.PERMISSION_USED_STATS

Allows a system application to access the permission usage records.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.NOTIFICATION_AGENT_CONTROLLER

Allows an application to send agent-powered notifications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ANSWER_CALL

Allows an application to answer incoming calls.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_CALENDAR

Allows an application to read calendar data.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_CALL_LOG

Allows an application to read call logs.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_CELL_MESSAGES

Allows an application to read cell broadcast messages received by the device.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_CONTACTS

Allows an application to read the Contacts.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_MESSAGES

Allows an application to read messages.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.RECEIVE_MMS

Allows an application to receive and process MMS messages.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.RECEIVE_SMS

Allows an application to receive and process SMS messages.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.RECEIVE_WAP_MESSAGES

Allows an application to receive and process WAP messages.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.MICROPHONE

Allows an application to access the microphone.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.SEND_MESSAGES

Allows an application to send messages.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_CALENDAR

Allows an application to add, remove, and modify Calendar events.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_CALL_LOG

Allows an application to add, remove, and modify call logs.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_CONTACTS

Allows an application to add, remove, and modify the Contacts.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.DISTRIBUTED_DATASYNC

Allows an application to exchange data with other devices.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_VOICEMAIL

Allows an application to leave messages in the voice mailbox.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.LOCATION_IN_BACKGROUND

Allows an application running in the background to obtain the device location.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable ACL**: FALSE

## ohos.permission.LOCATION

Allows an application to obtain the device location.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

**Application conditions**: The applications developed using the SDK earlier than API version 9 can directly apply for this permission. For the applications developed using the SDK of API version 9 or later, you need to apply for [ohos.permission.APPROXIMATELY_LOCATION](#ohospermissionapproximately_location) before applying for this permission.

## ohos.permission.APPROXIMATELY_LOCATION

Allows an application to obtain the approximate location information of a device.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable ACL**: FALSE

**Application conditions**: Only applications developed using the SDK of API version 9 or later can apply for this permission.

## ohos.permission.MEDIA_LOCATION

Allows an application to access geographical locations in the user's media file.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.CAMERA

Allows an application to use the camera to take photos and record videos.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_MEDIA

Allows an application to read media files from the user's external storage.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_MEDIA

Allows an application to read media files from and write media files into the user's external storage.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.ACTIVITY_MOTION

Allows an application to read the current workout status of the user.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_HEALTH_DATA

Allows an application to read the health data of the user.

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_DEFAULT_APPLICATION

Allows an application to query default applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_DEFAULT_APPLICATION

Allows an application to set and reset default applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_DISPOSED_APP_STATUS

Allows an application to set and query the application handling state.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_IDS

Allows an application to query the unique identifier of a device.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.DUMP

Allows the basic system information and SA service information to be exported.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.DISTRIBUTED_SOFTBUS_CENTER

Allows networking between different devices.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_DLP_FILE

Allows configuration and management of the permissions on .dlp files.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PROVISIONING_MESSAGE

Allows the Super Device Manager application to be activated.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_SYSTEM_SETTINGS

Allows an application to access or start system **Settings**.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_IMAGEVIDEO

Allows access to the images or video files in a user's directory.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_AUDIO

Allows access to the audio files in a user directory.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_DOCUMENT

Allows access to the files in a user directory.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_IMAGEVIDEO

Allows modification to the images or video files in a user's directory.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_AUDIO

Allows modification to the audio files in a user directory.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_DOCUMENT

Allows modification to the files in a user's directory.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.ABILITY_BACKGROUND_COMMUNICATION

Allows an application to start the Ability component in the background and establish a connection with it.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.securityguard.REPORT_SECURITY_INFO

Allows an application to report risk data for security guard.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.securityguard.REQUEST_SECURITY_MODEL_RESULT

Allows an application to obtain the device risk status.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.securityguard.REQUEST_SECURITY_EVENT_INFO

Allows an application to obtain detailed risk data.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_ACCESSIBILITY_CONFIG

Allows an application to read the accessibility configuration.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.WRITE_ACCESSIBILITY_CONFIG

Allows an application to set the accessibility configuration.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_CERT_MANAGER_INTERNAL

Allows an application to install, uninstall, enable, and disable certificates and credentials.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_CERT_MANAGER

Allows an application to manage private credentials and query certificate status.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_PUSH_SERVICE

Allows an application to access the Ability of the push service.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_APP_PUSH_DATA

Allows the push service to read data from an application.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.WRITE_APP_PUSH_DATA

Allows the push service to write data to an application.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.RECEIVER_STARTUP_COMPLETED

Allows an application to subscribe to the startup broadcast.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.MANAGE_CAMERA_CONFIG

Allows an application to enable or disable cameras globally.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.READ_WHOLE_CALENDAR

Allows an application to read all calendar information.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_WHOLE_CALENDAR

Allows an application to add, remove, or change all Calendar events.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.ENFORCE_USER_IAM

Allows an SA to delete user information from the IAM subsystem without a token.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_AUTH_RESPOOL

Allows an SA to register the executor.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MOUNT_UNMOUNT_MANAGER

Allows an application to mount and unmount external cards.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MOUNT_FORMAT_MANAGER

Allows an application to format external cards.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.STORAGE_MANAGER

Allows an application to call the interfaces of the Storage Manager service to query space statistics and volume information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.BACKUP

Allows an application to have backup and restore capabilities.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CLOUDFILE_SYNC_MANAGER

Allows an application to obtain the device-cloud synchronization management capability.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CLOUDFILE_SYNC

Allows an application to perform device-cloud synchronization.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.FILE_ACCESS_MANAGER

Allows a file management application to access user data files through the FAF.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_AUDIO_CONFIG

Allows an application to mute microphones globally.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_SERVICE_DM

Allows a system application to obtain the authentication and networking capability of distributed devices.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.APP_TRACKING_CONSENT

Allows an application to read the open anonymous device identifier (OAID).

**Permission level**: normal

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.RUN_ANY_CODE

Allows an application to run unsigned code.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PUBLISH_SYSTEM_COMMON_EVENT

Allows an application to publish system common events.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_SCREEN_LOCK_INNER

Allows an application to use the lock screen service to lock the screen, send a screen lock event, and invoke the system event callback.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.PRINT

Allows an application to obtain the print framework capability.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_PRINT_JOB

Allows an application to obtain the capability of managing print tasks.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CHANGE_OVERLAY_ENABLED_STATE

Allows a system application to disable the application with the overlay feature enabled.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CONNECT_CELLULAR_CALL_SERVICE

Allows a system ability (SA) to access the cellular call SA.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.CONNECT_IMS_SERVICE

Allows an SA to access the IMS SA.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_SENSING_WITH_ULTRASOUND

Allows an application to use ultrasonic sensing.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.INSTALL_ENTERPRISE_BUNDLE

Allows an application to install and uninstall enterprise InHouse applications.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PROXY_AUTHORIZATION_URI

Allows the application proxy to authorize the URI.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_INSTALLED_BUNDLE_LIST

Allows an application to obtain the list of installed applications.

**Permission level**: system_basic

**Authorization mode**: user_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_DISTRIBUTED_ACCOUNTS

Allows an application to manage distributed account information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_DISTRIBUTED_ACCOUNTS

Allows an application to obtain distributed account information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_LOCAL_ACCOUNTS

Allows an application to obtain local account information.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.READ_HIVIEW_SYSTEM

Allows an application to access HiView data.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.WRITE_HIVIEW_SYSTEM

Allows an application to modify HiView data.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_CAST_ENGINE_MIRROR

Allows an application to use the mirror projection capability.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.ACCESS_CAST_ENGINE_STREAM

Allows an application to invoke the system resource projection capability.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CLOUDDATA_CONFIG

Allows an application to obtain the device-cloud information of the configuration database.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_SENSOR

Allows an application that cannot directly use the sensor to turn on and off the sensor.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.DEVICE_STANDBY_EXEMPTION

Allows an application to use resources when the system is in standby mode.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.RESTRICT_APPLICATION_ACTIVE

Allows a standby component to publish a customized network limit event.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.UPLOAD_SESSION_MANAGER

Allows an application to manage the upload sessions.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.PREPARE_APP_TERMINATE

Allows an application to perform customized pre-termination actions before being terminated.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_ECOLOGICAL_RULE

Allows the rules for generating the scene code and the matching experience to be set for the manager service.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.GET_SCENE_CODE

Allows an application to obtain the scene code of the specified application.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.FILE_GUARD_MANAGER

Allows an application to scan user directories and set file extended properties.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.SET_FILE_GUARD_POLICY

Allows an application to update the file guard policy.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.securityguard.SET_MODEL_STATE

Allows an application to control the SecurityGuard model switch.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.hsdr.HSDR_ACCESS

Allows an application to access OpenHarmony Security Detection and Response Framework.

**Permission level**: normal

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.SUPPORT_USER_AUTH

Allows an application to interact with the user authentication framework and register ExtensionAbilities.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable ACL**: FALSE

## ohos.permission.ACCESS_BUNDLE_DIR

Allows an application to access the installation directory of another application.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.CAPTURE_VOICE_DOWNLINK_AUDIO

Allows an application to capture the downlink voice audio.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.MANAGE_INTELLIGENT_VOICE

Allows an application to access the intelligent voice service interfaces.

**Permission level**: system_basic

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INSTALL_ENTERPRISE_MDM_BUNDLE

Allows an enterprise MDM bundle to be installed on enterprise devices.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INSTALL_ENTERPRISE_NORMAL_BUNDLE

Allows an enterprise Normal bundle to be installed on enterprise devices.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE

## ohos.permission.INSTALL_SELF_BUNDLE

Allows automatic updates of the enterprise MDM applications on enterprise devices.

**Permission level**: system_core

**Authorization mode**: system_grant

**Enable via ACL**: TRUE
