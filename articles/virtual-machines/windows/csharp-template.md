---
title: aaaDeploy una macchina virtuale con c# e un modello di gestione risorse | Documenti Microsoft
description: Informazioni su toouse toohow c# e un toodeploy di modello una macchina virtuale di Azure Resource Manager.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: bfba66e8-c923-4df2-900a-0c2643b81240
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: davidmu
ms.openlocfilehash: 91d470228cfeed72336b488ffef4dfbb25bc3a40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="97f66-103">Distribuire una macchina virtuale di Azure con C# e un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97f66-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="97f66-104">In questo articolo illustra come toodeploy un modello di gestione risorse di Azure tramite c#.</span><span class="sxs-lookup"><span data-stu-id="97f66-104">This article shows you how toodeploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="97f66-105">modello Hello creato consente di distribuire una singola macchina virtuale che esegue Windows Server in una nuova rete virtuale con una singola subnet.</span><span class="sxs-lookup"><span data-stu-id="97f66-105">hello template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="97f66-106">Per una descrizione dettagliata della risorsa di macchina virtuale hello, vedere [macchine virtuali in un modello di gestione risorse di Azure](template-description.md).</span><span class="sxs-lookup"><span data-stu-id="97f66-106">For a detailed description of hello virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="97f66-107">Per ulteriori informazioni su tutte le risorse di hello in un modello, vedere [procedura dettagliata di modello di gestione risorse di Azure](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="97f66-107">For more information about all hello resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="97f66-108">Sono necessari circa 10 minuti toodo questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="97f66-108">It takes about 10 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="97f66-109">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="97f66-109">Create a Visual Studio project</span></span>

<span data-ttu-id="97f66-110">In questo passaggio è assicurarsi che Visual Studio è installato e si crea un modello di hello console toodeploy applicazione utilizzata.</span><span class="sxs-lookup"><span data-stu-id="97f66-110">In this step, you make sure that Visual Studio is installed and you create a console application used toodeploy hello template.</span></span>

1. <span data-ttu-id="97f66-111">Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="97f66-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="97f66-112">Selezionare **lo sviluppo desktop .NET** hello pagina carichi di lavoro e quindi fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="97f66-112">Select **.NET desktop development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="97f66-113">In hello riepilogo, è possibile vedere che **gli strumenti di sviluppo di .NET Framework 4 a 4.6** viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="97f66-113">In hello summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="97f66-114">Se già stato installato Visual Studio, è possibile aggiungere hello .NET il carico di lavoro hello utilità di avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97f66-114">If you have already installed Visual Studio, you can add hello .NET workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="97f66-115">In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="97f66-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="97f66-116">In **modelli** > **Visual c#**selezionare **applicazione Console (.NET Framework)**, immettere *myDotnetProject* per nome hello del progetto, il percorso di selezione hello del progetto di hello, Hello e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="97f66-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-hello-packages"></a><span data-ttu-id="97f66-117">Installare i pacchetti hello</span><span class="sxs-lookup"><span data-stu-id="97f66-117">Install hello packages</span></span>

<span data-ttu-id="97f66-118">Pacchetti NuGet sono hello più semplice modo tooinstall hello librerie necessario toofinish questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="97f66-118">NuGet packages are hello easiest way tooinstall hello libraries that you need toofinish these steps.</span></span> <span data-ttu-id="97f66-119">librerie di hello tooget che è necessario in Visual Studio, eseguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="97f66-119">tooget hello libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="97f66-120">Fare clic su **Strumenti** > **Gestione pacchetti NuGet** e quindi su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="97f66-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="97f66-121">Nella console di hello, digita questi comandi:</span><span class="sxs-lookup"><span data-stu-id="97f66-121">Type these commands in hello console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-hello-files"></a><span data-ttu-id="97f66-122">Creare file hello</span><span class="sxs-lookup"><span data-stu-id="97f66-122">Create hello files</span></span>

<span data-ttu-id="97f66-123">In questo passaggio si crea un file di modello che consente di distribuire risorse hello e un file di parametri che fornisce modelli di toohello valori di parametro.</span><span class="sxs-lookup"><span data-stu-id="97f66-123">In this step, you create a template file that deploys hello resources and a parameters file that supplies parameter values toohello template.</span></span> <span data-ttu-id="97f66-124">È inoltre possibile creare un file di autorizzazione che è utilizzati tooperform le operazioni di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="97f66-124">You also create an authorization file that is used tooperform Azure Resource Manager operations.</span></span>

