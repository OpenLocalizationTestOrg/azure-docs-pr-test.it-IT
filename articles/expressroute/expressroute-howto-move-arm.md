---
title: 'Spostare i circuiti ExpressRoute dal modello classico al modello Resource Manager: PowerShell: Azure | Microsoft Docs'
description: Questa pagina illustra come spostare un circuito classico nel modello di distribuzione Resource Manager usando PowerShell.
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
ms.openlocfilehash: c407e01e6d881cb8adcfe55faa246468669be883
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="move-expressroute-circuits-from-the-classic-to-the-resource-manager-deployment-model-using-powershell"></a><span data-ttu-id="036c0-103">Spostare i circuiti ExpressRoute dal modello di distribuzione classica a quello Resource Manager usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="036c0-103">Move ExpressRoute circuits from the classic to the Resource Manager deployment model using PowerShell</span></span>

<span data-ttu-id="036c0-104">Per usare un circuito ExpressRoute per il modello di distribuzione classica e per Resource Manager,è necessario spostare il circuito nel modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="036c0-104">To use an ExpressRoute circuit for both the classic and Resource Manager deployment models, you must move the circuit to the Resource Manager deployment model.</span></span> <span data-ttu-id="036c0-105">Le sezioni seguenti descrivono come spostare il circuito tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="036c0-105">The following sections help you move your circuit by using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="036c0-106">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="036c0-106">Before you begin</span></span>

