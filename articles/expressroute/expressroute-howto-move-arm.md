---
title: 'Spostare i circuiti ExpressRoute da tooResource classico Manager: PowerShell: Azure | Documenti Microsoft'
description: Questa pagina vengono descritti come toomove toohello un circuito classico distribuzione di gestione risorse del modello tramite PowerShell.
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 08152836-23e7-42d1-9a56-8306b341cd91
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/03/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8dcadafca5e4f40773902cec5786eba1dbe133eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a>Spostare i circuiti ExpressRoute dal modello di distribuzione del hello toohello classico di gestione delle risorse con PowerShell

toouse un circuito ExpressRoute per hello classic e modelli di distribuzione di gestione delle risorse, è necessario spostare modello di distribuzione di gestione risorse di hello circuito toohello. Hello nelle sezioni seguenti consentono di spostare il circuito mediante PowerShell.

## <a name="before-you-begin"></a>Prima di iniziare

* Verificare di disporre di più recente dei moduli di Azure PowerShell hello hello (almeno la versione 1.0). Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).
* Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.
* Esaminare le informazioni di hello previsti [lo spostamento di un circuito ExpressRoute da tooResource classico Manager](expressroute-move.md). Assicurarsi di aver compreso i limiti di hello e limitazioni.
* Verificare che il circuito hello è completamente operativo nel modello di distribuzione classica hello.
* Verificare di disporre di un gruppo di risorse creati nel modello di distribuzione di gestione risorse di hello.

## <a name="move-an-expressroute-circuit"></a>Spostare un circuito ExpressRoute

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a>Passaggio 1: Raccogliere informazioni dettagliate sul circuito dal modello di distribuzione classica hello

Accedi toohello ambiente classico di Azure e raccogliere chiave hello del servizio.

1. Accedi tooyour account Azure.

  ```powershell
  Add-AzureAccount
  ```

2. Selezionare la sottoscrizione Azure appropriata di hello.

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. Importare i moduli di PowerShell hello Azure ed ExpressRoute.

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. Utilizzare i cmdlet di hello sotto le chiavi del servizio hello tooget per tutti i circuiti ExpressRoute. Dopo il recupero delle chiavi di hello, copiare hello **chiave del servizio** del circuito hello che si desidera toomove toohello al modello di distribuzione di gestione delle risorse.

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a>Passaggio 2: Accedere e creare un gruppo di risorse

Firmare nell'ambiente di gestione risorse toohello e creare un nuovo gruppo di risorse.

1. Accedi tooyour ambiente di gestione risorse di Azure.

  ```powershell
  Login-AzureRmAccount
  ```

2. Selezionare la sottoscrizione Azure appropriata di hello.

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. Modificare il frammento di codice hello sotto toocreate un nuovo gruppo di risorse se si dispone già di un gruppo di risorse.

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a>Passaggio 3: Spostare il modello di distribuzione di gestione delle risorse hello ExpressRoute circuito toohello

Si è ora pronti toomove del circuito ExpressRoute dal modello di distribuzione di gestione delle risorse modello toohello hello distribuzione classica. Prima di procedere, verificare informazioni hello nel [lo spostamento di un circuito ExpressRoute dal modello di distribuzione di gestione risorse toohello classico hello](expressroute-move.md).

il metodo toomove del circuito, modificare ed eseguire hello frammento di codice seguente:

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> Al termine dell'operazione move hello hello nuovo nome che è elencato nel cmdlet precedente hello sarà usato tooaddress hello risorse. circuito Hello essenzialmente verrà rinominato.
> 

## <a name="modify-circuit-access"></a>Modificare l'accesso al circuito

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a>tooenable accesso circuito ExpressRoute per entrambi i modelli di distribuzione

Dopo aver spostato il modello di distribuzione di gestione delle risorse classico del toohello circuito ExpressRoute, è possibile abilitare l'accesso tooboth modelli di distribuzione. Eseguire i seguenti modelli di distribuzione di cmdlet tooenable accesso tooboth hello:

1. Ottenere informazioni dettagliate sul circuito hello.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Impostare tooTRUE "Consenti operazioni classico".

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. Aggiornare il circuito hello. Al termine questa operazione, sarà in grado di tooview circuito di hello nel modello di distribuzione classica hello.

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. Eseguire i seguenti cmdlet tooget hello dettagli di hello circuito ExpressRoute hello. È necessario essere in grado di toosee chiave del servizio hello elencati.

  ```powershell
  get-azurededicatedcircuit
  ```

5. È ora possibile gestire utilizzando i comandi di modello di distribuzione classica hello per le reti virtuali classiche e i comandi di gestione risorse di hello per Gestione risorse VNets il circuito ExpressRoute toohello collegamenti. Hello articoli seguenti consentono di gestire i collegamenti toohello circuito ExpressRoute:

    * [Collegamento del circuito ExpressRoute nel modello di distribuzione di gestione risorse di hello di tooyour rete virtuale](expressroute-howto-linkvnet-arm.md)
    * [Collegamento del circuito ExpressRoute nel modello di distribuzione classica hello di tooyour rete virtuale](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a>modello di distribuzione classica toohello accesso circuito ExpressRoute toodisable

Eseguire hello seguente modello di distribuzione classica toohello accesso toodisable cmdlet.

1. Ottenere i dettagli di hello circuito ExpressRoute.

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. Impostare tooFALSE "Consenti operazioni classico".

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. Aggiornare il circuito hello. Al termine questa operazione, non sarà in grado di tooview circuito di hello nel modello di distribuzione classica hello.

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a>Passaggi successivi

* [Creare e modificare il routing per un circuito ExpressRoute](expressroute-howto-routing-arm.md)
* [Collegamento del circuito ExpressRoute di tooyour di rete virtuale](expressroute-howto-linkvnet-arm.md)
