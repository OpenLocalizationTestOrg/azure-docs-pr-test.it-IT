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
# <a name="view-deployment-operations-with-azure-resource-manager"></a>Visualizzare le operazioni di distribuzione con Azure Resource Manager


È possibile visualizzare le operazioni di hello per una distribuzione tramite il portale di Azure hello. Potrebbe essere più interessati a visualizzare operazioni hello quando si riceve un errore durante la distribuzione in modo da questo articolo è incentrato sulle operazioni che non sono stato di visualizzazione. portale Hello fornisce un'interfaccia che consente gli errori di tooeasily trova hello e determinare potenziali correzioni.

[!INCLUDE [resource-manager-troubleshoot-introduction](../../includes/resource-manager-troubleshoot-introduction.md)]

## <a name="portal"></a>di Microsoft Azure
operazioni di distribuzione hello toosee, utilizzare hello alla procedura seguente:

1. Per gruppo di risorse hello coinvolto nella distribuzione di hello, notare stato hello dell'ultima distribuzione hello. È possibile selezionare questo tooget stato ulteriori dettagli.
   
    ![Stato della distribuzione](./media/resource-manager-deployment-operations/deployment-status.png)
2. Vedrai cronologia distribuzione hello. Selezionare la distribuzione di hello che non è riuscita.
   
    ![Stato della distribuzione](./media/resource-manager-deployment-operations/select-deployment.png)
3. Selezionare toosee collegamento hello una descrizione del motivo hello distribuzione non riuscita. Nella seguente figura hello record DNS hello non è univoco.  
   
    ![visualizzare la distribuzione non riuscita](./media/resource-manager-deployment-operations/view-error.png)
   
    Questo messaggio di errore dovrebbe essere sufficiente per la risoluzione dei problemi toobegin. Tuttavia, se sono necessarie ulteriori informazioni sulle attività siano state completate, è possibile visualizzare le operazioni di hello come illustrato nell'hello alla procedura seguente.
4. È possibile visualizzare tutte le operazioni di distribuzione hello in hello **distribuzione** blade. Selezionare qualsiasi toosee operazione ulteriori dettagli.
   
    ![visualizzare operazioni](./media/resource-manager-deployment-operations/view-operations.png)
   
    In questo caso, vedrai che hello account di archiviazione, rete virtuale e set di disponibilità sono stati creati. indirizzo IP pubblico Hello non è riuscita e non si è tentate di altre risorse.
5. È possibile visualizzare gli eventi per la distribuzione di hello selezionando **eventi**.
   
    ![visualizzare eventi](./media/resource-manager-deployment-operations/view-events.png)
6. Visualizzare tutti gli eventi di hello per la distribuzione di hello e selezionare uno per altri dettagli. Si noti troppo hello ID di correlazione. Questo valore può essere utile quando si lavora con il supporto tecnico tootroubleshoot una distribuzione.
   
    ![vedere eventi](./media/resource-manager-deployment-operations/see-all-events.png)

## <a name="powershell"></a>PowerShell
1. tooget hello stato generale di una distribuzione, utilizzare hello **Get AzureRmResourceGroupDeployment** comando. 

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup
  ```

   In alternativa, è possibile filtrare i risultati hello solo le distribuzioni non riuscite.

  ```powershell
  Get-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup | Where-Object ProvisioningState -eq Failed
  ```
   
2. Ogni distribuzione include più operazioni, Ogni operazione rappresenta un passaggio nel processo di distribuzione hello. toodiscover che cos'è verificato un errore con una distribuzione, è necessario in genere toosee dettagli sulle operazioni di distribuzione hello. È possibile visualizzare lo stato di hello delle operazioni di hello con **Get AzureRmResourceGroupDeploymentOperation**.

  ```powershell 
  Get-AzureRmResourceGroupDeploymentOperation -ResourceGroupName ExampleGroup -DeploymentName vmDeployment
  ```

    Che restituisce più operazioni con ciascuno di essi in hello seguente formato:

  ```powershell
  Id             : /subscriptions/{guid}/resourceGroups/ExampleGroup/providers/Microsoft.Resources/deployments/Microsoft.Template/operations/A3EB2DA598E0A780
  OperationId    : A3EB2DA598E0A780
  Properties     : @{provisioningOperation=Create; provisioningState=Succeeded; timestamp=2016-06-14T21:55:15.0156208Z;
                   duration=PT23.0227078S; trackingId=11d376e8-5d6d-4da8-847e-6f23c6443fbf;
                   serviceRequestId=0196828d-8559-4bf6-b6b8-8b9057cb0e23; statusCode=OK; targetResource=}
  PropertiesText : {duration:PT23.0227078S, provisioningOperation:Create, provisioningState:Succeeded,
                   serviceRequestId:0196828d-8559-4bf6-b6b8-8b9057cb0e23...}
  ```

3. tooget ulteriori dettagli sulle operazioni non riuscite, recuperare le proprietà di hello per le operazioni con **Failed** stato.

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object ProvisioningState -eq Failed
  ```
   
    Restituisce che tutti hello operazioni non riuscite con ognuno di essi in hello seguente formato:

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

    Si noti serviceRequestId hello e hello ID traccia per l'operazione di hello. Hello serviceRequestId può essere utile quando si lavora con il supporto tecnico tootroubleshoot una distribuzione. Si utilizzerà l'ID traccia hello in hello toofocus passaggio al successivo in una particolare operazione.
