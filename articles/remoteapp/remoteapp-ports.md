---
title: aaaList di porte e gli URL toowhitelist per Azure RemoteApp distribuito nella rete virtuale cliente | Documenti Microsoft
description: Informazioni sulle porte e gli URL, occorre tooconfigure per le comunicazioni tramite Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a>Elenco di porte e gli URL accesso toopermit per Azure RemoteApp distribuito nella rete virtuale cliente
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Se si distribuisce un insieme di cloud o ibrida di Azure RemoteApp in una rete virtuale (VNET), esaminare le seguenti informazioni porta hello. Per altre informazioni sulle reti virtuali, vedere la [panoramica sulle reti virtuali](../virtual-network/virtual-networks-overview.md). Se è stato creato un gruppo di sicurezza di rete (gruppo) limitando le risorse di rete virtuale toohello traffico nella raccolta, assicurarsi che hello seguenti porte siano accessibili e sono consentite tramite criteri di sicurezza hello nella rete virtuale hello. Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete (NSG)](../virtual-network/virtual-networks-nsg.md).

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a>Subnet di Azure RemoteApp deve endpoint toothese di accesso e gli URL:
* *.servicebus.windows.net
* *. servicebus.net
* https://*.remoteapp.windowsazure.com  
* https://www.remoteapp.windowsazure.com 
* https://*remoteapp.windowsazure.com  
* https://*.core.windows.net  
* In uscita:TCP: TCP: 443, 9351, 9352, 10101-10175 
* Facoltativo: UDP: 10201-10275  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a>I client di Azure RemoteApp è necessario accedere a endpoint toothese e URL:
Dai client che si intende hello desktop, dispositivi e così via, che gli utenti utilizzare tooconnect toohello App distribuite in hello raccolta di Azure RemoteApp.

* https://telemetry.remoteapp.windowsazure.com  
* https://*.RemoteApp.windowsazure.com (per questo indirizzo sono le porte UDP hello facoltative) 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* https://*.core.windows.net  
* In uscita: TCP: 443  
* Facoltativo: UDP: 3391 

