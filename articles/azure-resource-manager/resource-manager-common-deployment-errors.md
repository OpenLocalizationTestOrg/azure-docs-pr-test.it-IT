---
title: gli errori di distribuzione di Azure comuni aaaTroubleshoot | Documenti Microsoft
description: Viene descritto come tooresolve errori comuni quando si distribuisce tooAzure risorse usando Gestione risorse di Azure.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Errore di distribuzione, distribuzione di azure, distribuire tooazure
ms.assetid: c002a9be-4de5-4963-bd14-b54aa3d8fa59
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/17/2017
ms.author: tomfitz
ms.openlocfilehash: 8571e9941879eb5586e4258a785b6a09247da771
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-common-azure-deployment-errors-with-azure-resource-manager"></a><span data-ttu-id="d7f19-104">Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d7f19-104">Troubleshoot common Azure deployment errors with Azure Resource Manager</span></span>
<span data-ttu-id="d7f19-105">Questo argomento illustra come risolvere alcuni errori comuni che possono verificarsi durante la distribuzione di risorse in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f19-105">This topic describes how you can resolve some common Azure deployment errors you may encounter.</span></span>

<span data-ttu-id="d7f19-106">in questo argomento viene descritti i Hello codici di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="d7f19-106">hello following error codes are described in this topic:</span></span>

