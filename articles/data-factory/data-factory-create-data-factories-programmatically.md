---
title: Creare pipeline di dati usando Azure .NET SDK | Documentazione Microsoft
description: Informazioni su come creare, monitorare e gestire a livello di codice le istanze di Data factory di Azure usando Data Factory SDK.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: b0a357be-3040-4789-831e-0d0a32a0bda5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 9d9dac75321c5d4e079f49320d9b7c6f56e48754
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="e3b80-103">Creazione, monitoraggio e gestione delle istanze di Azure Data Factory mediante Azure Data Factory .NET SDK</span><span class="sxs-lookup"><span data-stu-id="e3b80-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="e3b80-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="e3b80-104">Overview</span></span>
<span data-ttu-id="e3b80-105">È possibile creare, monitorare e gestire le istanze di Data factory di Azure a livello di codice mediante Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e3b80-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="e3b80-106">Questo articolo contiene una procedura dettagliata per la creazione di un'applicazione console .NET di esempio che crea e monitora un'istanza di Data factory.</span><span class="sxs-lookup"><span data-stu-id="e3b80-106">This article contains a walkthrough that you can follow to create a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="e3b80-107">Questo articolo non descrive tutte le API .NET di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e3b80-107">This article does not cover all the Data Factory .NET API.</span></span> <span data-ttu-id="e3b80-108">Per la documentazione completa sull'API .NET per Data Factory, vedere [Informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="e3b80-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="e3b80-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="e3b80-109">Prerequisites</span></span>
* <span data-ttu-id="e3b80-110">Visual Studio 2012 o 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="e3b80-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="e3b80-111">Scaricare e installare [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e3b80-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="e3b80-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b80-112">Azure PowerShell.</span></span> <span data-ttu-id="e3b80-113">Seguire le istruzioni disponibili nell'articolo [Come installare e configurare Azure PowerShell](/powershell/azure/overview) per installare la versione più recente di Azure PowerShell nel computer.</span><span class="sxs-lookup"><span data-stu-id="e3b80-113">Follow instructions in [How to install and configure Azure PowerShell](/powershell/azure/overview) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="e3b80-114">Azure PowerShell verrà usato per creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e3b80-114">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="e3b80-115">Creare un'applicazione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e3b80-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="e3b80-116">Creare l'applicazione Azure Active Directory, creare un'entità servizio per l'applicazione e assegnarla al ruolo **Collaboratore Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="e3b80-116">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="e3b80-117">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="e3b80-118">Eseguire il comando seguente e immettere il nome utente e la password usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b80-118">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="e3b80-119">Eseguire il comando seguente per visualizzare tutte le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="e3b80-119">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="e3b80-120">Eseguire il comando seguente per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="e3b80-120">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="e3b80-121">Sostituire **&lt;NameOfAzureSubscription**&gt; con il nome della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b80-121">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e3b80-122">Dall'output del comando prendere nota dei valori di **SubscriptionId** e **TenantId**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-122">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="e3b80-123">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo il comando seguente in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e3b80-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="e3b80-124">Se il gruppo di risorse esiste già, specificare se deve essere aggiornato (Y) o mantenuto invariato (N).</span><span class="sxs-lookup"><span data-stu-id="e3b80-124">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="e3b80-125">Se si usa un gruppo di risorse diverso, è necessario usare il nome del gruppo di risorse invece di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="e3b80-125">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="e3b80-126">Creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e3b80-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="e3b80-127">Se viene visualizzato l'errore seguente, specificare un URL diverso ed eseguire di nuovo il comando.</span><span class="sxs-lookup"><span data-stu-id="e3b80-127">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="e3b80-128">Creare l'entità servizio di AD.</span><span class="sxs-lookup"><span data-stu-id="e3b80-128">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="e3b80-129">Aggiungere l'entità servizio al ruolo **Collaboratore Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="e3b80-129">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="e3b80-130">Ottenere l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="e3b80-130">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="e3b80-131">Annotare l'ID applicazione (applicationID) dall'output.</span><span class="sxs-lookup"><span data-stu-id="e3b80-131">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="e3b80-132">Da questi passaggi si avranno i quattro valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3b80-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="e3b80-133">ID tenant</span><span class="sxs-lookup"><span data-stu-id="e3b80-133">Tenant ID</span></span>
* <span data-ttu-id="e3b80-134">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e3b80-134">Subscription ID</span></span>
* <span data-ttu-id="e3b80-135">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="e3b80-135">Application ID</span></span>
* <span data-ttu-id="e3b80-136">Password (specificata nel primo comando)</span><span class="sxs-lookup"><span data-stu-id="e3b80-136">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="e3b80-137">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="e3b80-137">Walkthrough</span></span>
<span data-ttu-id="e3b80-138">Nella procedura dettagliata, si crea una data factory con una pipeline contenente un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="e3b80-138">In the walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="e3b80-139">L'attività di copia copia i dati da una cartella nell'archivio BLOB di Azure in un'altra cartella dello stesso archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e3b80-139">The copy activity copies data from a folder in your Azure blob storage to another folder in the same blob storage.</span></span> 

