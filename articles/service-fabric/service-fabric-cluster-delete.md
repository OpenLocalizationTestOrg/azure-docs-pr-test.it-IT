---
title: aaaDelete di Azure cluster e le relative risorse | Documenti Microsoft
description: Informazioni su come toocompletely Elimina un'infrastruttura di servizio cluster un gruppo di risorse hello eliminazione contenente cluster hello o eliminando in modo selettivo le risorse.
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: de422950-2d22-4ddb-ac47-dd663a946a7e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/24/2017
ms.author: chackdan
ms.openlocfilehash: 5c15a4184644da715cd69397f2150de86ab433ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-hello-resources-it-uses"></a><span data-ttu-id="200d5-103">Eliminare un cluster di Service Fabric sulle risorse di Azure e hello che usa</span><span class="sxs-lookup"><span data-stu-id="200d5-103">Delete a Service Fabric cluster on Azure and hello resources it uses</span></span>
<span data-ttu-id="200d5-104">Un cluster di Service Fabric è costituito da molte altre risorse di Azure inoltre toohello risorsa del cluster stesso.</span><span class="sxs-lookup"><span data-stu-id="200d5-104">A Service Fabric cluster is made up of many other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="200d5-105">In modo toocompletely eliminare un cluster di Service Fabric è inoltre necessario toodelete che tutti hello è composto di risorse.</span><span class="sxs-lookup"><span data-stu-id="200d5-105">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span>
<span data-ttu-id="200d5-106">Sono disponibili due opzioni: è un gruppo di risorse hello delete hello cluster in (che elimina risorsa cluster hello e altre risorse nel gruppo di risorse hello) o eliminare in modo specifico la risorsa di cluster hello e sono associati alle risorse (ma non altri risorse nel gruppo di risorse hello).</span><span class="sxs-lookup"><span data-stu-id="200d5-106">You have two options: Either delete hello resource group that hello cluster is in (which deletes hello cluster resource and any other resources in hello resource group) or specifically delete hello cluster resource and it's associated resources (but not other resources in hello resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="200d5-107">L'eliminazione di risorse cluster hello **non** tutti hello altre risorse del cluster di Service Fabric è composta da eliminare.</span><span class="sxs-lookup"><span data-stu-id="200d5-107">Deleting hello cluster resource **does not** delete all hello other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-hello-entire-resource-group-rg-that-hello-service-fabric-cluster-is-in"></a><span data-ttu-id="200d5-108">Eliminare hello intero gruppo di risorse (RG) che hello cluster di Service Fabric</span><span class="sxs-lookup"><span data-stu-id="200d5-108">Delete hello entire resource group (RG) that hello Service Fabric cluster is in</span></span>
<span data-ttu-id="200d5-109">Si tratta di tooensure modo più semplice hello di eliminare tutte le risorse di hello associate al cluster, inclusi il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="200d5-109">This is hello easiest way tooensure that you delete all hello resources associated with your cluster, including hello resource group.</span></span> <span data-ttu-id="200d5-110">È possibile eliminare il gruppo di risorse hello tramite PowerShell o tramite hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="200d5-110">You can delete hello resource group using PowerShell or through hello Azure portal.</span></span> <span data-ttu-id="200d5-111">Se il gruppo di risorse include risorse che non sono correlati tooService cluster di infrastruttura, è possibile eliminare le risorse specifiche.</span><span class="sxs-lookup"><span data-stu-id="200d5-111">If your resource group has resources that are not related tooService fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-hello-resource-group-using-azure-powershell"></a><span data-ttu-id="200d5-112">Eliminare il gruppo di risorse hello con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="200d5-112">Delete hello resource group using Azure PowerShell</span></span>
<span data-ttu-id="200d5-113">È anche possibile eliminare il gruppo di risorse hello eseguendo hello seguendo i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="200d5-113">You can also delete hello resource group by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="200d5-114">Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="200d5-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="200d5-115">Se non è stata eseguita questa operazione prima di, seguire i passaggi di hello illustrati in [come tooinstall e configurare Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="200d5-115">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="200d5-116">Aprire una finestra di PowerShell ed eseguire hello cmdlet di Powershell seguente:</span><span class="sxs-lookup"><span data-stu-id="200d5-116">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="200d5-117">Si otterrà l'eliminazione dei messaggi di richiesta tooconfirm hello se non è stato utilizzato hello *-Force* opzione.</span><span class="sxs-lookup"><span data-stu-id="200d5-117">You will get a prompt tooconfirm hello deletion if you did not use hello *-Force* option.</span></span> <span data-ttu-id="200d5-118">In conferma hello RG e vengono eliminate tutte le risorse di hello che contiene.</span><span class="sxs-lookup"><span data-stu-id="200d5-118">On confirmation hello RG and all hello resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-hello-azure-portal"></a><span data-ttu-id="200d5-119">Eliminare un gruppo di risorse in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="200d5-119">Delete a resource group in hello Azure portal</span></span>
1. <span data-ttu-id="200d5-120">Account di accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="200d5-120">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="200d5-121">Passare il cluster di Service Fabric toohello da toodelete.</span><span class="sxs-lookup"><span data-stu-id="200d5-121">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="200d5-122">Fare clic su hello Nome gruppo di risorse nella pagina di essentials hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="200d5-122">Click on hello Resource Group name on hello cluster essentials page.</span></span>
4. <span data-ttu-id="200d5-123">Verrà visualizzata hello **risorse gruppo Essentials** pagina.</span><span class="sxs-lookup"><span data-stu-id="200d5-123">This brings up hello **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="200d5-124">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="200d5-124">Click **Delete**.</span></span>
6. <span data-ttu-id="200d5-125">Seguire le istruzioni di hello l'eliminazione di hello toocomplete pagina hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="200d5-125">Follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>

