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
# <a name="create-an-iot-hub-using-hello-resource-provider-rest-api-net"></a><span data-ttu-id="b9637-103">Creazione di un hub IoT utilizzando il provider di risorse hello API REST (.NET)</span><span class="sxs-lookup"><span data-stu-id="b9637-103">Create an IoT hub using hello resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="b9637-104">È possibile utilizzare hello [il provider di risorse IoT Hub API REST] [ lnk-rest-api] toocreate e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="b9637-104">You can use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b9637-105">Questa esercitazione viene illustrato come toouse hello toocreate API REST del provider di IoT Hub risorsa un hub IoT da un programma c#.</span><span class="sxs-lookup"><span data-stu-id="b9637-105">This tutorial shows you how toouse hello IoT Hub resource provider REST API toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="b9637-106">Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b9637-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b9637-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="b9637-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="b9637-108">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9637-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="b9637-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b9637-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b9637-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b9637-110">An active Azure account.</span></span> <br/><span data-ttu-id="b9637-111">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b9637-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b9637-112">[Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b9637-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="b9637-113">Preparare il progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b9637-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="b9637-114">In Visual Studio, creare un progetto di Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="b9637-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b9637-115">Progetto hello nome **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="b9637-115">Name hello project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="b9637-116">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b9637-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="b9637-117">Controllare in Gestione pacchetti NuGet **versione provvisoria di inclusione**e in hello **Sfoglia** Cerca pagina **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="b9637-117">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="b9637-118">Selezionare il pacchetto di hello, fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenze hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="b9637-118">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="b9637-119">In Gestione pacchetti NuGet cercare **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="b9637-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="b9637-120">Fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenza hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="b9637-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="b9637-121">In Program.cs, sostituire hello **utilizzando** istruzioni con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b9637-121">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

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

6. <span data-ttu-id="b9637-122">In Program.cs aggiungere hello seguenti variabili statiche, sostituendo i valori segnaposto hello.</span><span class="sxs-lookup"><span data-stu-id="b9637-122">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="b9637-123">Nella parte precedente di questa esercitazione si è preso nota di **ApplicationId**, **SubscriptionId**, **TenantId** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="b9637-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="b9637-124">**Nome del gruppo di risorse** hello nome del gruppo di risorse hello è utilizzare quando si crea l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="b9637-124">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="b9637-125">È possibile usare un gruppo di risorse preesistente o nuovo.</span><span class="sxs-lookup"><span data-stu-id="b9637-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="b9637-126">**Nome dell'IoT Hub** nome hello di hello IoT Hub create, ad esempio **MyIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b9637-126">**IoT Hub name** is hello name of hello IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="b9637-127">nome Hello dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="b9637-127">hello name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="b9637-128">**Nome della distribuzione** è un nome per la distribuzione di hello, ad esempio **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="b9637-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-hello-resource-provider-rest-api-toocreate-an-iot-hub"></a><span data-ttu-id="b9637-129">Utilizzare i provider di risorse hello, toocreate API REST un hub IoT</span><span class="sxs-lookup"><span data-stu-id="b9637-129">Use hello resource provider REST API toocreate an IoT hub</span></span>

<span data-ttu-id="b9637-130">Hello utilizzare [il provider di risorse IoT Hub API REST] [ lnk-rest-api] toocreate un hub IoT nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b9637-130">Use hello [IoT Hub resource provider REST API][lnk-rest-api] toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="b9637-131">È possibile utilizzare anche hello resource provider API REST toomake modifiche tooan IoT hub esistente.</span><span class="sxs-lookup"><span data-stu-id="b9637-131">You can also use hello resource provider REST API toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="b9637-132">Aggiungere hello tooProgram.cs metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="b9637-132">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="b9637-133">Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo.</span><span class="sxs-lookup"><span data-stu-id="b9637-133">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="b9637-134">Questo codice crea un **HttpClient** oggetto con il token di autenticazione hello nelle intestazioni hello:</span><span class="sxs-lookup"><span data-stu-id="b9637-134">This code creates an **HttpClient** object with hello authentication token in hello headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="b9637-135">Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo.</span><span class="sxs-lookup"><span data-stu-id="b9637-135">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="b9637-136">Questo codice descrive hello IoT hub toocreate e genera una rappresentazione JSON.</span><span class="sxs-lookup"><span data-stu-id="b9637-136">This code describes hello IoT hub toocreate and generates a JSON representation.</span></span> <span data-ttu-id="b9637-137">Per l'elenco corrente di hello di percorsi che supportano IoT Hub vedere [stato Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="b9637-137">For hello current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="b9637-138">Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo.</span><span class="sxs-lookup"><span data-stu-id="b9637-138">Add hello following code toohello **CreateIoTHub** method.</span></span> <span data-ttu-id="b9637-139">Questo codice invia hello REST richiesta tooAzure.</span><span class="sxs-lookup"><span data-stu-id="b9637-139">This code submits hello REST request tooAzure.</span></span> <span data-ttu-id="b9637-140">codice Hello quindi controlla la risposta hello e recupera l'URL di hello è possibile utilizzare toomonitor hello stato dell'attività di distribuzione hello:</span><span class="sxs-lookup"><span data-stu-id="b9637-140">hello code then checks hello response and retrieves hello URL you can use toomonitor hello state of hello deployment task:</span></span>

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