<span data-ttu-id="e3b80-140">L'attività di copia esegue lo spostamento dei dati in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e3b80-140">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="e3b80-141">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="e3b80-141">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e3b80-142">Per informazioni dettagliate sull'attività di copia, vedere [Attività di spostamento dei dati](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="e3b80-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

1. <span data-ttu-id="e3b80-143">Creare un'applicazione console .NET in C# con Visual Studio 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="e3b80-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="e3b80-144">Avviare **Visual Studio** 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="e3b80-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="e3b80-145">Fare clic su **File**, scegliere **Nuovo** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-145">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="e3b80-146">Espandere **Modelli** e quindi selezionare **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="e3b80-147">In questa procedura dettagliata viene usato C#, ma è possibile usare qualsiasi linguaggio .NET.</span><span class="sxs-lookup"><span data-stu-id="e3b80-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="e3b80-148">Selezionare **Applicazione console** dall'elenco dei tipi di progetto a destra.</span><span class="sxs-lookup"><span data-stu-id="e3b80-148">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="e3b80-149">Immettere **DataFactoryAPITestApp** per Nome.</span><span class="sxs-lookup"><span data-stu-id="e3b80-149">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="e3b80-150">Selezionare **C:\ADFGetStarted** come percorso.</span><span class="sxs-lookup"><span data-stu-id="e3b80-150">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="e3b80-151">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="e3b80-151">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="e3b80-152">Fare clic su **Strumenti**, scegliere **Gestione pacchetti NuGet** e quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-152">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="e3b80-153">Nella finestra **Console di Gestione pacchetti** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="e3b80-153">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="e3b80-154">Eseguire questo comando per installare il pacchetto di Data factory: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="e3b80-154">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="e3b80-155">Eseguire questo comando per installare il pacchetto di Azure Active Directory. Nel codice viene usata l'API di Active Directory: `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="e3b80-155">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="e3b80-156">Sostituire il contenuto del file **App.config** nel progetto con il contenuto seguente:</span><span class="sxs-lookup"><span data-stu-id="e3b80-156">Replace the contents of **App.config** file in the project with the following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating the AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="e3b80-157">Nel file App.Config, aggiornare i valori di **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** e **&lt;tenant ID&gt;** con i propri valori.</span><span class="sxs-lookup"><span data-stu-id="e3b80-157">In the App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="e3b80-158">Aggiungere le seguenti istruzioni **using** al file **Program.cs** nel progetto.</span><span class="sxs-lookup"><span data-stu-id="e3b80-158">Add the following **using** statements to the **Program.cs** file in the project.</span></span>

    ```csharp
    using System.Configuration;
    using System.Collections.ObjectModel;
    using System.Threading;
    using System.Threading.Tasks;

    using Microsoft.Azure;
    using Microsoft.Azure.Management.DataFactories;
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Common.Models;

    using Microsoft.IdentityModel.Clients.ActiveDirectory;

    ```
6. <span data-ttu-id="e3b80-159">Aggiungere al metodo **Main** il codice seguente che crea un'istanza della classe **DataPipelineManagementClient**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-159">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="e3b80-160">Si userà questo oggetto per creare una data factory, un servizio collegato, i set di dati di input e output e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="e3b80-160">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="e3b80-161">Questo oggetto viene usato anche per monitorare le sezioni di un set di dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e3b80-161">You also use this object to monitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify the name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: the name of the data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="e3b80-162">Sostituire il valore di **resourceGroupName** con il nome del gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b80-162">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span> <span data-ttu-id="e3b80-163">Per creare un gruppo di risorse, usare il cmdlet [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) .</span><span class="sxs-lookup"><span data-stu-id="e3b80-163">You can create a resource group using the [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="e3b80-164">Aggiornare il nome della data factory (dataFactoryName) in modo che sia univoco.</span><span class="sxs-lookup"><span data-stu-id="e3b80-164">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="e3b80-165">Il nome della data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="e3b80-165">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="e3b80-166">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="e3b80-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="e3b80-167">Aggiungere al metodo **Main** il codice seguente che crea una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-167">Add the following code that creates a **data factory** to the **Main** method.</span></span>

    ```csharp
    // create a data factory
    Console.WriteLine("Creating a data factory");
    client.DataFactories.CreateOrUpdate(resourceGroupName,
        new DataFactoryCreateOrUpdateParameters()
        {
            DataFactory = new DataFactory()
            {
                Name = dataFactoryName,
                Location = "westus",
                Properties = new DataFactoryProperties()
            }
        }
    );
    ```
8. <span data-ttu-id="e3b80-168">Aggiungere al metodo **Main** il codice seguente che crea un **servizio collegato di Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-168">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="e3b80-169">Sostituire **storageaccountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b80-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

    ```csharp
    // create a linked service for input data store: Azure Storage
    Console.WriteLine("Creating Azure Storage linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureStorageLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureStorageLinkedService("DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<accountkey>")
                )
            }
        }
    );
    ```
9. <span data-ttu-id="e3b80-170">Aggiungere al metodo **Main** il codice seguente che crea **set di dati di input e output**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-170">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

    <span data-ttu-id="e3b80-171">**FolderPath** per il BLOB di input è impostato su **adftutorial/**, dove **adftutorial** è il nome del contenitore nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="e3b80-171">The **FolderPath** for the input blob is set to **adftutorial/** where **adftutorial** is the name of the container in your blob storage.</span></span> <span data-ttu-id="e3b80-172">Se questo contenitore non esiste nell'archivio BLOB di Azure, creare un contenitore con il nome **adftutorial** e caricare un file di testo nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="e3b80-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file to the container.</span></span>

    <span data-ttu-id="e3b80-173">FolderPath per il BLOB di output è impostato su **adftutorial/apifactoryoutput/{Slice}**, dove il valore **Slice** è calcolato in modo dinamico in base al valore **SliceStart** (data-ora di inizio di ogni sezione).</span><span class="sxs-lookup"><span data-stu-id="e3b80-173">The FolderPath for the output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on the value of **SliceStart** (start date-time of each slice.)</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "DatasetBlobSource";
    string Dataset_Destination = "DatasetBlobDestination";
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/",
                    FileName = "emp.txt"
                },
                External = true,
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
    
                Policy = new Policy()
                {
                    Validation = new ValidationPolicy()
                    {
                        MinimumRows = 1
                    }
                }
            }
        }
    });
    
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Destination,
            Properties = new DatasetProperties()
            {
    
                LinkedServiceName = "AzureStorageLinkedService",
                TypeProperties = new AzureBlobDataset()
                {
                    FolderPath = "adftutorial/apifactoryoutput/{Slice}",
                    PartitionedBy = new Collection<Partition>()
                    {
                        new Partition()
                        {
                            Name = "Slice",
                            Value = new DateTimePartitionValue()
                            {
                                Date = "SliceStart",
                                Format = "yyyyMMdd-HH"
                            }
                        }
                    }
                },
    
                Availability = new Availability()
                {
                    Frequency = SchedulePeriod.Hour,
                    Interval = 1,
                },
            }
        }
    });
    ```
10. <span data-ttu-id="e3b80-174">Aggiungere al metodo **Main** il codice seguente che **crea e attiva una pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-174">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="e3b80-175">Questa pipeline contiene una proprietà **CopyActivity** che accetta **BlobSource** come origine e **BlobSink** come sink.</span><span class="sxs-lookup"><span data-stu-id="e3b80-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="e3b80-176">L'attività di copia esegue lo spostamento dei dati in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e3b80-176">The Copy Activity performs the data movement in Azure Data Factory.</span></span> <span data-ttu-id="e3b80-177">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="e3b80-177">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="e3b80-178">Per informazioni dettagliate sull'attività di copia, vedere [Attività di spostamento dei dati](data-factory-data-movement-activities.md) .</span><span class="sxs-lookup"><span data-stu-id="e3b80-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about the Copy Activity.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2014, 8, 9, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = PipelineActivePeriodStartTime.AddMinutes(60);
    string PipelineName = "PipelineBlobSample";
    
    client.Pipelines.CreateOrUpdate(resourceGroupName, dataFactoryName,
    new PipelineCreateOrUpdateParameters()
    {
        Pipeline = new Pipeline()
        {
            Name = PipelineName,
            Properties = new PipelineProperties()
            {
                Description = "Demo Pipeline for data transfer between blobs",
    
                // Initial value for pipeline's active period. With this, you won't need to set slice status
                Start = PipelineActivePeriodStartTime,
                End = PipelineActivePeriodEndTime,
    
                Activities = new List<Activity>()
                {
                    new Activity()
                    {
                        Name = "BlobToBlob",
                        Inputs = new List<ActivityInput>()
                        {
                            new ActivityInput()
                {
                                Name = Dataset_Source
                            }
                        },
                        Outputs = new List<ActivityOutput>()
                        {
                            new ActivityOutput()
                            {
                                Name = Dataset_Destination
                            }
                        },
                        TypeProperties = new CopyActivity()
                        {
                            Source = new BlobSource(),
                            Sink = new BlobSink()
                            {
                                WriteBatchSize = 10000,
                                WriteBatchTimeout = TimeSpan.FromMinutes(10)
                            }
                        }
                    }
    
                },
            }
        }
    });
    ```
12. <span data-ttu-id="e3b80-179">Aggiungere al metodo **Main** il codice seguente per ottenere lo stato di una sezione di dati del set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="e3b80-179">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="e3b80-180">In questo esempio è prevista solo una sezione.</span><span class="sxs-lookup"><span data-stu-id="e3b80-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling the slice status");
        // wait before the next status check
        Thread.Sleep(1000 * 12);
    
        var datalistResponse = client.DataSlices.List(resourceGroupName, dataFactoryName, Dataset_Destination,
            new DataSliceListParameters()
            {
                DataSliceRangeStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString(),
                DataSliceRangeEndTime = PipelineActivePeriodEndTime.ConvertToISO8601DateTimeString()
            });
    
        foreach (DataSlice slice in datalistResponse.DataSlices)
        {
            if (slice.State == DataSliceState.Failed || slice.State == DataSliceState.Ready)
            {
                Console.WriteLine("Slice execution is done with status: {0}", slice.State);
                done = true;
                break;
            }
            else
            {
                Console.WriteLine("Slice status is: {0}", slice.State);
            }
        }
    }
    ```
13. <span data-ttu-id="e3b80-181">**(facoltativo)** Aggiungere al metodo **Main** il codice seguente per ottenere i dettagli dell'esecuzione di una sezione di dati.</span><span class="sxs-lookup"><span data-stu-id="e3b80-181">**(optional)** Add the following code to get run details for a data slice to the **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for the output slice to be ready
    Console.WriteLine("\nGive it a few minutes for the output slice to be ready and press any key.");
    Console.ReadKey();
    
    var datasliceRunListResponse = client.DataSliceRuns.List(
        resourceGroupName,
        dataFactoryName,
        Dataset_Destination,
        new DataSliceRunListParameters()
        {
            DataSliceStartTime = PipelineActivePeriodStartTime.ConvertToISO8601DateTimeString()
        });
    
    foreach (DataSliceRun run in datasliceRunListResponse.DataSliceRuns)
    {
        Console.WriteLine("Status: \t\t{0}", run.Status);
        Console.WriteLine("DataSliceStart: \t{0}", run.DataSliceStart);
        Console.WriteLine("DataSliceEnd: \t\t{0}", run.DataSliceEnd);
        Console.WriteLine("ActivityId: \t\t{0}", run.ActivityName);
        Console.WriteLine("ProcessingStartTime: \t{0}", run.ProcessingStartTime);
        Console.WriteLine("ProcessingEndTime: \t{0}", run.ProcessingEndTime);
        Console.WriteLine("ErrorMessage: \t{0}", run.ErrorMessage);
    }
    
    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="e3b80-182">Aggiungere alla classe **Program** il metodo helper seguente usato per il metodo **Main**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-182">Add the following helper method used by the **Main** method to the **Program** class.</span></span> <span data-ttu-id="e3b80-183">Questo metodo visualizza una finestra di dialogo che consente di specificare il **nome utente** e la **password** usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b80-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use to log in to Azure portal.</span></span>

    ```csharp
    public static async Task<string> GetAuthorizationHeader()
    {
        AuthenticationContext context = new AuthenticationContext(ConfigurationManager.AppSettings["ActiveDirectoryEndpoint"] + ConfigurationManager.AppSettings["ActiveDirectoryTenantId"]);
        ClientCredential credential = new ClientCredential(
            ConfigurationManager.AppSettings["ApplicationId"],
            ConfigurationManager.AppSettings["Password"]);
        AuthenticationResult result = await context.AcquireTokenAsync(
            resource: ConfigurationManager.AppSettings["WindowsManagementUri"],
            clientCredential: credential);

        if (result != null)
            return result.AccessToken;

        throw new InvalidOperationException("Failed to acquire token");
    }
    ```

15. <span data-ttu-id="e3b80-184">In Esplora soluzioni espandere il progetto **DataFactoryAPITestApp**, fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-184">In the Solution Explorer, expand the project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="e3b80-185">Selezionare la casella di controllo per l'assembly `System.Configuration` e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="e3b80-186">Compilare l'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="e3b80-186">Build the console application.</span></span> <span data-ttu-id="e3b80-187">Scegliere **Compila** dal menu e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-187">Click **Build** on the menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="e3b80-188">Verificare che esista almeno un file nel contenitore adftutorial nell'archiviazione BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="e3b80-188">Confirm that there is at least one file in the adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="e3b80-189">In caso contrario, creare il file Emp.txt nel Blocco note con il contenuto seguente e caricarlo nel contenitore adftutorial.</span><span class="sxs-lookup"><span data-stu-id="e3b80-189">If not, create Emp.txt file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="e3b80-190">Eseguire l'esempio scegliendo **Debug** -> **Avvia debug** dal menu.</span><span class="sxs-lookup"><span data-stu-id="e3b80-190">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="e3b80-191">Quando viene visualizzato un messaggio simile ad **Acquisizione dettagli dell'esecuzione di una sezione di dati**, attendere qualche minuto e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-191">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="e3b80-192">Usare il portale di Azure per verificare che la data factory **APITutorialFactory** venga creata con gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e3b80-192">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
    * <span data-ttu-id="e3b80-193">Servizio collegato: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="e3b80-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="e3b80-194">Set di dati: **DatasetBlobSource** e **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="e3b80-195">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="e3b80-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="e3b80-196">Verificare che venga creato un file di output nella cartella **apifactoryoutput** nel contenitore **adftutorial**.</span><span class="sxs-lookup"><span data-stu-id="e3b80-196">Verify that an output file is created in the **apifactoryoutput** folder in the **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="e3b80-197">Ottenere un elenco di sezioni di dati non riusciti</span><span class="sxs-lookup"><span data-stu-id="e3b80-197">Get a list of failed data slices</span></span> 

```csharp
// Parse the resource path
var ResourceGroupName = "ADFTutorialResourceGroup";
var DataFactoryName = "DataFactoryAPITestApp";

var parameters = new ActivityWindowsByDataFactoryListParameters(ResourceGroupName, DataFactoryName);
parameters.WindowState = "Failed";
var response = dataFactoryManagementClient.ActivityWindows.List(parameters);
do
{
    foreach (var activityWindow in response.ActivityWindowListResponseValue.ActivityWindows)
    {
        var row = string.Join(
            "\t",
            activityWindow.WindowStart.ToString(),
            activityWindow.WindowEnd.ToString(),
            activityWindow.RunStart.ToString(),
            activityWindow.RunEnd.ToString(),
            activityWindow.DataFactoryName,
            activityWindow.PipelineName,
            activityWindow.ActivityName,
            string.Join(",", activityWindow.OutputDatasets));
        Console.WriteLine(row);
    }

    if (response.NextLink != null)
    {
        response = dataFactoryManagementClient.ActivityWindows.ListNext(response.NextLink, parameters);
    }
    else
    {
        response = null;
    }
}
while (response != null);
```

## <a name="next-steps"></a><span data-ttu-id="e3b80-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e3b80-198">Next steps</span></span>
<span data-ttu-id="e3b80-199">Vedere l'esempio seguente per la creazione di una pipeline mediante .NET SDK che copia i dati da un archivio BLOB di Azure a un database SQL Azure:</span><span class="sxs-lookup"><span data-stu-id="e3b80-199">See the following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage to an Azure SQL database:</span></span> 

- [<span data-ttu-id="e3b80-200">Creare una pipeline per copiare i dati dall'archivio BLOB al database SQL</span><span class="sxs-lookup"><span data-stu-id="e3b80-200">Create a pipeline to copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
