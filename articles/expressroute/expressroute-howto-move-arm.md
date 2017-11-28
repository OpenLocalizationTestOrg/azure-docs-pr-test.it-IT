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
# <a name="move-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="228ff-103">Spostare i circuiti ExpressRoute dal modello di distribuzione del hello toohello classico di gestione delle risorse con PowerShell</span><span class="sxs-lookup"><span data-stu-id="228ff-103">Move ExpressRoute circuits from hello classic toohello Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="228ff-104">toouse un circuito ExpressRoute per hello classic e modelli di distribuzione di gestione delle risorse, è necessario spostare modello di distribuzione di gestione risorse di hello circuito toohello.</span><span class="sxs-lookup"><span data-stu-id="228ff-104">toouse an ExpressRoute circuit for both hello classic and Resource Manager deployment models, you must move hello circuit toohello Resource Manager deployment model.</span></span> <span data-ttu-id="228ff-105">Hello nelle sezioni seguenti consentono di spostare il circuito mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="228ff-105">hello following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="228ff-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="228ff-106">Before you begin</span></span>

* <span data-ttu-id="228ff-107">Verificare di disporre di più recente dei moduli di Azure PowerShell hello hello (almeno la versione 1.0).</span><span class="sxs-lookup"><span data-stu-id="228ff-107">Verify that you have hello latest version of hello Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="228ff-108">Per ulteriori informazioni, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="228ff-108">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="228ff-109">Assicurarsi di aver esaminato hello [prerequisiti](expressroute-prerequisites.md), [requisiti di routing](expressroute-routing.md), e [flussi di lavoro](expressroute-workflows.md) prima di iniziare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="228ff-109">Make sure that you have reviewed hello [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="228ff-110">Esaminare le informazioni di hello previsti [lo spostamento di un circuito ExpressRoute da tooResource classico Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="228ff-110">Review hello information that is provided under [Moving an ExpressRoute circuit from classic tooResource Manager](expressroute-move.md).</span></span> <span data-ttu-id="228ff-111">Assicurarsi di aver compreso i limiti di hello e limitazioni.</span><span class="sxs-lookup"><span data-stu-id="228ff-111">Make sure that you fully understand hello limits and limitations.</span></span>
* <span data-ttu-id="228ff-112">Verificare che il circuito hello è completamente operativo nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-112">Verify that hello circuit is fully operational in hello classic deployment model.</span></span>
* <span data-ttu-id="228ff-113">Verificare di disporre di un gruppo di risorse creati nel modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-113">Ensure that you have a resource group that was created in hello Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="228ff-114">Spostare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="228ff-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-hello-classic-deployment-model"></a><span data-ttu-id="228ff-115">Passaggio 1: Raccogliere informazioni dettagliate sul circuito dal modello di distribuzione classica hello</span><span class="sxs-lookup"><span data-stu-id="228ff-115">Step 1: Gather circuit details from hello classic deployment model</span></span>

<span data-ttu-id="228ff-116">Accedi toohello ambiente classico di Azure e raccogliere chiave hello del servizio.</span><span class="sxs-lookup"><span data-stu-id="228ff-116">Sign in toohello Azure classic environment and gather hello service key.</span></span>

1. <span data-ttu-id="228ff-117">Accedi tooyour account Azure.</span><span class="sxs-lookup"><span data-stu-id="228ff-117">Sign in tooyour Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="228ff-118">Selezionare la sottoscrizione Azure appropriata di hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-118">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="228ff-119">Importare i moduli di PowerShell hello Azure ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="228ff-119">Import hello PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="228ff-120">Utilizzare i cmdlet di hello sotto le chiavi del servizio hello tooget per tutti i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="228ff-120">Use hello cmdlet below tooget hello service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="228ff-121">Dopo il recupero delle chiavi di hello, copiare hello **chiave del servizio** del circuito hello che si desidera toomove toohello al modello di distribuzione di gestione delle risorse.</span><span class="sxs-lookup"><span data-stu-id="228ff-121">After retrieving hello keys, copy hello **service key** of hello circuit that you want toomove toohello Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="228ff-122">Passaggio 2: Accedere e creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="228ff-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="228ff-123">Firmare nell'ambiente di gestione risorse toohello e creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="228ff-123">Sign in toohello Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="228ff-124">Accedi tooyour ambiente di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="228ff-124">Sign in tooyour Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="228ff-125">Selezionare la sottoscrizione Azure appropriata di hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-125">Select hello appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="228ff-126">Modificare il frammento di codice hello sotto toocreate un nuovo gruppo di risorse se si dispone già di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="228ff-126">Modify hello snippet below toocreate a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-hello-expressroute-circuit-toohello-resource-manager-deployment-model"></a><span data-ttu-id="228ff-127">Passaggio 3: Spostare il modello di distribuzione di gestione delle risorse hello ExpressRoute circuito toohello</span><span class="sxs-lookup"><span data-stu-id="228ff-127">Step 3: Move hello ExpressRoute circuit toohello Resource Manager deployment model</span></span>

<span data-ttu-id="228ff-128">Si è ora pronti toomove del circuito ExpressRoute dal modello di distribuzione di gestione delle risorse modello toohello hello distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="228ff-128">You are now ready toomove your ExpressRoute circuit from hello classic deployment model toohello Resource Manager deployment model.</span></span> <span data-ttu-id="228ff-129">Prima di procedere, verificare informazioni hello nel [lo spostamento di un circuito ExpressRoute dal modello di distribuzione di gestione risorse toohello classico hello](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="228ff-129">Before proceeding, review hello information provided in [Moving an ExpressRoute circuit from hello classic toohello Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="228ff-130">il metodo toomove del circuito, modificare ed eseguire hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="228ff-130">toomove your circuit, modify and run hello following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="228ff-131">Al termine dell'operazione move hello hello nuovo nome che è elencato nel cmdlet precedente hello sarà usato tooaddress hello risorse.</span><span class="sxs-lookup"><span data-stu-id="228ff-131">After hello move has finished, hello new name that is listed in hello previous cmdlet will be used tooaddress hello resource.</span></span> <span data-ttu-id="228ff-132">circuito Hello essenzialmente verrà rinominato.</span><span class="sxs-lookup"><span data-stu-id="228ff-132">hello circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="228ff-133">Modificare l'accesso al circuito</span><span class="sxs-lookup"><span data-stu-id="228ff-133">Modify circuit access</span></span>

### <a name="tooenable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="228ff-134">tooenable accesso circuito ExpressRoute per entrambi i modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="228ff-134">tooenable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="228ff-135">Dopo aver spostato il modello di distribuzione di gestione delle risorse classico del toohello circuito ExpressRoute, è possibile abilitare l'accesso tooboth modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="228ff-135">After moving your classic ExpressRoute circuit toohello Resource Manager deployment model, you can enable access tooboth deployment models.</span></span> <span data-ttu-id="228ff-136">Eseguire i seguenti modelli di distribuzione di cmdlet tooenable accesso tooboth hello:</span><span class="sxs-lookup"><span data-stu-id="228ff-136">Run hello following cmdlets tooenable access tooboth deployment models:</span></span>

1. <span data-ttu-id="228ff-137">Ottenere informazioni dettagliate sul circuito hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-137">Get hello circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="228ff-138">Impostare tooTRUE "Consenti operazioni classico".</span><span class="sxs-lookup"><span data-stu-id="228ff-138">Set "Allow Classic Operations" tooTRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="228ff-139">Aggiornare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-139">Update hello circuit.</span></span> <span data-ttu-id="228ff-140">Al termine questa operazione, sarà in grado di tooview circuito di hello nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-140">After this operation has finished successfully, you will be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="228ff-141">Eseguire i seguenti cmdlet tooget hello dettagli di hello circuito ExpressRoute hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-141">Run hello following cmdlet tooget hello details of hello ExpressRoute circuit.</span></span> <span data-ttu-id="228ff-142">È necessario essere in grado di toosee chiave del servizio hello elencati.</span><span class="sxs-lookup"><span data-stu-id="228ff-142">You must be able toosee hello service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="228ff-143">È ora possibile gestire utilizzando i comandi di modello di distribuzione classica hello per le reti virtuali classiche e i comandi di gestione risorse di hello per Gestione risorse VNets il circuito ExpressRoute toohello collegamenti.</span><span class="sxs-lookup"><span data-stu-id="228ff-143">You can now manage links toohello ExpressRoute circuit using hello classic deployment model commands for classic VNets, and hello Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="228ff-144">Hello articoli seguenti consentono di gestire i collegamenti toohello circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="228ff-144">hello following articles help you manage links toohello ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="228ff-145">Collegamento del circuito ExpressRoute nel modello di distribuzione di gestione risorse di hello di tooyour rete virtuale</span><span class="sxs-lookup"><span data-stu-id="228ff-145">Link your virtual network tooyour ExpressRoute circuit in hello Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="228ff-146">Collegamento del circuito ExpressRoute nel modello di distribuzione classica hello di tooyour rete virtuale</span><span class="sxs-lookup"><span data-stu-id="228ff-146">Link your virtual network tooyour ExpressRoute circuit in hello classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="toodisable-expressroute-circuit-access-toohello-classic-deployment-model"></a><span data-ttu-id="228ff-147">modello di distribuzione classica toohello accesso circuito ExpressRoute toodisable</span><span class="sxs-lookup"><span data-stu-id="228ff-147">toodisable ExpressRoute circuit access toohello classic deployment model</span></span>

<span data-ttu-id="228ff-148">Eseguire hello seguente modello di distribuzione classica toohello accesso toodisable cmdlet.</span><span class="sxs-lookup"><span data-stu-id="228ff-148">Run hello following cmdlets toodisable access toohello classic deployment model.</span></span>

1. <span data-ttu-id="228ff-149">Ottenere i dettagli di hello circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="228ff-149">Get details of hello ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="228ff-150">Impostare tooFALSE "Consenti operazioni classico".</span><span class="sxs-lookup"><span data-stu-id="228ff-150">Set "Allow Classic Operations" tooFALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="228ff-151">Aggiornare il circuito hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-151">Update hello circuit.</span></span> <span data-ttu-id="228ff-152">Al termine questa operazione, non sarà in grado di tooview circuito di hello nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="228ff-152">After this operation has finished successfully, you will not be able tooview hello circuit in hello classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="228ff-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="228ff-153">Next steps</span></span>

* [<span data-ttu-id="228ff-154">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="228ff-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="228ff-155">Collegamento del circuito ExpressRoute di tooyour di rete virtuale</span><span class="sxs-lookup"><span data-stu-id="228ff-155">Link your virtual network tooyour ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)
