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
# <a name="create-an-iot-hub-using-azure-resource-manager-template-net"></a><span data-ttu-id="2f1e0-103">Creare un hub IoT usando un modello di Azure Resource Manager (.NET)</span><span class="sxs-lookup"><span data-stu-id="2f1e0-103">Create an IoT hub using Azure Resource Manager template (.NET)</span></span>

[!INCLUDE [iot-hub-resource-manager-selector](../../includes/iot-hub-resource-manager-selector.md)]

<span data-ttu-id="2f1e0-104">È possibile utilizzare Gestione risorse di Azure toocreate e gestire hub IoT di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-104">You can use Azure Resource Manager toocreate and manage Azure IoT hubs programmatically.</span></span> <span data-ttu-id="2f1e0-105">In questa esercitazione illustra come toouse un toocreate modello di gestione risorse di Azure un hub IoT da un programma c#.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-105">This tutorial shows you how toouse an Azure Resource Manager template toocreate an IoT hub from a C# program.</span></span>

> [!NOTE]
> <span data-ttu-id="2f1e0-106">Azure offre due modelli di distribuzione per creare e usare le risorse: [modello di distribuzione classica e Azure Resource Manager](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="2f1e0-106">Azure has two different deployment models for creating and working with resources:  [Azure Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="2f1e0-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-107">This article covers using hello Azure Resource Manager deployment model.</span></span>

<span data-ttu-id="2f1e0-108">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-108">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2f1e0-109">Visual Studio 2015 o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-109">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2f1e0-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-110">An active Azure account.</span></span> <br/><span data-ttu-id="2f1e0-111">Se non si ha un account, è possibile crearne uno [gratuito][lnk-free-trial] in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-111">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>
* <span data-ttu-id="2f1e0-112">Un [account di archiviazione di Azure][lnk-storage-account] in cui è possibile archiviare i file del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-112">An [Azure Storage account][lnk-storage-account] where you can store your Azure Resource Manager template files.</span></span>
* <span data-ttu-id="2f1e0-113">[Azure PowerShell 1.0][lnk-powershell-install] o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-113">[Azure PowerShell 1.0][lnk-powershell-install] or later.</span></span>

[!INCLUDE [iot-hub-prepare-resource-manager](../../includes/iot-hub-prepare-resource-manager.md)]

## <a name="prepare-your-visual-studio-project"></a><span data-ttu-id="2f1e0-114">Preparare il progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f1e0-114">Prepare your Visual Studio project</span></span>

1. <span data-ttu-id="2f1e0-115">In Visual Studio, creare un progetto di Visual c# Windows Desktop classico utilizzando hello **applicazione Console (.NET Framework)** modello di progetto.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-115">In Visual Studio, create a Visual C# Windows Classic Desktop project using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="2f1e0-116">Progetto hello nome **CreateIoTHub**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-116">Name hello project **CreateIoTHub**.</span></span>

2. <span data-ttu-id="2f1e0-117">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-117">In Solution Explorer, right-click on your project and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="2f1e0-118">Controllare in Gestione pacchetti NuGet **versione provvisoria di inclusione**e in hello **Sfoglia** Cerca pagina **Microsoft.Azure.Management.ResourceManager**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-118">In NuGet Package Manager, check **Include prerelease**, and on hello **Browse** page search for **Microsoft.Azure.Management.ResourceManager**.</span></span> <span data-ttu-id="2f1e0-119">Selezionare il pacchetto di hello, fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenze hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-119">Select hello package, click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello licenses.</span></span>

4. <span data-ttu-id="2f1e0-120">In Gestione pacchetti NuGet cercare **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-120">In NuGet Package Manager, search for **Microsoft.IdentityModel.Clients.ActiveDirectory**.</span></span>  <span data-ttu-id="2f1e0-121">Fare clic su **installare**nella **verificare le modifiche** fare clic su **OK**, quindi fare clic su **accetto** licenza hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-121">Click **Install**, in **Review Changes** click **OK**, then click **I Accept** tooaccept hello license.</span></span>

5. <span data-ttu-id="2f1e0-122">In Program.cs, sostituire hello **utilizzando** istruzioni con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-122">In Program.cs, replace hello existing **using** statements with hello following code:</span></span>

    ```csharp
    using System;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.ResourceManager.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```

6. <span data-ttu-id="2f1e0-123">In Program.cs aggiungere hello seguenti variabili statiche, sostituendo i valori segnaposto hello.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-123">In Program.cs, add hello following static variables replacing hello placeholder values.</span></span> <span data-ttu-id="2f1e0-124">Nella parte precedente di questa esercitazione si è preso nota di **ApplicationId**, **SubscriptionId**, **TenantId** e **Password**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-124">You made a note of **ApplicationId**, **SubscriptionId**, **TenantId**, and **Password** earlier in this tutorial.</span></span> <span data-ttu-id="2f1e0-125">**Il nome dell'account di archiviazione di Azure** è il nome di hello di hello account di archiviazione di Azure in cui si archiviano i file di modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-125">**Your Azure Storage account name** is hello name of hello Azure Storage account where you store your Azure Resource Manager template files.</span></span> <span data-ttu-id="2f1e0-126">**Nome del gruppo di risorse** hello nome del gruppo di risorse hello è utilizzare quando si crea l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-126">**Resource group name** is hello name of hello resource group you use when you create hello IoT hub.</span></span> <span data-ttu-id="2f1e0-127">nome di Hello può essere un gruppo di risorse nuovo o esistente.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-127">hello name can be a pre-existing or new resource group.</span></span> <span data-ttu-id="2f1e0-128">**Nome della distribuzione** è un nome per la distribuzione di hello, ad esempio **Deployment_01**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-128">**Deployment name** is a name for hello deployment, such as **Deployment_01**.</span></span>

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

## <a name="submit-a-template-toocreate-an-iot-hub"></a><span data-ttu-id="2f1e0-129">Inviare un toocreate modello un hub IoT</span><span class="sxs-lookup"><span data-stu-id="2f1e0-129">Submit a template toocreate an IoT hub</span></span>

<span data-ttu-id="2f1e0-130">Utilizzare un JSON modello e parametro file toocreate un hub IoT nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-130">Use a JSON template and parameter file toocreate an IoT hub in your resource group.</span></span> <span data-ttu-id="2f1e0-131">È anche possibile utilizzare un Azure Resource Manager modello toomake modifiche tooan IoT hub esistente.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-131">You can also use an Azure Resource Manager template toomake changes tooan existing IoT hub.</span></span>

1. <span data-ttu-id="2f1e0-132">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi su **Aggiungi** e infine su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-132">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2f1e0-133">Aggiungere un file JSON denominato **template.json** tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-133">Add a JSON file called **template.json** tooyour project.</span></span>

2. <span data-ttu-id="2f1e0-134">tooadd un standard toohello hub IoT **Stati Uniti orientali** regione, sostituire hello contenuto di **template.json** con hello seguente definizione di risorsa.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-134">tooadd a standard IoT hub toohello **East US** region, replace hello contents of **template.json** with hello following resource definition.</span></span> <span data-ttu-id="2f1e0-135">Per l'elenco corrente di hello delle aree che supportano IoT Hub vedere [stato Azure][lnk-status]:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-135">For hello current list of regions that support IoT Hub see [Azure Status][lnk-status]:</span></span>

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

3. <span data-ttu-id="2f1e0-136">In Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto, quindi su **Aggiungi** e infine su **Nuovo elemento**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-136">In Solution Explorer, right-click on your project, click **Add**, and then click **New Item**.</span></span> <span data-ttu-id="2f1e0-137">Aggiungere un file JSON denominato **parameters.json** tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-137">Add a JSON file called **parameters.json** tooyour project.</span></span>

4. <span data-ttu-id="2f1e0-138">Sostituire il contenuto di hello di **parameters.json** con le seguenti informazioni di parametro che imposta, ad esempio un nome per l'hub IoT nuovo hello hello **{iniziali} mynewiothub**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-138">Replace hello contents of **parameters.json** with hello following parameter information that sets a name for hello new IoT hub such as **{your initials}mynewiothub**.</span></span> <span data-ttu-id="2f1e0-139">nome dell'hub IoT Hello deve essere globalmente univoco, pertanto deve includere il nome o iniziali:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-139">hello IoT hub name must be globally unique so it should include your name or initials:</span></span>

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

5. <span data-ttu-id="2f1e0-140">In **Esplora Server**, connettersi tooyour sottoscrizione di Azure e l'archiviazione di Azure account creare un contenitore chiamato **modelli**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-140">In **Server Explorer**, connect tooyour Azure subscription, and in your Azure Storage account create a container called **templates**.</span></span> <span data-ttu-id="2f1e0-141">In hello **proprietà** pannello, hello set **accesso in lettura pubblico** le autorizzazioni per hello **modelli** contenitore troppo**Blob**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-141">In hello **Properties** panel, set hello **Public Read Access** permissions for hello **templates** container too**Blob**.</span></span>

6. <span data-ttu-id="2f1e0-142">In **Esplora Server**, fare clic su hello **modelli** contenitore e quindi fare clic su **Visualizza contenitore Blob**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-142">In **Server Explorer**, right-click on hello **templates** container and then click **View Blob Container**.</span></span> <span data-ttu-id="2f1e0-143">Fare clic su hello **carica Blob** pulsante, selezionare due file hello, **parameters.json** e **templates.json**, quindi fare clic su **aprire** hello tooupload JSON file toohello **modelli** contenitore.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-143">Click hello **Upload Blob** button, select hello two files, **parameters.json** and **templates.json**, and then click **Open** tooupload hello JSON files toohello **templates** container.</span></span> <span data-ttu-id="2f1e0-144">URL di Hello di BLOB hello contenente i dati JSON hello sono:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-144">hello URLs of hello blobs containing hello JSON data are:</span></span>

    ```csharp
    https://{Your storage account name}.blob.core.windows.net/templates/parameters.json
    https://{Your storage account name}.blob.core.windows.net/templates/template.json
    ```
7. <span data-ttu-id="2f1e0-145">Aggiungere hello tooProgram.cs metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-145">Add hello following method tooProgram.cs:</span></span>

    ```csharp
    static void CreateIoTHub(ResourceManagementClient client)
    {

    }
    ```

8. <span data-ttu-id="2f1e0-146">Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo toosubmit hello modello e parametro file toohello Gestione risorse di Azure:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-146">Add hello following code toohello **CreateIoTHub** method toosubmit hello template and parameter files toohello Azure Resource Manager:</span></span>

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

9. <span data-ttu-id="2f1e0-147">Aggiungere i seguenti toohello codice hello **CreateIoTHub** metodo che visualizza lo stato di hello e le chiavi di hello per l'hub IoT hello nuovo:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-147">Add hello following code toohello **CreateIoTHub** method that displays hello status and hello keys for hello new IoT hub:</span></span>

    ```csharp
    string state = createResponse.Properties.ProvisioningState;
    Console.WriteLine("Deployment state: {0}", state);

    if (state != "Succeeded")
    {
      Console.WriteLine("Failed toocreate iothub");
    }
    Console.WriteLine(createResponse.Properties.Outputs);
    ```

## <a name="complete-and-run-hello-application"></a><span data-ttu-id="2f1e0-148">Applicazione hello completo e di esecuzione</span><span class="sxs-lookup"><span data-stu-id="2f1e0-148">Complete and run hello application</span></span>

<span data-ttu-id="2f1e0-149">È ora possibile completare un'applicazione hello dal chiamante hello **CreateIoTHub** metodo prima di generare ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-149">You can now complete hello application by calling hello **CreateIoTHub** method before you build and run it.</span></span>

1. <span data-ttu-id="2f1e0-150">Aggiungere hello successivo toohello codice alla fine di hello **Main** metodo:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-150">Add hello following code toohello end of hello **Main** method:</span></span>

    ```csharp
    CreateIoTHub(client);
    Console.ReadLine();
    ```

2. <span data-ttu-id="2f1e0-151">Fare clic su **Compila** e quindi su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-151">Click **Build** and then **Build Solution**.</span></span> <span data-ttu-id="2f1e0-152">Correggere eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-152">Correct any errors.</span></span>

3. <span data-ttu-id="2f1e0-153">Fare clic su **Debug** e quindi **Avvia debug** toorun un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-153">Click **Debug** and then **Start Debugging** toorun hello application.</span></span> <span data-ttu-id="2f1e0-154">Potrebbe richiedere alcuni minuti per hello toorun di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-154">It may take several minutes for hello deployment toorun.</span></span>

4. <span data-ttu-id="2f1e0-155">l'applicazione aggiunta tooverify hello nuovo hub IoT, visitare hello [portale di Azure] [ lnk-azure-portal] e visualizzare l'elenco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-155">tooverify your application added hello new IoT hub, visit hello [Azure portal][lnk-azure-portal] and view your list of resources.</span></span> <span data-ttu-id="2f1e0-156">In alternativa, utilizzare hello **Get-AzureRmResource** cmdlet di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-156">Alternatively, use hello **Get-AzureRmResource** PowerShell cmdlet.</span></span>

> [!NOTE]
> <span data-ttu-id="2f1e0-157">Questa applicazione di esempio aggiunge un hub IoT Standard S1 che viene addebitato.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-157">This example application adds an S1 Standard IoT Hub for which you are billed.</span></span> <span data-ttu-id="2f1e0-158">È possibile eliminare l'hub IoT hello tramite hello [portale di Azure] [ lnk-azure-portal] o utilizzando hello **Remove-AzureRmResource** cmdlet PowerShell dopo aver terminato.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-158">You can delete hello IoT hub through hello [Azure portal][lnk-azure-portal] or by using hello **Remove-AzureRmResource** PowerShell cmdlet when you are finished.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f1e0-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f1e0-159">Next steps</span></span>
<span data-ttu-id="2f1e0-160">Dopo aver distribuito un hub IoT utilizzando un modello di gestione risorse di Azure con un programma c#, è opportuno tooexplore ulteriormente:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-160">Now you have deployed an IoT hub using an Azure Resource Manager template with a C# program, you may want tooexplore further:</span></span>

* <span data-ttu-id="2f1e0-161">Leggere informazioni sulle funzionalità di hello di hello [il provider di risorse IoT Hub API REST][lnk-rest-api].</span><span class="sxs-lookup"><span data-stu-id="2f1e0-161">Read about hello capabilities of hello [IoT Hub resource provider REST API][lnk-rest-api].</span></span>
* <span data-ttu-id="2f1e0-162">Lettura [Panoramica di gestione risorse di Azure] [ lnk-azure-rm-overview] toolearn ulteriori informazioni sulla funzionalità hello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f1e0-162">Read [Azure Resource Manager overview][lnk-azure-rm-overview] toolearn more about hello capabilities of Azure Resource Manager.</span></span>

<span data-ttu-id="2f1e0-163">toolearn più sullo sviluppo per l'IoT Hub, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-163">toolearn more about developing for IoT Hub, see hello following articles:</span></span>

* <span data-ttu-id="2f1e0-164">[Introduzione tooC SDK][lnk-c-sdk]</span><span class="sxs-lookup"><span data-stu-id="2f1e0-164">[Introduction tooC SDK][lnk-c-sdk]</span></span>
* <span data-ttu-id="2f1e0-165">[Azure IoT SDKs][lnk-sdks] (SDK di IoT di Azure)</span><span class="sxs-lookup"><span data-stu-id="2f1e0-165">[Azure IoT SDKs][lnk-sdks]</span></span>

<span data-ttu-id="2f1e0-166">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="2f1e0-166">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="2f1e0-167">[Simulazione di un dispositivo con Azure IoT Edge][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="2f1e0-167">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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
