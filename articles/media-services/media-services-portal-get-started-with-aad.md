---
title: Introduzione all'autenticazione di Azure AD tramite il portale di Azure| Microsoft Docs
description: Informazioni su come usare il portale di Azure per accedere all'autenticazione di Azure Active Directory (Azure AD) per usare l'API Servizi multimediali di Azure.
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
ms.openlocfilehash: 829e0759f8aeb8758f6b8895b88b60b66ffb22ed
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-the-azure-portal"></a><span data-ttu-id="ebbfa-103">Introduzione all'autenticazione di Azure AD tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ebbfa-103">Get started with Azure AD authentication by using the Azure portal</span></span>

<span data-ttu-id="ebbfa-104">Informazioni su come usare il portale di Azure per accedere all'autenticazione di Azure Active Directory (Azure AD) per accedere all'API Servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-104">Learn how to use the Azure portal to access Azure Active Directory (Azure AD) authentication to access the Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ebbfa-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="ebbfa-105">Prerequisites</span></span>

- <span data-ttu-id="ebbfa-106">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-106">An Azure account.</span></span> <span data-ttu-id="ebbfa-107">Se non si dispone di un account, iniziare con una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="ebbfa-108">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-108">A Media Services account.</span></span> <span data-ttu-id="ebbfa-109">Per altre informazioni, vedere [Creare un account Servizi multimediali di Azure con il portale di Azure](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-109">For more information, see [Create an Azure Media Services account by using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="ebbfa-110">Assicurarsi di rivedere l'argomento di [panoramica dell'accesso all'API Servizi multimediali di Azure con autenticazione Azure Active Directory](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-110">Make sure you review the [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="ebbfa-111">Quando si usa l'autenticazione di Azure AD con Servizi multimediali di Azure, sono disponibili due opzioni di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="ebbfa-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="ebbfa-112">**Autenticazione utente**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-112">**User authentication**.</span></span> <span data-ttu-id="ebbfa-113">Consente di autenticare una persona che usa l'app per interagire con le risorse di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-113">Authenticate a person who is using the app to interact with Media Services resources.</span></span> <span data-ttu-id="ebbfa-114">L'applicazione interattiva deve prima richiedere all'utente le credenziali.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-114">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="ebbfa-115">Un esempio è un'app della console di gestione usata dagli utenti autorizzati per monitorare i processi di codifica o lo streaming live.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-115">An example is a management console app used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="ebbfa-116">**Autenticazione basata su entità servizio**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-116">**Service principal authentication**.</span></span> <span data-ttu-id="ebbfa-117">Consente di autenticare un servizio.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-117">Authenticate a service.</span></span> <span data-ttu-id="ebbfa-118">Le applicazioni che solitamente usano questo metodo di autenticazione sono app che eseguono servizi daemon, servizi di livello intermedio o processi pianificati, ad esempio App Web, app per le funzioni, app per la logica, API o microservizi.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ebbfa-119">Servizi multimediali supporta attualmente il modello di autenticazione del Servizio di controllo di accesso di Azure.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-119">Currently, Media Services supports the Azure Access Control service authentication model.</span></span> <span data-ttu-id="ebbfa-120">L'autorizzazione di Controllo di accesso, tuttavia, verrà dichiarata deprecata il 1° giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="ebbfa-121">È consigliabile eseguire al più presto la migrazione al modello di autenticazione di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-121">We recommend that you migrate to the Azure AD authentication model as soon as possible.</span></span>

## <a name="select-the-authentication-method"></a><span data-ttu-id="ebbfa-122">Selezionare il metodo di autenticazione</span><span class="sxs-lookup"><span data-stu-id="ebbfa-122">Select the authentication method</span></span>

1. <span data-ttu-id="ebbfa-123">Nel [portale di Azure ](https://portal.azure.com/) selezionare l'account Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-123">In the [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="ebbfa-124">Scegliere come connettersi all'API Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-124">Select how to connect to the Media Services API.</span></span>

    ![Selezionare la pagina del metodo di connessione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="ebbfa-126">Autenticazione utente</span><span class="sxs-lookup"><span data-stu-id="ebbfa-126">User authentication</span></span>

<span data-ttu-id="ebbfa-127">Per connettersi all'API Servizi multimediali usando l'opzione di autenticazione utente, l'app client deve richiedere un token di Azure AD che contenga i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebbfa-127">To connect to the Media Services API by using the user authentication option, the client app needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="ebbfa-128">Endpoint del tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebbfa-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="ebbfa-129">URI di risorsa di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ebbfa-129">Media Services resource URI</span></span>
* <span data-ttu-id="ebbfa-130">ID client dell'applicazione Servizi multimediali (nativa)</span><span class="sxs-lookup"><span data-stu-id="ebbfa-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="ebbfa-131">URI di reindirizzamento dell'applicazione Servizi multimediali (nativa)</span><span class="sxs-lookup"><span data-stu-id="ebbfa-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="ebbfa-132">URI di risorsa per Servizi multimediali REST</span><span class="sxs-lookup"><span data-stu-id="ebbfa-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="ebbfa-133">È possibile ottenere i valori per questi parametri nella pagina **API Servizi multimediali con l'autenticazione utente**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-133">You can get the values for these parameters on the **Media Services API with user authentication** page.</span></span> 

![Connettersi con la pagina di autenticazione utente](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="ebbfa-135">Se ci si connette all'API Servizi multimediali con Media Services Microsoft .NET SDK, i valori richiesti sono disponibili nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-135">If you connect to the Media Services API by using the Media Services Microsoft .NET SDK, the required values are available to you as part of the SDK.</span></span> <span data-ttu-id="ebbfa-136">Per altre informazioni, vedere [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md) (Usare l'autenticazione di Azure AD per accedere all'API Servizi multimediali di Azure con .NET).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-136">For more information, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="ebbfa-137">Se non si usa l'SDK del client .NET di Servizi multimediali, è necessario creare manualmente una richiesta di token di Azure AD tramite i parametri descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-137">If you're not using the Media Services .NET client SDK, you must manually create an Azure AD token request by using the parameters discussed earlier.</span></span> <span data-ttu-id="ebbfa-138">Per altre informazioni, vedere [Come usare Azure AD Authentication Library per ottenere il token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-138">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="ebbfa-139">Autenticazione di un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="ebbfa-139">Service principal authentication</span></span>

<span data-ttu-id="ebbfa-140">Per connettersi all'API Servizi multimediali di Azure con l'opzione dell'entità servizio, l'app di livello intermedio (API o applicazione Web) deve richiedere un token di Azure AD che abbia i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebbfa-140">To connect to the Media Services API by using the service principal option, your middle-tier app (web API or web application) needs to request an Azure AD token that has the following parameters:</span></span>  

* <span data-ttu-id="ebbfa-141">Endpoint del tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebbfa-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="ebbfa-142">URI di risorsa di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="ebbfa-142">Media Services resource URI</span></span> 
* <span data-ttu-id="ebbfa-143">URI di risorsa per Servizi multimediali REST</span><span class="sxs-lookup"><span data-stu-id="ebbfa-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="ebbfa-144">Valori dell'applicazione Azure AD: **ID client** e **Segreto client**</span><span class="sxs-lookup"><span data-stu-id="ebbfa-144">Azure AD application values: the **client ID** and **client secret**</span></span>

<span data-ttu-id="ebbfa-145">È possibile ottenere i valori per questi parametri nella pagina **Connettersi all'API Servizi multimediali con l'entità servizio** .</span><span class="sxs-lookup"><span data-stu-id="ebbfa-145">You can get the values for these parameters on the **Connect to Media Services API with service principal** page.</span></span> <span data-ttu-id="ebbfa-146">In questa pagina è possibile creare una nuova applicazione Azure AD o selezionarne una esistente.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-146">Use this page to create a new Azure AD application or to select an existing one.</span></span> <span data-ttu-id="ebbfa-147">Dopo avere selezionato l'app Azure AD, è possibile ottenere l'ID client (ID applicazione) e generare i valori del segreto client (chiave).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-147">After you select the Azure AD app, you can get the client ID (Application ID) and generate the client secret (key) values.</span></span> 

![Connettersi alla pagina entità servizio](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="ebbfa-149">Quando si apre il pannello **Entità servizio**, viene selezionata la prima applicazione Azure AD che soddisfa i criteri seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebbfa-149">When the **Service Principal** blade opens, the first Azure AD application that meets the following criteria is selected:</span></span>

- <span data-ttu-id="ebbfa-150">Si tratta di un'applicazione Azure AD registrata.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="ebbfa-151">Dispone di autorizzazioni di controllo degli accessi in base al ruolo di proprietario o collaboratore per l'account.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-151">It has Contributor or Owner Role-Based Access Control permissions on the account.</span></span>

<span data-ttu-id="ebbfa-152">Dopo avere creato o selezionato un'app Azure AD, è possibile creare e copiare un segreto client (chiave) e l'ID client (ID applicazione).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and the client ID (Application ID).</span></span> <span data-ttu-id="ebbfa-153">L'ID client e il segreto client sono necessari per ottenere il token di accesso in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-153">The client secret and client ID are required to get the access token in this scenario.</span></span>

<span data-ttu-id="ebbfa-154">Se non si dispone delle autorizzazioni per creare app Azure AD nel dominio, i controlli del pannello dell'app Azure AD non vengono visualizzati e viene visualizzato un messaggio di avviso.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-154">If you don't have permissions to create Azure AD apps in your domain, the Azure AD app controls of the blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="ebbfa-155">Se ci si connette all'API Servizi multimediali con Media Services .NET SDK, vedere [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md) (Usare l'autenticazione di Azure AD per accedere all'API Servizi multimediali di Azure con .NET).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-155">If you connect to the Media Services API by using the Media Services .NET SDK, see [Use Azure AD authentication to access the Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="ebbfa-156">Se non si usa l'SDK del client .NET di Servizi multimediali, è necessario creare una richiesta di token di Azure AD manualmente specificando i parametri descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-156">If you are not using the Media Services .NET client SDK, you must manually create an Azure AD token request using the parameters discussed earlier.</span></span> <span data-ttu-id="ebbfa-157">Per altre informazioni, vedere [Come usare Azure AD Authentication Library per ottenere il token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-157">For more information, see [How to use the Azure AD Authentication Library to get the Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-the-client-id-and-client-secret"></a><span data-ttu-id="ebbfa-158">Ottenere l'ID client e il segreto client</span><span class="sxs-lookup"><span data-stu-id="ebbfa-158">Get the client ID and client secret</span></span>

<span data-ttu-id="ebbfa-159">Dopo avere selezionato un'app Azure AD esistente o avere selezionato l'opzione per crearne una nuova, vengono visualizzati i pulsanti seguenti:</span><span class="sxs-lookup"><span data-stu-id="ebbfa-159">After you select an existing Azure AD app or select the option to create a new one, the following buttons appear:</span></span>

![Pulsante Gestisci autorizzazioni e pulsante Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="ebbfa-161">Per aprire il pannello dell'applicazione Azure AD, fare clic su **Gestisci l'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-161">To open the Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="ebbfa-162">Nel pannello **Gestisci l'applicazione** è possibile ottenere l'ID client (ID applicazione) dell'app.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-162">On the **Manage application** blade, you can get the app's client ID (Application ID).</span></span> <span data-ttu-id="ebbfa-163">Per generare un segreto client (chiave), selezionare **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-163">To generate a client secret (key), select **Keys**.</span></span>

![Opzione Chiavi del pannello Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-the-application"></a><span data-ttu-id="ebbfa-165">Gestire le autorizzazioni e l'applicazione</span><span class="sxs-lookup"><span data-stu-id="ebbfa-165">Manage permissions and the application</span></span>

<span data-ttu-id="ebbfa-166">Dopo avere selezionato l'applicazione Azure AD, è possibile gestire l'applicazione e le autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-166">After you select the Azure AD application, you can manage the application and permissions.</span></span> <span data-ttu-id="ebbfa-167">Per configurare l'applicazione Azure AD in modo che acceda ad altre applicazioni, fare clic su **Gestisci autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-167">To set up your Azure AD application to access other applications, click **Manage permissions**.</span></span> <span data-ttu-id="ebbfa-168">Per le attività di gestione, ad esempio la modifica di chiavi e gli URL di risposta, o per modificare il manifesto dell'applicazione, fare clic su **Gestisci l'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-168">For management tasks, such as changing keys and reply URLs, or to edit the application’s manifest, click **Manage application**.</span></span>

### <a name="edit-the-apps-settings-or-manifest"></a><span data-ttu-id="ebbfa-169">Modificare le impostazioni o il manifesto dell'app</span><span class="sxs-lookup"><span data-stu-id="ebbfa-169">Edit the app's settings or manifest</span></span>

<span data-ttu-id="ebbfa-170">Per modificare le impostazioni o il manifesto dell'app, fare clic su **Gestisci l'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="ebbfa-170">To edit the app's settings or manifest, click **Manage application**.</span></span>

![Pagina Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="ebbfa-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ebbfa-172">Next steps</span></span>

<span data-ttu-id="ebbfa-173">Introduzione al [caricamento di file nell'account](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="ebbfa-173">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
