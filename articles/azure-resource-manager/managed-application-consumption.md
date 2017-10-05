---
title: Utilizzare un'applicazione gestita di Azure | Microsoft Docs
description: Descrive come un cliente crea un'applicazione gestita di Azure dai file pubblicati.
services: azure-resource-manager
author: ravbhatnagar
manager: rjmax
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 08/23/2017
ms.author: gauravbh; tomfitz
ms.openlocfilehash: ed8fbaf2a4546c8e31eeced11cd0b5627fd62c0c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="8e249-103">Usare un'applicazione gestita interna</span><span class="sxs-lookup"><span data-stu-id="8e249-103">Consume an internal managed application</span></span>

<span data-ttu-id="8e249-104">È possibile usare [applicazioni gestite](managed-application-overview.md) di Azure studiate per i membri della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8e249-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="8e249-105">È, ad esempio, possibile selezionare applicazioni gestite disponibili dal reparto IT che garantiscano la conformità agli standard aziendali.</span><span class="sxs-lookup"><span data-stu-id="8e249-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="8e249-106">Queste applicazioni gestite sono disponibili nel catalogo dei servizi, non in Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="8e249-106">These managed applications are available through the Service Catalog, not the Azure Marketplace.</span></span>

<span data-ttu-id="8e249-107">Prima di procedere con questo articolo, è necessario disporre di un'applicazione gestita nel catalogo dei servizi per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="8e249-107">Before proceeding with this article, you must have a managed application available in the service catalog for your subscription.</span></span> <span data-ttu-id="8e249-108">Se qualcuno nell'organizzazione ha già creato un'applicazione gestita, vedere [Creare e pubblicare un'applicazione gestita di Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8e249-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="8e249-109">Attualmente, per usare un'applicazione gestita è possibile usare l'interfaccia della riga di comando di Azure o il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e249-109">Currently, you can use either Azure CLI or the Azure portal to consume a managed application.</span></span>

## <a name="create-the-managed-application-by-using-the-portal"></a><span data-ttu-id="8e249-110">Creare l'applicazione gestita con il portale</span><span class="sxs-lookup"><span data-stu-id="8e249-110">Create the managed application by using the portal</span></span>

<span data-ttu-id="8e249-111">Per distribuire un'applicazione gestita tramite il portale, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="8e249-111">To deploy a managed application through the portal, follow these steps:</span></span>

