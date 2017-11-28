---
title: Operazioni di distribuzione con Azure Resource Manager | Documentazione Microsoft
description: Questo articolo descrive come visualizzare le operazioni di distribuzione di Azure Resource Manager tramite il portale, PowerShell, l'interfaccia della riga di comando di Azure e l'API REST.
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
ms.openlocfilehash: fb6b3b357fd1f66184e480115a9c863ba31ac193
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="view-deployment-operations-with-azure-resource-manager"></a><span data-ttu-id="d4719-103">Visualizzare le operazioni di distribuzione con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d4719-103">View deployment operations with Azure Resource Manager</span></span>


<span data-ttu-id="d4719-104">È possibile visualizzare le operazioni per una distribuzione tramite il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d4719-104">You can view the operations for a deployment through the Azure portal.</span></span> <span data-ttu-id="d4719-105">È possibile che si sia più interessati a visualizzare le operazioni quando si riceve un errore durante la distribuzione, quindi questo articolo è incentrato sulla visualizzazione delle operazioni non riuscite.</span><span class="sxs-lookup"><span data-stu-id="d4719-105">You may be most interested in viewing the operations when you have received an error during deployment so this article focuses on viewing operations that have failed.</span></span> <span data-ttu-id="d4719-106">Il portale offre un'interfaccia che consente di individuare facilmente gli errori e determinare le potenziali correzioni.</span><span class="sxs-lookup"><span data-stu-id="d4719-106">The portal provides an interface that enables you to easily find the errors and determine potential fixes.</span></span>

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a><span data-ttu-id="d4719-107">di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d4719-107">Portal</span></span>
<span data-ttu-id="d4719-108">Per visualizzare le operazioni di distribuzione, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="d4719-108">To see the deployment operations, use the following steps:</span></span>

1. <span data-ttu-id="d4719-109">Per il gruppo di risorse coinvolte nella distribuzione, si noti lo stato dell'ultima distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-109">For the resource group involved in the deployment, notice the status of the last deployment.</span></span> <span data-ttu-id="d4719-110">È possibile selezionare questo stato per ottenere altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="d4719-110">You can select this status to get more details.</span></span>
   
    ![Stato della distribuzione](./media/resource-manager-deployment-operations/deployment-status.png)
2. <span data-ttu-id="d4719-112">Viene visualizzata la cronologia di distribuzione recente.</span><span class="sxs-lookup"><span data-stu-id="d4719-112">You see the recent deployment history.</span></span> <span data-ttu-id="d4719-113">Selezionare la distribuzione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="d4719-113">Select the deployment that failed.</span></span>
   
    ![Stato della distribuzione](./media/resource-manager-deployment-operations/select-deployment.png)
3. <span data-ttu-id="d4719-115">Selezionare il collegamento per visualizzare una descrizione del motivo per cui la distribuzione non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="d4719-115">Select the link to see a description of why the deployment failed.</span></span> <span data-ttu-id="d4719-116">Nell'immagine seguente il record DNS non è univoco.</span><span class="sxs-lookup"><span data-stu-id="d4719-116">In the image below, the DNS record is not unique.</span></span>  
   
    ![visualizzare la distribuzione non riuscita](./media/resource-manager-deployment-operations/view-error.png)
   
    <span data-ttu-id="d4719-118">Questo messaggio di errore dovrebbe essere sufficiente per iniziare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="d4719-118">This error message should be enough for you to begin troubleshooting.</span></span> <span data-ttu-id="d4719-119">Tuttavia, se sono necessari altri dettagli sulle attività completate, è possibile visualizzare le operazioni, come illustrato nei passaggi seguenti.</span><span class="sxs-lookup"><span data-stu-id="d4719-119">However, if you need more details about which tasks were completed, you can view the operations as shown in the following steps.</span></span>
4. <span data-ttu-id="d4719-120">È possibile visualizzare tutte le operazioni di distribuzione nel pannello **Distribuzione** .</span><span class="sxs-lookup"><span data-stu-id="d4719-120">You can view all the deployment operations in the **Deployment** blade.</span></span> <span data-ttu-id="d4719-121">Selezionare un'operazione per visualizzare altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="d4719-121">Select any operation to see more details.</span></span>
   
    ![visualizzare operazioni](./media/resource-manager-deployment-operations/view-operations.png)
   
    <span data-ttu-id="d4719-123">In questo caso, si noterà che l'account di archiviazione, la rete virtuale e il set di disponibilità sono stati creati correttamente.</span><span class="sxs-lookup"><span data-stu-id="d4719-123">In this case, you see that the storage account, virtual network, and availability set were successfully created.</span></span> <span data-ttu-id="d4719-124">L'indirizzo IP pubblico non è riuscito e non si sono state tentate altre risorse.</span><span class="sxs-lookup"><span data-stu-id="d4719-124">The public IP address failed, and other resources were not attempted.</span></span>