* [<span data-ttu-id="d7f19-107">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="d7f19-107">AccountNameInvalid</span></span>](#accountnameinvalid)
* [<span data-ttu-id="d7f19-108">Authorization failed</span><span class="sxs-lookup"><span data-stu-id="d7f19-108">Authorization failed</span></span>](#authorization-failed)
* [<span data-ttu-id="d7f19-109">BadRequest</span><span class="sxs-lookup"><span data-stu-id="d7f19-109">BadRequest</span></span>](#badrequest)
* [<span data-ttu-id="d7f19-110">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="d7f19-110">DeploymentFailed</span></span>](#deploymentfailed)
* [<span data-ttu-id="d7f19-111">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="d7f19-111">DisallowedOperation</span></span>](#disallowedoperation)
* [<span data-ttu-id="d7f19-112">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="d7f19-112">InvalidContentLink</span></span>](#invalidcontentlink)
* [<span data-ttu-id="d7f19-113">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="d7f19-113">InvalidTemplate</span></span>](#invalidtemplate)
* [<span data-ttu-id="d7f19-114">MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="d7f19-114">MissingSubscriptionRegistration</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="d7f19-115">NotFound</span><span class="sxs-lookup"><span data-stu-id="d7f19-115">NotFound</span></span>](#notfound)
* [<span data-ttu-id="d7f19-116">NoRegisteredProviderFound</span><span class="sxs-lookup"><span data-stu-id="d7f19-116">NoRegisteredProviderFound</span></span>](#noregisteredproviderfound)
* [<span data-ttu-id="d7f19-117">OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="d7f19-117">OperationNotAllowed</span></span>](#quotaexceeded)
* [<span data-ttu-id="d7f19-118">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="d7f19-118">ParentResourceNotFound</span></span>](#parentresourcenotfound)
* [<span data-ttu-id="d7f19-119">QuotaExceeded</span><span class="sxs-lookup"><span data-stu-id="d7f19-119">QuotaExceeded</span></span>](#quotaexceeded)
* [<span data-ttu-id="d7f19-120">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="d7f19-120">RequestDisallowedByPolicy</span></span>](#requestdisallowedbypolicy)
* [<span data-ttu-id="d7f19-121">ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="d7f19-121">ResourceNotFound</span></span>](#notfound)
* [<span data-ttu-id="d7f19-122">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="d7f19-122">SkuNotAvailable</span></span>](#skunotavailable)
* [<span data-ttu-id="d7f19-123">StorageAccountAlreadyExists</span><span class="sxs-lookup"><span data-stu-id="d7f19-123">StorageAccountAlreadyExists</span></span>](#storagenamenotunique)
* [<span data-ttu-id="d7f19-124">StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="d7f19-124">StorageAccountAlreadyTaken</span></span>](#storagenamenotunique)

## <a name="deploymentfailed"></a><span data-ttu-id="d7f19-125">DeploymentFailed</span><span class="sxs-lookup"><span data-stu-id="d7f19-125">DeploymentFailed</span></span>

<span data-ttu-id="d7f19-126">Questo codice di errore indica un errore di distribuzione generale, ma non è il codice di errore hello necessario toostart risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d7f19-126">This error code indicates a general deployment error, but it is not hello error code you need toostart troubleshooting.</span></span> <span data-ttu-id="d7f19-127">codice di errore Hello effettivamente consente di risolvere il problema di hello è in genere un livello di sotto di questo errore.</span><span class="sxs-lookup"><span data-stu-id="d7f19-127">hello error code that actually helps you resolve hello issue is usually one level below this error.</span></span> <span data-ttu-id="d7f19-128">Ad esempio, hello seguente immagine Mostra hello **RequestDisallowedByPolicy** codice di errore che si trova sotto l'errore di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-128">For example, hello following image shows hello **RequestDisallowedByPolicy** error code that is under hello deployment error.</span></span>

![mostra codice di errore](./media/resource-manager-common-deployment-errors/error-code.png)

## <a name="skunotavailable"></a><span data-ttu-id="d7f19-130">SkuNotAvailable</span><span class="sxs-lookup"><span data-stu-id="d7f19-130">SkuNotAvailable</span></span>

<span data-ttu-id="d7f19-131">Quando si distribuisce una risorsa (in genere una macchina virtuale), potrebbe essere visualizzato hello messaggio di errore e codice di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="d7f19-131">When deploying a resource (typically a virtual machine), you may receive hello following error code and error message:</span></span>

```
Code: SkuNotAvailable
Message: hello requested tier for resource '<resource>' is currently not available in location '<location>' 
for subscription '<subscriptionID>'. Please try another tier or deploy tooa different location.
```

<span data-ttu-id="d7f19-132">Viene visualizzato questo errore quando hello risorsa SKU selezionato (ad esempio, dimensioni della macchina virtuale) non è disponibile per il percorso di hello selezionato.</span><span class="sxs-lookup"><span data-stu-id="d7f19-132">You receive this error when hello resource SKU you have selected (such as VM size) is not available for hello location you have selected.</span></span> <span data-ttu-id="d7f19-133">tooresolve questo problema, è necessario toodetermine SKU disponibili in un'area.</span><span class="sxs-lookup"><span data-stu-id="d7f19-133">tooresolve this issue, you need toodetermine which SKUs are available in a region.</span></span> <span data-ttu-id="d7f19-134">È possibile utilizzare PowerShell, portale hello o un toofind operazione REST SKU disponibile.</span><span class="sxs-lookup"><span data-stu-id="d7f19-134">You can use PowerShell, hello portal, or a REST operation toofind available SKUs.</span></span>

- <span data-ttu-id="d7f19-135">Per PowerShell usare [Get AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) e filtrare in base al percorso.</span><span class="sxs-lookup"><span data-stu-id="d7f19-135">For PowerShell, use [Get-AzureRmComputeResourceSku](/powershell/module/azurerm.compute/get-azurermcomputeresourcesku) and filter by location.</span></span> <span data-ttu-id="d7f19-136">È necessario disporre di hello più recente di PowerShell per questo comando.</span><span class="sxs-lookup"><span data-stu-id="d7f19-136">You must have hello latest version of PowerShell for this command.</span></span>

  ```powershell
  Get-AzureRmComputeResourceSku | where {$_.Locations.Contains("southcentralus")}
  ```

  <span data-ttu-id="d7f19-137">risultati di Hello includono un elenco di SKU per la posizione di hello ed eventuali restrizioni per tale SKU.</span><span class="sxs-lookup"><span data-stu-id="d7f19-137">hello results include a list of SKUs for hello location and any restrictions for that SKU.</span></span>

  ```powershell
  ResourceType                Name      Locations Restriction                      Capability Value
  ------------                ----      --------- -----------                      ---------- -----
  availabilitySets         Classic southcentralus             MaximumPlatformFaultDomainCount     3
  availabilitySets         Aligned southcentralus             MaximumPlatformFaultDomainCount     3
  virtualMachines      Standard_A0 southcentralus
  virtualMachines      Standard_A1 southcentralus
  virtualMachines      Standard_A2 southcentralus
  ```

- <span data-ttu-id="d7f19-138">hello toouse [portal](https://portal.azure.com), accedi al portale toohello e aggiungere una risorsa tramite l'interfaccia di hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-138">toouse hello [portal](https://portal.azure.com), log in toohello portal and add a resource through hello interface.</span></span> <span data-ttu-id="d7f19-139">Quando si impostano i valori hello, vedrai hello SKU disponibili per tale risorsa.</span><span class="sxs-lookup"><span data-stu-id="d7f19-139">As you set hello values, you see hello available SKUs for that resource.</span></span> <span data-ttu-id="d7f19-140">Non è necessario distribuzione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="d7f19-140">You do not need toocomplete hello deployment.</span></span>

    ![SKU disponibili](./media/resource-manager-common-deployment-errors/view-sku.png)

- <span data-ttu-id="d7f19-142">toouse hello API REST per le macchine virtuali, inviare hello seguito richiesta:</span><span class="sxs-lookup"><span data-stu-id="d7f19-142">toouse hello REST API for virtual machines, send hello following request:</span></span>

  ```HTTP 
  GET
  https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/skus?api-version=2016-03-30
  ```

  <span data-ttu-id="d7f19-143">Restituisce le SKU e le aree disponibili in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="d7f19-143">It returns available SKUs and regions in hello following format:</span></span>

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

<span data-ttu-id="d7f19-144">Se si è grado toofind uno SKU adatto in tale area o un'area alternativa che soddisfa le esigenze aziendali, inviare un [richiesta SKU](https://aka.ms/skurestriction) tooAzure supporto.</span><span class="sxs-lookup"><span data-stu-id="d7f19-144">If you are unable toofind a suitable SKU in that region or an alternative region that meets your business needs, submit a [SKU request](https://aka.ms/skurestriction) tooAzure Support.</span></span>

## <a name="disallowedoperation"></a><span data-ttu-id="d7f19-145">DisallowedOperation</span><span class="sxs-lookup"><span data-stu-id="d7f19-145">DisallowedOperation</span></span>

```
Code: DisallowedOperation
Message: hello current subscription type is not permitted tooperform operations on any provider 
namespace. Please use a different subscription.
```

<span data-ttu-id="d7f19-146">Se si riceve questo errore, si utilizza una sottoscrizione che non è consentito tooaccess tutti i servizi Azure diverso da Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d7f19-146">If you receive this error, you are using a subscription that is not permitted tooaccess any Azure services other than Azure Active Directory.</span></span> <span data-ttu-id="d7f19-147">Questo tipo di sottoscrizione possono verificarsi quando è necessario portale classico di hello tooaccess ma non sono consentiti toodeploy risorse.</span><span class="sxs-lookup"><span data-stu-id="d7f19-147">You might have this type of subscription when you need tooaccess hello classic portal but are not permitted toodeploy resources.</span></span> <span data-ttu-id="d7f19-148">tooresolve questo problema, è necessario utilizzare una sottoscrizione che dispone dell'autorizzazione toodeploy risorse.</span><span class="sxs-lookup"><span data-stu-id="d7f19-148">tooresolve this issue, you must use a subscription that has permission toodeploy resources.</span></span>  

<span data-ttu-id="d7f19-149">tooview le sottoscrizioni disponibili con PowerShell, usare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-149">tooview your available subscriptions with PowerShell, use:</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="d7f19-150">Inoltre, tooset hello abbonamento, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-150">And, tooset hello current subscription, use:</span></span>

```powershell
Set-AzureRmContext -SubscriptionName {subscription-name}
```

<span data-ttu-id="d7f19-151">tooview le sottoscrizioni disponibili con l'interfaccia CLI di Azure 2.0, usare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-151">tooview your available subscriptions with Azure CLI 2.0, use:</span></span>

```azurecli
az account list
```

<span data-ttu-id="d7f19-152">Inoltre, tooset hello abbonamento, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-152">And, tooset hello current subscription, use:</span></span>

```azurecli
az account set --subscription {subscription-name}
```

## <a name="invalidtemplate"></a><span data-ttu-id="d7f19-153">InvalidTemplate</span><span class="sxs-lookup"><span data-stu-id="d7f19-153">InvalidTemplate</span></span>
<span data-ttu-id="d7f19-154">Questo errore può essere causato da diversi tipi di errori.</span><span class="sxs-lookup"><span data-stu-id="d7f19-154">This error can result from several different types of errors.</span></span>

- <span data-ttu-id="d7f19-155">Errore di sintassi</span><span class="sxs-lookup"><span data-stu-id="d7f19-155">Syntax error</span></span>

   <span data-ttu-id="d7f19-156">Se si riceve un messaggio di errore che indica di convalida del modello non è stato possibile hello, potrebbe essere un problema di sintassi nel modello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-156">If you receive an error message that indicates hello template failed validation, you may have a syntax problem in your template.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed
  ```

   <span data-ttu-id="d7f19-157">Questo errore è facile toomake perché le espressioni del modello possono essere complesse.</span><span class="sxs-lookup"><span data-stu-id="d7f19-157">This error is easy toomake because template expressions can be intricate.</span></span> <span data-ttu-id="d7f19-158">Ad esempio, hello seguente assegnazione del nome per un account di archiviazione contiene un set di parentesi, tre funzioni, tre set di parentesi, un set di virgolette singole e una proprietà:</span><span class="sxs-lookup"><span data-stu-id="d7f19-158">For example, hello following name assignment for a storage account contains one set of brackets, three functions, three sets of parentheses, one set of single quotes, and one property:</span></span>

  ```json
  "name": "[concat('storage', uniqueString(resourceGroup().id))]",
  ```

   <span data-ttu-id="d7f19-159">Se non si fornisce la sintassi corrispondente hello, modello hello produce un valore diverso da quello l'intenzione.</span><span class="sxs-lookup"><span data-stu-id="d7f19-159">If you do not provide hello matching syntax, hello template produces a value that is different than your intention.</span></span>

   <span data-ttu-id="d7f19-160">Quando si riceve questo tipo di errore, esaminare attentamente la sintassi dell'espressione hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-160">When you receive this type of error, carefully review hello expression syntax.</span></span> <span data-ttu-id="d7f19-161">È consigliabile usare un editor JSON come [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) o [Visual Studio Code](resource-manager-vs-code.md) che può segnalare gli errori di sintassi.</span><span class="sxs-lookup"><span data-stu-id="d7f19-161">Consider using a JSON editor like [Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md) or [Visual Studio Code](resource-manager-vs-code.md), which can warn you about syntax errors.</span></span>

- <span data-ttu-id="d7f19-162">Lunghezze di segmenti non valide</span><span class="sxs-lookup"><span data-stu-id="d7f19-162">Incorrect segment lengths</span></span>

   <span data-ttu-id="d7f19-163">Un altro errore di modello non valido si verifica quando il nome di risorsa hello non è nel formato corretto hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-163">Another invalid template error occurs when hello resource name is not in hello correct format.</span></span>

  ```
  Code=InvalidTemplate
  Message=Deployment template validation failed: 'hello template resource {resource-name}'
  for type {resource-type} has incorrect segment lengths.
  ```

   <span data-ttu-id="d7f19-164">Una risorsa di livello radice deve avere un segmento di meno nel nome hello nel tipo di risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-164">A root level resource must have one less segment in hello name than in hello resource type.</span></span> <span data-ttu-id="d7f19-165">Ogni segmento si differenzia mediante una barra.</span><span class="sxs-lookup"><span data-stu-id="d7f19-165">Each segment is differentiated by a slash.</span></span> <span data-ttu-id="d7f19-166">Nell'esempio seguente di hello, sono presenti due segmenti di tipo hello e nome hello include un segmento, pertanto è un **valido**.</span><span class="sxs-lookup"><span data-stu-id="d7f19-166">In hello following example, hello type has two segments and hello name has one segment, so it is a **valid name**.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="d7f19-167">Ma l'esempio successivo hello è **nome non valido** perché contiene hello stesso numero di segmenti di tipo hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-167">But hello next example is **not a valid name** because it has hello same number of segments as hello type.</span></span>

  ```json
  {
    "type": "Microsoft.Web/serverfarms",
    "name": "appPlan/myHostingPlanName",
    ...
  }
  ```

   <span data-ttu-id="d7f19-168">Per le risorse figlio, necessario hello tipo hello e il nome stesso numero di segmenti.</span><span class="sxs-lookup"><span data-stu-id="d7f19-168">For child resources, hello type and name have hello same number of segments.</span></span> <span data-ttu-id="d7f19-169">Questo numero di segmenti è utile perché il nome completo di hello e il tipo per l'elemento figlio di hello include hello padre nome e il tipo.</span><span class="sxs-lookup"><span data-stu-id="d7f19-169">This number of segments makes sense because hello full name and type for hello child includes hello parent name and type.</span></span> <span data-ttu-id="d7f19-170">Pertanto, nome completo di hello dispone ancora di una minore segmento di tipo completo hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-170">Therefore, hello full name still has one less segment than hello full type.</span></span>

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

   <span data-ttu-id="d7f19-171">Segmenti di hello recupero corretti possono risultare difficile con tipi di gestione risorse che vengono applicati ai provider di risorse.</span><span class="sxs-lookup"><span data-stu-id="d7f19-171">Getting hello segments right can be tricky with Resource Manager types that are applied across resource providers.</span></span> <span data-ttu-id="d7f19-172">Ad esempio, l'applicazione di un sito web di risorsa lock tooa richiede un tipo con quattro segmenti.</span><span class="sxs-lookup"><span data-stu-id="d7f19-172">For example, applying a resource lock tooa web site requires a type with four segments.</span></span> <span data-ttu-id="d7f19-173">Pertanto, il nome di hello è tre segmenti:</span><span class="sxs-lookup"><span data-stu-id="d7f19-173">Therefore, hello name is three segments:</span></span>

  ```json
  {
      "type": "Microsoft.Web/sites/providers/locks",
      "name": "[concat(variables('siteName'),'/Microsoft.Authorization/MySiteLock')]",
      ...
  }
  ```

- <span data-ttu-id="d7f19-174">Indice di copia non previsto</span><span class="sxs-lookup"><span data-stu-id="d7f19-174">Copy index is not expected</span></span>

   <span data-ttu-id="d7f19-175">Si verifica questo **InvalidTemplate** errore una volta applicata hello **copia** parte tooa elemento del modello di hello che non supporta questo elemento.</span><span class="sxs-lookup"><span data-stu-id="d7f19-175">You encounter this **InvalidTemplate** error when you have applied hello **copy** element tooa part of hello template that does not support this element.</span></span> <span data-ttu-id="d7f19-176">È possibile applicare solo tipo di risorsa tooa hello Copia elemento.</span><span class="sxs-lookup"><span data-stu-id="d7f19-176">You can only apply hello copy element tooa resource type.</span></span> <span data-ttu-id="d7f19-177">Non è possibile applicare proprietà tooa copia all'interno di un tipo di risorsa.</span><span class="sxs-lookup"><span data-stu-id="d7f19-177">You cannot apply copy tooa property within a resource type.</span></span> <span data-ttu-id="d7f19-178">Ad esempio, si applica una macchina virtuale tooa di copia, ma non è possibile applicare i dischi del sistema operativo toohello per una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d7f19-178">For example, you apply copy tooa virtual machine, but you cannot apply it toohello OS disks for a virtual machine.</span></span> <span data-ttu-id="d7f19-179">In alcuni casi, è possibile convertire un toocreate risorse figlio risorsa tooa padre un ciclo di copia.</span><span class="sxs-lookup"><span data-stu-id="d7f19-179">In some cases, you can convert a child resource tooa parent resource toocreate a copy loop.</span></span> <span data-ttu-id="d7f19-180">Per altre informazioni sull'uso di copy, vedere [Creare più istanze di risorse in Azure Resource Manager](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-180">For more information about using copy, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

- <span data-ttu-id="d7f19-181">Parametro non valido</span><span class="sxs-lookup"><span data-stu-id="d7f19-181">Parameter is not valid</span></span>

   <span data-ttu-id="d7f19-182">Se il modello hello specifica valori consentiti per un parametro e specificare un valore che non fa parte di tali valori, viene visualizzato un toohello simile messaggio errore seguente:</span><span class="sxs-lookup"><span data-stu-id="d7f19-182">If hello template specifies permitted values for a parameter, and you provide a value that is not one of those values, you receive a message similar toohello following error:</span></span>

  ```
  Code=InvalidTemplate;
  Message=Deployment template validation failed: 'hello provided value {parameter value}
  for hello template parameter {parameter name} is not valid. hello parameter value is not
  part of hello allowed values
  ``` 

   <span data-ttu-id="d7f19-183">Hello verificare i valori consentiti nel modello hello e forniscono uno durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d7f19-183">Double check hello allowed values in hello template, and provide one during deployment.</span></span>

- <span data-ttu-id="d7f19-184">È stata rilevata una dipendenza circolare</span><span class="sxs-lookup"><span data-stu-id="d7f19-184">Circular dependency detected</span></span>

   <span data-ttu-id="d7f19-185">Viene visualizzato questo errore quando risorse dipendono tra loro in modo che impedisce la distribuzione di hello avvio.</span><span class="sxs-lookup"><span data-stu-id="d7f19-185">You receive this error when resources depend on each other in a way that prevents hello deployment from starting.</span></span> <span data-ttu-id="d7f19-186">A causa di una combinazione di interdipendenze, due o più risorse attendono altre risorse che sono a propria volta in attesa.</span><span class="sxs-lookup"><span data-stu-id="d7f19-186">A combination of interdependencies makes two or more resource wait for other resources that are also waiting.</span></span> <span data-ttu-id="d7f19-187">Ad esempio, la risorsa 1 dipende dalla risorsa 3, la risorsa 2 dipende dalla risorsa 1 e la risorsa 3 dipende dalla risorsa 2.</span><span class="sxs-lookup"><span data-stu-id="d7f19-187">For example, resource1 depends on resource3, resource2 depends on resource1, and resource3 depends on resource2.</span></span> <span data-ttu-id="d7f19-188">È in genere possibile risolvere questo problema rimuovendo le dipendenze non necessarie.</span><span class="sxs-lookup"><span data-stu-id="d7f19-188">You can usually solve this problem by removing unnecessary dependencies.</span></span> 

<a id="notfound" />
### <a name="notfound-and-resourcenotfound"></a><span data-ttu-id="d7f19-189">NotFound and ResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="d7f19-189">NotFound and ResourceNotFound</span></span>
<span data-ttu-id="d7f19-190">Quando il modello include il nome di hello di una risorsa che non può essere risolti, viene visualizzato un errore simile a:</span><span class="sxs-lookup"><span data-stu-id="d7f19-190">When your template includes hello name of a resource that cannot be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="d7f19-191">Se si sta tentando di hello toodeploy risorsa nel modello hello mancante, verificare se è necessario tooadd una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="d7f19-191">If you are attempting toodeploy hello missing resource in hello template, check whether you need tooadd a dependency.</span></span> <span data-ttu-id="d7f19-192">Azure Resource Manager consente di ottimizzare la distribuzione creando risorse in parallelo, quando ciò è possibile.</span><span class="sxs-lookup"><span data-stu-id="d7f19-192">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="d7f19-193">Se una risorsa deve essere distribuita dopo un'altra risorsa, è necessario hello toouse **dependsOn** hello di elemento del modello di toocreate una dipendenza da un'altra risorsa.</span><span class="sxs-lookup"><span data-stu-id="d7f19-193">If one resource must be deployed after another resource, you need toouse hello **dependsOn** element in your template toocreate a dependency on hello other resource.</span></span> <span data-ttu-id="d7f19-194">Ad esempio, quando si distribuisce un'app web, deve esistere hello piano di servizio App.</span><span class="sxs-lookup"><span data-stu-id="d7f19-194">For example, when deploying a web app, hello App Service plan must exist.</span></span> <span data-ttu-id="d7f19-195">Se non è stato specificato hello web app dipende dal piano di servizio App hello, Gestione risorse crea entrambe le risorse hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="d7f19-195">If you have not specified that hello web app depends on hello App Service plan, Resource Manager creates both resources at hello same time.</span></span> <span data-ttu-id="d7f19-196">Viene visualizzato un errore che informa che hello risorse piano di servizio App non viene trovata, perché non esiste ancora durante il tentativo di una proprietà nell'applicazione web hello tooset.</span><span class="sxs-lookup"><span data-stu-id="d7f19-196">You receive an error stating that hello App Service plan resource cannot be found, because it does not exist yet when attempting tooset a property on hello web app.</span></span> <span data-ttu-id="d7f19-197">Evitare questo errore impostando dipendenza hello in hello web app.</span><span class="sxs-lookup"><span data-stu-id="d7f19-197">You prevent this error by setting hello dependency in hello web app.</span></span>

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

<span data-ttu-id="d7f19-198">Per suggerimenti sulla risoluzione degli errori relativi alle dipendenze, vedere [Controllare la sequenza di distribuzione](#check-deployment-sequence).</span><span class="sxs-lookup"><span data-stu-id="d7f19-198">For suggestions on troubleshooting dependency errors, see [Check deployment sequence](#check-deployment-sequence).</span></span>

<span data-ttu-id="d7f19-199">È inoltre possibile visualizzare questo errore quando la risorsa hello esiste in un gruppo di risorse diverso da quello hello uno vengono distribuite negli.</span><span class="sxs-lookup"><span data-stu-id="d7f19-199">You also see this error when hello resource exists in a different resource group than hello one being deployed to.</span></span> <span data-ttu-id="d7f19-200">In tal caso, utilizzare hello [funzione resourceId](resource-group-template-functions-resource.md#resourceid) tooget hello il nome completo della risorsa hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-200">In that case, use hello [resourceId function](resource-group-template-functions-resource.md#resourceid) tooget hello fully qualified name of hello resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

<span data-ttu-id="d7f19-201">Se si tenta di hello toouse [riferimento](resource-group-template-functions-resource.md#reference) o [elenco chiavi del](resource-group-template-functions-resource.md#listkeys) funzioni con una risorsa che non possono essere risolti, viene visualizzato il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="d7f19-201">If you attempt toouse hello [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that cannot be resolved, you receive hello following error:</span></span>

```
Code=ResourceNotFound;
Message=hello Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

<span data-ttu-id="d7f19-202">Cercare un'espressione che include hello **riferimento** (funzione).</span><span class="sxs-lookup"><span data-stu-id="d7f19-202">Look for an expression that includes hello **reference** function.</span></span> <span data-ttu-id="d7f19-203">Verificare che i valori di parametro hello siano corretti.</span><span class="sxs-lookup"><span data-stu-id="d7f19-203">Double check that hello parameter values are correct.</span></span>

## <a name="parentresourcenotfound"></a><span data-ttu-id="d7f19-204">ParentResourceNotFound</span><span class="sxs-lookup"><span data-stu-id="d7f19-204">ParentResourceNotFound</span></span>

<span data-ttu-id="d7f19-205">Quando una risorsa è una risorsa di tooanother padre, risorsa padre hello deve esistere prima di creare la risorsa figlio hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-205">When one resource is a parent tooanother resource, hello parent resource must exist before creating hello child resource.</span></span> <span data-ttu-id="d7f19-206">Se non esiste ancora, viene visualizzato il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="d7f19-206">If it does not yet exist, you receive hello following error:</span></span>

```
Code=ParentResourceNotFound;
Message=Can not perform requested operation on nested resource. Parent resource 'exampleserver' not found."
```

<span data-ttu-id="d7f19-207">nome di Hello della risorsa figlio hello include il nome del padre hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-207">hello name of hello child resource includes hello parent name.</span></span> <span data-ttu-id="d7f19-208">Ad esempio, un database SQL può essere definito come segue:</span><span class="sxs-lookup"><span data-stu-id="d7f19-208">For example, a SQL Database might be defined as:</span></span>

```json
{
  "type": "Microsoft.Sql/servers/databases",
  "name": "[concat(variables('databaseServerName'), '/', parameters('databaseName'))]",
  ...
```

<span data-ttu-id="d7f19-209">Tuttavia, se non si specifica una dipendenza sulla risorsa padre hello, risorsa figlio hello può ottenere distribuita prima padre hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-209">But, if you do not specify a dependency on hello parent resource, hello child resource may get deployed before hello parent.</span></span> <span data-ttu-id="d7f19-210">tooresolve questo errore, includere una dipendenza.</span><span class="sxs-lookup"><span data-stu-id="d7f19-210">tooresolve this error, include a dependency.</span></span>

```json
"dependsOn": [
    "[variables('databaseServerName')]"
]
```

<a id="storagenamenotunique" />

## <a name="storageaccountalreadyexists-and-storageaccountalreadytaken"></a><span data-ttu-id="d7f19-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span><span class="sxs-lookup"><span data-stu-id="d7f19-211">StorageAccountAlreadyExists and StorageAccountAlreadyTaken</span></span>
<span data-ttu-id="d7f19-212">Per gli account di archiviazione, è necessario fornire un nome per la risorsa hello che è univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f19-212">For storage accounts, you must provide a name for hello resource that is unique across Azure.</span></span> <span data-ttu-id="d7f19-213">Se non si specifica un nome univoco, verrà visualizzato un errore come il seguente:</span><span class="sxs-lookup"><span data-stu-id="d7f19-213">If you do not provide a unique name, you receive an error like:</span></span>

```
Code=StorageAccountAlreadyTaken
Message=hello storage account named mystorage is already taken.
```

<span data-ttu-id="d7f19-214">È possibile creare un nome univoco concatenando la convenzione di denominazione con risultato hello hello [uniqueString](resource-group-template-functions-string.md#uniquestring) (funzione).</span><span class="sxs-lookup"><span data-stu-id="d7f19-214">You can create a unique name by concatenating your naming convention with hello result of hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function.</span></span>

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]",
"type": "Microsoft.Storage/storageAccounts",
```

<span data-ttu-id="d7f19-215">Se si distribuisce un account di archiviazione con hello stesso nome di un account di archiviazione esistente nella sottoscrizione, ma fornire un percorso diverso, viene visualizzato un errore che indica che account di archiviazione hello già presente in un percorso diverso.</span><span class="sxs-lookup"><span data-stu-id="d7f19-215">If you deploy a storage account with hello same name as an existing storage account in your subscription, but provide a different location, you receive an error indicating hello storage account already exists in a different location.</span></span> <span data-ttu-id="d7f19-216">Eliminare l'account di archiviazione esistente hello o fornire hello nello stesso percorso come hello account di archiviazione esistente.</span><span class="sxs-lookup"><span data-stu-id="d7f19-216">Either delete hello existing storage account, or provide hello same location as hello existing storage account.</span></span>

## <a name="accountnameinvalid"></a><span data-ttu-id="d7f19-217">AccountNameInvalid</span><span class="sxs-lookup"><span data-stu-id="d7f19-217">AccountNameInvalid</span></span>
<span data-ttu-id="d7f19-218">Vedrai hello **AccountNameInvalid** errore durante il tentativo di toogive uno spazio di archiviazione account un nome che include caratteri non consentiti.</span><span class="sxs-lookup"><span data-stu-id="d7f19-218">You see hello **AccountNameInvalid** error when attempting toogive a storage account a name that includes prohibited characters.</span></span> <span data-ttu-id="d7f19-219">I nomi degli account di archiviazione devono essere di lunghezza compresa tra 3 e 24 caratteri e utilizzare solo numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="d7f19-219">Storage account names must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span> <span data-ttu-id="d7f19-220">Hello [uniqueString](resource-group-template-functions-string.md#uniquestring) funzione restituisce 13 caratteri.</span><span class="sxs-lookup"><span data-stu-id="d7f19-220">hello [uniqueString](resource-group-template-functions-string.md#uniquestring) function returns 13 characters.</span></span> <span data-ttu-id="d7f19-221">Se si concatena toohello un prefisso **uniqueString** provocare, fornire un prefisso di 11 caratteri o meno.</span><span class="sxs-lookup"><span data-stu-id="d7f19-221">If you concatenate a prefix toohello **uniqueString** result, provide a prefix that is 11 characters or less.</span></span>

## <a name="badrequest"></a><span data-ttu-id="d7f19-222">RichiestaNonValida</span><span class="sxs-lookup"><span data-stu-id="d7f19-222">BadRequest</span></span>

<span data-ttu-id="d7f19-223">Quando per una proprietà si specifica un valore non valido, può comparire lo stato BadRequest.</span><span class="sxs-lookup"><span data-stu-id="d7f19-223">You may encounter a BadRequest status when you provide an invalid value for a property.</span></span> <span data-ttu-id="d7f19-224">Ad esempio, se si fornisce un valore SKU non corretto per un account di archiviazione, hello distribuzione non riesce.</span><span class="sxs-lookup"><span data-stu-id="d7f19-224">For example, if you provide an incorrect SKU value for a storage account, hello deployment fails.</span></span> <span data-ttu-id="d7f19-225">Esaminare i valori validi per la proprietà, toodetermine hello [API REST](/rest/api) per il tipo di risorsa hello si sta distribuendo.</span><span class="sxs-lookup"><span data-stu-id="d7f19-225">toodetermine valid values for property, look at hello [REST API](/rest/api) for hello resource type you are deploying.</span></span>

<a id="noregisteredproviderfound" />

## <a name="noregisteredproviderfound-and-missingsubscriptionregistration"></a><span data-ttu-id="d7f19-226">NoRegisteredProviderFound e MissingSubscriptionRegistration</span><span class="sxs-lookup"><span data-stu-id="d7f19-226">NoRegisteredProviderFound and MissingSubscriptionRegistration</span></span>
<span data-ttu-id="d7f19-227">Durante la distribuzione di risorse, è possibile ricevere hello seguente codice di errore e di messaggio:</span><span class="sxs-lookup"><span data-stu-id="d7f19-227">When deploying resource, you may receive hello following error code and message:</span></span>

```
Code: NoRegisteredProviderFound
Message: No registered resource provider found for location {location}
and API version {api-version} for type {resource-type}.
```

<span data-ttu-id="d7f19-228">In alternativa, si potrebbe ricevere un messaggio analogo che indica:</span><span class="sxs-lookup"><span data-stu-id="d7f19-228">Or, you may receive a similar message that states:</span></span>

```
Code: MissingSubscriptionRegistration
Message: hello subscription is not registered toouse namespace {resource-provider-namespace}
```

<span data-ttu-id="d7f19-229">Questi errori vengono visualizzati per uno di questi tre motivi:</span><span class="sxs-lookup"><span data-stu-id="d7f19-229">You receive these errors for one of three reasons:</span></span>

1. <span data-ttu-id="d7f19-230">provider di risorse Hello non è stato registrato per la sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="d7f19-230">hello resource provider has not been registered for your subscription</span></span>
2. <span data-ttu-id="d7f19-231">Versione dell'API non è supportata per il tipo di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="d7f19-231">API version not supported for hello resource type</span></span>
3. <span data-ttu-id="d7f19-232">Percorso non è supportata per il tipo di risorsa hello</span><span class="sxs-lookup"><span data-stu-id="d7f19-232">Location not supported for hello resource type</span></span>

<span data-ttu-id="d7f19-233">messaggio di errore Hello deve contenere suggerimenti per percorsi hello supportato e le versioni dell'API.</span><span class="sxs-lookup"><span data-stu-id="d7f19-233">hello error message should give you suggestions for hello supported locations and API versions.</span></span> <span data-ttu-id="d7f19-234">È possibile modificare il modello tooone di hello valori consigliati.</span><span class="sxs-lookup"><span data-stu-id="d7f19-234">You can change your template tooone of hello suggested values.</span></span> <span data-ttu-id="d7f19-235">La maggior parte dei provider vengono registrati automaticamente da hello Azure interfaccia della riga di comando di portale o hello in uso, ma non tutte.</span><span class="sxs-lookup"><span data-stu-id="d7f19-235">Most providers are registered automatically by hello Azure portal or hello command-line interface you are using, but not all.</span></span> <span data-ttu-id="d7f19-236">Se non è stato utilizzato un provider di risorse specifico prima, si potrebbe essere necessario tooregister tale provider.</span><span class="sxs-lookup"><span data-stu-id="d7f19-236">If you have not used a particular resource provider before, you may need tooregister that provider.</span></span> <span data-ttu-id="d7f19-237">È possibile ottenere altre informazioni sui provider di risorse tramite PowerShell o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f19-237">You can discover more about resource providers through PowerShell or Azure CLI.</span></span>

<span data-ttu-id="d7f19-238">**Portale**</span><span class="sxs-lookup"><span data-stu-id="d7f19-238">**Portal**</span></span>

<span data-ttu-id="d7f19-239">È possibile vedere lo stato della registrazione hello e registrare uno spazio dei nomi del provider di risorse tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-239">You can see hello registration status and register a resource provider namespace through hello portal.</span></span>

1. <span data-ttu-id="d7f19-240">Selezionare **Provider di risorse** per la propria sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="d7f19-240">For your subscription, select **Resource providers**.</span></span>

   ![selezionare i provider di risorse](./media/resource-manager-common-deployment-errors/select-resource-provider.png)

2. <span data-ttu-id="d7f19-242">Esaminare hello elenco di provider di risorse e, se necessario, selezionare hello **registrare** provider di risorse hello tooregister collegamento di tipo hello che si sta tentando di toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d7f19-242">Look at hello list of resource providers, and if necessary, select hello **Register** link tooregister hello resource provider of hello type you are trying toodeploy.</span></span>

   ![Elenco di provider di risorse](./media/resource-manager-common-deployment-errors/list-resource-providers.png)

<span data-ttu-id="d7f19-244">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="d7f19-244">**PowerShell**</span></span>

<span data-ttu-id="d7f19-245">toosee lo stato di registrazione, utilizzare **Get AzureRmResourceProvider**.</span><span class="sxs-lookup"><span data-stu-id="d7f19-245">toosee your registration status, use **Get-AzureRmResourceProvider**.</span></span>

```powershell
Get-AzureRmResourceProvider -ListAvailable
```

<span data-ttu-id="d7f19-246">tooregister un provider, utilizzare **registro AzureRmResourceProvider** e specificare il nome di hello del provider di risorse hello desiderato tooregister.</span><span class="sxs-lookup"><span data-stu-id="d7f19-246">tooregister a provider, use **Register-AzureRmResourceProvider** and provide hello name of hello resource provider you wish tooregister.</span></span>

```powershell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Cdn
```

<span data-ttu-id="d7f19-247">percorsi di tooget hello è supportato per un particolare tipo di risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-247">tooget hello supported locations for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

<span data-ttu-id="d7f19-248">hello tooget supportate le versioni dell'API per un particolare tipo di risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-248">tooget hello supported API versions for a particular type of resource, use:</span></span>

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).ApiVersions
```

<span data-ttu-id="d7f19-249">**Interfaccia della riga di comando di Azure**</span><span class="sxs-lookup"><span data-stu-id="d7f19-249">**Azure CLI**</span></span>

<span data-ttu-id="d7f19-250">toosee se il provider di hello è registrato, utilizzare hello `azure provider list` comando.</span><span class="sxs-lookup"><span data-stu-id="d7f19-250">toosee whether hello provider is registered, use hello `azure provider list` command.</span></span>

```azurecli
az provider list
```

<span data-ttu-id="d7f19-251">tooregister un provider di risorse, utilizzare hello `azure provider register` comando e specificare hello *dello spazio dei nomi* tooregister.</span><span class="sxs-lookup"><span data-stu-id="d7f19-251">tooregister a resource provider, use hello `azure provider register` command, and specify hello *namespace* tooregister.</span></span>

```azurecli
az provider register --namespace Microsoft.Cdn
```

<span data-ttu-id="d7f19-252">percorsi supportato hello toosee e le versioni dell'API per un tipo di risorsa, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="d7f19-252">toosee hello supported locations and API versions for a resource type, use:</span></span>

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

<a id="quotaexceeded" />

## <a name="quotaexceeded-and-operationnotallowed"></a><span data-ttu-id="d7f19-253">QuotaExceeded e OperationNotAllowed</span><span class="sxs-lookup"><span data-stu-id="d7f19-253">QuotaExceeded and OperationNotAllowed</span></span>
<span data-ttu-id="d7f19-254">Alcuni problemi potrebbero verificarsi quando una distribuzione supera una quota specifica per un gruppo di risorse, le sottoscrizioni, gli account o per altri ambiti.</span><span class="sxs-lookup"><span data-stu-id="d7f19-254">You might have issues when deployment exceeds a quota, which could be per resource group, subscriptions, accounts, and other scopes.</span></span> <span data-ttu-id="d7f19-255">Ad esempio, la sottoscrizione potrebbe essere configurato toolimit hello numero di core per un'area.</span><span class="sxs-lookup"><span data-stu-id="d7f19-255">For example, your subscription may be configured toolimit hello number of cores for a region.</span></span> <span data-ttu-id="d7f19-256">Se si tenta di toodeploy una macchina virtuale con più core di hello consentito quantità, viene visualizzato un errore indicante hello è stato superato.</span><span class="sxs-lookup"><span data-stu-id="d7f19-256">If you attempt toodeploy a virtual machine with more cores than hello permitted amount, you receive an error stating hello quota has been exceeded.</span></span>
<span data-ttu-id="d7f19-257">Per informazioni complete sulle quote, vedere [Sottoscrizione di Azure e limiti, quote e vincoli dei servizi](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-257">For complete quota information, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="d7f19-258">tooexamine le quote della sottoscrizione per core, è possibile utilizzare hello `azure vm list-usage` comando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7f19-258">tooexamine your subscription's quotas for cores, you can use hello `azure vm list-usage` command in hello Azure CLI.</span></span> <span data-ttu-id="d7f19-259">per un account di prova è 4, Hello di esempio seguente viene illustrato tale quota di core hello:</span><span class="sxs-lookup"><span data-stu-id="d7f19-259">hello following example illustrates that hello core quota for a free trial account is 4:</span></span>

```azurecli
az vm list-usage --location "South Central US"
```

<span data-ttu-id="d7f19-260">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="d7f19-260">Which returns:</span></span>

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

<span data-ttu-id="d7f19-261">Se si distribuisce un modello che crea più di quattro core nell'area Stati Uniti occidentali hello, viene visualizzato un errore simile a quello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="d7f19-261">If you deploy a template that creates more than four cores in hello West US region, you get a deployment error that looks like:</span></span>

```
Code=OperationNotAllowed
Message=Operation results in exceeding quota limits of Core.
Maximum allowed: 4, Current in use: 4, Additional requested: 2.
```

<span data-ttu-id="d7f19-262">O in PowerShell, è possibile utilizzare hello **Get AzureRmVMUsage** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d7f19-262">Or in PowerShell, you can use hello **Get-AzureRmVMUsage** cmdlet.</span></span>

```powershell
Get-AzureRmVMUsage
```

<span data-ttu-id="d7f19-263">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="d7f19-263">Which returns:</span></span>

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

<span data-ttu-id="d7f19-264">In questi casi, si deve passare toohello portal e file un tooraise problema supporto la quota per area hello in cui si desidera toodeploy.</span><span class="sxs-lookup"><span data-stu-id="d7f19-264">In these cases, you should go toohello portal and file a support issue tooraise your quota for hello region into which you want toodeploy.</span></span>

> [!NOTE]
> <span data-ttu-id="d7f19-265">Tenere presente che per gruppi di risorse, la quota hello per le singole aree, non per l'intera sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-265">Remember that for resource groups, hello quota is for each individual region, not for hello entire subscription.</span></span> <span data-ttu-id="d7f19-266">Se è necessario toodeploy 30 core negli Stati Uniti occidentali, è necessario tooask per 30 core di gestione delle risorse negli Stati Uniti occidentali.</span><span class="sxs-lookup"><span data-stu-id="d7f19-266">If you need toodeploy 30 cores in West US, you have tooask for 30 Resource Manager cores in West US.</span></span> <span data-ttu-id="d7f19-267">Se è necessario toodeploy 30 core delle toowhich aree hello è disponibile, è necessario richiedere 30 core di gestione risorse in tutte le aree.</span><span class="sxs-lookup"><span data-stu-id="d7f19-267">If you need toodeploy 30 cores in any of hello regions toowhich you have access, you should ask for 30 Resource Manager cores in all regions.</span></span>
>
>

## <a name="invalidcontentlink"></a><span data-ttu-id="d7f19-268">InvalidContentLink</span><span class="sxs-lookup"><span data-stu-id="d7f19-268">InvalidContentLink</span></span>
<span data-ttu-id="d7f19-269">Quando si riceve il messaggio di errore hello:</span><span class="sxs-lookup"><span data-stu-id="d7f19-269">When you receive hello error message:</span></span>

```
Code=InvalidContentLink
Message=Unable toodownload deployment content from ...
```

<span data-ttu-id="d7f19-270">Si è probabilmente tentato toolink tooa modello nidificato che non è disponibile.</span><span class="sxs-lookup"><span data-stu-id="d7f19-270">You have most likely attempted toolink tooa nested template that is not available.</span></span> <span data-ttu-id="d7f19-271">Verificare hello URI è fornito per il modello annidato hello.</span><span class="sxs-lookup"><span data-stu-id="d7f19-271">Double check hello URI you provided for hello nested template.</span></span> <span data-ttu-id="d7f19-272">Se il modello di hello esiste in un account di archiviazione, assicurarsi che hello URI sia accessibile.</span><span class="sxs-lookup"><span data-stu-id="d7f19-272">If hello template exists in a storage account, make sure hello URI is accessible.</span></span> <span data-ttu-id="d7f19-273">Potrebbe essere necessario toopass un token di firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="d7f19-273">You may need toopass a SAS token.</span></span> <span data-ttu-id="d7f19-274">Per altre informazioni, vedere [Uso di modelli collegati con Gestione risorse di Azure](resource-group-linked-templates.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-274">For more information, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

## <a name="requestdisallowedbypolicy"></a><span data-ttu-id="d7f19-275">RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="d7f19-275">RequestDisallowedByPolicy</span></span>
<span data-ttu-id="d7f19-276">Viene visualizzato questo errore quando la sottoscrizione include un criterio che impedisce a un'azione che si sta tentando di tooperform durante la distribuzione di risorse.</span><span class="sxs-lookup"><span data-stu-id="d7f19-276">You receive this error when your subscription includes a resource policy that prevents an action you are trying tooperform during deployment.</span></span> <span data-ttu-id="d7f19-277">Nel messaggio di errore hello, cercare l'identificatore hello dei criteri.</span><span class="sxs-lookup"><span data-stu-id="d7f19-277">In hello error message, look for hello policy identifier.</span></span>

```
Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'
```

<span data-ttu-id="d7f19-278">In **PowerShell**, fornire tale identificatore dei criteri come hello **Id** dettagli sui criteri hello bloccati distribuzione tooretrieve del parametro.</span><span class="sxs-lookup"><span data-stu-id="d7f19-278">In **PowerShell**, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

<span data-ttu-id="d7f19-279">In **CLI di Azure**, specificare il nome di hello della definizione di criteri hello:</span><span class="sxs-lookup"><span data-stu-id="d7f19-279">In **Azure CLI**, provide hello name of hello policy definition:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

<span data-ttu-id="d7f19-280">Per ulteriori informazioni, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="d7f19-280">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="d7f19-281">Errore RequestDisallowedByPolicy</span><span class="sxs-lookup"><span data-stu-id="d7f19-281">RequestDisallowedByPolicy error</span></span>](resource-manager-policy-requestdisallowedbypolicy-error.md)
- <span data-ttu-id="d7f19-282">[Usare criteri toomanage risorse e controllare l'accesso](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-282">[Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="authorization-failed"></a><span data-ttu-id="d7f19-283">L'autorizzazione non è riuscita</span><span class="sxs-lookup"><span data-stu-id="d7f19-283">Authorization failed</span></span>
<span data-ttu-id="d7f19-284">Si potrebbe ricevere un errore durante la distribuzione perché hello account o il tentativo di risorse hello toodeploy entità servizio non dispone di accesso tooperform tali azioni.</span><span class="sxs-lookup"><span data-stu-id="d7f19-284">You may receive an error during deployment because hello account or service principal attempting toodeploy hello resources does not have access tooperform those actions.</span></span> <span data-ttu-id="d7f19-285">Azure Active Directory consente o l'amministratore toocontrol le identità che possono accedere le risorse con un elevato livello di precisione.</span><span class="sxs-lookup"><span data-stu-id="d7f19-285">Azure Active Directory enables you or your administrator toocontrol which identities can access what resources with a great degree of precision.</span></span> <span data-ttu-id="d7f19-286">Ad esempio, se l'account viene assegnato il ruolo di lettore toohello, non sono in grado di toocreate risorse.</span><span class="sxs-lookup"><span data-stu-id="d7f19-286">For example, if your account is assigned toohello Reader role, you are not able toocreate resources.</span></span> <span data-ttu-id="d7f19-287">In tal caso verrà visualizzato un messaggio di errore che indica che l'autorizzazione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="d7f19-287">In that case, you see an error message indicating that authorization failed.</span></span>

<span data-ttu-id="d7f19-288">Per altre informazioni sul controllo degli accessi in base al ruolo, vedere [Controllo degli accessi in base al ruolo di Azure](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-288">For more information about role-based access control, see [Azure Role-Based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="d7f19-289">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7f19-289">Next steps</span></span>
* <span data-ttu-id="d7f19-290">toolearn sul controllo delle azioni, vedere [controllare le operazioni con Gestione risorse di](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-290">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="d7f19-291">toolearn sugli errori di hello toodetermine azioni durante la distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d7f19-291">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