1. <span data-ttu-id="8e249-112">Accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e249-112">Go to the Azure portal.</span></span> <span data-ttu-id="8e249-113">Cercare **Service Catalog Managed Application** (Applicazione gestita del catalogo di servizi).</span><span class="sxs-lookup"><span data-stu-id="8e249-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Applicazione gestita del catalogo di servizi](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="8e249-115">Selezionare l'applicazione gestita che si vuole creare dall'elenco di soluzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="8e249-115">Select the managed application you want to create from the list of available solutions.</span></span> <span data-ttu-id="8e249-116">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="8e249-116">Select **Create**.</span></span>

   ![Selezione di applicazioni gestite](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="8e249-118">Immettere i parametri necessari per il provisioning delle risorse.</span><span class="sxs-lookup"><span data-stu-id="8e249-118">Provide values for the parameters that are required to provision the resources.</span></span> <span data-ttu-id="8e249-119">Selezionare **West Central US** (Stati Uniti centro-occidentali) per il percorso.</span><span class="sxs-lookup"><span data-stu-id="8e249-119">Select **West Central US** for location.</span></span> <span data-ttu-id="8e249-120">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="8e249-120">Select **OK**.</span></span>

   ![Parametri delle applicazioni gestite](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="8e249-122">Il modello convalida i valori specificati.</span><span class="sxs-lookup"><span data-stu-id="8e249-122">The template validates the values you provided.</span></span> <span data-ttu-id="8e249-123">Se la convalida ha esito positivo, selezionare **OK** per iniziare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="8e249-123">If validation succeeds, select **OK** to start the deployment.</span></span>

   ![Convalida dell'applicazione gestita](./media/managed-application-consumption/validation.png)

<span data-ttu-id="8e249-125">Al termine della distribuzione, nel gruppo di risorse gestite specificato viene eseguito il provisioning delle risorse appropriate definite nel modello.</span><span class="sxs-lookup"><span data-stu-id="8e249-125">After the deployment finishes, the appropriate resources defined in the template are provisioned in the managed resource group you provided.</span></span>

## <a name="create-the-managed-application-by-using-azure-cli"></a><span data-ttu-id="8e249-126">Creare l'applicazione gestita con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="8e249-126">Create the managed application by using Azure CLI</span></span>

<span data-ttu-id="8e249-127">A tale scopo, è possibile procedere in due modi usando l'interfaccia della riga di comando di Azure per creare un'applicazione gestita:</span><span class="sxs-lookup"><span data-stu-id="8e249-127">There are two ways to create a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="8e249-128">Usare il comando per la creazione di applicazioni gestite.</span><span class="sxs-lookup"><span data-stu-id="8e249-128">Use the command for creating managed applications.</span></span>
* <span data-ttu-id="8e249-129">Usare il normale comando di distribuzione modelli.</span><span class="sxs-lookup"><span data-stu-id="8e249-129">Use the regular template deployment command.</span></span>

### <a name="use-the-template-deployment-command"></a><span data-ttu-id="8e249-130">Usare il comando di distribuzione modelli.</span><span class="sxs-lookup"><span data-stu-id="8e249-130">Use the template deployment command</span></span>

<span data-ttu-id="8e249-131">Distribuire il file applianceMainTemplate.json creato dal fornitore.</span><span class="sxs-lookup"><span data-stu-id="8e249-131">Deploy the applianceMainTemplate.json file that the vendor created.</span></span>

<span data-ttu-id="8e249-132">Creare quindi due gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="8e249-132">Then create two resource groups.</span></span> <span data-ttu-id="8e249-133">Il primo gruppo di risorse deve essere creato nel punto in cui viene creata la risorsa applicazione gestita: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="8e249-133">The first resource group is where the managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="8e249-134">Il secondo gruppo contiene tutte le risorse definite nel file mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8e249-134">The second resource group contains all the resources defined in mainTemplate.json.</span></span> <span data-ttu-id="8e249-135">Questo gruppo di risorse è gestito dal fornitore di software indipendente.</span><span class="sxs-lookup"><span data-stu-id="8e249-135">This resource group is managed by the ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="8e249-136">Usare `westcentralus` come località del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8e249-136">Use `westcentralus` as the location of the resource group.</span></span>
>

<span data-ttu-id="8e249-137">Per distribuire il file applianceMainTemplate.json in mainResourceGroup, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="8e249-137">To deploy applianceMainTemplate.json in mainResourceGroup, use the following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="8e249-138">Dopo l'esecuzione del modello precedente, vengono richiesti i valori dei parametri definiti nel modello.</span><span class="sxs-lookup"><span data-stu-id="8e249-138">After the preceding template runs, it prompts you for the values of the parameters that are defined in the template.</span></span> <span data-ttu-id="8e249-139">Oltre ai parametri richiesti per il provisioning delle risorse in un modello, sono necessari due valori di parametri chiave:</span><span class="sxs-lookup"><span data-stu-id="8e249-139">In addition to the parameters that are needed to provision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="8e249-140">**managedResourceGroupId**: ID del gruppo di risorse contenente le risorse definite nel file applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8e249-140">**managedResourceGroupId**: The ID of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="8e249-141">L'ID è nel formato `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="8e249-141">The ID is of the form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="8e249-142">Nell'esempio precedente si tratta dell'ID di `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="8e249-142">In the preceding example, it's the ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="8e249-143">**applianceDefinitionId**: ID della risorsa di definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e249-143">**applianceDefinitionId**: The ID of the managed application definition resource.</span></span> <span data-ttu-id="8e249-144">Questo valore viene fornito dal fornitore di software indipendente.</span><span class="sxs-lookup"><span data-stu-id="8e249-144">This value is provided by the ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="8e249-145">Il server di pubblicazione deve concedere l'accesso al gruppo di risorse che contiene la definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e249-145">The publisher must grant access to the resource group that contains the managed application definition.</span></span> <span data-ttu-id="8e249-146">La risorsa di definizione viene creata nella sottoscrizione dell'editore.</span><span class="sxs-lookup"><span data-stu-id="8e249-146">The definition resource is created in the publisher subscription.</span></span> <span data-ttu-id="8e249-147">È quindi necessario che utenti, gruppi di utenti o applicazioni nel tenant del cliente abbiano accesso in lettura a questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="8e249-147">Therefore, a user, user group, or application in the customer tenant needs read access to this resource.</span></span>

<span data-ttu-id="8e249-148">Al termine della distribuzione, l'applicazione gestita viene creata in mainResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="8e249-148">After the deployment finishes successfully, you see the managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="8e249-149">La risorsa storageAccount viene creata in managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="8e249-149">The storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-the-create-command"></a><span data-ttu-id="8e249-150">Usare il comando di creazione</span><span class="sxs-lookup"><span data-stu-id="8e249-150">Use the create command</span></span>

<span data-ttu-id="8e249-151">È possibile usare il comando `az managedapp create` per creare un'applicazione gestita dalla definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e249-151">You can use the `az managedapp create` command to create a managed application from the managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="8e249-152">**appliance-definition-Id**: ID risorsa della definizione di applicazione gestita creata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="8e249-152">**appliance-definition-Id**: The resource ID of the managed application definition created in the preceding step.</span></span> <span data-ttu-id="8e249-153">Per ottenere questo ID, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="8e249-153">To obtain this ID, run the following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="8e249-154">Questo comando restituisce la definizione di applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e249-154">This command returns the managed application definition.</span></span> <span data-ttu-id="8e249-155">È necessario il valore della proprietà ID.</span><span class="sxs-lookup"><span data-stu-id="8e249-155">You need the value of the ID property.</span></span>

* <span data-ttu-id="8e249-156">**managed-rg-id**: nome del gruppo di risorse contenente le risorse definite nel file applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8e249-156">**managed-rg-id**: The name of the resource group containing the resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="8e249-157">Questo gruppo di risorse è il gruppo di risorse gestite</span><span class="sxs-lookup"><span data-stu-id="8e249-157">This resource group is the managed resource group.</span></span> <span data-ttu-id="8e249-158">e viene gestito dall'editore.</span><span class="sxs-lookup"><span data-stu-id="8e249-158">It's managed by the publisher.</span></span> <span data-ttu-id="8e249-159">Se non esiste, viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8e249-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="8e249-160">**resource-group**: gruppo di risorse in cui viene creata la risorsa applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e249-160">**resource-group**: The resource group where the managed application resource is created.</span></span> <span data-ttu-id="8e249-161">La risorsa Microsoft.Solutions/appliance si trova in questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8e249-161">The Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="8e249-162">**parameters**: parametri necessari per le risorse definite nel file applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="8e249-162">**parameters**: The parameters that are needed for the resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="8e249-163">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="8e249-163">Known issues</span></span>

<span data-ttu-id="8e249-164">Questa versione di anteprima contiene i problemi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8e249-164">This preview release includes the following issues:</span></span>

* <span data-ttu-id="8e249-165">Un messaggio 500 - Errore interno del server viene visualizzato durante la creazione dell'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="8e249-165">A 500 internal server error appears during the creation of the managed application.</span></span> <span data-ttu-id="8e249-166">In questo caso, è probabile che si tratti di un problema intermittente.</span><span class="sxs-lookup"><span data-stu-id="8e249-166">If you run into this issue, it's likely to be intermittent.</span></span> <span data-ttu-id="8e249-167">Ripetere l'operazione.</span><span class="sxs-lookup"><span data-stu-id="8e249-167">Retry the operation.</span></span>
* <span data-ttu-id="8e249-168">Per il gruppo di risorse gestite è necessario un nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="8e249-168">A new resource group is needed for the managed resource group.</span></span> <span data-ttu-id="8e249-169">Se si usa un gruppo di risorse esistente, la distribuzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="8e249-169">If you use an existing resource group, the deployment fails.</span></span>
* <span data-ttu-id="8e249-170">Il gruppo di risorse contenente la risorsa Microsoft.Solutions/appliances deve essere creato nella località **westcentralus**.</span><span class="sxs-lookup"><span data-stu-id="8e249-170">The resource group that contains the Microsoft.Solutions/appliances resource must be created in the **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8e249-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e249-171">Next steps</span></span>

* <span data-ttu-id="8e249-172">Per un'introduzione alle applicazioni gestite, vedere [Panoramica delle applicazioni gestite di Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8e249-172">For an introduction to managed applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8e249-173">Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="8e249-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="8e249-174">Per informazioni sulla pubblicazione di applicazioni gestite in Azure Marketplace, vedere [Applicazioni gestite di Azure nel Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="8e249-174">For information about publishing managed applications to the Azure Marketplace, see [Azure managed applications in the Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="8e249-175">Per informazioni sull'uso di un'applicazione gestita dal Marketplace, vedere [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md) (Uso delle applicazioni gestite di Azure nel Marketplace).</span><span class="sxs-lookup"><span data-stu-id="8e249-175">For information about consuming a managed application from the Marketplace, see [Consume Azure managed applications in the Marketplace](managed-application-consume-marketplace.md).</span></span>
