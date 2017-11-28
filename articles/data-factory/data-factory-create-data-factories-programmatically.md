---
title: pipeline di dati aaaCreate tramite Azure .NET SDK | Documenti Microsoft
description: Informazioni su come tooprogrammatically creare, monitorare e gestire data factory di Azure con Data Factory SDK.
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
ms.openlocfilehash: 190b5f99edbb3c27e1e8efb8990b9e601b22458f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-monitor-and-manage-azure-data-factories-using-azure-data-factory-net-sdk"></a><span data-ttu-id="fb10c-103">Creazione, monitoraggio e gestione delle istanze di Azure Data Factory mediante Azure Data Factory .NET SDK</span><span class="sxs-lookup"><span data-stu-id="fb10c-103">Create, monitor, and manage Azure data factories using Azure Data Factory .NET SDK</span></span>
## <a name="overview"></a><span data-ttu-id="fb10c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="fb10c-104">Overview</span></span>
<span data-ttu-id="fb10c-105">È possibile creare, monitorare e gestire le istanze di Data factory di Azure a livello di codice mediante Data Factory .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="fb10c-105">You can create, monitor, and manage Azure data factories programmatically using Data Factory .NET SDK.</span></span> <span data-ttu-id="fb10c-106">Questo articolo contiene una procedura dettagliata che è possibile seguire toocreate un'applicazione console .NET di esempio che crea e controlla una data factory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-106">This article contains a walkthrough that you can follow toocreate a sample .NET console application that creates and monitors a data factory.</span></span> 

