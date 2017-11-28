---
title: applicazioni di toodevelop aaaUse hello .NET SDK in archivio Azure Data Lake | Documenti Microsoft
description: Utilizzare SDK .NET di Azure Data Lake archivio toocreate un account archivio Data Lake ed eseguire operazioni di base in hello archivio Data Lake
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
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="ce4ab-103">Introduzione ad Azure Data Lake Store con .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ce4ab-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ce4ab-104">Portale</span><span class="sxs-lookup"><span data-stu-id="ce4ab-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ce4ab-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce4ab-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ce4ab-106">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="ce4ab-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ce4ab-107">SDK per Java</span><span class="sxs-lookup"><span data-stu-id="ce4ab-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ce4ab-108">API REST</span><span class="sxs-lookup"><span data-stu-id="ce4ab-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ce4ab-109">Interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ce4ab-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ce4ab-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="ce4ab-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ce4ab-111">Python</span><span class="sxs-lookup"><span data-stu-id="ce4ab-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="ce4ab-112">Informazioni su come hello toouse [Azure Data Lake archivio .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform operazioni di base, ad esempio, creare cartelle, caricare e scaricare i file di dati e così via. Per altre informazioni su Data Lake, vedere [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ab-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ce4ab-113">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ce4ab-113">Prerequisites</span></span>
* <span data-ttu-id="ce4ab-114">**Visual Studio 2013, 2015 o 2017**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="ce4ab-115">istruzioni di Hello seguente si usa Visual Studio 2015 Update 2.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="ce4ab-116">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-116">**An Azure subscription**.</span></span> <span data-ttu-id="ce4ab-117">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ce4ab-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="ce4ab-118">**Account di Archivio Data Lake di Azure**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="ce4ab-119">Per istruzioni su come toocreate un account, vedere [introduzione archivio Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ce4ab-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="ce4ab-120">**Creare un'applicazione di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="ce4ab-121">Utilizzare un'applicazione hello Azure AD applicazione tooauthenticate hello archivio Data Lake con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="ce4ab-122">Esistono diversi approcci tooauthenticate con Azure AD, che sono **autenticazione dell'utente finale** o **authentication service to service**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ce4ab-123">Per istruzioni e ulteriori informazioni su come tooauthenticate, vedere [autenticazione dell'utente finale](data-lake-store-end-user-authenticate-using-active-directory.md) o [authentication Service to service](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ab-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="ce4ab-124">Creare un'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="ce4ab-124">Create a .NET application</span></span>
1. <span data-ttu-id="ce4ab-125">Aprire Visual Studio e creare un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="ce4ab-126">Da hello **File** menu, fare clic su **New**, quindi fare clic su **progetto**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="ce4ab-127">Da **nuovo progetto**digitare o selezionare hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="ce4ab-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="ce4ab-128">Proprietà</span><span class="sxs-lookup"><span data-stu-id="ce4ab-128">Property</span></span> | <span data-ttu-id="ce4ab-129">Valore</span><span class="sxs-lookup"><span data-stu-id="ce4ab-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="ce4ab-130">Categoria</span><span class="sxs-lookup"><span data-stu-id="ce4ab-130">Category</span></span> |<span data-ttu-id="ce4ab-131">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="ce4ab-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="ce4ab-132">Modello</span><span class="sxs-lookup"><span data-stu-id="ce4ab-132">Template</span></span> |<span data-ttu-id="ce4ab-133">Applicazione console</span><span class="sxs-lookup"><span data-stu-id="ce4ab-133">Console Application</span></span> |
   | <span data-ttu-id="ce4ab-134">Nome</span><span class="sxs-lookup"><span data-stu-id="ce4ab-134">Name</span></span> |<span data-ttu-id="ce4ab-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="ce4ab-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="ce4ab-136">Fare clic su **OK** progetto hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="ce4ab-137">Aggiungere hello Nuget pacchetti tooyour progetto.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="ce4ab-138">Nome del progetto in Esplora soluzioni hello hello destro e fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="ce4ab-139">In hello **Gestione pacchetti Nuget** scheda, assicurarsi che **origine pacchetto** è troppo**nuget.org** e che **Includi versione preliminare** casella di controllo viene selezionato.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="ce4ab-140">Cercare e installare i seguenti pacchetti NuGet hello:</span><span class="sxs-lookup"><span data-stu-id="ce4ab-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="ce4ab-141">`Microsoft.Azure.Management.DataLake.Store` - Questa esercitazione usa v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="ce4ab-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - Questa esercitazione usa la versione 2.2.12.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="ce4ab-143">![Aggiungere un'origine Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Creare un nuovo account di Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="ce4ab-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="ce4ab-144">Chiude hello **Gestione pacchetti Nuget**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="ce4ab-145">Aprire **Program.cs**, eliminare il codice esistente hello e quindi includere hello seguendo le istruzioni tooadd riferimenti toonamespaces.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="ce4ab-146">Dichiarare le variabili di hello come illustrato di seguito e fornire i valori hello per nome di archivio Data Lake e nome di gruppo di risorse hello che esiste già.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="ce4ab-147">Assicurarsi inoltre che deve essere presente nel computer di hello hello percorso e il nome locale che qui.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="ce4ab-148">Aggiungere hello seguente frammento di codice dopo le dichiarazioni dello spazio dei nomi di hello.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-148">Add hello following code snippet after hello namespace declarations.</span></span>

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
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="ce4ab-149">In hello rimanenti sezioni dell'articolo hello, è possibile visualizzare come toouse hello .NET metodi tooperform le operazioni disponibili, ad esempio l'autenticazione, il caricamento di file e così via.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="ce4ab-150">Autenticazione</span><span class="sxs-lookup"><span data-stu-id="ce4ab-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="ce4ab-151">Se si usa l'autenticazione dell'utente finale (consigliata per questa esercitazione)</span><span class="sxs-lookup"><span data-stu-id="ce4ab-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="ce4ab-152">Utilizzare con un'applicazione nativa tooauthenticate di esistente AD Azure, l'applicazione **in modo interattivo**, che significa che sarà richiesto tooenter le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="ce4ab-153">Per semplicità, frammento hello seguente utilizza valori predefiniti per ID client e reindirizzamento URI che funzioneranno con qualsiasi sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="ce4ab-154">toohelp aver completato questa esercitazione più velocemente, è consigliabile che utilizzare questo approccio.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="ce4ab-155">Nel seguente frammento di hello, è sufficiente fornire il valore di hello per l'ID del tenant.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="ce4ab-156">È possibile recuperare tramite istruzioni hello disponibili all'indirizzo [creare un'applicazione di Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ab-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="ce4ab-157">Un paio di aspetti tooknow su questo frammento di codice precedente:</span><span class="sxs-lookup"><span data-stu-id="ce4ab-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="ce4ab-158">Questo frammento di codice toohelp completare l'esercitazione hello più velocemente, utilizza una Azure Active Directory ID client e di dominio che è disponibile per impostazione predefinita per tutte le sottoscrizioni di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="ce4ab-159">È quindi possibile **usare questo frammento così com'è nell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="ce4ab-160">Tuttavia, se desidera toouse il proprio dominio di Azure AD e ID client dell'applicazione, è necessario creare un'applicazione nativa AD Azure e quindi utilizzare hello Azure AD tenant ID, ID client e URI di reindirizzamento per un'applicazione hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="ce4ab-161">Per istruzioni, vedere [Autenticazione dell'utente finale con Data Lake Store tramite Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ab-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="ce4ab-162">Se si usa l'autenticazione da servizio a servizio con il segreto client</span><span class="sxs-lookup"><span data-stu-id="ce4ab-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="ce4ab-163">Hello seguente frammento di codice può essere utilizzato tooauthenticate applicazione **in modo non interattivo**, utilizzando la chiave privata client hello / chiave per un'entità servizio / dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="ce4ab-164">Usare il frammento con una "app Web" di Azure AD esistente.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="ce4ab-165">Per istruzioni su come visualizzare un'applicazione web toocreate hello Azure AD e come tooretrieve hello client ID e segreto client richiesto nel seguente frammento di hello [creare applicazione Active Directory per l'autenticazione al servizio dati Archivio Lake](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ce4ab-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="ce4ab-166">Se si usa l'autenticazione da servizio a servizio con il certificato</span><span class="sxs-lookup"><span data-stu-id="ce4ab-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="ce4ab-167">Come una terza opzione, hello seguente frammento di codice può essere utilizzato tooauthenticate applicazione **in modo non interattivo**, per un'applicazione Azure Active Directory utilizza certificato hello / entità di servizio.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="ce4ab-168">Usare il frammento con un'[applicazione di Azure AD con certificati](../azure-resource-manager/resource-group-authenticate-service-principal.md) esistente.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="ce4ab-169">Creare oggetti client</span><span class="sxs-lookup"><span data-stu-id="ce4ab-169">Create client objects</span></span>
<span data-ttu-id="ce4ab-170">Hello frammento di codice seguente crea account archivio Data Lake hello e filesystem oggetti client, che vengono utilizzati tooissue richiede toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="ce4ab-171">Elencare tutti gli account Data Lake Store all'interno di una sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="ce4ab-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="ce4ab-172">Hello frammento di codice seguente sono elencati tutti gli account archivio Data Lake all'interno di una specifica sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
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

## <a name="create-a-directory"></a><span data-ttu-id="ce4ab-173">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="ce4ab-173">Create a directory</span></span>
<span data-ttu-id="ce4ab-174">Hello seguente mostra un `CreateDirectory` metodo che è possibile utilizzare una directory all'interno di un account archivio Data Lake toocreate.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="ce4ab-175">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="ce4ab-175">Upload a file</span></span>
<span data-ttu-id="ce4ab-176">Hello seguente mostra un `UploadFile` metodo che è possibile utilizzare tooupload file account archivio Data Lake tooa.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="ce4ab-177">Hello SDK supporta ricorsiva caricamento e download tra un percorso file locale e un percorso di file di archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="ce4ab-178">Ottenere informazioni su un file o una directory</span><span class="sxs-lookup"><span data-stu-id="ce4ab-178">Get file or directory info</span></span>
<span data-ttu-id="ce4ab-179">Hello seguente mostra un `GetItemInfo` metodo che è possibile utilizzare un file o directory disponibili tooretrieve informazioni nell'archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="ce4ab-180">Elencare file o directory</span><span class="sxs-lookup"><span data-stu-id="ce4ab-180">List file or directories</span></span>
<span data-ttu-id="ce4ab-181">Hello seguente mostra un `ListItem` metodo che è possibile utilizzare toolist hello file e directory in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="ce4ab-182">Concatenare file</span><span class="sxs-lookup"><span data-stu-id="ce4ab-182">Concatenate files</span></span>
<span data-ttu-id="ce4ab-183">Hello seguente mostra un `ConcatenateFiles` metodo utilizzare file tooconcatenate.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="ce4ab-184">Aggiungere file tooa</span><span class="sxs-lookup"><span data-stu-id="ce4ab-184">Append tooa file</span></span>
<span data-ttu-id="ce4ab-185">Hello seguente mostra un `AppendToFile` metodo da utilizzare accodare il file di tooa dati già archiviati in un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="ce4ab-186">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="ce4ab-186">Download a file</span></span>
<span data-ttu-id="ce4ab-187">Hello seguente mostra un `DownloadFile` metodo utilizzare toodownload un file da un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="ce4ab-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="ce4ab-188">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ce4ab-188">Next steps</span></span>
* [<span data-ttu-id="ce4ab-189">Proteggere i dati in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ce4ab-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="ce4ab-190">Usare Azure Data Lake Analytics con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ce4ab-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ce4ab-191">Usare Azure HDInsight con Archivio Data Lake</span><span class="sxs-lookup"><span data-stu-id="ce4ab-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="ce4ab-192">Informazioni di riferimento su .NET SDK con Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ce4ab-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="ce4ab-193">Data Lake Store REST Reference (Informazioni di riferimento su REST per Data Lake Store)</span><span class="sxs-lookup"><span data-stu-id="ce4ab-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
