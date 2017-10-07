---
title: aaaGet avviato con l'autenticazione di Azure AD con hello portale di Azure | Documenti Microsoft
description: Informazioni su come toouse hello Azure tooaccess portale Azure Active Directory (Azure AD) autenticazione tooconsume hello API di servizi multimediali di Azure.
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
ms.openlocfilehash: 497ad1806b3fd1262802adefb6e12b65ee9f2d61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-ad-authentication-by-using-hello-azure-portal"></a><span data-ttu-id="5cf7a-103">Introduzione all'autenticazione di Azure AD tramite hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5cf7a-103">Get started with Azure AD authentication by using hello Azure portal</span></span>

<span data-ttu-id="5cf7a-104">Informazioni su come toouse hello Azure tooaccess portale Azure Active Directory (Azure AD) autenticazione tooaccess hello API di servizi multimediali di Azure.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-104">Learn how toouse hello Azure portal tooaccess Azure Active Directory (Azure AD) authentication tooaccess hello Azure Media Services API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5cf7a-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5cf7a-105">Prerequisites</span></span>

- <span data-ttu-id="5cf7a-106">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-106">An Azure account.</span></span> <span data-ttu-id="5cf7a-107">Se non si dispone di un account, iniziare con una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-107">If you don't have an account, start with an [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="5cf7a-108">Account di Servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-108">A Media Services account.</span></span> <span data-ttu-id="5cf7a-109">Per ulteriori informazioni, vedere [creare un account di servizi multimediali di Azure tramite il portale di Azure hello](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-109">For more information, see [Create an Azure Media Services account by using hello Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="5cf7a-110">Verificare hello [accesso alle API di servizi multimediali Azure con panoramica dell'autenticazione AD Azure](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-110">Make sure you review hello [Accessing Azure Media Services API with Azure AD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="5cf7a-111">Quando si usa l'autenticazione di Azure AD con Servizi multimediali di Azure, sono disponibili due opzioni di autenticazione:</span><span class="sxs-lookup"><span data-stu-id="5cf7a-111">When you use Azure AD authentication with Azure Media Services, you have two authentication options:</span></span>

- <span data-ttu-id="5cf7a-112">**Autenticazione utente**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-112">**User authentication**.</span></span> <span data-ttu-id="5cf7a-113">Eseguire l'autenticazione di una persona che utilizza hello app toointeract con risorse di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-113">Authenticate a person who is using hello app toointeract with Media Services resources.</span></span> <span data-ttu-id="5cf7a-114">applicazione interattiva Hello deve prima richiedere le credenziali utente hello.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-114">hello interactive application should first prompt hello user for credentials.</span></span> <span data-ttu-id="5cf7a-115">Un esempio è un'applicazione console di gestione usata dai processi di codifica toomonitor gli utenti autorizzati o streaming live.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-115">An example is a management console app used by authorized users toomonitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="5cf7a-116">**Autenticazione basata su entità servizio**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-116">**Service principal authentication**.</span></span> <span data-ttu-id="5cf7a-117">Consente di autenticare un servizio.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-117">Authenticate a service.</span></span> <span data-ttu-id="5cf7a-118">Le applicazioni che solitamente usano questo metodo di autenticazione sono app che eseguono servizi daemon, servizi di livello intermedio o processi pianificati, ad esempio App Web, app per le funzioni, app per la logica, API o microservizi.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs: web apps, function apps, logic apps, APIs, or a microservice.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5cf7a-119">Attualmente servizi multimediali supporta modello di autenticazione hello Azure Access Control service.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-119">Currently, Media Services supports hello Azure Access Control service authentication model.</span></span> <span data-ttu-id="5cf7a-120">L'autorizzazione di Controllo di accesso, tuttavia, verrà dichiarata deprecata il 1° giugno 2018.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-120">However, Access Control authorization will be deprecated on June 1, 2018.</span></span> <span data-ttu-id="5cf7a-121">Si consiglia di migrare il modello di autenticazione di Azure AD toohello appena possibile.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-121">We recommend that you migrate toohello Azure AD authentication model as soon as possible.</span></span>

## <a name="select-hello-authentication-method"></a><span data-ttu-id="5cf7a-122">Selezionare il metodo di autenticazione hello</span><span class="sxs-lookup"><span data-stu-id="5cf7a-122">Select hello authentication method</span></span>

1. <span data-ttu-id="5cf7a-123">In hello [portale di Azure](https://portal.azure.com/), selezionare l'account di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-123">In hello [Azure portal](https://portal.azure.com/), select your Media Services account.</span></span>
2. <span data-ttu-id="5cf7a-124">Selezionare come tooconnect toohello API di servizi multimediali.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-124">Select how tooconnect toohello Media Services API.</span></span>

    ![Selezionare la pagina del metodo di connessione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started01.png)

## <a name="user-authentication"></a><span data-ttu-id="5cf7a-126">Autenticazione utente</span><span class="sxs-lookup"><span data-stu-id="5cf7a-126">User authentication</span></span>

<span data-ttu-id="5cf7a-127">tooconnect toohello API di servizi multimediali usando hello opzione di autenticazione utente, app client hello deve toorequest un token di Azure AD che ha hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="5cf7a-127">tooconnect toohello Media Services API by using hello user authentication option, hello client app needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="5cf7a-128">Endpoint del tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cf7a-128">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="5cf7a-129">URI di risorsa di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5cf7a-129">Media Services resource URI</span></span>
* <span data-ttu-id="5cf7a-130">ID client dell'applicazione Servizi multimediali (nativa)</span><span class="sxs-lookup"><span data-stu-id="5cf7a-130">Media Services (native) application client ID</span></span> 
* <span data-ttu-id="5cf7a-131">URI di reindirizzamento dell'applicazione Servizi multimediali (nativa)</span><span class="sxs-lookup"><span data-stu-id="5cf7a-131">Media Services (native) application redirect URI</span></span> 
* <span data-ttu-id="5cf7a-132">URI di risorsa per Servizi multimediali REST</span><span class="sxs-lookup"><span data-stu-id="5cf7a-132">Resource URI for REST Media Services</span></span>

<span data-ttu-id="5cf7a-133">È possibile ottenere i valori hello per questi parametri in hello **API dei servizi multimediali con l'autenticazione utente** pagina.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-133">You can get hello values for these parameters on hello **Media Services API with user authentication** page.</span></span> 

![Connettersi con la pagina di autenticazione utente](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started02.png)

<span data-ttu-id="5cf7a-135">Se ci si connette toohello API di servizi multimediali con Media Services Microsoft .NET SDK hello, hello necessari valori tooyou disponibile come parte di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-135">If you connect toohello Media Services API by using hello Media Services Microsoft .NET SDK, hello required values are available tooyou as part of hello SDK.</span></span> <span data-ttu-id="5cf7a-136">Per ulteriori informazioni, vedere [usano Azure AD authentication tooaccess hello API di servizi multimediali di Azure con .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-136">For more information, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="5cf7a-137">Se non si utilizza client .NET di servizi multimediali hello SDK, è necessario creare manualmente una richiesta di token di Azure AD utilizzando i parametri di hello descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-137">If you're not using hello Media Services .NET client SDK, you must manually create an Azure AD token request by using hello parameters discussed earlier.</span></span> <span data-ttu-id="5cf7a-138">Per ulteriori informazioni, vedere [come toouse hello Azure AD Authentication Library tooget hello token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-138">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

## <a name="service-principal-authentication"></a><span data-ttu-id="5cf7a-139">Autenticazione di un'entità servizio</span><span class="sxs-lookup"><span data-stu-id="5cf7a-139">Service principal authentication</span></span>

<span data-ttu-id="5cf7a-140">tooconnect toohello API di servizi multimediali usando hello opzione dell'entità servizio, l'applicazione di livello intermedio (API web o applicazione web) deve toorequest un token di Azure AD che ha hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="5cf7a-140">tooconnect toohello Media Services API by using hello service principal option, your middle-tier app (web API or web application) needs toorequest an Azure AD token that has hello following parameters:</span></span>  

* <span data-ttu-id="5cf7a-141">Endpoint del tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="5cf7a-141">Azure AD tenant endpoint</span></span>
* <span data-ttu-id="5cf7a-142">URI di risorsa di Servizi multimediali</span><span class="sxs-lookup"><span data-stu-id="5cf7a-142">Media Services resource URI</span></span> 
* <span data-ttu-id="5cf7a-143">URI di risorsa per Servizi multimediali REST</span><span class="sxs-lookup"><span data-stu-id="5cf7a-143">Resource URI for REST Media Services</span></span>
* <span data-ttu-id="5cf7a-144">I valori dell'applicazione Azure AD: hello **ID client** e **segreto client**</span><span class="sxs-lookup"><span data-stu-id="5cf7a-144">Azure AD application values: hello **client ID** and **client secret**</span></span>

<span data-ttu-id="5cf7a-145">È possibile ottenere i valori hello per questi parametri in hello **connettersi tooMedia API dei servizi con un'entità servizio** pagina.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-145">You can get hello values for these parameters on hello **Connect tooMedia Services API with service principal** page.</span></span> <span data-ttu-id="5cf7a-146">Utilizzare questo toocreate pagina Azure un nuova applicazione AD o tooselect uno esistente.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-146">Use this page toocreate a new Azure AD application or tooselect an existing one.</span></span> <span data-ttu-id="5cf7a-147">Dopo aver selezionato hello Azure AD app, è possibile ottenere l'ID client hello (ID applicazione) e generare i valori di hello client secret (chiave).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-147">After you select hello Azure AD app, you can get hello client ID (Application ID) and generate hello client secret (key) values.</span></span> 

![Connettersi alla pagina entità servizio](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started04.png)

<span data-ttu-id="5cf7a-149">Quando hello **dell'entità servizio** pannello viene aperto, è selezionata l'applicazione Azure AD prima hello che soddisfi i seguenti criteri hello:</span><span class="sxs-lookup"><span data-stu-id="5cf7a-149">When hello **Service Principal** blade opens, hello first Azure AD application that meets hello following criteria is selected:</span></span>

- <span data-ttu-id="5cf7a-150">Si tratta di un'applicazione Azure AD registrata.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-150">It is a registered Azure AD application.</span></span>
- <span data-ttu-id="5cf7a-151">Disponga di autorizzazioni di collaboratore o il controllo di accesso Owner Role-Based account hello.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-151">It has Contributor or Owner Role-Based Access Control permissions on hello account.</span></span>

<span data-ttu-id="5cf7a-152">Dopo aver creato o selezionare un'app di Azure AD, è possibile creare un segreto client (chiave) e copiare hello ID client (ID applicazione).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-152">After you create or select an Azure AD app, you can create and copy a client secret (key) and hello client ID (Application ID).</span></span> <span data-ttu-id="5cf7a-153">ID client e il segreto client Hello sono token di accesso obbligatorio tooget hello in questo scenario.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-153">hello client secret and client ID are required tooget hello access token in this scenario.</span></span>

<span data-ttu-id="5cf7a-154">Se non si dispone delle autorizzazioni app di Azure AD toocreate nel dominio, non vengono visualizzati i controlli app di Azure AD hello del pannello hello e viene visualizzato un messaggio di avviso.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-154">If you don't have permissions toocreate Azure AD apps in your domain, hello Azure AD app controls of hello blade are not shown, and a warning message is displayed.</span></span>

<span data-ttu-id="5cf7a-155">Se ci si connette toohello API di servizi multimediali con Media Services .NET SDK hello, vedere [usano Azure AD authentication tooaccess hello API di servizi multimediali di Azure con .NET](media-services-dotnet-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-155">If you connect toohello Media Services API by using hello Media Services .NET SDK, see [Use Azure AD authentication tooaccess hello Azure Media Services API with .NET](media-services-dotnet-get-started-with-aad.md).</span></span>

<span data-ttu-id="5cf7a-156">Se non si utilizza client .NET di servizi multimediali hello SDK, è necessario creare manualmente una richiesta di token di Azure AD utilizzando parametri hello descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-156">If you are not using hello Media Services .NET client SDK, you must manually create an Azure AD token request using hello parameters discussed earlier.</span></span> <span data-ttu-id="5cf7a-157">Per ulteriori informazioni, vedere [come toouse hello Azure AD Authentication Library tooget hello token di Azure AD](../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-157">For more information, see [How toouse hello Azure AD Authentication Library tooget hello Azure AD token](../active-directory/develop/active-directory-authentication-libraries.md).</span></span>

### <a name="get-hello-client-id-and-client-secret"></a><span data-ttu-id="5cf7a-158">Ottenere il client di hello ID e client secret</span><span class="sxs-lookup"><span data-stu-id="5cf7a-158">Get hello client ID and client secret</span></span>

<span data-ttu-id="5cf7a-159">Dopo aver selezionato un'app di Azure AD esistente o hello selezionare opzione toocreate uno nuovo, verrà visualizzato hello seguenti pulsanti:</span><span class="sxs-lookup"><span data-stu-id="5cf7a-159">After you select an existing Azure AD app or select hello option toocreate a new one, hello following buttons appear:</span></span>

![Pulsante Gestisci autorizzazioni e pulsante Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-manage.png)

<span data-ttu-id="5cf7a-161">hello tooopen pannello applicazione Azure AD, fare clic su **Gestisci applicazione**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-161">tooopen hello Azure AD application blade, click **Manage application**.</span></span> <span data-ttu-id="5cf7a-162">In hello **Gestisci applicazione** pannello, è possibile ottenere l'ID client dell'applicazione hello (ID applicazione).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-162">On hello **Manage application** blade, you can get hello app's client ID (Application ID).</span></span> <span data-ttu-id="5cf7a-163">un segreto client (chiave), seleziona toogenerate **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-163">toogenerate a client secret (key), select **Keys**.</span></span>

![Opzione Chiavi del pannello Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started06.png) 

### <a name="manage-permissions-and-hello-application"></a><span data-ttu-id="5cf7a-165">Gestire le autorizzazioni e l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="5cf7a-165">Manage permissions and hello application</span></span>

<span data-ttu-id="5cf7a-166">Dopo aver selezionato un'applicazione hello Azure AD, è possibile gestire le autorizzazioni e l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-166">After you select hello Azure AD application, you can manage hello application and permissions.</span></span> <span data-ttu-id="5cf7a-167">tooset backup il tooaccess applicazione Azure AD altre applicazioni, fare clic su **gestire le autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-167">tooset up your Azure AD application tooaccess other applications, click **Manage permissions**.</span></span> <span data-ttu-id="5cf7a-168">Per le attività di gestione, ad esempio la modifica di chiavi e gli URL di risposta o il manifesto dell'applicazione hello tooedit, fare clic su **Gestisci applicazione**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-168">For management tasks, such as changing keys and reply URLs, or tooedit hello application’s manifest, click **Manage application**.</span></span>

### <a name="edit-hello-apps-settings-or-manifest"></a><span data-ttu-id="5cf7a-169">Modificare le impostazioni dell'applicazione hello o manifesto</span><span class="sxs-lookup"><span data-stu-id="5cf7a-169">Edit hello app's settings or manifest</span></span>

<span data-ttu-id="5cf7a-170">le impostazioni dell'applicazione hello tooedit o manifesto, fare clic su **Gestisci applicazione**.</span><span class="sxs-lookup"><span data-stu-id="5cf7a-170">tooedit hello app's settings or manifest, click **Manage application**.</span></span>

![Pagina Gestisci l'applicazione](./media/media-services-portal-get-started-with-aad/media-services-portal-get-started05.png)

## <a name="next-steps"></a><span data-ttu-id="5cf7a-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5cf7a-172">Next steps</span></span>

<span data-ttu-id="5cf7a-173">Introduzione a [caricamento file account tooyour](media-services-portal-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="5cf7a-173">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
