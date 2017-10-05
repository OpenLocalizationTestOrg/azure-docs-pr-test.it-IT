---
title: Creare un hub IoT di Azure con l'API REST del provider di risorse | Documentazione Microsoft
description: Come usare l'API REST del provider di risorse per creare un hub IoT.
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
ms.openlocfilehash: e443259507aacbefca141be4c9c1688ab19bf6ec
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-iot-hub-using-the-resource-provider-rest-api-net"></a><span data-ttu-id="cbe4a-103">Creare un hub IoT con l'API REST del provider di risorse (.NET)</span><span class="sxs-lookup"><span data-stu-id="cbe4a-103">Create an IoT hub using the resource provider REST API (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="cbe4a-104">È possibile usare l'[API REST del provider di risorse dell'hub IoT][lnk-rest-api] per creare e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-104">You can use the [IoT Hub resource provider REST API][lnk-rest-api] to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="cbe4a-105">In questa esercitazione viene illustrato come usare l'API REST del provider di risorse hub IoT per creare un hub IoT da un programma C#.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-105">This tutorial shows you how to use the IoT Hub resource provider REST API to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="cbe4a-106">Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="cbe4a-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="cbe4a-107">In questo articolo viene illustrato l'uso del modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="cbe4a-108">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="cbe4a-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="cbe4a-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-110">An active Azure account.</span></span> <br/><span data-ttu-id="cbe4a-111">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="cbe4a-112">[Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-112">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="cbe4a-113">Preparare il progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cbe4a-113">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="cbe4a-114">In Visual Studio creare un progetto desktop classico di Windows Visual C# usando il modello di progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-114">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="cbe4a-115">Denominare il progetto **CreateIoTHubREST**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-115">Name the project **CreateIoTHubREST**.</span></span>

2. <span data-ttu-id="cbe4a-116">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-116">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="cbe4a-117">In Gestione pacchetti NuGet selezionare **Includi versione preliminare** e nella pagina **Sfoglia** cercare **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-117">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="cbe4a-118">Selezionare il pacchetto, fare clic su **Installa**, in **Rivedi modifiche** fare clic su **OK**, quindi fare clic su **I Accept** (Accetto) per accettare le licenze.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-118">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="cbe4a-119">In Gestione pacchetti NuGet cercare **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-119">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="cbe4a-120">Fare clic su **Installa**, in **Rivedi modifiche** fare clic su **OK**, quindi fare clic su **I Accept** (Accetto) per accettare la licenza.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-120">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="cbe4a-121">In Program.cs sostituire le istruzioni **using** esistenti con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-121">In Program.cs, replace the existing **using** statements with the following code:</span></span>

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

6. <span data-ttu-id="cbe4a-122">In Program.cs aggiungere le seguenti variabili statiche sostituendo i valori dei segnaposto.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-122">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="cbe4a-123">Nella parte precedente di questa esercitazione si è preso nota di **ApplicationId**, **SubscriptionId**, **TenantId** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-123">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="cbe4a-124">**Nome gruppo di risorse** è il nome del gruppo di risorse che viene usato quando si crea l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-124">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="cbe4a-125">È possibile usare un gruppo di risorse preesistente o nuovo.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-125">You can use a pre-existing or a new resource group.</span></span> <span data-ttu-id="cbe4a-126">**Nome hub IoT** è il nome dell'hub IoT creato, ad esempio **MioHubIoT**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-126">**IoT Hub name** is the name of the IoT Hub you create, such as **MyIoTHub**.</span></span> <span data-ttu-id="cbe4a-127">Il nome dell'hub IoT deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-127">The name of your IoT hub must be globally unique.</span></span> <span data-ttu-id="cbe4a-128">**Nome distribuzione** è un nome per la distribuzione, ad esempio **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="use-the-resource-provider-rest-api-to-create-an-iot-hub"></a><span data-ttu-id="cbe4a-129">Usare l'API REST del provider di risorse per creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="cbe4a-129">Use the resource provider REST API to create an IoT hub</span></span>

