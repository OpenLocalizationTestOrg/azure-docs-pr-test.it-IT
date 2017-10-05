---
title: Usare .NET SDK per sviluppare applicazioni in Azure Data Lake Store | Documentazione Microsoft
description: Usare .NET SDK con Azure Data Lake Store per creare un account Data Lake Store ed eseguire le relative operazioni di base
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: 70f94a07b0102e3135eaf85e5877e3502762d7e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="c6536-103">Introduzione ad Azure Data Lake Store con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c6536-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c6536-104">Portale</span><span class="sxs-lookup"><span data-stu-id="c6536-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="c6536-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6536-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="c6536-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="c6536-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="c6536-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="c6536-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="c6536-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c6536-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="c6536-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="c6536-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="c6536-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="c6536-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="c6536-111">Python</span><span class="sxs-lookup"><span data-stu-id="c6536-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="c6536-112">Informazioni su come usare [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) per eseguire operazioni di base, ad esempio creare cartelle, caricare e scaricare file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c6536-112">Learn how to use the [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) to perform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c6536-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c6536-113">Prerequisites</span></span>
* <span data-ttu-id="c6536-114">**Visual Studio 2013, 2015 o 2017**.</span><span class="sxs-lookup"><span data-stu-id="c6536-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="c6536-115">Le istruzioni seguenti fanno riferimento a Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="c6536-115">The instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="c6536-116">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6536-116">**An Azure subscription**.</span></span> <span data-ttu-id="c6536-117">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c6536-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="c6536-118">**Account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="c6536-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="c6536-119">Per istruzioni su come creare un account, vedere [Introduzione ad Azure Data Lake Store tramite il portale di Azure](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c6536-119">For instructions on how to create an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="c6536-120">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c6536-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="c6536-121">Usare l'applicazione Azure AD per autenticare l'applicazione Data Lake Store con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c6536-121">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="c6536-122">Per l'autenticazione con Azure AD è possibile usare l'**autenticazione dell'utente finale** o l'**autenticazione da servizio a servizio**.</span><span class="sxs-lookup"><span data-stu-id="c6536-122">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="c6536-123">Per altre informazioni e istruzioni su come eseguire l'autenticazione, vedere [Autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [Autenticazione da servizio a servizio](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c6536-123">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="c6536-124">Creare un'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="c6536-124">Create a .NET application</span></span>
1. <span data-ttu-id="c6536-125">Aprire Visual Studio e creare un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="c6536-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="c6536-126">Scegliere **Nuovo** dal menu **File** e quindi fare clic su **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="c6536-126">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="c6536-127">In **Nuovo progetto**digitare o selezionare i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6536-127">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="c6536-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="c6536-128">Property</span></span> | <span data-ttu-id="c6536-129">Valore</span><span class="sxs-lookup"><span data-stu-id="c6536-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="c6536-130">Categoria</span><span class="sxs-lookup"><span data-stu-id="c6536-130">Category</span></span> |<span data-ttu-id="c6536-131">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="c6536-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="c6536-132">Modello</span><span class="sxs-lookup"><span data-stu-id="c6536-132">Template</span></span> |<span data-ttu-id="c6536-133">Applicazione console</span><span class="sxs-lookup"><span data-stu-id="c6536-133">Console Application</span></span> |
   | <span data-ttu-id="c6536-134">Nome</span><span class="sxs-lookup"><span data-stu-id="c6536-134">Name</span></span> |<span data-ttu-id="c6536-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="c6536-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="c6536-136">Fare clic su **OK** per creare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c6536-136">Click **OK** to create the project.</span></span>
