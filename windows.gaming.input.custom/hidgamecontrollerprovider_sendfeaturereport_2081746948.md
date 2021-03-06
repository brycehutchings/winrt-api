---
-api-id: M:Windows.Gaming.Input.Custom.HidGameControllerProvider.SendFeatureReport(System.Byte,System.Byte[])
-api-type: winrt method
---

<!-- Method syntax.
public void HidGameControllerProvider.SendFeatureReport(Byte reportId, Byte[] reportBuffer)
-->

# Windows.Gaming.Input.Custom.HidGameControllerProvider.SendFeatureReport

## -description

Sends the specified HID (Human Interface Device) feature report to the device.

## -parameters

### -param reportId

The ID of the report to send.

### -param reportBuffer

The buffer containing the report data to send.

## -remarks

When using this method for your own custom classes, make sure to pass in a valid report ID that is supported by your device; otherwise, the device will ignore it. Also make sure that your report buffer is the correct size and has valid contents.

The report that you send from this method is the raw, unmodified version in its original format; no parsing is done on it.

## -see-also

## -examples