4. messaggio di stato tooget hello di una determinata operazione non riuscita, utilizzare hello comando seguente:

  ```powershell
  ((Get-AzureRmResourceGroupDeploymentOperation -DeploymentName Microsoft.Template -ResourceGroupName ExampleGroup).Properties | Where-Object trackingId -eq f4ed72f8-4203-43dc-958a-15d041e8c233).StatusMessage.error
  ```

    Che restituisce:

  ```powershell
  code           message                                                                        details
  ----           -------                                                                        -------
  DnsRecordInUse DNS record dns.westus.cloudapp.azure.com is already used by another public IP. {}
  ```
4. Ogni operazione di distribuzione in Azure include il contenuto della richiesta e della risposta. contenuto della richiesta Hello è ciò che è stata inviata tooAzure durante la distribuzione (ad esempio, creare una macchina virtuale, disco del sistema operativo e altre risorse). contenuto della risposta Hello è ciò che Azure inviati nuovamente la richiesta di distribuzione. Durante la distribuzione, è possibile utilizzare **DeploymentDebugLogLevel** toospecify parametro che hello richiesta e/o risposta vengono mantenute nel registro hello. 

  Ottenere tali informazioni dal Registro di hello e salvarlo localmente utilizzando i seguenti comandi PowerShell hello:

  ```powershell
  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.request | ConvertTo-Json |  Out-File -FilePath <PathToFile>

  (Get-AzureRmResourceGroupDeploymentOperation -DeploymentName "TestDeployment" -ResourceGroupName "Test-RG").Properties.response | ConvertTo-Json |  Out-File -FilePath <PathToFile>
  ```

## <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

1. Ottenere hello stato generale di una distribuzione con hello **Mostra la distribuzione di azure gruppo** comando.

  ```azurecli
  azure group deployment show --resource-group ExampleGroup --name ExampleDeployment --json
  ```
  
  Uno dei valori restituito hello è hello **correlationId**. Questo valore viene utilizzato tootrack eventi correlati e può essere utile quando utilizzato con il supporto tecnico tootroubleshoot una distribuzione.

  ```azurecli
  "properties": {
    "provisioningState": "Failed",
    "correlationId": "4002062a-a506-4b5e-aaba-4147036b771a",
  ```

2. operazioni di hello toosee per una distribuzione, utilizzare:

  ```azurecli
  azure group deployment operation list --resource-group ExampleGroup --name ExampleDeployment --json
  ```

## <a name="rest"></a>REST

1. Ottenere informazioni su una distribuzione con hello [ottenere informazioni su una distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_Get) operazione.

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}?api-version={api-version}
  ```

    In risposta hello, notare in particolare hello **provisioningState**, **correlationId**, e **errore** elementi. Hello **correlationId** utilizzato tootrack eventi correlati e può essere utile quando utilizzato con il supporto tecnico tootroubleshoot una distribuzione.

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

2. Ottenere informazioni sulle operazioni di distribuzione con hello [elencare tutte le operazioni di distribuzione modello](https://docs.microsoft.com/rest/api/resources/deployments#Deployments_List) operazione. 

  ```http
  GET https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group-name}/providers/microsoft.resources/deployments/{deployment-name}/operations?$skiptoken={skiptoken}&api-version={api-version}
  ```
   
    risposta Hello include informazioni di richiesta e/o risposta in base a quanto specificato in hello **debugSetting** proprietà durante la distribuzione.

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


## <a name="next-steps"></a>Passaggi successivi
* Per informazioni sulla risoluzione degli errori di distribuzione specifici, vedere [risolvere gli errori comuni durante la distribuzione di risorse tooAzure con Azure Resource Manager](resource-manager-common-deployment-errors.md).
* toolearn sull'utilizzo di attività hello registri toomonitor altri tipi di azioni, vedere [Visualizza attività registra toomanage Azure risorse](resource-group-audit.md).
* vedere la distribuzione prima dell'esecuzione, toovalidate [distribuire un gruppo di risorse con il modello di gestione risorse di Azure](resource-group-template-deploy.md).

