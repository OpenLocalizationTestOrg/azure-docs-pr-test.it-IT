---
title: Eliminare un cluster di Azure e le risorse correlate | Microsoft Docs
description: Informazioni su come eliminare completamente un cluster Service Fabric rimuovendo il gruppo di risorse contenente il cluster o rimuovendo le risorse in modo selettivo.
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
ms.openlocfilehash: 7672aa12421fbe4ad86e7315d6a7a06c2ff5124d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="delete-a-service-fabric-cluster-on-azure-and-the-resources-it-uses"></a><span data-ttu-id="1dd56-103">Eliminare un cluster Service Fabric in Azure e le risorse che utilizzate</span><span class="sxs-lookup"><span data-stu-id="1dd56-103">Delete a Service Fabric cluster on Azure and the resources it uses</span></span>
<span data-ttu-id="1dd56-104">Un cluster Service Fabric è costituito da molte risorse di Azure oltre alla risorsa cluster stessa.</span><span class="sxs-lookup"><span data-stu-id="1dd56-104">A Service Fabric cluster is made up of many other Azure resources in addition to the cluster resource itself.</span></span> <span data-ttu-id="1dd56-105">Per eliminare completamente un cluster Service Fabric è necessario eliminare anche tutte le risorse di cui è composto.</span><span class="sxs-lookup"><span data-stu-id="1dd56-105">So to completely delete a Service Fabric cluster you also need to delete all the resources it is made of.</span></span>
<span data-ttu-id="1dd56-106">Sono disponibili due opzioni: eliminare il gruppo di risorse contenente il cluster (in modo da rimuovere la risorsa cluster e le altre risorse del gruppo) oppure eliminare la specifica risorsa cluster e le risorse associate (ma non le altre risorse del gruppo).</span><span class="sxs-lookup"><span data-stu-id="1dd56-106">You have two options: Either delete the resource group that the cluster is in (which deletes the cluster resource and any other resources in the resource group) or specifically delete the cluster resource and it's associated resources (but not other resources in the resource group).</span></span>

> [!NOTE]
> <span data-ttu-id="1dd56-107">Quando si elimina la risorsa cluster, tutte le altre risorse che compongono il cluster Service Fabric **non** vengono eliminate.</span><span class="sxs-lookup"><span data-stu-id="1dd56-107">Deleting the cluster resource **does not** delete all the other resources that your Service Fabric cluster is composed of.</span></span>
> 
> 

## <a name="delete-the-entire-resource-group-rg-that-the-service-fabric-cluster-is-in"></a><span data-ttu-id="1dd56-108">Eliminare l'intero gruppo di risorse contenente il cluster Service Fabric</span><span class="sxs-lookup"><span data-stu-id="1dd56-108">Delete the entire resource group (RG) that the Service Fabric cluster is in</span></span>
<span data-ttu-id="1dd56-109">Questo è il modo più semplice per verificare che vengano eliminate tutte le risorse associate al cluster, incluso il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1dd56-109">This is the easiest way to ensure that you delete all the resources associated with your cluster, including the resource group.</span></span> <span data-ttu-id="1dd56-110">È possibile eliminare il gruppo di risorse mediante PowerShell o tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1dd56-110">You can delete the resource group using PowerShell or through the Azure portal.</span></span> <span data-ttu-id="1dd56-111">Se nel gruppo sono incluse risorse non correlate al cluster Service Fabric, è possibile eliminare le risorse specifiche.</span><span class="sxs-lookup"><span data-stu-id="1dd56-111">If your resource group has resources that are not related to Service fabric cluster, then you can delete specific resources.</span></span>

### <a name="delete-the-resource-group-using-azure-powershell"></a><span data-ttu-id="1dd56-112">Eliminare il gruppo di risorse mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1dd56-112">Delete the resource group using Azure PowerShell</span></span>
<span data-ttu-id="1dd56-113">Per eliminare il gruppo di risorse è anche possibile eseguire i cmdlet di Azure PowerShell seguenti.</span><span class="sxs-lookup"><span data-stu-id="1dd56-113">You can also delete the resource group by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="1dd56-114">Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1dd56-114">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="1dd56-115">Se non è ancora installato, seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="1dd56-115">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="1dd56-116">Aprire una finestra di PowerShell ed eseguire i cmdlet di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="1dd56-116">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount

