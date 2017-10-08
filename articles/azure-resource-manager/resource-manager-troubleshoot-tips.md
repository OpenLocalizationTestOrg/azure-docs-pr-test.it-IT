---
title: errori di distribuzione di Azure aaaUnderstand | Documenti Microsoft
description: Viene descritto come toolearn sugli errori di distribuzione di Azure.
services: azure-resource-manager
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
keywords: Errore di distribuzione, distribuzione di azure, distribuire tooazure
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: support-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: tomfitz
ms.openlocfilehash: a335e121e9b908a763374907e34b1f6e823d6e96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="understand-azure-deployment-errors"></a><span data-ttu-id="084be-104">Informazioni sugli errori di distribuzione di Azure</span><span class="sxs-lookup"><span data-stu-id="084be-104">Understand Azure deployment errors</span></span>
<span data-ttu-id="084be-105">In questo argomento vengono descritti gli errori di distribuzione e le modalità per reperire altre informazioni sull'errore.</span><span class="sxs-lookup"><span data-stu-id="084be-105">This topic describes deployment errors and how you can discover more information about an error.</span></span> <span data-ttu-id="084be-106">Per errori di distribuzione toocommon risoluzioni, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="084be-106">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="two-types-of-errors"></a><span data-ttu-id="084be-107">Due tipi di errori</span><span class="sxs-lookup"><span data-stu-id="084be-107">Two types of errors</span></span>
<span data-ttu-id="084be-108">I possibili errori sono di due tipi:</span><span class="sxs-lookup"><span data-stu-id="084be-108">There are two types of errors you can receive:</span></span>

* <span data-ttu-id="084be-109">errori di convalida</span><span class="sxs-lookup"><span data-stu-id="084be-109">validation errors</span></span>
* <span data-ttu-id="084be-110">errori di distribuzione</span><span class="sxs-lookup"><span data-stu-id="084be-110">deployment errors</span></span>

<span data-ttu-id="084be-111">Hello seguente immagine mostra il registro attività hello per una sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="084be-111">hello following image shows hello activity log for a subscription.</span></span> <span data-ttu-id="084be-112">Rappresenta due distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="084be-112">It represents two deployments.</span></span> <span data-ttu-id="084be-113">In una distribuzione modello hello convalida non riuscita (**convalida**) e non è stata eseguita.</span><span class="sxs-lookup"><span data-stu-id="084be-113">In one deployment, hello template failed validation (**Validate**) and did not proceed.</span></span> <span data-ttu-id="084be-114">In hello altra distribuzione, il modello di hello ha superato la convalida, ma non riuscita durante la creazione di risorse hello (**scrivere distribuzioni**).</span><span class="sxs-lookup"><span data-stu-id="084be-114">In hello other deployment, hello template passed validation but failed when creating hello resources (**Write Deployments**).</span></span> 

![mostra codice di errore](./media/resource-manager-troubleshoot-tips/show-activity-log.png)

<span data-ttu-id="084be-116">Gli errori di convalida sono causati da scenari già determinati prima della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="084be-116">Validation errors arise from scenarios that can be determined before deployment.</span></span> <span data-ttu-id="084be-117">Errori di sintassi includono nel modello o durante il tentativo risorse toodeploy superano il quote della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="084be-117">They include syntax errors in your template, or trying toodeploy resources that would exceed your subscription quotas.</span></span> <span data-ttu-id="084be-118">Errori di distribuzione sono causati da condizioni che si verificano durante il processo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="084be-118">Deployment errors arise from conditions that occur during hello deployment process.</span></span> <span data-ttu-id="084be-119">È incluso il tentativo di tooaccess una risorsa che viene distribuita in parallelo.</span><span class="sxs-lookup"><span data-stu-id="084be-119">They include trying tooaccess a resource that is being deployed in parallel.</span></span>