> [!NOTE]
> <span data-ttu-id="fb10c-107">In questo articolo non copre tutti hello API .NET di Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-107">This article does not cover all hello Data Factory .NET API.</span></span> <span data-ttu-id="fb10c-108">Per la documentazione completa sull'API .NET per Data Factory, vedere [Informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="fb10c-108">See [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1) for comprehensive documentation on .NET API for Data Factory.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="fb10c-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fb10c-109">Prerequisites</span></span>
* <span data-ttu-id="fb10c-110">Visual Studio 2012 o 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="fb10c-110">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="fb10c-111">Scaricare e installare [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fb10c-111">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>
* <span data-ttu-id="fb10c-112">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fb10c-112">Azure PowerShell.</span></span> <span data-ttu-id="fb10c-113">Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview) articolo tooinstall Azure PowerShell nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="fb10c-113">Follow instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="fb10c-114">Usare Azure PowerShell toocreate un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-114">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="fb10c-115">Creare un'applicazione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb10c-115">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="fb10c-116">Creare un'applicazione Azure Active Directory, creare un'entità servizio per un'applicazione hello e assegnarlo toohello **Data Factory collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-116">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="fb10c-117">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-117">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="fb10c-118">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb10c-118">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="fb10c-119">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="fb10c-119">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="fb10c-120">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fb10c-120">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="fb10c-121">Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="fb10c-121">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="fb10c-122">Prendere nota delle **SubscriptionId** e **TenantId** dall'output di hello del comando.</span><span class="sxs-lookup"><span data-stu-id="fb10c-122">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="fb10c-123">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="fb10c-123">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="fb10c-124">Se il gruppo di risorse hello esiste già, specificare se tooupdate è (Y) o mantenerlo come (N).</span><span class="sxs-lookup"><span data-stu-id="fb10c-124">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="fb10c-125">Se si utilizza un gruppo di risorse diverso, è necessario il nome hello toouse del gruppo di risorse al posto di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="fb10c-125">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="fb10c-126">Creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-126">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFDotNetWalkthroughApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfdotnetwalkthroughapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="fb10c-127">Se viene visualizzato il seguente errore hello, specificare un URL diverso ed eseguire nuovamente il comando di hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-127">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="fb10c-128">Creare hello dell'entità servizio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-128">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="fb10c-129">Aggiungere servizio principale toohello **Data Factory collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-129">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="fb10c-130">Ottieni ID applicazione hello</span><span class="sxs-lookup"><span data-stu-id="fb10c-130">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="fb10c-131">Annotare l'ID dell'applicazione hello (applicationID) dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-131">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="fb10c-132">Da questi passaggi si avranno i quattro valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb10c-132">You should have following four values from these steps:</span></span>

* <span data-ttu-id="fb10c-133">ID tenant</span><span class="sxs-lookup"><span data-stu-id="fb10c-133">Tenant ID</span></span>
* <span data-ttu-id="fb10c-134">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="fb10c-134">Subscription ID</span></span>
* <span data-ttu-id="fb10c-135">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="fb10c-135">Application ID</span></span>
* <span data-ttu-id="fb10c-136">Password (specificata nel primo comando hello)</span><span class="sxs-lookup"><span data-stu-id="fb10c-136">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="fb10c-137">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="fb10c-137">Walkthrough</span></span>
<span data-ttu-id="fb10c-138">In questa procedura dettagliata hello, creare una data factory con una pipeline che contiene un'attività di copia.</span><span class="sxs-lookup"><span data-stu-id="fb10c-138">In hello walkthrough, you create a data factory with a pipeline that contains a copy activity.</span></span> <span data-ttu-id="fb10c-139">attività di copia Hello copia dati da una cartella nella cartella tooanother di archiviazione blob di Azure in hello stesso nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="fb10c-139">hello copy activity copies data from a folder in your Azure blob storage tooanother folder in hello same blob storage.</span></span> 

<span data-ttu-id="fb10c-140">Attività di copia Hello esegue lo spostamento dei dati di hello in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-140">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="fb10c-141">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="fb10c-141">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="fb10c-142">Vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo per informazioni dettagliate sulle attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-142">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

1. <span data-ttu-id="fb10c-143">Creare un'applicazione console .NET in C# con Visual Studio 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="fb10c-143">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="fb10c-144">Avviare **Visual Studio** 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="fb10c-144">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="fb10c-145">Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-145">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="fb10c-146">Espandere **Modelli** e quindi selezionare **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-146">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="fb10c-147">In questa procedura dettagliata viene usato C#, ma è possibile usare qualsiasi linguaggio .NET.</span><span class="sxs-lookup"><span data-stu-id="fb10c-147">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="fb10c-148">Selezionare **applicazione Console** dall'elenco di hello dei tipi di progetto su hello destra.</span><span class="sxs-lookup"><span data-stu-id="fb10c-148">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="fb10c-149">Immettere **DataFactoryAPITestApp** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="fb10c-149">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="fb10c-150">Selezionare **C:\ADFGetStarted** per hello percorso.</span><span class="sxs-lookup"><span data-stu-id="fb10c-150">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="fb10c-151">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="fb10c-151">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="fb10c-152">Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-152">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="fb10c-153">In hello **Package Manager Console**, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="fb10c-153">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="fb10c-154">Eseguire hello pacchetto Data Factory tooinstall di comando seguente:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="fb10c-154">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="fb10c-155">Eseguire hello seguente pacchetto di Azure Active Directory tooinstall comando (utilizzare API di Active Directory nel codice hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="fb10c-155">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="fb10c-156">Sostituire il contenuto di hello di **app** file nel progetto hello con hello seguente contenuto:</span><span class="sxs-lookup"><span data-stu-id="fb10c-156">Replace hello contents of **App.config** file in hello project with hello following content:</span></span> 
    
    ```xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <appSettings>
            <add key="ActiveDirectoryEndpoint" value="https://login.microsoftonline.com/" />
            <add key="ResourceManagerEndpoint" value="https://management.azure.com/" />
            <add key="WindowsManagementUri" value="https://management.core.windows.net/" />

            <add key="ApplicationId" value="your application ID" />
            <add key="Password" value="Password you used while creating hello AAD application" />
            <add key="SubscriptionId" value= "Subscription ID" />
            <add key="ActiveDirectoryTenantId" value="Tenant ID" />
        </appSettings>
    </configuration>
    ```
5. <span data-ttu-id="fb10c-157">Nel file app. config hello, aggiornare i valori per  **&lt;ID applicazione&gt;**,  **&lt;Password&gt;**,  **&lt; ID sottoscrizione&gt;**, e  **&lt;ID tenant&gt;**  con valori personalizzati.</span><span class="sxs-lookup"><span data-stu-id="fb10c-157">In hello App.Config file, update values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>
6. <span data-ttu-id="fb10c-158">Aggiungere il seguente hello **utilizzando** istruzioni toohello **Program.cs** file nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-158">Add hello following **using** statements toohello **Program.cs** file in hello project.</span></span>

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
6. <span data-ttu-id="fb10c-159">Aggiungere hello dopo il codice che crea un'istanza di **DataPipelineManagementClient** classe toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-159">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="fb10c-160">Utilizzare questo toocreate oggetto una data factory, un servizio collegato, i set di dati di input e output e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="fb10c-160">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="fb10c-161">È inoltre possibile utilizzare le sezioni di toomonitor questo oggetto di un set di dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="fb10c-161">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client

    //IMPORTANT: specify hello name of Azure resource group here
    string resourceGroupName = "ADFTutorialResourceGroup";

    //IMPORTANT: hello name of hello data factory must be globally unique.
    // Therefore, update this value. For example:APITutorialFactory05122017
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="fb10c-162">Sostituire il valore di hello di **resourceGroupName** con il nome di hello del gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb10c-162">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span> <span data-ttu-id="fb10c-163">È possibile creare un gruppo di risorse utilizzando hello [New AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="fb10c-163">You can create a resource group using hello [New-AzureResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet.</span></span>
   >
   > <span data-ttu-id="fb10c-164">Aggiorna nome di hello toobe factory (dataFactoryName) di dati univoco.</span><span class="sxs-lookup"><span data-stu-id="fb10c-164">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="fb10c-165">Nome della data factory di hello deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="fb10c-165">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="fb10c-166">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="fb10c-166">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
7. <span data-ttu-id="fb10c-167">Aggiungere hello dopo il codice che crea un **data factory di** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-167">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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
8. <span data-ttu-id="fb10c-168">Aggiungere hello dopo il codice che crea un **servizio collegato di archiviazione di Azure** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-168">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="fb10c-169">Sostituire **storageaccountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb10c-169">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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
9. <span data-ttu-id="fb10c-170">Aggiungere hello dopo il codice che crea **set di dati di input e output** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-170">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    <span data-ttu-id="fb10c-171">Hello **FolderPath** per blob di input hello è troppo**adftutorial /** in **adftutorial** hello nome del contenitore di hello nell'archiviazione blob.</span><span class="sxs-lookup"><span data-stu-id="fb10c-171">hello **FolderPath** for hello input blob is set too**adftutorial/** where **adftutorial** is hello name of hello container in your blob storage.</span></span> <span data-ttu-id="fb10c-172">Se questo contenitore non esiste nell'archiviazione blob di Azure, creare un contenitore con lo stesso nome: **adftutorial** e caricare un contenitore di toohello file di testo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-172">If this container does not exist in your Azure blob storage, create a container with this name: **adftutorial** and upload a text file toohello container.</span></span>

    <span data-ttu-id="fb10c-173">output di Hello FolderPath per hello blob è impostato su: **adftutorial/apifactoryoutput / {Slice}** in **sezione** è calcolato in modo dinamico hello in base a valore di **SliceStart**(avvio di data e ora di ogni sezione).</span><span class="sxs-lookup"><span data-stu-id="fb10c-173">hello FolderPath for hello output blob is set to: **adftutorial/apifactoryoutput/{Slice}** where **Slice** is dynamically calculated based on hello value of **SliceStart** (start date-time of each slice.)</span></span>

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
10. <span data-ttu-id="fb10c-174">Aggiunta di codice seguente hello che **viene creato e attivato una pipeline** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-174">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="fb10c-175">Questa pipeline contiene una proprietà **CopyActivity** che accetta **BlobSource** come origine e **BlobSink** come sink.</span><span class="sxs-lookup"><span data-stu-id="fb10c-175">This pipeline has a **CopyActivity** that takes **BlobSource** as a source and **BlobSink** as a sink.</span></span>

    <span data-ttu-id="fb10c-176">Attività di copia Hello esegue lo spostamento dei dati di hello in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="fb10c-176">hello Copy Activity performs hello data movement in Azure Data Factory.</span></span> <span data-ttu-id="fb10c-177">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="fb10c-177">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="fb10c-178">Vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md) articolo per informazioni dettagliate sulle attività di copia hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-178">See [Data Movement Activities](data-factory-data-movement-activities.md) article for details about hello Copy Activity.</span></span>

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
    
                // Initial value for pipeline's active period. With this, you won't need tooset slice status
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
12. <span data-ttu-id="fb10c-179">Aggiungere i seguenti toohello codice hello **Main** metodo tooget hello stato una sezione di dati di hello set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="fb10c-179">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="fb10c-180">In questo esempio è prevista solo una sezione.</span><span class="sxs-lookup"><span data-stu-id="fb10c-180">There is only one slice expected in this sample.</span></span>

    ```csharp
    // Pulling status within a timeout threshold
    DateTime start = DateTime.Now;
    bool done = false;
    
    while (DateTime.Now - start < TimeSpan.FromMinutes(5) && !done)
    {
        Console.WriteLine("Pulling hello slice status");
        // wait before hello next status check
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
13. <span data-ttu-id="fb10c-181">**(facoltativo)**  Tooget eseguire dettagli per un toohello porzioni di dati di codice seguente di hello di Aggiungi **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="fb10c-181">**(optional)** Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

    ```csharp
    Console.WriteLine("Getting run details of a data slice");
    
    // give it a few minutes for hello output slice toobe ready
    Console.WriteLine("\nGive it a few minutes for hello output slice toobe ready and press any key.");
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
    
    Console.WriteLine("\nPress any key tooexit.");
    Console.ReadKey();
    ```
14. <span data-ttu-id="fb10c-182">Aggiungere hello seguente metodo helper utilizzato dal hello **Main** metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="fb10c-182">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span> <span data-ttu-id="fb10c-183">Questo metodo viene visualizzata una finestra di dialogo che consente di fornire **nome utente** e **password** utilizzare toolog nel portale tooAzure.</span><span class="sxs-lookup"><span data-stu-id="fb10c-183">This method pops a dialog box that that lets you provide **user name** and **password** that you use toolog in tooAzure portal.</span></span>

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

        throw new InvalidOperationException("Failed tooacquire token");
    }
    ```