![Eliminazione di un gruppo di risorse][ResourceGroupDelete]

## <a name="delete-hello-cluster-resource-and-hello-resources-it-uses-but-not-other-resources-in-hello-resource-group"></a><span data-ttu-id="200d5-127">Eliminare una risorsa cluster hello e risorse di hello che viene utilizzato, ma non ad altre risorse nel gruppo di risorse hello</span><span class="sxs-lookup"><span data-stu-id="200d5-127">Delete hello cluster resource and hello resources it uses, but not other resources in hello resource group</span></span>
<span data-ttu-id="200d5-128">Se il gruppo di risorse contiene solo le risorse cluster di Service Fabric toohello correlati si desidera toodelete, quindi è più facile toodelete hello intero gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="200d5-128">If your resource group has only resources that are related toohello Service Fabric cluster you want toodelete, then it is easier toodelete hello entire resource group.</span></span> <span data-ttu-id="200d5-129">Se si desiderano risorse hello di eliminazione tooselectively uno alla volta nel gruppo di risorse, attenersi alla seguente procedura.</span><span class="sxs-lookup"><span data-stu-id="200d5-129">If you want tooselectively delete hello resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="200d5-130">Se è stato distribuito il cluster usando il portale di hello o usando uno dei modelli di gestione risorse di infrastruttura servizio hello dalla raccolta di modelli di hello, tutte le risorse hello hello cluster utilizza sono contrassegnate con hello due tag seguenti.</span><span class="sxs-lookup"><span data-stu-id="200d5-130">If you deployed your cluster using hello portal or using one of hello Service Fabric Resource Manager templates from hello template gallery, then all hello resources that hello cluster uses are tagged with hello following two tags.</span></span> <span data-ttu-id="200d5-131">È possibile usarli toodecide le risorse che si desidera toodelete.</span><span class="sxs-lookup"><span data-stu-id="200d5-131">You can use them toodecide which resources you want toodelete.</span></span>

<span data-ttu-id="200d5-132">***Tag n. 1:*** chiave = NomeCluster, valore = 'nome del cluster hello'</span><span class="sxs-lookup"><span data-stu-id="200d5-132">***Tag#1:*** Key = clusterName, Value = 'name of hello cluster'</span></span>

