---
title: chiamare aaaDeploy e l'autenticazione web API e le API REST per le app di logica di Azure | Documenti Microsoft
description: Distribuire, autenticare e chiamare API Web e API REST nei flussi di lavoro per le integrazioni di sistema con le app per la logica di Azure
keywords: API Web, API REST, connettori, flussi di lavoro, integrazioni di sistema, autenticazione
services: logic-apps
author: stepsic-microsoft-com
manager: anneta
editor: 
documentationcenter: 
ms.assetid: f113005d-0ba6-496b-8230-c1eadbd6dbb9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: LADocs; stepsic
ms.openlocfilehash: ca1e4f28196b21f43b7c9ab94029684121e36f63
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="018ce-104">Distribuire, chiamare e autenticare le API personalizzate come connettori per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="018ce-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="018ce-105">Dopo aver [creare API personalizzate](./logic-apps-create-api-app.md) toouse azioni o i trigger nella logica che forniscono i flussi di lavoro di applicazioni, è necessario distribuire le API prima di poter chiamare.</span><span class="sxs-lookup"><span data-stu-id="018ce-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers toouse in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="018ce-106">Sebbene sia possibile chiamare qualsiasi API da un'app, la logica per un'esperienza ottimale di hello, aggiungere [metadati Swagger](http://swagger.io/specification/) che descrive le operazioni dell'API e parametri.</span><span class="sxs-lookup"><span data-stu-id="018ce-106">And although you can call any API from a logic app, for hello best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="018ce-107">Il file Swagger consente all'API di funzionare meglio e di integrarsi più facilmente con le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="018ce-108">È possibile distribuire le API come [le app web](../app-service-web/app-service-web-overview.md), ma è consigliabile distribuire le API come [App per le API](../app-service-api/app-service-api-apps-why-best-platform.md), che può semplificare il lavoro quando si compila, host e utilizzare le API nel cloud hello e in locale.</span><span class="sxs-lookup"><span data-stu-id="018ce-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in hello cloud and on premises.</span></span> <span data-ttu-id="018ce-109">Non si dispone toochange qualsiasi codice nelle API--è sufficiente distribuire l'app per le API tooan di codice.</span><span class="sxs-lookup"><span data-stu-id="018ce-109">You don't have toochange any code in your APIs -- just deploy your code tooan API app.</span></span> <span data-ttu-id="018ce-110">È possibile ospitare le API in [Azure App Service](../app-service/app-service-value-prop-what-is.md), un platform-as-a-service (PaaS) offerta che fornisce uno dei modi di hello migliori, più semplici e più scalabili per l'API di hosting.</span><span class="sxs-lookup"><span data-stu-id="018ce-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of hello best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="018ce-111">tooauthenticate chiamate da logica App tooyour API, è possibile impostare Azure Active Directory in hello portale di Azure in modo non si dispone di codice tooupdate.</span><span class="sxs-lookup"><span data-stu-id="018ce-111">tooauthenticate calls from logic apps tooyour APIs, you can set up Azure Active Directory in hello Azure portal so you don't have tooupdate your code.</span></span> <span data-ttu-id="018ce-112">Oppure, è possibile richiedere e applicare l'autenticazione attraverso il codice dell'API.</span><span class="sxs-lookup"><span data-stu-id="018ce-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="018ce-113">Distribuire l'API come app Web o app per le API</span><span class="sxs-lookup"><span data-stu-id="018ce-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="018ce-114">Prima di poter chiamare l'API personalizzata da un'app di logica, è possibile distribuire l'API come un'app web o l'API app tooAzure servizio App.</span><span class="sxs-lookup"><span data-stu-id="018ce-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app tooAzure App Service.</span></span> <span data-ttu-id="018ce-115">Inoltre, toomake documento Swagger leggibile da hello logica progettazione applicazione, impostare le proprietà di definizione API hello e attivare [risorse multiorigine (CORS) di condivisione](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) per le app web o API.</span><span class="sxs-lookup"><span data-stu-id="018ce-115">Also, toomake your Swagger document readable by hello Logic App Designer, set hello API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="018ce-116">Nel portale di Azure hello, selezionare le app web o API.</span><span class="sxs-lookup"><span data-stu-id="018ce-116">In hello Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="018ce-117">Nel pannello hello visualizzata nell'area **API**, scegliere **di definizione dell'API**.</span><span class="sxs-lookup"><span data-stu-id="018ce-117">In hello blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="018ce-118">Set hello **percorso definizione API** toohello URL per il file swagger.</span><span class="sxs-lookup"><span data-stu-id="018ce-118">Set hello **API definition location** toohello URL for your swagger.json file.</span></span>

   <span data-ttu-id="018ce-119">URL hello in genere, viene visualizzato nel formato seguente:`https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="018ce-119">Usually, hello URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![File di collegamento tooSwagger dell'API personalizzata](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="018ce-121">Scegliere **CORS** nell'area **API**.</span><span class="sxs-lookup"><span data-stu-id="018ce-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="018ce-122">Impostare il criterio CORS hello per **le origini consentite** troppo**'*'** (Consenti tutti).</span><span class="sxs-lookup"><span data-stu-id="018ce-122">Set hello CORS policy for **Allowed origins** too**'*'** (allow all).</span></span>

   <span data-ttu-id="018ce-123">Questa impostazione consente le richieste da Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-123">This setting permits requests from Logic App Designer.</span></span>

   ![Consentire richieste dall'API di progettazione applicazione logica tooyour personalizzato](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="018ce-125">Per altre informazioni, vedere questi articoli:</span><span class="sxs-lookup"><span data-stu-id="018ce-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="018ce-126">Aggiungere metadati Swagger per le API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="018ce-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="018ce-127">Distribuzione di ASP.NET web API tooAzure servizio App</span><span class="sxs-lookup"><span data-stu-id="018ce-127">Deploy ASP.NET web APIs tooAzure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="018ce-128">Chiamare l'API personalizzata dai flussi di lavoro delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="018ce-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="018ce-129">Dopo aver impostato le proprietà di definizione API hello e CORS, trigger e le azioni dell'API personalizzata dovrebbero diventare disponibile per tooinclude nel flusso di lavoro logica app.</span><span class="sxs-lookup"><span data-stu-id="018ce-129">After you set up hello API definition properties and CORS, your custom API's triggers and actions should become available for you tooinclude in your logic app workflow.</span></span> 

*  <span data-ttu-id="018ce-130">tooview hello siti Web con l'URL di Swagger, è possibile esplorare i siti Web di sottoscrizione nella logica di progettazione di App hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-130">tooview hello websites that have Swagger URLs, you can browse your subscription websites in hello Logic Apps Designer.</span></span>

*  <span data-ttu-id="018ce-131">azioni disponibili tooview e degli input che punta a un documento di Swagger, utilizzare hello [HTTP + Swagger azione](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="018ce-131">tooview available actions and inputs by pointing at a Swagger document, use hello [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="018ce-132">toocall qualsiasi API, incluse le API che non hanno o esporre un documento di Swagger, è sempre possibile creare una richiesta con hello [azione HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="018ce-132">toocall any API, including APIs that don't have or expose a Swagger document, you can always create a request with hello [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-tooyour-custom-api"></a><span data-ttu-id="018ce-133">Autenticare le chiamate API personalizzata di tooyour</span><span class="sxs-lookup"><span data-stu-id="018ce-133">Authenticate calls tooyour custom API</span></span>

<span data-ttu-id="018ce-134">È possibile proteggere le chiamate API personalizzata di tooyour nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="018ce-134">You can secure calls tooyour custom API in these ways:</span></span>

* <span data-ttu-id="018ce-135">[Nessuna modifica di codice](#no-code): proteggere le API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) tramite hello portale di Azure, pertanto non disporre di tooupdate codice oppure ridistribuire l'API.</span><span class="sxs-lookup"><span data-stu-id="018ce-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through hello Azure portal, so you don't have tooupdate your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="018ce-136">Per impostazione predefinita, l'autenticazione di Azure AD hello che attivare in hello portale di Azure non fornisce un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="018ce-136">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="018ce-137">Ad esempio, questa autenticazione Blocca toojust l'API, un tenant specifico, non tooa utente o specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="018ce-137">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

* <span data-ttu-id="018ce-138">[Aggiornare il codice dell'API](#update-code): proteggere l'API applicando [l'autenticazione del certificato](#certificate), [l'autenticazione di base](#basic) o [autenticazione di Azure AD](#azure-ad-code) attraverso il codice.</span><span class="sxs-lookup"><span data-stu-id="018ce-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-tooyour-api-without-changing-code"></a><span data-ttu-id="018ce-139">Autenticare le chiamate API di tooyour senza modificare il codice</span><span class="sxs-lookup"><span data-stu-id="018ce-139">Authenticate calls tooyour API without changing code</span></span>

<span data-ttu-id="018ce-140">Ecco i passaggi generali hello per questo metodo:</span><span class="sxs-lookup"><span data-stu-id="018ce-140">Here's hello general steps for this method:</span></span>

1. <span data-ttu-id="018ce-141">Creare due [identità di applicazione di Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md), una per l'app per la logica e una per l'app Web (o l'app per le API).</span><span class="sxs-lookup"><span data-stu-id="018ce-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="018ce-142">tooauthenticate tooyour di chiamate API, utilizzare le credenziali di hello (ID client e segreto) per hello [dell'entità servizio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associato hello identità dell'applicazione Azure AD per l'app logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-142">tooauthenticate calls tooyour API, use hello credentials (client ID and secret) for hello [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with hello Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="018ce-143">Includere un'applicazione hello ID nella definizione dell'app logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-143">Include hello application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="018ce-144">Parte 1: Creare un'identità di applicazione di Azure AD per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="018ce-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="018ce-145">Logica app Usa questa tooauthenticate identità di applicazione di Azure AD con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="018ce-145">Your logic app uses this Azure AD application identity tooauthenticate against Azure AD.</span></span> <span data-ttu-id="018ce-146">È solo una volta per la directory tooset backup questa identità.</span><span class="sxs-lookup"><span data-stu-id="018ce-146">You only have tooset up this identity one time for your directory.</span></span> <span data-ttu-id="018ce-147">Ad esempio, è possibile scegliere toouse hello identità stesso per tutte le app di logica, anche se è possibile creare le identità univoche per ogni app logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-147">For example, you can choose toouse hello same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="018ce-148">È possibile impostare queste identità nel portale di Azure hello [portale di Azure classico](#app-identity-logic-classic), oppure utilizzare [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="018ce-148">You can set up these identities in hello Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="018ce-149">**Creare l'identità dell'applicazione hello per le app per la logica in hello portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="018ce-149">**Create hello application identity for your logic app in hello Azure portal**</span></span>

1. <span data-ttu-id="018ce-150">In hello [portale di Azure](https://portal.azure.com "https://portal.azure.com"), scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="018ce-150">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="018ce-151">Confermare che si è in hello stessa directory le app web o API.</span><span class="sxs-lookup"><span data-stu-id="018ce-151">Confirm that you're in hello same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="018ce-152">Directory tooswitch, scegliere il profilo e selezionare un'altra directory.</span><span class="sxs-lookup"><span data-stu-id="018ce-152">tooswitch directories, click your profile and select another directory.</span></span> <span data-ttu-id="018ce-153">In alternativa, scegliere **Panoramica** > **Cambia directory**.</span><span class="sxs-lookup"><span data-stu-id="018ce-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="018ce-154">Menu directory hello in **Gestisci**, scegliere **registrazioni di App** > **nuova registrazione applicazione**.</span><span class="sxs-lookup"><span data-stu-id="018ce-154">On hello directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="018ce-155">Per impostazione predefinita, elenco di registrazioni app hello Mostra tutte le registrazioni di app nella directory.</span><span class="sxs-lookup"><span data-stu-id="018ce-155">By default, hello app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="018ce-156">Selezionare solo le registrazioni di app, casella di ricerca toohello Avanti tooview **le mie app**.</span><span class="sxs-lookup"><span data-stu-id="018ce-156">tooview only your app registrations, next toohello search box, select **My apps**.</span></span> 

   ![Creare una nuova registrazione di app](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="018ce-158">Assegnare un nome di identità applicazione, lasciare **tipo di applicazione** impostato troppo**app Web / API**, fornire un univoco stringa formattata come un dominio per **Sign-on URL**e scegliere  **Creare**.</span><span class="sxs-lookup"><span data-stu-id="018ce-158">Give your application identity a name, leave **Application type** set too**Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Specificare nome e URL di accesso per l'identità di applicazione](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="018ce-160">identità dell'applicazione Hello creato per l'app logica ora viene visualizzato nell'elenco di registrazioni app hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-160">hello application identity that you created for your logic app now appears in hello app registrations list.</span></span>

   ![Identità di applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="018ce-162">Nell'elenco di registrazioni hello app, selezionare la nuova identità di applicazione.</span><span class="sxs-lookup"><span data-stu-id="018ce-162">In hello app registrations list, select your new application identity.</span></span> <span data-ttu-id="018ce-163">Copiare e salvare hello **ID applicazione** toouse come hello "ID client" per l'app logica nella parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-163">Copy and save hello **Application ID** toouse as hello "client ID" for your logic app in Part 3.</span></span>

   ![Copiare e salvare l'ID applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="018ce-165">Se le impostazioni dell'identità di applicazione non sono visibili, scegliere **Impostazioni** o **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="018ce-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="018ce-166">Scegliere **Chiavi** in **Accesso all'API**.</span><span class="sxs-lookup"><span data-stu-id="018ce-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="018ce-167">In **Descrizione** specificare un nome per la chiave.</span><span class="sxs-lookup"><span data-stu-id="018ce-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="018ce-168">Selezionare una **scadenza** per la durata della chiave.</span><span class="sxs-lookup"><span data-stu-id="018ce-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="018ce-169">chiave Hello che si sta creando funge da dell'identità di applicazione hello "segreto" o la password per l'app logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-169">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

   ![Creare una chiave per l'identità dell'app per la logica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="018ce-171">Sulla barra degli strumenti hello, scegliere **salvare**.</span><span class="sxs-lookup"><span data-stu-id="018ce-171">On hello toolbar, choose **Save**.</span></span> <span data-ttu-id="018ce-172">La chiave viene visualizzata in **Valore**.</span><span class="sxs-lookup"><span data-stu-id="018ce-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="018ce-173">**Verificare che toocopy e salvare la chiave** per un utilizzo successivo perché è nascosta chiave hello se si lascia pannello chiave hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-173">**Make sure toocopy and save your key** for later use because hello key is hidden when you leave hello key blade.</span></span>

   <span data-ttu-id="018ce-174">Quando si configura l'app logica nella parte 3, specificare questa chiave come hello "segreto" o la password.</span><span class="sxs-lookup"><span data-stu-id="018ce-174">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

   ![Copiare e salvare la chiave per usarla in un momento successivo](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="018ce-176">**Creare l'identità dell'applicazione hello per le app per la logica nel portale di Azure classico hello**</span><span class="sxs-lookup"><span data-stu-id="018ce-176">**Create hello application identity for your logic app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="018ce-177">Nel portale di Azure classico hello, scegliere [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="018ce-177">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="018ce-178">Selezionare hello stessa directory in cui si utilizza per l'app web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="018ce-178">Select hello same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="018ce-179">In hello **applicazioni** scegliere **Aggiungi** nella parte inferiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-179">On hello **Applications** tab, choose **Add** at hello bottom of hello page.</span></span>

4. <span data-ttu-id="018ce-180">Assegnare un nome all'identità di applicazione e scegliere **Avanti** (freccia destra).</span><span class="sxs-lookup"><span data-stu-id="018ce-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="018ce-181">In **Proprietà dell'app** specificare una stringa univoca formattata come dominio per **URL accesso** e **URI ID app** e scegliere **Completa** (segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="018ce-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="018ce-182">In hello **configura** scheda, copiare e salvare hello **ID Client** per il toouse app logica nella parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-182">On hello **Configure** tab, copy and save hello **Client ID** for your logic app toouse in Part 3.</span></span>

7. <span data-ttu-id="018ce-183">In **chiavi**aprire hello **Seleziona durata** elenco.</span><span class="sxs-lookup"><span data-stu-id="018ce-183">Under **Keys**, open hello **Select duration** list.</span></span> <span data-ttu-id="018ce-184">Selezionare una durata per la chiave.</span><span class="sxs-lookup"><span data-stu-id="018ce-184">Select a duration for your key.</span></span>

   <span data-ttu-id="018ce-185">chiave Hello che si sta creando funge da dell'identità di applicazione hello "segreto" o la password per l'app logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-185">hello key that you're creating acts as hello application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="018ce-186">Nella parte inferiore di hello della pagina hello, scegliere **salvare**.</span><span class="sxs-lookup"><span data-stu-id="018ce-186">At hello bottom of hello page, choose **Save**.</span></span> <span data-ttu-id="018ce-187">Potrebbe essere toowait pochi secondi.</span><span class="sxs-lookup"><span data-stu-id="018ce-187">You might have toowait a few seconds.</span></span>

9. <span data-ttu-id="018ce-188">In **chiavi**, assicurarsi che toocopy e salvare chiave hello che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="018ce-188">Under **Keys**, make sure toocopy and save hello key that now appears.</span></span> 

   <span data-ttu-id="018ce-189">Quando si configura l'app logica nella parte 3, specificare questa chiave come hello "segreto" o la password.</span><span class="sxs-lookup"><span data-stu-id="018ce-189">When you configure your logic app in Part 3, you specify this key as hello "secret" or password.</span></span>

<span data-ttu-id="018ce-190">Per ulteriori informazioni, vedere come troppo [configurare l'accesso di Azure Active Directory di servizio App applicazione toouse](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="018ce-190">For more information, learn how too [configure your App Service application toouse Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="018ce-191">**Creare l'identità dell'applicazione hello per le app per la logica in PowerShell**</span><span class="sxs-lookup"><span data-stu-id="018ce-191">**Create hello application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="018ce-192">È possibile eseguire questa attività usando Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018ce-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="018ce-193">In PowerShell eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="018ce-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="018ce-194">Verificare che hello toocopy **ID Tenant** hello (GUID per il tenant di Azure AD), **ID applicazione**e la password di hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="018ce-194">Make sure toocopy hello **Tenant ID** (GUID for your Azure AD tenant), hello **Application ID**, and hello password that you used.</span></span>

<span data-ttu-id="018ce-195">Per ulteriori informazioni, vedere come troppo [creare un'entità servizio con PowerShell tooaccess risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="018ce-195">For more information, learn how too [create a service principal with PowerShell tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="018ce-196">Parte 2: Creare un'identità di applicazione di Azure AD per l'app Web o l'app per le API</span><span class="sxs-lookup"><span data-stu-id="018ce-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="018ce-197">Se è già stato distribuito l'app web o app per le API, è possibile attivare l'autenticazione e creare l'identità dell'applicazione hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="018ce-197">If your web app or API app is already deployed, you can turn on authentication and create hello application identity in hello Azure portal.</span></span> <span data-ttu-id="018ce-198">In alternativa, è possibile [attivare l'autenticazione quando si effettua la distribuzione con un modello di Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="018ce-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="018ce-199">**Creare l'identità dell'applicazione hello e attivare l'autenticazione nel portale di Azure per le app distribuite hello**</span><span class="sxs-lookup"><span data-stu-id="018ce-199">**Create hello application identity and turn on authentication in hello Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="018ce-200">In hello [portale di Azure](https://portal.azure.com "https://portal.azure.com"), individuare e selezionare le app web o API.</span><span class="sxs-lookup"><span data-stu-id="018ce-200">In hello [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="018ce-201">In **Impostazioni** scegliere **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="018ce-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="018ce-202">In **Autenticazione servizio app** **attivare** l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="018ce-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="018ce-203">In **Provider di autenticazione** scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="018ce-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Attivare l'autenticazione](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="018ce-205">Creare un'identità di applicazione per l'app Web o l'app per le API come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="018ce-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="018ce-206">In hello **impostazioni di Azure Active Directory** pannello, impostare **modalità di gestione** troppo**Express**.</span><span class="sxs-lookup"><span data-stu-id="018ce-206">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Express**.</span></span> <span data-ttu-id="018ce-207">Scegliere **Crea nuova App AD**.</span><span class="sxs-lookup"><span data-stu-id="018ce-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="018ce-208">Assegnare un nome all'identità di applicazione e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="018ce-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Creare un'identità di applicazione per l'app Web o l'app per le API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="018ce-210">In hello **autenticazione / pannello autorizzazione**, scegliere **salvare**.</span><span class="sxs-lookup"><span data-stu-id="018ce-210">On hello **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="018ce-211">A questo punto è necessario trovare l'ID client hello e ID tenant per l'identità di applicazione hello associata con l'app web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="018ce-211">Now you must find hello client ID and tenant ID for hello application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="018ce-212">Questi ID verranno usati nella Parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="018ce-213">Pertanto, continuare con la procedura per hello portale di Azure o [portale di Azure classico](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="018ce-213">So continue with these steps for hello Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="018ce-214">**Trovare l'ID client dell'identità di applicazione e l'ID tenant per l'app web o app per le API nel portale di Azure hello**</span><span class="sxs-lookup"><span data-stu-id="018ce-214">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure portal**</span></span>

1. <span data-ttu-id="018ce-215">In **Provider di autenticazione** scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="018ce-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Scegliere "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="018ce-217">In hello **impostazioni di Azure Active Directory** pannello, impostare **modalità di gestione** troppo**avanzate**.</span><span class="sxs-lookup"><span data-stu-id="018ce-217">On hello **Azure Active Directory Settings** blade, set **Management mode** too**Advanced**.</span></span>

3. <span data-ttu-id="018ce-218">Hello copia **ID Client**e salvare tale GUID per l'utilizzo nella parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-218">Copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="018ce-219">Se **ID Client** e **Url autorità di certificazione** non vengono visualizzati, provare ad aggiornare hello portale di Azure e ripetere il passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="018ce-219">If **Client ID** and **Issuer Url** don't appear, try refreshing hello Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="018ce-220">In **Url autorità di certificazione**, copiare e salvare solo hello GUID per la parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-220">Under **Issuer Url**, copy and save just hello GUID for Part 3.</span></span> <span data-ttu-id="018ce-221">È anche possibile usare questo GUID nel modello di distribuzione dell'app Web o app per le API, se necessario.</span><span class="sxs-lookup"><span data-stu-id="018ce-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="018ce-222">Questo GUID è il GUID del tenant specifico ("ID tenant") e deve apparire in questo URL: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="018ce-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="018ce-223">Senza salvare le modifiche, chiudere hello **impostazioni di Azure Active Directory** blade.</span><span class="sxs-lookup"><span data-stu-id="018ce-223">Without saving your changes, close hello **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="018ce-224">**Trovare l'ID client dell'identità di applicazione e l'ID tenant per l'app web o app per le API nel portale di Azure classico hello**</span><span class="sxs-lookup"><span data-stu-id="018ce-224">**Find application identity's client ID and tenant ID for your web app or API app in hello Azure classic portal**</span></span>

1. <span data-ttu-id="018ce-225">Nel portale di Azure classico hello, scegliere [ **Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="018ce-225">In hello Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="018ce-226">Selezionare la directory di hello utilizzato per le app web o API.</span><span class="sxs-lookup"><span data-stu-id="018ce-226">Select hello directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="018ce-227">In hello **ricerca** , trovare e selezionare l'identità dell'applicazione hello per le app web o API.</span><span class="sxs-lookup"><span data-stu-id="018ce-227">In hello **Search** box, find and select hello application identity for your web app or API app.</span></span>

4. <span data-ttu-id="018ce-228">In hello **configura** scheda, hello copia **ID Client**e salvare tale GUID per l'utilizzo nella parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-228">On hello **Configure** tab, copy hello **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="018ce-229">Dopo avere ottenuto l'ID client hello, nella parte inferiore di hello di hello **configura** scegliere **visualizzare endpoint**.</span><span class="sxs-lookup"><span data-stu-id="018ce-229">After you get hello client ID, at hello bottom of hello **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="018ce-230">Copia URL hello per **documento metadati federazione**e passare toothat URL.</span><span class="sxs-lookup"><span data-stu-id="018ce-230">Copy hello URL for **Federation Metadata Document**, and browse toothat URL.</span></span>

7. <span data-ttu-id="018ce-231">Nel documento di metadati hello che si apre, trovare radice hello **EntityDescriptor ID** elemento, che ha un **entityID** attributo in questo formato:`https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="018ce-231">In hello metadata document that opens, find hello root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="018ce-232">Hello GUID in questo attributo è il GUID del tenant specifica (ID tenant).</span><span class="sxs-lookup"><span data-stu-id="018ce-232">hello GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="018ce-233">Copiare l'ID tenant hello e salvare tale ID per l'utilizzo nella parte 3 e toouse in app web o il modello di distribuzione dell'app dell'API, se necessario.</span><span class="sxs-lookup"><span data-stu-id="018ce-233">Copy hello tenant ID and save that ID for use in Part 3, and also toouse in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="018ce-234">Per altre informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="018ce-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="018ce-235">Autenticazione utente per le app per le API nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="018ce-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="018ce-236">Autenticazione e autorizzazione nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="018ce-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="018ce-237">**Attivare l'autenticazione quando si esegue la distribuzione con un modello di Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="018ce-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="018ce-238">È ancora necessario creare identità di un'applicazione Azure AD per l'app web o app per le API che differisce dall'identità dell'applicazione hello per le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="018ce-238">You must still create an Azure AD application identity for your web app or API app that differs from hello app identity for your logic app.</span></span> <span data-ttu-id="018ce-239">identità dell'applicazione hello toocreate, seguire hello precedente procedura nella parte 2 di hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="018ce-239">toocreate hello application identity, follow hello previous steps in Part 2 for hello Azure portal.</span></span> <span data-ttu-id="018ce-240">È anche possibile seguire i passaggi di hello nella parte 1, ma rendere toouse che l'app web o dell'app per le API effettivo `https://{URL}` per **Sign-on URL** e **URI ID App**.</span><span class="sxs-lookup"><span data-stu-id="018ce-240">You can also follow hello steps in Part 1, but make sure toouse your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="018ce-241">Da questi passaggi, è necessario toosave sia client hello ID e l'ID tenant per l'utilizzo nel modello di distribuzione dell'applicazione, nonché per la parte 3.</span><span class="sxs-lookup"><span data-stu-id="018ce-241">From these steps, you have toosave both hello client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="018ce-242">Quando si crea l'identità dell'applicazione hello Azure AD per le app web o API, è necessario utilizzare hello portale di Azure o portale di Azure classico, anziché PowerShell.</span><span class="sxs-lookup"><span data-stu-id="018ce-242">When you create hello Azure AD application identity for your web app or API app, you must use hello Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="018ce-243">cmdlet di PowerShell Hello non impostare le autorizzazioni di hello necessario toosign gli utenti in un sito Web.</span><span class="sxs-lookup"><span data-stu-id="018ce-243">hello PowerShell commandlet doesn't set up hello required permissions toosign users into a website.</span></span>

<span data-ttu-id="018ce-244">Dopo avere ottenuto l'ID client hello e l'ID tenant, è possibile includere questi ID come un subresource dell'app web o app per le API del modello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="018ce-244">After you get hello client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

   ```
   "resources": [
       {
           "apiVersion": "2015-08-01",
           "name": "web",
           "type": "config",
           "dependsOn": ["[concat('Microsoft.Web/sites/','parameters('webAppName'))]"],
           "properties": {
               "siteAuthEnabled": true,
               "siteAuthSettings": {
                 "clientId": "{client-ID}",
                 "issuer": "https://sts.windows.net/{tenant-ID}/",
               }
           }
       }
   ]
   ```

<span data-ttu-id="018ce-245">tooautomatically distribuire un'app web vuota e una logica app con l'autenticazione di Azure Active Directory, [visualizzazione hello completo modello](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), oppure fare clic su **distribuire tooAzure** qui:</span><span class="sxs-lookup"><span data-stu-id="018ce-245">tooautomatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view hello complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy tooAzure** here:</span></span>

<span data-ttu-id="018ce-246">[![Distribuire tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="018ce-246">[![Deploy tooAzure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-hello-authorization-section-in-your-logic-app"></a><span data-ttu-id="018ce-247">Parte 3: Popolare sezione Authorization hello nell'app logica</span><span class="sxs-lookup"><span data-stu-id="018ce-247">Part 3: Populate hello Authorization section in your logic app</span></span>

<span data-ttu-id="018ce-248">modello precedente di Hello ha già impostata in questa sezione di autorizzazione, ma se si modifica direttamente hello logica app, è necessario includere sezione autorizzazioni complete hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-248">hello previous template already has this authorization section set up, but if you are directly authoring hello logic app, you must include hello full authorization section.</span></span>

<span data-ttu-id="018ce-249">Aprire la definizione dell'app logica nella visualizzazione codice, passa toohello **HTTP** una sezione di azione di ricerca hello **autorizzazione** sezione e includere questa riga:</span><span class="sxs-lookup"><span data-stu-id="018ce-249">Open your logic app definition in code view, go toohello **HTTP** action section, find hello **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="018ce-250">Elemento</span><span class="sxs-lookup"><span data-stu-id="018ce-250">Element</span></span> | <span data-ttu-id="018ce-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="018ce-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="018ce-252">tenant</span><span class="sxs-lookup"><span data-stu-id="018ce-252">tenant</span></span> |<span data-ttu-id="018ce-253">Hello GUID per il tenant hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="018ce-253">hello GUID for hello Azure AD tenant</span></span> |
| <span data-ttu-id="018ce-254">audience</span><span class="sxs-lookup"><span data-stu-id="018ce-254">audience</span></span> |<span data-ttu-id="018ce-255">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-255">Required.</span></span> <span data-ttu-id="018ce-256">Hello GUID per la risorsa di destinazione hello che si desidera tooaccess - ID client hello dall'identità dell'applicazione hello per le app web o API</span><span class="sxs-lookup"><span data-stu-id="018ce-256">hello GUID for hello target resource that you want tooaccess - hello client ID from hello application identity for your web app or API app</span></span> |
| <span data-ttu-id="018ce-257">clientId</span><span class="sxs-lookup"><span data-stu-id="018ce-257">clientId</span></span> |<span data-ttu-id="018ce-258">Hello GUID per il client di hello richiedendo l'accesso - ID client hello dall'identità dell'applicazione hello per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="018ce-258">hello GUID for hello client requesting access - hello client ID from hello application identity for your logic app</span></span> |
| <span data-ttu-id="018ce-259">secret</span><span class="sxs-lookup"><span data-stu-id="018ce-259">secret</span></span> |<span data-ttu-id="018ce-260">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-260">Required.</span></span> <span data-ttu-id="018ce-261">Hello chiave o una password dall'identità dell'applicazione hello per client hello che richiede il token di accesso di hello</span><span class="sxs-lookup"><span data-stu-id="018ce-261">hello key or password from hello application identity for hello client that's requesting hello access token</span></span> |
| <span data-ttu-id="018ce-262">type</span><span class="sxs-lookup"><span data-stu-id="018ce-262">type</span></span> |<span data-ttu-id="018ce-263">tipo di autenticazione Hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-263">hello authentication type.</span></span> <span data-ttu-id="018ce-264">Per l'autenticazione ActiveDirectoryOAuth, il valore di hello è `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="018ce-264">For ActiveDirectoryOAuth authentication, hello value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="018ce-265">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="018ce-265">For example:</span></span>

```
{
   ...
   "actions": {
      "some-action": {
         "conditions": [],
         "inputs": {
            "method": "post",
            "uri": "https://your-api-azurewebsites.net/api/your-method",
            "authentication": {
               "tenant": "tenant-ID",
               "audience": "client-ID-from-azure-ad-app-for-web-app-or-api-app",
               "clientId": "client-ID-from-azure-ad-app-for-logic-app",
               "secret": "key-from-azure-ad-app-for-logic-app",
               "type": "ActiveDirectoryOAuth"
            }
         },
      }
   }
}
```

<a name="update-code"></a>

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="018ce-266">Chiamate API protette con codice</span><span class="sxs-lookup"><span data-stu-id="018ce-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="018ce-267">Autenticazione del certificato</span><span class="sxs-lookup"><span data-stu-id="018ce-267">Certificate authentication</span></span>

<span data-ttu-id="018ce-268">toovalidate hello le richieste in ingresso dal logica app tooyour web app o app per le API, è possibile utilizzare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="018ce-268">toovalidate hello incoming requests from your logic app tooyour web app or API app, you can use client certificates.</span></span> <span data-ttu-id="018ce-269">informazioni su tooset il codice, [come l'autenticazione reciproca TLS tooconfigure](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="018ce-269">tooset up your code, learn [how tooconfigure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="018ce-270">In hello **autorizzazione** sezione, includere questa riga:</span><span class="sxs-lookup"><span data-stu-id="018ce-270">In hello **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="018ce-271">Elemento</span><span class="sxs-lookup"><span data-stu-id="018ce-271">Element</span></span> | <span data-ttu-id="018ce-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="018ce-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="018ce-273">type</span><span class="sxs-lookup"><span data-stu-id="018ce-273">type</span></span> |<span data-ttu-id="018ce-274">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-274">Required.</span></span> <span data-ttu-id="018ce-275">tipo di autenticazione Hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-275">hello authentication type.</span></span> <span data-ttu-id="018ce-276">Per i certificati client SSL, deve essere il valore di hello `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="018ce-276">For SSL client certificates, hello value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="018ce-277">password</span><span class="sxs-lookup"><span data-stu-id="018ce-277">password</span></span> |<span data-ttu-id="018ce-278">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-278">Required.</span></span> <span data-ttu-id="018ce-279">password di Hello per accedere al certificato del client hello (file. PFX)</span><span class="sxs-lookup"><span data-stu-id="018ce-279">hello password for accessing hello client certificate (PFX file)</span></span> |
| <span data-ttu-id="018ce-280">pfx</span><span class="sxs-lookup"><span data-stu-id="018ce-280">pfx</span></span> |<span data-ttu-id="018ce-281">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-281">Required.</span></span> <span data-ttu-id="018ce-282">Contenuto con codifica Base64 del certificato del client hello (file. PFX)</span><span class="sxs-lookup"><span data-stu-id="018ce-282">Base64-encoded contents of hello client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="018ce-283">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="018ce-283">Basic authentication</span></span>

<span data-ttu-id="018ce-284">toovalidate richieste in ingresso dal logica app tooyour web app o app per le API, è possibile utilizzare l'autenticazione di base, ad esempio un nome utente e password.</span><span class="sxs-lookup"><span data-stu-id="018ce-284">toovalidate incoming requests from your logic app tooyour web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="018ce-285">Autenticazione di base è un modello comune, e le app web o API, è possibile utilizzare l'autenticazione in qualsiasi toobuild linguaggio utilizzato.</span><span class="sxs-lookup"><span data-stu-id="018ce-285">Basic authentication is a common pattern, and you can use this authentication in any language used toobuild your web app or API app.</span></span>

<span data-ttu-id="018ce-286">In hello **autorizzazione** sezione, includere questa riga:</span><span class="sxs-lookup"><span data-stu-id="018ce-286">In hello **Authorization** section, include this line:</span></span>

<span data-ttu-id="018ce-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="018ce-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="018ce-288">Elemento</span><span class="sxs-lookup"><span data-stu-id="018ce-288">Element</span></span> | <span data-ttu-id="018ce-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="018ce-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="018ce-290">type</span><span class="sxs-lookup"><span data-stu-id="018ce-290">type</span></span> |<span data-ttu-id="018ce-291">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-291">Required.</span></span> <span data-ttu-id="018ce-292">tipo di autenticazione Hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-292">hello authentication type.</span></span> <span data-ttu-id="018ce-293">L'autenticazione di base, deve essere il valore di hello `Basic`.</span><span class="sxs-lookup"><span data-stu-id="018ce-293">For basic authentication, hello value must be `Basic`.</span></span> |
| <span data-ttu-id="018ce-294">username</span><span class="sxs-lookup"><span data-stu-id="018ce-294">username</span></span> |<span data-ttu-id="018ce-295">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-295">Required.</span></span> <span data-ttu-id="018ce-296">nome utente di Hello per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="018ce-296">hello username for authentication</span></span> |
| <span data-ttu-id="018ce-297">password</span><span class="sxs-lookup"><span data-stu-id="018ce-297">password</span></span> |<span data-ttu-id="018ce-298">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="018ce-298">Required.</span></span> <span data-ttu-id="018ce-299">password Hello per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="018ce-299">hello password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="018ce-300">Autenticazione di Azure Active Directory usando il codice</span><span class="sxs-lookup"><span data-stu-id="018ce-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="018ce-301">Per impostazione predefinita, l'autenticazione di Azure AD hello che attivare in hello portale di Azure non fornisce un'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="018ce-301">By default, hello Azure AD authentication that you turn on in hello Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="018ce-302">Ad esempio, questa autenticazione Blocca toojust l'API, un tenant specifico, non tooa utente o specifico dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="018ce-302">For example, this authentication locks your API toojust a specific tenant, not tooa specific user or app.</span></span> 

<span data-ttu-id="018ce-303">API toorestrict accesso tooyour logica app tramite codice, estrarre l'intestazione hello che dispone di hello JSON web token (JWT).</span><span class="sxs-lookup"><span data-stu-id="018ce-303">toorestrict API access tooyour logic app through code, extract hello header that has hello JSON web token (JWT).</span></span> <span data-ttu-id="018ce-304">Verificare l'identità del chiamante hello e rifiutare le richieste che non corrispondono.</span><span class="sxs-lookup"><span data-stu-id="018ce-304">Check hello caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="018ce-305">Continua, tooimplement questa autenticazione interamente nel proprio codice e non utilizzare hello portale di Azure, informazioni su come troppo [l'autenticazione con locale di Active Directory in Azure app](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="018ce-305">Going further, tooimplement this authentication entirely in your own code, and not use hello Azure portal, learn how too [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="018ce-306">identità di un'applicazione per l'app logica toocreate e utilizzare tale toocall identità dell'API, è necessario seguire i passaggi precedenti hello.</span><span class="sxs-lookup"><span data-stu-id="018ce-306">toocreate an application identity for your logic app and use that identity toocall your API, you must follow hello previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="018ce-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="018ce-307">Next steps</span></span>

* [<span data-ttu-id="018ce-308">Controllare le prestazioni dell'app per la logica con avvisi e log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="018ce-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)