15. <span data-ttu-id="fb10c-184">In Esplora soluzioni hello, espandere il progetto di hello: **DataFactoryAPITestApp**, fare doppio clic su **riferimenti**, fare clic su **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-184">In hello Solution Explorer, expand hello project: **DataFactoryAPITestApp**, right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="fb10c-185">Selezionare la casella di controllo per l'assembly `System.Configuration` e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-185">Select check box for `System.Configuration` assembly and click **OK**.</span></span>
15. <span data-ttu-id="fb10c-186">Compilare un'applicazione console hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-186">Build hello console application.</span></span> <span data-ttu-id="fb10c-187">Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-187">Click **Build** on hello menu and click **Build Solution**.</span></span>
16. <span data-ttu-id="fb10c-188">Verificare che esista almeno un file nel contenitore adftutorial hello nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="fb10c-188">Confirm that there is at least one file in hello adftutorial container in your Azure blob storage.</span></span> <span data-ttu-id="fb10c-189">In caso contrario, creare file Emp.txt nel blocco note con hello seguente contenuto e caricarlo toohello adftutorial contenitore.</span><span class="sxs-lookup"><span data-stu-id="fb10c-189">If not, create Emp.txt file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
17. <span data-ttu-id="fb10c-190">Eseguire l'esempio hello facendo **Debug** -> **Avvia debug** menu hello.</span><span class="sxs-lookup"><span data-stu-id="fb10c-190">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="fb10c-191">Quando viene visualizzato hello **dettagli di una sezione di dati di esecuzione**, attendere qualche minuto e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-191">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
18. <span data-ttu-id="fb10c-192">Utilizzare hello tooverify portale Azure data factory di tale hello **APITutorialFactory** viene creato con hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fb10c-192">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
    * <span data-ttu-id="fb10c-193">Servizio collegato: **AzureStorageLinkedService**</span><span class="sxs-lookup"><span data-stu-id="fb10c-193">Linked service: **AzureStorageLinkedService**</span></span>
    * <span data-ttu-id="fb10c-194">Set di dati: **DatasetBlobSource** e **DatasetBlobDestination**.</span><span class="sxs-lookup"><span data-stu-id="fb10c-194">Dataset: **DatasetBlobSource** and **DatasetBlobDestination**.</span></span>
    * <span data-ttu-id="fb10c-195">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="fb10c-195">Pipeline: **PipelineBlobSample**</span></span>
19. <span data-ttu-id="fb10c-196">Verificare che un file di output venga creato in hello **apifactoryoutput** cartella hello **adftutorial** contenitore.</span><span class="sxs-lookup"><span data-stu-id="fb10c-196">Verify that an output file is created in hello **apifactoryoutput** folder in hello **adftutorial** container.</span></span>

## <a name="get-a-list-of-failed-data-slices"></a><span data-ttu-id="fb10c-197">Ottenere un elenco di sezioni di dati non riusciti</span><span class="sxs-lookup"><span data-stu-id="fb10c-197">Get a list of failed data slices</span></span> 

```csharp
// Parse hello resource path
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

## <a name="next-steps"></a><span data-ttu-id="fb10c-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fb10c-198">Next steps</span></span>
<span data-ttu-id="fb10c-199">Vedere hello di esempio per la creazione di una pipeline mediante .NET SDK che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure seguente:</span><span class="sxs-lookup"><span data-stu-id="fb10c-199">See hello following example for creating a pipeline using .NET SDK that copies data from an Azure blob storage tooan Azure SQL database:</span></span> 

- [<span data-ttu-id="fb10c-200">Creare una pipeline di dati toocopy da archiviazione Blob tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="fb10c-200">Create a pipeline toocopy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)
