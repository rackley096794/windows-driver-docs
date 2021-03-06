---
title: Interrupt Affinity
author: windows-driver-content
description: Interrupt Affinity
ms.assetid: e36a52d0-3a94-4017-b4a1-0b41f737523c
keywords: ["interrupt service routines WDK kernel , affinity", "ISRs WDK kernel , affinity", "affinity policy WDK interrupts", "IRQ_DEVICE_POLICY", "processor affinity WDK kernel"]
ms.author: windowsdriverdev
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
---

# Interrupt Affinity


The *affinity* of an interrupt is the set of processors that can service the interrupt. Each device has an *affinity policy*. The operating system uses the affinity policy to compute the affinity for that device's interrupts. The affinity policy can be specified in the device's INF file or registry settings.

Starting with Windows Vista, administrators can use the registry to set an affinity policy for an interrupt.

Administrators can set the following entries under the **\\Interrupt Management\\Affinity Policy** registry key:

-   **DevicePolicy** is a REG\_DWORD value that specifies an affinity policy. Each possible setting corresponds to a [**IRQ\_DEVICE\_POLICY**](https://msdn.microsoft.com/library/windows/hardware/ff551783) value.

-   **AssignmentSetOverride** is a REG\_BINARY value that specifies a [**KAFFINITY**](https://msdn.microsoft.com/library/windows/hardware/ff551830) mask. If **DevicePolicy** is 0x04 (**IrqPolicySpecifiedProcessors**), then this mask specifies a set of processors to assign the device's interrupts to.

The following table lists the [**IRQ\_DEVICE\_POLICY**](https://msdn.microsoft.com/library/windows/hardware/ff551783) values, and the corresponding registry setting for **DevicePolicy**. For more information about the meaning of each value, see [**IRQ\_DEVICE\_POLICY**](https://msdn.microsoft.com/library/windows/hardware/ff551783).

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IRQ_DEVICE_POLICY value</th>
<th>Numeric value in registry</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>IrqPolicyMachineDefault</strong></p></td>
<td><p>0x00</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicyAllCloseProcessors</strong></p></td>
<td><p>0x01</p></td>
</tr>
<tr class="odd">
<td><p><strong>IrqPolicyOneCloseProcessor</strong></p></td>
<td><p>0x02</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicyAllProcessorsInMachine</strong></p></td>
<td><p>0x03</p></td>
</tr>
<tr class="odd">
<td><p><strong>IrqPolicySpecifiedProcessors</strong></p></td>
<td><p>0x04</p></td>
</tr>
<tr class="even">
<td><p><strong>IrqPolicySpreadMessagesAcrossAllProcessors</strong></p></td>
<td><p>0x05</p></td>
</tr>
</tbody>
</table>

 

A driver's INF file can provide default settings for the registry values. Here is an example of how to set the **DevicePolicy** value to **IrqPolicyOneCloseProcessor** in the INF file. For more information, see [**INF AddReg Directive**](https://msdn.microsoft.com/library/windows/hardware/ff546320).

```
[install-section-name.HW]
AddReg=add-registry-section 

[add-registry-section]
HKR, "Interrupt Management\Affinity Policy", DevicePolicy, 0x00010001, 2
```

The system makes the registry settings available to the device's driver when it sends the [**IRP\_MN\_FILTER\_RESOURCE\_REQUIREMENTS**](https://msdn.microsoft.com/library/windows/hardware/ff550874) IRP to the driver. The operating system provides an [**IO\_RESOURCE\_DESCRIPTOR**](https://msdn.microsoft.com/library/windows/hardware/ff550598) structure for each interrupt with the **Type** member set to **CmResourceTypeInterrupt**. For a message-signaled interrupt, the CM\_RESOURCE\_INTERRUPT\_MESSAGE bit of the **Flags** member is set; otherwise, it is clear. The **u.Interrupt** member describes the settings for the interrupt.

The following table gives the correspondence between registry settings and members of **u.Interrupt**.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Registry Value</th>
<th>Member of u.Interrupt</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>DevicePolicy</strong></p></td>
<td><p><strong>AffinityPolicy</strong></p></td>
</tr>
<tr class="even">
<td><p><strong>AssignmentSetOverride</strong></p></td>
<td><p><strong>TargetedProcessors</strong></p></td>
</tr>
</tbody>
</table>

 

 

 




