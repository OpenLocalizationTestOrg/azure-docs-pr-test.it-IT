---
title: aaaDeployment operazioni con Azure Resource Manager | Documenti Microsoft
description: Viene descritto come le operazioni di distribuzione Azure Resource Manager tooview con hello portale, PowerShell, CLI di Azure e API REST.
services: azure-resource-manager,virtual-machines
documentationcenter: 
tags: top-support-issue
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: infrastructure
ms.date: 01/13/2017
ms.author: tomfitz
ms.openlocfilehash: ba4823ca73caca83dfc07c99d736344ef8b7b54d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="37e75-103">Visualizzare le operazioni di distribuzione con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="37e75-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="37e75-104">È possibile visualizzare le operazioni di hello per una distribuzione tramite il portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-104">You can view hello operations for a deployment through hello Azure portal.</span></span> <span data-ttu-id="37e75-105">Potrebbe essere più interessati a visualizzare operazioni hello quando si riceve un errore durante la distribuzione in modo da questo articolo è incentrato sulle operazioni che non sono stato di visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="37e75-105">You may be most interested in viewing hello operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="37e75-106">portale Hello fornisce un'interfaccia che consente gli errori di tooeasily trova hello e determinare potenziali correzioni.</span><span class="sxs-lookup"><span data-stu-id="37e75-106">hello portal provides an interface that enables you tooeasily find hello errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="37e75-107">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="37e75-107">Portal</span></span>
<span data-ttu-id="37e75-108">operazioni di distribuzione hello toosee, utilizzare hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="37e75-108">toosee hello deployment operations, use hello following steps:</span></span>

