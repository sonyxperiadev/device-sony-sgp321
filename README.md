Copyright (C) Sony Mobile Communications 2013
=============================================

This is the Android device configuration for Xperia Tablet Z (SGP321 and SGP311).

To setup a tree and build images for the device do the following:

`repo init` as described by Google over at:
http://source.android.com/source/downloading.html

Put the following snippet in `.repo/local_manifests/sgp321.xml`:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<manifest>
<remote  name="sony" fetch="git://github.com/sonyxperiadev/" />

<remove-project name="platform/hardware/qcom/camera" />
<remove-project name="platform/hardware/qcom/display" />
<remove-project name="platform/hardware/qcom/keymaster" />
<remove-project name="platform/hardware/qcom/media" />
<remove-project name="platform/hardware/qcom/msm8960" />
<remove-project name="platform/hardware/qcom/power" />
<remove-project name="platform/hardware/qcom/sensors" />
<remove-project name="platform/hardware/invensense" />
<remove-project name="platform/hardware/akm" />

<project path="device/sony/lagan" name="device-sony-lagan" groups="device" remote="sony" revision="master" />
<project path="device/sony/sgp321" name="device-sony-sgp321" groups="device" remote="sony" revision="master" />
<project path="vendor/sony/dash" name="DASH" groups="device" revision="master" remote="sony" />
</manifest>
```

Download the zip file with vendor binaries from:
http://developer.sonymobile.com/downloads/tool/software-binaries-for-xperia-z-and-xperia-tablet-z/

In the root of your Android code tree unzip the `SW_binaries_for_Xperia_Z_Xperia_Tablet_Z_v3.zip`.

You should now have directories named `vendor/sony/lagan` and `vendor/sony/sgp321` in your tree.

To build for SGP321:

* `repo sync`
* `lunch full_sgp321-userdebug`
* `make`

To build for SGP311:

* `repo sync`
* `lunch full_sgp311-userdebug`
* `make`

To flash the images produced make sure your device is unlocked, as described on
http://unlockbootloader.sonymobile.com/

Enter fastboot mode on the device by pressing volume up while inserting the USB
cable or execute `adb reboot bootloader`.

* `fastboot flash userdata out/target/product/sgp321/userdata.img`
* `fastboot flashall`

Reflashing userdata is not necessary every time, but incompatibilities with
previous content might result in a device that doesn't boot. If this happens
try to reflash just the userdata again.
