# Sending Notifications to the Panel

There are two notification types, that can be triggered by sending a command over mqtt to the panel here are examples for homeassistant scripts:

<details>
<summary>Seperate Page</summary>
<br>

  This is the notification used by the backend for updates, opening it requires to the following commands to the CustomSend Topic:
   
  `pageType popupNotify`
   
  `entityUpdateDetail~internalName~heading~headingColor~button1text~button1color~button2text~tB2Color~notificationText~textColor~sleepTimeout`

  It is possible to exit from the page by sending `exitPopup`
  
Send Message to the Panel combined with a buzzer sound:
   
 ```yaml
nspanel_popup_notification:
  alias: Popup Notification
  sequence:
  - service: mqtt.publish
    data:
      topic: cmnd/tasmota_NsPanelTerrasse/Backlog
      payload: CustomSend pageType~popupNotify; CustomSend entityUpdateDetail~id~{{
        title }}~65535~~~~~{{ message }}~65535~{{ timeout }}; Buzzer 2,2,2
  mode: single
  icon: mdi:message-badge
 ```

Send Message to the Panel:
   
 ```yaml
nspanel_popup_notification:
  alias: Popup Notification
  sequence:
  - service: mqtt.publish
    data:
      topic: cmnd/tasmota_NsPanelTerrasse/Backlog
      payload: CustomSend pageType~popupNotify; CustomSend entityUpdateDetail~id~{{
        title }}~65535~~~~~{{ message }}~65535~{{ timeout }}
  mode: single
  icon: mdi:message-badge
 ```
</details>


<details>
<summary>Notification on screensaver</summary>
<br>

   The screensaver can display Notifications by sending this command to the CustomSend topic: `notify~heading~text`
   

Send Message to the Screensaver combined with a buzzer sound:
   
 ```yaml
nspanel_screensaver_notification:
  alias: Screensaver Notification
  sequence:
  - service: mqtt.publish
    data:
      topic: cmnd/tasmota_NsPanelTerrasse/Backlog
      payload: CustomSend notify~{{ heading }}~{{ message }}; Buzzer 2,2,2
  mode: single
  icon: mdi:message-badge
 ```

Send Message to the Screensaver:
   
 ```yaml
nspanel_screensaver_notification:
  alias: Screensaver Notification
  sequence:
  - service: mqtt.publish
    data:
      topic: cmnd/tasmota_NsPanelTerrasse/Backlog
      payload: CustomSend notify~{{ heading }}~{{ message }}
  mode: single
  icon: mdi:message-badge
 ```
   
</details>