5. <span data-ttu-id="c6536-137">Aggiungere i pacchetti NuGet al progetto.</span><span class="sxs-lookup"><span data-stu-id="c6536-137">Add the Nuget packages to your project.</span></span>

   1. <span data-ttu-id="c6536-138">Fare clic con il pulsante destro del mouse sul nome del progetto in Esplora soluzioni e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c6536-138">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="c6536-139">Nella scheda **Gestione pacchetti NuGet** verificare che l'opzione **Origine pacchetto** sia impostata su **nuget.org** e che la casella di controllo **Includi versione preliminare** sia selezionata.</span><span class="sxs-lookup"><span data-stu-id="c6536-139">In the **Nuget Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="c6536-140">Cercare e installare i pacchetti NuGet seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6536-140">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="c6536-141">`Microsoft.Azure.Management.DataLake.Store` - Questa esercitazione usa v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="c6536-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="c6536-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - Questa esercitazione usa la versione 2.2.12.</span><span class="sxs-lookup"><span data-stu-id="c6536-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="c6536-143">![Aggiungere un'origine Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Creare un nuovo account di Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="c6536-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="c6536-144">Chiudere la finestra **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c6536-144">Close the **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="c6536-145">Aprire **Program.cs**, eliminare il codice esistente e quindi includere le istruzioni seguenti per aggiungere riferimenti agli spazi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="c6536-145">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="c6536-146">Dichiarare le variabili come illustrato di seguito e specificare i valori per il nome di Data Lake Store e il nome del gruppo di risorse già esistenti.</span><span class="sxs-lookup"><span data-stu-id="c6536-146">Declare the variables as shown below, and provide the values for Data Lake Store name and the resource group name that already exist.</span></span> <span data-ttu-id="c6536-147">Assicurarsi anche che il nome file e percorso locale forniti esistano già nel computer.</span><span class="sxs-lookup"><span data-stu-id="c6536-147">Also, make sure the local path and file name you provide here must exist on the computer.</span></span> <span data-ttu-id="c6536-148">Aggiungere il frammento di codice seguente dopo le dichiarazioni dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="c6536-148">Add the following code snippet after the namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with the name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with the name of the resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="c6536-149">Nelle sezioni rimanenti dell'articolo è possibile vedere come usare i metodi .NET disponibili per eseguire operazioni come autenticazione, caricamento di file e così via.</span><span class="sxs-lookup"><span data-stu-id="c6536-149">In the remaining sections of the article, you can see how to use the available .NET methods to perform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="c6536-150">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="c6536-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="c6536-151">Se si usa l'autenticazione dell'utente finale (consigliata per questa esercitazione)</span><span class="sxs-lookup"><span data-stu-id="c6536-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="c6536-152">Usare questo codice con un'applicazione nativa esistente di Azure AD per autenticare l'applicazione **in modo interattivo**, ovvero con la richiesta di immettere le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6536-152">Use this with an existing Azure AD native application to authenticate your application **interactively**, which means you will be prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="c6536-153">Per semplicità, il frammento seguente usa valori predefiniti per ID client e URI di reindirizzamento, funzionanti con qualsiasi sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6536-153">For ease of use, the snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="c6536-154">Per completare più rapidamente questa esercitazione, è consigliabile adottare questo approccio.</span><span class="sxs-lookup"><span data-stu-id="c6536-154">To help you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="c6536-155">Nel frammento seguente specificare semplicemente il valore per l'ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="c6536-155">In the snippet below, just provide the value for your tenant ID.</span></span> <span data-ttu-id="c6536-156">È possibile recuperarlo usando le istruzioni disponibili in [Creare un'applicazione di Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c6536-156">You can retrieve it using the instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use the client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with the user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="c6536-157">Informazioni utili sul frammento di codice precedente:</span><span class="sxs-lookup"><span data-stu-id="c6536-157">A couple of things to know about this snippet above:</span></span>

