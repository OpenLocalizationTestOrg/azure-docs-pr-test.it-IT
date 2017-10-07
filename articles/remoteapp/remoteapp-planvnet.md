---
title: aaaHow tooplan della rete virtuale per una raccolta di Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooplan della rete virtuale per una raccolta di Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: ad9aff0e-f374-49c0-951d-4a7be1c36de0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: d7eeefc3c66815b18f9338e2e428585e6f81a12a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooplan-your-virtual-network-for-azure-remoteapp"></a>Come tooplan la rete virtuale di Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Questo documento descrive come tooset backup di rete virtuale di Azure (VNET) e una subnet hello per Azure RemoteApp. Se non si ha familiarità con reti virtuali di Azure, questa è una funzionalità che consente di toovirtualize la rete dell'infrastruttura toohello cloud e toocreate soluzioni ibride con Azure e alle risorse locali. Per altre informazioni, leggere [qui](../virtual-network/virtual-networks-overview.md).

Se si desiderano toodefine criteri di sicurezza per il traffico (in ingresso e in uscita) nella rete virtuale in cui si intende distribuire Azure RemoteApp, è fortemente consigliabile creare una subnet distinta per Azure RemoteApp da rest hello delle distribuzioni in hello Azure rete virtuale. Per ulteriori informazioni sulla modalità di rete subnet toodefine i criteri di protezione su di virtuale di Azure, leggere [che cos'è un gruppo di sicurezza di rete (gruppo)?](../virtual-network/virtual-networks-nsg.md).

## <a name="types-of-azure-remoteapp-collections-with-azure-virtual-networks"></a>Tipi di raccolte Azure RemoteApp con reti virtuali di Azure
Hello grafici seguenti mostrano hello due opzioni di raccolta diverso quando si desidera toouse una rete virtuale.

### <a name="azure-remoteapp-cloud-collection-with-vnet"></a>Raccolta nel cloud di Azure RemoteApp con la rete virtuale
 ![Azure RemoteApp - Raccolta nel cloud con una rete virtuale](./media/remoteapp-planvpn/ra-cloudvpn.png)

Rappresenta una raccolta di Azure RemoteApp in tutte le risorse di hello che gli host della sessione di RemoteApp di hello devono tooaccess vengono distribuite in Azure. Possono essere in hello stessa rete virtuale come hello RemoteApp VNET o una diversa rete virtuale in Azure.

### <a name="azure-remoteapp-hybrid-collection-with-vnet"></a>Raccolta ibrida di Azure RemoteApp con la rete virtuale
![Azure RemoteApp - Raccolta ibrida con una rete virtuale](./media/remoteapp-planvpn/ra-hybridvpn.png)

Rappresenta una raccolta di Azure RemoteApp in cui alcune risorse hello che gli host della sessione di RemoteApp di hello devono tooaccess sono distribuiti in locale. Hello VNET RemoteApp è una rete locale toohello collegato utilizzando tecnologie ibridi di Azure come VPN site-to-site o Expressroute.

## <a name="how-hello-system-works"></a>Funzionamento del sistema hello
Dietro quinte hello Azure RemoteApp consente di distribuire macchine virtuali di Azure (con l'immagine caricata) toohello subnet della rete virtuale che si è scelto durante il provisioning. Se si è scelto per una raccolta ibrida, si tenta di hello tooresolve FQDN hello del controller di dominio che immesso nel provisioning del flusso di lavoro con il server DNS hello fornito nella rete virtuale hello hello.  
Se ci si connette tooan una rete virtuale esistente, verificare le porte necessarie che tooexpose hello nei gruppi di sicurezza di rete nella subnet di Azure RemoteApp. 

È consigliabile usare una [subnet sufficientemente estesa per Azure RemoteApp](remoteapp-vnetsizing.md). Hello più grande supportata dalla rete virtuale di Azure è valore/8 (utilizzando le definizioni di subnet CIDR). La subnet deve essere sufficientemente grande tooaccommodate tutte hello Azure RemoteApp le macchine virtuali durante la scalabilità verticale quando più utenti accedono alle App hello. 

Di seguito sono hello gli elementi tooenable sulla subnet rete virtuale: 

1. Consentire il traffico in uscita dalla subnet hello nella porta intervallo 10101 10175 toocommunicate con uno dei servizi Azure RemoteApp interni hello.
2. Il traffico in uscita deve essere consentito dal tooAzure tooconnect subnet archiviazione sulla porta 443
3. Se si dispone di Active Directory ospitati in Azure, assicurarsi che qualsiasi macchina virtuale nella subnet della rete virtuale hello per Azure RemoteApp è in grado di tooconnect toothat controller di dominio. Hello DNS nella rete virtuale hello deve essere in grado di tooresolve hello FQDN controller di dominio.

## <a name="virtual-network-with-forced-tunneling"></a>Rete virtuale con tunneling forzato
[tunneling forzato](../vpn-gateway/vpn-gateway-about-forced-tunneling.md) ora è supportato per tutte le nuove raccolte Azure RemoteApp. Attualmente non è supportata la migrazione di hello di un toosupport raccolta esistente, il tunneling forzato.  Sarà necessario toodelete delle raccolte esistenti utilizzando hello rete virtuale che si sta collegando tooAzure RemoteApp e creare un nuovo uno tooget attivato le raccolte di tunneling forzato. 