<span data-ttu-id="cbe4a-130">Usare l'[API REST del provider di risorse dell'hub IoT][lnk-rest-api] per creare un hub IoT nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-130">Use the [IoT Hub resource provider REST API][lnk-rest-api] to create an IoT hub in your resource group.</span></span> <span data-ttu-id="cbe4a-131">È possibile usare l'API REST del provider di risorse anche per apportare modifiche a un hub IoT esistente.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-131">You can also use the resource provider REST API to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="cbe4a-132">Aggiungere il metodo seguente a Program.cs:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-132">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(string token)
    {

    }
    ```

2. <span data-ttu-id="cbe4a-133">Aggiungere il codice seguente al metodo **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-133">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="cbe4a-134">Questo codice crea un oggetto **HttpClient** con il token di autenticazione nelle intestazioni:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-134">This code creates an **HttpClient** object with the authentication token in the headers:</span></span>

    ```csharp
    HttpClient client = new HttpClient();
    client.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", token);
    ```

3. <span data-ttu-id="cbe4a-135">Aggiungere il codice seguente al metodo **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-135">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="cbe4a-136">Questo codice descrive l'hub IoT per creare e genera una rappresentazione JSON.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-136">This code describes the IoT hub to create and generates a JSON representation.</span></span> <span data-ttu-id="cbe4a-137">Per un elenco aggiornato delle località in cui è supportato l'hub IoT, vedere lo [Stato di Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-137">For the current list of locations that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

4. <span data-ttu-id="cbe4a-138">Aggiungere il codice seguente al metodo **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-138">Add the following code to the **CreateIoTHub** method.</span></span> <span data-ttu-id="cbe4a-139">Questo codice invia la richiesta REST ad Azure.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-139">This code submits the REST request to Azure.</span></span> <span data-ttu-id="cbe4a-140">Il codice verifica quindi la risposta e recupera l'URL da usare per monitorare lo stato dell'attività di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-140">The code then checks the response and retrieves the URL you can use to monitor the state of the deployment task:</span></span>

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

5. <span data-ttu-id="cbe4a-141">Alla fine del metodo **CreateIoTHub** aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-141">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="cbe4a-142">Questo codice usa l'indirizzo **asyncStatusUri** recuperato nel passaggio precedente per attendere il completamento della distribuzione:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-142">This code uses the **asyncStatusUri** address retrieved in the previous step to wait for the deployment to complete:</span></span>

    ```csharp
    string body;
    do
    {
      Thread.Sleep(10000);
      HttpResponseMessage deploymentstatus = client.GetAsync(asyncStatusUri).Result;
      body = deploymentstatus.Content.ReadAsStringAsync().Result;
    } while (body == "{\"status\":\"Running\"}");
    ```

6. <span data-ttu-id="cbe4a-143">Alla fine del metodo **CreateIoTHub** aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-143">Add the following code to the end of the **CreateIoTHub** method.</span></span> <span data-ttu-id="cbe4a-144">Questo codice recupera le chiavi dell'hub IoT creato e le visualizza nella console:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-144">This code retrieves the keys of the IoT hub you created and prints them to the console:</span></span>

    ```csharp
    var listKeysUri = string.Format("https://management.azure.com/subscriptions/{0}/resourceGroups/{1}/providers/Microsoft.Devices/IotHubs/{2}/IoTHubKeys/listkeys?api-version=2016-02-03", subscriptionId, rgName, iotHubName);
    var keysresults = client.PostAsync(listKeysUri, null).Result;

    Console.WriteLine("Keys: {0}", keysresults.Content.ReadAsStringAsync().Result);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="cbe4a-145">Compilare ed eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="cbe4a-145">Complete and run the application</span></span>

<span data-ttu-id="cbe4a-146">È ora possibile completare l'applicazione chiamando il metodo **CreateIoTHub** prima di compilarla ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-146">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="cbe4a-147">Alla fine del metodo **Main** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-147">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(token.AccessToken);
    Console.ReadLine();
    ```

2. <span data-ttu-id="cbe4a-148">Fare clic su **Compila** e quindi su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-148">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="cbe4a-149">Correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-149">Correct any errors.</span></span>

3. <span data-ttu-id="cbe4a-150">Fare clic su **Debug** e quindi su **Avvia debug** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-150">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="cbe4a-151">Potrebbero occorrere alcuni minuti per l'esecuzione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-151">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="cbe4a-152">Per verificare che l'applicazione abbia aggiunto il nuovo hub IoT, visitare il [portale di Azure][lnk-azure-portal] e visualizzare l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-152">To verify that your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="cbe4a-153">In alternativa, usare il cmdlet di PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-153">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="cbe4a-154">Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-154">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="cbe4a-155">Al termine è possibile eliminare l'hub IoT tramite il [portale di Azure][lnk-azure-portal] o usando il cmdlet di PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="cbe4a-155">When you are finished, you can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cbe4a-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cbe4a-156">Next steps</span></span>
<span data-ttu-id="cbe4a-157">Dopo aver distribuito un hub IoT mediante l'API REST del provider di risorse, può essere opportuno approfondire gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-157">Now you have deployed an IoT hub using the resource provider REST API, you may want to explore further:</span></span>

* <span data-ttu-id="cbe4a-158">Informazioni sulle funzionalità dell'[API REST del provider di risorse dell'hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="cbe4a-158">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="cbe4a-159">Per altre informazioni sulle funzionalità di Azure Resource Manager, vedere la [Panoramica di Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="cbe4a-159">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="cbe4a-160">Per altre informazioni sulle attività di sviluppo per l'hub IoT, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-160">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="cbe4a-161">[Introduzione a C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="cbe4a-161">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="cbe4a-162">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="cbe4a-162">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="cbe4a-163">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="cbe4a-163">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="cbe4a-164">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="cbe4a-164">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