5. <span data-ttu-id="b9637-141">Aggiungere hello successivo toohello codice alla fine di hello **CreateIoTHub** metodo.</span><span class="sxs-lookup"><span data-stu-id="b9637-141">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="b9637-142">Questo codice Usa hello **asyncStatusUri** hello toowait di passaggio precedente per hello distribuzione toocomplete recuperare l'indirizzo:</span><span class="sxs-lookup"><span data-stu-id="b9637-142">This code uses hello **asyncStatusUri** address retrieved in hello previous step toowait for hello deployment toocomplete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="b9637-143">Aggiungere hello successivo toohello codice alla fine di hello **CreateIoTHub** metodo.</span><span class="sxs-lookup"><span data-stu-id="b9637-143">Add hello following code toohello end of hello **CreateIoTHub** method.</span></span> <span data-ttu-id="b9637-144">Questo codice recupera le chiavi di hello di hello hub IoT è stato creato e li visualizza toohello console:</span><span class="sxs-lookup"><span data-stu-id="b9637-144">This code retrieves hello keys of hello IoT hub you created and prints them toohello console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="b9637-145">Applicazione hello completo e di esecuzione</span><span class="sxs-lookup"><span data-stu-id="b9637-145">Complete and run hello application</span></span>

<span data-ttu-id="b9637-146">È ora possibile completare un'applicazione hello dal chiamante hello **CreateIoTHub** metodo prima di generare ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="b9637-146">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="b9637-147">Aggiungere hello successivo toohello codice alla fine di hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="b9637-147">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="b9637-148">Fare clic su **Compila** e quindi su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="b9637-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="b9637-149">Correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="b9637-149">Correct any errors.</span></span>

3. <span data-ttu-id="b9637-150">Fare clic su **Debug** e quindi **Avvia debug** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b9637-150">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="b9637-151">Potrebbe richiedere alcuni minuti per hello toorun di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b9637-151">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="b9637-152">tooverify che l'applicazione aggiunta hello nuovo hub IoT, visitare hello [portale di Azure] [ lnk-azure-portal] e visualizzare l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="b9637-152">tooverify that your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="b9637-153">In alternativa, utilizzare hello **Get-AzureRmResource** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9637-153">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="b9637-154">Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="b9637-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="b9637-155">Al termine, è possibile eliminare l'hub IoT hello tramite hello [portale di Azure] [ lnk-azure-portal] o utilizzando hello **Remove-AzureRmResource** cmdlet PowerShell dopo aver terminato.</span><span class="sxs-lookup"><span data-stu-id="b9637-155">When you are finished, you can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9637-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9637-156">Next steps</span></span>
<span data-ttu-id="b9637-157">Dopo aver distribuito un hub IoT utilizzando il provider di risorse hello API REST, è opportuno tooexplore ulteriormente:</span><span class="sxs-lookup"><span data-stu-id="b9637-157">Now you have deployed an IoT hub using hello resource provider REST API, you may want tooexplore further:</span></span>

* <span data-ttu-id="b9637-158">Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="b9637-158">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="b9637-159">Lettura [Panoramica di gestione risorse di Azure] [ lnk-azure-rm-overview] toolearn ulteriori informazioni sulla funzionalità hello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9637-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="b9637-160">toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="b9637-160">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="b9637-161">[Introduzione tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b9637-161">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b9637-162">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="b9637-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b9637-163">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="b9637-163">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b9637-164">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b9637-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
