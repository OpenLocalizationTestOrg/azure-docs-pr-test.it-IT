---
title: "Esercitazione: Creare una pipeline con l'attività di copia usando l'API .NET | Documentazione Microsoft"
description: "In questa esercitazione viene creata una pipeline di Azure Data Factory con un'attività di copia usando l'API .NET."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 58fc4007-b46d-4c8e-a279-cb9e479b3e2b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: 52f72da54cdd80691e09d7453bf6730454c4089e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="b80f4-103">Esercitazione: Creare una pipeline con l'attività di copia usando l'API .NET</span><span class="sxs-lookup"><span data-stu-id="b80f4-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b80f4-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b80f4-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="b80f4-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="b80f4-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="b80f4-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b80f4-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="b80f4-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b80f4-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="b80f4-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b80f4-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="b80f4-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="b80f4-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="b80f4-110">API REST</span><span class="sxs-lookup"><span data-stu-id="b80f4-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="b80f4-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="b80f4-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="b80f4-112">In questo articolo viene illustrato come toouse [API .NET](https://portal.azure.com) toocreate una data factory con una pipeline che copia i dati da un database di SQL Azure tooan di archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-112">In this article, you learn how toouse [.NET API](https://portal.azure.com) toocreate a data factory with a pipeline that copies data from an Azure blob storage tooan Azure SQL database.</span></span> <span data-ttu-id="b80f4-113">Se si tooAzure nuova Data Factory, leggere hello [tooAzure introduzione Data Factory](data-factory-introduction.md) articolo prima di eseguire questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-113">If you are new tooAzure Data Factory, read through hello [Introduction tooAzure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="b80f4-114">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="b80f4-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="b80f4-115">attività di copia Hello copia dati da un archivio dati di sink supportati tooa di archivio di dati supportati.</span><span class="sxs-lookup"><span data-stu-id="b80f4-115">hello copy activity copies data from a supported data store tooa supported sink data store.</span></span> <span data-ttu-id="b80f4-116">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b80f4-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b80f4-117">attività Hello è alimentato da un servizio disponibile a livello globale che è possibile copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="b80f4-117">hello activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="b80f4-118">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b80f4-118">For more information about hello Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="b80f4-119">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="b80f4-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="b80f4-120">Inoltre, è possibile concatenare le due attività (eseguire un'attività dopo l'altro) mediante l'impostazione di set di dati di hello output di un'attività come hello input set di dati di hello altre attività.</span><span class="sxs-lookup"><span data-stu-id="b80f4-120">And, you can chain two activities (run one activity after another) by setting hello output dataset of one activity as hello input dataset of hello other activity.</span></span> <span data-ttu-id="b80f4-121">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="b80f4-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="b80f4-122">Per la documentazione completa sull'API .NET per Data Factory, vedere le [informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="b80f4-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="b80f4-123">pipeline di dati Hello in questa esercitazione consente di copiare dati da un archivio dati di origine dati archivio tooa destinazione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-123">hello data pipeline in this tutorial copies data from a source data store tooa destination data store.</span></span> <span data-ttu-id="b80f4-124">Per un'esercitazione su come dati di tootransform tramite Data Factory di Azure, vedere [esercitazione: creare una pipeline di dati tootransform utilizzando cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="b80f4-124">For a tutorial on how tootransform data using Azure Data Factory, see [Tutorial: Build a pipeline tootransform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b80f4-125">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b80f4-125">Prerequisites</span></span>
* <span data-ttu-id="b80f4-126">Seguire i passaggi [esercitazione panoramica e prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget una panoramica di esercitazione hello e hello completo **prerequisito** passaggi.</span><span class="sxs-lookup"><span data-stu-id="b80f4-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) tooget an overview of hello tutorial and complete hello **prerequisite** steps.</span></span>
* <span data-ttu-id="b80f4-127">Visual Studio 2012 o 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="b80f4-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="b80f4-128">Scaricare e installare [.NET SDK di Azure](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b80f4-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="b80f4-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b80f4-129">Azure PowerShell.</span></span> <span data-ttu-id="b80f4-130">Seguire le istruzioni [come tooinstall e configurare Azure PowerShell](../powershell-install-configure.md) articolo tooinstall Azure PowerShell nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="b80f4-130">Follow instructions in [How tooinstall and configure Azure PowerShell](../powershell-install-configure.md) article tooinstall Azure PowerShell on your computer.</span></span> <span data-ttu-id="b80f4-131">Usare Azure PowerShell toocreate un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b80f4-131">You use Azure PowerShell toocreate an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="b80f4-132">Creare un'applicazione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b80f4-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="b80f4-133">Creare un'applicazione Azure Active Directory, creare un'entità servizio per un'applicazione hello e assegnarlo toohello **Data Factory collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-133">Create an Azure Active Directory application, create a service principal for hello application, and assign it toohello **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="b80f4-134">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="b80f4-135">Eseguire hello comando seguente e immettere nome utente hello e la password usati toosign in toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-135">Run hello following command and enter hello user name and password that you use toosign in toohello Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="b80f4-136">Eseguire hello successivo comando tooview tutte le sottoscrizioni di hello per questo account.</span><span class="sxs-lookup"><span data-stu-id="b80f4-136">Run hello following command tooview all hello subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="b80f4-137">Sottoscrizione hello tooselect da toowork con il comando seguente hello esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-137">Run hello following command tooselect hello subscription that you want toowork with.</span></span> <span data-ttu-id="b80f4-138">Sostituire  **&lt;NameOfAzureSubscription** &gt; con nome hello della sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-138">Replace **&lt;NameOfAzureSubscription**&gt; with hello name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="b80f4-139">Prendere nota delle **SubscriptionId** e **TenantId** dall'output di hello del comando.</span><span class="sxs-lookup"><span data-stu-id="b80f4-139">Note down **SubscriptionId** and **TenantId** from hello output of this command.</span></span>

5. <span data-ttu-id="b80f4-140">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo hello comando in hello PowerShell seguente.</span><span class="sxs-lookup"><span data-stu-id="b80f4-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running hello following command in hello PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="b80f4-141">Se il gruppo di risorse hello esiste già, specificare se tooupdate è (Y) o mantenerlo come (N).</span><span class="sxs-lookup"><span data-stu-id="b80f4-141">If hello resource group already exists, you specify whether tooupdate it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="b80f4-142">Se si utilizza un gruppo di risorse diverso, è necessario il nome hello toouse del gruppo di risorse al posto di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-142">If you use a different resource group, you need toouse hello name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="b80f4-143">Creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b80f4-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="b80f4-144">Se viene visualizzato il seguente errore hello, specificare un URL diverso ed eseguire nuovamente il comando di hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-144">If you get hello following error, specify a different URL and run hello command again.</span></span>
    
    ```PowerShell
    Another object with hello same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="b80f4-145">Creare hello dell'entità servizio Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b80f4-145">Create hello AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="b80f4-146">Aggiungere servizio principale toohello **Data Factory collaboratore** ruolo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-146">Add service principal toohello **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="b80f4-147">Ottieni ID applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b80f4-147">Get hello application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="b80f4-148">Annotare l'ID dell'applicazione hello (applicationID) dall'output di hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-148">Note down hello application ID (applicationID) from hello output.</span></span>

<span data-ttu-id="b80f4-149">Da questi passaggi si avranno i quattro valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="b80f4-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="b80f4-150">ID tenant</span><span class="sxs-lookup"><span data-stu-id="b80f4-150">Tenant ID</span></span>
* <span data-ttu-id="b80f4-151">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="b80f4-151">Subscription ID</span></span>
* <span data-ttu-id="b80f4-152">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="b80f4-152">Application ID</span></span>
* <span data-ttu-id="b80f4-153">Password (specificata nel primo comando hello)</span><span class="sxs-lookup"><span data-stu-id="b80f4-153">Password (specified in hello first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="b80f4-154">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="b80f4-154">Walkthrough</span></span>
1. <span data-ttu-id="b80f4-155">Creare un'applicazione console .NET in C# con Visual Studio 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="b80f4-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="b80f4-156">Avviare **Visual Studio** 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="b80f4-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="b80f4-157">Fare clic su **File**, punto troppo**New**, fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-157">Click **File**, point too**New**, and click **Project**.</span></span>
   3. <span data-ttu-id="b80f4-158">Espandere **Modelli** e quindi selezionare **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="b80f4-159">In questa procedura dettagliata viene usato C#, ma è possibile usare qualsiasi linguaggio .NET.</span><span class="sxs-lookup"><span data-stu-id="b80f4-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="b80f4-160">Selezionare **applicazione Console** dall'elenco di hello dei tipi di progetto su hello destra.</span><span class="sxs-lookup"><span data-stu-id="b80f4-160">Select **Console Application** from hello list of project types on hello right.</span></span>
   5. <span data-ttu-id="b80f4-161">Immettere **DataFactoryAPITestApp** per hello Name.</span><span class="sxs-lookup"><span data-stu-id="b80f4-161">Enter **DataFactoryAPITestApp** for hello Name.</span></span>
   6. <span data-ttu-id="b80f4-162">Selezionare **C:\ADFGetStarted** per hello percorso.</span><span class="sxs-lookup"><span data-stu-id="b80f4-162">Select **C:\ADFGetStarted** for hello Location.</span></span>
   7. <span data-ttu-id="b80f4-163">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="b80f4-163">Click **OK** toocreate hello project.</span></span>
2. <span data-ttu-id="b80f4-164">Fare clic su **strumenti**, punto troppo**Gestione pacchetti NuGet**, fare clic su **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-164">Click **Tools**, point too**NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="b80f4-165">In hello **Package Manager Console**, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b80f4-165">In hello **Package Manager Console**, do hello following steps:</span></span>
   1. <span data-ttu-id="b80f4-166">Eseguire hello pacchetto Data Factory tooinstall di comando seguente:`Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="b80f4-166">Run hello following command tooinstall Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="b80f4-167">Eseguire hello seguente pacchetto di Azure Active Directory tooinstall comando (utilizzare API di Active Directory nel codice hello):`Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="b80f4-167">Run hello following command tooinstall Azure Active Directory package (you use Active Directory API in hello code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="b80f4-168">Aggiungere il seguente hello **appSetttings** sezione toohello **app** file.</span><span class="sxs-lookup"><span data-stu-id="b80f4-168">Add hello following **appSetttings** section toohello **App.config** file.</span></span> <span data-ttu-id="b80f4-169">Queste impostazioni vengono utilizzate dal metodo di supporto hello: **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-169">These settings are used by hello helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="b80f4-170">Sostituire i valori di **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** e **&lt;tenant ID&gt;** con i propri valori.</span><span class="sxs-lookup"><span data-stu-id="b80f4-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="b80f4-171">Aggiungere il seguente hello **utilizzando** istruzioni toohello file di origine (Program.cs) nel progetto hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-171">Add hello following **using** statements toohello source file (Program.cs) in hello project.</span></span>

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

6. <span data-ttu-id="b80f4-172">Aggiungere hello dopo il codice che crea un'istanza di **DataPipelineManagementClient** classe toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-172">Add hello following code that creates an instance of **DataPipelineManagementClient** class toohello **Main** method.</span></span> <span data-ttu-id="b80f4-173">Utilizzare questo toocreate oggetto una data factory, un servizio collegato, i set di dati di input e output e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="b80f4-173">You use this object toocreate a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="b80f4-174">È inoltre possibile utilizzare le sezioni di toomonitor questo oggetto di un set di dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-174">You also use this object toomonitor slices of a dataset at runtime.</span></span>

    ```csharp
    // create data factory management client
    string resourceGroupName = "ADFTutorialResourceGroup";
    string dataFactoryName = "APITutorialFactory";

    TokenCloudCredentials aadTokenCredentials = new TokenCloudCredentials(
            ConfigurationManager.AppSettings["SubscriptionId"],
            GetAuthorizationHeader().Result);

    Uri resourceManagerUri = new Uri(ConfigurationManager.AppSettings["ResourceManagerEndpoint"]);

    DataFactoryManagementClient client = new DataFactoryManagementClient(aadTokenCredentials, resourceManagerUri);
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="b80f4-175">Sostituire il valore di hello di **resourceGroupName** con il nome di hello del gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-175">Replace hello value of **resourceGroupName** with hello name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="b80f4-176">Aggiorna nome di hello toobe factory (dataFactoryName) di dati univoco.</span><span class="sxs-lookup"><span data-stu-id="b80f4-176">Update name of hello data factory (dataFactoryName) toobe unique.</span></span> <span data-ttu-id="b80f4-177">Nome della data factory di hello deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="b80f4-177">Name of hello data factory must be globally unique.</span></span> <span data-ttu-id="b80f4-178">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="b80f4-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="b80f4-179">Aggiungere hello dopo il codice che crea un **data factory di** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-179">Add hello following code that creates a **data factory** toohello **Main** method.</span></span>

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

    <span data-ttu-id="b80f4-180">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="b80f4-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="b80f4-181">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="b80f4-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="b80f4-182">Ad esempio, una data toocopy attività di copia da un archivio dati di origine tooa destinazione e un toorun attività Hive di HDInsight un tootransform script Hive i dati di output tooproduct dati di input.</span><span class="sxs-lookup"><span data-stu-id="b80f4-182">For example, a Copy Activity toocopy data from a source tooa destination data store and a HDInsight Hive activity toorun a Hive script tootransform input data tooproduct output data.</span></span> <span data-ttu-id="b80f4-183">Iniziamo con la creazione di data factory di hello in questo passaggio.</span><span class="sxs-lookup"><span data-stu-id="b80f4-183">Let's start with creating hello data factory in this step.</span></span>
8. <span data-ttu-id="b80f4-184">Aggiungere hello dopo il codice che crea un **servizio collegato di archiviazione di Azure** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-184">Add hello following code that creates an **Azure Storage linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b80f4-185">Sostituire **storageaccountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="b80f4-186">Creare servizi collegati in un toolink factory dati i dati vengono archiviati e toohello data factory di servizi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-186">You create linked services in a data factory toolink your data stores and compute services toohello data factory.</span></span> <span data-ttu-id="b80f4-187">In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics,</span><span class="sxs-lookup"><span data-stu-id="b80f4-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="b80f4-188">ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione).</span><span class="sxs-lookup"><span data-stu-id="b80f4-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="b80f4-189">Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="b80f4-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="b80f4-190">Hello AzureStorageLinkedService collega la data factory toohello account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-190">hello AzureStorageLinkedService links your Azure storage account toohello data factory.</span></span> <span data-ttu-id="b80f4-191">Questo account di archiviazione è hello uno in cui è stato creato un contenitore e caricato dati hello come parte del [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b80f4-191">This storage account is hello one in which you created a container and uploaded hello data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="b80f4-192">Aggiungere hello dopo il codice che crea un **servizio collegato SQL Azure** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-192">Add hello following code that creates an **Azure SQL linked service** toohello **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="b80f4-193">Sostituire **servername**, **databasename**, **username** e **password** con i nomi del server, del database, dell'utente e della password di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="b80f4-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

    ```csharp
    // create a linked service for output data store: Azure SQL Database
    Console.WriteLine("Creating Azure SQL Database linked service");
    client.LinkedServices.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new LinkedServiceCreateOrUpdateParameters()
        {
            LinkedService = new LinkedService()
            {
                Name = "AzureSqlLinkedService",
                Properties = new LinkedServiceProperties
                (
                    new AzureSqlDatabaseLinkedService("Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30")
                )
            }
        }
    );
    ```

    <span data-ttu-id="b80f4-194">AzureSqlLinkedService collega il toohello data factory di Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="b80f4-194">AzureSqlLinkedService links your Azure SQL database toohello data factory.</span></span> <span data-ttu-id="b80f4-195">dati Hello che viene copiati dall'archiviazione blob hello vengono archiviati nel database.</span><span class="sxs-lookup"><span data-stu-id="b80f4-195">hello data that is copied from hello blob storage is stored in this database.</span></span> <span data-ttu-id="b80f4-196">Tabella emp hello è stato creato in questo database come parte di [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b80f4-196">You created hello emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="b80f4-197">Aggiungere hello dopo il codice che crea **set di dati di input e output** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-197">Add hello following code that creates **input and output datasets** toohello **Main** method.</span></span>

    ```csharp
    // create input and output datasets
    Console.WriteLine("Creating input and output datasets");
    string Dataset_Source = "InputDataset";
    string Dataset_Destination = "OutputDataset";

    Console.WriteLine("Creating input dataset of type: Azure Blob");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,

    new DatasetCreateOrUpdateParameters()
    {
        Dataset = new Dataset()
        {
            Name = Dataset_Source,
            Properties = new DatasetProperties()
            {
                Structure = new List<DataElement>()
                {
                    new DataElement() { Name = "FirstName", Type = "String" },
                    new DataElement() { Name = "LastName", Type = "String" }
                },
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

    Console.WriteLine("Creating output dataset of type: Azure SQL");
    client.Datasets.CreateOrUpdate(resourceGroupName, dataFactoryName,
        new DatasetCreateOrUpdateParameters()
        {
            Dataset = new Dataset()
            {
                Name = Dataset_Destination,
                Properties = new DatasetProperties()
                {
                    Structure = new List<DataElement>()
                    {
                        new DataElement() { Name = "FirstName", Type = "String" },
                        new DataElement() { Name = "LastName", Type = "String" }
                    },
                    LinkedServiceName = "AzureSqlLinkedService",
                    TypeProperties = new AzureSqlTableDataset()
                    {
                        TableName = "emp"
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
    
    <span data-ttu-id="b80f4-198">Nel passaggio precedente hello, servizi collegati toolink è creato l'account di archiviazione di Azure e la data factory di Azure SQL database tooyour.</span><span class="sxs-lookup"><span data-stu-id="b80f4-198">In hello previous step, you created linked services toolink your Azure Storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="b80f4-199">In questo passaggio si definiscono due set di dati denominati InputDataset e OutputDataset che rappresentano l'input e output i dati archiviati in archivi dati hello a cui fa riferimento AzureStorageLinkedService e AzureSqlLinkedService rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="b80f4-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in hello data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="b80f4-200">il servizio di archiviazione di Azure collegati Hello specifica hello stringa di connessione del servizio Data Factory utilizzata in fase di esecuzione tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-200">hello Azure storage linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b80f4-201">E, set di dati blob di input hello (InputDataset) specifica il contenitore di hello e la cartella di hello che contiene i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-201">And, hello input blob dataset (InputDataset) specifies hello container and hello folder that contains hello input data.</span></span>  

    <span data-ttu-id="b80f4-202">Analogamente, hello servizio Database SQL di Azure collegati specifica hello stringa di connessione del servizio Data Factory utilizzata nel database di SQL Azure tooyour tooconnect fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-202">Similarly, hello Azure SQL Database linked service specifies hello connection string that Data Factory service uses at run time tooconnect tooyour Azure SQL database.</span></span> <span data-ttu-id="b80f4-203">E, di output di hello set di dati nella tabella SQL (OututDataset) specifica la tabella hello in hello di toowhich hello database vengono copiati dati dall'archiviazione blob hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-203">And, hello output SQL table dataset (OututDataset) specifies hello table in hello database toowhich hello data from hello blob storage is copied.</span></span>

    <span data-ttu-id="b80f4-204">In questo passaggio, creare un set di dati denominato InputDataset che punta il file di blob tooa (emp.txt) nella cartella radice hello di un contenitore di blob (adftutorial) in hello rappresentato da hello AzureStorageLinkedService collegato servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-204">In this step, you create a dataset named InputDataset that points tooa blob file (emp.txt) in hello root folder of a blob container (adftutorial) in hello Azure Storage represented by hello AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="b80f4-205">Se non specifica un valore per il nome file hello (o ignorarlo), i dati da tutti i BLOB nella cartella input hello sono copiati toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-205">If you don't specify a value for hello fileName (or skip it), data from all blobs in hello input folder are copied toohello destination.</span></span> <span data-ttu-id="b80f4-206">In questa esercitazione, si specifica un valore per il nome file hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-206">In this tutorial, you specify a value for hello fileName.</span></span>    

    <span data-ttu-id="b80f4-207">In questo passaggio si crea un set di dati di output denominato **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="b80f4-208">Questo set di dati fa riferimento nella tabella SQL tooa nel database di SQL Azure hello rappresentato da **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-208">This dataset points tooa SQL table in hello Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="b80f4-209">Aggiunta di codice seguente hello che **viene creato e attivato una pipeline** toohello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-209">Add hello following code that **creates and activates a pipeline** toohello **Main** method.</span></span> <span data-ttu-id="b80f4-210">In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="b80f4-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

    ```csharp
    // create a pipeline
    Console.WriteLine("Creating a pipeline");
    DateTime PipelineActivePeriodStartTime = new DateTime(2017, 5, 11, 0, 0, 0, 0, DateTimeKind.Utc);
    DateTime PipelineActivePeriodEndTime = new DateTime(2017, 5, 12, 0, 0, 0, 0, DateTimeKind.Utc);
    string PipelineName = "ADFTutorialPipeline";

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
                            Name = "BlobToAzureSql",
                            Inputs = new List<ActivityInput>()
                            {
                                new ActivityInput() {
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
                    }
                }
            }
        });
    ```

    <span data-ttu-id="b80f4-211">Si noti hello seguenti punti:</span><span class="sxs-lookup"><span data-stu-id="b80f4-211">Note hello following points:</span></span>
   
    - <span data-ttu-id="b80f4-212">Nella sezione attività hello, è presente una sola attività il cui **tipo** è troppo**copia**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-212">In hello activities section, there is only one activity whose **type** is set too**Copy**.</span></span> <span data-ttu-id="b80f4-213">Per ulteriori informazioni sulle attività di copia hello, vedere [attività lo spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b80f4-213">For more information about hello copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="b80f4-214">Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="b80f4-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="b80f4-215">Input per attività hello è troppo**InputDataset** e di output per attività hello è troppo**OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-215">Input for hello activity is set too**InputDataset** and output for hello activity is set too**OutputDataset**.</span></span> 
    - <span data-ttu-id="b80f4-216">In hello **typeProperties** sezione **BlobSource** è specificato come tipo di origine hello e **SqlSink** è specificato come tipo di sink hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-216">In hello **typeProperties** section, **BlobSource** is specified as hello source type and **SqlSink** is specified as hello sink type.</span></span> <span data-ttu-id="b80f4-217">Per un elenco completo degli archivi di dati supportati dall'attività di copia hello come origini e sink, vedere [supportati archivi dati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b80f4-217">For a complete list of data stores supported by hello copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b80f4-218">toolearn sulla modalità di memorizzazione toouse dati specifici supportati come origine/sink, fare clic su collegamento hello nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-218">toolearn how toouse a specific supported data store as a source/sink, click hello link in hello table.</span></span>  
   
    <span data-ttu-id="b80f4-219">Set di dati di output è attualmente, quali unità hello pianificazione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-219">Currently, output dataset is what drives hello schedule.</span></span> <span data-ttu-id="b80f4-220">In questa esercitazione, set di dati di output è tooproduce configurato una sezione di una volta all'ora.</span><span class="sxs-lookup"><span data-stu-id="b80f4-220">In this tutorial, output dataset is configured tooproduce a slice once an hour.</span></span> <span data-ttu-id="b80f4-221">pipeline Hello dispone ora di inizio e ora di fine di un giorno separato, ovvero 24 ore.</span><span class="sxs-lookup"><span data-stu-id="b80f4-221">hello pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="b80f4-222">Pertanto, 24 sezioni del set di dati di output vengono generate dalla pipeline hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-222">Therefore, 24 slices of output dataset are produced by hello pipeline.</span></span>
12. <span data-ttu-id="b80f4-223">Aggiungere i seguenti toohello codice hello **Main** metodo tooget hello stato una sezione di dati di hello set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="b80f4-223">Add hello following code toohello **Main** method tooget hello status of a data slice of hello output dataset.</span></span> <span data-ttu-id="b80f4-224">In questo esempio è prevista solo una sezione.</span><span class="sxs-lookup"><span data-stu-id="b80f4-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="b80f4-225">Aggiungere i seguenti dettagli tooget eseguire codice per un toohello sezione dati hello **Main** metodo.</span><span class="sxs-lookup"><span data-stu-id="b80f4-225">Add hello following code tooget run details for a data slice toohello **Main** method.</span></span>

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
            }
        );

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

14. <span data-ttu-id="b80f4-226">Aggiungere hello seguente metodo helper utilizzato dal hello **Main** metodo toohello **programma** classe.</span><span class="sxs-lookup"><span data-stu-id="b80f4-226">Add hello following helper method used by hello **Main** method toohello **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="b80f4-227">Quando si copia e Incolla hello seguente di codice, assicurarsi che tale hello codice copiato è hello stesso livello come hello metodo Main.</span><span class="sxs-lookup"><span data-stu-id="b80f4-227">When you copy and paste hello following code, make sure that hello copied code is at hello same level as hello Main method.</span></span>

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

15. <span data-ttu-id="b80f4-228">In hello Esplora soluzioni, espandere il progetto di hello (DataFactoryAPITestApp), fare doppio clic su **riferimenti**, fare clic su **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-228">In hello Solution Explorer, expand hello project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="b80f4-229">Selezionare la casella di controllo per l'assembly **System.Configuration**</span><span class="sxs-lookup"><span data-stu-id="b80f4-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="b80f4-230">e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-230">and click **OK**.</span></span>
16. <span data-ttu-id="b80f4-231">Compilare un'applicazione console hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-231">Build hello console application.</span></span> <span data-ttu-id="b80f4-232">Fare clic su **compilare** menu hello e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-232">Click **Build** on hello menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="b80f4-233">Verificare che esista almeno un file in hello **adftutorial** contenitore nell'archiviazione blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-233">Confirm that there is at least one file in hello **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="b80f4-234">In caso contrario, creare **Emp.txt** con hello seguente contenuto del file nel blocco note e caricarlo toohello adftutorial contenitore.</span><span class="sxs-lookup"><span data-stu-id="b80f4-234">If not, create **Emp.txt** file in Notepad with hello following content and upload it toohello adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="b80f4-235">Eseguire l'esempio hello facendo **Debug** -> **Avvia debug** menu hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-235">Run hello sample by clicking **Debug** -> **Start Debugging** on hello menu.</span></span> <span data-ttu-id="b80f4-236">Quando viene visualizzato hello **dettagli di una sezione di dati di esecuzione**, attendere qualche minuto e premere **invio**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-236">When you see hello **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="b80f4-237">Utilizzare hello tooverify portale Azure data factory di tale hello **APITutorialFactory** viene creato con hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="b80f4-237">Use hello Azure portal tooverify that hello data factory **APITutorialFactory** is created with hello following artifacts:</span></span>
   * <span data-ttu-id="b80f4-238">Servizio collegato: **LinkedService_AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="b80f4-239">Set di dati: **InputDataset** e **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="b80f4-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="b80f4-240">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="b80f4-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="b80f4-241">Verificare che i record dipendente hello due vengono creati in hello **emp** tabella hello specificato database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="b80f4-241">Verify that hello two employee records are created in hello **emp** table in hello specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b80f4-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b80f4-242">Next steps</span></span>
<span data-ttu-id="b80f4-243">Per la documentazione completa sull'API .NET per Data Factory, vedere le [informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="b80f4-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="b80f4-244">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="b80f4-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="b80f4-245">Hello nella tabella seguente fornisce un elenco di archivi di dati supportato come origini e destinazioni da attività di copia hello:</span><span class="sxs-lookup"><span data-stu-id="b80f4-245">hello following table provides a list of data stores supported as sources and destinations by hello copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="b80f4-246">toolearn su come archiviano dati toocopy da e verso un tipo di dati, fare clic su collegamento hello per hello archivio di dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b80f4-246">toolearn about how toocopy data to/from a data store, click hello link for hello data store in hello table.</span></span>

