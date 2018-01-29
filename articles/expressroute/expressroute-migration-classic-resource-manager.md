---
title: 'Eseguire la migrazione ExpressRoute e delle reti virtuali associate dal modello di distribuzione classica a Resource Manager: Azure: PowerShell | Microsoft Docs'
description: Questa pagina illustra come eseguire la migrazione delle reti virtuali associate in Resource Manager dopo lo spostamento del circuito.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 336f68308f7d4b4dd3c7476a4fabd793939e9e85
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/11/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-to-resource-manager"></a>Eseguire la migrazione di reti virtuali associate ExpressRoute dal modello di distribuzione classica a Resource Manager

Questo articolo illustra come eseguire la migrazione delle reti virtuali associate di Azure ExpressRoute dal modello di distribuzione classica al modello di distribuzione Azure Resource Manager dopo lo spostamento del circuito ExpressRoute. 


## <a name="before-you-begin"></a>Prima di iniziare
* Verificare di avere la versione più recente dei moduli di Azure PowerShell. Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).
* Prima di procedere con la configurazione, assicurarsi di avere verificato i [prerequisiti](expressroute-prerequisites.md), i [requisiti di routing](expressroute-routing.md) e i [flussi di lavoro](expressroute-workflows.md).
* Rivedere le informazioni disponibili in [Spostamento dei circuiti ExpressRoute dal modello di distribuzione classica al modello di distribuzione Resource Manager](expressroute-move.md). Assicurarsi di aver compreso pienamente i limiti e le limitazioni.
* Verificare che il circuito sia completamente operativo nel modello di distribuzione classica.
* Assicurarsi che sia disponibile un gruppo di risorse creato nel modello di distribuzione Resource Manager.
* Vedere la documentazione seguente sulla migrazione delle risorse:

    * [Migrazione supportata dalla piattaforma di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md) (Domande frequenti: Migrazione supportata dalla piattaforma per risorse IaaS dalla distribuzione classica ad Azure Resource Manager)
    * [Rivedere gli errori di migrazione più comuni e le soluzioni](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Scenari supportati e non supportati

* È possibile spostare un circuito ExpressRoute dal modello di distribuzione classica all'ambiente Resource Manager senza tempi di inattività. È possibile spostare qualsiasi circuito ExpressRoute dal modello di distribuzione classica all'ambiente Resource Manager senza tempi di inattività. Seguire le istruzioni disponibili in [Moving ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell](expressroute-howto-move-arm.md) (Spostare i circuiti ExpressRoute dal modello di distribuzione classica a quello Resource Manager usando PowerShell). Questo è un prerequisito per lo spostamento di risorse connesse alla rete virtuale.
* È possibile eseguire la migrazione nell'ambiente Resource Manager di reti virtuali, gateway e distribuzioni associate che si trovano nella rete virtuale e sono associati al circuito ExpressRoute nella stessa sottoscrizione, senza tempi di inattività. È possibile seguire la procedura illustrata più avanti per eseguire la migrazione di risorse come reti virtuali, gateway e macchine virtuali distribuiti nella rete virtuale. È necessario assicurare che le reti virtuali siano configurate correttamente prima della migrazione. 
* Le reti virtuali, i gateway e le distribuzioni associate che si trovano nella rete virtuale ma non sono inclusi nella stessa sottoscrizione del circuito ExpressRoute richiedono del tempo di inattività per il completamento della migrazione. L'ultima sezione del documento illustra la procedura da seguire per eseguire la migrazione delle risorse.
* Non è possibile eseguire la migrazione di una rete virtuale con Gateway ExpressRoute e Gateway VPN.

## <a name="move-an-expressroute-circuit-from-classic-to-resource-manager"></a>Spostare un circuito ExpressRoute dal modello di distribuzione classica a Resource Manager
È necessario spostare un circuito ExpressRoute da una distribuzione classica a un ambiente Resource Manager prima di provare a eseguire la migrazione delle risorse associate al circuito ExpressRoute. Per ottenere questo risultato, vedere gli articoli seguenti:

* Rivedere le informazioni disponibili in [Spostamento dei circuiti ExpressRoute dal modello di distribuzione classica al modello di distribuzione Resource Manager](expressroute-move.md).
* [Spostare un circuito dal modello di distribuzione classica a quello Resource Manager usando Azure PowerShell](expressroute-howto-move-arm.md).
* Usare il portale di gestione dei servizi di Azure. È possibile seguire il flusso di lavoro per [creare un nuovo circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e selezionare l'opzione di importazione. 

Questa operazione non comporta tempi di inattività. È possibile continuare a trasferire dati tra l'istanza locale e Microsoft durante la migrazione.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Eseguire la migrazione di reti virtuali, i gateway e distribuzioni associate

I passaggi necessari per eseguire la migrazione variano a seconda che le risorse siano nella stessa sottoscrizione, in diverse sottoscrizioni o in presenza di entrambi i casi.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-the-same-subscription-as-the-expressroute-circuit"></a>Eseguire la migrazione di reti virtuali, gateway e distribuzioni associate nella stessa sottoscrizione del circuito ExpressRoute
Questa sezione illustra la procedura da seguire per eseguire la migrazione di una rete virtuale, un gateway e le distribuzioni associate nella stessa sottoscrizione del circuito ExpressRoute. Questa migrazione non comporta tempi di inattività. È possibile continuare a usare tutte le risorse durante il processo di migrazione. Il piano di gestione è bloccato durante la migrazione. 

1. Assicurarsi che il circuito ExpressRoute sia stato spostato dalla distribuzione classica all'ambiente Resource Manager.
2. Assicurarsi che la rete virtuale sia stata preparata in modo appropriato per la migrazione.
3. Registrare la sottoscrizione per la migrazione delle risorse. Per registrare la sottoscrizione per la migrazione delle risorse, usare il frammento di codice di PowerShell seguente:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Convalidare, preparare ed eseguire la migrazione. Per spostare la rete virtuale, usare il frammento di codice di PowerShell seguente:

  ```powershell
  Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
  Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
  Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
  ```

  È anche possibile interrompere la migrazione eseguendo il cmdlet di PowerShell seguente:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Passaggi successivi
* [Migrazione supportata dalla piattaforma di risorse IaaS dal modello di distribuzione classica ad Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Approfondimento tecnico sulla migrazione supportata dalla piattaforma dal modello di distribuzione classica ad Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [FAQs: Platform-supported migration of IaaS resources from classic to Azure Resource Manager](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md) (Domande frequenti: Migrazione supportata dalla piattaforma per risorse IaaS dalla distribuzione classica ad Azure Resource Manager)
* [Rivedere gli errori di migrazione più comuni e le soluzioni](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
