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
ms.openlocfilehash: 30c7cd1ba455d7b1bc93d76e7ee79455bb52aae9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="tutorial-create-a-pipeline-with-copy-activity-using-net-api"></a><span data-ttu-id="ac43f-103">Esercitazione: Creare una pipeline con l'attività di copia usando l'API .NET</span><span class="sxs-lookup"><span data-stu-id="ac43f-103">Tutorial: Create a pipeline with Copy Activity using .NET API</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ac43f-104">Panoramica e prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ac43f-104">Overview and prerequisites</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [<span data-ttu-id="ac43f-105">Copia guidata</span><span class="sxs-lookup"><span data-stu-id="ac43f-105">Copy Wizard</span></span>](data-factory-copy-data-wizard-tutorial.md)
> * [<span data-ttu-id="ac43f-106">Portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ac43f-106">Azure portal</span></span>](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [<span data-ttu-id="ac43f-107">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ac43f-107">Visual Studio</span></span>](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [<span data-ttu-id="ac43f-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ac43f-108">PowerShell</span></span>](data-factory-copy-activity-tutorial-using-powershell.md)
> * [<span data-ttu-id="ac43f-109">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ac43f-109">Azure Resource Manager template</span></span>](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [<span data-ttu-id="ac43f-110">API REST</span><span class="sxs-lookup"><span data-stu-id="ac43f-110">REST API</span></span>](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [<span data-ttu-id="ac43f-111">API .NET</span><span class="sxs-lookup"><span data-stu-id="ac43f-111">.NET API</span></span>](data-factory-copy-activity-tutorial-using-dotnet-api.md)

<span data-ttu-id="ac43f-112">Questo articolo illustra l'uso dell'[API .NET](https://portal.azure.com) per creare una data factory con una pipeline che copia i dati da un archivio BLOB di Azure a un database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-112">In this article, you learn how to use [.NET API](https://portal.azure.com) to create a data factory with a pipeline that copies data from an Azure blob storage to an Azure SQL database.</span></span> <span data-ttu-id="ac43f-113">Se non si ha familiarità con Azure Data Factory, prima di eseguire questa esercitazione vedere l'articolo [Introduzione ad Azure Data Factory](data-factory-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="ac43f-113">If you are new to Azure Data Factory, read through the [Introduction to Azure Data Factory](data-factory-introduction.md) article before doing this tutorial.</span></span>   

<span data-ttu-id="ac43f-114">In questa esercitazione si crea una pipeline contenente una sola attività: un'attività di copia</span><span class="sxs-lookup"><span data-stu-id="ac43f-114">In this tutorial, you create a pipeline with one activity in it: Copy Activity.</span></span> <span data-ttu-id="ac43f-115">che copia i dati da un archivio dati supportato a un archivio dati sink supportato.</span><span class="sxs-lookup"><span data-stu-id="ac43f-115">The copy activity copies data from a supported data store to a supported sink data store.</span></span> <span data-ttu-id="ac43f-116">Per un elenco degli archivi dati supportati come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ac43f-116">For a list of data stores supported as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ac43f-117">e si basa su un servizio disponibile a livello globale che può copiare dati tra diversi archivi dati in modo sicuro, affidabile e scalabile.</span><span class="sxs-lookup"><span data-stu-id="ac43f-117">The activity is powered by a globally available service that can copy data between various data stores in a secure, reliable, and scalable way.</span></span> <span data-ttu-id="ac43f-118">Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ac43f-118">For more information about the Copy Activity, see [Data Movement Activities](data-factory-data-movement-activities.md).</span></span>

<span data-ttu-id="ac43f-119">Una pipeline può includere più attività</span><span class="sxs-lookup"><span data-stu-id="ac43f-119">A pipeline can have more than one activity.</span></span> <span data-ttu-id="ac43f-120">ed è possibile concatenarne due, ovvero eseguire un'attività dopo l'altra, impostando il set di dati di output di un'attività come set di dati di input dell'altra.</span><span class="sxs-lookup"><span data-stu-id="ac43f-120">And, you can chain two activities (run one activity after another) by setting the output dataset of one activity as the input dataset of the other activity.</span></span> <span data-ttu-id="ac43f-121">Per altre informazioni, vedere [Attività multiple in una pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span><span class="sxs-lookup"><span data-stu-id="ac43f-121">For more information, see [multiple activities in a pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).</span></span> 

> [!NOTE] 
> <span data-ttu-id="ac43f-122">Per la documentazione completa sull'API .NET per Data Factory, vedere le [informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="ac43f-122">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>
> 
> <span data-ttu-id="ac43f-123">La pipeline di dati in questa esercitazione copia i dati da un archivio dati di origine a un archivio dati di destinazione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-123">The data pipeline in this tutorial copies data from a source data store to a destination data store.</span></span> <span data-ttu-id="ac43f-124">Per un'esercitazione su come trasformare i dati usando Azure Data Factory, vedere [Esercitazione: Creare una pipeline per trasformare i dati usando un cluster Hadoop](data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="ac43f-124">For a tutorial on how to transform data using Azure Data Factory, see [Tutorial: Build a pipeline to transform data using Hadoop cluster](data-factory-build-your-first-pipeline.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac43f-125">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ac43f-125">Prerequisites</span></span>
* <span data-ttu-id="ac43f-126">Per una panoramica dell'esercitazione e per eseguire i passaggi relativi ai [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) , vedere **Panoramica e prerequisiti** .</span><span class="sxs-lookup"><span data-stu-id="ac43f-126">Go through [Tutorial Overview and Pre-requisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) to get an overview of the tutorial and complete the **prerequisite** steps.</span></span>
* <span data-ttu-id="ac43f-127">Visual Studio 2012 o 2013 o 2015</span><span class="sxs-lookup"><span data-stu-id="ac43f-127">Visual Studio 2012 or 2013 or 2015</span></span>
* <span data-ttu-id="ac43f-128">Scaricare e installare [.NET SDK di Azure](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="ac43f-128">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>
* <span data-ttu-id="ac43f-129">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac43f-129">Azure PowerShell.</span></span> <span data-ttu-id="ac43f-130">Seguire le istruzioni disponibili nell'articolo [Come installare e configurare Azure PowerShell](../powershell-install-configure.md) per installare la versione più recente di Azure PowerShell nel computer.</span><span class="sxs-lookup"><span data-stu-id="ac43f-130">Follow instructions in [How to install and configure Azure PowerShell](../powershell-install-configure.md) article to install Azure PowerShell on your computer.</span></span> <span data-ttu-id="ac43f-131">Azure PowerShell verrà usato per creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-131">You use Azure PowerShell to create an Azure Active Directory application.</span></span>

### <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="ac43f-132">Creare un'applicazione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ac43f-132">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="ac43f-133">Creare l'applicazione Azure Active Directory, creare un'entità servizio per l'applicazione e assegnarla al ruolo **Collaboratore Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="ac43f-133">Create an Azure Active Directory application, create a service principal for the application, and assign it to the **Data Factory Contributor** role.</span></span>

1. <span data-ttu-id="ac43f-134">Avviare **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-134">Launch **PowerShell**.</span></span>
2. <span data-ttu-id="ac43f-135">Eseguire il comando seguente e immettere il nome utente e la password usati per accedere al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-135">Run the following command and enter the user name and password that you use to sign in to the Azure portal.</span></span>

    ```PowerShell
    Login-AzureRmAccount
    ```
3. <span data-ttu-id="ac43f-136">Eseguire il comando seguente per visualizzare tutte le sottoscrizioni per l'account.</span><span class="sxs-lookup"><span data-stu-id="ac43f-136">Run the following command to view all the subscriptions for this account.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    ```
4. <span data-ttu-id="ac43f-137">Eseguire il comando seguente per selezionare la sottoscrizione da usare.</span><span class="sxs-lookup"><span data-stu-id="ac43f-137">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="ac43f-138">Sostituire **&lt;NameOfAzureSubscription**&gt; con il nome della sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-138">Replace **&lt;NameOfAzureSubscription**&gt; with the name of your Azure subscription.</span></span>

    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```

   > [!IMPORTANT]
   > <span data-ttu-id="ac43f-139">Dall'output del comando prendere nota dei valori di **SubscriptionId** e **TenantId**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-139">Note down **SubscriptionId** and **TenantId** from the output of this command.</span></span>

5. <span data-ttu-id="ac43f-140">Creare un gruppo di risorse di Azure denominato **ADFTutorialResourceGroup** eseguendo il comando seguente in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ac43f-140">Create an Azure resource group named **ADFTutorialResourceGroup** by running the following command in the PowerShell.</span></span>

    ```PowerShell
    New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```

    <span data-ttu-id="ac43f-141">Se il gruppo di risorse esiste già, specificare se deve essere aggiornato (Y) o mantenuto invariato (N).</span><span class="sxs-lookup"><span data-stu-id="ac43f-141">If the resource group already exists, you specify whether to update it (Y) or keep it as (N).</span></span>

    <span data-ttu-id="ac43f-142">Se si usa un gruppo di risorse diverso, è necessario usare il nome del gruppo di risorse invece di ADFTutorialResourceGroup in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-142">If you use a different resource group, you need to use the name of your resource group in place of ADFTutorialResourceGroup in this tutorial.</span></span>
6. <span data-ttu-id="ac43f-143">Creare un'applicazione Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-143">Create an Azure Active Directory application.</span></span>

    ```PowerShell
    $azureAdApplication = New-AzureRmADApplication -DisplayName "ADFCopyTutotiralApp" -HomePage "https://www.contoso.org" -IdentifierUris "https://www.adfcopytutorialapp.org/example" -Password "Pass@word1"
    ```

    <span data-ttu-id="ac43f-144">Se viene visualizzato l'errore seguente, specificare un URL diverso ed eseguire di nuovo il comando.</span><span class="sxs-lookup"><span data-stu-id="ac43f-144">If you get the following error, specify a different URL and run the command again.</span></span>
    
    ```PowerShell
    Another object with the same value for property identifierUris already exists.
    ```
7. <span data-ttu-id="ac43f-145">Creare l'entità servizio di AD.</span><span class="sxs-lookup"><span data-stu-id="ac43f-145">Create the AD service principal.</span></span>

    ```PowerShell
    New-AzureRmADServicePrincipal -ApplicationId $azureAdApplication.ApplicationId
    ```
8. <span data-ttu-id="ac43f-146">Aggiungere l'entità servizio al ruolo **Collaboratore Data Factory** .</span><span class="sxs-lookup"><span data-stu-id="ac43f-146">Add service principal to the **Data Factory Contributor** role.</span></span>

    ```PowerShell
    New-AzureRmRoleAssignment -RoleDefinitionName "Data Factory Contributor" -ServicePrincipalName $azureAdApplication.ApplicationId.Guid
    ```
9. <span data-ttu-id="ac43f-147">Ottenere l'ID applicazione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-147">Get the application ID.</span></span>

    ```PowerShell
    $azureAdApplication 
    ```
    <span data-ttu-id="ac43f-148">Annotare l'ID applicazione (applicationID) dall'output.</span><span class="sxs-lookup"><span data-stu-id="ac43f-148">Note down the application ID (applicationID) from the output.</span></span>

<span data-ttu-id="ac43f-149">Da questi passaggi si avranno i quattro valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac43f-149">You should have following four values from these steps:</span></span>

* <span data-ttu-id="ac43f-150">ID tenant</span><span class="sxs-lookup"><span data-stu-id="ac43f-150">Tenant ID</span></span>
* <span data-ttu-id="ac43f-151">ID sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ac43f-151">Subscription ID</span></span>
* <span data-ttu-id="ac43f-152">ID applicazione</span><span class="sxs-lookup"><span data-stu-id="ac43f-152">Application ID</span></span>
* <span data-ttu-id="ac43f-153">Password (specificata nel primo comando)</span><span class="sxs-lookup"><span data-stu-id="ac43f-153">Password (specified in the first command)</span></span>

## <a name="walkthrough"></a><span data-ttu-id="ac43f-154">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="ac43f-154">Walkthrough</span></span>
1. <span data-ttu-id="ac43f-155">Creare un'applicazione console .NET in C# con Visual Studio 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="ac43f-155">Using Visual Studio 2012/2013/2015, create a C# .NET console application.</span></span>
   1. <span data-ttu-id="ac43f-156">Avviare **Visual Studio** 2012, 2013 o 2015.</span><span class="sxs-lookup"><span data-stu-id="ac43f-156">Launch **Visual Studio** 2012/2013/2015.</span></span>
   2. <span data-ttu-id="ac43f-157">Fare clic su **File**, scegliere **Nuovo** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-157">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="ac43f-158">Espandere **Modelli** e quindi selezionare **Visual C#**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-158">Expand **Templates**, and select **Visual C#**.</span></span> <span data-ttu-id="ac43f-159">In questa procedura dettagliata viene usato C#, ma è possibile usare qualsiasi linguaggio .NET.</span><span class="sxs-lookup"><span data-stu-id="ac43f-159">In this walkthrough, you use C#, but you can use any .NET language.</span></span>
   4. <span data-ttu-id="ac43f-160">Selezionare **Applicazione console** dall'elenco dei tipi di progetto a destra.</span><span class="sxs-lookup"><span data-stu-id="ac43f-160">Select **Console Application** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="ac43f-161">Immettere **DataFactoryAPITestApp** per Nome.</span><span class="sxs-lookup"><span data-stu-id="ac43f-161">Enter **DataFactoryAPITestApp** for the Name.</span></span>
   6. <span data-ttu-id="ac43f-162">Selezionare **C:\ADFGetStarted** come percorso.</span><span class="sxs-lookup"><span data-stu-id="ac43f-162">Select **C:\ADFGetStarted** for the Location.</span></span>
   7. <span data-ttu-id="ac43f-163">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="ac43f-163">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="ac43f-164">Fare clic su **Strumenti**, scegliere **Gestione pacchetti NuGet** e quindi fare clic su **Console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-164">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="ac43f-165">Nella finestra **Console di Gestione pacchetti** seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="ac43f-165">In the **Package Manager Console**, do the following steps:</span></span>
   1. <span data-ttu-id="ac43f-166">Eseguire questo comando per installare il pacchetto di Data factory: `Install-Package Microsoft.Azure.Management.DataFactories`</span><span class="sxs-lookup"><span data-stu-id="ac43f-166">Run the following command to install Data Factory package: `Install-Package Microsoft.Azure.Management.DataFactories`</span></span>
   2. <span data-ttu-id="ac43f-167">Eseguire questo comando per installare il pacchetto di Azure Active Directory. Nel codice viene usata l'API di Active Directory: `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span><span class="sxs-lookup"><span data-stu-id="ac43f-167">Run the following command to install Azure Active Directory package (you use Active Directory API in the code): `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.19.208020213`</span></span>
4. <span data-ttu-id="ac43f-168">Aggiungere la sezione **appSettings** seguente al file **App.config**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-168">Add the following **appSetttings** section to the **App.config** file.</span></span> <span data-ttu-id="ac43f-169">Queste impostazioni sono usate dal metodo helper **GetAuthorizationHeader**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-169">These settings are used by the helper method: **GetAuthorizationHeader**.</span></span>

    <span data-ttu-id="ac43f-170">Sostituire i valori di **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;** e **&lt;tenant ID&gt;** con i propri valori.</span><span class="sxs-lookup"><span data-stu-id="ac43f-170">Replace values for **&lt;Application ID&gt;**, **&lt;Password&gt;**, **&lt;Subscription ID&gt;**, and **&lt;tenant ID&gt;** with your own values.</span></span>

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

5. <span data-ttu-id="ac43f-171">Aggiungere le istruzioni **using** seguenti al file di origine (Program.cs) nel progetto.</span><span class="sxs-lookup"><span data-stu-id="ac43f-171">Add the following **using** statements to the source file (Program.cs) in the project.</span></span>

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

6. <span data-ttu-id="ac43f-172">Aggiungere al metodo **Main** il codice seguente che crea un'istanza della classe **DataPipelineManagementClient**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-172">Add the following code that creates an instance of **DataPipelineManagementClient** class to the **Main** method.</span></span> <span data-ttu-id="ac43f-173">Si userà questo oggetto per creare una data factory, un servizio collegato, i set di dati di input e output e una pipeline.</span><span class="sxs-lookup"><span data-stu-id="ac43f-173">You use this object to create a data factory, a linked service, input and output datasets, and a pipeline.</span></span> <span data-ttu-id="ac43f-174">Questo oggetto viene usato anche per monitorare le sezioni di un set di dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-174">You also use this object to monitor slices of a dataset at runtime.</span></span>

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
   > <span data-ttu-id="ac43f-175">Sostituire il valore di **resourceGroupName** con il nome del gruppo di risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-175">Replace the value of **resourceGroupName** with the name of your Azure resource group.</span></span>
   >
   > <span data-ttu-id="ac43f-176">Aggiornare il nome della data factory (dataFactoryName) in modo che sia univoco.</span><span class="sxs-lookup"><span data-stu-id="ac43f-176">Update name of the data factory (dataFactoryName) to be unique.</span></span> <span data-ttu-id="ac43f-177">Il nome della data factory deve essere globalmente univoco.</span><span class="sxs-lookup"><span data-stu-id="ac43f-177">Name of the data factory must be globally unique.</span></span> <span data-ttu-id="ac43f-178">Per informazioni sulle regole di denominazione per gli elementi di Data factory, vedere l'argomento relativo alle [regole di denominazione di Data factory](data-factory-naming-rules.md) .</span><span class="sxs-lookup"><span data-stu-id="ac43f-178">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>

7. <span data-ttu-id="ac43f-179">Aggiungere al metodo **Main** il codice seguente che crea una **data factory**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-179">Add the following code that creates a **data factory** to the **Main** method.</span></span>

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

    <span data-ttu-id="ac43f-180">Una data factory può comprendere una o più pipeline.</span><span class="sxs-lookup"><span data-stu-id="ac43f-180">A data factory can have one or more pipelines.</span></span> <span data-ttu-id="ac43f-181">Una pipeline può comprendere una o più attività.</span><span class="sxs-lookup"><span data-stu-id="ac43f-181">A pipeline can have one or more activities in it.</span></span> <span data-ttu-id="ac43f-182">Ad esempio, un'attività di copia per copiare dati da un archivio dati di origine a uno di destinazione e un'attività Hive HDInsight per eseguire uno script Hive e trasformare i dati di input in dati di output di prodotto.</span><span class="sxs-lookup"><span data-stu-id="ac43f-182">For example, a Copy Activity to copy data from a source to a destination data store and a HDInsight Hive activity to run a Hive script to transform input data to product output data.</span></span> <span data-ttu-id="ac43f-183">In questo passaggio iniziale viene creata la data factory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-183">Let's start with creating the data factory in this step.</span></span>
8. <span data-ttu-id="ac43f-184">Aggiungere al metodo **Main** il codice seguente che crea un **servizio collegato di Archiviazione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-184">Add the following code that creates an **Azure Storage linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ac43f-185">Sostituire **storageaccountname** e **accountkey** con il nome e la chiave dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-185">Replace **storageaccountname** and **accountkey** with name and key of your Azure Storage account.</span></span>

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

    <span data-ttu-id="ac43f-186">Si creano servizi collegati in una data factory per collegare gli archivi dati e i servizi di calcolo alla data factory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-186">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="ac43f-187">In questa esercitazione non si usano servizi di calcolo come Azure HDInsight o Azure Data Lake Analytics,</span><span class="sxs-lookup"><span data-stu-id="ac43f-187">In this tutorial, you don't use any compute service such as Azure HDInsight or Azure Data Lake Analytics.</span></span> <span data-ttu-id="ac43f-188">ma due archivi dati di tipo Archiviazione di Azure (origine) e database SQL di Azure (destinazione).</span><span class="sxs-lookup"><span data-stu-id="ac43f-188">You use two data stores of type Azure Storage (source) and Azure SQL Database (destination).</span></span> 

    <span data-ttu-id="ac43f-189">Si creano quindi due servizi collegati denominati AzureStorageLinkedService e AzureSqlLinkedService di tipo AzureStorage e AzureSqlDatabase.</span><span class="sxs-lookup"><span data-stu-id="ac43f-189">Therefore, you create two linked services named AzureStorageLinkedService and AzureSqlLinkedService of types: AzureStorage and AzureSqlDatabase.</span></span>  

    <span data-ttu-id="ac43f-190">AzureStorageLinkedService collega l'account di archiviazione di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-190">The AzureStorageLinkedService links your Azure storage account to the data factory.</span></span> <span data-ttu-id="ac43f-191">L'account di archiviazione è quello in cui, come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md), è stato creato un contenitore e sono stati caricati i dati.</span><span class="sxs-lookup"><span data-stu-id="ac43f-191">This storage account is the one in which you created a container and uploaded the data as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
9. <span data-ttu-id="ac43f-192">Aggiungere al metodo **Main** il codice seguente che crea un **servizio collegato di Azure SQL**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-192">Add the following code that creates an **Azure SQL linked service** to the **Main** method.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ac43f-193">Sostituire **servername**, **databasename**, **username** e **password** con i nomi del server, del database, dell'utente e della password di Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="ac43f-193">Replace **servername**, **databasename**, **username**, and **password** with names of your Azure SQL server, database, user, and password.</span></span>

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

    <span data-ttu-id="ac43f-194">AzureSqlLinkedService collega il database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-194">AzureSqlLinkedService links your Azure SQL database to the data factory.</span></span> <span data-ttu-id="ac43f-195">I dati copiati dall'archivio BLOB vengono archiviati in questo database.</span><span class="sxs-lookup"><span data-stu-id="ac43f-195">The data that is copied from the blob storage is stored in this database.</span></span> <span data-ttu-id="ac43f-196">Come parte dei [prerequisiti](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) è stata creata la tabella emp in questo database.</span><span class="sxs-lookup"><span data-stu-id="ac43f-196">You created the emp table in this database as part of [prerequisites](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
10. <span data-ttu-id="ac43f-197">Aggiungere al metodo **Main** il codice seguente che crea **set di dati di input e output**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-197">Add the following code that creates **input and output datasets** to the **Main** method.</span></span>

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
    
    <span data-ttu-id="ac43f-198">Nel passaggio precedente sono stati creati servizi collegati per collegare l'account di archiviazione di Azure e un database SQL di Azure alla data factory.</span><span class="sxs-lookup"><span data-stu-id="ac43f-198">In the previous step, you created linked services to link your Azure Storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="ac43f-199">In questo passaggio vengono definiti due set di dati denominati InputDataset e OutputDataset, che rappresentano i dati di input e di output memorizzati negli archivi dati a cui fanno riferimento rispettivamente AzureStorageLinkedService e AzureSqlLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ac43f-199">In this step, you define two datasets named InputDataset and OutputDataset that represent input and output data that is stored in the data stores referred by AzureStorageLinkedService and AzureSqlLinkedService respectively.</span></span>

    <span data-ttu-id="ac43f-200">Il servizio collegato Archiviazione di Azure specifica la stringa di connessione usata dal servizio Data Factory in fase di esecuzione per connettersi all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-200">The Azure storage linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure storage account.</span></span> <span data-ttu-id="ac43f-201">Il set di dati del BLOB di input (InputDataset) specifica il contenitore e la cartella che contiene i dati di input.</span><span class="sxs-lookup"><span data-stu-id="ac43f-201">And, the input blob dataset (InputDataset) specifies the container and the folder that contains the input data.</span></span>  

    <span data-ttu-id="ac43f-202">Analogamente, il servizio collegato per il database SQL di Azure specifica la stringa di connessione usata dal servizio Data Factory in fase di esecuzione per connettersi al database SQL di Azure</span><span class="sxs-lookup"><span data-stu-id="ac43f-202">Similarly, the Azure SQL Database linked service specifies the connection string that Data Factory service uses at run time to connect to your Azure SQL database.</span></span> <span data-ttu-id="ac43f-203">e il set di dati della tabella SQL di output (OututDataset) specifica la tabella del database in cui vengono copiati i dati dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="ac43f-203">And, the output SQL table dataset (OututDataset) specifies the table in the database to which the data from the blob storage is copied.</span></span>

    <span data-ttu-id="ac43f-204">In questo passaggio viene creato un set di dati denominato InputDataset che punta a un file BLOB (emp.txt) nella cartella radice di un contenitore BLOB (adftutorial) nella risorsa di archiviazione di Azure rappresentata dal servizio collegato AzureStorageLinkedService.</span><span class="sxs-lookup"><span data-stu-id="ac43f-204">In this step, you create a dataset named InputDataset that points to a blob file (emp.txt) in the root folder of a blob container (adftutorial) in the Azure Storage represented by the AzureStorageLinkedService linked service.</span></span> <span data-ttu-id="ac43f-205">Se non si specifica un valore per fileName (o lo si ignora), i dati di tutti i BLOB della cartella di input vengono copiati nella destinazione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-205">If you don't specify a value for the fileName (or skip it), data from all blobs in the input folder are copied to the destination.</span></span> <span data-ttu-id="ac43f-206">In questa esercitazione si specifica un valore per fileName.</span><span class="sxs-lookup"><span data-stu-id="ac43f-206">In this tutorial, you specify a value for the fileName.</span></span>    

    <span data-ttu-id="ac43f-207">In questo passaggio si crea un set di dati di output denominato **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-207">In this step, you create an output dataset named **OutputDataset**.</span></span> <span data-ttu-id="ac43f-208">Questo set di dati punta a una tabella SQL nel database SQL di Azure rappresentato da **AzureSqlLinkedService**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-208">This dataset points to a SQL table in the Azure SQL database represented by **AzureSqlLinkedService**.</span></span>
11. <span data-ttu-id="ac43f-209">Aggiungere al metodo **Main** il codice seguente che **crea e attiva una pipeline**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-209">Add the following code that **creates and activates a pipeline** to the **Main** method.</span></span> <span data-ttu-id="ac43f-210">In questo passaggio viene creata una pipeline con un'**attività di copia** che usa **InputDataset** come input e **OutputDataset** come output.</span><span class="sxs-lookup"><span data-stu-id="ac43f-210">In this step, you create a pipeline with a **copy activity** that uses **InputDataset** as an input and **OutputDataset** as an output.</span></span>

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

                    // Initial value for pipeline's active period. With this, you won't need to set slice status
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

    <span data-ttu-id="ac43f-211">Tenere presente quanto segue:</span><span class="sxs-lookup"><span data-stu-id="ac43f-211">Note the following points:</span></span>
   
    - <span data-ttu-id="ac43f-212">Nella sezione delle attività esiste una sola attività con l'oggetto **type** impostato su **Copy**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-212">In the activities section, there is only one activity whose **type** is set to **Copy**.</span></span> <span data-ttu-id="ac43f-213">Per altre informazioni sull'attività di copia, vedere le [attività di spostamento dei dati](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ac43f-213">For more information about the copy activity, see [data movement activities](data-factory-data-movement-activities.md).</span></span> <span data-ttu-id="ac43f-214">Nelle soluzioni Data Factory è anche possibile usare le [attività di trasformazione dei dati](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="ac43f-214">In Data Factory solutions, you can also use [data transformation activities](data-factory-data-transformation-activities.md).</span></span>
    - <span data-ttu-id="ac43f-215">L'input per l'attività è impostato su **InputDataset** e l'output è impostato su **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-215">Input for the activity is set to **InputDataset** and output for the activity is set to **OutputDataset**.</span></span> 
    - <span data-ttu-id="ac43f-216">Nella sezione **typeProperties** vengono specificati **BlobSource** come tipo di origine e **SqlSink** come tipo di sink.</span><span class="sxs-lookup"><span data-stu-id="ac43f-216">In the **typeProperties** section, **BlobSource** is specified as the source type and **SqlSink** is specified as the sink type.</span></span> <span data-ttu-id="ac43f-217">Per un elenco completo degli archivi dati supportati dall'attività di copia come origini e sink, vedere gli [archivi dati supportati](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="ac43f-217">For a complete list of data stores supported by the copy activity as sources and sinks, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="ac43f-218">Per informazioni su come usare uno specifico archivio dati supportato come origine/sink, fare clic sul collegamento nella tabella.</span><span class="sxs-lookup"><span data-stu-id="ac43f-218">To learn how to use a specific supported data store as a source/sink, click the link in the table.</span></span>  
   
    <span data-ttu-id="ac43f-219">Attualmente, è il set di dati di output a determinare la pianificazione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-219">Currently, output dataset is what drives the schedule.</span></span> <span data-ttu-id="ac43f-220">In questa esercitazione il set di dati di output viene configurato per generare una sezione una volta ogni ora.</span><span class="sxs-lookup"><span data-stu-id="ac43f-220">In this tutorial, output dataset is configured to produce a slice once an hour.</span></span> <span data-ttu-id="ac43f-221">La pipeline ha un'ora di inizio e un'ora di fine intervallate da un giorno, ovvero 24 ore.</span><span class="sxs-lookup"><span data-stu-id="ac43f-221">The pipeline has a start time and end time that are one day apart, which is 24 hours.</span></span> <span data-ttu-id="ac43f-222">Vengono quindi generate dalla pipeline 24 sezioni di set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="ac43f-222">Therefore, 24 slices of output dataset are produced by the pipeline.</span></span>
12. <span data-ttu-id="ac43f-223">Aggiungere al metodo **Main** il codice seguente per ottenere lo stato di una sezione di dati del set di dati di output.</span><span class="sxs-lookup"><span data-stu-id="ac43f-223">Add the following code to the **Main** method to get the status of a data slice of the output dataset.</span></span> <span data-ttu-id="ac43f-224">In questo esempio è prevista solo una sezione.</span><span class="sxs-lookup"><span data-stu-id="ac43f-224">There is only slice expected in this sample.</span></span>

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

13. <span data-ttu-id="ac43f-225">Aggiungere al metodo **Main** il codice seguente per ottenere i dettagli di esecuzione di una sezione dati.</span><span class="sxs-lookup"><span data-stu-id="ac43f-225">Add the following code to get run details for a data slice to the **Main** method.</span></span>

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

    Console.WriteLine("\nPress any key to exit.");
    Console.ReadKey();
    ```

14. <span data-ttu-id="ac43f-226">Aggiungere alla classe **Program** il metodo helper seguente usato per il metodo **Main**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-226">Add the following helper method used by the **Main** method to the **Program** class.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="ac43f-227">Quando si copia e incolla il codice seguente, assicurarsi che il codice copiato si trovi allo stesso livello del metodo Main.</span><span class="sxs-lookup"><span data-stu-id="ac43f-227">When you copy and paste the following code, make sure that the copied code is at the same level as the Main method.</span></span>

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

15. <span data-ttu-id="ac43f-228">In Esplora soluzioni espandere il progetto (DataFactoryAPITestApp), fare clic con il pulsante destro del mouse su **Riferimenti** e scegliere **Aggiungi riferimento**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-228">In the Solution Explorer, expand the project (DataFactoryAPITestApp), right-click **References**, and click **Add Reference**.</span></span> <span data-ttu-id="ac43f-229">Selezionare la casella di controllo per l'assembly **System.Configuration**</span><span class="sxs-lookup"><span data-stu-id="ac43f-229">Select check box for **System.Configuration** assembly.</span></span> <span data-ttu-id="ac43f-230">e fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-230">and click **OK**.</span></span>
16. <span data-ttu-id="ac43f-231">Compilare l'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="ac43f-231">Build the console application.</span></span> <span data-ttu-id="ac43f-232">Scegliere **Compila** dal menu e fare clic su **Compila soluzione**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-232">Click **Build** on the menu and click **Build Solution**.</span></span>
17. <span data-ttu-id="ac43f-233">Verificare che esista almeno un file nel contenitore **adftutorial** nell'archivio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac43f-233">Confirm that there is at least one file in the **adftutorial** container in your Azure blob storage.</span></span> <span data-ttu-id="ac43f-234">In caso contrario, creare il file **Emp.txt** nel Blocco note con il contenuto seguente e caricarlo nel contenitore adftutorial.</span><span class="sxs-lookup"><span data-stu-id="ac43f-234">If not, create **Emp.txt** file in Notepad with the following content and upload it to the adftutorial container.</span></span>

    ```
    John, Doe
    Jane, Doe
    ```
18. <span data-ttu-id="ac43f-235">Eseguire l'esempio scegliendo **Debug** -> **Avvia debug** dal menu.</span><span class="sxs-lookup"><span data-stu-id="ac43f-235">Run the sample by clicking **Debug** -> **Start Debugging** on the menu.</span></span> <span data-ttu-id="ac43f-236">Quando viene visualizzato un messaggio simile ad **Acquisizione dettagli dell'esecuzione di una sezione di dati**, attendere qualche minuto e premere **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-236">When you see the **Getting run details of a data slice**, wait for a few minutes, and press **ENTER**.</span></span>
19. <span data-ttu-id="ac43f-237">Usare il portale di Azure per verificare che la data factory **APITutorialFactory** venga creata con gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="ac43f-237">Use the Azure portal to verify that the data factory **APITutorialFactory** is created with the following artifacts:</span></span>
   * <span data-ttu-id="ac43f-238">Servizio collegato: **LinkedService_AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-238">Linked service: **LinkedService_AzureStorage**</span></span>
   * <span data-ttu-id="ac43f-239">Set di dati: **InputDataset** e **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="ac43f-239">Dataset: **InputDataset** and **OutputDataset**.</span></span>
   * <span data-ttu-id="ac43f-240">Pipeline: **PipelineBlobSample**</span><span class="sxs-lookup"><span data-stu-id="ac43f-240">Pipeline: **PipelineBlobSample**</span></span>
20. <span data-ttu-id="ac43f-241">Verificare che i due record dipendente vengano creati nella tabella **emp** del database SQL di Azure specificato.</span><span class="sxs-lookup"><span data-stu-id="ac43f-241">Verify that the two employee records are created in the **emp** table in the specified Azure SQL database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac43f-242">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac43f-242">Next steps</span></span>
<span data-ttu-id="ac43f-243">Per la documentazione completa sull'API .NET per Data Factory, vedere le [informazioni di riferimento sull'API NET di Data Factory](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span><span class="sxs-lookup"><span data-stu-id="ac43f-243">For complete documentation on .NET API for Data Factory, see [Data Factory .NET API Reference](/dotnet/api/index?view=azuremgmtdatafactories-4.12.1).</span></span>

<span data-ttu-id="ac43f-244">In questa esercitazione sono stati usati l'archivio BLOB di Azure come archivio dati di origine e un database SQL di Azure come archivio dati di destinazione in un'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="ac43f-244">In this tutorial, you used Azure blob storage as a source data store and an Azure SQL database as a destination data store in a copy operation.</span></span> <span data-ttu-id="ac43f-245">La tabella seguente contiene un elenco degli archivi dati supportati come origini e come destinazioni dall'attività di copia:</span><span class="sxs-lookup"><span data-stu-id="ac43f-245">The following table provides a list of data stores supported as sources and destinations by the copy activity:</span></span> 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

<span data-ttu-id="ac43f-246">Per informazioni su come copiare dati da/in un archivio dati, fare clic sul collegamento relativo all'archivio dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="ac43f-246">To learn about how to copy data to/from a data store, click the link for the data store in the table.</span></span>