1. <span data-ttu-id="37e75-109">Per gruppo di risorse hello coinvolto nella distribuzione di hello, notare stato hello dell'ultima distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-109">For hello resource group involved in hello deployment, notice hello status of hello last deployment.</span></span> <span data-ttu-id="37e75-110">È possibile selezionare questo tooget stato ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="37e75-110">You can select this status tooget more details.</span></span>
   
    ![Stato della distribuzione](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="37e75-112">Vedrai cronologia distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-112">You see hello recent deployment history.</span></span> <span data-ttu-id="37e75-113">Selezionare la distribuzione di hello che non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="37e75-113">Select hello deployment that failed.</span></span>
   
    ![Stato della distribuzione](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="37e75-115">Selezionare toosee collegamento hello una descrizione del motivo hello distribuzione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="37e75-115">Select hello link toosee a description of why hello deployment failed.</span></span> <span data-ttu-id="37e75-116">Nella seguente figura hello record DNS hello non è univoco.</span><span class="sxs-lookup"><span data-stu-id="37e75-116">In hello image below, hello DNS record is not unique.</span></span>  
   
    ![visualizzare la distribuzione non riuscita](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="37e75-118">Questo messaggio di errore dovrebbe essere sufficiente per la risoluzione dei problemi toobegin.</span><span class="sxs-lookup"><span data-stu-id="37e75-118">This error message should be enough for you toobegin troubleshooting.</span></span> <span data-ttu-id="37e75-119">Tuttavia, se sono necessarie ulteriori informazioni sulle attività siano state completate, è possibile visualizzare le operazioni di hello come illustrato nell'hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="37e75-119">However, if you need more details about which tasks were completed, you can view hello operations as shown in hello following steps.</span></span>
4. <span data-ttu-id="37e75-120">È possibile visualizzare tutte le operazioni di distribuzione hello in hello **distribuzione** blade.</span><span class="sxs-lookup"><span data-stu-id="37e75-120">You can view all hello deployment operations in hello **Deployment** blade.</span></span> <span data-ttu-id="37e75-121">Selezionare qualsiasi toosee operazione ulteriori dettagli.</span><span class="sxs-lookup"><span data-stu-id="37e75-121">Select any operation toosee more details.</span></span>
   
    ![visualizzare operazioni](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="37e75-123">In questo caso, vedrai che hello account di archiviazione, rete virtuale e set di disponibilità sono stati creati.</span><span class="sxs-lookup"><span data-stu-id="37e75-123">In this case, you see that hello storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="37e75-124">indirizzo IP pubblico Hello non è riuscita e non si è tentate di altre risorse.</span><span class="sxs-lookup"><span data-stu-id="37e75-124">hello public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="37e75-125">È possibile visualizzare gli eventi per la distribuzione di hello selezionando **eventi**.</span><span class="sxs-lookup"><span data-stu-id="37e75-125">You can view events for hello deployment by selecting **Events**.</span></span>
   
    ![visualizzare eventi](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="37e75-127">Visualizzare tutti gli eventi di hello per la distribuzione di hello e selezionare uno per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="37e75-127">You see all hello events for hello deployment and select any one for more details.</span></span> <span data-ttu-id="37e75-128">Si noti troppo hello ID di correlazione.</span><span class="sxs-lookup"><span data-stu-id="37e75-128">Notice too hello correlation IDs.</span></span> <span data-ttu-id="37e75-129">Questo valore può essere utile quando si lavora con il supporto tecnico tootroubleshoot una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37e75-129">This value can be helpful when working with technical support tootroubleshoot a deployment.</span></span>
   
    ![vedere eventi](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="37e75-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="37e75-131">PowerShell</span></span>
1. <span data-ttu-id="37e75-132">tooget hello stato generale di una distribuzione, utilizzare hello **Get AzureRmResourceGroupDeployment** comando.</span><span class="sxs-lookup"><span data-stu-id="37e75-132">tooget hello overall status of a deployment, use hello **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="37e75-133">In alternativa, è possibile filtrare i risultati hello solo le distribuzioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="37e75-133">Or, you can filter hello results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="37e75-134">Ogni distribuzione include più operazioni,</span><span class="sxs-lookup"><span data-stu-id="37e75-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="37e75-135">Ogni operazione rappresenta un passaggio nel processo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-135">Each operation represents a step in hello deployment process.</span></span> <span data-ttu-id="37e75-136">toodiscover che cos'è verificato un errore con una distribuzione, è necessario in genere toosee dettagli sulle operazioni di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-136">toodiscover what went wrong with a deployment, you usually need toosee details about hello deployment operations.</span></span> <span data-ttu-id="37e75-137">È possibile visualizzare lo stato di hello delle operazioni di hello con **Get AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="37e75-137">You can see hello status of hello operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="37e75-138">Che restituisce più operazioni con ciascuno di essi in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="37e75-138">Which returns multiple operations with each one in hello following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="37e75-139">tooget ulteriori dettagli sulle operazioni non riuscite, recuperare le proprietà di hello per le operazioni con **Failed** stato.</span><span class="sxs-lookup"><span data-stu-id="37e75-139">tooget more details about failed operations, retrieve hello properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="37e75-140">Restituisce che tutti hello operazioni non riuscite con ognuno di essi in hello seguente formato:</span><span class="sxs-lookup"><span data-stu-id="37e75-140">Which returns all hello failed operations with each one in hello following format:</span></span>

  ```powershell
  provisioningOperation : Create
  provisioningState     : Failed
  timestamp             : 2016-06-14T21:54:55.1468068Z
  duration              : PT3.1449887S
  trackingId            : f4ed72f8-4203-43dc-958a-15d041e8c233
  serviceRequestId      : a426f689-5d5a-448d-a2f0-9784d14c900a
  statusCode            : BadRequest
  statusMessage         : @{error=}
  targetResource        : @{id=/subscriptions/{guid}/resourceGroups/ExampleGroup/providers/
                          Microsoft.Network/publicIPAddresses/myPublicIP;
                          resourceType=Microsoft.Network/publicIPAddresses; resourceName=myPublicIP}
  ```

    <span data-ttu-id="37e75-141">Si noti serviceRequestId hello e hello ID traccia per l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-141">Note hello serviceRequestId and hello trackingId for hello operation.</span></span> <span data-ttu-id="37e75-142">Hello serviceRequestId può essere utile quando si lavora con il supporto tecnico tootroubleshoot una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37e75-142">hello serviceRequestId can be helpful when working with technical support tootroubleshoot a deployment.</span></span> <span data-ttu-id="37e75-143">Si utilizzerà l'ID traccia hello in hello toofocus passaggio al successivo in una particolare operazione.</span><span class="sxs-lookup"><span data-stu-id="37e75-143">You will use hello trackingId in hello next step toofocus on a particular operation.</span></span>
4. <span data-ttu-id="37e75-144">messaggio di stato tooget hello di una determinata operazione non riuscita, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="37e75-144">tooget hello status message of a particular failed operation, use hello following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="37e75-145">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="37e75-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="37e75-146">Ogni operazione di distribuzione in Azure include il contenuto della richiesta e della risposta.</span><span class="sxs-lookup"><span data-stu-id="37e75-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="37e75-147">contenuto della richiesta Hello è ciò che è stata inviata tooAzure durante la distribuzione (ad esempio, creare una macchina virtuale, disco del sistema operativo e altre risorse).</span><span class="sxs-lookup"><span data-stu-id="37e75-147">hello request content is what you sent tooAzure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="37e75-148">contenuto della risposta Hello è ciò che Azure inviati nuovamente la richiesta di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37e75-148">hello response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="37e75-149">Durante la distribuzione, è possibile utilizzare **DeploymentDebugLogLevel** toospecify parametro che hello richiesta e/o risposta vengono mantenute nel registro hello.</span><span class="sxs-lookup"><span data-stu-id="37e75-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter toospecify that hello request and/or response are retained in hello log.</span></span> 

  <span data-ttu-id="37e75-150">Ottenere tali informazioni dal Registro di hello e salvarlo localmente utilizzando i seguenti comandi PowerShell hello:</span><span class="sxs-lookup"><span data-stu-id="37e75-150">You get that information from hello log, and save it locally by using hello following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="37e75-151">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="37e75-151">Azure CLI</span></span>

1. <span data-ttu-id="37e75-152">Ottenere hello stato generale di una distribuzione con hello **Mostra la distribuzione di azure gruppo** comando.</span><span class="sxs-lookup"><span data-stu-id="37e75-152">Get hello overall status of a deployment with hello **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="37e75-153">Uno dei valori restituito hello è hello **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="37e75-153">One of hello returned values is hello **correlationId**.</span></span> <span data-ttu-id="37e75-154">Questo valore viene utilizzato tootrack eventi correlati e può essere utile quando utilizzato con il supporto tecnico tootroubleshoot una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37e75-154">This value is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="37e75-155">operazioni di hello toosee per una distribuzione, utilizzare:</span><span class="sxs-lookup"><span data-stu-id="37e75-155">toosee hello operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="37e75-156">REST</span><span class="sxs-lookup"><span data-stu-id="37e75-156">REST</span></span>

1. <span data-ttu-id="37e75-157">Ottenere informazioni su una distribuzione con hello [ottenere informazioni su una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operazione.</span><span class="sxs-lookup"><span data-stu-id="37e75-157">Get information about a deployment with hello [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="37e75-158">In risposta hello, notare in particolare hello **provisioningState**, **correlationId**, e **errore** elementi.</span><span class="sxs-lookup"><span data-stu-id="37e75-158">In hello response, note in particular hello **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="37e75-159">Hello **correlationId** utilizzato tootrack eventi correlati e può essere utile quando utilizzato con il supporto tecnico tootroubleshoot una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37e75-159">hello **correlationId** is used tootrack related events, and can be helpful when working with technical support tootroubleshoot a deployment.</span></span>

  ```json
  { 
    ...
    "properties": {
      "provisioningState":"Failed",
      "correlationId":"d5062e45-6e9f-4fd3-a0a0-6b2c56b15757",
      ...
      "error":{
        "code":"DeploymentFailed","message":"At least one resource deployment operation failed. Please list deployment operations for details. Please see http://aka.ms/arm-debug for usage details.",
        "details":[{"code":"Conflict","message":"{\r\n  \"error\": {\r\n    \"message\": \"Conflict\",\r\n    \"code\": \"Conflict\"\r\n  }\r\n}"}]
      }  
    }
  }
  ```

2. <span data-ttu-id="37e75-160">Ottenere informazioni sulle operazioni di distribuzione con hello [elencare tutte le operazioni di distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operazione.</span><span class="sxs-lookup"><span data-stu-id="37e75-160">Get information about deployment operations with hello [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="37e75-161">risposta Hello include informazioni di richiesta e/o risposta in base a quanto specificato in hello **debugSetting** proprietà durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="37e75-161">hello response includes request and/or response information based on what you specified in hello **debugSetting** property during deployment.</span></span>

  ```json
  {
    ...
    "properties": 
    {
      ...
      "request":{
        "content":{
          "location":"West US",
          "properties":{
            "accountType": "Standard_LRS"
          }
        }
      },
      "response":{
        "content":{
          "error":{
            "message":"Conflict","code":"Conflict"
          }
        }
      }
    }
  }
  ```


## <a name="next-steps"></a><span data-ttu-id="37e75-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="37e75-162">Next steps</span></span>
* <span data-ttu-id="37e75-163">Per informazioni sulla risoluzione degli errori di distribuzione specifici, vedere [risolvere gli errori comuni durante la distribuzione di risorse tooAzure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="37e75-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources tooAzure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="37e75-164">toolearn sull'utilizzo di attività hello registri toomonitor altri tipi di azioni, vedere [Visualizza attività registra toomanage Azure risorse](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="37e75-164">toolearn about using hello activity logs toomonitor other types of actions, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="37e75-165">vedere la distribuzione prima dell'esecuzione, toovalidate [distribuire un gruppo di risorse con il modello di gestione risorse di Azure](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="37e75-165">toovalidate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