### <a name="create-hello-template-file"></a><span data-ttu-id="97f66-125">Creare il file di modello hello</span><span class="sxs-lookup"><span data-stu-id="97f66-125">Create hello template file</span></span>

1. <span data-ttu-id="97f66-126">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="97f66-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="97f66-127">File con nome hello *CreateVMTemplate.json*, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="97f66-127">Name hello file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="97f66-128">Aggiungere questo file toohello di codice JSON che è stato creato:</span><span class="sxs-lookup"><span data-stu-id="97f66-128">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUsername": { "type": "string" },
        "adminPassword": { "type": "securestring" }
      },
      "variables": {
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks','myVNet')]", 
        "subnetRef": "[concat(variables('vnetID'),'/subnets/mySubnet')]", 
      },
      "resources": [
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/publicIPAddresses",
          "name": "myPublicIPAddress",
          "location": "[resourceGroup().location]",
          "properties": {
            "publicIPAllocationMethod": "Dynamic",
            "dnsSettings": {
              "domainNameLabel": "myresourcegroupdns1"
            }
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "myVNet",
          "location": "[resourceGroup().location]",
          "properties": {
            "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
            "subnets": [
              {
                "name": "mySubnet",
                "properties": { "addressPrefix": "10.0.0.0/24" }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-03-30",
          "type": "Microsoft.Network/networkInterfaces",
          "name": "myNic",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/publicIPAddresses/', 'myPublicIPAddress')]",
            "[resourceId('Microsoft.Network/virtualNetworks/', 'myVNet')]"
          ],
          "properties": {
            "ipConfigurations": [
              {
                "name": "ipconfig1",
                "properties": {
                  "privateIPAllocationMethod": "Dynamic",
                  "publicIPAddress": { "id": "[resourceId('Microsoft.Network/publicIPAddresses','myPublicIPAddress')]" },
                  "subnet": { "id": "[variables('subnetRef')]" }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2016-04-30-preview",
          "type": "Microsoft.Compute/virtualMachines",
          "name": "myVM",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[resourceId('Microsoft.Network/networkInterfaces/', 'myNic')]"
          ],
          "properties": {
            "hardwareProfile": { "vmSize": "Standard_DS1" },
            "osProfile": {
              "computerName": "myVM",
              "adminUsername": "[parameters('adminUsername')]",
              "adminPassword": "[parameters('adminPassword')]"
            },
            "storageProfile": {
              "imageReference": {
                "publisher": "MicrosoftWindowsServer",
                "offer": "WindowsServer",
                "sku": "2012-R2-Datacenter",
                "version": "latest"
              },
              "osDisk": {
                "name": "myManagedOSDisk",
                "caching": "ReadWrite",
                "createOption": "FromImage"
              }
            },
            "networkProfile": {
              "networkInterfaces": [
                {
                  "id": "[resourceId('Microsoft.Network/networkInterfaces','myNic')]"
                }
              ]
            }
          }
        }
      ]
    }
    ```

3. <span data-ttu-id="97f66-129">Salvare il file di CreateVMTemplate.json hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-129">Save hello CreateVMTemplate.json file.</span></span>

### <a name="create-hello-parameters-file"></a><span data-ttu-id="97f66-130">Creare i file dei parametri hello</span><span class="sxs-lookup"><span data-stu-id="97f66-130">Create hello parameters file</span></span>

<span data-ttu-id="97f66-131">toospecify i valori per i parametri delle risorse hello definiti nel modello di hello, creare un file di parametri che contiene i valori hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-131">toospecify values for hello resource parameters that are defined in hello template, you create a parameters file that contains hello values.</span></span>

1. <span data-ttu-id="97f66-132">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="97f66-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="97f66-133">File con nome hello *Parameters.json*, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="97f66-133">Name hello file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="97f66-134">Aggiungere questo file toohello di codice JSON che è stato creato:</span><span class="sxs-lookup"><span data-stu-id="97f66-134">Add this JSON code toohello file that you created:</span></span>

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adminUserName": { "value": "azureuser" },
        "adminPassword": { "value": "Azure12345678" }
      }
    }
    ```

4. <span data-ttu-id="97f66-135">Salvare il file di Parameters.json hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-135">Save hello Parameters.json file.</span></span>

### <a name="create-hello-authorization-file"></a><span data-ttu-id="97f66-136">Creare il file di autorizzazione hello</span><span class="sxs-lookup"><span data-stu-id="97f66-136">Create hello authorization file</span></span>

<span data-ttu-id="97f66-137">Prima di poter distribuire un modello, assicurarsi di disporre di accesso tooan [entità servizio Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="97f66-137">Before you can deploy a template, make sure that you have access tooan [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="97f66-138">Dall'entità servizio hello, acquisire un token per autenticare le richieste tooAzure Gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="97f66-138">From hello service principal, you acquire a token for authenticating requests tooAzure Resource Manager.</span></span> <span data-ttu-id="97f66-139">È inoltre necessario registrare ID applicazione hello, chiave di autenticazione hello e ID tenant hello che è necessario che nel file di autorizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-139">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in hello authorization file.</span></span>

1. <span data-ttu-id="97f66-140">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="97f66-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="97f66-141">File con nome hello *azureauth.properties*, quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="97f66-141">Name hello file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="97f66-142">Aggiungere le proprietà di autorizzazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="97f66-142">Add these authorization properties:</span></span>

    ```
    subscription=<subscription-id>
    client=<application-id>
    key=<authentication-key>
    tenant=<tenant-id>
    managementURI=https://management.core.windows.net/
    baseURL=https://management.azure.com/
    authURL=https://login.windows.net/
    graphURL=https://graph.windows.net/
    ```

    <span data-ttu-id="97f66-143">Sostituire  **&lt;id sottoscrizione&gt;**  con l'identificatore della sottoscrizione,  **&lt;id applicazione&gt;**  con hello applicazione Active Directory identificatore,  **&lt;chiave di autenticazione&gt;**  con chiave applicazione hello e  **&lt;id tenant&gt;**  con tenant hello identificatore.</span><span class="sxs-lookup"><span data-stu-id="97f66-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with hello Active Directory application identifier, **&lt;authentication-key&gt;** with hello application key, and **&lt;tenant-id&gt;** with hello tenant identifier.</span></span>

3. <span data-ttu-id="97f66-144">Salvare il file di azureauth.properties hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-144">Save hello azureauth.properties file.</span></span>
4. <span data-ttu-id="97f66-145">Impostare una variabile di ambiente Windows denominata AZURE_AUTH_LOCATION con file di tooauthorization hello percorso completo che è stato creato, ad esempio hello possibile usare il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="97f66-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with hello full path tooauthorization file that you created, for example hello following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-hello-management-client"></a><span data-ttu-id="97f66-146">Creare il client di gestione hello</span><span class="sxs-lookup"><span data-stu-id="97f66-146">Create hello management client</span></span>

1. <span data-ttu-id="97f66-147">Aprire il file Program.cs hello per progetto hello creato e quindi aggiungerle utilizzando istruzioni esistente toohello all'inizio del file hello:</span><span class="sxs-lookup"><span data-stu-id="97f66-147">Open hello Program.cs file for hello project that you created, and then add these using statements toohello existing statements at top of hello file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="97f66-148">client di gestione di hello toocreate, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="97f66-148">toocreate hello management client, add this code toohello Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="97f66-149">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="97f66-149">Create a resource group</span></span>

<span data-ttu-id="97f66-150">i valori toospecify per un'applicazione hello, aggiungere metodo Main toohello di codice:</span><span class="sxs-lookup"><span data-stu-id="97f66-150">toospecify values for hello application, add code toohello Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="97f66-151">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="97f66-151">Create a storage account</span></span>

<span data-ttu-id="97f66-152">parametri e modello hello vengono distribuiti da un account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="97f66-152">hello template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="97f66-153">In questo passaggio, creare account hello e caricare file hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-153">In this step, you create hello account and upload hello files.</span></span> 

<span data-ttu-id="97f66-154">toocreate hello account, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="97f66-154">toocreate hello account, add this code toohello Main method:</span></span>

```
string storageAccountName = SdkContext.RandomResourceName("st", 10);

Console.WriteLine("Creating storage account...");
var storage = azure.StorageAccounts.Define(storageAccountName)
    .WithRegion(Region.USWest)
    .WithExistingResourceGroup(resourceGroup)
    .Create();

var storageKeys = storage.GetKeys();
string storageConnectionString = "DefaultEndpointsProtocol=https;"
    + "AccountName=" + storage.Name
    + ";AccountKey=" + storageKeys[0].Value
    + ";EndpointSuffix=core.windows.net";

var account = CloudStorageAccount.Parse(storageConnectionString);
var serviceClient = account.CreateCloudBlobClient();

Console.WriteLine("Creating container...");
var container = serviceClient.GetContainerReference("templates");
container.CreateIfNotExistsAsync().Wait();
var containerPermissions = new BlobContainerPermissions()
    { PublicAccess = BlobContainerPublicAccessType.Container };
container.SetPermissionsAsync(containerPermissions).Wait();

Console.WriteLine("Uploading template file...");
var templateblob = container.GetBlockBlobReference("CreateVMTemplate.json");
templateblob.UploadFromFile("..\\..\\CreateVMTemplate.json");

Console.WriteLine("Uploading parameters file...");
var paramblob = container.GetBlockBlobReference("Parameters.json");
paramblob.UploadFromFile("..\\..\\Parameters.json");
```

## <a name="deploy-hello-template"></a><span data-ttu-id="97f66-155">Distribuire il modello di hello</span><span class="sxs-lookup"><span data-stu-id="97f66-155">Deploy hello template</span></span>

<span data-ttu-id="97f66-156">Distribuire il modello di hello e i parametri dall'account di archiviazione hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="97f66-156">Deploy hello template and parameters from hello storage account that was created.</span></span> 

<span data-ttu-id="97f66-157">modello di hello toodeploy, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="97f66-157">toodeploy hello template, add this code toohello Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter toodelete hello resource group...");
Console.ReadLine();
```

## <a name="delete-hello-resources"></a><span data-ttu-id="97f66-158">Eliminare le risorse di hello</span><span class="sxs-lookup"><span data-stu-id="97f66-158">Delete hello resources</span></span>

<span data-ttu-id="97f66-159">Poiché vengono addebitate per le risorse utilizzate in Azure, è sempre risorse toodelete buona norma che non sono più necessari.</span><span class="sxs-lookup"><span data-stu-id="97f66-159">Because you are charged for resources used in Azure, it is always good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="97f66-160">Non è necessario toodelete ogni risorsa separatamente da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="97f66-160">You don’t need toodelete each resource separately from a resource group.</span></span> <span data-ttu-id="97f66-161">Elimina il gruppo di risorse hello e tutte le relative risorse vengono eliminate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="97f66-161">Delete hello resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="97f66-162">risorsa hello toodelete gruppo, aggiungere questo toohello codice metodo Main:</span><span class="sxs-lookup"><span data-stu-id="97f66-162">toodelete hello resource group, add this code toohello Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-hello-application"></a><span data-ttu-id="97f66-163">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="97f66-163">Run hello application</span></span>

<span data-ttu-id="97f66-164">Richiede circa cinque minuti per questo toorun di applicazione console completamente dall'inizio toofinish.</span><span class="sxs-lookup"><span data-stu-id="97f66-164">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> 

1. <span data-ttu-id="97f66-165">un'applicazione console hello toorun, fare clic su **avviare**.</span><span class="sxs-lookup"><span data-stu-id="97f66-165">toorun hello console application, click **Start**.</span></span>

2. <span data-ttu-id="97f66-166">Prima di premere **invio** toostart eliminato le risorse, si potrebbe richiedere alcuni minuti Creazione hello tooverify delle risorse hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="97f66-166">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify hello creation of hello resources in hello Azure portal.</span></span> <span data-ttu-id="97f66-167">Fare clic su hello distribuzione informazioni sullo stato toosee distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="97f66-167">Click hello deployment status toosee information about hello deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97f66-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="97f66-168">Next steps</span></span>
* <span data-ttu-id="97f66-169">Se si sono verificati problemi con la distribuzione di hello, un passaggio successivo consisterebbe toolook in [risolvere i problemi relativi a errori comuni di distribuzione di Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="97f66-169">If there were issues with hello deployment, a next step would be toolook at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="97f66-170">Informazioni su come toodeploy una macchina virtuale e le risorse di supporto, è consigliabile consultare [distribuire un Azure macchina virtuale utilizzando c#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="97f66-170">Learn how toodeploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