5. <span data-ttu-id="d4719-125">È possibile visualizzare gli eventi relativi alla distribuzione selezionando **venti**.</span><span class="sxs-lookup"><span data-stu-id="d4719-125">You can view events for the deployment by selecting **Events**.</span></span>
   
    ![visualizzare eventi](./media/resource-manager-deployment-operations/view-events.png)
6. <span data-ttu-id="d4719-127">Visualizzare tutti gli eventi per la distribuzione e selezionarne una per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="d4719-127">You see all the events for the deployment and select any one for more details.</span></span> <span data-ttu-id="d4719-128">Si notino anche gli ID di correlazione.</span><span class="sxs-lookup"><span data-stu-id="d4719-128">Notice too the correlation IDs.</span></span> <span data-ttu-id="d4719-129">Questo valore può essere utile quando si interagisce con il supporto tecnico per risolvere i problemi relativi a una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-129">This value can be helpful when working with technical support to troubleshoot a deployment.</span></span>
   
    ![vedere eventi](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a><span data-ttu-id="d4719-131">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d4719-131">PowerShell</span></span>
1. <span data-ttu-id="d4719-132">Per ottenere lo stato complessivo di una distribuzione, usare il comando **Get-AzureRmResourceGroupDeployment** .</span><span class="sxs-lookup"><span data-stu-id="d4719-132">To get the overall status of a deployment, use the **Get-AzureRmResourceGroupDeployment** command.</span></span> 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   <span data-ttu-id="d4719-133">In alternativa, è possibile filtrare i risultati per visualizzare solo le distribuzioni con esito negativo.</span><span class="sxs-lookup"><span data-stu-id="d4719-133">Or, you can filter the results for only those deployments that have failed.</span></span>

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. <span data-ttu-id="d4719-134">Ogni distribuzione include più operazioni,</span><span class="sxs-lookup"><span data-stu-id="d4719-134">Each deployment includes multiple operations.</span></span> <span data-ttu-id="d4719-135">ognuna delle quali rappresenta un passaggio del processo di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-135">Each operation represents a step in the deployment process.</span></span> <span data-ttu-id="d4719-136">Per individuare eventuali problemi, solitamente è necessario visualizzare i dettagli relativi alle operazioni di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-136">To discover what went wrong with a deployment, you usually need to see details about the deployment operations.</span></span> <span data-ttu-id="d4719-137">Per visualizzare lo stato delle operazioni, usare il comando **Get-AzureRmResourceGroupDeploymentOperation**.</span><span class="sxs-lookup"><span data-stu-id="d4719-137">You can see the status of the operations with **Get-AzureRmResourceGroupDeploymentOperation**.</span></span>

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    <span data-ttu-id="d4719-138">Che restituisce più operazioni, ognuna nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="d4719-138">Which returns multiple operations with each one in the following format:</span></span>

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. <span data-ttu-id="d4719-139">Per ottenere altre informazioni sulle operazioni non riuscite, recuperare le proprietà per le operazioni con stato **Non riuscita** .</span><span class="sxs-lookup"><span data-stu-id="d4719-139">To get more details about failed operations, retrieve the properties for operations with **Failed** state.</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    <span data-ttu-id="d4719-140">Vengono restituite tutte le operazioni non riuscite, ognuna nel formato seguente:</span><span class="sxs-lookup"><span data-stu-id="d4719-140">Which returns all the failed operations with each one in the following format:</span></span>

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

    <span data-ttu-id="d4719-141">Si notino gli elementi serviceRequestId e trackingId per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="d4719-141">Note the serviceRequestId and the trackingId for the operation.</span></span> <span data-ttu-id="d4719-142">L'elemento serviceRequestId può essere utile quando si interagisce con il supporto tecnico per risolvere i problemi relativi a una distribuzione,</span><span class="sxs-lookup"><span data-stu-id="d4719-142">The serviceRequestId can be helpful when working with technical support to troubleshoot a deployment.</span></span> <span data-ttu-id="d4719-143">mentre l'elemento trackingId viene usato nel passaggio successivo per concentrarsi su una particolare operazione.</span><span class="sxs-lookup"><span data-stu-id="d4719-143">You will use the trackingId in the next step to focus on a particular operation.</span></span>
4. <span data-ttu-id="d4719-144">Per ottenere il messaggio di stato di un'operazione non riuscita particolare, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d4719-144">To get the status message of a particular failed operation, use the following command:</span></span>

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    <span data-ttu-id="d4719-145">Che restituisce:</span><span class="sxs-lookup"><span data-stu-id="d4719-145">Which returns:</span></span>

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. <span data-ttu-id="d4719-146">Ogni operazione di distribuzione in Azure include il contenuto della richiesta e della risposta.</span><span class="sxs-lookup"><span data-stu-id="d4719-146">Every deployment operation in Azure includes request and response content.</span></span> <span data-ttu-id="d4719-147">Il contenuto della richiesta corrisponde a quanto è stato inviato a Azure durante la distribuzione, ad esempio la richiesta di creare una macchina virtuale, un disco del sistema operativo e altre risorse.</span><span class="sxs-lookup"><span data-stu-id="d4719-147">The request content is what you sent to Azure during deployment (for example, create a VM, OS disk, and other resources).</span></span> <span data-ttu-id="d4719-148">Il contenuto della risposta è la risposta di Azure alla richiesta di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-148">The response content is what Azure sent back from your deployment request.</span></span> <span data-ttu-id="d4719-149">Durante la distribuzione è possibile usare il parametro **DeploymentDebugLogLevel** per specificare che la richiesta e/o la risposta vengono mantenute nel log.</span><span class="sxs-lookup"><span data-stu-id="d4719-149">During deployment, you can use **DeploymentDebugLogLevel** paramenter to specify that the request and/or response are retained in the log.</span></span> 

  <span data-ttu-id="d4719-150">Per ottenere tali informazioni dal log e salvarle in locale, usare i comandi PowerShell seguenti:</span><span class="sxs-lookup"><span data-stu-id="d4719-150">You get that information from the log, and save it locally by using the following PowerShell commands:</span></span>

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a><span data-ttu-id="d4719-151">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d4719-151">Azure CLI</span></span>

1. <span data-ttu-id="d4719-152">Per ottenere lo stato complessivo di una distribuzione, è possibile usare il comando **azure group deployment show** .</span><span class="sxs-lookup"><span data-stu-id="d4719-152">Get the overall status of a deployment with the **azure group deployment show** command.</span></span>

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  <span data-ttu-id="d4719-153">Uno dei calori restituiti è **correlationId**.</span><span class="sxs-lookup"><span data-stu-id="d4719-153">One of the returned values is the **correlationId**.</span></span> <span data-ttu-id="d4719-154">Tale valore viene usato per tenere traccia degli eventi correlati e può essere utile quando si interagisce con il supporto tecnico per risolvere i problema relativi a una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-154">This value is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. <span data-ttu-id="d4719-155">Per visualizzare le operazioni per una distribuzione, usare:</span><span class="sxs-lookup"><span data-stu-id="d4719-155">To see the operations for a deployment, use:</span></span>

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a><span data-ttu-id="d4719-156">REST</span><span class="sxs-lookup"><span data-stu-id="d4719-156">REST</span></span>

1. <span data-ttu-id="d4719-157">Ottenere informazioni su una distribuzione con l'operazione [Ottenere informazioni su una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get).</span><span class="sxs-lookup"><span data-stu-id="d4719-157">Get information about a deployment with the [Get information about a template deployment](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operation.</span></span>

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    <span data-ttu-id="d4719-158">Nella risposta si notino in particolare gli elementi **provisioningState**, **correlationId** ed **error**.</span><span class="sxs-lookup"><span data-stu-id="d4719-158">In the response, note in particular the **provisioningState**, **correlationId**, and **error** elements.</span></span> <span data-ttu-id="d4719-159">Il valore **correlationId** viene usato per tenere traccia degli eventi correlati e può essere utile quando si interagisce con il supporto tecnico per risolvere i problemi relativi a una distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-159">The **correlationId** is used to track related events, and can be helpful when working with technical support to troubleshoot a deployment.</span></span>

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

2. <span data-ttu-id="d4719-160">Ottenere informazioni sulle operazioni di distribuzione con l'operazione [Elencare tutte le operazioni di distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List).</span><span class="sxs-lookup"><span data-stu-id="d4719-160">Get information about deployment operations with the [List all template deployment operations](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operation.</span></span> 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    <span data-ttu-id="d4719-161">La risposta include la richiesta e/o le informazioni sulla risposta in base a quanto specificato nella proprietà **debugSetting** durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="d4719-161">The response includes request and/or response information based on what you specified in the **debugSetting** property during deployment.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="d4719-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d4719-162">Next steps</span></span>
* <span data-ttu-id="d4719-163">Per informazioni sulla risoluzione di errori di distribuzione specifici vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="d4719-163">For help with resolving particular deployment errors, see [Resolve common errors when deploying resources to Azure with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="d4719-164">Per altre informazioni sull'uso dei log attività per monitorare altri tipi di azioni, vedere [Visualizzare i log attività per gestire le risorse di Azure](resource-group-audit.md).</span><span class="sxs-lookup"><span data-stu-id="d4719-164">To learn about using the activity logs to monitor other types of actions, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>
* <span data-ttu-id="d4719-165">Per convalidare la distribuzione prima di eseguirla, vedere [Distribuire le risorse con i modelli di Azure Resource Manager e Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="d4719-165">To validate your deployment before executing it, see [Deploy a resource group with Azure Resource Manager template](resource-group-template-deploy.md).</span></span>

