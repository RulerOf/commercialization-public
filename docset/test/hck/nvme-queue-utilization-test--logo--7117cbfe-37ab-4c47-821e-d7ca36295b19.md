---
author: joshbax-msft
title: NVMe Queue Utilization Test (LOGO)
description: NVMe Queue Utilization Test (LOGO)
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 705cd0f8-c805-48c5-8abf-0bcc3d99e2d4
---

# NVMe Queue Utilization Test (LOGO)


This test measures the I/O Queue statistics of both Submission Queue and Completion Queue. There are 2 scenarios here:

-   Activate queues mapped to all processors

-   Activate queues mapped to random number of processors

## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Storage.ControllerDrive.NVMe.BasicFunction</p>
<p>[See the device hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254483)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows 8.1 x64 Windows 8.1 x86 Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~60 minutes</p></td>
</tr>
<tr class="even">
<td><p><strong>Categories</strong></p></td>
<td><p>Certification</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type</strong></p></td>
<td><p>Automated</p></td>
</tr>
</tbody>
</table>

 

## Running the test


Before you run the test, complete the test setup as described in the test requirements: [Hard Disk Drive Testing Prerequisites](hard-disk-drive-testing-prerequisites.md).

## Troubleshooting


For troubleshooting information, see [Troubleshooting Device.Storage Testing](troubleshooting-devicestorage-testing.md).

If the test fails to find the drive letter of the device, try to restart the machine with device attached, format and mount NTFS volume and assign drive letter, reboot machine to confirm drive letter and drive number of device are recognizable in diskmgmt.msc and then schedule the test.

## More information


### Command syntax

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Command</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>/DriveLetter</strong></p></td>
<td><p>The drive letter of the device. You can get help by running <strong>nvmeshim /DriveLetter /?</strong></p>
<p>Example: D:</p></td>
</tr>
<tr class="even">
<td><p><strong>/DriveNumber</strong></p></td>
<td><p>The drive number of the device. You can get help by running <strong>nvmeshim /DriveNumber /?</strong></p>
<p>Example: 1</p></td>
</tr>
<tr class="odd">
<td><p><strong>/Duration</strong></p></td>
<td><p>I/O duration in seconds. You can get help by running <strong>nvmeshim.exe /Duration /?</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>/Operation QueueUtilization</strong></p></td>
<td><p>Run QueueUtilization scenarios.</p></td>
</tr>
<tr class="odd">
<td><p><strong>/Verbosity</strong></p></td>
<td><p>The level of logging verbosity. Larger values cause more verbose output.</p></td>
</tr>
<tr class="even">
<td><p><strong>/Scenario All</strong></p></td>
<td><p>Run all scenarios in the specified operation.</p></td>
</tr>
</tbody>
</table>

 

### File list

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>File</th>
<th>Location</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>nvmeshim.exe</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
<tr class="even">
<td><p>Enable.cmd</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
<tr class="odd">
<td><p>stornvme.sys</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
<tr class="even">
<td><p>Stornvmeshim.cat</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
<tr class="odd">
<td><p>Stornvmeshim.man</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
<tr class="even">
<td><p>Stornvmeshim.inf</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
<tr class="odd">
<td><p>Stornvmeshim.sys</p></td>
<td><p><em>&lt;testbinroot&gt;</em>\NTTEST\driverstest\storage\wdk\nvme\</p></td>
</tr>
</tbody>
</table>

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20NVMe%20Queue%20Utilization%20Test%20%28LOGO%29%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



