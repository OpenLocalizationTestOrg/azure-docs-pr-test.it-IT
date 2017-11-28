---
title: applicazione gestita di Azure aaaConsume | Documenti Microsoft
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
ms.openlocfilehash: b8510086eb05304c0e351a391b7e0cf34a467568
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="consume-an-internal-managed-application"></a><span data-ttu-id="c36dc-103">Usare un'applicazione gestita interna</span><span class="sxs-lookup"><span data-stu-id="c36dc-103">Consume an internal managed application</span></span>

<span data-ttu-id="c36dc-104">È possibile usare [applicazioni gestite](managed-application-overview.md) di Azure studiate per i membri della propria organizzazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-104">You can consume Azure [managed applications](managed-application-overview.md) that are intended for members of your organization.</span></span> <span data-ttu-id="c36dc-105">È, ad esempio, possibile selezionare applicazioni gestite disponibili dal reparto IT che garantiscano la conformità agli standard aziendali.</span><span class="sxs-lookup"><span data-stu-id="c36dc-105">For example, you can select managed applications from your IT department that ensure compliance with organizational standards.</span></span> <span data-ttu-id="c36dc-106">Queste applicazioni gestite sono disponibili tramite hello catalogo di servizi, non hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c36dc-106">These managed applications are available through hello Service Catalog, not hello Azure Marketplace.</span></span>

<span data-ttu-id="c36dc-107">Prima di procedere con questo articolo, è necessario disporre di un'applicazione gestita disponibile nel catalogo di servizi di hello per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-107">Before proceeding with this article, you must have a managed application available in hello service catalog for your subscription.</span></span> <span data-ttu-id="c36dc-108">Se qualcuno nell'organizzazione ha già creato un'applicazione gestita, vedere [Creare e pubblicare un'applicazione gestita di Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c36dc-108">If someone in your organization has not already created a managed application, see [Publish a managed application for internal consumption](managed-application-publishing.md).</span></span>

<span data-ttu-id="c36dc-109">Attualmente, è possibile utilizzare Azure CLI o hello tooconsume portale Azure un'applicazione gestita.</span><span class="sxs-lookup"><span data-stu-id="c36dc-109">Currently, you can use either Azure CLI or hello Azure portal tooconsume a managed application.</span></span>

## <a name="create-hello-managed-application-by-using-hello-portal"></a><span data-ttu-id="c36dc-110">Creare un'applicazione hello gestito tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="c36dc-110">Create hello managed application by using hello portal</span></span>

<span data-ttu-id="c36dc-111">toodeploy un'applicazione gestita tramite il portale di hello, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="c36dc-111">toodeploy a managed application through hello portal, follow these steps:</span></span>

1. <span data-ttu-id="c36dc-112">Passare toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="c36dc-112">Go toohello Azure portal.</span></span> <span data-ttu-id="c36dc-113">Cercare **Service Catalog Managed Application** (Applicazione gestita del catalogo di servizi).</span><span class="sxs-lookup"><span data-stu-id="c36dc-113">Search for **Service Catalog Managed Application**.</span></span>

   ![Applicazione gestita del catalogo di servizi](./media/managed-application-consumption/create-service-catalog-managed-application.png)

1. <span data-ttu-id="c36dc-115">Seleziona hello gestiti applicazione cui si desidera toocreate dall'elenco di hello delle soluzioni disponibili.</span><span class="sxs-lookup"><span data-stu-id="c36dc-115">Select hello managed application you want toocreate from hello list of available solutions.</span></span> <span data-ttu-id="c36dc-116">Selezionare **Crea**.</span><span class="sxs-lookup"><span data-stu-id="c36dc-116">Select **Create**.</span></span>

   ![Selezione di applicazioni gestite](./media/managed-application-consumption/select-offer.png)

1. <span data-ttu-id="c36dc-118">Fornire valori per parametri hello risorse hello tooprovision obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="c36dc-118">Provide values for hello parameters that are required tooprovision hello resources.</span></span> <span data-ttu-id="c36dc-119">Selezionare **West Central US** (Stati Uniti centro-occidentali) per il percorso.</span><span class="sxs-lookup"><span data-stu-id="c36dc-119">Select **West Central US** for location.</span></span> <span data-ttu-id="c36dc-120">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c36dc-120">Select **OK**.</span></span>

   ![Parametri delle applicazioni gestite](./media/managed-application-consumption/input-parameters.png)

