# Nightwatch-Extra guide for iOS app test

## Pre-requisites

 1. install appium (follow steps from [here](https://github.com/appium/appium))
 2. install xcode and correct iOS simulator versions for your test.

## Usage

### 1. Create test entry in `nightwatch.json`

In order to run test in appium locally, you can start with adding following code block into `nightwatch.json`

```javascript
"appiummweb": {
    "desiredCapabilities": {
        "browserName": "safari",
        "appiumVersion": "1.6.3",
        "automationName": "xcuitest",
        "platformName": "iOS",
        "platformVersion": "9.3",
        "deviceName": "iPhone 6",
        "waitForAppScript": "true"
    },
    "selenium": {
        "start_process": false
    },
    "appium": {
        "start_process": true
    }
}
```

Notice that 
 1. `appiumVersion` has to match the appium version you installed
 2. `platformVersion` has to match the iOS simulator version you installed
 3. `deviceName` has to match the iOS simulator type you installed

You can also use the following block as template if you want to run an iOS native app test
```javascript
"appiumapp": {
    "skip_testcases_on_fail": true,
    "desiredCapabilities": {
        "app": "${PATH_TO_YOUR_LOCAL_APP}",
        "appiumVersion": "1.6.3",
        "automationName": "xcuitest",
        "platformName": "iOS",
        "platformVersion": "9.3",
        "deviceName": "iPhone 6",
        "sendKeyStrategy": "setValue",
        "waitForAppScript": "true"
    },
    "selenium": {
        "start_process": false
    },
    "appium": {
        "start_process": true
    }
}
``` 

### 2. Config test entry

The allowed configuration for `desiredCapabilities` can be found [here](https://github.com/appium/appium/blob/master/docs/en/writing-running-appium/running-tests.md).

if `appium.start_process` is configured and is true, `nightwatch-extra` will launch appium automatically at `http://${selenium_host}:${selenium_port}`. 

NOTE: appium is also a selenium server. so `selenium.start_process` and `appium.start_process` are mutually exclusive, meaning that you can only enable one at a time.

## Command vocabulary

The mobile command/assertion set follows the same convention of their desktop counterparts (see [here](web.md)). But we don't recommend applying nightwatch command/assertion directly in your app test because nightwatch doesn't support `accessibility id`. To use `accessibility id` as your element identifier we recommend to implement your own command/assertion in the same way as the included mobile command/assertion in `nightwatch-extra`.

### Mobile command list

<table>
  <tr>
    <th>Nightwatch-extra Command</th>
    <th>Example</th>
    <th>Nightwatch Equivalent</th>
  </tr>
  <tr>
    <td>clickMobileEl(using, selector, callback)</td>
    <td>clickMobileEl("accessibility id", "mybutton")</td>
    <td>(no nightwatch equivalent)</td>
  </tr>
  <tr>
    <td>getMobileEl(using, selector, callback)</td>
    <td>getMobileEl('xpath', '//UIAButton[@name = "Add"]')</td>
    <td>(no nightwatch equivalent)</td>
  </tr>
  <tr>
    <td>setMobileElValue(using, selector, valueToSet, callback)</td>
    <td>setMobileElValue("accessibility id", "search", "cereal")</td>
    <td>(no nightwatch equivalent)</td>
  </tr>
</table>

### Mobile assertion list

<table>
  <tr>
    <th>Nightwatch-extra Assertion</th>
    <th>Example</th>
    <th>Nightwatch Equivalent</th>
  </tr>
  <tr>
    <td>mobileElAttrContains(using, selector, attribute, expected)</td>
    <td>mobileElAttrContains("accessibility id", "submit", "label", "Add a Card")</td>
    <td>(no nightwatch equivalent)</td>
  </tr>
</table>