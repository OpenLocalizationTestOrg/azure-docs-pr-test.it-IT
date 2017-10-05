---
title: Creare un hub IoT di Azure con un modello (.NET) | Documentazione Microsoft
description: Come usare un modello di Azure Resource Manager per creare un hub IoT con un programma C#.
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
ms.openlocfilehash: 0f197a28e0c51b06d0b47a03c29fe1fde0c6b78d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="b84fc-103">Creare un hub IoT usando un modello di Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="b84fc-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="b84fc-104">È possibile utilizzare Gestione risorse di Azure per creare e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="b84fc-104">You can use Azure Resource Manager to create and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="b84fc-105">In questa esercitazione viene mostrato come usare un modello di Azure Resource Manager per creare un hub IoT da un programma C#.</span><span class="sxs-lookup"><span data-stu-id="b84fc-105">This tutorial shows you how to use an Azure Resource Manager template to create an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="b84fc-106">Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="b84fc-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="b84fc-107">In questo articolo viene illustrato l'uso del modello di distribuzione Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b84fc-107">This article covers using the Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="b84fc-108">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b84fc-108">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b84fc-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="b84fc-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="b84fc-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="b84fc-110">An active Azure account.</span></span> <br/><span data-ttu-id="b84fc-111">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="b84fc-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="b84fc-112">Un [account di archiviazione di Azure][lnk-storage-account] in cui è possibile archiviare i file del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b84fc-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="b84fc-113">[Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b84fc-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="b84fc-114">Preparare il progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b84fc-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="b84fc-115">In Visual Studio creare un progetto desktop classico di Windows Visual C# usando il modello di progetto **App console (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="b84fc-116">Denominare il progetto **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-116">Name the project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="b84fc-117">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="b84fc-118">In Gestione pacchetti NuGet selezionare **Includi versione preliminare** e nella pagina **Sfoglia** cercare **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-118">In NuGet Package Manager, check **Include prerelease**, and on the **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="b84fc-119">Selezionare il pacchetto, fare clic su **Installa**, in **Rivedi modifiche** fare clic su **OK**, quindi fare clic su **I Accept** (Accetto) per accettare le licenze.</span><span class="sxs-lookup"><span data-stu-id="b84fc-119">Select the package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the licenses.</span></span>

4. <span data-ttu-id="b84fc-120">In Gestione pacchetti NuGet cercare **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="b84fc-121">Fare clic su **Installa**, in **Rivedi modifiche** fare clic su **OK**, quindi fare clic su **I Accept** (Accetto) per accettare la licenza.</span><span class="sxs-lookup"><span data-stu-id="b84fc-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** to accept the license.</span></span>

5. <span data-ttu-id="b84fc-122">In Program.cs sostituire le istruzioni **using** esistenti con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b84fc-122">In Program.cs, replace the existing **using** statements with the following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="b84fc-123">In Program.cs aggiungere le seguenti variabili statiche sostituendo i valori dei segnaposto.</span><span class="sxs-lookup"><span data-stu-id="b84fc-123">In Program.cs, add the following static variables replacing the placeholder values.</span></span> <span data-ttu-id="b84fc-124">Nella parte precedente di questa esercitazione si è preso nota di **ApplicationId**, **SubscriptionId**, **TenantId** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="b84fc-125">**Il nome dell'account di archiviazione di Azure** è il nome dell'account di archiviazione di Azure in cui vengono archiviati i file del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="b84fc-125">**Your Azure Storage account name** is the name of the Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="b84fc-126">**Nome gruppo di risorse** è il nome del gruppo di risorse che viene usato quando si crea l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="b84fc-126">**Resource group name** is the name of the resource group you use when you create the IoT hub.</span></span> <span data-ttu-id="b84fc-127">Può essere un gruppo di risorse preesistente o nuovo.</span><span class="sxs-lookup"><span data-stu-id="b84fc-127">The name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="b84fc-128">**Nome distribuzione** è un nome per la distribuzione, ad esempio **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-128">**Deployment name** is a name for the deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-to-create-an-iot-hub"></a><span data-ttu-id="b84fc-129">Inviare un modello per creare un hub IoT</span><span class="sxs-lookup"><span data-stu-id="b84fc-129">Submit a template to create an IoT hub</span></span>