* <span data-ttu-id="036c0-107">Verificare di avere la versione più recente dei moduli di Azure PowerShell (almeno la versione 1.0).</span><span class="sxs-lookup"><span data-stu-id="036c0-107">Verify that you have the latest version of the Azure PowerShell modules (at least version 1.0).</span></span> <span data-ttu-id="036c0-108">Per altre informazioni, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="036c0-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="036c0-109">Prima di procedere con la configurazione, assicurarsi di avere verificato i [prerequisiti](expressroute-prerequisites.md), i [requisiti di routing](expressroute-routing.md) e i [flussi di lavoro](expressroute-workflows.md).</span><span class="sxs-lookup"><span data-stu-id="036c0-109">Make sure that you have reviewed the [prerequisites](expressroute-prerequisites.md), [routing requirements](expressroute-routing.md), and [workflows](expressroute-workflows.md) before you begin configuration.</span></span>
* <span data-ttu-id="036c0-110">Rivedere le informazioni disponibili in [Spostamento dei circuiti ExpressRoute dal modello di distribuzione classica al modello di distribuzione Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="036c0-110">Review the information that is provided under [Moving an ExpressRoute circuit from classic to Resource Manager](expressroute-move.md).</span></span> <span data-ttu-id="036c0-111">Assicurarsi di aver compreso pienamente i limiti e le limitazioni.</span><span class="sxs-lookup"><span data-stu-id="036c0-111">Make sure that you fully understand the limits and limitations.</span></span>
* <span data-ttu-id="036c0-112">Verificare che il circuito sia completamente operativo nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="036c0-112">Verify that the circuit is fully operational in the classic deployment model.</span></span>
* <span data-ttu-id="036c0-113">Assicurarsi che sia disponibile un gruppo di risorse creato nel modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="036c0-113">Ensure that you have a resource group that was created in the Resource Manager deployment model.</span></span>

## <a name="move-an-expressroute-circuit"></a><span data-ttu-id="036c0-114">Spostare un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="036c0-114">Move an ExpressRoute circuit</span></span>

### <a name="step-1-gather-circuit-details-from-the-classic-deployment-model"></a><span data-ttu-id="036c0-115">Passaggio 1: Raccogliere informazioni dettagliate sul circuito dal modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="036c0-115">Step 1: Gather circuit details from the classic deployment model</span></span>

<span data-ttu-id="036c0-116">Accedere all'ambiente Azure classico e quindi ottenere la chiave servizio.</span><span class="sxs-lookup"><span data-stu-id="036c0-116">Sign in to the Azure classic environment and gather the service key.</span></span>

1. <span data-ttu-id="036c0-117">Accedere all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="036c0-117">Sign in to your Azure account.</span></span>

  ```powershell
  Add-AzureAccount
  ```

2. <span data-ttu-id="036c0-118">Selezionare la sottoscrizione di Azure appropriata.</span><span class="sxs-lookup"><span data-stu-id="036c0-118">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Select-AzureSubscription "<Enter Subscription Name here>"
  ```

3. <span data-ttu-id="036c0-119">Importare i moduli di PowerShell per Azure ed ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="036c0-119">Import the PowerShell modules for Azure and ExpressRoute.</span></span>

  ```powershell
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\Azure.psd1'
  Import-Module 'C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\ServiceManagement\Azure\ExpressRoute\ExpressRoute.psd1'
  ```

4. <span data-ttu-id="036c0-120">Usare il cmdlet seguente per ottenere le chiavi servizio per tutti i circuiti ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="036c0-120">Use the cmdlet below to get the service keys for all of your ExpressRoute circuits.</span></span> <span data-ttu-id="036c0-121">Dopo avere recuperato le chiavi, copiare la **chiave servizio** del circuito che si desidera spostare nel modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="036c0-121">After retrieving the keys, copy the **service key** of the circuit that you want to move to the Resource Manager deployment model.</span></span>

  ```powershell
  Get-AzureDedicatedCircuit
  ```

### <a name="step-2-sign-in-and-create-a-resource-group"></a><span data-ttu-id="036c0-122">Passaggio 2: Accedere e creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="036c0-122">Step 2: Sign in and create a resource group</span></span>

<span data-ttu-id="036c0-123">Accedere all'ambiente Resource Manager e creare un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="036c0-123">Sign in to the Resource Manager environment and create a new resource group.</span></span>

1. <span data-ttu-id="036c0-124">Accedere all'ambiente Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="036c0-124">Sign in to your Azure Resource Manager environment.</span></span>

  ```powershell
  Login-AzureRmAccount
  ```

2. <span data-ttu-id="036c0-125">Selezionare la sottoscrizione di Azure appropriata.</span><span class="sxs-lookup"><span data-stu-id="036c0-125">Select the appropriate Azure subscription.</span></span>

  ```powershell
  Get-AzureRmSubscription -SubscriptionName "<Enter Subscription Name here>" | Select-AzureRmSubscription
  ```

3. <span data-ttu-id="036c0-126">Modificare il frammento seguente per creare un nuovo gruppo di risorse se non si dispone già di un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="036c0-126">Modify the snippet below to create a new resource group if you don't already have a resource group.</span></span>

  ```powershell
  New-AzureRmResourceGroup -Name "DemoRG" -Location "West US"
  ```

### <a name="step-3-move-the-expressroute-circuit-to-the-resource-manager-deployment-model"></a><span data-ttu-id="036c0-127">Passaggio 3: Spostare il circuito ExpressRoute nel modello di distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="036c0-127">Step 3: Move the ExpressRoute circuit to the Resource Manager deployment model</span></span>

<span data-ttu-id="036c0-128">È ora possibile spostare il circuito ExpressRoute dal modello di distribuzione classica al modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="036c0-128">You are now ready to move your ExpressRoute circuit from the classic deployment model to the Resource Manager deployment model.</span></span> <span data-ttu-id="036c0-129">Prima di continuare, verificare le informazioni disponibili in [Spostamento di un circuito ExpressRoute dal modello di distribuzione classica al modello di distribuzione Resource Manager](expressroute-move.md).</span><span class="sxs-lookup"><span data-stu-id="036c0-129">Before proceeding, review the information provided in [Moving an ExpressRoute circuit from the classic to the Resource Manager deployment model](expressroute-move.md).</span></span>

<span data-ttu-id="036c0-130">Per spostare il circuito, modificare ed eseguire il frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="036c0-130">To move your circuit, modify and run the following snippet:</span></span>

```powershell
Move-AzureRmExpressRouteCircuit -Name "MyCircuit" -ResourceGroupName "DemoRG" -Location "West US" -ServiceKey "<Service-key>"
```

> [!NOTE]
> <span data-ttu-id="036c0-131">Al termine dello spostamento, il nuovo nome elencato nel cmdlet precedente verrà usato per fare riferimento alla risorsa.</span><span class="sxs-lookup"><span data-stu-id="036c0-131">After the move has finished, the new name that is listed in the previous cmdlet will be used to address the resource.</span></span> <span data-ttu-id="036c0-132">Il circuito verrà essenzialmente rinominato.</span><span class="sxs-lookup"><span data-stu-id="036c0-132">The circuit will essentially be renamed.</span></span>
> 

## <a name="modify-circuit-access"></a><span data-ttu-id="036c0-133">Modificare l'accesso al circuito</span><span class="sxs-lookup"><span data-stu-id="036c0-133">Modify circuit access</span></span>

### <a name="to-enable-expressroute-circuit-access-for-both-deployment-models"></a><span data-ttu-id="036c0-134">Per abilitare il circuito ExpressRoute accedere ad entrambi i modelli di distribuzione</span><span class="sxs-lookup"><span data-stu-id="036c0-134">To enable ExpressRoute circuit access for both deployment models</span></span>

<span data-ttu-id="036c0-135">Dopo aver spostato il circuito ExpressRoute classico nel modello di distribuzione Resource Manager, è possibile abilitare l'accesso a entrambi i modelli di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="036c0-135">After moving your classic ExpressRoute circuit to the Resource Manager deployment model, you can enable access to both deployment models.</span></span> <span data-ttu-id="036c0-136">Eseguire i cmdlet seguenti per abilitare l'accesso a entrambi i modelli di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="036c0-136">Run the following cmdlets to enable access to both deployment models:</span></span>

1. <span data-ttu-id="036c0-137">Ottenere i dettagli del circuito.</span><span class="sxs-lookup"><span data-stu-id="036c0-137">Get the circuit details.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="036c0-138">Impostare "Allow Classic Operations" (Consenti operazioni classiche) su VERO.</span><span class="sxs-lookup"><span data-stu-id="036c0-138">Set "Allow Classic Operations" to TRUE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $true
  ```

3. <span data-ttu-id="036c0-139">Aggiornamento del circuito.</span><span class="sxs-lookup"><span data-stu-id="036c0-139">Update the circuit.</span></span> <span data-ttu-id="036c0-140">Al termine di questa operazione, sarà possibile visualizzare il circuito nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="036c0-140">After this operation has finished successfully, you will be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
  Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

4. <span data-ttu-id="036c0-141">Eseguire il cmdlet seguente per ottenere i dettagli del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="036c0-141">Run the following cmdlet to get the details of the ExpressRoute circuit.</span></span> <span data-ttu-id="036c0-142">Si dovrebbe essere in grado di vedere la chiave servizio elencata.</span><span class="sxs-lookup"><span data-stu-id="036c0-142">You must be able to see the service key listed.</span></span>

  ```powershell
  get-azurededicatedcircuit
  ```

5. <span data-ttu-id="036c0-143">È ora possibile gestire i collegamenti al circuito ExpressRoute usando i comandi del modello di distribuzione classica per le reti virtuali classiche e i comandi di Resource Manager per le reti virtuali di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="036c0-143">You can now manage links to the ExpressRoute circuit using the classic deployment model commands for classic VNets, and the Resource Manager commands for Resource Manager VNets.</span></span> <span data-ttu-id="036c0-144">Gli articoli seguenti descrivono come gestire i collegamenti al circuito ExpressRoute:</span><span class="sxs-lookup"><span data-stu-id="036c0-144">The following articles help you manage links to the ExpressRoute circuit:</span></span>

    * [<span data-ttu-id="036c0-145">Collegare la rete virtuale al circuito ExpressRoute nel modello di distribuzione Resource Manager</span><span class="sxs-lookup"><span data-stu-id="036c0-145">Link your virtual network to your ExpressRoute circuit in the Resource Manager deployment model</span></span>](expressroute-howto-linkvnet-arm.md)
    * [<span data-ttu-id="036c0-146">Collegare la rete virtuale al circuito ExpressRoute nel modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="036c0-146">Link your virtual network to your ExpressRoute circuit in the classic deployment model</span></span>](expressroute-howto-linkvnet-classic.md)

### <a name="to-disable-expressroute-circuit-access-to-the-classic-deployment-model"></a><span data-ttu-id="036c0-147">Per disabilitare l'accesso del circuito ExpressRoute al modello di distribuzione classica</span><span class="sxs-lookup"><span data-stu-id="036c0-147">To disable ExpressRoute circuit access to the classic deployment model</span></span>

<span data-ttu-id="036c0-148">Eseguire i cmdlet seguenti per disabilitare l'accesso al modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="036c0-148">Run the following cmdlets to disable access to the classic deployment model.</span></span>

1. <span data-ttu-id="036c0-149">Ottenere i dettagli del circuito ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="036c0-149">Get details of the ExpressRoute circuit.</span></span>

  ```powershell
  $ckt = Get-AzureRmExpressRouteCircuit -Name "DemoCkt" -ResourceGroupName "DemoRG"
  ```

2. <span data-ttu-id="036c0-150">Impostare "Allow Classic Operations" (Consenti operazioni classiche) su FALSO.</span><span class="sxs-lookup"><span data-stu-id="036c0-150">Set "Allow Classic Operations" to FALSE.</span></span>

  ```powershell
  $ckt.AllowClassicOperations = $false
  ```

3. <span data-ttu-id="036c0-151">Aggiornamento del circuito.</span><span class="sxs-lookup"><span data-stu-id="036c0-151">Update the circuit.</span></span> <span data-ttu-id="036c0-152">Al termine di questa operazione, non sarà possibile visualizzare il circuito nel modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="036c0-152">After this operation has finished successfully, you will not be able to view the circuit in the classic deployment model.</span></span>

  ```powershell
Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
  ```

## <a name="next-steps"></a><span data-ttu-id="036c0-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="036c0-153">Next steps</span></span>

* [<span data-ttu-id="036c0-154">Creare e modificare il routing per un circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="036c0-154">Create and modify routing for your ExpressRoute circuit</span></span>](expressroute-howto-routing-arm.md)
* [<span data-ttu-id="036c0-155">Collegare la rete virtuale al circuito ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="036c0-155">Link your virtual network to your ExpressRoute circuit</span></span>](expressroute-howto-linkvnet-arm.md)