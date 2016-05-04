---
author: joshbax-msft
title: Multipath I-O Test (LOGO)
description: Multipath I-O Test (LOGO)
MSHAttr:
- 'PreferredSiteName:MSDN'
- 'PreferredLib:/library/windows/hardware'
ms.assetid: 4b7aa31e-b350-4b13-ac2c-faf7147fa451
---

# Multipath I-O Test (LOGO)


This test provides multi-path I/O testing for the compatibility of a vendor's storage solution with Microsoft® driver solutions.

**Note**  
The test is specifically designed to run on x64 processor architectures.

 

## Test details


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Associated requirements</strong></p></td>
<td><p>Device.Storage.Hd.Mpio.BasicFunction</p>
<p>[See the device hardware requirements.](http://go.microsoft.com/fwlink/p/?linkid=254483)</p></td>
</tr>
<tr class="even">
<td><p><strong>Platforms</strong></p></td>
<td><p>Windows Server 2012 (x64) Windows Server 2008 R2 (x64) Windows Server 2008 x64 Windows Server 2008 x86Windows Server 2012 R2</p></td>
</tr>
<tr class="odd">
<td><p><strong>Expected run time</strong></p></td>
<td><p>~180 minutes</p></td>
</tr>
<tr class="even">
<td><p><strong>Categories</strong></p></td>
<td><p>Certification Reliability</p></td>
</tr>
<tr class="odd">
<td><p><strong>Type</strong></p></td>
<td><p>Manual</p></td>
</tr>
</tbody>
</table>

 

## Running the test


Before you run the test, complete the test setup for the type of Raid Storage array that you are testing. For more information see, [Hardware-based RAID (Storage Array) Testing Overview](hardware-based-raid--storage-array--testing-overview.md).

In addition, this test requires the following software and hardware:

-   Hardware storage RAID array that uses either the Microsoft Device Specific Module (DSM) or a third-party DSM that interfaces to the Microsoft MPIO core architecture

-   Software components included with the DSM or hardware storage RAID array being tested.

-   Multi-Path I/O Setup

## Troubleshooting


For general storage troubleshooting information, see [Troubleshooting Device.Storage Testing](troubleshooting-devicestorage-testing.md).

In addition, this test has the following known issues:

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>Issue</strong></p></td>
<td><p><strong>Details</strong></p></td>
</tr>
<tr class="even">
<td><p>The MPIO test environment for a non-iSCSI scenario may not be configured correctly.</p></td>
<td><p>When testing in a non-iSCSI MPIO test environment, the test requires the Host Bus Adapter (HBA) with at least two ports (or at least two HBAs, if the HBA just has one port) to be connected to the same iSCSI target. The following manual steps can verify that the test environment is set up properly:</p>
<ol>
<li><p>On the test computer, open Device Manager and click <strong>Show hidden devices</strong>. You will see some disks shown and each hidden disk is for one path.</p></li>
<li><p>For each HBA port device node:</p>
<ol>
<li><p>Disable it by right-clicking each HBA port and then click <strong>Disable</strong>.</p></li>
<li><p>Verify that the hidden disks are removed after disabling that port instance. If the hidden disks remain, the HBA port is not connected to the iSCSI target.</p></li>
</ol></li>
</ol></td>
</tr>
<tr class="odd">
<td><p>The test fails to get HBA device instance when installing filter.</p></td>
<td><p>Ensure that the DSM name in the registry key (INF file) is the same as the name specified in the DSM itself.</p></td>
</tr>
<tr class="even">
<td><p>The test fails to get the iSCSI WMI information, when connected to the test storage device through both Fibre Channel and iSCSI when the test is running against the Fibre Channel.</p></td>
<td><p>We recommend that you not configure MPIO LUNs that are claimed by the same DSM over more than one bus type in the same test environment.</p></td>
</tr>
<tr class="odd">
<td><p>The test fails when paths are removed after the test runs the link bouncing and simultaneous bouncing test cases.</p></td>
<td><p>Please make sure that the HBA is running the latest driver (one that has passed Windows Logo Certification). When testing in a non-iSCSI test environment, the Multi-Path I/O test requires that the HBA driver successfully pass the Plug and Play Driver test. If the HBA cannot pass that test, please change to another certified HBA model of HBA and retest This issue may occur because MPIO paths require a long time to be recovered.</p></td>
</tr>
<tr class="even">
<td><p>The test fails when run under an MPIO boot environment.</p></td>
<td><p>Do not run the test in a MPIO boot test environment.</p></td>
</tr>
<tr class="odd">
<td><p>The test fails to restore iSCSI sessions on the iSCSI target.</p></td>
<td><p>Within the MPIO test environment, if there are multiple ports (IP addresses) related to one iSCSI target, you need to make sure there are at least two iSCSI sessions connected through the IP address during the test. Although the Multi-Path I/O test permit user’s to configure multiple port connections to an iSCSI target, at the same time for all iSCSI related tests, user can only associate one IP address during testing.</p></td>
</tr>
<tr class="even">
<td><p>The test did not display the iSCSI UI</p></td>
<td><p>First, verify that the selected LUN bus type is iSCSI. If not, the Multi-Path I/O test will not display the iSCSI UI. Second, please check if the iscsihctconfig.ini file is present at the following path: [WLKClient]\JobsWorkingDir\. If this file is present, delete it if you want to use the iSCSI UI to input the iSCSI configuration information manually.</p></td>
</tr>
<tr class="odd">
<td><p>The test failed or crashed.</p></td>
<td><p>If the Multi-Path I/O test failed to run, please make sure that the test environment is clean before rerunning the test. This issue may occur if your controller initially contained Windows Logo Kit 1.5 and you did not reinstall Windows before installing and using Windows Logokit 1.6 to complet your storage testing.If this occurred, reinstall Windows and restart your testing.</p></td>
</tr>
<tr class="even">
<td><p>The test fails with IO operation errors</p></td>
<td><p>If the Multi-Path I/O test failed anf the log file contains IO operations errors, please verify that yourLUNs are online and initialized in the raw status before running the test. If the LUNs are online and initialized, , please try to copy or read a file from a LUN with some paths failed over.</p></td>
</tr>
</tbody>
</table>

 

If you intend to open a support incident, follow these steps to obtain information useful to Customer Support Services:

1.  Please provide your submission .cpk package. This .cpk package should not just include Multi-Path I/O test t log but include logs for the SCSI Compliance test and the ALUA MPIO test.

2.  Please capture screenshots of your test environment. If the operating system is Windows 2008 R2 or later, please capture the MPIO configuration Snapshot screen from the Control Panel. To view this, click Start&gt;Control Panel&gt;MPIO&gt;Configuration Snapshot.

3.  If a crash happened, please create a dump file. Also rerun the following test in steps:

    1.  Copy the test binaries binaries and files to the Windows HCK test computer, which include: mpiotest.exe, mpioinstallfiltr.exe, iscsiui.exe, devcon.exe, pnpfiltr.sys, pnpdtest.exe and the mpiotest\_script\_fvt.txt file.

    2.  Open a command prompt window with Administrator privileges.

    3.  Run one of the following commands:

        -   If the bus type is iSCSI, then run the iscsui.exe tool and input information to create an iscsihctconfig.ini file.

        -   If the bus type is non-iSCSI, then run the command: mpioinstallfiltr –d &lt;DSM device instance path&gt; (for example ROOT\\MPIO\\0001) -i and then restart the test computer. If this command crashes, copy all the log files from the command console using Notepad.

    4.  Run the following command for test. Even if test crashes, you still can copy all log from command console to notepad.

        -   Mpiotest.exe -d &lt;DSM device instance path&gt; (for example ROOT\\MPIO\\0001) -s \[ScriptName\] –logo –isiSCSI \[T/F\].

    5.  If the bus type is non-iSCSI, then, from a command prompt, run the following command to uninstall the filter driver: mpioinstallfiltr –d &lt;DSM device instance path&gt;, (for example, ROOT\\MPIO\\0001) -c and restart the system boot machine.

## More information


This test is applied for Device Specific Modules (DSM) only, either Microsoft DSM or a third party DSM.

The test includes the following basic test assertions, which are combined into four test cases:

-   Failover: Data transfer is not broken when some paths are broken but not all.

-   Failback: Data transfer works normally when some paths are restored from failover.

-   Link bounce: For an MPIO environment, all paths except for one path are broken. If that path is broken and recovers within 15 seconds, the data transfer is able to continue without error.

-   Simultaneous failover and failback, or "simultaneous bouncing": Data transfer is not broken when some paths fail over and other paths fail back simultaneously.

-   Load balance policy: Different policy can be set and data transfer can work correctly with it. For Round Robin Load Policy and Round Robin Load Policy with subset, the test checks whether efficiency is degraded.

The test components include a stand-alone test application, a fault injection filter driver, a test case configuration file, an iSCSI configuration file (if the path is created over an iSCSI session), and the Device Test Manager (DTM).

Customers of an enterprise storage solution rely heavily on the high availability of its components. In storage, high availability is often implemented by redundancy. Multi-path I/O (MPIO) is one such implementation for the fabric layer of an enterprise storage solution. Microsoft supports multi-path I/O with a multi-path driver (mpio.sys) and a Device Specific Module (msdsm.sys) that ship with Windows Advanced Server operating system in the Windows Vista timeframe.

The test provides multi-path I/O testing for the compatibility of a vendor's storage solution with Microsoft driver solutions. It focuses on the following areas:

1.  Path failover and recovery should not affect data transfer quality. One purpose of setting up an MPIO environment is to increase the reliability of data transferring. This test simulates several simple scenarios that would happen in the real world to break a path, and then checks whether the environment can transfer data normally.

2.  Data transfer efficiency should be improved, or at least not degraded, in an MPIO environment.

3.  Storage devices should work normally under all policies they declare to support.

**Note**  
For a Device Specific Module (DSM) that supports vendor policy (policy value is 7), please make the vendor's policy the current policy before running this test.

 

**To run this test**

1.  The Windows Hardware Certification Kit (Windows HCK) starts the stand-alone test application, which retrieves the test cases to run.

2.  The Windows HCK retrieves the MPIO test environment information for further testing.

3.  If a path is not over iSCSI, the test loads the filter driver for a related HBA instance for further testing.

4.  If the path is over iSCSI, provide the iSCSI configuration information using one of the following ways:

    -   Input the configuration data into the window pop-up on the test client, which creates the Iscsihctconfig.ini file under \[WLK PATH\]\\JobsWorkingDir\\Tasks\\\[WTTJOBNAME\]\\. For more information, go to [iSCSI HBA Boot Test (LOGO)](iscsi-hba-boot-test--logo-ca7ad4d0-6950-4e2d-bdfe-b80c7873ba90.md).

        **Note**  
        If your test environment includes multiple targets, please choose to input one target related information, including IQN, portal IP and port number. For IP address, if you have several IP addresses, please input the one used to connect that target. Please for MPIO test, you do not need to input HBA PnP ID.

         

        **Note**  
        If your iSCSI environment support mutual chap, please check both Mutual radio box and Supports Mutual Chap check box.

         

    -   The input iSCSI configuration information will be stored in the file of iscsihctconfig.ini. To save users time, we put a copy of this configuration file under \[WLKClient\]\\JobsWorkingDir\\ on test machine. Then users can rerun the test on same test client for same iSCSI storage target without inputting iSCSI configuration information again. Also, before testing, users can choose to create the Iscsihctconfig.ini file manually and put it under \[WLKClient\] \\JobsWorkingDir\\ on test machine, which contains the configuration data. Use the following format:

        ``` syntax
        [Targets] DiskTarget=Target [Target] TargetName=iqn.2001-05.com.equallogic:0-8a0906-7e2dd0401-fd1d03f67f74b96b-10-2411a0920-0 PortalPort=3260 PortalIPAddress=10.10.20.80 CHAPType=None
        ```

5.  Set the load balance policy, which declares support, simulates failover and failback scenarios, and performs testing. For a non-iSCSI test environment, simulate the link bouncing and simultaneous bouncing scenarios.

6.  Set the Round Robin policy for non-ALUA storage and ALUA storage to enable performance checking.

7.  The test tool logs to WTTLogger.

### Parameters

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ScriptName</p></td>
<td><p>The name of the test script.</p>
<p>Default value: mpiotest_script_fvt.txt</p></td>
</tr>
<tr class="even">
<td><p>WDKDeviceID</p></td>
<td><p>The device instance ID.</p></td>
</tr>
<tr class="odd">
<td><p>isiSCSI</p></td>
<td><p>The storage bus type is iSCSI or not. (T/F)</p></td>
</tr>
</tbody>
</table>

 

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
<td><p><strong>mpiotest.exe -d &quot;[WDKDeviceID]&quot; -s [ScriptName] -logo –isiSCSI [isiSCSI]</strong></p></td>
<td><p>Runs the test.</p></td>
</tr>
</tbody>
</table>

 

**Note**  
For command-line help for this test binary, type **/h**.

 

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
<td><p>Devcon.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\idw\</p></td>
</tr>
<tr class="even">
<td><p>EDT_Disable_Support.vbs</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\DriversTest\storage\wdk\mpiotest\</p></td>
</tr>
<tr class="odd">
<td><p>EDT_Enable_Support.vbs</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>nttest\DriversTest\storage\wdk\mpiotest\</p></td>
</tr>
<tr class="even">
<td><p>Iscsiui.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\DriversTest\storage\wdk\mpiotest\</p></td>
</tr>
<tr class="odd">
<td><p>Mpioinstallfiltr.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\DriversTest\storage\wdk\mpiotest\</p></td>
</tr>
<tr class="even">
<td><p>Mpiotest.exe</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\nttest\DriversTest\storage\wdk\</p></td>
</tr>
<tr class="odd">
<td><p>Mpiotest_script_fvt.txt</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\nttest\DriversTest\storage\wdk\mpiotest\</p></td>
</tr>
<tr class="even">
<td><p>DevFund_PnPDTest_WLK.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\</p></td>
</tr>
<tr class="odd">
<td><p>Utility_Enable_Disable_DriverVerifier.dll</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\</p></td>
</tr>
<tr class="even">
<td><p>Utility_DeviceStatusCheck.wsc</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\</p></td>
</tr>
<tr class="odd">
<td><p>Utility_DisableEDTSupport.wsc</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\</p></td>
</tr>
<tr class="even">
<td><p>Utility_EmptyTest.wsc</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\</p></td>
</tr>
<tr class="odd">
<td><p>Utility_WdfRelatedVerification.wsc</p></td>
<td><p><em>&lt;[testbinroot]&gt;</em>\</p></td>
</tr>
</tbody>
</table>

 

 

 

[Send comments about this topic to Microsoft](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20%5Bp_hck\p_hck%5D:%20Multipath%20I-O%20Test%20%28LOGO%29%20%20RELEASE:%20%284/27/2016%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20http://privacy.microsoft.com/default.aspx. "Send comments about this topic to Microsoft")



