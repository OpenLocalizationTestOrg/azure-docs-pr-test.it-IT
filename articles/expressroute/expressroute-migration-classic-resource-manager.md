---
title: 'Eseguire la migrazione delle reti virtuali associate ExpressRoute da tooResource classico Manager: Azure: PowerShell | Documenti Microsoft'
description: Questa pagina vengono descritti come toomigrate associate reti virtuali tooResource Manager dopo lo spostamento del circuito.
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
ms.openlocfilehash: e64506c6909296f98c5dd23b1437bc0b81f31c75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-expressroute-associated-virtual-networks-from-classic-tooresource-manager"></a>Eseguire la migrazione delle reti virtuali associate ExpressRoute da tooResource classico Manager

Questo articolo spiega come Azure ExpressRoute toomigrate associata le reti virtuali del modello di distribuzione Azure Resource Manager hello distribuzione classica modello toohello dopo lo spostamento del circuito ExpressRoute. 


## <a name="before-you-begin"></a>Prima di iniziare
* Verificare di disporre di più recente dei moduli di Azure PowerShell hello hello. Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
* Esaminare le informazioni di hello previsti [lo spostamento di un circuito ExpressRoute da tooResource classico Manager](expressroute-move.md). Assicurarsi di aver compreso i limiti di hello e limitazioni.
* Verificare che il circuito hello è completamente operativo nel modello di distribuzione classica hello.
* Verificare di disporre di un gruppo di risorse creati nel modello di distribuzione di gestione risorse di hello.
* Esaminare hello documentazione per la migrazione di risorse seguenti:

    * [Piattaforma supportata la migrazione di risorse IaaS tooAzure classico Gestione risorse](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
    * [Domande frequenti: Piattaforma supportata migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
    * [Rivedere gli errori di migrazione più comuni e le soluzioni](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="supported-and-unsupported-scenarios"></a>Scenari supportati e non supportati

* Un circuito ExpressRoute può essere spostato dall'ambiente di gestione risorse hello classic toohello senza alcun tempo di inattività. È possibile spostare qualsiasi circuito ExpressRoute da hello classic toohello ambiente di gestione delle risorse senza tempi di inattività. Seguire le istruzioni hello [lo spostamento di circuiti ExpressRoute dal modello di distribuzione del hello toohello classico di gestione delle risorse con PowerShell](expressroute-howto-move-arm.md). Si tratta di una rete virtuale di risorse collegate toohello toomove dei prerequisiti.
* Reti virtuali, i gateway e le distribuzioni associate all'interno di rete virtuale hello sono collegati tooan circuito ExpressRoute nella stessa sottoscrizione può essere hello migrate ambiente di gestione risorse toohello senza alcun tempo di inattività. È possibile seguire hello passaggi descritti più avanti toomigrate risorse, ad esempio le reti virtuali, i gateway e macchine virtuali distribuite in una rete virtuale hello. È necessario assicurarsi che le reti virtuali hello siano configurate correttamente prima di eseguirne la migrazione. 
* Distribuzioni associate all'interno di rete virtuale hello che non si trovano in reti virtuali e gateway hello stessa sottoscrizione come hello circuito ExpressRoute richiedono alcuni migrazione hello toocomplete di tempi di inattività. ultima sezione del documento hello in Hello descrive hello passaggi toobe seguito toomigrate risorse.
* Non è possibile eseguire la migrazione di una rete virtuale con Gateway ExpressRoute e Gateway VPN.

## <a name="move-an-expressroute-circuit-from-classic-tooresource-manager"></a>Spostare un circuito ExpressRoute da tooResource classico Manager
È necessario spostare un circuito ExpressRoute da hello classic toohello ambiente di gestione delle risorse prima di provare toomigrate risorse che sono collegati circuito ExpressRoute toohello. tooaccomplish questa attività, vedere hello seguenti articoli:

* Esaminare le informazioni di hello previsti [lo spostamento di un circuito ExpressRoute da tooResource classico Manager](expressroute-move.md).
* [Spostare un circuito da tooResource classico gestione tramite Azure PowerShell](expressroute-howto-move-arm.md).
* Utilizzare il portale di gestione del servizio Azure hello. È possibile seguire del flusso di lavoro hello troppo[creare un nuovo circuito ExpressRoute](expressroute-howto-circuit-portal-resource-manager.md) e selezionare l'opzione di importazione hello. 

Questa operazione non comporta tempi di inattività. È possibile continuare tootransfer dati tra la rete locale e Microsoft mentre è in corso la migrazione di hello.

## <a name="migrate-virtual-networks-gateways-and-associated-deployments"></a>Eseguire la migrazione di reti virtuali, i gateway e distribuzioni associate

Hello passaggi toomigrate variano a seconda che le risorse vengano hello stessa sottoscrizione, diverse sottoscrizioni o entrambi.

### <a name="migrate-virtual-networks-gateways-and-associated-deployments-in-hello-same-subscription-as-hello-expressroute-circuit"></a>Eseguire la migrazione delle reti virtuali, i gateway, e distribuzioni associate in hello stessa sottoscrizione come hello circuito ExpressRoute
In questa sezione descrive hello passaggi toobe seguito toomigrate una rete virtuale, gateway e le distribuzioni associate in hello stessa sottoscrizione come hello circuito ExpressRoute. Questa migrazione non comporta tempi di inattività. È possibile continuare toouse tutte le risorse tramite il processo di migrazione hello. il piano di gestione di Hello è bloccato mentre è in corso la migrazione di hello. 

1. Verificare che il circuito ExpressRoute hello è stato spostato dall'ambiente di gestione risorse di hello toohello classico.
2. Verificare che tale rete virtuale hello è stato preparato in modo appropriato per la migrazione di hello.
3. Registrare la sottoscrizione per la migrazione delle risorse. tooregister la sottoscrizione per la migrazione di risorse, utilizzare hello seguente frammento di PowerShell:

  ```powershell 
  Select-AzureRmSubscription -SubscriptionName <Your Subscription Name>
  Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
  ```
4. Convalidare, preparare ed eseguire la migrazione. toomove hello rete virtuale hello utilizzare seguente frammento di PowerShell:

  ```powershell
  Move-AzureVirtualNetwork -Prepare $vnetName  
  Move-AzureVirtualNetwork -Commit $vnetName
  ```

  È anche possibile interrompere la migrazione eseguendo hello cmdlet di PowerShell seguente:

  ```powershell
  Move-AzureVirtualNetwork -Abort $vnetName
  ```

## <a name="next-steps"></a>Passaggi successivi
* [Piattaforma supportata la migrazione di risorse IaaS tooAzure classico Gestione risorse](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Tecnica di informazioni approfondite su piattaforma supportata la migrazione da Gestione risorse di tooAzure classico](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager-deep-dive.md)
* [Domande frequenti: Piattaforma supportata migrazione delle risorse IaaS da Gestione risorse di tooAzure classico](../virtual-machines/virtual-machines-windows-migration-classic-resource-manager.md)
* [Rivedere gli errori di migrazione più comuni e le soluzioni](../virtual-machines/windows/migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