Remove-AzureRmResourceGroup -Name <name of ResouceGroup> -Force
```

<span data-ttu-id="1dd56-117">Verrà visualizzato un prompt per confermare l'eliminazione, se non è stata usata l'opzione *-Force* .</span><span class="sxs-lookup"><span data-stu-id="1dd56-117">You will get a prompt to confirm the deletion if you did not use the *-Force* option.</span></span> <span data-ttu-id="1dd56-118">Al momento della conferma verranno eliminati il gruppo e tutte le risorse incluse.</span><span class="sxs-lookup"><span data-stu-id="1dd56-118">On confirmation the RG and all the resources it contains are deleted.</span></span>

### <a name="delete-a-resource-group-in-the-azure-portal"></a><span data-ttu-id="1dd56-119">Eliminare un gruppo di risorse nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1dd56-119">Delete a resource group in the Azure portal</span></span>
1. <span data-ttu-id="1dd56-120">Eseguire l'accesso al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1dd56-120">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1dd56-121">Passare al cluster Service Fabric da eliminare.</span><span class="sxs-lookup"><span data-stu-id="1dd56-121">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="1dd56-122">Fare clic sul nome del gruppo di risorse nella pagina delle informazioni di base del cluster.</span><span class="sxs-lookup"><span data-stu-id="1dd56-122">Click on the Resource Group name on the cluster essentials page.</span></span>
4. <span data-ttu-id="1dd56-123">Verrà visualizzata la pagina **Informazioni di base** del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1dd56-123">This brings up the **Resource Group Essentials** page.</span></span>
5. <span data-ttu-id="1dd56-124">Fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="1dd56-124">Click **Delete**.</span></span>
6. <span data-ttu-id="1dd56-125">Seguire le istruzioni visualizzate nella pagina per completare l'eliminazione del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1dd56-125">Follow the instructions on that page to complete the deletion of the resource group.</span></span>

![Eliminazione di un gruppo di risorse][ResourceGroupDelete]

## <a name="delete-the-cluster-resource-and-the-resources-it-uses-but-not-other-resources-in-the-resource-group"></a><span data-ttu-id="1dd56-127">Eliminare la risorsa cluster e le risorse correlate, ma non le altre risorse del gruppo</span><span class="sxs-lookup"><span data-stu-id="1dd56-127">Delete the cluster resource and the resources it uses, but not other resources in the resource group</span></span>
<span data-ttu-id="1dd56-128">Se nel gruppo sono incluse solo le risorse correlate al cluster Service Fabric da eliminare, è più semplice eliminare l'intero gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="1dd56-128">If your resource group has only resources that are related to the Service Fabric cluster you want to delete, then it is easier to delete the entire resource group.</span></span> <span data-ttu-id="1dd56-129">Se invece si vuole eliminare in modo selettivo una risorsa alla volta nel gruppo, seguire questa procedura.</span><span class="sxs-lookup"><span data-stu-id="1dd56-129">If you want to selectively delete the resources one-by-one in your resource group, then follow these steps.</span></span>

<span data-ttu-id="1dd56-130">Se il cluster è stato distribuito mediante il portale o tramite uno dei modelli Resource Manager di Service Fabric inclusi nella raccolta dei modelli, tutte le risorse usate dal cluster vengono contrassegnate con i due tag seguenti.</span><span class="sxs-lookup"><span data-stu-id="1dd56-130">If you deployed your cluster using the portal or using one of the Service Fabric Resource Manager templates from the template gallery, then all the resources that the cluster uses are tagged with the following two tags.</span></span> <span data-ttu-id="1dd56-131">Questi tag sono utili per identificare le risorse da eliminare.</span><span class="sxs-lookup"><span data-stu-id="1dd56-131">You can use them to decide which resources you want to delete.</span></span>

<span data-ttu-id="1dd56-132">***Tag#1:*** chiave = clusterName, valore = 'nome del cluster'</span><span class="sxs-lookup"><span data-stu-id="1dd56-132">***Tag#1:*** Key = clusterName, Value = 'name of the cluster'</span></span>

<span data-ttu-id="1dd56-133">***Tag#2:*** chiave = resourceName, valore = ServiceFabric</span><span class="sxs-lookup"><span data-stu-id="1dd56-133">***Tag#2:*** Key = resourceName, Value = ServiceFabric</span></span>

### <a name="delete-specific-resources-in-the-azure-portal"></a><span data-ttu-id="1dd56-134">Eliminare risorse specifiche nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1dd56-134">Delete specific resources in the Azure portal</span></span>
1. <span data-ttu-id="1dd56-135">Eseguire l'accesso al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1dd56-135">Login to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1dd56-136">Passare al cluster Service Fabric da eliminare.</span><span class="sxs-lookup"><span data-stu-id="1dd56-136">Navigate to the Service Fabric cluster you want to delete.</span></span>
3. <span data-ttu-id="1dd56-137">Scegliere **Tutte le impostazioni** nel pannello Informazioni di base.</span><span class="sxs-lookup"><span data-stu-id="1dd56-137">Go to **All settings** on the essentials blade.</span></span>
4. <span data-ttu-id="1dd56-138">Fare clic su **Tag** in **Gestione risorse** nel pannello delle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="1dd56-138">Click on **Tags** under **Resource Management** in the settings blade.</span></span>
5. <span data-ttu-id="1dd56-139">Fare clic su uno dei **tag** nel pannello Tag per ottenere l'elenco di tutte le risorse con il tag selezionato.</span><span class="sxs-lookup"><span data-stu-id="1dd56-139">Click on one of the **Tags** in the tags blade to get a list of all the resources with that tag.</span></span>
   
    ![Tag delle risorse][ResourceTags]
6. <span data-ttu-id="1dd56-141">Nell'elenco delle risorse contrassegnate con il tag fare clic su ciascuna risorsa ed eliminarla.</span><span class="sxs-lookup"><span data-stu-id="1dd56-141">Once you have the list of tagged resources, click on each of the resources and delete them.</span></span>
   
    ![Risorse con tag][TaggedResources]

### <a name="delete-the-resources-using-azure-powershell"></a><span data-ttu-id="1dd56-143">Eliminare le risorse mediante Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1dd56-143">Delete the resources using Azure PowerShell</span></span>
<span data-ttu-id="1dd56-144">Per eliminare una risorsa alla volta è possibile eseguire i cmdlet di Azure PowerShell seguenti.</span><span class="sxs-lookup"><span data-stu-id="1dd56-144">You can delete the resources one-by-one by running the following Azure PowerShell cmdlets.</span></span> <span data-ttu-id="1dd56-145">Verificare che nel computer sia installato Azure PowerShell 1.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="1dd56-145">Make sure Azure PowerShell 1.0 or greater is installed on your computer.</span></span> <span data-ttu-id="1dd56-146">Se non è ancora installato, seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="1dd56-146">If you have not done this before, follow the steps outlined in [How to install and Configure Azure PowerShell.](/powershell/azure/overview)</span></span>

<span data-ttu-id="1dd56-147">Aprire una finestra di PowerShell ed eseguire i cmdlet di PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="1dd56-147">Open a PowerShell window and run the following PS cmdlets:</span></span>

```powershell
Login-AzureRmAccount
```
<span data-ttu-id="1dd56-148">Per ogni risorsa da eliminare, eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="1dd56-148">For each of the resources you want to delete, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "<Resource Type>" -ResourceGroupName "<name of the resource group>" -Force
```