1. <span data-ttu-id="c36dc-122">modello Hello convalida valori hello specificati.</span><span class="sxs-lookup"><span data-stu-id="c36dc-122">hello template validates hello values you provided.</span></span> <span data-ttu-id="c36dc-123">Se la convalida ha esito positivo, selezionare **OK** distribuzione hello toostart.</span><span class="sxs-lookup"><span data-stu-id="c36dc-123">If validation succeeds, select **OK** toostart hello deployment.</span></span>

   ![Convalida dell'applicazione gestita](./media/managed-application-consumption/validation.png)

<span data-ttu-id="c36dc-125">Al termine della distribuzione di hello, vengono effettuato il provisioning delle risorse appropriate hello definite nel modello hello nel gruppo di risorse gestite hello fornito.</span><span class="sxs-lookup"><span data-stu-id="c36dc-125">After hello deployment finishes, hello appropriate resources defined in hello template are provisioned in hello managed resource group you provided.</span></span>

## <a name="create-hello-managed-application-by-using-azure-cli"></a><span data-ttu-id="c36dc-126">Creare un'applicazione hello gestito tramite l'interfaccia CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="c36dc-126">Create hello managed application by using Azure CLI</span></span>

<span data-ttu-id="c36dc-127">Esistono due modi toocreate un'applicazione gestita tramite l'interfaccia CLI di Azure:</span><span class="sxs-lookup"><span data-stu-id="c36dc-127">There are two ways toocreate a managed application by using Azure CLI:</span></span>

* <span data-ttu-id="c36dc-128">Comando hello per la creazione di applicazioni gestite.</span><span class="sxs-lookup"><span data-stu-id="c36dc-128">Use hello command for creating managed applications.</span></span>
* <span data-ttu-id="c36dc-129">Comando distribuzione hello modello regolare.</span><span class="sxs-lookup"><span data-stu-id="c36dc-129">Use hello regular template deployment command.</span></span>

### <a name="use-hello-template-deployment-command"></a><span data-ttu-id="c36dc-130">Comando di distribuzione modello hello</span><span class="sxs-lookup"><span data-stu-id="c36dc-130">Use hello template deployment command</span></span>

<span data-ttu-id="c36dc-131">Distribuire file applianceMainTemplate.json hello hello fornitore creato.</span><span class="sxs-lookup"><span data-stu-id="c36dc-131">Deploy hello applianceMainTemplate.json file that hello vendor created.</span></span>

<span data-ttu-id="c36dc-132">Creare quindi due gruppi di risorse.</span><span class="sxs-lookup"><span data-stu-id="c36dc-132">Then create two resource groups.</span></span> <span data-ttu-id="c36dc-133">Hello primo gruppo di risorse è dove hello risorse applicazione gestita viene creata: Microsoft.Solutions/appliances.</span><span class="sxs-lookup"><span data-stu-id="c36dc-133">hello first resource group is where hello managed application resource is created: Microsoft.Solutions/appliances.</span></span> <span data-ttu-id="c36dc-134">il secondo gruppo di risorse Hello contiene tutte le risorse di hello definite in mainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="c36dc-134">hello second resource group contains all hello resources defined in mainTemplate.json.</span></span> <span data-ttu-id="c36dc-135">Questo gruppo di risorse è gestito da hello ISV.</span><span class="sxs-lookup"><span data-stu-id="c36dc-135">This resource group is managed by hello ISV.</span></span>

```azurecli
az group create --name mainResourceGroup --location westcentralus
az group create --name managedResourceGroup --location westcentralus
```

> [!NOTE]
> <span data-ttu-id="c36dc-136">Utilizzare `westcentralus` come percorso di hello hello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c36dc-136">Use `westcentralus` as hello location of hello resource group.</span></span>
>

<span data-ttu-id="c36dc-137">applianceMainTemplate.json toodeploy in mainResourceGroup, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c36dc-137">toodeploy applianceMainTemplate.json in mainResourceGroup, use hello following command:</span></span>

```azurecli
az group deployment create --name managedAppDeployment --resourceGroup mainResourceGroup --templateUri
```

<span data-ttu-id="c36dc-138">Dopo aver hello precedenti esecuzioni di modello, viene richiesto per i valori dei parametri definiti nel modello hello hello hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-138">After hello preceding template runs, it prompts you for hello values of hello parameters that are defined in hello template.</span></span> <span data-ttu-id="c36dc-139">Inoltre toohello parametri che sono necessarie risorse tooprovision in un modello, sono necessari due valori di parametro della chiave:</span><span class="sxs-lookup"><span data-stu-id="c36dc-139">In addition toohello parameters that are needed tooprovision resources in a template, you need two key parameter values:</span></span>

- <span data-ttu-id="c36dc-140">**managedResourceGroupId**: ID di hello gruppo contenitore hello di risorse definiti in applianceMainTemplate.json hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-140">**managedResourceGroupId**: hello ID of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="c36dc-141">ID Hello è formato hello `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span><span class="sxs-lookup"><span data-stu-id="c36dc-141">hello ID is of hello form `/subscriptions/{subscriptionId}/resourceGroups/{resoureGroupName}`.</span></span> <span data-ttu-id="c36dc-142">Nel precedente esempio di hello, dell'ID hello del `managedResourceGroup`.</span><span class="sxs-lookup"><span data-stu-id="c36dc-142">In hello preceding example, it's hello ID of `managedResourceGroup`.</span></span>
- <span data-ttu-id="c36dc-143">**applianceDefinitionId**: ID hello di hello gestiti risorsa di definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-143">**applianceDefinitionId**: hello ID of hello managed application definition resource.</span></span> <span data-ttu-id="c36dc-144">Questo valore viene fornito da hello ISV.</span><span class="sxs-lookup"><span data-stu-id="c36dc-144">This value is provided by hello ISV.</span></span>

> [!NOTE]
> <span data-ttu-id="c36dc-145">publisher Hello deve concedere accesso toohello risorse al gruppo che contiene la definizione di applicazione hello gestito.</span><span class="sxs-lookup"><span data-stu-id="c36dc-145">hello publisher must grant access toohello resource group that contains hello managed application definition.</span></span> <span data-ttu-id="c36dc-146">risorse di definizione Hello viene creata nella sottoscrizione di hello server di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-146">hello definition resource is created in hello publisher subscription.</span></span> <span data-ttu-id="c36dc-147">Pertanto, un utente, gruppo di utenti o l'applicazione nel tenant del cliente hello deve risorsa toothis accesso in lettura.</span><span class="sxs-lookup"><span data-stu-id="c36dc-147">Therefore, a user, user group, or application in hello customer tenant needs read access toothis resource.</span></span>

<span data-ttu-id="c36dc-148">Dopo la distribuzione di hello viene completata correttamente, viene visualizzato hello gestito in mainResourceGroup viene creata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-148">After hello deployment finishes successfully, you see hello managed application is created in mainResourceGroup.</span></span> <span data-ttu-id="c36dc-149">risorsa storageAccount Hello viene creato in managedResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="c36dc-149">hello storageAccount resource is created in managedResourceGroup.</span></span>

### <a name="use-hello-create-command"></a><span data-ttu-id="c36dc-150">Hello utilizzare creare un comando</span><span class="sxs-lookup"><span data-stu-id="c36dc-150">Use hello create command</span></span>

<span data-ttu-id="c36dc-151">È possibile utilizzare hello `az managedapp create` comando toocreate un'applicazione gestita da hello gestiti definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-151">You can use hello `az managedapp create` command toocreate a managed application from hello managed application definition.</span></span>

```azurecli
az managedapp create --name ravtestappliance401 --location "westcentralus"
    --kind "Servicecatalog" --resource-group "ravApplianceCustRG401"
    --managedapp-definition-id "/subscriptions/{guid}/resourceGroups/ravApplianceDefRG401/providers/Microsoft.Solutions/applianceDefinitions/ravtestAppDef401"
    --managed-rg-id "/subscriptions/{guid}/resourceGroups/ravApplianceCustManagedRG401"
    --parameters "{\"storageAccountName\": {\"value\": \"ravappliancedemostore1\"}}"
    --debug
```

* <span data-ttu-id="c36dc-152">**Id di definizione dello strumento**: ID di risorsa hello di hello gestiti creato nel passaggio precedente hello definizione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-152">**appliance-definition-Id**: hello resource ID of hello managed application definition created in hello preceding step.</span></span> <span data-ttu-id="c36dc-153">tooobtain questo ID, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c36dc-153">tooobtain this ID, run hello following command:</span></span>

  ```azurecli
  az appliance definition show -n ravtestAppDef1 -g ravApplianceRG2
  ```

  <span data-ttu-id="c36dc-154">Questo comando restituisce la definizione di applicazione hello gestito.</span><span class="sxs-lookup"><span data-stu-id="c36dc-154">This command returns hello managed application definition.</span></span> <span data-ttu-id="c36dc-155">È necessario il valore di hello della proprietà ID hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-155">You need hello value of hello ID property.</span></span>

* <span data-ttu-id="c36dc-156">**rg-id gestito**: nome hello di hello gruppo contenitore hello di risorse definiti in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="c36dc-156">**managed-rg-id**: hello name of hello resource group containing hello resources defined in applianceMainTemplate.json.</span></span> <span data-ttu-id="c36dc-157">Questo gruppo di risorse è il gruppo di risorse gestite hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-157">This resource group is hello managed resource group.</span></span> <span data-ttu-id="c36dc-158">È gestito dal server di pubblicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-158">It's managed by hello publisher.</span></span> <span data-ttu-id="c36dc-159">Se non esiste, viene creato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c36dc-159">If it doesn't exist, it's created for you.</span></span>
* <span data-ttu-id="c36dc-160">**gruppo di risorse**: viene creato il gruppo di risorse hello in hello gestiti risorsa dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c36dc-160">**resource-group**: hello resource group where hello managed application resource is created.</span></span> <span data-ttu-id="c36dc-161">Hello Microsoft.Solutions/appliance risorsa si trova in questo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="c36dc-161">hello Microsoft.Solutions/appliance resource lives in this resource group.</span></span>
* <span data-ttu-id="c36dc-162">**i parametri**: hello parametri che sono necessari per le risorse di hello definite in applianceMainTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="c36dc-162">**parameters**: hello parameters that are needed for hello resources defined in applianceMainTemplate.json.</span></span>

## <a name="known-issues"></a><span data-ttu-id="c36dc-163">Problemi noti</span><span class="sxs-lookup"><span data-stu-id="c36dc-163">Known issues</span></span>

<span data-ttu-id="c36dc-164">Questa versione di anteprima include hello seguenti problemi:</span><span class="sxs-lookup"><span data-stu-id="c36dc-164">This preview release includes hello following issues:</span></span>

* <span data-ttu-id="c36dc-165">Durante la creazione di un'applicazione hello gestito hello viene visualizzato un errore di 500 interno del server.</span><span class="sxs-lookup"><span data-stu-id="c36dc-165">A 500 internal server error appears during hello creation of hello managed application.</span></span> <span data-ttu-id="c36dc-166">Se si esegue questo problema, è probabile che toobe intermittenti.</span><span class="sxs-lookup"><span data-stu-id="c36dc-166">If you run into this issue, it's likely toobe intermittent.</span></span> <span data-ttu-id="c36dc-167">Ripetere l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-167">Retry hello operation.</span></span>
* <span data-ttu-id="c36dc-168">Un nuovo gruppo di risorse è necessaria per il gruppo di risorse gestite hello.</span><span class="sxs-lookup"><span data-stu-id="c36dc-168">A new resource group is needed for hello managed resource group.</span></span> <span data-ttu-id="c36dc-169">Se si utilizza un gruppo di risorse esistente, la distribuzione di hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="c36dc-169">If you use an existing resource group, hello deployment fails.</span></span>
* <span data-ttu-id="c36dc-170">Hello gruppo di risorse contenente hello Microsoft.Solutions/appliances risorsa deve essere creato in hello **westcentralus** percorso.</span><span class="sxs-lookup"><span data-stu-id="c36dc-170">hello resource group that contains hello Microsoft.Solutions/appliances resource must be created in hello **westcentralus** location.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c36dc-171">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c36dc-171">Next steps</span></span>

* <span data-ttu-id="c36dc-172">Per le applicazioni toomanaged un'introduzione, vedere [panoramica delle applicazioni gestite](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c36dc-172">For an introduction toomanaged applications, see [Managed application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c36dc-173">Per informazioni sulla pubblicazione di un'applicazione gestita del catalogo di servizi, vedere [Creare e pubblicare un'applicazione gestita del catalogo di servizi](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="c36dc-173">For information about publishing a Service Catalog managed application, see [Create and publish a Service Catalog managed application](managed-application-publishing.md).</span></span>
* <span data-ttu-id="c36dc-174">Per informazioni sulla pubblicazione applicazioni gestite toohello Azure Marketplace, vedere [gestito di Azure le applicazioni in hello Marketplace](managed-application-author-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="c36dc-174">For information about publishing managed applications toohello Azure Marketplace, see [Azure managed applications in hello Marketplace](managed-application-author-marketplace.md).</span></span>
* <span data-ttu-id="c36dc-175">Per informazioni sull'utilizzo di un'applicazione gestita da hello Marketplace, vedere [utilizzare Azure gestite le applicazioni in hello Marketplace](managed-application-consume-marketplace.md).</span><span class="sxs-lookup"><span data-stu-id="c36dc-175">For information about consuming a managed application from hello Marketplace, see [Consume Azure managed applications in hello Marketplace](managed-application-consume-marketplace.md).</span></span>