<span data-ttu-id="200d5-133">***Tag#2:*** chiave = resourceName, valore = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="200d5-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-hello-azure-portal"></a><span data-ttu-id="200d5-134">Elimina le risorse specifiche in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="200d5-134">Delete specific resources in hello Azure portal</span></span>
1. <span data-ttu-id="200d5-135">Account di accesso toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="200d5-135">Login toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="200d5-136">Passare il cluster di Service Fabric toohello da toodelete.</span><span class="sxs-lookup"><span data-stu-id="200d5-136">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
3. <span data-ttu-id="200d5-137">Andare troppo**tutte le impostazioni** nel Pannello di essentials hello.</span><span class="sxs-lookup"><span data-stu-id="200d5-137">Go too**All settings** on hello essentials blade.</span></span>
4. <span data-ttu-id="200d5-138">Fare clic su **tag** in **la gestione delle risorse** nel pannello impostazioni hello.</span><span class="sxs-lookup"><span data-stu-id="200d5-138">Click on **Tags** under **Resource Management** in hello settings blade.</span></span>
5. <span data-ttu-id="200d5-139">Fare clic su uno di hello **tag** in hello tag pannello tooget un elenco di tutte le risorse di hello con tale tag.</span><span class="sxs-lookup"><span data-stu-id="200d5-139">Click on one of hello **Tags** in hello tags blade tooget a list of all hello resources with that tag.</span></span>
   
    ![Tag delle risorse][ResourceTags]
6. <span data-ttu-id="200d5-141">Dopo aver creato elenco hello delle risorse con tag, fare clic su ognuna delle risorse hello ed eliminarli.</span><span class="sxs-lookup"><span data-stu-id="200d5-141">Once you have hello list of tagged resources, click on each of hello resources and delete them.</span></span>
   
    ![Risorse con tag][TaggedResources]

### <a name="delete-hello-resources-using-azure-powershell"></a><span data-ttu-id="200d5-143">Eliminare le risorse di hello con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="200d5-143">Delete hello resources using Azure PowerShell</span></span>
<span data-ttu-id="200d5-144">È possibile eliminare le risorse hello uno alla volta eseguendo hello seguendo i cmdlet PowerShell di Azure.</span><span class="sxs-lookup"><span data-stu-id="200d5-144">You can delete hello resources one-by-one by running hello following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="200d5-145">Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="200d5-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="200d5-146">Se non è stata eseguita questa operazione prima di, seguire i passaggi di hello illustrati in [come tooinstall e configurare Azure PowerShell.](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="200d5-146">If you have not done this before, follow hello steps outlined in [How tooinstall and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="200d5-147">Aprire una finestra di PowerShell ed eseguire hello cmdlet di Powershell seguente:</span><span class="sxs-lookup"><span data-stu-id="200d5-147">Open a PowerShell window and run hello following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="200d5-148">Per ogni risorsa hello toodelete desiderata, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="200d5-148">For each of hello resources you want toodelete, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of hello resource group>" -Force
```

<span data-ttu-id="200d5-149">risorsa di cluster di hello di toodelete, eseguire hello seguente:</span><span class="sxs-lookup"><span data-stu-id="200d5-149">toodelete hello cluster resource, run hello following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of hello Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of hello resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="200d5-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="200d5-150">Next steps</span></span>
<span data-ttu-id="200d5-151">Hello lettura seguente tooalso informazioni sull'aggiornamento di un cluster e partizionamento servizi:</span><span class="sxs-lookup"><span data-stu-id="200d5-151">Read hello following tooalso learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="200d5-152">Informazioni sugli aggiornamenti dei cluster</span><span class="sxs-lookup"><span data-stu-id="200d5-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="200d5-153">Informazioni sul partizionamento dei servizi con stato per la massima scalabilità</span><span class="sxs-lookup"><span data-stu-id="200d5-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
