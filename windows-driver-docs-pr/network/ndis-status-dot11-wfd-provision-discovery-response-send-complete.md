---
title: NDIS_STATUS_DOT11_WFD_PROVISION_DISCOVERY_RESPONSE_SEND_COMPLETE
author: windows-driver-content
ms.assetid: D3A4CD1B-51E0-4BA8-8D49-B0FD5D72F48F
description: 
ms.author: windowsdriverdev 
ms.date: 07/18/2017 
ms.topic: article 
ms.prod: windows-hardware 
ms.technology: windows-devices 
keywords:
 - NDIS_STATUS_DOT11_WFD_PROVISION_DISCOVERY_RESPONSE_SEND_COMPLETE Network Drivers Starting with Windows Vista
---

# NDIS\_STATUS\_DOT11\_WFD\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE


**Important**  The [Native 802.11 Wireless LAN](https://msdn.microsoft.com/library/windows/hardware/ff560690) interface is deprecated in Windows 10 and later. Please use the WLAN Device Driver Interface (WDI) instead. For more information about WDI, see [WLAN Universal Windows driver model](https://msdn.microsoft.com/library/windows/hardware/dn897672).

 

The status of a provision discovery reponse transmission is reported with an NDIS\_STATUS\_DOT11\_WFD\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE indication. A provision discovery response is initiated by an [OID\_DOT11\_WFD\_SEND\_PROVISION\_DISCOVERY\_RESPONSE](https://msdn.microsoft.com/library/windows/hardware/hh451808) OID.

The data type for this indication is the [**DOT11\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh406515) structure.

The miniport driver calls [**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) to make an NDIS\_STATUS\_DOT11\_WFD\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE indication, and must pass a pointer to an [**NDIS\_STATUS\_INDICATION**](https://msdn.microsoft.com/library/windows/hardware/ff567373) structure through the *StatusIndication* parameter. When making this indication, the miniport driver must set the following members of the **NDIS\_STATUS\_INDICATION** structure:

-   **StatusCode** must be set to [NDIS\_STATUS\_DOT11\_WFD\_PROVISION\_DISCOVERY\_REQUEST\_SEND\_COMPLETE](ndis-status-dot11-wfd-provision-discovery-request-send-complete.md).

-   **StatusBuffer** must be set to the address of a [**DOT11\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh406515) structure.

-   **StatusBufferSize** must be set to the total of both the size of [**DOT11\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh406515) and the size of the list of returned Information Elements (IEs).

Requirements
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Supported starting with Windows 8.</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h (include Ndis.h)</td>
</tr>
</tbody>
</table>

## See also


[**DOT11\_PROVISION\_DISCOVERY\_RESPONSE\_SEND\_COMPLETE\_PARAMETERS**](https://msdn.microsoft.com/library/windows/hardware/hh406515)

[OID\_DOT11\_WFD\_SEND\_PROVISION\_DISCOVERY\_RESPONSE](https://msdn.microsoft.com/library/windows/hardware/hh451808)

 

 