<span data-ttu-id="b84fc-130">Usare un modello JSON e un file di parametri per creare un hub IoT nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="b84fc-130">Use a JSON template and parameter file to create an IoT hub in your resource group.</span></span> <span data-ttu-id="b84fc-131">È anche possibile usare un modello di Azure Resource Manager per apportare modifiche a un hub IoT esistente.</span><span class="sxs-lookup"><span data-stu-id="b84fc-131">You can also use an Azure Resource Manager template to make changes to an existing IoT hub.</span></span>

1. <span data-ttu-id="b84fc-132">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi su **Aggiungi** e infine su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="b84fc-133">Aggiungere un file JSON denominato **template.json** al progetto.</span><span class="sxs-lookup"><span data-stu-id="b84fc-133">Add a JSON file called **template.json** to your project.</span></span>

2. <span data-ttu-id="b84fc-134">Per aggiungere un hub IoT standard per l'area **Stati Uniti orientali**, sostituire il contenuto di **template.json** con la definizione di risorsa seguente.</span><span class="sxs-lookup"><span data-stu-id="b84fc-134">To add a standard IoT hub to the **East US** region, replace the contents of **template.json** with the following resource definition.</span></span> <span data-ttu-id="b84fc-135">Per un elenco aggiornato delle aree in cui è supportato l'hub IoT, vedere lo [Stato di Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="b84fc-135">For the current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="b84fc-136">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi su **Aggiungi** e infine su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="b84fc-137">Aggiungere un file JSON denominato **parameters.json** al progetto.</span><span class="sxs-lookup"><span data-stu-id="b84fc-137">Add a JSON file called **parameters.json** to your project.</span></span>

4. <span data-ttu-id="b84fc-138">Sostituire il contenuto di **parameters.json** con le informazioni di parametro seguenti che impostano il nome del nuovo hub IoT su **{iniziali utente}mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-138">Replace the contents of **parameters.json** with the following parameter information that sets a name for the new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="b84fc-139">Il nome dell'hub IoT deve essere globalmente univoco, quindi deve includere il nome o le iniziali dell'utente:</span><span class="sxs-lookup"><span data-stu-id="b84fc-139">The IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="b84fc-140">In **Esplora server** connettersi alla sottoscrizione di Azure e nell'account di archiviazione di Azure creare un contenitore denominato **templates**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-140">In **Server Explorer**, connect to your Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="b84fc-141">Nel pannello **Proprietà** impostare le autorizzazioni **Accesso in lettura pubblico** per il contenitore **templates** su **BLOB**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-141">In the **Properties** panel, set the **Public Read Access** permissions for the **templates** container to **Blob**.</span></span>

6. <span data-ttu-id="b84fc-142">In **Esplora server** fare clic con il pulsante destro del mouse sul contenitore **templates** e quindi fare clic su **Visualizza contenitore BLOB**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-142">In **Server Explorer**, right-click on the **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="b84fc-143">Fare clic sul pulsante **Carica BLOB**, selezionare i due file **parameters.json** e **templates.json** e quindi fare clic su **Apri** per caricare i file JSON nel contenitore **templates**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-143">Click the **Upload Blob** button, select the two files, **parameters.json** and **templates.json**, and then click **Open** to upload the JSON files to the **templates** container.</span></span> <span data-ttu-id="b84fc-144">Gli URL dei BLOB contenenti i dati JSON sono:</span><span class="sxs-lookup"><span data-stu-id="b84fc-144">The URLs of the blobs containing the JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="b84fc-145">Aggiungere il metodo seguente a Program.cs:</span><span class="sxs-lookup"><span data-stu-id="b84fc-145">Add the following method to Program.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="b84fc-146">Aggiungere il codice seguente al metodo **CreateIoTHub** per inviare i file di modello e di parametri a Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="b84fc-146">Add the following code to the **CreateIoTHub** method to submit the template and parameter files to the Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="b84fc-147">Aggiungere il codice seguente al metodo **CreateIoTHub** che visualizza lo stato e le chiavi del nuovo hub IoT:</span><span class="sxs-lookup"><span data-stu-id="b84fc-147">Add the following code to the **CreateIoTHub** method that displays the status and the keys for the new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed to create iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-the-application"></a><span data-ttu-id="b84fc-148">Compilare ed eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="b84fc-148">Complete and run the application</span></span>

<span data-ttu-id="b84fc-149">È ora possibile completare l'applicazione chiamando il metodo **CreateIoTHub** prima di compilarla ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="b84fc-149">You can now complete the application by calling the **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="b84fc-150">Alla fine del metodo **Main** aggiungere il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="b84fc-150">Add the following code to the end of the **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="b84fc-151">Fare clic su **Compila** e quindi su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="b84fc-152">Correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="b84fc-152">Correct any errors.</span></span>

3. <span data-ttu-id="b84fc-153">Fare clic su **Debug** e quindi su **Avvia debug** per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b84fc-153">Click **Debug** and then **Start Debugging** to run the application.</span></span> <span data-ttu-id="b84fc-154">Potrebbero occorrere alcuni minuti per l'esecuzione della distribuzione.</span><span class="sxs-lookup"><span data-stu-id="b84fc-154">It may take several minutes for the deployment to run.</span></span>

4. <span data-ttu-id="b84fc-155">Per verificare che l'applicazione abbia aggiunto il nuovo hub IoT, visitare il [portale di Azure][lnk-azure-portal] e visualizzare l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="b84fc-155">To verify your application added the new IoT hub, visit the [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="b84fc-156">In alternativa, usare il cmdlet di PowerShell **Get-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-156">Alternatively, use the **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="b84fc-157">Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="b84fc-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="b84fc-158">Al termine è possibile eliminare l'hub IoT usando il [portale di Azure][lnk-azure-portal] o il cmdlet di PowerShell **Remove-AzureRmResource**.</span><span class="sxs-lookup"><span data-stu-id="b84fc-158">You can delete the IoT hub through the [Azure portal][lnk-azure-portal] or by using the **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b84fc-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b84fc-159">Next steps</span></span>
<span data-ttu-id="b84fc-160">Dopo avere distribuito un hub IoT usando un modello di Azure Resource Manager con un programma C#, può essere opportuno ottenere informazioni più dettagliate:</span><span class="sxs-lookup"><span data-stu-id="b84fc-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want to explore further:</span></span>

* <span data-ttu-id="b84fc-161">Informazioni sulle funzionalità dell'[API REST del provider di risorse dell'hub IoT][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="b84fc-161">Read about the capabilities of the [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="b84fc-162">Per altre informazioni sulle funzionalità di Azure Resource Manager, vedere la [Panoramica di Azure Resource Manager][lnk-azure-rm-overview].</span><span class="sxs-lookup"><span data-stu-id="b84fc-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] to learn more about the capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="b84fc-163">Per altre informazioni sulle attività di sviluppo per l'hub IoT, vedere gli articoli seguenti:</span><span class="sxs-lookup"><span data-stu-id="b84fc-163">To learn more about developing for IoT Hub, see the following articles:</span></span>

* <span data-ttu-id="b84fc-164">[Introduzione a C SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="b84fc-164">[Introduction to C SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="b84fc-165">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="b84fc-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="b84fc-166">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="b84fc-166">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="b84fc-167">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="b84fc-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
