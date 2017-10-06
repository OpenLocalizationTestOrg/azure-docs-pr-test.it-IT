---
title: aaaDeploy QuickBooks in Azure RemoteApp | Documenti Microsoft
description: Informazioni su come tooshare QuickBooks con Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>Come distribuire QuickBooks in Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Utilizzare hello seguente informazioni tooshare QuickBooks come un'app in Azure RemoteApp.

È possibile condividere QuickBooks 2015 Enterprise con Azure RemoteApp in una raccolta ibrida o cloud. file aziendale Hello deve risiedere in una macchina virtuale che esegue server di database QuickBooks è separato dai server di Azure RemoteApp hello. Non memorizzare mai file aziendale hello sull'immagine Azure RemoteApp: perdita di dati è previsto se si esegue questa operazione. Solo QuickBooks Enterprise supporta file di QuickBooks hello hosting in una condivisione esterna con server di database QuickBooks accessibile tramite rete standard di Windows.   

> [!IMPORTANT]
> Hello QuickBooks i server di database che ospita i file aziendale hello devono risiedere in una macchina virtuale separata all'interno di hello stessa rete virtuale come hello raccolta di Azure RemoteApp.  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>Passaggi toodeploy QuickBooks
1. Creare una macchina virtuale di Azure e installare QuickBooks, server di database QuickBooks e inserire file aziendale hello in una macchina virtuale di Azure.  Verificare che tooproperly configurare regole firewall.
2. Installare QuickBooks in un [immagine personalizzata](remoteapp-imageoptions.md) e creare un [raccolta di Azure RemoteApp](remoteapp-collections.md), cloud o ibrida, all'interno di hello esatta stessa rete virtuale in cui hello macchina virtuale che ospita hello QuickBooks server di database con i file aziendali si trova. 
3. [Pubblicare](remoteapp-publish.md) toousers app QuickBooks
4. Avviare il client di hello QuickBooks ospitati in Azure RemoteApp, passare tramite rete toohello VM hello QuickBooks database server di hosting standard di Windows e aprire file aziendale hello. 

## <a name="documentation-references"></a>Riferimenti di documentazione
* [Configurazioni supportate](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* [Opzioni di distribuzione](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

È inoltre possibile estrarre la presentazione, Ignite [nozioni di base di Microsoft Azure RemoteApp gestione e amministrazione](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) -too1:02:45 tooget toohello QuickBooks parte di uno sprint.

## <a name="deployment-architecture"></a>Architettura di distribuzione
![QuickBooks + distribuzione di Azure RemoteApp](./media/remoteapp-quickbooks/ra-quickbooks.png)

