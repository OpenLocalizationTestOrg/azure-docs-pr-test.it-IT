---
title: un hub IoT di Azure mediante aaaCreate hello API REST del provider di risorse | Documenti Microsoft
description: Come un IoT Hub toouse hello toocreate API REST del provider di risorse.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 52814ee5-bc10-4abe-9eb2-f8973096c2d8
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 98d240ccce47dec13a255bce28943b40f5354ecf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a>Creazione di un hub IoT utilizzando il provider di risorse hello API REST (.NET)

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

È possibile utilizzare hello [il provider di risorse IoT Hub API REST] [ lnk-rest-api] toocreate e gestire hub IoT di Azure a livello di codice. Questa esercitazione viene illustrato come toouse hello toocreate API REST del provider di IoT Hub risorsa un hub IoT da un programma c#.

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).  In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.

toocomplete questa esercitazione, è necessario hello seguenti:

* Visual Studio 2015 o Visual Studio 2017.
* Un account Azure attivo. <br/>Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.
* [Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a>Preparare il progetto di Visual Studio

1. In Visual Studio, creare un progetto di Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto. Progetto hello nome **CreateIoTHubREST**.

2. In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Gestisci pacchetti NuGet**.

3. Controllare in Gestione pacchetti NuGet **versione provvisoria di inclusione**e in hello **Sfoglia** Cerca pagina **Microsoft.Azure.Management.ResourceManager**. Selezionare il pacchetto di hello, fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenze hello tooaccept.

4. In Gestione pacchetti NuGet cercare **Microsoft.IdentityModel.Clients.ActiveDirectory**.  Fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenza hello tooaccept.

5. In Program.cs, sostituire hello **utilizzando** istruzioni con hello seguente codice:

    ```csharp
    using System;
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Text;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Newtonsoft.Json;
    using Microsoft.Rest;
    using System.Linq;
    using System.Threading;
    ```

6. In Program.cs aggiungere hello seguenti variabili statiche, sostituendo i valori segnaposto hello. Nella parte precedente di questa esercitazione si è preso nota di **ApplicationId**, **SubscriptionId**, **TenantId** e **Password**. **Nome del gruppo di risorse** hello nome del gruppo di risorse hello è utilizzare quando si crea l'hub IoT hello. È possibile usare un gruppo di risorse preesistente o nuovo. **Nome dell'IoT Hub** nome hello di hello IoT Hub create, ad esempio **MyIoTHub**. nome Hello dell'hub IoT deve essere globalmente univoco. **Nome della distribuzione** è un nome per la distribuzione di hello, ad esempio **Deployment_01**.

    ```csharp
    static string applicationId = "{Your ApplicationId}";
    static string subscriptionId = "{Your SubscriptionId}";
    static string tenantId = "{Your TenantId}";
    static string password = "{Your application Password}";

    static string rgName = "{Resource group name}";
    static string iotHubName = "{IoT Hub name including your initials}";
    ```
[!INCLUDE [iot-hub-pii-note-naming-hub](../../includes/iot-hub-pii-note-naming-hub.md)]

[!INCLUDE [iot-hub-get-access-token](../../includes/iot-hub-get-access-token.md)]

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a>Utilizzare i provider di risorse hello, toocreate API REST un hub IoT

Hello utilizzare [il provider di risorse IoT Hub API REST] [ lnk-rest-api] toocreate un hub IoT nel gruppo di risorse. È possibile utilizzare anche hello resource provider API REST toomake modifiche tooan IoT hub esistente.

1. Aggiungere hello tooProgram.cs metodo seguente:

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo. Questo codice crea un **HttpClient** oggetto con il token di autenticazione hello nelle intestazioni hello:

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo. Questo codice descrive hello IoT hub toocreate e genera una rappresentazione JSON. Per l'elenco corrente di hello di percorsi che supportano IoT Hub vedere [stato Azure][lnk-status]:

    ```csharp
    var description = new
    {
      name = iotHubName,
      location = "East US",
      sku = new
      {
        name = "S1",
        tier = "Standard",
        capacity = 1
      }
    };

    var json = JsonConvert.SerializeObject(description, Formatting.Indented);
    ```

4. Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo. Questo codice invia hello REST richiesta tooAzure. codice Hello quindi controlla la risposta hello e recupera l'URL di hello è possibile utilizzare toomonitor hello stato dell'attività di distribuzione hello:

    ```csharp
    var content = new StringContent(JsonConvert.SerializeObject(description), Encoding.UTF8, "application/json");
    var requestUri = string.Format("https://management.azure.com/subscriptions/{0}/resourcegroups/{1}/providers/Microsoft.devices/IotHubs/{2}?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var result = client.PutAsync(requestUri, content).Result;

    if (!result.IsSuccessStatusCode)
    {
      Console.WriteLine("Failed {0}", result.Content.ReadAsStringAsync().Result);
      return;
    }

    var asyncStatusUri = result.Headers.GetValues("Azure-AsyncOperation").First();
    ```

5. Aggiungere hello successivo toohello codice alla fine di hello **CreateIoTHub** metodo. Questo codice Usa hello **asyncStatusUri** hello toowait di passaggio precedente per hello distribuzione toocomplete recuperare l'indirizzo:

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. Aggiungere hello successivo toohello codice alla fine di hello **CreateIoTHub** metodo. Questo codice recupera le chiavi di hello di hello hub IoT è stato creato e li visualizza toohello console:

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a>Applicazione hello completo e di esecuzione

È ora possibile completare un'applicazione hello dal chiamante hello **CreateIoTHub** metodo prima di generare ed eseguirlo.

1. Aggiungere hello successivo toohello codice alla fine di hello **Main** metodo:

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. Fare clic su **Compila** e quindi su **Compila soluzione**. Correggere eventuali errori.

3. Fare clic su **Debug** e quindi **Avvia debug** toorun un'applicazione hello. Potrebbe richiedere alcuni minuti per hello toorun di distribuzione.

4. tooverify che l'applicazione aggiunta hello nuovo hub IoT, visitare hello [portale di Azure] [ lnk-azure-portal] e visualizzare l'elenco delle risorse. In alternativa, utilizzare hello **Get-AzureRmResource** cmdlet di PowerShell.

> [!NOTE]
> Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato. Al termine, è possibile eliminare l'hub IoT hello tramite hello [portale di Azure] [ lnk-azure-portal] o utilizzando hello **Remove-AzureRmResource** cmdlet PowerShell dopo aver terminato.

## <a name="next-steps"></a>Passaggi successivi
Dopo aver distribuito un hub IoT utilizzando il provider di risorse hello API REST, è opportuno tooexplore ulteriormente:

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

[lnk-c-sdk]: iot-hub-device-sdk-c-intro.md
[lnk-sdks]: iot-hub-devguide-sdks.md

[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
