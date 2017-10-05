---
title: Distribuire una macchina virtuale con C# e un modello di Azure Resource Manager | Microsoft Docs
description: Informazioni su come usare C# e un modello di Resource Manager per distribuire una macchina virtuale di Azure.
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
ms.openlocfilehash: bd1c860db026f948202cd1f3aa763b4547c597b4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-an-azure-virtual-machine-using-c-and-a-resource-manager-template"></a><span data-ttu-id="dc913-103">Distribuire una macchina virtuale di Azure con C# e un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="dc913-103">Deploy an Azure Virtual Machine using C# and a Resource Manager template</span></span>
<span data-ttu-id="dc913-104">Questo articolo descrive come distribuire un modello di Azure Resource Manager tramite C#.</span><span class="sxs-lookup"><span data-stu-id="dc913-104">This article shows you how to deploy an Azure Resource Manager template using C#.</span></span> <span data-ttu-id="dc913-105">Il modello creato consente di distribuire una singola macchina virtuale che esegue Windows Server in una nuova rete virtuale con un'unica subnet.</span><span class="sxs-lookup"><span data-stu-id="dc913-105">The template that you create deploys a single virtual machine running Windows Server in a new virtual network with a single subnet.</span></span>

<span data-ttu-id="dc913-106">Per una descrizione dettagliata della risorsa macchina virtuale, vedere [Virtual machines in an Azure Resource Manager template](template-description.md) (Macchine virtuali in un modello di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="dc913-106">For a detailed description of the virtual machine resource, see [Virtual machines in an Azure Resource Manager template](template-description.md).</span></span> <span data-ttu-id="dc913-107">Per altre informazioni su tutte le risorse in un modello, vedere [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md) (Procedura dettagliata sui modelli di Azure Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="dc913-107">For more information about all the resources in a template, see [Azure Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="dc913-108">L'esecuzione di questi passaggi richiede circa 10 minuti.</span><span class="sxs-lookup"><span data-stu-id="dc913-108">It takes about 10 minutes to do these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="dc913-109">Creare un progetto di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc913-109">Create a Visual Studio project</span></span>

<span data-ttu-id="dc913-110">In questo passaggio, ci si assicura che Visual Studio sia installato e si crea un'applicazione console da usare per distribuire il modello.</span><span class="sxs-lookup"><span data-stu-id="dc913-110">In this step, you make sure that Visual Studio is installed and you create a console application used to deploy the template.</span></span>

1. <span data-ttu-id="dc913-111">Se non è già installato, installare [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="dc913-111">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="dc913-112">Selezionare **Sviluppo per desktop .NET** nella pagina Carichi di lavoro e quindi fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="dc913-112">Select **.NET desktop development** on the Workloads page, and then click **Install**.</span></span> <span data-ttu-id="dc913-113">Nel riepilogo si noti che **Strumenti di sviluppo per .NET Framework 4-4.6** viene selezionato automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dc913-113">In the summary, you can see that **.NET Framework 4 - 4.6 development tools** is automatically selected for you.</span></span> <span data-ttu-id="dc913-114">Se Visual Studio è già stato installato, è possibile aggiungere il carico di lavoro .NET usando l'utilità di avvio di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc913-114">If you have already installed Visual Studio, you can add the .NET workload using the Visual Studio Launcher.</span></span>
2. <span data-ttu-id="dc913-115">In Visual Studio fare clic su **File** > **Nuovo** > **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="dc913-115">In Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="dc913-116">In **Modelli** > **Visual C#** selezionare **App console (.NET Framework)**, immettere *myDotnetProject* come nome del progetto, selezionare il percorso del progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="dc913-116">In **Templates** > **Visual C#**, select **Console App (.NET Framework)**, enter *myDotnetProject* for the name of the project, select the location of the project, and then click **OK**.</span></span>

## <a name="install-the-packages"></a><span data-ttu-id="dc913-117">Installare i pacchetti</span><span class="sxs-lookup"><span data-stu-id="dc913-117">Install the packages</span></span>

<span data-ttu-id="dc913-118">I pacchetti NuGet sono il modo più semplice per installare le librerie necessarie per completare questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="dc913-118">NuGet packages are the easiest way to install the libraries that you need to finish these steps.</span></span> <span data-ttu-id="dc913-119">Per ottenere le librerie necessarie in Visual Studio, eseguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dc913-119">To get the libraries that you need in Visual Studio, do these steps:</span></span>

1. <span data-ttu-id="dc913-120">Fare clic su **Strumenti** > **Gestione pacchetti Nuget** e quindi su **Console di Gestione Pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="dc913-120">Click **Tools** > **Nuget Package Manager**, and then click **Package Manager Console**.</span></span>
2. <span data-ttu-id="dc913-121">Nella console digitare questi comandi:</span><span class="sxs-lookup"><span data-stu-id="dc913-121">Type these commands in the console:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.Fluent
    Install-Package WindowsAzure.Storage
    ```

## <a name="create-the-files"></a><span data-ttu-id="dc913-122">Creare i file</span><span class="sxs-lookup"><span data-stu-id="dc913-122">Create the files</span></span>

<span data-ttu-id="dc913-123">In questo passaggio si crea un file di modello che consente di distribuire le risorse e un file di parametri che fornisce i valori dei parametri nel modello.</span><span class="sxs-lookup"><span data-stu-id="dc913-123">In this step, you create a template file that deploys the resources and a parameters file that supplies parameter values to the template.</span></span> <span data-ttu-id="dc913-124">È possibile anche creare un file di autorizzazione da usare per eseguire operazioni in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dc913-124">You also create an authorization file that is used to perform Azure Resource Manager operations.</span></span>

### <a name="create-the-template-file"></a><span data-ttu-id="dc913-125">Creare il file di modello</span><span class="sxs-lookup"><span data-stu-id="dc913-125">Create the template file</span></span>

1. <span data-ttu-id="dc913-126">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="dc913-126">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="dc913-127">Assegnare un nome al file *CreateVMTemplate.json* e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dc913-127">Name the file *CreateVMTemplate.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="dc913-128">Aggiungere questo codice JSON al file appena creato:</span><span class="sxs-lookup"><span data-stu-id="dc913-128">Add this JSON code to the file that you created:</span></span>

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

3. <span data-ttu-id="dc913-129">Salvare il file CreateVMTemplate.json.</span><span class="sxs-lookup"><span data-stu-id="dc913-129">Save the CreateVMTemplate.json file.</span></span>

### <a name="create-the-parameters-file"></a><span data-ttu-id="dc913-130">Creare il file dei parametri</span><span class="sxs-lookup"><span data-stu-id="dc913-130">Create the parameters file</span></span>

<span data-ttu-id="dc913-131">Per specificare i valori per i parametri delle risorse definiti nel modello, creare un file dei parametri contenente i valori.</span><span class="sxs-lookup"><span data-stu-id="dc913-131">To specify values for the resource parameters that are defined in the template, you create a parameters file that contains the values.</span></span>

1. <span data-ttu-id="dc913-132">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="dc913-132">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="dc913-133">Assegnare un nome al file *Parameters.json* e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dc913-133">Name the file *Parameters.json*, and then click **Add**.</span></span>
2. <span data-ttu-id="dc913-134">Aggiungere questo codice JSON al file appena creato:</span><span class="sxs-lookup"><span data-stu-id="dc913-134">Add this JSON code to the file that you created:</span></span>

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

4. <span data-ttu-id="dc913-135">Salvare il file Parameters.json.</span><span class="sxs-lookup"><span data-stu-id="dc913-135">Save the Parameters.json file.</span></span>

### <a name="create-the-authorization-file"></a><span data-ttu-id="dc913-136">Creare il file di autorizzazione</span><span class="sxs-lookup"><span data-stu-id="dc913-136">Create the authorization file</span></span>

<span data-ttu-id="dc913-137">Prima di poter distribuire un modello, è necessario assicurarsi di avere accesso a un'[entità servizio Active Directory](../../resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="dc913-137">Before you can deploy a template, make sure that you have access to an [Active Directory service principal](../../resource-group-authenticate-service-principal.md).</span></span> <span data-ttu-id="dc913-138">Dall'entità servizio si acquisisce un token per autenticare le richieste ad Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="dc913-138">From the service principal, you acquire a token for authenticating requests to Azure Resource Manager.</span></span> <span data-ttu-id="dc913-139">È necessario anche registrare l'ID dell'applicazione, la chiave di autenticazione e l'ID del tenant necessari nel file di autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="dc913-139">You should also record the application ID, the authentication key, and the tenant ID that you need in the authorization file.</span></span>

1. <span data-ttu-id="dc913-140">In Esplora soluzioni fare clic con il pulsante destro del mouse su *myDotnetProject* > **Aggiungi** > **Nuovo elemento** e quindi selezionare **File di testo** in *Elementi di Visual C#*.</span><span class="sxs-lookup"><span data-stu-id="dc913-140">In Solution Explorer, right-click *myDotnetProject* > **Add** > **New Item**, and then select **Text File** in *Visual C# Items*.</span></span> <span data-ttu-id="dc913-141">Assegnare al file il nome *azureauth.properties* e quindi fare clic su **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="dc913-141">Name the file *azureauth.properties*, and then click **Add**.</span></span>
2. <span data-ttu-id="dc913-142">Aggiungere le proprietà di autorizzazione seguenti:</span><span class="sxs-lookup"><span data-stu-id="dc913-142">Add these authorization properties:</span></span>

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

    <span data-ttu-id="dc913-143">Sostituire **&lt;subscription-id&gt;** con l'identificatore della sottoscrizione, **&lt;application-id&gt;** con l'identificatore dell'applicazione Active Directory, **&lt;authentication-key&gt;** con la chiave dell'applicazione e **&lt;tenant-id&gt;** con l'identificatore del tenant.</span><span class="sxs-lookup"><span data-stu-id="dc913-143">Replace **&lt;subscription-id&gt;** with your subscription identifier, **&lt;application-id&gt;** with the Active Directory application identifier, **&lt;authentication-key&gt;** with the application key, and **&lt;tenant-id&gt;** with the tenant identifier.</span></span>

3. <span data-ttu-id="dc913-144">Salvare il file azureauth.properties.</span><span class="sxs-lookup"><span data-stu-id="dc913-144">Save the azureauth.properties file.</span></span>
4. <span data-ttu-id="dc913-145">Impostare una variabile di ambiente Windows denominata AZURE_AUTH_LOCATION con il percorso completo al file di autorizzazione creato. È possibile usare, ad esempio, il comando PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="dc913-145">Set an environment variable in Windows named AZURE_AUTH_LOCATION with the full path to authorization file that you created, for example the following PowerShell command can be used:</span></span>

    ```
    [Environment]::SetEnvironmentVariable("AZURE_AUTH_LOCATION", "C:\Visual Studio 2017\Projects\myDotnetProject\myDotnetProject\azureauth.properties", "User")
    ```
    
## <a name="create-the-management-client"></a><span data-ttu-id="dc913-146">Creare il client di gestione</span><span class="sxs-lookup"><span data-stu-id="dc913-146">Create the management client</span></span>

1. <span data-ttu-id="dc913-147">Aprire il file Program.cs per il progetto creato e quindi aggiungere le istruzioni using seguenti alle istruzioni esistenti all'inizio del file:</span><span class="sxs-lookup"><span data-stu-id="dc913-147">Open the Program.cs file for the project that you created, and then add these using statements to the existing statements at top of the file:</span></span>

    ```
    using Microsoft.Azure.Management.Compute.Fluent;
    using Microsoft.Azure.Management.Compute.Fluent.Models;
    using Microsoft.Azure.Management.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent;
    using Microsoft.Azure.Management.ResourceManager.Fluent.Core;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```

2. <span data-ttu-id="dc913-148">Per creare il client di gestione, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="dc913-148">To create the management client, add this code to the Main method:</span></span>

    ```
    var credentials = SdkContext.AzureCredentialsFactory
        .FromFile(Environment.GetEnvironmentVariable("AZURE_AUTH_LOCATION"));

    var azure = Azure
        .Configure()
        .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
        .Authenticate(credentials)
        .WithDefaultSubscription();
    ```

## <a name="create-a-resource-group"></a><span data-ttu-id="dc913-149">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="dc913-149">Create a resource group</span></span>

<span data-ttu-id="dc913-150">Per specificare i valori per l'applicazione, aggiungere il codice necessario al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="dc913-150">To specify values for the application, add code to the Main method:</span></span>

```
var groupName = "myResourceGroup";
var location = Region.USWest;

var resourceGroup = azure.ResourceGroups.Define(groupName)
    .WithRegion(location)
    .Create();
```

## <a name="create-a-storage-account"></a><span data-ttu-id="dc913-151">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="dc913-151">Create a storage account</span></span>

<span data-ttu-id="dc913-152">Il modello e i parametri vengono distribuiti da un account di archiviazione in Azure.</span><span class="sxs-lookup"><span data-stu-id="dc913-152">The template and parameters are deployed from a storage account in Azure.</span></span> <span data-ttu-id="dc913-153">In questo passaggio si creerà l'account e si caricheranno i file.</span><span class="sxs-lookup"><span data-stu-id="dc913-153">In this step, you create the account and upload the files.</span></span> 

<span data-ttu-id="dc913-154">Per creare l'account, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="dc913-154">To create the account, add this code to the Main method:</span></span>

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

## <a name="deploy-the-template"></a><span data-ttu-id="dc913-155">Distribuire il modello</span><span class="sxs-lookup"><span data-stu-id="dc913-155">Deploy the template</span></span>

<span data-ttu-id="dc913-156">Distribuire il modello e i parametri dall'account di archiviazione appena creato.</span><span class="sxs-lookup"><span data-stu-id="dc913-156">Deploy the template and parameters from the storage account that was created.</span></span> 

<span data-ttu-id="dc913-157">Per distribuire il modello, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="dc913-157">To deploy the template, add this code to the Main method:</span></span>

```
var templatePath = "https://" + storageAccountName + ".blob.core.windows.net/templates/CreateVMTemplate.json";
var paramPath = "https://" + storageAccountName + ".blob.core.windows.net/templates/Parameters.json";
var deployment = azure.Deployments.Define("myDeployment")
    .WithExistingResourceGroup(groupName)
    .WithTemplateLink(templatePath, "1.0.0.0")
    .WithParametersLink(paramPath, "1.0.0.0")
    .WithMode(Microsoft.Azure.Management.ResourceManager.Fluent.Models.DeploymentMode.Incremental)
    .Create();
Console.WriteLine("Press enter to delete the resource group...");
Console.ReadLine();
```

## <a name="delete-the-resources"></a><span data-ttu-id="dc913-158">Eliminare le risorse</span><span class="sxs-lookup"><span data-stu-id="dc913-158">Delete the resources</span></span>

<span data-ttu-id="dc913-159">Poiché vengono applicati addebiti per le risorse usate in Azure, è sempre consigliabile eliminare le risorse che non sono più necessarie.</span><span class="sxs-lookup"><span data-stu-id="dc913-159">Because you are charged for resources used in Azure, it is always good practice to delete resources that are no longer needed.</span></span> <span data-ttu-id="dc913-160">Non è necessario eliminare separatamente ogni risorsa da un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="dc913-160">You don’t need to delete each resource separately from a resource group.</span></span> <span data-ttu-id="dc913-161">Eliminando il gruppo di risorse, tutte le relative risorse verranno eliminate automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dc913-161">Delete the resource group and all its resources are automatically deleted.</span></span> 

<span data-ttu-id="dc913-162">Per eliminare il gruppo di risorse, aggiungere questo codice al metodo Main:</span><span class="sxs-lookup"><span data-stu-id="dc913-162">To delete the resource group, add this code to the Main method:</span></span>

```
azure.ResourceGroups.DeleteByName(groupName);
```

## <a name="run-the-application"></a><span data-ttu-id="dc913-163">Eseguire l'applicazione</span><span class="sxs-lookup"><span data-stu-id="dc913-163">Run the application</span></span>

<span data-ttu-id="dc913-164">L'esecuzione completa dell'applicazione console dall'inizio alla fine richiederà circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="dc913-164">It should take about five minutes for this console application to run completely from start to finish.</span></span> 

1. <span data-ttu-id="dc913-165">Per eseguire l'applicazione console, fare clic su **Avvia**.</span><span class="sxs-lookup"><span data-stu-id="dc913-165">To run the console application, click **Start**.</span></span>

2. <span data-ttu-id="dc913-166">Prima di premere **INVIO** per avviare l'eliminazione delle risorse, è consigliabile dedicare alcuni minuti alla verifica della creazione delle risorse nel Portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="dc913-166">Before you press **Enter** to start deleting resources, you could take a few minutes to verify the creation of the resources in the Azure portal.</span></span> <span data-ttu-id="dc913-167">Fare clic sullo stato della distribuzione per visualizzare le informazioni corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="dc913-167">Click the deployment status to see information about the deployment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc913-168">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dc913-168">Next steps</span></span>
* <span data-ttu-id="dc913-169">Se si sono verificati problemi con la distribuzione, vedere [Risolvere errori comuni durante la distribuzione di risorse in Azure con Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="dc913-169">If there were issues with the deployment, a next step would be to look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="dc913-170">Informazioni su come distribuire una macchina virtuale e le relative risorse di supporto sono disponibili in [Distribuire una macchina virtuale di Azure con C#](csharp.md).</span><span class="sxs-lookup"><span data-stu-id="dc913-170">Learn how to deploy a virtual machine and its supporting resources by reviewing [Deploy an Azure Virtual Machine Using C#](csharp.md).</span></span>