<span data-ttu-id="1dd56-149">Per eliminare la risorsa cluster, eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="1dd56-149">To delete the cluster resource, run the following:</span></span>

```powershell
Remove-AzureRmResource -ResourceName "<name of the Resource>" -ResourceType "Microsoft.ServiceFabric/clusters" -ResourceGroupName "<name of the resource group>" -Force
```

## <a name="next-steps"></a><span data-ttu-id="1dd56-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1dd56-150">Next steps</span></span>
<span data-ttu-id="1dd56-151">Per altre informazioni sull'aggiornamento di un cluster e il partizionamento dei servizi, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="1dd56-151">Read the following to also learn about upgrading a cluster and partitioning services:</span></span>

* [<span data-ttu-id="1dd56-152">Informazioni sugli aggiornamenti dei cluster</span><span class="sxs-lookup"><span data-stu-id="1dd56-152">Learn about cluster upgrades</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="1dd56-153">Informazioni sul partizionamento dei servizi con stato per la massima scalabilità</span><span class="sxs-lookup"><span data-stu-id="1dd56-153">Learn about partitioning stateful services for maximum scale</span></span>](service-fabric-concepts-partitioning.md)

<!--Image references-->
[ResourceGroupDelete]: ./media/service-fabric-cluster-delete/ResourceGroupDelete.PNG

[ResourceTags]: ./media/service-fabric-cluster-delete/ResourceTags.png

[TaggedResources]: ./media/service-fabric-cluster-delete/TaggedResources.PNG