<span data-ttu-id="084be-120">Entrambi i tipi di errori restituito un codice di errore di utilizzare tootroubleshoot hello distribuzione.</span><span class="sxs-lookup"><span data-stu-id="084be-120">Both types of errors return an error code that you use tootroubleshoot hello deployment.</span></span> <span data-ttu-id="084be-121">Entrambi i tipi di errori vengono visualizzati in hello [log attività](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="084be-121">Both types of errors appear in hello [activity log](resource-group-audit.md).</span></span> <span data-ttu-id="084be-122">Tuttavia, gli errori di convalida non vengono visualizzati nella cronologia di distribuzione perché la distribuzione di hello mai avviata.</span><span class="sxs-lookup"><span data-stu-id="084be-122">However, validation errors do not appear in your deployment history because hello deployment never started.</span></span>

## <a name="determine-error-code"></a><span data-ttu-id="084be-123">Determinare il codice di errore</span><span class="sxs-lookup"><span data-stu-id="084be-123">Determine error code</span></span>

<span data-ttu-id="084be-124">Per informazioni sull'errore esaminando il messaggio di errore hello e codice di errore hello.</span><span class="sxs-lookup"><span data-stu-id="084be-124">You can learn about an error by looking at hello error message and hello error code.</span></span> <span data-ttu-id="084be-125">Hello [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md) articolo vengono elencati le risoluzioni da codice di errore.</span><span class="sxs-lookup"><span data-stu-id="084be-125">hello [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md) article lists resolutions by error code.</span></span> <span data-ttu-id="084be-126">Questo argomento viene illustrato come toouse hello codice di errore hello toodiscover portale Azure.</span><span class="sxs-lookup"><span data-stu-id="084be-126">This topic shows how toouse hello Azure portal toodiscover hello error code.</span></span>

### <a name="validation-errors"></a><span data-ttu-id="084be-127">Errori di convalida</span><span class="sxs-lookup"><span data-stu-id="084be-127">Validation errors</span></span>

<span data-ttu-id="084be-128">Durante la distribuzione tramite il portale di hello, viene visualizzato un errore di convalida dopo l'invio dei valori.</span><span class="sxs-lookup"><span data-stu-id="084be-128">When deploying through hello portal, you see a validation error after submitting your values.</span></span>

![vista dell'errore di convalida nel portale](./media/resource-manager-troubleshoot-tips/validation-error.png)

<span data-ttu-id="084be-130">Selezionare il messaggio hello per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="084be-130">Select hello message for more details.</span></span> <span data-ttu-id="084be-131">Nella seguente immagine di hello, vedrai un **InvalidTemplateDeployment** errore e un messaggio che indica un criterio di distribuzione sia bloccato.</span><span class="sxs-lookup"><span data-stu-id="084be-131">In hello following image, you see an **InvalidTemplateDeployment** error and a message that indicates a policy blocked deployment.</span></span>

![visualizzare le informazioni di convalida](./media/resource-manager-troubleshoot-tips/validation-details.png)

### <a name="deployment-errors"></a><span data-ttu-id="084be-133">Errori di distribuzione</span><span class="sxs-lookup"><span data-stu-id="084be-133">Deployment errors</span></span>

<span data-ttu-id="084be-134">Quando l'operazione di hello supera la convalida, ma non riesce durante la distribuzione, viene visualizzato l'errore di hello nelle notifiche hello.</span><span class="sxs-lookup"><span data-stu-id="084be-134">When hello operation passes validation, but fails during deployment, you see hello error in hello notifications.</span></span> <span data-ttu-id="084be-135">Selezionare hello notifica.</span><span class="sxs-lookup"><span data-stu-id="084be-135">Select hello notification.</span></span>

![Notifica di errore](./media/resource-manager-troubleshoot-tips/notification.png)

<span data-ttu-id="084be-137">Visualizzare ulteriori dettagli sulla distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="084be-137">You see more details about hello deployment.</span></span> <span data-ttu-id="084be-138">Selezionare hello opzione toofind ulteriori informazioni sull'errore hello.</span><span class="sxs-lookup"><span data-stu-id="084be-138">Select hello option toofind more information about hello error.</span></span>

![distribuzione non riuscita](./media/resource-manager-troubleshoot-tips/deployment-failed.png)

<span data-ttu-id="084be-140">Vedere i codici di errore e messaggi di errore hello.</span><span class="sxs-lookup"><span data-stu-id="084be-140">You see hello error message and error codes.</span></span> <span data-ttu-id="084be-141">Si noti che sono presenti due codici di errore.</span><span class="sxs-lookup"><span data-stu-id="084be-141">Notice there are two error codes.</span></span> <span data-ttu-id="084be-142">Hello primo codice di errore (**DeploymentFailed**) è un errore generale che non fornisce i dettagli di hello è necessario errore hello toosolve.</span><span class="sxs-lookup"><span data-stu-id="084be-142">hello first error code (**DeploymentFailed**) is a general error that does not provide hello details you need toosolve hello error.</span></span> <span data-ttu-id="084be-143">Hello secondo codice di errore (**StorageAccountNotFound**) fornisce i dettagli di hello è necessario.</span><span class="sxs-lookup"><span data-stu-id="084be-143">hello second error code (**StorageAccountNotFound**) provides hello details you need.</span></span> 

![dettagli dell'errore](./media/resource-manager-troubleshoot-tips/error-details.png)

## <a name="enable-debug-logging"></a><span data-ttu-id="084be-145">Abilitazione della registrazione di debug</span><span class="sxs-lookup"><span data-stu-id="084be-145">Enable debug logging</span></span>
<span data-ttu-id="084be-146">Talvolta è necessario ulteriori informazioni su hello richiesta e risposta toodiscover la causa dell'errore.</span><span class="sxs-lookup"><span data-stu-id="084be-146">Sometimes you need more information about hello request and response toodiscover what went wrong.</span></span> <span data-ttu-id="084be-147">Con PowerShell o l'interfaccia della riga di comando di Azure è possibile richiedere la registrazione di informazioni aggiuntive durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="084be-147">By using PowerShell or Azure CLI, you can request that additional information is logged during a deployment.</span></span>

- <span data-ttu-id="084be-148">PowerShell</span><span class="sxs-lookup"><span data-stu-id="084be-148">PowerShell</span></span>

   <span data-ttu-id="084be-149">In PowerShell, impostare hello **DeploymentDebugLogLevel** parametro tooAll, ResponseContent o RequestContent.</span><span class="sxs-lookup"><span data-stu-id="084be-149">In PowerShell, set hello **DeploymentDebugLogLevel** parameter tooAll, ResponseContent, or RequestContent.</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -ResourceGroupName examplegroup -TemplateFile c:\Azure\Templates\storage.json -DeploymentDebugLogLevel All
  ```

   <span data-ttu-id="084be-150">Esaminare il contenuto di richiesta hello con hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="084be-150">Examine hello request content with hello following cmdlet:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.request | ConvertTo-Json
  ```

   <span data-ttu-id="084be-151">In alternativa, hello risposta contenuto con:</span><span class="sxs-lookup"><span data-stu-id="084be-151">Or, hello response content with:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName storageonly -ResourceGroupName startgroup).Properties.response | ConvertTo-Json
  ```

   <span data-ttu-id="084be-152">Queste informazioni consentono di determinare se un valore nel modello di hello è impostato in modo non corretto.</span><span class="sxs-lookup"><span data-stu-id="084be-152">This information can help you determine whether a value in hello template is being incorrectly set.</span></span>

- <span data-ttu-id="084be-153">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="084be-153">Azure CLI</span></span>

   <span data-ttu-id="084be-154">Esaminare le operazioni di distribuzione hello con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="084be-154">Examine hello deployment operations with hello following command:</span></span>

  ```azurecli
  az group deployment operation list --resource-group ExampleGroup --name vmlinux
  ```

- <span data-ttu-id="084be-155">Modello annidato</span><span class="sxs-lookup"><span data-stu-id="084be-155">Nested template</span></span>

   <span data-ttu-id="084be-156">informazioni di debug toolog per un modello annidato, utilizzare hello **debugSetting** elemento.</span><span class="sxs-lookup"><span data-stu-id="084be-156">toolog debug information for a nested template, use hello **debugSetting** element.</span></span>

  ```json
  {
      "apiVersion": "2016-09-01",
      "name": "nestedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
          "mode": "Incremental",
          "templateLink": {
              "uri": "{template-uri}",
              "contentVersion": "1.0.0.0"
          },
          "debugSetting": {
             "detailLevel": "requestContent, responseContent"
          }
      }
  }
  ```


## <a name="create-a-troubleshooting-template"></a><span data-ttu-id="084be-157">Creare un modello per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="084be-157">Create a troubleshooting template</span></span>
<span data-ttu-id="084be-158">In alcuni casi, hello tootroubleshoot modo più semplice del modello è tootest parti di esso.</span><span class="sxs-lookup"><span data-stu-id="084be-158">In some cases, hello easiest way tootroubleshoot your template is tootest parts of it.</span></span> <span data-ttu-id="084be-159">È possibile creare un modello semplificato che consente di toofocus parte hello che si ritiene che sta provocando errore hello.</span><span class="sxs-lookup"><span data-stu-id="084be-159">You can create a simplified template that enables you toofocus on hello part that you believe is causing hello error.</span></span> <span data-ttu-id="084be-160">Si supponga, ad esempio, di ricevere un errore quando si fa riferimento a una risorsa.</span><span class="sxs-lookup"><span data-stu-id="084be-160">For example, suppose you are receiving an error when referencing a resource.</span></span> <span data-ttu-id="084be-161">Anziché gestire un intero modello, creare un modello che restituisce parte di hello che potrebbe causare il problema.</span><span class="sxs-lookup"><span data-stu-id="084be-161">Rather than dealing with an entire template, create a template that returns hello part that may be causing your problem.</span></span> <span data-ttu-id="084be-162">Consentono di determinare se si sta passando parametri corretti hello, correttamente, l'utilizzo delle funzioni di modello e recupero hello risorsa desiderato.</span><span class="sxs-lookup"><span data-stu-id="084be-162">It can help you determine whether you are passing in hello right parameters, using template functions correctly, and getting hello resource you expect.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageName": {
        "type": "string"
    },
    "storageResourceGroup": {
        "type": "string"
    }
  },
  "variables": {},
  "resources": [],
  "outputs": {
    "exampleOutput": {
        "value": "[reference(resourceId(parameters('storageResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('storageName')), '2016-05-01')]",
        "type" : "object"
    }
  }
}
```

<span data-ttu-id="084be-163">In alternativa, si supponga che si rilevano errori di distribuzione che si ritengono correlati tooincorrectly impostare le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="084be-163">Or, suppose you are encountering deployment errors that you believe are related tooincorrectly set dependencies.</span></span> <span data-ttu-id="084be-164">Testare il modello suddividendolo in modelli semplificati.</span><span class="sxs-lookup"><span data-stu-id="084be-164">Test your template by breaking it into simplified templates.</span></span> <span data-ttu-id="084be-165">Creare innanzitutto un modello che distribuisce una sola risorsa (ad esempio SQL Server).</span><span class="sxs-lookup"><span data-stu-id="084be-165">First, create a template that deploys only a single resource (like a SQL Server).</span></span> <span data-ttu-id="084be-166">Quando si è certi che la risorsa sia definita correttamente, aggiungere una risorsa che dipende da essa (ad esempio un database SQL).</span><span class="sxs-lookup"><span data-stu-id="084be-166">When you are sure you have that resource correctly defined, add a resource that depends on it (like a SQL Database).</span></span> <span data-ttu-id="084be-167">Una volta definite correttamente queste due risorse, aggiungere altre risorse che dipendono da esse (ad esempio criteri di controllo).</span><span class="sxs-lookup"><span data-stu-id="084be-167">When you have those two resources correctly defined, add other dependent resources (like auditing policies).</span></span> <span data-ttu-id="084be-168">Tra ogni distribuzione di test, eliminare hello gruppo toomake che è adeguata test hello dipendenze delle risorse.</span><span class="sxs-lookup"><span data-stu-id="084be-168">In between each test deployment, delete hello resource group toomake sure you adequately testing hello dependencies.</span></span> 

## <a name="check-deployment-sequence"></a><span data-ttu-id="084be-169">Controllare la sequenza di distribuzione</span><span class="sxs-lookup"><span data-stu-id="084be-169">Check deployment sequence</span></span>

<span data-ttu-id="084be-170">Molti errori di distribuzione si verificano quando le risorse vengono distribuite secondo una sequenza imprevista.</span><span class="sxs-lookup"><span data-stu-id="084be-170">Many deployment errors happen when resources are deployed in an unexpected sequence.</span></span> <span data-ttu-id="084be-171">Questi errori vengono generati quando le dipendenze non sono impostate correttamente.</span><span class="sxs-lookup"><span data-stu-id="084be-171">These errors arise when dependencies are not correctly set.</span></span> <span data-ttu-id="084be-172">Quando manca una dipendenza necessaria, una risorsa tenta toouse che un valore per un'altra risorsa mentre altri hello non esiste ancora.</span><span class="sxs-lookup"><span data-stu-id="084be-172">When you are missing a needed dependency, one resource attempts toouse a value for another resource but hello other does not yet exist.</span></span> <span data-ttu-id="084be-173">e viene visualizzato un errore che indica che non è stata trovata una risorsa.</span><span class="sxs-lookup"><span data-stu-id="084be-173">You get an error stating that a resource is not found.</span></span> <span data-ttu-id="084be-174">Questo tipo di errore possono verificarsi a intermittenza perché hello tempo di distribuzione per ogni risorsa può variare.</span><span class="sxs-lookup"><span data-stu-id="084be-174">You may encounter this type of error intermittently because hello deployment time for each resource can vary.</span></span> <span data-ttu-id="084be-175">Ad esempio, il primo toodeploy tentativo le risorse ha esito positivo perché una risorsa necessaria viene completato in modo casuale in tempo.</span><span class="sxs-lookup"><span data-stu-id="084be-175">For example, your first attempt toodeploy your resources succeeds because a required resource randomly completes in time.</span></span> <span data-ttu-id="084be-176">Tuttavia, il secondo tentativo ha esito negativo perché hello necessarie risorse non è stata completata nel tempo.</span><span class="sxs-lookup"><span data-stu-id="084be-176">However, your second attempt fails because hello required resource did not complete in time.</span></span> 

<span data-ttu-id="084be-177">Tuttavia, si desidera tooavoid impostazione delle dipendenze che non è necessari.</span><span class="sxs-lookup"><span data-stu-id="084be-177">But, you want tooavoid setting dependencies that are not needed.</span></span> <span data-ttu-id="084be-178">Se si dispone di dipendenze non necessari, si prolungare durata hello della distribuzione hello impedendo le risorse che non sono interdipendenti vengano distribuiti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="084be-178">When you have unnecessary dependencies, you prolong hello duration of hello deployment by preventing resources that are not dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="084be-179">Inoltre, è possibile creare dipendenze circolari che bloccano la distribuzione di hello.</span><span class="sxs-lookup"><span data-stu-id="084be-179">In addition, you may create circular dependencies that block hello deployment.</span></span> <span data-ttu-id="084be-180">Hello [riferimento](resource-group-template-functions-resource.md#reference) funzione crea una relazione implicita sulla risorsa a cui fa riferimento hello, quando tale risorsa è distribuita in hello stesso modello.</span><span class="sxs-lookup"><span data-stu-id="084be-180">hello [reference](resource-group-template-functions-resource.md#reference) function creates an implicit dependency on hello referenced resource, when that resource is deployed in hello same template.</span></span> <span data-ttu-id="084be-181">Pertanto, è possibile altre dipendenze di dipendenze di hello specificate in hello **dependsOn** proprietà.</span><span class="sxs-lookup"><span data-stu-id="084be-181">Therefore, you may have more dependencies than hello dependencies specified in hello **dependsOn** property.</span></span> <span data-ttu-id="084be-182">Hello [resourceId](resource-group-template-functions-resource.md#resourceid) funzione non creare una relazione implicita o verificare l'esistenza di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="084be-182">hello [resourceId](resource-group-template-functions-resource.md#resourceid) function does not create an implicit dependency or validate that hello resource exists.</span></span>

<span data-ttu-id="084be-183">Quando si verificano problemi di dipendenza, è necessario comprendere toogain ordine hello di distribuzione di risorse.</span><span class="sxs-lookup"><span data-stu-id="084be-183">When you encounter dependency problems, you need toogain insight into hello order of resource deployment.</span></span> <span data-ttu-id="084be-184">ordine di hello tooview di operazioni di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="084be-184">tooview hello order of deployment operations:</span></span>

1. <span data-ttu-id="084be-185">Selezionare la cronologia della distribuzione hello per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="084be-185">Select hello deployment history for your resource group.</span></span>

   ![selezionare la cronologia delle distribuzioni](./media/resource-manager-troubleshoot-tips/select-deployment.png)

2. <span data-ttu-id="084be-187">Selezionare una distribuzione dalla cronologia hello e **eventi**.</span><span class="sxs-lookup"><span data-stu-id="084be-187">Select a deployment from hello history, and select **Events**.</span></span>

   ![selezionare gli eventi di distribuzione](./media/resource-manager-troubleshoot-tips/select-deployment-events.png)

3. <span data-ttu-id="084be-189">Esaminare la sequenza hello di eventi per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="084be-189">Examine hello sequence of events for each resource.</span></span> <span data-ttu-id="084be-190">Si paga stato toohello attenzione di ogni operazione.</span><span class="sxs-lookup"><span data-stu-id="084be-190">Pay attention toohello status of each operation.</span></span> <span data-ttu-id="084be-191">Ad esempio, hello immagine seguente mostra tre degli account di archiviazione distribuito in parallelo.</span><span class="sxs-lookup"><span data-stu-id="084be-191">For example, hello following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="084be-192">Si noti che hello tre account di archiviazione vengono avviate in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="084be-192">Notice that hello three storage accounts are started at hello same time.</span></span>

   ![distribuzione parallela](./media/resource-manager-troubleshoot-tips/deployment-events-parallel.png)

   <span data-ttu-id="084be-194">immagine successiva Hello mostra tre account di archiviazione che non vengono distribuiti in parallelo.</span><span class="sxs-lookup"><span data-stu-id="084be-194">hello next image shows three storage accounts that are not deployed in parallel.</span></span> <span data-ttu-id="084be-195">account di archiviazione secondo Hello dipende dal primo account di archiviazione hello e account di archiviazione terzo hello dipende dall'account di archiviazione secondo hello.</span><span class="sxs-lookup"><span data-stu-id="084be-195">hello second storage account depends on hello first storage account, and hello third storage account depends on hello second storage account.</span></span> <span data-ttu-id="084be-196">Pertanto, il primo account di archiviazione hello è avviato, accettati e completata prima che venga avviata hello accanto.</span><span class="sxs-lookup"><span data-stu-id="084be-196">Therefore, hello first storage account is started, accepted, and completed before hello next is started.</span></span>

   ![distribuzione sequenziale](./media/resource-manager-troubleshoot-tips/deployment-events-sequence.png)

<span data-ttu-id="084be-198">Anche per scenari più complessi, è possibile utilizzare hello stessa tecnica toodiscover quando la distribuzione è avviata e completata per ogni risorsa.</span><span class="sxs-lookup"><span data-stu-id="084be-198">Even for more complicated scenarios, you can use hello same technique toodiscover when deployment is started and completed for each resource.</span></span> <span data-ttu-id="084be-199">Se la sequenza hello è diversa da quello previsto, esaminare il toosee gli eventi di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="084be-199">Look through your deployment events toosee if hello sequence is different than you would expect.</span></span> <span data-ttu-id="084be-200">In questo caso, valutare di nuovo le dipendenze di hello per questa risorsa.</span><span class="sxs-lookup"><span data-stu-id="084be-200">If so, reevaluate hello dependencies for this resource.</span></span>

<span data-ttu-id="084be-201">Resource Manager identifica le dipendenze circolari durante la convalida del modello.</span><span class="sxs-lookup"><span data-stu-id="084be-201">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="084be-202">Restituisce quindi un messaggio di errore che indica specificamente la presenza di una dipendenza circolare.</span><span class="sxs-lookup"><span data-stu-id="084be-202">It returns an error message that specifically states a circular dependency exists.</span></span> <span data-ttu-id="084be-203">toosolve una dipendenza circolare:</span><span class="sxs-lookup"><span data-stu-id="084be-203">toosolve a circular dependency:</span></span>

1. <span data-ttu-id="084be-204">Nel modello, trovare la risorsa hello identificata una dipendenza circolare hello.</span><span class="sxs-lookup"><span data-stu-id="084be-204">In your template, find hello resource identified in hello circular dependency.</span></span> 
2. <span data-ttu-id="084be-205">Per tale risorsa, esaminare hello **dependsOn** proprietà e gli utilizzi di hello **riferimento** toosee le risorse dipende dalla funzione.</span><span class="sxs-lookup"><span data-stu-id="084be-205">For that resource, examine hello **dependsOn** property and any uses of hello **reference** function toosee which resources it depends on.</span></span> 
3. <span data-ttu-id="084be-206">Esaminare tali toosee risorse quali risorse cui dipendono.</span><span class="sxs-lookup"><span data-stu-id="084be-206">Examine those resources toosee which resources they depend on.</span></span> <span data-ttu-id="084be-207">Seguire le dipendenze di hello finché non si nota una risorsa che dipende dalla risorsa originale hello.</span><span class="sxs-lookup"><span data-stu-id="084be-207">Follow hello dependencies until you notice a resource that depends on hello original resource.</span></span>
5. <span data-ttu-id="084be-208">Per le risorse hello coinvolti in una dipendenza circolare hello, esaminare attentamente tutte le occorrenze di hello **dependsOn** tooidentify proprietà tutte le dipendenze che non sono necessari.</span><span class="sxs-lookup"><span data-stu-id="084be-208">For hello resources involved in hello circular dependency, carefully examine all uses of hello **dependsOn** property tooidentify any dependencies that are not needed.</span></span> <span data-ttu-id="084be-209">Rimuovere tali dipendenze.</span><span class="sxs-lookup"><span data-stu-id="084be-209">Remove those dependencies.</span></span> <span data-ttu-id="084be-210">Se non si è certi che una dipendenza sia necessaria, provare a rimuoverla.</span><span class="sxs-lookup"><span data-stu-id="084be-210">If you are unsure that a dependency is needed, try removing it.</span></span> 
6. <span data-ttu-id="084be-211">Ridistribuire il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="084be-211">Redeploy hello template.</span></span>

<span data-ttu-id="084be-212">Rimuovere i valori dal hello **dependsOn** proprietà può causare errori quando si distribuisce il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="084be-212">Removing values from hello **dependsOn** property can cause errors when you deploy hello template.</span></span> <span data-ttu-id="084be-213">Se si verifica un errore, aggiungere una dipendenza hello nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="084be-213">If you encounter an error, add hello dependency back into hello template.</span></span> 

<span data-ttu-id="084be-214">Se tale approccio non consente di risolvere una dipendenza circolare hello, è consigliabile spostare parte della logica di distribuzione in risorse figlio (ad esempio estensioni o le impostazioni di configurazione).</span><span class="sxs-lookup"><span data-stu-id="084be-214">If that approach does not solve hello circular dependency, consider moving part of your deployment logic into child resources (such as extensions or configuration settings).</span></span> <span data-ttu-id="084be-215">Dopo le risorse di hello coinvolte in una dipendenza circolare hello, configurare tali toodeploy risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="084be-215">Configure those child resources toodeploy after hello resources involved in hello circular dependency.</span></span> <span data-ttu-id="084be-216">Si supponga, ad esempio, si distribuiscono due macchine virtuali, ma è necessario impostare proprietà su ciascuna di esse che fanno riferimento altri toohello.</span><span class="sxs-lookup"><span data-stu-id="084be-216">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="084be-217">È possibile distribuirli in hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="084be-217">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="084be-218">VM 1</span><span class="sxs-lookup"><span data-stu-id="084be-218">vm1</span></span>
2. <span data-ttu-id="084be-219">VM 2</span><span class="sxs-lookup"><span data-stu-id="084be-219">vm2</span></span>
3. <span data-ttu-id="084be-220">L'estensione in VM 1 dipende da VM 1 e VM 2.</span><span class="sxs-lookup"><span data-stu-id="084be-220">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="084be-221">estensione Hello imposta valori per vm1 ottenute da vm2.</span><span class="sxs-lookup"><span data-stu-id="084be-221">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="084be-222">L'estensione in VM 2 dipende da VM 1 e VM 2.</span><span class="sxs-lookup"><span data-stu-id="084be-222">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="084be-223">estensione Hello imposta valori per vm2 ottenute da vm1.</span><span class="sxs-lookup"><span data-stu-id="084be-223">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="084be-224">Hello stesso approccio funziona per le applicazioni di servizio App.</span><span class="sxs-lookup"><span data-stu-id="084be-224">hello same approach works for App Service apps.</span></span> <span data-ttu-id="084be-225">Provare a spostare i valori di configurazione in una risorsa figlio della risorsa app hello.</span><span class="sxs-lookup"><span data-stu-id="084be-225">Consider moving configuration values into a child resource of hello app resource.</span></span> <span data-ttu-id="084be-226">È possibile distribuire due App web in hello seguente ordine:</span><span class="sxs-lookup"><span data-stu-id="084be-226">You can deploy two web apps in hello following order:</span></span>

1. <span data-ttu-id="084be-227">App Web 1</span><span class="sxs-lookup"><span data-stu-id="084be-227">webapp1</span></span>
2. <span data-ttu-id="084be-228">App Web 2</span><span class="sxs-lookup"><span data-stu-id="084be-228">webapp2</span></span>
3. <span data-ttu-id="084be-229">La configurazione per App Web 1 dipende da App Web 1 e App Web 2.</span><span class="sxs-lookup"><span data-stu-id="084be-229">config for webapp1 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="084be-230">Contiene impostazioni dell'app con valori di App Web 2.</span><span class="sxs-lookup"><span data-stu-id="084be-230">It contains app settings with values from webapp2.</span></span>
4. <span data-ttu-id="084be-231">La configurazione per App Web 2 dipende da App Web 1 e App Web 2.</span><span class="sxs-lookup"><span data-stu-id="084be-231">config for webapp2 depends on webapp1 and webapp2.</span></span> <span data-ttu-id="084be-232">Contiene impostazioni dell'app con valori di App Web 1.</span><span class="sxs-lookup"><span data-stu-id="084be-232">It contains app settings with values from webapp1.</span></span>


## <a name="next-steps"></a><span data-ttu-id="084be-233">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="084be-233">Next steps</span></span>
* <span data-ttu-id="084be-234">Per errori di distribuzione toocommon risoluzioni, vedere [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="084be-234">For resolutions toocommon deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="084be-235">toolearn sul controllo delle azioni, vedere [controllare le operazioni con Gestione risorse di](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="084be-235">toolearn about auditing actions, see [Audit operations with Resource Manager](resource-group-audit.md).</span></span>
* <span data-ttu-id="084be-236">toolearn sugli errori di hello toodetermine azioni durante la distribuzione, vedere [per visualizzare le operazioni di distribuzione](resource-manager-deployment-operations.md).</span><span class="sxs-lookup"><span data-stu-id="084be-236">toolearn about actions toodetermine hello errors during deployment, see [View deployment operations](resource-manager-deployment-operations.md).</span></span>
