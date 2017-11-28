---
title: aaaUse tooaccess l'autenticazione di Azure AD API di servizi multimediali di Azure con .NET | Documenti Microsoft
description: Questo argomento viene illustrato come toouse tooaccess l'autenticazione di Azure Active Directory (Azure AD) di Azure Media Services API (AMS) con .NET.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: 2f750e460d9e476ad92e96adeac6500cb692cd77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-ad-authentication-tooaccess-azure-media-services-api-with-net"></a><span data-ttu-id="359eb-103">Utilizzare l'autenticazione di Azure AD tooaccess API di servizi multimediali di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="359eb-103">Use Azure AD authentication tooaccess Azure Media Services API with .NET</span></span>

<span data-ttu-id="359eb-104">A partire da windowsazure.mediaservices 4.0.0.4, Servizi multimediali di Azure supporta l'autenticazione basata su Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="359eb-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="359eb-105">In questo argomento illustra come toouse tooaccess l'autenticazione di Azure AD API di servizi multimediali di Azure con Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="359eb-105">This topic shows you how toouse Azure AD  authentication tooaccess Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="359eb-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="359eb-106">Prerequisites</span></span>

- <span data-ttu-id="359eb-107">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-107">An Azure account.</span></span> <span data-ttu-id="359eb-108">Per informazioni dettagliate, vedere la pagina relativa alla [versione di prova gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="359eb-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="359eb-109">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="359eb-109">A Media Services account.</span></span> <span data-ttu-id="359eb-110">Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-110">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="359eb-111">versione più recente Hello [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacchetto.</span><span class="sxs-lookup"><span data-stu-id="359eb-111">hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="359eb-112">Familiarità con l'argomento hello [accesso alle API di servizi multimediali Azure con panoramica dell'autenticazione AAD](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-112">Familiarity with hello topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="359eb-113">Quando si usa l'autenticazione di Azure AD con Servizi multimediali di Azure, è possibile eseguire l'autenticazione in uno di due modi:</span><span class="sxs-lookup"><span data-stu-id="359eb-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="359eb-114">**Autenticazione utente** autentica un utente hello app toointeract con risorse di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-114">**User authentication** authenticates a person who is using hello app toointeract with Azure Media Services resources.</span></span> <span data-ttu-id="359eb-115">applicazione interattiva Hello deve prima richiedere le credenziali utente hello.</span><span class="sxs-lookup"><span data-stu-id="359eb-115">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="359eb-116">Un esempio è un'applicazione console di gestione che viene utilizzata dagli utenti autorizzati toomonitor processi di codifica o di streaming live.</span><span class="sxs-lookup"><span data-stu-id="359eb-116">An example is a management console app that's used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="359eb-117">L'**autenticazione basata su un'entità servizio** consente di eseguire l'autenticazione di un servizio.</span><span class="sxs-lookup"><span data-stu-id="359eb-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="359eb-118">Le applicazioni che usano in genere questo metodo di autenticazione sono app che eseguono servizi daemon, servizi di livello intermedio o processi pianificati, ad esempio app Web, app per le funzioni, app per la logica, API o microservizi.</span><span class="sxs-lookup"><span data-stu-id="359eb-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="359eb-119">Attualmente, Servizi multimediali di Azure supporta un modello di autenticazione di Servizio di controllo di accesso Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="359eb-120">Tuttavia, autorizzazione di controllo di accesso verrà deprecato in 1 giugno 2018 toobe.</span><span class="sxs-lookup"><span data-stu-id="359eb-120">However, Access Control authorization is going toobe deprecated on June 1, 2018.</span></span> <span data-ttu-id="359eb-121">È consigliabile eseguire la migrazione di modello di autenticazione di Azure Active Directory tooan appena possibile.</span><span class="sxs-lookup"><span data-stu-id="359eb-121">We recommend that you migrate tooan Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="359eb-122">Ottenere un token di accesso di Azure AD</span><span class="sxs-lookup"><span data-stu-id="359eb-122">Get an Azure AD access token</span></span>

