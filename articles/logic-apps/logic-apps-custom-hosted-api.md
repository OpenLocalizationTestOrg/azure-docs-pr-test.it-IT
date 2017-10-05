---
title: Distribuire, chiamare e autenticare API Web e API REST per le app per la logica di Azure | Microsoft Docs
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
ms.openlocfilehash: 88c62d5ab046d8cf4bce5d23b776e517bb0e1d87
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-call-and-authenticate-custom-apis-as-connectors-for-logic-apps"></a><span data-ttu-id="b9fa3-104">Distribuire, chiamare e autenticare le API personalizzate come connettori per le app per la logica</span><span class="sxs-lookup"><span data-stu-id="b9fa3-104">Deploy, call, and authenticate custom APIs as connectors for logic apps</span></span>

<span data-ttu-id="b9fa3-105">Dopo aver [creato le API personalizzate](./logic-apps-create-api-app.md) che offrono le azioni o i trigger da usare nei flussi di lavoro delle app per la logica, è necessario implementare le API prima di eseguire la chiamata.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-105">After you [create custom APIs](./logic-apps-create-api-app.md) that provide actions or triggers to use in logic apps workflows, you must deploy your APIs before you can call them.</span></span> <span data-ttu-id="b9fa3-106">Sebbene sia possibile chiamare qualsiasi API da un'app per la logica, per ottimizzare i risultati aggiungere [metadati Swagger](http://swagger.io/specification/) che descrivano le operazioni e i parametri dell'API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-106">And although you can call any API from a logic app, for the best experience, add [Swagger metadata](http://swagger.io/specification/) that describes your API's operations and parameters.</span></span> <span data-ttu-id="b9fa3-107">Il file Swagger consente all'API di funzionare meglio e di integrarsi più facilmente con le app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-107">This Swagger file helps your API work better and integrate more easily with logic apps.</span></span>

<span data-ttu-id="b9fa3-108">È possibile implementare le API come [app Web](../app-service-web/app-service-web-overview.md), ma è consigliabile distribuirle come [app per le API](../app-service-api/app-service-api-apps-why-best-platform.md), in modo da semplificare il lavoro durante la compilazione, l'hosting e l'uso delle API nel cloud e in locale.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-108">You can deploy your APIs as [web apps](../app-service-web/app-service-web-overview.md), but consider deploying your APIs as [API apps](../app-service-api/app-service-api-apps-why-best-platform.md), which can make your job easier when you build, host, and consume APIs in the cloud and on premises.</span></span> <span data-ttu-id="b9fa3-109">Non è necessario modificare alcun codice nelle API, è sufficiente implementare il codice a un'app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-109">You don't have to change any code in your APIs -- just deploy your code to an API app.</span></span> <span data-ttu-id="b9fa3-110">È possibile ospitare le API nel [servizio app di Azure](../app-service/app-service-value-prop-what-is.md), una soluzione PaaS (platform-as-a-service) che offre uno dei modi più efficaci, semplici e scalabili per ospitare l'API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-110">You can host your APIs on [Azure App Service](../app-service/app-service-value-prop-what-is.md), a platform-as-a-service (PaaS) offering that provides one of the best, easiest, and most scalable ways for API hosting.</span></span>

<span data-ttu-id="b9fa3-111">Per autenticare le chiamate dalle app per la logica all'API, è possibile configurare Azure Active Directory nel portale di Azure, in modo da non dover aggiornare il codice.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-111">To authenticate calls from logic apps to your APIs, you can set up Azure Active Directory in the Azure portal so you don't have to update your code.</span></span> <span data-ttu-id="b9fa3-112">Oppure, è possibile richiedere e applicare l'autenticazione attraverso il codice dell'API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-112">Or, you can require and enforce authentication through your API's code.</span></span>

## <a name="deploy-your-api-as-a-web-app-or-api-app"></a><span data-ttu-id="b9fa3-113">Distribuire l'API come app Web o app per le API</span><span class="sxs-lookup"><span data-stu-id="b9fa3-113">Deploy your API as a web app or API app</span></span>

<span data-ttu-id="b9fa3-114">Prima di chiamare l'API personalizzata da un'app per la logica, implementare l'API come app Web o app per le API al servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-114">Before you can call your custom API from a logic app, deploy your API as a web app or API app to Azure App Service.</span></span> <span data-ttu-id="b9fa3-115">Rendere inoltre leggibile il documento Swagger per Progettazione app per la logica, impostare le proprietà di definizione dell'API e attivare la [condivisione di risorse tra le origini](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) per l'app Web o l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-115">Also, to make your Swagger document readable by the Logic App Designer, set the API definition properties and turn on [cross-origin resource sharing (CORS)](../app-service-api/app-service-api-cors-consume-javascript.md#corsconfig) for your web app or API app.</span></span>

1. <span data-ttu-id="b9fa3-116">Nel portale di Azure selezionare l'app Web o l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-116">In the Azure portal, select your web app or API app.</span></span>

2. <span data-ttu-id="b9fa3-117">Nell'area **API** del pannello visualizzato scegliere **Definizione API**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-117">In the blade that opens, under **API**, choose **API definition**.</span></span> <span data-ttu-id="b9fa3-118">Impostare la **posizione della definizione dell'API** sull'URL del file swagger.json.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-118">Set the **API definition location** to the URL for your swagger.json file.</span></span>

   <span data-ttu-id="b9fa3-119">In genere, l'URL viene visualizzato in questo formato: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span><span class="sxs-lookup"><span data-stu-id="b9fa3-119">Usually, the URL appears in this format: `https://{name}.azurewebsites.net/swagger/docs/v1)`</span></span>

   ![Collegamento al file Swagger per l'API personalizzata](media/logic-apps-custom-hosted-api/custom-api-swagger-url.png)

3. <span data-ttu-id="b9fa3-121">Scegliere **CORS** nell'area **API**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-121">Under **API**, choose **CORS**.</span></span> <span data-ttu-id="b9fa3-122">Impostare i criteri CORS per le **origini consentite** su **'*'** (consenti tutto).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-122">Set the CORS policy for **Allowed origins** to **'*'** (allow all).</span></span>

   <span data-ttu-id="b9fa3-123">Questa impostazione consente le richieste da Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-123">This setting permits requests from Logic App Designer.</span></span>

   ![Consentire le richieste da Progettazione app per la logica all'API personalizzata](media/logic-apps-custom-hosted-api/custom-api-cors.png)

<span data-ttu-id="b9fa3-125">Per altre informazioni, vedere questi articoli:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-125">For more information, see these articles:</span></span>

* [<span data-ttu-id="b9fa3-126">Aggiungere metadati Swagger per le API Web ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b9fa3-126">Add Swagger metadata for ASP.NET web APIs</span></span>](../app-service-api/app-service-api-dotnet-get-started.md#use-swagger-api-metadata-and-ui)
* [<span data-ttu-id="b9fa3-127">Distribuire app Web ASP.NET al servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b9fa3-127">Deploy ASP.NET web APIs to Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-get-started.md)

## <a name="call-your-custom-api-from-logic-app-workflows"></a><span data-ttu-id="b9fa3-128">Chiamare l'API personalizzata dai flussi di lavoro delle app per la logica</span><span class="sxs-lookup"><span data-stu-id="b9fa3-128">Call your custom API from logic app workflows</span></span>

<span data-ttu-id="b9fa3-129">Dopo aver impostato le proprietà di definizione API e CORS, i trigger e le azioni dell'API personalizzata devono essere disponibili per l'inserimento nel flusso di lavoro delle app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-129">After you set up the API definition properties and CORS, your custom API's triggers and actions should become available for you to include in your logic app workflow.</span></span> 

*  <span data-ttu-id="b9fa3-130">Per visualizzare i siti Web con URL di Swagger, è possibile sfogliare i siti Web di sottoscrizione in Progettazione app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-130">To view the websites that have Swagger URLs, you can browse your subscription websites in the Logic Apps Designer.</span></span>

*  <span data-ttu-id="b9fa3-131">Per visualizzare le azioni e gli input disponibili puntando a un documento di Swagger, usare l'[azione HTTP + Swagger](../connectors/connectors-native-http-swagger.md).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-131">To view available actions and inputs by pointing at a Swagger document, use the [HTTP + Swagger action](../connectors/connectors-native-http-swagger.md).</span></span>

*  <span data-ttu-id="b9fa3-132">Per chiamare qualsiasi API, incluse le API che non hanno o non espongono un documento Swagger, è sempre possibile creare una richiesta con l'[azione HTTP](../connectors/connectors-native-http.md).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-132">To call any API, including APIs that don't have or expose a Swagger document, you can always create a request with the [HTTP action](../connectors/connectors-native-http.md).</span></span>

## <a name="authenticate-calls-to-your-custom-api"></a><span data-ttu-id="b9fa3-133">Autenticare le chiamate all'API personalizzata</span><span class="sxs-lookup"><span data-stu-id="b9fa3-133">Authenticate calls to your custom API</span></span>

<span data-ttu-id="b9fa3-134">È possibile proteggere le chiamate all'API personalizzata nei modi seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-134">You can secure calls to your custom API in these ways:</span></span>

* <span data-ttu-id="b9fa3-135">[Nessuna modifica del codice](#no-code): proteggere l'API con [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) dal portale di Azure, in modo che non sia necessario aggiornare il codice o implementare nuovamente l'API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-135">[No code changes](#no-code): Protect your API with [Azure Active Directory (Azure AD)](../active-directory/active-directory-whatis.md) through the Azure portal, so you don't have to update your code or redeploy your API.</span></span>

  > [!NOTE]
  > <span data-ttu-id="b9fa3-136">Per impostazione predefinita, l'autenticazione di Azure AD che si attiva nel portale di Azure non offre un'autorizzazione con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-136">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="b9fa3-137">Ad esempio, questa autenticazione blocca l'API a un tenant specifico, non a un determinato utente o app.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-137">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

* <span data-ttu-id="b9fa3-138">[Aggiornare il codice dell'API](#update-code): proteggere l'API applicando [l'autenticazione del certificato](#certificate), [l'autenticazione di base](#basic) o [autenticazione di Azure AD](#azure-ad-code) attraverso il codice.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-138">[Update your API's code](#update-code): Protect your API by enforcing [certificate authentication](#certificate), [basic authentication](#basic), or [Azure AD authentication](#azure-ad-code) through code.</span></span>

<a name="no-code"></a>

### <a name="authenticate-calls-to-your-api-without-changing-code"></a><span data-ttu-id="b9fa3-139">Autenticare le chiamate all'API senza modificare il codice</span><span class="sxs-lookup"><span data-stu-id="b9fa3-139">Authenticate calls to your API without changing code</span></span>

<span data-ttu-id="b9fa3-140">Questi sono i passaggi generali per questo metodo:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-140">Here's the general steps for this method:</span></span>

1. <span data-ttu-id="b9fa3-141">Creare due [identità di applicazione di Azure Active Directory (Azure AD)](../app-service-api/app-service-api-dotnet-service-principal-auth.md), una per l'app per la logica e una per l'app Web (o l'app per le API).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-141">Create two [Azure Active Directory (Azure AD) application identities](../app-service-api/app-service-api-dotnet-service-principal-auth.md): one for your logic app and one for your web app (or API app).</span></span>

2. <span data-ttu-id="b9fa3-142">Per autenticare le chiamate all'API, usare le credenziali (ID client e segreto) per l'[entità servizio](../app-service-api/app-service-api-dotnet-service-principal-auth.md) associata all'identità di applicazione di Azure AD per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-142">To authenticate calls to your API, use the credentials (client ID and secret) for the [service principal](../app-service-api/app-service-api-dotnet-service-principal-auth.md) that's associated with the Azure AD application identity for your logic app.</span></span>

3. <span data-ttu-id="b9fa3-143">Includere gli ID applicazione nella definizione di app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-143">Include the application IDs in your logic app definition.</span></span>

#### <a name="part-1-create-an-azure-ad-application-identity-for-your-logic-app"></a><span data-ttu-id="b9fa3-144">Parte 1: Creare un'identità di applicazione di Azure AD per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="b9fa3-144">Part 1: Create an Azure AD application identity for your logic app</span></span>

<span data-ttu-id="b9fa3-145">L'app per la logica usa questa identità di applicazione di Azure AD per l'autenticazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-145">Your logic app uses this Azure AD application identity to authenticate against Azure AD.</span></span> <span data-ttu-id="b9fa3-146">È sufficiente impostare l'identità una sola volta per la directory.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-146">You only have to set up this identity one time for your directory.</span></span> <span data-ttu-id="b9fa3-147">Ad esempio, si può scegliere di usare la stessa identità per tutte le app per la logica, anche se è possibile creare identità univoche per ogni app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-147">For example, you can choose to use the same identity for all your logic apps, even though you can create unique identities for each logic app.</span></span> <span data-ttu-id="b9fa3-148">È possibile impostare queste identità nel portale di Azure, nel [portale di Azure classico](#app-identity-logic-classic) o usare [PowerShell](#powershell).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-148">You can set up these identities in the Azure portal, [Azure classic portal](#app-identity-logic-classic), or use [PowerShell](#powershell).</span></span>

<span data-ttu-id="b9fa3-149">**Creare l'identità di applicazione per l'app per la logica nel portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-149">**Create the application identity for your logic app in the Azure portal**</span></span>

1. <span data-ttu-id="b9fa3-150">Nel [portale di Azure](https://portal.azure.com "https://portal.azure.com") scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-150">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), choose **Azure Active Directory**.</span></span> 

2. <span data-ttu-id="b9fa3-151">Verificare di essere nella stessa directory dell'app Web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-151">Confirm that you're in the same directory as your web app or API app.</span></span>

   > [!TIP]
   > <span data-ttu-id="b9fa3-152">Per passare da una directory all'altra, fare clic sul proprio profilo e selezionare un'altra directory.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-152">To switch directories, click your profile and select another directory.</span></span> <span data-ttu-id="b9fa3-153">In alternativa, scegliere **Panoramica** > **Cambia directory**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-153">Or, choose **Overview** > **Switch directory**.</span></span>

3. <span data-ttu-id="b9fa3-154">Nel menu delle directory scegliere da **Gestisci** **Registrazioni per l'app** > **Registrazione nuova applicazione**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-154">On the directory menu, under **Manage**, choose **App registrations** > **New application registration**.</span></span>

   > [!TIP]
   > <span data-ttu-id="b9fa3-155">Per impostazione predefinita, l'elenco delle registrazioni di app indica tutte le registrazioni di app presenti nella directory.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-155">By default, the app registrations list shows all app registrations in your directory.</span></span> <span data-ttu-id="b9fa3-156">Per visualizzare solo le registrazioni delle proprie app, selezionare **Le mie app** accanto alla casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-156">To view only your app registrations, next to the search box, select **My apps**.</span></span> 

   ![Creare una nuova registrazione di app](./media/logic-apps-custom-hosted-api/new-app-registration-azure-portal.png)

4. <span data-ttu-id="b9fa3-158">Assegnare un nome all'identità di applicazione, lasciare il **tipo di applicazione** impostato su **App Web/API**, specificare una stringa univoca formattata come dominio per **URL accesso** e scegliere **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-158">Give your application identity a name, leave **Application type** set to **Web app / API**, provide a unique string formatted as a domain for **Sign-on URL**, and choose **Create**.</span></span>

   ![Specificare nome e URL di accesso per l'identità di applicazione](./media/logic-apps-custom-hosted-api/logic-app-identity-azure-portal.png)

   <span data-ttu-id="b9fa3-160">L'identità di applicazione creata per l'app per la logica ora appare nell'elenco delle registrazioni di app.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-160">The application identity that you created for your logic app now appears in the app registrations list.</span></span>

   ![Identità di applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-identity-created.png)

5. <span data-ttu-id="b9fa3-162">Nell'elenco di registrazioni di app selezionare la nuova identità di applicazione.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-162">In the app registrations list, select your new application identity.</span></span> <span data-ttu-id="b9fa3-163">Copiare e salvare l'**ID applicazione** da usare come "ID client" per l'app per la logica nella Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-163">Copy and save the **Application ID** to use as the "client ID" for your logic app in Part 3.</span></span>

   ![Copiare e salvare l'ID applicazione per l'app per la logica](./media/logic-apps-custom-hosted-api/logic-app-application-id.png)

6. <span data-ttu-id="b9fa3-165">Se le impostazioni dell'identità di applicazione non sono visibili, scegliere **Impostazioni** o **Tutte le impostazioni**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-165">If your application identity settings aren't visible, choose **Settings** or **All settings**.</span></span>

7. <span data-ttu-id="b9fa3-166">Scegliere **Chiavi** in **Accesso all'API**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-166">Under **API Access**, choose **Keys**.</span></span> <span data-ttu-id="b9fa3-167">In **Descrizione** specificare un nome per la chiave.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-167">Under **Description**, provide a name for your key.</span></span> <span data-ttu-id="b9fa3-168">Selezionare una **scadenza** per la durata della chiave.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-168">Under **Expires**, select a duration for your key.</span></span>

   <span data-ttu-id="b9fa3-169">La chiave che si sta creando agisce come "segreto" o password dell'identità di applicazione per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-169">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

   ![Creare una chiave per l'identità dell'app per la logica](./media/logic-apps-custom-hosted-api/create-logic-app-identity-key-secret-password.png)

8. <span data-ttu-id="b9fa3-171">Scegliere **Salva** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-171">On the toolbar, choose **Save**.</span></span> <span data-ttu-id="b9fa3-172">La chiave viene visualizzata in **Valore**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-172">Under **Value**, your key now appears.</span></span> 
<span data-ttu-id="b9fa3-173">Poiché la chiave viene nascosta quando si lascia il pannello, **assicurarsi di copiarla e salvarla** per usarla in un secondo tempo.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-173">**Make sure to copy and save your key** for later use because the key is hidden when you leave the key blade.</span></span>

   <span data-ttu-id="b9fa3-174">Quando si configura l'app per la logica nella Parte 3, si specifica questa chiave come "segreto" o password.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-174">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

   ![Copiare e salvare la chiave per usarla in un momento successivo](./media/logic-apps-custom-hosted-api/logic-app-copy-key-secret-password.png)

<a name="app-identity-logic-classic"></a>

<span data-ttu-id="b9fa3-176">**Creare l'identità di applicazione per l'app per la logica nel portale di Azure classico**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-176">**Create the application identity for your logic app in the Azure classic portal**</span></span>

1. <span data-ttu-id="b9fa3-177">Nel portale di Azure classico scegliere [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-177">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2. <span data-ttu-id="b9fa3-178">Selezionare la stessa directory che si usa per l'app Web o l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-178">Select the same directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="b9fa3-179">Nella scheda **Applicazioni** scegliere **Aggiungi** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-179">On the **Applications** tab, choose **Add** at the bottom of the page.</span></span>

4. <span data-ttu-id="b9fa3-180">Assegnare un nome all'identità di applicazione e scegliere **Avanti** (freccia destra).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-180">Give your application identity a name, and choose **Next** (right arrow).</span></span>

5. <span data-ttu-id="b9fa3-181">In **Proprietà dell'app** specificare una stringa univoca formattata come dominio per **URL accesso** e **URI ID app** e scegliere **Completa** (segno di spunta).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-181">Under **App properties**, provide a unique string formatted as a domain for **Sign-on URL** and **App ID URI**, and choose **Complete** (checkmark).</span></span>

6. <span data-ttu-id="b9fa3-182">Nella scheda di **configurazione** copiare e salvare l'**ID client** per l'app per la logica da usare nella Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-182">On the **Configure** tab, copy and save the **Client ID** for your logic app to use in Part 3.</span></span>

7. <span data-ttu-id="b9fa3-183">In **Chiavi** aprire l'elenco **Seleziona durata**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-183">Under **Keys**, open the **Select duration** list.</span></span> <span data-ttu-id="b9fa3-184">Selezionare una durata per la chiave.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-184">Select a duration for your key.</span></span>

   <span data-ttu-id="b9fa3-185">La chiave che si sta creando agisce come "segreto" o password dell'identità di applicazione per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-185">The key that you're creating acts as the application identity's "secret" or password for your logic app.</span></span>

8. <span data-ttu-id="b9fa3-186">Fare clic su **Salva** nella parte inferiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-186">At the bottom of the page, choose **Save**.</span></span> <span data-ttu-id="b9fa3-187">Potrebbe essere necessario attendere alcuni secondi.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-187">You might have to wait a few seconds.</span></span>

9. <span data-ttu-id="b9fa3-188">In **Chiavi** assicurarsi di copiare e salvare la chiave che ora viene visualizzata.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-188">Under **Keys**, make sure to copy and save the key that now appears.</span></span> 

   <span data-ttu-id="b9fa3-189">Quando si configura l'app per la logica nella Parte 3, si specifica questa chiave come "segreto" o password.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-189">When you configure your logic app in Part 3, you specify this key as the "secret" or password.</span></span>

<span data-ttu-id="b9fa3-190">Per altre informazioni, vedere la procedura di [configurazione di un'applicazione del servizio app per usare l'account di accesso di Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-190">For more information, learn how to [configure your App Service application to use Azure Active Directory login](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).</span></span>

<a name="powershell"></a>

<span data-ttu-id="b9fa3-191">**Creare l'identità di applicazione per l'app per la logica in PowerShell**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-191">**Create the application identity for your logic app in PowerShell**</span></span>

<span data-ttu-id="b9fa3-192">È possibile eseguire questa attività usando Azure Resource Manager con PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-192">You can perform this task through Azure Resource Manager with PowerShell.</span></span> <span data-ttu-id="b9fa3-193">In PowerShell eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-193">In PowerShell, run these commands:</span></span>

1. `Switch-AzureMode AzureResourceManager`

2. `Add-AzureAccount`

3. `New-AzureADApplication -DisplayName "MyLogicAppID" -HomePage "http://mydomain.tld" -IdentifierUris "http://mydomain.tld" -Password "identity-password"`

4. <span data-ttu-id="b9fa3-194">Assicurarsi di copiare l'**ID tenant** (GUID per il tenant di Azure AD), l'**ID applicazione** e la password usati.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-194">Make sure to copy the **Tenant ID** (GUID for your Azure AD tenant), the **Application ID**, and the password that you used.</span></span>

<span data-ttu-id="b9fa3-195">Per altre informazioni, vedere la procedura di [creazione di un'entità servizio con PowerShell per accedere alle risorse](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-195">For more information, learn how to [create a service principal with PowerShell to access resources](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

#### <a name="part-2-create-an-azure-ad-application-identity-for-your-web-app-or-api-app"></a><span data-ttu-id="b9fa3-196">Parte 2: Creare un'identità di applicazione di Azure AD per l'app Web o l'app per le API</span><span class="sxs-lookup"><span data-stu-id="b9fa3-196">Part 2: Create an Azure AD application identity for your web app or API app</span></span>

<span data-ttu-id="b9fa3-197">Se l'app Web o l'app per le API è già stata distribuita, è possibile attivare l'autenticazione e creare l'identità di applicazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-197">If your web app or API app is already deployed, you can turn on authentication and create the application identity in the Azure portal.</span></span> <span data-ttu-id="b9fa3-198">In alternativa, è possibile [attivare l'autenticazione quando si effettua la distribuzione con un modello di Azure Resource Manager](#authen-deploy).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-198">Otherwise, you can [turn on authentication when you deploy with an Azure Resource Manager template](#authen-deploy).</span></span> 

<span data-ttu-id="b9fa3-199">**Creare l'identità di applicazione e attivare l'autenticazione nel portale di Azure per le app distribuite**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-199">**Create the application identity and turn on authentication in the Azure portal for deployed apps**</span></span>

1. <span data-ttu-id="b9fa3-200">Nel [portale di Azure](https://portal.azure.com "https://portal.azure.com") individuare e selezionare l'app Web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-200">In the [Azure portal](https://portal.azure.com "https://portal.azure.com"), find and select your web app or API app.</span></span> 

2. <span data-ttu-id="b9fa3-201">In **Impostazioni** scegliere **Autenticazione/Autorizzazione**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-201">Under **Settings**, choose **Authentication/Authorization**.</span></span> <span data-ttu-id="b9fa3-202">In **Autenticazione servizio app** **attivare** l'autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-202">Under **App Service Authentication**, turn authentication **On**.</span></span> <span data-ttu-id="b9fa3-203">In **Provider di autenticazione** scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-203">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span>

   ![Attivare l'autenticazione](./media/logic-apps-custom-hosted-api/custom-web-api-app-authentication.png)

3. <span data-ttu-id="b9fa3-205">Creare un'identità di applicazione per l'app Web o l'app per le API come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-205">Now create an application identity for your web app or API app as shown here.</span></span> <span data-ttu-id="b9fa3-206">Nel pannello **Impostazioni di Azure Active Directory** impostare la **modalità di gestione** su **Rapida**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-206">On the **Azure Active Directory Settings** blade, set **Management mode** to **Express**.</span></span> <span data-ttu-id="b9fa3-207">Scegliere **Crea nuova App AD**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-207">Choose **Create New AD App**.</span></span> <span data-ttu-id="b9fa3-208">Assegnare un nome all'identità di applicazione e scegliere **OK**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-208">Give your application identity a name, and choose **OK**.</span></span> 

   ![Creare un'identità di applicazione per l'app Web o l'app per le API](./media/logic-apps-custom-hosted-api/custom-api-application-identity.png)

4. <span data-ttu-id="b9fa3-210">Nel pannello **Autenticazione/Autorizzazione** scegliere **Salva**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-210">On the **Authentication / Authorization blade**, choose **Save**.</span></span>

<span data-ttu-id="b9fa3-211">A questo punto è necessario trovare l'ID client e l'ID tenant per l'identità di applicazione associata all'app Web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-211">Now you must find the client ID and tenant ID for the application identity that's associated with your web app or API app.</span></span> <span data-ttu-id="b9fa3-212">Questi ID verranno usati nella Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-212">You use these IDs in Part 3.</span></span> <span data-ttu-id="b9fa3-213">Continuare con la procedura per il portale di Azure o il [portale di Azure classico](#find-id-classic).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-213">So continue with these steps for the Azure portal or [Azure classic portal](#find-id-classic).</span></span>

<span data-ttu-id="b9fa3-214">**Trovare l'ID client e l'ID tenant dell'identità di applicazione per l'app Web o app per le API nel portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-214">**Find application identity's client ID and tenant ID for your web app or API app in the Azure portal**</span></span>

1. <span data-ttu-id="b9fa3-215">In **Provider di autenticazione** scegliere **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-215">Under **Authentication Providers**, choose **Azure Active Directory**.</span></span> 

   ![Scegliere "Azure Active Directory"](./media/logic-apps-custom-hosted-api/custom-api-app-identity-client-id-tenant-id.png)

2. <span data-ttu-id="b9fa3-217">Nel pannello **Impostazioni di Azure Active Directory** impostare la **modalità di gestione** su **Avanzata**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-217">On the **Azure Active Directory Settings** blade, set **Management mode** to **Advanced**.</span></span>

3. <span data-ttu-id="b9fa3-218">Copiare l'**ID client** e salvare il GUID per usarlo nella Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-218">Copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

   > [!TIP] 
   > <span data-ttu-id="b9fa3-219">Se l'**ID client** e l'**URL dell'autorità di certificazione** non appaiono, provare ad aggiornare il portale di Azure e ripetere il passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-219">If **Client ID** and **Issuer Url** don't appear, try refreshing the Azure portal, and repeat Step 1.</span></span>

4. <span data-ttu-id="b9fa3-220">In **URL autorità di certificazione** copiare e salvare solo il GUID per la Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-220">Under **Issuer Url**, copy and save just the GUID for Part 3.</span></span> <span data-ttu-id="b9fa3-221">È anche possibile usare questo GUID nel modello di distribuzione dell'app Web o app per le API, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-221">You can also use this GUID in your web app or API app's deployment template, if necessary.</span></span>

   <span data-ttu-id="b9fa3-222">Questo GUID è il GUID del tenant specifico ("ID tenant") e deve apparire in questo URL: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="b9fa3-222">This GUID is your specific tenant's GUID ("tenant ID") and should appear in this URL: `https://sts.windows.net/{GUID}`</span></span>

5. <span data-ttu-id="b9fa3-223">Senza salvare le modifiche, chiudere il pannello delle **impostazioni di Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-223">Without saving your changes, close the **Azure Active Directory Settings** blade.</span></span>

<a name="find-id-classic"></a>

<span data-ttu-id="b9fa3-224">**Trovare l'ID client e l'ID tenant dell'identità di applicazione per l'app Web o app per le API nel portale di Azure classico**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-224">**Find application identity's client ID and tenant ID for your web app or API app in the Azure classic portal**</span></span>

1. <span data-ttu-id="b9fa3-225">Nel portale di Azure classico scegliere [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-225">In the Azure classic portal, choose [**Active Directory**](https://manage.windowsazure.com/#Workspaces/ActiveDirectoryExtension/directory).</span></span>

2.  <span data-ttu-id="b9fa3-226">Selezionare la directory che si usa per l'app Web o l'app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-226">Select the directory that you use for your web app or API app.</span></span>

3. <span data-ttu-id="b9fa3-227">Nella casella di **ricerca** trovare e selezionare l'identità di applicazione per l'app Web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-227">In the **Search** box, find and select the application identity for your web app or API app.</span></span>

4. <span data-ttu-id="b9fa3-228">Nella scheda **Configura** copiare l'**ID client** e salvare il GUID per usarlo nella Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-228">On the **Configure** tab, copy the **Client ID**, and save that GUID for use in Part 3.</span></span>

5. <span data-ttu-id="b9fa3-229">Dopo avere ottenuto l'ID client, nella parte inferiore della scheda **Configura** scegliere **Visualizza endpoint**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-229">After you get the client ID, at the bottom of the **Configure** tab, choose **View endpoints**.</span></span>

6. <span data-ttu-id="b9fa3-230">Copiare l'URL del **documento metadati federazione** e passare a tale URL.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-230">Copy the URL for **Federation Metadata Document**, and browse to that URL.</span></span>

7. <span data-ttu-id="b9fa3-231">Nel documento di metadati che si apre individuare l'elemento **EntityDescriptor ID** della radice, che ha un attributo **entityID** in questo formato: `https://sts.windows.net/{GUID}`</span><span class="sxs-lookup"><span data-stu-id="b9fa3-231">In the metadata document that opens, find the root **EntityDescriptor ID** element, which has an **entityID** attribute in this form: `https://sts.windows.net/{GUID}`</span></span> 

      <span data-ttu-id="b9fa3-232">Il GUID in questo attributo è il GUID del tenant specifico (ID tenant).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-232">The GUID in this attribute is your specific tenant's GUID (tenant ID).</span></span>

8. <span data-ttu-id="b9fa3-233">Copiare l'ID tenant e salvarlo per usarlo nella Parte 3, nonché nel modello di distribuzione dell'app Web o app per le API, se necessario.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-233">Copy the tenant ID and save that ID for use in Part 3, and also to use in your web app or API app's deployment template, if necessary.</span></span>

<span data-ttu-id="b9fa3-234">Per altre informazioni, vedere gli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-234">For more information, see these topics:</span></span>

* [<span data-ttu-id="b9fa3-235">Autenticazione utente per le app per le API nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b9fa3-235">User authentication for API apps in Azure App Service</span></span>](../app-service-api/app-service-api-dotnet-user-principal-auth.md)
* [<span data-ttu-id="b9fa3-236">Autenticazione e autorizzazione nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b9fa3-236">Authentication and authorization in Azure App Service</span></span>](../app-service/app-service-authentication-overview.md)

<a name="authen-deploy"></a>

<span data-ttu-id="b9fa3-237">**Attivare l'autenticazione quando si esegue la distribuzione con un modello di Azure Resource Manager**</span><span class="sxs-lookup"><span data-stu-id="b9fa3-237">**Turn on authentication when you deploy with an Azure Resource Manager template**</span></span>

<span data-ttu-id="b9fa3-238">È comunque necessario creare un'identità di applicazione di Azure AD per l'app Web o app per le API che differisce dall'identità di applicazione per l'app per la logica.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-238">You must still create an Azure AD application identity for your web app or API app that differs from the app identity for your logic app.</span></span> <span data-ttu-id="b9fa3-239">Per creare l'identità di applicazione, seguire i passaggi descritti in precedenza nella Parte 2 per il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-239">To create the application identity, follow the previous steps in Part 2 for the Azure portal.</span></span> <span data-ttu-id="b9fa3-240">È anche possibile seguire i passaggi della Parte 1, ma assicurarsi di usare l'elemento `https://{URL}` reale dell'app Web o app per le API per **URL accesso** e **URI dell'ID dell'app**.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-240">You can also follow the steps in Part 1, but make sure to use your web app or API app's actual `https://{URL}` for **Sign-on URL** and **App ID URI**.</span></span> <span data-ttu-id="b9fa3-241">Da questi passaggi è necessario salvare sia l'ID client che l'ID tenant per usarli nel modello di distribuzione dell'app, nonché per la Parte 3.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-241">From these steps, you have to save both the client ID and tenant ID for use in your app's deployment template and also for Part 3.</span></span>

> [!NOTE]
> <span data-ttu-id="b9fa3-242">Quando si crea l'identità di applicazione di Azure AD per l'app Web o l'app per le API, è necessario usare il portale di Azure o il portale di Azure classico, anziché PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-242">When you create the Azure AD application identity for your web app or API app, you must use the Azure portal or Azure classic portal, rather than PowerShell.</span></span> <span data-ttu-id="b9fa3-243">Il cmdlet di PowerShell non consente di impostare le autorizzazioni necessarie per l'accesso degli utenti in un sito Web.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-243">The PowerShell commandlet doesn't set up the required permissions to sign users into a website.</span></span>

<span data-ttu-id="b9fa3-244">Dopo aver ottenuto l'ID client e l'ID tenant, includerli come risorsa secondaria dell'app Web o app per le API nel modello di distribuzione:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-244">After you get the client ID and tenant ID, include these IDs as a subresource of your web app or API app in your deployment template:</span></span>

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

<span data-ttu-id="b9fa3-245">Per implementare automaticamente un'app Web vuota e un'app per la logica con l'autenticazione di Azure Active Directory, [visualizzare il modello completo qui](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json) oppure fare clic su **Distribuzione in Azure** qui:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-245">To automatically deploy a blank web app and a logic app together with Azure Active Directory authentication, [view the complete template here](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-custom-api/azuredeploy.json), or click **Deploy to Azure** here:</span></span>

<span data-ttu-id="b9fa3-246">[![Distribuzione in Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="b9fa3-246">[![Deploy to Azure](media/logic-apps-custom-hosted-api/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-logic-app-custom-api%2Fazuredeploy.json)</span></span>

#### <a name="part-3-populate-the-authorization-section-in-your-logic-app"></a><span data-ttu-id="b9fa3-247">Parte 3: Compilare la sezione Autorizzazione nell'app per la logica</span><span class="sxs-lookup"><span data-stu-id="b9fa3-247">Part 3: Populate the Authorization section in your logic app</span></span>

<span data-ttu-id="b9fa3-248">Questa sezione dell'autorizzazione è già stata configurata nel modello precedente, ma se si crea direttamente l'app per la logica, sarà necessario includere l'intera sezione relativa all'autorizzazione.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-248">The previous template already has this authorization section set up, but if you are directly authoring the logic app, you must include the full authorization section.</span></span>

<span data-ttu-id="b9fa3-249">Aprire la definizione dell'app per la logica nella visualizzazione Codice, passare alla sezione dell'azione **HTTP**, trovare la sezione dell'**autorizzazione** e includere questa riga:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-249">Open your logic app definition in code view, go to the **HTTP** action section, find the **Authorization** section, and include this line:</span></span>

`{"tenant": "{tenant-ID}", "audience": "{client-ID-from-Part-2-web-app-or-API app}", "clientId": "{client-ID-from-Part-1-logic-app}", "secret": "{key-from-Part-1-logic-app}", "type": "ActiveDirectoryOAuth" }`

| <span data-ttu-id="b9fa3-250">Elemento</span><span class="sxs-lookup"><span data-stu-id="b9fa3-250">Element</span></span> | <span data-ttu-id="b9fa3-251">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9fa3-251">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="b9fa3-252">tenant</span><span class="sxs-lookup"><span data-stu-id="b9fa3-252">tenant</span></span> |<span data-ttu-id="b9fa3-253">Il GUID per il tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="b9fa3-253">The GUID for the Azure AD tenant</span></span> |
| <span data-ttu-id="b9fa3-254">audience</span><span class="sxs-lookup"><span data-stu-id="b9fa3-254">audience</span></span> |<span data-ttu-id="b9fa3-255">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-255">Required.</span></span> <span data-ttu-id="b9fa3-256">Il GUID per la risorsa di destinazione a cui si vuole accedere: ID client dall'identità di applicazione per l'app Web o app per le API</span><span class="sxs-lookup"><span data-stu-id="b9fa3-256">The GUID for the target resource that you want to access - the client ID from the application identity for your web app or API app</span></span> |
| <span data-ttu-id="b9fa3-257">clientId</span><span class="sxs-lookup"><span data-stu-id="b9fa3-257">clientId</span></span> |<span data-ttu-id="b9fa3-258">Il GUID per il client che richiede l'accesso: ID client dall'identità di applicazione per l'app per la logica</span><span class="sxs-lookup"><span data-stu-id="b9fa3-258">The GUID for the client requesting access - the client ID from the application identity for your logic app</span></span> |
| <span data-ttu-id="b9fa3-259">secret</span><span class="sxs-lookup"><span data-stu-id="b9fa3-259">secret</span></span> |<span data-ttu-id="b9fa3-260">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-260">Required.</span></span> <span data-ttu-id="b9fa3-261">La chiave o la password dall'identità di applicazione per il client che richiede il token di accesso</span><span class="sxs-lookup"><span data-stu-id="b9fa3-261">The key or password from the application identity for the client that's requesting the access token</span></span> |
| <span data-ttu-id="b9fa3-262">type</span><span class="sxs-lookup"><span data-stu-id="b9fa3-262">type</span></span> |<span data-ttu-id="b9fa3-263">Il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-263">The authentication type.</span></span> <span data-ttu-id="b9fa3-264">Per l'autenticazione ActiveDirectoryOAuth, il valore è `ActiveDirectoryOAuth`.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-264">For ActiveDirectoryOAuth authentication, the value is `ActiveDirectoryOAuth`.</span></span> |

<span data-ttu-id="b9fa3-265">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-265">For example:</span></span>

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

### <a name="secure-api-calls-through-code"></a><span data-ttu-id="b9fa3-266">Chiamate API protette con codice</span><span class="sxs-lookup"><span data-stu-id="b9fa3-266">Secure API calls through code</span></span>

<a name="certificate"></a>

#### <a name="certificate-authentication"></a><span data-ttu-id="b9fa3-267">Autenticazione del certificato</span><span class="sxs-lookup"><span data-stu-id="b9fa3-267">Certificate authentication</span></span>

<span data-ttu-id="b9fa3-268">Per convalidare le richieste in ingresso dall'app per la logica all'app Web o all'app per le API, è possibile usare i certificati client.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-268">To validate the incoming requests from your logic app to your web app or API app, you can use client certificates.</span></span> <span data-ttu-id="b9fa3-269">Per configurare il codice, vedere le informazioni relative alla [configurazione dell'autenticazione reciproca TLS](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-269">To set up your code, learn [how to configure TLS mutual authentication](../app-service-web/app-service-web-configure-tls-mutual-auth.md).</span></span>

<span data-ttu-id="b9fa3-270">Includere questa riga nella sezione dell'**autorizzazione**:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-270">In the **Authorization** section, include this line:</span></span> 

`{"type": "clientcertificate", "password": "password", "pfx": "long-pfx-key"}`

| <span data-ttu-id="b9fa3-271">Elemento</span><span class="sxs-lookup"><span data-stu-id="b9fa3-271">Element</span></span> | <span data-ttu-id="b9fa3-272">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9fa3-272">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="b9fa3-273">type</span><span class="sxs-lookup"><span data-stu-id="b9fa3-273">type</span></span> |<span data-ttu-id="b9fa3-274">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-274">Required.</span></span> <span data-ttu-id="b9fa3-275">Il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-275">The authentication type.</span></span> <span data-ttu-id="b9fa3-276">Per i certificati client SSL, il valore deve essere `ClientCertificate`.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-276">For SSL client certificates, the value must be `ClientCertificate`.</span></span> |
| <span data-ttu-id="b9fa3-277">password</span><span class="sxs-lookup"><span data-stu-id="b9fa3-277">password</span></span> |<span data-ttu-id="b9fa3-278">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-278">Required.</span></span> <span data-ttu-id="b9fa3-279">La password per accedere al certificato client (file PFX)</span><span class="sxs-lookup"><span data-stu-id="b9fa3-279">The password for accessing the client certificate (PFX file)</span></span> |
| <span data-ttu-id="b9fa3-280">pfx</span><span class="sxs-lookup"><span data-stu-id="b9fa3-280">pfx</span></span> |<span data-ttu-id="b9fa3-281">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-281">Required.</span></span> <span data-ttu-id="b9fa3-282">I contenuti del certificato client in codifica Base64 (file PFX)</span><span class="sxs-lookup"><span data-stu-id="b9fa3-282">Base64-encoded contents of the client certificate (PFX file)</span></span> |

<a name="basic"></a>

#### <a name="basic-authentication"></a><span data-ttu-id="b9fa3-283">Autenticazione di base</span><span class="sxs-lookup"><span data-stu-id="b9fa3-283">Basic authentication</span></span>

<span data-ttu-id="b9fa3-284">Per convalidare le richieste in ingresso dall'app per la logica all'app Web o app per le API, è possibile usare l'autenticazione di base, ad esempio un nome utente e una password.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-284">To validate incoming requests from your logic app to your web app or API app, you can use basic authentication, such as a username and password.</span></span> <span data-ttu-id="b9fa3-285">L'autenticazione di base è un modello comune applicabile a qualsiasi linguaggio usato per compilare l'app Web o app per le API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-285">Basic authentication is a common pattern, and you can use this authentication in any language used to build your web app or API app.</span></span>

<span data-ttu-id="b9fa3-286">Includere questa riga nella sezione dell'**autorizzazione**:</span><span class="sxs-lookup"><span data-stu-id="b9fa3-286">In the **Authorization** section, include this line:</span></span>

<span data-ttu-id="b9fa3-287">`{"type": "basic", "username": "username", "password": "password"}`.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-287">`{"type": "basic", "username": "username", "password": "password"}`.</span></span>

| <span data-ttu-id="b9fa3-288">Elemento</span><span class="sxs-lookup"><span data-stu-id="b9fa3-288">Element</span></span> | <span data-ttu-id="b9fa3-289">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b9fa3-289">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9fa3-290">type</span><span class="sxs-lookup"><span data-stu-id="b9fa3-290">type</span></span> |<span data-ttu-id="b9fa3-291">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-291">Required.</span></span> <span data-ttu-id="b9fa3-292">Il tipo di autenticazione.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-292">The authentication type.</span></span> <span data-ttu-id="b9fa3-293">Per l'autenticazione di base il valore deve essere `Basic`.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-293">For basic authentication, the value must be `Basic`.</span></span> |
| <span data-ttu-id="b9fa3-294">username</span><span class="sxs-lookup"><span data-stu-id="b9fa3-294">username</span></span> |<span data-ttu-id="b9fa3-295">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-295">Required.</span></span> <span data-ttu-id="b9fa3-296">Il nome utente per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="b9fa3-296">The username for authentication</span></span> |
| <span data-ttu-id="b9fa3-297">password</span><span class="sxs-lookup"><span data-stu-id="b9fa3-297">password</span></span> |<span data-ttu-id="b9fa3-298">Obbligatorio.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-298">Required.</span></span> <span data-ttu-id="b9fa3-299">La password per l'autenticazione</span><span class="sxs-lookup"><span data-stu-id="b9fa3-299">The password for authentication</span></span> |

<a name="azure-ad-code"></a>

#### <a name="azure-active-directory-authentication-through-code"></a><span data-ttu-id="b9fa3-300">Autenticazione di Azure Active Directory usando il codice</span><span class="sxs-lookup"><span data-stu-id="b9fa3-300">Azure Active Directory authentication through code</span></span>

<span data-ttu-id="b9fa3-301">Per impostazione predefinita, l'autenticazione di Azure AD che si attiva nel portale di Azure non offre un'autorizzazione con granularità fine.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-301">By default, the Azure AD authentication that you turn on in the Azure portal doesn't provide fine-grained authorization.</span></span> <span data-ttu-id="b9fa3-302">Ad esempio, questa autenticazione blocca l'API a un tenant specifico, non a un determinato utente o app.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-302">For example, this authentication locks your API to just a specific tenant, not to a specific user or app.</span></span> 

<span data-ttu-id="b9fa3-303">Per limitare l'accesso dell'API all'app per la logica usando il codice, estrarre l'intestazione che contiene il token JSON Web (JWT).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-303">To restrict API access to your logic app through code, extract the header that has the JSON web token (JWT).</span></span> <span data-ttu-id="b9fa3-304">Verificare l'identità del chiamante e rifiutare le richieste che non corrispondono.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-304">Check the caller's identity, and reject requests that don't match.</span></span>

<span data-ttu-id="b9fa3-305">Per approfondimenti su come implementare l'autenticazione interamente nel codice e non usare il Portale di Azure, vedere la procedura di [autenticazione con l'istanza locale di Active Directory nell'app Azure](../app-service-web/web-sites-authentication-authorization.md).</span><span class="sxs-lookup"><span data-stu-id="b9fa3-305">Going further, to implement this authentication entirely in your own code, and not use the Azure portal, learn how to [authenticate with on-premises Active Directory in your Azure app](../app-service-web/web-sites-authentication-authorization.md).</span></span>

<span data-ttu-id="b9fa3-306">È necessario seguire la procedura precedente per creare un'identità di applicazione per l'app per la logica e usarla per chiamare l'API.</span><span class="sxs-lookup"><span data-stu-id="b9fa3-306">To create an application identity for your logic app and use that identity to call your API, you must follow the previous steps.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9fa3-307">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9fa3-307">Next steps</span></span>

* [<span data-ttu-id="b9fa3-308">Controllare le prestazioni dell'app per la logica con avvisi e log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="b9fa3-308">Check logic app performance with diagnostic logs and alerts</span></span>](logic-apps-monitor-your-logic-apps.md)