---
title: Risolvere errori comuni durante la distribuzione di risorse in Azure | Microsoft Docs
description: Descrive come risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: errore di distribuzione, distribuzione di azure, distribuire in azure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 30adc10d01290f14a3e116813b19916fa36ab0bc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="fd074-104">Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="fd074-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="fd074-105">Questo argomento illustra come risolvere alcuni errori comuni che possono verificarsi durante la distribuzione di risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="fd074-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="fd074-106">In questo argomento sono descritti i codici di errore seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd074-106">The following error codes are described in this topic:</span></span>

* [<span data-ttu-id="fd074-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="fd074-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="fd074-108">Authorization failed</span><span class="sxs-lookup"><span data-stu-id="fd074-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="fd074-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="fd074-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="fd074-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="fd074-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="fd074-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="fd074-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="fd074-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="fd074-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="fd074-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="fd074-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="fd074-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="fd074-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="fd074-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="fd074-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="fd074-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="fd074-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="fd074-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="fd074-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="fd074-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="fd074-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="fd074-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="fd074-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="fd074-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="fd074-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="fd074-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="fd074-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="fd074-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="fd074-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="fd074-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="fd074-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="fd074-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="fd074-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="fd074-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="fd074-125">DeploymentFailed</span></span>

<span data-ttu-id="fd074-126">Questo codice di errore indica un errore di distribuzione generale, ma non consente di avviare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="fd074-126">This error code indicates a general deployment error, but it is not the error code you need to start troubleshooting.</span></span> <span data-ttu-id="fd074-127">Il codice di errore effettivamente utile per risolvere il problema si trova in genere un livello sotto tale errore.</span><span class="sxs-lookup"><span data-stu-id="fd074-127">The error code that actually helps you resolve the issue is usually one level below this error.</span></span> <span data-ttu-id="fd074-128">L'immagine seguente illustra ad esempio il codice di errore **RequestDisallowedByPolicy** sotto l'errore di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-128">For example, the following image shows the **RequestDisallowedByPolicy** error code that is under the deployment error.</span></span>

![mostra codice di errore](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="fd074-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="fd074-130">SkuNotAvailable</span></span>

<span data-ttu-id="fd074-131">Quando si distribuisce una risorsa, in genere una macchina virtuale, è possibile che venga visualizzato il codice di errore e il messaggio di errore seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd074-131">When deploying a resource (typically a virtual machine), you may receive the following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: The requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy to a different location.
```

<span data-ttu-id="fd074-132">Questo errore viene visualizzato quando lo SKU della risorsa selezionato, ad esempio le dimensioni della macchina virtuale, non è disponibile per il percorso selezionato.</span><span class="sxs-lookup"><span data-stu-id="fd074-132">You receive this error when the resource SKU you have selected (such as VM size) is not available for the location you have selected.</span></span> <span data-ttu-id="fd074-133">Per risolvere questo problema, è necessario determinare gli SKU disponibili in un'area.</span><span class="sxs-lookup"><span data-stu-id="fd074-133">To resolve this issue, you need to determine which SKUs are available in a region.</span></span> <span data-ttu-id="fd074-134">Per trovare gli SKU disponibili è possibile usare PowerShell o un'operazione REST.</span><span class="sxs-lookup"><span data-stu-id="fd074-134">You can use PowerShell, the portal, or a REST operation to find available SKUs.</span></span>

- <span data-ttu-id="fd074-135">Per PowerShell usare [Get AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) e filtrare in base al percorso.</span><span class="sxs-lookup"><span data-stu-id="fd074-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="fd074-136">Per questo comando, è necessaria la versione più recente di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd074-136">You must have the latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="fd074-137">I risultati includono un elenco di SKU per la località e le eventuali limitazioni per tale SKU.</span><span class="sxs-lookup"><span data-stu-id="fd074-137">The results include a list of SKUs for the location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="fd074-138">Per usare il portale, accedere al [portale](https://portal.azure.com) e aggiungere una risorsa tramite l'interfaccia.</span><span class="sxs-lookup"><span data-stu-id="fd074-138">To use the [portal](https://portal.azure.com), log in to the portal and add a resource through the interface.</span></span> <span data-ttu-id="fd074-139">Quando si impostano i valori, vengono visualizzati gli SKU disponibili per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="fd074-139">As you set the values, you see the available SKUs for that resource.</span></span> <span data-ttu-id="fd074-140">Non è necessario completare la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-140">You do not need to complete the deployment.</span></span>

    ![SKU disponibili](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="fd074-142">Per usare l'API REST per le macchine virtuali, inviare la richiesta seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-142">To use the REST API for virtual machines, send the following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="fd074-143">Le aree e gli SKU disponibili vengono restituiti nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-143">It returns available SKUs and regions in the following format:</span></span>

  ```json
  {
    "value": [
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A0",
        "tier": "Standard",
        "size": "A0",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      {
        "resourceType": "virtualMachines",
        "name": "Standard_A1",
        "tier": "Standard",
        "size": "A1",
        "locations": [
          "eastus"
        ],
        "restrictions": []
      },
      ...
    ]
  }    
  ```

<span data-ttu-id="fd074-144">Se non si riesce a trovare uno SKU appropriato in tale area o un'area alternativa che soddisfi le esigenze aziendali, inviare una [richiesta di SKU](https://aka.ms/skurestriction) al supporto di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd074-144">If you are unable to find a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) to Azure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="fd074-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="fd074-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: The current subscription type is not permitted to perform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="fd074-146">Se viene visualizzato questo errore, si sta usando una sottoscrizione a cui non è consentito accedere a nessun altro servizio di Azure tranne Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd074-146">If you receive this error, you are using a subscription that is not permitted to access any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="fd074-147">Questo tipo di sottoscrizione può essere in uso quando è necessario accedere al portale classico, ma non è consentito distribuire le risorse.</span><span class="sxs-lookup"><span data-stu-id="fd074-147">You might have this type of subscription when you need to access the classic portal but are not permitted to deploy resources.</span></span> <span data-ttu-id="fd074-148">Per risolvere questo problema, è necessario usare una sottoscrizione con l'autorizzazione a distribuire le risorse.</span><span class="sxs-lookup"><span data-stu-id="fd074-148">To resolve this issue, you must use a subscription that has permission to deploy resources.</span></span>  

<span data-ttu-id="fd074-149">Per visualizzare le sottoscrizioni disponibili con PowerShell, usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-149">To view your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="fd074-150">Per impostare la sottoscrizione corrente, usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-150">And, to set the current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="fd074-151">Per visualizzare le sottoscrizioni disponibili con l'interfaccia della riga di comando di Azure 2.0, usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-151">To view your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="fd074-152">Per impostare la sottoscrizione corrente, usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-152">And, to set the current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="fd074-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="fd074-153">InvalidTemplate</span></span>
<span data-ttu-id="fd074-154">Questo errore può essere causato da diversi tipi di errori.</span><span class="sxs-lookup"><span data-stu-id="fd074-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="fd074-155">Errore di sintassi</span><span class="sxs-lookup"><span data-stu-id="fd074-155">Syntax error</span></span>

   <span data-ttu-id="fd074-156">Se viene visualizzato un messaggio di errore che indica che la convalida del modello non è riuscita, potrebbe trattarsi di un problema di sintassi nel modello.</span><span class="sxs-lookup"><span data-stu-id="fd074-156">If you receive an error message that indicates the template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="fd074-157">Non è insolito commettere questo errore, perché le espressioni del modello possono essere complesse.</span><span class="sxs-lookup"><span data-stu-id="fd074-157">This error is easy to make because template expressions can be intricate.</span></span> <span data-ttu-id="fd074-158">Ad esempio, l'assegnazione di nome seguente per un account di archiviazione contiene un set di parentesi, tre funzioni, tre set di parentesi, un set di virgolette singole e una proprietà:</span><span class="sxs-lookup"><span data-stu-id="fd074-158">For example, the following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="fd074-159">Se non si specifica la sintassi corrispondente, il modello produce un valore diverso dal previsto.</span><span class="sxs-lookup"><span data-stu-id="fd074-159">If you do not provide the matching syntax, the template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="fd074-160">Quando viene visualizzato questo tipo di errore, esaminare attentamente la sintassi dell'espressione.</span><span class="sxs-lookup"><span data-stu-id="fd074-160">When you receive this type of error, carefully review the expression syntax.</span></span> <span data-ttu-id="fd074-161">È consigliabile usare un editor JSON come [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) o [Visual Studio Code](resource-manager-vs-code.md) che può segnalare gli errori di sintassi.</span><span class="sxs-lookup"><span data-stu-id="fd074-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="fd074-162">Lunghezze di segmenti non valide</span><span class="sxs-lookup"><span data-stu-id="fd074-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="fd074-163">Un altro errore di modello non valido si verifica quando il nome della risorsa non è nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="fd074-163">Another invalid template error occurs when the resource name is not in the correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'The template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="fd074-164">Il nome di una risorsa a livello di radice deve contenere un segmento in meno rispetto al tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="fd074-164">A root level resource must have one less segment in the name than in the resource type.</span></span> <span data-ttu-id="fd074-165">Ogni segmento si differenzia mediante una barra.</span><span class="sxs-lookup"><span data-stu-id="fd074-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="fd074-166">Nell'esempio seguente, il tipo ha due segmenti e il nome un segmento, quindi è un **nome valido**.</span><span class="sxs-lookup"><span data-stu-id="fd074-166">In the following example, the type has two segments and the name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="fd074-167">L'esempio successivo invece **non è un nome valido** , perché ha lo stesso numero di segmenti del tipo.</span><span class="sxs-lookup"><span data-stu-id="fd074-167">But the next example is **not a valid name** because it has the same number of segments as the type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="fd074-168">Per le risorse figlio, il tipo e il nome devono avere lo stesso numero di segmenti.</span><span class="sxs-lookup"><span data-stu-id="fd074-168">For child resources, the type and name have the same number of segments.</span></span> <span data-ttu-id="fd074-169">Questo è dovuto al fatto che il nome completo e il tipo dell'elemento figlio includono il nome e il tipo dell'elemento padre.</span><span class="sxs-lookup"><span data-stu-id="fd074-169">This number of segments makes sense because the full name and type for the child includes the parent name and type.</span></span> <span data-ttu-id="fd074-170">Di conseguenza, il nome completo ha comunque un segmento in meno rispetto al tipo completo.</span><span class="sxs-lookup"><span data-stu-id="fd074-170">Therefore, the full name still has one less segment than the full type.</span></span>

  ```json
  "resources": [
      {
          "type": "Microsoft.KeyVault/vaults",
          "name": "contosokeyvault",
          ...
          "resources": [
              {
                  "type": "secrets",
                  "name": "appPassword",
                  ...
              }
          ]
      }
  ]
  ```

   <span data-ttu-id="fd074-171">Ottenere il numero di segmenti corretto può essere difficile con i tipi di Resource Manager applicati ai provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="fd074-171">Getting the segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="fd074-172">Per applicare un blocco di risorsa a un sito Web, ad esempio, è necessario un tipo con quattro segmenti.</span><span class="sxs-lookup"><span data-stu-id="fd074-172">For example, applying a resource lock to a web site requires a type with four segments.</span></span> <span data-ttu-id="fd074-173">Il nome è quindi costituito da tre segmenti:</span><span class="sxs-lookup"><span data-stu-id="fd074-173">Therefore, the name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="fd074-174">Indice di copia non previsto</span><span class="sxs-lookup"><span data-stu-id="fd074-174">Copy index is not expected</span></span>

   <span data-ttu-id="fd074-175">Questo errore **InvalidTemplate** viene visualizzato quando è stato applicato l'elemento **copy** a una parte del modello che non supporta questo elemento.</span><span class="sxs-lookup"><span data-stu-id="fd074-175">You encounter this **InvalidTemplate** error when you have applied the **copy** element to a part of the template that does not support this element.</span></span> <span data-ttu-id="fd074-176">È possibile applicare l'elemento copy solo a un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="fd074-176">You can only apply the copy element to a resource type.</span></span> <span data-ttu-id="fd074-177">Copia non è possibile applicare copy a una proprietà all'interno di un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="fd074-177">You cannot apply copy to a property within a resource type.</span></span> <span data-ttu-id="fd074-178">Ad esempio, si applica copy a una macchina virtuale, ma non è possibile applicarlo ai dischi del sistema operativo per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fd074-178">For example, you apply copy to a virtual machine, but you cannot apply it to the OS disks for a virtual machine.</span></span> <span data-ttu-id="fd074-179">In alcuni casi, è possibile convertire una risorsa figlio in una risorsa padre per creare un ciclo di copy.</span><span class="sxs-lookup"><span data-stu-id="fd074-179">In some cases, you can convert a child resource to a parent resource to create a copy loop.</span></span> <span data-ttu-id="fd074-180">Per altre informazioni sull'uso di copy, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="fd074-181">Parametro non valido</span><span class="sxs-lookup"><span data-stu-id="fd074-181">Parameter is not valid</span></span>

   <span data-ttu-id="fd074-182">Se il modello specifica i valori consentiti per un parametro e si fornisce un valore diverso da tali valori, verrà visualizzato un messaggio simile all'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-182">If the template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar to the following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'The provided value {parameter value}
  for the template parameter {parameter name} is not valid. The parameter value is not
  part of the allowed values
  ``` 

   <span data-ttu-id="fd074-183">Ricontrollare i valori consentiti nel modello e specificarne uno durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-183">Double check the allowed values in the template, and provide one during deployment.</span></span>

- <span data-ttu-id="fd074-184">È stata rilevata una dipendenza circolare</span><span class="sxs-lookup"><span data-stu-id="fd074-184">Circular dependency detected</span></span>

   <span data-ttu-id="fd074-185">Questo errore viene visualizzato quando le dipendenze tra le risorse impediscono l'avvio della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-185">You receive this error when resources depend on each other in a way that prevents the deployment from starting.</span></span> <span data-ttu-id="fd074-186">A causa di una combinazione di interdipendenze, due o più risorse attendono altre risorse che sono a propria volta in attesa.</span><span class="sxs-lookup"><span data-stu-id="fd074-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="fd074-187">Ad esempio, la risorsa 1 dipende dalla risorsa 3, la risorsa 2 dipende dalla risorsa 1 e la risorsa 3 dipende dalla risorsa 2.</span><span class="sxs-lookup"><span data-stu-id="fd074-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="fd074-188">È in genere possibile risolvere questo problema rimuovendo le dipendenze non necessarie.</span><span class="sxs-lookup"><span data-stu-id="fd074-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="fd074-189">NotFound and ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="fd074-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="fd074-190">Quando il modello include il nome di una risorsa che non può essere risolta, verrà visualizzato un errore simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-190">When your template includes the name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="fd074-191">Se si sta provando a distribuire la risorsa mancante nel modello, verificare se sia necessario aggiungere una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="fd074-191">If you are attempting to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="fd074-192">Azure Resource Manager consente di ottimizzare la distribuzione creando risorse in parallelo, quando ciò è possibile.</span><span class="sxs-lookup"><span data-stu-id="fd074-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="fd074-193">Se una risorsa deve essere distribuita dopo un'altra, è necessario usare l'elemento **dependsOn** nel modello per creare una dipendenza dall'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="fd074-193">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template to create a dependency on the other resource.</span></span> <span data-ttu-id="fd074-194">Ad esempio, quando si distribuisce un'app Web deve esistere il piano di servizio app.</span><span class="sxs-lookup"><span data-stu-id="fd074-194">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="fd074-195">Se non è stato specificato che l'app Web dipende dal piano di servizio app, Azure Resource Manager crea entrambe le risorse contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="fd074-195">If you have not specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="fd074-196">Verrà visualizzato un messaggio di errore che informa che la risorsa del piano di servizio app non è stata trovata, perché non esiste ancora al momento del tentativo di impostare una proprietà nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="fd074-196">You receive an error stating that the App Service plan resource cannot be found, because it does not exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="fd074-197">È possibile prevenire questo errore impostando la dipendenza nell'app Web.</span><span class="sxs-lookup"><span data-stu-id="fd074-197">You prevent this error by setting the dependency in the web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="fd074-198">Per suggerimenti sulla risoluzione degli errori relativi alle dipendenze, vedere [Controllare la sequenza di distribuzione](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="fd074-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="fd074-199">Questo errore viene visualizzato anche quando la risorsa si trova in un gruppo di risorse diverso rispetto a quello in cui viene distribuita.</span><span class="sxs-lookup"><span data-stu-id="fd074-199">You also see this error when the resource exists in a different resource group than the one being deployed to.</span></span> <span data-ttu-id="fd074-200">In tal caso, usare la [funzione resourceId](resource-group-template-functions-resource.md#resourceid) per ottenere il nome completo della risorsa.</span><span class="sxs-lookup"><span data-stu-id="fd074-200">In that case, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="fd074-201">Se si prova a usare la funzione [reference](resource-group-template-functions-resource.md#reference) o la funzione [listKeys](resource-group-template-functions-resource.md#listkeys) con una risorsa che non può essere risolta, verrà visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-201">If you attempt to use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="fd074-202">Cercare un'espressione contenente la funzione **reference**.</span><span class="sxs-lookup"><span data-stu-id="fd074-202">Look for an expression that includes the **reference** function.</span></span> <span data-ttu-id="fd074-203">Verificare che i valori dei parametri siano corretti.</span><span class="sxs-lookup"><span data-stu-id="fd074-203">Double check that the parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="fd074-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="fd074-204">ParentResourceNotFound</span></span>

<span data-ttu-id="fd074-205">Quando una risorsa è l'elemento padre di un'altra risorsa, deve già esistere prima di creare la risorsa figlio.</span><span class="sxs-lookup"><span data-stu-id="fd074-205">When one resource is a parent to another resource, the parent resource must exist before creating the child resource.</span></span> <span data-ttu-id="fd074-206">Se non esiste ancora, viene visualizzato l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-206">If it does not yet exist, you receive the following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="fd074-207">Il nome della risorsa figlio include il nome della risorsa padre.</span><span class="sxs-lookup"><span data-stu-id="fd074-207">The name of the child resource includes the parent name.</span></span> <span data-ttu-id="fd074-208">Ad esempio, un database SQL può essere definito come segue:</span><span class="sxs-lookup"><span data-stu-id="fd074-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="fd074-209">Tuttavia, se non si specifica una dipendenza dalla risorsa padre, la risorsa figlio può essere distribuita prima dell'elemento padre.</span><span class="sxs-lookup"><span data-stu-id="fd074-209">But, if you do not specify a dependency on the parent resource, the child resource may get deployed before the parent.</span></span> <span data-ttu-id="fd074-210">Per risolvere questo errore, includere una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="fd074-210">To resolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="fd074-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="fd074-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="fd074-212">Per gli account di archiviazione, il nome della risorsa specificato deve essere univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="fd074-212">For storage accounts, you must provide a name for the resource that is unique across Azure.</span></span> <span data-ttu-id="fd074-213">Se non si specifica un nome univoco, verrà visualizzato un errore come il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=The storage account named mystorage is already taken.
```

<span data-ttu-id="fd074-214">È possibile creare un nome univoco concatenando la convenzione di denominazione con il risultato della funzione [uniqueString](resource-group-template-functions-string.md#uniquestring) .</span><span class="sxs-lookup"><span data-stu-id="fd074-214">You can create a unique name by concatenating your naming convention with the result of the [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="fd074-215">Se si distribuisce un account di archiviazione con lo steso nome di un account di archiviazione esistente nella sottoscrizione specificando però una diversa località, verrà visualizzato un errore che indica che l'account di archiviazione esiste già in un'altra località.</span><span class="sxs-lookup"><span data-stu-id="fd074-215">If you deploy a storage account with the same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating the storage account already exists in a different location.</span></span> <span data-ttu-id="fd074-216">Eliminare l'account di archiviazione esistente oppure specificare la stessa località di tale account.</span><span class="sxs-lookup"><span data-stu-id="fd074-216">Either delete the existing storage account, or provide the same location as the existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="fd074-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="fd074-217">AccountNameInvalid</span></span>
<span data-ttu-id="fd074-218">L'errore **AccountNameInvalid** viene visualizzato quando si prova ad assegnare a un account di archiviazione un nome contenente caratteri non consentiti.</span><span class="sxs-lookup"><span data-stu-id="fd074-218">You see the **AccountNameInvalid** error when attempting to give a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="fd074-219">I nomi degli account di archiviazione devono essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="fd074-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="fd074-220">La funzione [uniqueString](resource-group-template-functions-string.md#uniquestring) restituisce 13 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd074-220">The [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="fd074-221">Se si concatena un prefisso al risultato di **uniqueString**, specificare un prefisso composto al massimo da 11 caratteri.</span><span class="sxs-lookup"><span data-stu-id="fd074-221">If you concatenate a prefix to the **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="fd074-222">RichiestaNonValida</span><span class="sxs-lookup"><span data-stu-id="fd074-222">BadRequest</span></span>

<span data-ttu-id="fd074-223">Quando per una proprietà si specifica un valore non valido, può comparire lo stato BadRequest.</span><span class="sxs-lookup"><span data-stu-id="fd074-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="fd074-224">Ad esempio, se per un account di archiviazione si fornisce un valore SKU non corretto, la distribuzione ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="fd074-224">For example, if you provide an incorrect SKU value for a storage account, the deployment fails.</span></span> <span data-ttu-id="fd074-225">Per determinare i valori validi per la proprietà, vedere l'articolo relativo all'[API REST](/rest/api) in relazione al tipo di risorsa distribuito.</span><span class="sxs-lookup"><span data-stu-id="fd074-225">To determine valid values for property, look at the [REST API](/rest/api) for the resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="fd074-226">NoRegisteredProviderFound e MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="fd074-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="fd074-227">Quando si distribuisce una risorsa, è possibile che venga visualizzato il codice di errore e il messaggio seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd074-227">When deploying resource, you may receive the following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="fd074-228">In alternativa, si potrebbe ricevere un messaggio analogo che indica:</span><span class="sxs-lookup"><span data-stu-id="fd074-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: The subscription is not registered to use namespace {resource-provider-namespace}
```

<span data-ttu-id="fd074-229">Questi errori vengono visualizzati per uno di questi tre motivi:</span><span class="sxs-lookup"><span data-stu-id="fd074-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="fd074-230">Il provider di risorse non è stato registrato per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="fd074-230">The resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="fd074-231">La versione dell'API non è supportata per il tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="fd074-231">API version not supported for the resource type</span></span>
3. <span data-ttu-id="fd074-232">Il percorso non è supportato per il tipo di risorsa</span><span class="sxs-lookup"><span data-stu-id="fd074-232">Location not supported for the resource type</span></span>

<span data-ttu-id="fd074-233">Il messaggio di errore dovrebbe fornire suggerimenti per le versioni di API e i percorsi supportati.</span><span class="sxs-lookup"><span data-stu-id="fd074-233">The error message should give you suggestions for the supported locations and API versions.</span></span> <span data-ttu-id="fd074-234">È possibile modificare il modello impostando uno dei valori suggeriti.</span><span class="sxs-lookup"><span data-stu-id="fd074-234">You can change your template to one of the suggested values.</span></span> <span data-ttu-id="fd074-235">La maggior parte dei provider, ma non tutti, vengono registrati automaticamente dal portale di Azure o dall'interfaccia della riga di comando che si sta usando.</span><span class="sxs-lookup"><span data-stu-id="fd074-235">Most providers are registered automatically by the Azure portal or the command-line interface you are using, but not all.</span></span> <span data-ttu-id="fd074-236">Se non è mai stato usato un provider di risorse specifico, potrebbe essere necessario registrarlo.</span><span class="sxs-lookup"><span data-stu-id="fd074-236">If you have not used a particular resource provider before, you may need to register that provider.</span></span> <span data-ttu-id="fd074-237">È possibile ottenere altre informazioni sui provider di risorse tramite PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd074-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="fd074-238">**Portale**</span><span class="sxs-lookup"><span data-stu-id="fd074-238">**Portal**</span></span>

<span data-ttu-id="fd074-239">È possibile visualizzare lo stato di registrazione e registrare uno spazio dei nomi del provider di risorse tramite il portale.</span><span class="sxs-lookup"><span data-stu-id="fd074-239">You can see the registration status and register a resource provider namespace through the portal.</span></span>

1. <span data-ttu-id="fd074-240">Selezionare **Provider di risorse** per la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fd074-240">For your subscription, select **Resource providers**.</span></span>

   ![selezionare i provider di risorse](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="fd074-242">Esaminare l'elenco dei provider di risorse e, se necessario, selezionare il link **Registra** per registrare il provider di risorse del tipo che si intende distribuire.</span><span class="sxs-lookup"><span data-stu-id="fd074-242">Look at the list of resource providers, and if necessary, select the **Register** link to register the resource provider of the type you are trying to deploy.</span></span>

   ![Elenco di provider di risorse](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="fd074-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="fd074-244">**PowerShell**</span></span>

<span data-ttu-id="fd074-245">Per visualizzare lo stato della registrazione, usare **Get-AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="fd074-245">To see your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="fd074-246">Per registrare un provider, usare **Register-AzureRmResourceProvider** e specificare il nome del provider di risorse da registrare.</span><span class="sxs-lookup"><span data-stu-id="fd074-246">To register a provider, use **Register-AzureRmResourceProvider** and provide the name of the resource provider you wish to register.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="fd074-247">Per ottenere i percorsi supportati per un tipo di risorsa particolare è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-247">To get the supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="fd074-248">Per ottenere le versioni di API supportate per un tipo di risorsa particolare è possibile usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-248">To get the supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="fd074-249">**Interfaccia della riga di comando di Azure**</span><span class="sxs-lookup"><span data-stu-id="fd074-249">**Azure CLI**</span></span>

<span data-ttu-id="fd074-250">Per vedere se il provider è registrato, usare il comando `azure provider list` .</span><span class="sxs-lookup"><span data-stu-id="fd074-250">To see whether the provider is registered, use the `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="fd074-251">Per registrare un provider di risorse, usare il comando `azure provider register` e specificare lo *spazio dei nomi* per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="fd074-251">To register a resource provider, use the `azure provider register` command, and specify the *namespace* to register.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="fd074-252">Per visualizzare le versioni di API e i percorsi supportati per un tipo di risorsa, usare:</span><span class="sxs-lookup"><span data-stu-id="fd074-252">To see the supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="fd074-253">QuotaExceeded e OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="fd074-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="fd074-254">Alcuni problemi potrebbero verificarsi quando una distribuzione supera una quota specifica per un gruppo di risorse, le sottoscrizioni, gli account o per altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="fd074-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="fd074-255">Ad esempio, la sottoscrizione potrebbe essere configurata in modo da limitare il numero di core per un'area.</span><span class="sxs-lookup"><span data-stu-id="fd074-255">For example, your subscription may be configured to limit the number of cores for a region.</span></span> <span data-ttu-id="fd074-256">Se si prova a distribuire una macchina virtuale con un numero di core superiore alla quantità consentita, verrà visualizzato un messaggio di errore che informa che la quota è stata superata.</span><span class="sxs-lookup"><span data-stu-id="fd074-256">If you attempt to deploy a virtual machine with more cores than the permitted amount, you receive an error stating the quota has been exceeded.</span></span>
<span data-ttu-id="fd074-257">Per informazioni complete sulle quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="fd074-258">Per esaminare le quote per i core della sottoscrizione, è possibile usare il comando `azure vm list-usage` nell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="fd074-258">To examine your subscription's quotas for cores, you can use the `azure vm list-usage` command in the Azure CLI.</span></span> <span data-ttu-id="fd074-259">L'esempio seguente mostra che la quota di core per un account della versione di valutazione gratuita è quattro:</span><span class="sxs-lookup"><span data-stu-id="fd074-259">The following example illustrates that the core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="fd074-260">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="fd074-260">Which returns:</span></span>

```azurecli
[
  {
    "currentValue": 0,
    "limit": 2000,
    "name": {
      "localizedValue": "Availability Sets",
      "value": "availabilitySets"
    }
  },
  ...
]
```

<span data-ttu-id="fd074-261">Se si distribuisce un modello che crea più di quattro core nell'area Stati Uniti occidentali, verrà visualizzato un errore di distribuzione come il seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-261">If you deploy a template that creates more than four cores in the West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="fd074-262">In alternativa, in PowerShell è possibile usare il cmdlet **Get-AzureRmVMUsage** .</span><span class="sxs-lookup"><span data-stu-id="fd074-262">Or in PowerShell, you can use the **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="fd074-263">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="fd074-263">Which returns:</span></span>

```powershell
...
CurrentValue : 0
Limit        : 4
Name         : {
                 "value": "cores",
                 "localizedValue": "Total Regional Cores"
               }
Unit         : null
...
```

<span data-ttu-id="fd074-264">In questi casi, si deve accedere al portale e rivolgersi all'assistenza per richiedere l'aumento della quota per l'area di destinazione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-264">In these cases, you should go to the portal and file a support issue to raise your quota for the region into which you want to deploy.</span></span>

> [!NOTE]
> <span data-ttu-id="fd074-265">Tenere presente che per i gruppi di risorse, la quota è riferita alle singole aree e non all'intera sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="fd074-265">Remember that for resource groups, the quota is for each individual region, not for the entire subscription.</span></span> <span data-ttu-id="fd074-266">Se è necessario distribuire 30 core nell'area Stati Uniti occidentali, è necessario richiedere 30 core di gestione delle risorse per Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="fd074-266">If you need to deploy 30 cores in West US, you have to ask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="fd074-267">Se è necessario distribuire 30 core in qualsiasi area a cui si ha accesso, è consigliabile richiedere 30 core di Resource Manager in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="fd074-267">If you need to deploy 30 cores in any of the regions to which you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="fd074-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="fd074-268">InvalidContentLink</span></span>
<span data-ttu-id="fd074-269">Quando viene visualizzato il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="fd074-269">When you receive the error message:</span></span>

```
Code=InvalidContentLink
Message=Unable to download deployment content from ...
```

<span data-ttu-id="fd074-270">È probabile che si sia tentato il collegamento a un modello annidato non disponibile.</span><span class="sxs-lookup"><span data-stu-id="fd074-270">You have most likely attempted to link to a nested template that is not available.</span></span> <span data-ttu-id="fd074-271">Ricontrollare l'URI specificato per il modello annidato.</span><span class="sxs-lookup"><span data-stu-id="fd074-271">Double check the URI you provided for the nested template.</span></span> <span data-ttu-id="fd074-272">Se il modello si trova in un account di archiviazione, verificare che l'URI sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="fd074-272">If the template exists in a storage account, make sure the URI is accessible.</span></span> <span data-ttu-id="fd074-273">Potrebbe essere necessario passare un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="fd074-273">You may need to pass a SAS token.</span></span> <span data-ttu-id="fd074-274">Per altre informazioni, vedere [Uso di modelli collegati con Gestione risorse di Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="fd074-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="fd074-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="fd074-276">Questo errore viene visualizzato quando la sottoscrizione include un criterio che impedisce di eseguire un'azione desiderata in fase distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying to perform during deployment.</span></span> <span data-ttu-id="fd074-277">Cercare l'identificatore del criterio nel messaggio di errore</span><span class="sxs-lookup"><span data-stu-id="fd074-277">In the error message, look for the policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="fd074-278">e specificarlo in **PowerShell** come parametro **Id** per recuperare i dettagli relativi al criterio che ha bloccato la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="fd074-278">In **PowerShell**, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="fd074-279">Nell'**interfaccia della riga di comando di Azure** specificare il nome della definizione del criterio:</span><span class="sxs-lookup"><span data-stu-id="fd074-279">In **Azure CLI**, provide the name of the policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="fd074-280">Per altre informazioni, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="fd074-280">For more information, see the following articles:</span></span>

- [<span data-ttu-id="fd074-281">Errore RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="fd074-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="fd074-282">[Usare i criteri per gestire le risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-282">[Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="fd074-283">L'autorizzazione non è riuscita</span><span class="sxs-lookup"><span data-stu-id="fd074-283">Authorization failed</span></span>
<span data-ttu-id="fd074-284">Si può ricevere un messaggio di errore durante la distribuzione perché l'account o l'entità servizio che prova a distribuire le risorse non ha l'accesso necessario per eseguire tali azioni.</span><span class="sxs-lookup"><span data-stu-id="fd074-284">You may receive an error during deployment because the account or service principal attempting to deploy the resources does not have access to perform those actions.</span></span> <span data-ttu-id="fd074-285">Azure Active Directory consente all'utente o all'amministratore di controllare con un'elevata precisione quali identità possono accedere e a quali risorse.</span><span class="sxs-lookup"><span data-stu-id="fd074-285">Azure Active Directory enables you or your administrator to control which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="fd074-286">Se l'account è assegnato al ruolo Lettore, ad esempio, non è possibile creare nuove risorse.</span><span class="sxs-lookup"><span data-stu-id="fd074-286">For example, if your account is assigned to the Reader role, you are not able to create resources.</span></span> <span data-ttu-id="fd074-287">In tal caso verrà visualizzato un messaggio di errore che indica che l'autorizzazione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="fd074-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="fd074-288">Per altre informazioni sul controllo degli accessi in base al ruolo, vedere [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="fd074-289">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd074-289">Next steps</span></span>
* <span data-ttu-id="fd074-290">Per altre informazioni sulle azioni di controllo, vedere [Operazioni di controllo con Resource Manager](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-290">To learn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="fd074-291">Per altre informazioni sulle azioni che consentono di determinare gli errori di distribuzione, vedere [Visualizzare le operazioni di distribuzione con il portale di Azure](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="fd074-291">To learn about actions to determine the errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