* <span data-ttu-id="c6536-158">Per completare più rapidamente l'esercitazione, questo frammento di codice usa un dominio di Azure AD e un ID client disponibili per impostazione predefinita per tutte le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6536-158">To help you complete the tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="c6536-159">È quindi possibile **usare questo frammento così com'è nell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="c6536-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="c6536-160">Se, tuttavia, si vuole usare il proprio dominio di Azure AD e il proprio ID client dell'applicazione, è necessario creare un'applicazione nativa di Azure AD e quindi usare l'ID tenant di Azure AD, l'ID client e l'URI di reindirizzamento per l'applicazione creata.</span><span class="sxs-lookup"><span data-stu-id="c6536-160">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="c6536-161">Per istruzioni, vedere [Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c6536-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="c6536-162">Se si usa l'autenticazione da servizio a servizio con il segreto client</span><span class="sxs-lookup"><span data-stu-id="c6536-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="c6536-163">Il frammento di codice seguente può essere usato per autenticare l'applicazione in modo **non interattivo**, usando il segreto client, la chiave per un'applicazione o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="c6536-163">The following snippet can be used to authenticate your application **non-interactively**, using the client secret / key for an application / service principal.</span></span> <span data-ttu-id="c6536-164">Usare il frammento con una "app Web" di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="c6536-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="c6536-165">Per istruzioni su come creare l'applicazione Web di Azure AD e come recuperare l'ID client e il segreto client richiesti nel frammento di codice seguente, vedere [Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c6536-165">For instructions on how to create the Azure AD web application and how to retrieve the client ID and client secret required in the snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use the client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="c6536-166">Se si usa l'autenticazione da servizio a servizio con il certificato</span><span class="sxs-lookup"><span data-stu-id="c6536-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="c6536-167">Come terza opzione, il frammento seguente può essere usato per autenticare l'applicazione in modo **non interattivo**, usando il certificato per un'applicazione di Azure Active Directory o un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="c6536-167">As a third option, the following snippet can be used to authenticate your application **non-interactively**, using the certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="c6536-168">Usare il frammento con un'[applicazione di Azure AD con certificati](../azure-resource-manager/resource-group-authenticate-service-principal.md) esistente.</span><span class="sxs-lookup"><span data-stu-id="c6536-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use the client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="c6536-169">Creare oggetti client</span><span class="sxs-lookup"><span data-stu-id="c6536-169">Create client objects</span></span>
<span data-ttu-id="c6536-170">Il frammento seguente crea gli account Data Lake Store e gli oggetti client del file system, usati per inviare richieste al servizio.</span><span class="sxs-lookup"><span data-stu-id="c6536-170">The following snippet creates the Data Lake Store account and filesystem client objects, which are used to issue requests to the service.</span></span>

    // Create client objects and set the subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="c6536-171">Elencare tutti gli account Data Lake Store all'interno di una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="c6536-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="c6536-172">Il frammento seguente elenca tutti gli account Data Lake Store all'interno di una determinata sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6536-172">The following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within the subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="c6536-173">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="c6536-173">Create a directory</span></span>
<span data-ttu-id="c6536-174">Il frammento seguente illustra il metodo `CreateDirectory` che è possibile usare per creare una directory in un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-174">The following snippet shows a `CreateDirectory` method that you can use to create a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="c6536-175">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="c6536-175">Upload a file</span></span>
<span data-ttu-id="c6536-176">Il frammento seguente illustra il metodo `UploadFile` che è possibile usare per caricare file in un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-176">The following snippet shows an `UploadFile` method that you can use to upload files to a Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="c6536-177">L'SDK supporta il caricamento e il download ricorsivi tra un percorso di file locale e un percorso di file Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-177">The SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="c6536-178">Ottenere informazioni su un file o una directory</span><span class="sxs-lookup"><span data-stu-id="c6536-178">Get file or directory info</span></span>
<span data-ttu-id="c6536-179">Il frammento seguente illustra il metodo `GetItemInfo` che è possibile usare per recuperare informazioni su un file o una directory disponibile in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-179">The following snippet shows a `GetItemInfo` method that you can use to retrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="c6536-180">Elencare file o directory</span><span class="sxs-lookup"><span data-stu-id="c6536-180">List file or directories</span></span>
<span data-ttu-id="c6536-181">Il frammento seguente illustra il metodo `ListItem` che è possibile usare per elencare il file e le directory in un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-181">The following snippet shows a `ListItem` method that can use to list the file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="c6536-182">Concatenare file</span><span class="sxs-lookup"><span data-stu-id="c6536-182">Concatenate files</span></span>
<span data-ttu-id="c6536-183">Il frammento seguente illustra il metodo `ConcatenateFiles` da usare per concatenare file.</span><span class="sxs-lookup"><span data-stu-id="c6536-183">The following snippet shows a `ConcatenateFiles` method that you use to concatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-to-a-file"></a><span data-ttu-id="c6536-184">Aggiungere a un file</span><span class="sxs-lookup"><span data-stu-id="c6536-184">Append to a file</span></span>
<span data-ttu-id="c6536-185">Il frammento seguente illustra il metodo `AppendToFile` da usare per aggiungere dati a un file già archiviato in un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-185">The following snippet shows a `AppendToFile` method that you use append data to a file already stored in a Data Lake Store account.</span></span>

    // Append to file
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="c6536-186">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="c6536-186">Download a file</span></span>
<span data-ttu-id="c6536-187">Il frammento seguente illustra il metodo `DownloadFile` da usare per scaricare un file da un account Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c6536-187">The following snippet shows a `DownloadFile` method that you use to download a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="c6536-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c6536-188">Next steps</span></span>
* [<span data-ttu-id="c6536-189">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c6536-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="c6536-190">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c6536-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="c6536-191">Usare Azure HDInsight con Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="c6536-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="c6536-192">Informazioni di riferimento su .NET SDK con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c6536-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="c6536-193">Data Lake Store REST Reference (Informazioni di riferimento su REST per Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="c6536-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
