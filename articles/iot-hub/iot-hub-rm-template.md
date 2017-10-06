---
title: un IoT Hub di Azure utilizzando un modello (.NET) aaaCreate | Documenti Microsoft
description: Come toouse un toocreate modello di gestione risorse di Azure un IoT Hub con un programma c#.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a447b40c-c728-487e-875d-db554db5adc3
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 6140deff3553701f994502fd4a60178f874e27cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a>Creare un hub IoT usando un modello di Azure Resource Manager (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

È possibile utilizzare Gestione risorse di Azure toocreate e gestire hub IoT di Azure a livello di codice. In questa esercitazione illustra come toouse un toocreate modello di gestione risorse di Azure un hub IoT da un programma c#.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. <br/>Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* Un [account di archiviazione di Azure][lnk-storage-account] in cui è possibile archiviare i file del modello di Azure Resource Manager.
* [Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Preparare il progetto di Visual Studio

1. In Visual Studio, creare un progetto di Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto. Progetto hello nome **CreateIoTHub**.

2. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Gestisci pacchetti NuGet**.

3. Controllare in Gestione pacchetti NuGet **versione provvisoria di inclusione**e in hello **Sfoglia** Cerca pagina **Microsoft.Azure.Management.ResourceManager**. Selezionare il pacchetto di hello, fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenze hello tooaccept.

4. In Gestione pacchetti NuGet cercare **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenza hello tooaccept.

5. In Program.cs, sostituire hello **utilizzando** istruzioni con hello seguente codice:

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. In Program.cs aggiungere hello seguenti variabili statiche, sostituendo i valori segnaposto hello. Nella parte precedente di questa esercitazione si è preso nota di **ApplicationId**, **SubscriptionId**, **TenantId** e **Password**. **Il nome dell'account di archiviazione di Azure** è il nome di hello di hello account di archiviazione di Azure in cui si archiviano i file di modello di gestione risorse di Azure. **Nome del gruppo di risorse** hello nome del gruppo di risorse hello è utilizzare quando si crea l'hub IoT hello. nome di Hello può essere un gruppo di risorse nuovo o esistente. **Nome della distribuzione** è un nome per la distribuzione di hello, ad esempio **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";
    static string storageAddress = "https://{Your storage account name}.blob.core.windows.net";
    static string rgName = "{Resource group name}";
    static string deploymentName = "{Deployment name}";
    ```

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="submit-a-template-toocreate-an-iot-hub"></a>Inviare un toocreate modello un hub IoT

Utilizzare un JSON modello e parametro file toocreate un hub IoT nel gruppo di risorse. È anche possibile utilizzare un Azure Resource Manager modello toomake modifiche tooan IoT hub esistente.

1. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi su **Aggiungi** e infine su **Nuovo elemento**. Aggiungere un file JSON denominato **template.json** tooyour progetto.

2. tooadd un standard toohello hub IoT **Stati Uniti orientali** regione, sostituire hello contenuto di **template.json** con hello seguente definizione di risorsa. Per l'elenco corrente di hello delle aree che supportano IoT Hub vedere [stato Azure][lnk-status]:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": {
          "type": "string"
        }
      },
      "resources": [
      {
        "apiVersion": "2016-02-03",
        "type": "Microsoft.Devices/IotHubs",
        "name": "[parameters('hubName')]",
        "location": "East US",
        "sku": {
          "name": "S1",
          "tier": "Standard",
          "capacity": 1
        },
        "properties": {
          "location": "East US"
        }
      }
      ],
      "outputs": {
        "hubKeys": {
          "value": "[listKeys(resourceId('Microsoft.Devices/IotHubs', parameters('hubName')), '2016-02-03')]",
          "type": "object"
        }
      }
    }
    ```

3. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi su **Aggiungi** e infine su **Nuovo elemento**. Aggiungere un file JSON denominato **parameters.json** tooyour progetto.

4. Sostituire il contenuto di hello di **parameters.json** con le seguenti informazioni di parametro che imposta, ad esempio un nome per l'hub IoT nuovo hello hello **{iniziali} mynewiothub**. nome dell'hub IoT Hello deve essere globalmente univoco, pertanto deve includere il nome o iniziali:

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "hubName": { "value": "mynewiothub" }
      }
    }
    ```
  [!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

5. In **Esplora Server**, connettersi tooyour sottoscrizione di Azure e l'archiviazione di Azure account creare un contenitore chiamato **modelli**. In hello **proprietà** pannello, hello set **accesso in lettura pubblico** le autorizzazioni per hello **modelli** contenitore troppo**Blob**.

6. In **Esplora Server**, fare clic su hello **modelli** contenitore e quindi fare clic su **Visualizza contenitore Blob**. Fare clic su hello **carica Blob** pulsante, selezionare due file hello, **parameters.json** e **templates.json**, quindi fare clic su **aprire** hello tooupload JSON file toohello **modelli** contenitore. URL di Hello di BLOB hello contenente i dati JSON hello sono:

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. Aggiungere hello tooProgram.cs metodo seguente:

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo toosubmit hello modello e parametro file toohello Gestione risorse di Azure:

    ```csharp
    var createResponse = client.Deployments.CreateOrUpdate(
        rgName,
        deploymentName,
        new Deployment()
        {
          Properties = new DeploymentProperties
          {
            Mode = DeploymentMode.Incremental,
            TemplateLink = new TemplateLink
            {
              Uri = storageAddress + "/templates/template.json"
            },
            ParametersLink = new ParametersLink
            {
              Uri = storageAddress + "/templates/parameters.json"
            }
          }
        });
    ```

9. Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo che visualizza lo stato di hello e le chiavi di hello per l'hub IoT hello nuovo:

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a>Applicazione hello completo e di esecuzione

È ora possibile completare un'applicazione hello dal chiamante hello **CreateIoTHub** metodo prima di generare ed eseguirlo.

1. Aggiungere hello successivo toohello codice alla fine di hello **Main** metodo:

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. Fare clic su **Compila** e quindi su **Compila soluzione**. Correggere eventuali errori.

3. Fare clic su **Debug** e quindi **Avvia debug** toorun un'applicazione hello. Potrebbe richiedere alcuni minuti per hello toorun di distribuzione.

4. l'applicazione aggiunta tooverify hello nuovo hub IoT, visitare hello [portale di Azure] [ lnk-azure-portal] e visualizzare l'elenco delle risorse. In alternativa, utilizzare hello **Get-AzureRmResource** cmdlet di PowerShell.

> [!NOTE]
> Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato. È possibile eliminare l'hub IoT hello tramite hello [portale di Azure] [ lnk-azure-portal] o utilizzando hello **Remove-AzureRmResource** cmdlet PowerShell dopo aver terminato.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver distribuito un hub IoT utilizzando un modello di gestione risorse di Azure con un programma c#, è opportuno tooexplore ulteriormente:

* Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].
* Lettura [Panoramica di gestione risorse di Azure] [ lnk-azure-rm-overview] toolearn ulteriori informazioni sulla funzionalità hello di gestione risorse di Azure.

toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:

* [Introduzione tooC SDK][lnk-c-sdk]
* [Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)

toofurther esplorare le funzionalità di hello di IoT Hub, vedere:

* [Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]

<!-- Links -->
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-azure-portal]: https://portal.azure.com/
[lnk-status]: https://azure.microsoft.com/status/
[lnk-powershell-install]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps
[lnk-rest-api]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-azure-rm-overview]: ../azure-resource-manager/resource-group-overview.md
[lnk-storage-account]:../storage/common/storage-create-storage-account.md

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
