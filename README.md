# capacitor-sms-inbox

A Capacitor plugin to read SMS inbox on Android devices.

## Installation

1. Install the plugin:

```bash
npm i @solimanware/capacitor-sms-reader
```

2. Sync your Capacitor project:

```bash
npx cap sync android
```

3. Add the following permissions to your `AndroidManifest.xml` file:

```xml
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.RECEIVE_SMS" />
```

4. In your Capacitor config file (usually `capacitor.config.json` or `capacitor.config.ts`), add the following:

```json
{
  "plugins": {
    "SMSInboxReader": {
      "android": {
        "name": "com.capacitor.sms.reader.SMSInboxReaderPlugin"
      }
    }
  }
}
```

5. Import and initialize the plugin in your TypeScript/JavaScript code:

```typescript
import { Plugins } from '@capacitor/core';
import { SMSInboxReader } from 'capacitor-sms-reader';

// Use the plugin
const { SMSInboxReader } = Plugins;

// Check permissions
const permissionStatus = await SMSInboxReader.checkPermissions();
if (permissionStatus.sms !== 'granted') {
  await SMSInboxReader.requestPermissions();
}

// Now you can use other methods like getCount(), getSMSList(), etc.
```

## Usage

After installation, you can use the plugin's methods to interact with the SMS inbox. Remember to always check and request permissions before accessing SMS data.

For detailed API documentation, see the [API section](#api) below.

## API

<docgen-index>

* [`checkPermissions()`](#checkpermissions)
* [`requestPermissions()`](#requestpermissions)
* [`getCount(...)`](#getcount)
* [`getSMSList(...)`](#getsmslist)
* [`getRawSMSList(...)`](#getrawsmslist)
* [Interfaces](#interfaces)
* [Type Aliases](#type-aliases)
* [Enums](#enums)

</docgen-index>

<docgen-api>
<!--Update the source file JSDoc comments and rerun docgen to update the docs below-->

### checkPermissions()

```typescript
checkPermissions() => Promise<PermissionStatus>
```

**Returns:** <code>Promise&lt;<a href="#permissionstatus">PermissionStatus</a>&gt;</code>

--------------------


### requestPermissions()

```typescript
requestPermissions() => Promise<PermissionStatus>
```

**Returns:** <code>Promise&lt;<a href="#permissionstatus">PermissionStatus</a>&gt;</code>

--------------------


### getCount(...)

```typescript
getCount(options: { filter?: SMSFilter; }) => Promise<{ count: number; }>
```

| Param         | Type                                                          |
| ------------- | ------------------------------------------------------------- |
| **`options`** | <code>{ filter?: <a href="#smsfilter">SMSFilter</a>; }</code> |

**Returns:** <code>Promise&lt;{ count: number; }&gt;</code>

--------------------


### getSMSList(...)

```typescript
getSMSList(options: { projection?: Projection; filter?: SMSFilter; }) => Promise<{ smsList: SMSObject[]; }>
```

| Param         | Type                                                                                                             |
| ------------- | ---------------------------------------------------------------------------------------------------------------- |
| **`options`** | <code>{ projection?: <a href="#projection">Projection</a>; filter?: <a href="#smsfilter">SMSFilter</a>; }</code> |

**Returns:** <code>Promise&lt;{ smsList: SMSObject[]; }&gt;</code>

--------------------


### getRawSMSList(...)

```typescript
getRawSMSList(options: { filter?: SMSFilter; }) => Promise<{ rawSmsList: any; }>
```

Returns a raw sms object (all columns). Its like running SELECT * FROM ..

E.g.
```json
{
  "_id": 33,
  "thread_id": 153,
  "address": "TEST",
  "person": null,
  "date": 1679232404564,
  "date_sent": 1679562604444,
  "protocol": 0,
  "read": 0,
  "status": -1,
  "type": 1,
  "reply_path_present": 0,
  "subject": null,
  "body": "SMS body",
  "service_center": "+918299901123",
  "locked": 0,
  "sub_id": 1,
  "error_code": 0,
  "creator": "com.google.android.apps.messaging",
  "seen": 1,
  "priority": -1
}
```
**Note: This is a raw query and ineffecient. Use with caution**

| Param         | Type                                                          |
| ------------- | ------------------------------------------------------------- |
| **`options`** | <code>{ filter?: <a href="#smsfilter">SMSFilter</a>; }</code> |

**Returns:** <code>Promise&lt;{ rawSmsList: any; }&gt;</code>

--------------------


### Interfaces


#### PermissionStatus

| Prop      | Type                                                        |
| --------- | ----------------------------------------------------------- |
| **`sms`** | <code><a href="#permissionstate">PermissionState</a></code> |


#### SMSFilter

| Prop               | Type                                                | Default                        |
| ------------------ | --------------------------------------------------- | ------------------------------ |
| **`type`**         | <code><a href="#messagetype">MessageType</a></code> | <code>MessageType.INBOX</code> |
| **`id`**           | <code>number</code>                                 |                                |
| **`threadId`**     | <code>number</code>                                 |                                |
| **`body`**         | <code>string</code>                                 |                                |
| **`bodyRegex`**    | <code>string</code>                                 |                                |
| **`address`**      | <code>string</code>                                 |                                |
| **`addressRegex`** | <code>string</code>                                 |                                |
| **`minDate`**      | <code>number</code>                                 |                                |
| **`maxDate`**      | <code>number</code>                                 |                                |
| **`indexFrom`**    | <code>number</code>                                 |                                |
| **`maxCount`**     | <code>number</code>                                 |                                |


#### SMSObject

| Prop           | Type                                                |
| -------------- | --------------------------------------------------- |
| **`id`**       | <code>number</code>                                 |
| **`threadId`** | <code>number</code>                                 |
| **`type`**     | <code><a href="#messagetype">MessageType</a></code> |
| **`address`**  | <code>string</code>                                 |
| **`creator`**  | <code>string</code>                                 |
| **`person`**   | <code>string</code>                                 |
| **`date`**     | <code>number</code>                                 |
| **`dateSent`** | <code>number</code>                                 |
| **`subject`**  | <code>string</code>                                 |
| **`body`**     | <code>string</code>                                 |


#### Projection

| Prop           | Type                 | Default            |
| -------------- | -------------------- | ------------------ |
| **`id`**       | <code>boolean</code> | <code>true</code>  |
| **`threadId`** | <code>boolean</code> | <code>true</code>  |
| **`type`**     | <code>boolean</code> | <code>true</code>  |
| **`address`**  | <code>boolean</code> | <code>true</code>  |
| **`creator`**  | <code>boolean</code> | <code>false</code> |
| **`person`**   | <code>boolean</code> | <code>false</code> |
| **`date`**     | <code>boolean</code> | <code>true</code>  |
| **`dateSent`** | <code>boolean</code> | <code>false</code> |
| **`subject`**  | <code>boolean</code> | <code>true</code>  |
| **`body`**     | <code>boolean</code> | <code>true</code>  |


### Type Aliases


#### PermissionState

<code>'prompt' | 'prompt-with-rationale' | 'granted' | 'denied'</code>


### Enums


#### MessageType

| Members      | Value          |
| ------------ | -------------- |
| **`ALL`**    | <code>0</code> |
| **`INBOX`**  | <code>1</code> |
| **`SENT`**   | <code>2</code> |
| **`DRAFT`**  | <code>3</code> |
| **`OUTBOX`** | <code>4</code> |
| **`FAILED`** | <code>5</code> |
| **`QUEUED`** | <code>6</code> |

</docgen-api>