<span data-ttu-id="359eb-123">tooconnect toohello API di servizi multimediali di Azure con autenticazione di Azure AD, hello client app deve toorequest un token di accesso di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359eb-123">tooconnect toohello Azure Media Services API with Azure AD authentication, hello client app needs toorequest an Azure AD access token.</span></span> <span data-ttu-id="359eb-124">Quando si utilizza client .NET di servizi multimediali hello SDK, molti dei dettagli di hello sul tooacquire un token di accesso di Azure AD vengono incapsulati e semplificato per l'utente in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) e [AzureAdTokenCredentials ](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classi.</span><span class="sxs-lookup"><span data-stu-id="359eb-124">When you use hello Media Services .NET client SDK, many of hello details about how tooacquire an Azure AD access token are wrapped and simplified for you in hello [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="359eb-125">Ad esempio, non è necessario tooprovide hello Azure AD autorità, URI di risorsa di servizi multimediali oppure nativo dettagli dell'applicazione Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359eb-125">For example, you don't need tooprovide hello Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="359eb-126">Questi sono valori noti che sono già configurati per hello classe provider di token di accesso AD Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-126">These are well-known values that are already configured by hello Azure AD access token provider class.</span></span> 

<span data-ttu-id="359eb-127">Se non si utilizza .NET SDK servizi multimediali di Azure, è consigliabile utilizzare hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-127">If you are not using Azure Media Service .NET SDK, we recommend that you use hello [Azure AD Authentication Library](../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="359eb-128">vedere tooget valori per parametri hello necessari toouse con Azure AD Authentication Library [utilizzare impostazioni di autenticazione tooaccess portale Azure AD Azure hello](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-128">tooget values for hello parameters that you need toouse with Azure AD Authentication Library, see [Use hello Azure portal tooaccess Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="359eb-129">È inoltre possibile hello sostituire l'implementazione predefinita di hello di hello **AzureAdTokenProvider** con la propria implementazione.</span><span class="sxs-lookup"><span data-stu-id="359eb-129">You also have hello option of replacing hello default implementation of hello **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="359eb-130">Installare e configurare l'SDK .NET di Servizi multimediali di Azure</span><span class="sxs-lookup"><span data-stu-id="359eb-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="359eb-131">autenticazione toouse Azure AD con hello Media Services .NET SDK, è necessario toohave hello più recente [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) pacchetto.</span><span class="sxs-lookup"><span data-stu-id="359eb-131">toouse Azure AD authentication with hello Media Services .NET SDK, you need toohave hello latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="359eb-132">Inoltre, aggiungere un riferimento toohello **ActiveDirectory** assembly.</span><span class="sxs-lookup"><span data-stu-id="359eb-132">Also, add a reference toohello **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="359eb-133">Se si utilizza un'app esistente, includere hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span><span class="sxs-lookup"><span data-stu-id="359eb-133">If you are using an existing app, include hello **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="359eb-134">Creare una nuova applicazione console C# in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="359eb-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="359eb-135">Hello utilizzare [windowsazure. mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) tooinstall pacchetto NuGet **Azure Media Services .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="359eb-135">Use hello [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package tooinstall **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="359eb-136">tooadd riferimenti utilizzando NuGet, richiedere hello alla procedura seguente: in **Esplora**, nome del progetto hello e quindi scegliere **Gestione pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="359eb-136">tooadd references by using NuGet, take hello following steps: in **Solution Explorer**, right-click hello project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="359eb-137">Cercare quindi **windowsazure.mediaservices** e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="359eb-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="359eb-138">-oppure-</span><span class="sxs-lookup"><span data-stu-id="359eb-138">-or-</span></span>

    <span data-ttu-id="359eb-139">Esecuzione hello il seguente comando in **Package Manager Console** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="359eb-139">Run hello following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="359eb-140">Aggiungere **utilizzando** tooyour il codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="359eb-140">Add **using** tooyour source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="359eb-141">Usare l'autenticazione utente</span><span class="sxs-lookup"><span data-stu-id="359eb-141">Use user authentication</span></span>

<span data-ttu-id="359eb-142">tooconnect toohello API del servizio di supporto di Azure con l'opzione di autenticazione utente hello, hello client app deve toorequest un token di Azure AD tramite hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="359eb-142">tooconnect toohello Azure Media Service API with hello user authentication option, hello client app needs toorequest an Azure AD token by using hello following parameters:</span></span>  

- <span data-ttu-id="359eb-143">Endpoint tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359eb-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="359eb-144">le informazioni sul tenant Hello possono essere recuperate da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-144">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="359eb-145">Passare il mouse su hello utente connesso nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="359eb-145">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="359eb-146">URI di risorsa per Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="359eb-146">Media Services resource URI.</span></span>
- <span data-ttu-id="359eb-147">ID client dell'applicazione Servizi multimediali (nativa).</span><span class="sxs-lookup"><span data-stu-id="359eb-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="359eb-148">URI di reindirizzamento dell'applicazione Servizi multimediali (nativa).</span><span class="sxs-lookup"><span data-stu-id="359eb-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="359eb-149">i valori Hello per questi parametri possono essere disponibili nella **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="359eb-149">hello values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="359eb-150">Hello **AzureEnvironments.AzureCloudEnvironment** costante è un supporto in hello .NET SDK tooget impostazioni delle variabili di ambiente destra hello per un Data Center di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="359eb-150">hello **AzureEnvironments.AzureCloudEnvironment** constant is a helper in hello .NET SDK tooget hello right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="359eb-151">Contiene le impostazioni di ambiente predefinite per l'accesso a servizi multimediali di hello solo i centri dati pubblici.</span><span class="sxs-lookup"><span data-stu-id="359eb-151">It contains pre-defined environment settings for accessing Media Services in hello public data centers only.</span></span> <span data-ttu-id="359eb-152">Per le regioni cloud sovrane o governative è possibile usare rispettivamente **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvironment** o **AzureGermanCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="359eb-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="359eb-153">Hello esempio di codice seguente viene creato un token:</span><span class="sxs-lookup"><span data-stu-id="359eb-153">hello following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="359eb-154">toostart programmazione in servizi multimediali, è necessario toocreate un **CloudMediaContext** istanza che rappresenta il contesto di server hello.</span><span class="sxs-lookup"><span data-stu-id="359eb-154">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="359eb-155">Hello **CloudMediaContext** include riferimenti tooimportant insiemi inclusi i processi, asset, file, i criteri di accesso e localizzatori.</span><span class="sxs-lookup"><span data-stu-id="359eb-155">hello **CloudMediaContext** includes references tooimportant collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="359eb-156">È inoltre necessario hello toopass **URI per i servizi REST di supporti della risorsa** toohello **CloudMediaContext** costruttore.</span><span class="sxs-lookup"><span data-stu-id="359eb-156">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="359eb-157">URI della risorsa hello tooget per i servizi REST di supporti, accedi toohello portale di Azure, selezionare l'account di servizi multimediali di Azure, selezionare **l'accesso all'API**, quindi selezionare **la connessione di servizi multimediali tooAzure con l'utente autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="359eb-157">tooget hello resource URI for Media REST Services, sign in toohello Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect tooAzure Media Services with user authentication**.</span></span> 

<span data-ttu-id="359eb-158">Hello codice seguente viene creato un **CloudMediaContext** istanza:</span><span class="sxs-lookup"><span data-stu-id="359eb-158">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="359eb-159">Hello di esempio seguente viene illustrato come toocreate hello il contesto di token e hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="359eb-159">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="359eb-160">Se si verifica un'eccezione che indica "server remoto hello ha restituito un errore: non autorizzato (401)," hello vedere [il controllo degli accessi](media-services-use-aad-auth-to-access-ams-api.md#access-control) sezione di accesso alle API di servizi multimediali Azure con panoramica dell'autenticazione AD Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-160">If you get an exception that says "hello remote server returned an error: (401) Unauthorized," see hello [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="359eb-161">Usare l'autenticazione basata su entità servizio</span><span class="sxs-lookup"><span data-stu-id="359eb-161">Use service principal authentication</span></span>
    
<span data-ttu-id="359eb-162">tooconnect toohello API di servizi multimediali di Azure con l'opzione dell'entità servizio di hello, l'applicazione di livello intermedio (API web o applicazione web) con, è necessario un token di Azure AD toorequests hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="359eb-162">tooconnect toohello Azure Media Services API with hello service principal option, your middle-tier app (web API or web application) needs toorequests an Azure AD token with hello following parameters:</span></span>  

- <span data-ttu-id="359eb-163">Endpoint tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="359eb-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="359eb-164">le informazioni sul tenant Hello possono essere recuperate da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-164">hello tenant information can be retrieved from hello Azure portal.</span></span> <span data-ttu-id="359eb-165">Passare il mouse su hello utente connesso nell'angolo superiore destro di hello.</span><span class="sxs-lookup"><span data-stu-id="359eb-165">Hover over hello signed-in user in hello upper-right corner.</span></span>
- <span data-ttu-id="359eb-166">URI di risorsa per Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="359eb-166">Media Services resource URI.</span></span>
- <span data-ttu-id="359eb-167">I valori dell'applicazione Azure AD: hello **ID Client** e **segreto Client**.</span><span class="sxs-lookup"><span data-stu-id="359eb-167">Azure AD application values: hello **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="359eb-168">i valori per hello Hello **ID Client** e **segreto Client** parametri è reperibile nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="359eb-168">hello values for hello **Client ID** and **Client secret** parameters can be found in hello Azure portal.</span></span> <span data-ttu-id="359eb-169">Per ulteriori informazioni, vedere [Introduzione a Azure AD mediante l'autenticazione hello Azure portal](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-169">For more information, see [Getting started with Azure AD authentication using hello Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="359eb-170">Hello esempio di codice seguente crea un token tramite hello **AzureAdTokenCredentials** costruttore che accetta **AzureAdClientSymmetricKey** come parametro:</span><span class="sxs-lookup"><span data-stu-id="359eb-170">hello following code example creates a token by using hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="359eb-171">È inoltre possibile specificare hello **AzureAdTokenCredentials** costruttore che accetta **AzureAdClientCertificate** come parametro.</span><span class="sxs-lookup"><span data-stu-id="359eb-171">You can also specify hello **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="359eb-172">Per istruzioni su come toocreate e configurare un certificato in un formato che può essere utilizzato da Azure AD, vedere [tooAzure AD App daemon con certificati - passaggi di configurazione manuale di autenticazione](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-172">For instructions about how toocreate and configure a certificate in a form that can be used by Azure AD, see [Authenticating tooAzure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="359eb-173">toostart programmazione in servizi multimediali, è necessario toocreate un **CloudMediaContext** istanza che rappresenta il contesto di server hello.</span><span class="sxs-lookup"><span data-stu-id="359eb-173">toostart programming against Media Services, you need toocreate a **CloudMediaContext** instance that represents hello server context.</span></span> <span data-ttu-id="359eb-174">È inoltre necessario hello toopass **URI per i servizi REST di supporti della risorsa** toohello **CloudMediaContext** costruttore.</span><span class="sxs-lookup"><span data-stu-id="359eb-174">You also need toopass hello **resource URI for Media REST Services** toohello **CloudMediaContext** constructor.</span></span> <span data-ttu-id="359eb-175">È possibile ottenere hello **URI per i servizi REST di supporti della risorsa** valore hello anche portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="359eb-175">You can get hello **resource URI for Media REST Services** value from hello Azure portal as well.</span></span>

<span data-ttu-id="359eb-176">Hello codice seguente viene creato un **CloudMediaContext** istanza:</span><span class="sxs-lookup"><span data-stu-id="359eb-176">hello following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="359eb-177">Hello di esempio seguente viene illustrato come toocreate hello il contesto di token e hello Azure AD:</span><span class="sxs-lookup"><span data-stu-id="359eb-177">hello following example shows how toocreate hello Azure AD token and hello context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="359eb-178">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="359eb-178">Next steps</span></span>

<span data-ttu-id="359eb-179">Introduzione a [caricamento file account tooyour](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="359eb-179">Get started with [uploading files tooyour account](media-services-dotnet-upload-files.md).</span></span>
