---
title: aaaAzure AD Android introduzione | Documenti Microsoft
description: Come un'applicazione Android che si integra con Azure AD per l'accesso e le chiamate AD Azure toobuild protetto API tramite OAuth.
services: active-directory
documentationcenter: android
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: da1ee39f-89d3-4d36-96f1-4eabbc662343
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: mobile-android
ms.devlang: java
ms.topic: article
ms.date: 01/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 1aedc8ff60874b405a182a4ccbfb2c8b4d9d3704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="9b1c1-103">Integrare Azure AD in un'app per Android</span><span class="sxs-lookup"><span data-stu-id="9b1c1-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="9b1c1-104">Provare l'anteprima di hello delle nuove [portale per sviluppatori](https://identity.microsoft.com/Docs/Android), che consente di sfruttare in esecuzione in Azure AD in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-104">Try hello preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="9b1c1-105">portale per sviluppatori Hello assiste l'utente attraverso il processo di hello di registrazione di un'app e l'integrazione di Azure AD nel codice.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-105">hello developer portal will walk you through hello process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="9b1c1-106">Al termine si ottiene una semplice applicazione in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="9b1c1-107">Se si sta sviluppando un'applicazione desktop, Azure Active Directory (Azure AD) rende semplice e diretto per si tooauthenticate gli utenti con gli account di Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you tooauthenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="9b1c1-108">Consente inoltre l'applicazione toosecurely utilizzare qualsiasi web API protetta da Azure AD, ad esempio hello API di Office 365 o hello API di Azure.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-108">It also enables your application toosecurely consume any web API protected by Azure AD, such as hello Office 365 APIs or hello Azure API.</span></span>

<span data-ttu-id="9b1c1-109">Per i client Android che necessitano di risorse tooaccess protetto, Azure AD fornisce hello Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-109">For Android clients that need tooaccess protected resources, Azure AD provides hello Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="9b1c1-110">Hello unico scopo della libreria ADAL è toomake è più facile per i token di accesso tooget app.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-110">hello sole purpose of ADAL is toomake it easy for your app tooget access tokens.</span></span> <span data-ttu-id="9b1c1-111">toodemonstrate facilmente, verrà creata un'applicazione Android elenco di attività che:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-111">toodemonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="9b1c1-112">Ottiene i token per chiamare un'API di elenco attività da eseguire tramite hello di accesso [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-112">Gets access tokens for calling a To-Do List API by using hello [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="9b1c1-113">Ottiene l'elenco attività (To-Do List) dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="9b1c1-114">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-114">Signs out users.</span></span>

<span data-ttu-id="9b1c1-115">tooget avviato, è necessario un tenant di Azure Active Directory in cui è possibile creare utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-115">tooget started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="9b1c1-116">Se si dispone già di un tenant, [informazioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-116">If you don't already have a tenant, [learn how tooget one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-hello-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="9b1c1-117">Passaggio 1: Scaricare ed eseguire i server di esempio hello TODO API REST di Node.js</span><span class="sxs-lookup"><span data-stu-id="9b1c1-117">Step 1: Download and run hello Node.js REST API TODO sample server</span></span>
<span data-ttu-id="9b1c1-118">esempio Node.js REST API TODO Hello viene scritto in modo specifico toowork contro l'esempio esistente per la creazione di un tenant singolo API REST di attività da eseguire per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-118">hello Node.js REST API TODO sample is written specifically toowork against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="9b1c1-119">Questo è un prerequisito per l'avvio rapido hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-119">This is a prerequisite for hello Quick Start.</span></span>

<span data-ttu-id="9b1c1-120">Per informazioni su come tooset, vedere gli esempi esistenti in [servizio Microsoft Azure Active Directory esempio REST API per Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-120">For information on how tooset this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="9b1c1-121">Passaggio 2: Registrare l'API Web con il tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b1c1-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="9b1c1-122">Active Directory supporta l'aggiunta di due tipi di applicazioni:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="9b1c1-123">API che offrono servizi toousers Web</span><span class="sxs-lookup"><span data-stu-id="9b1c1-123">Web APIs that offer services toousers</span></span>
- <span data-ttu-id="9b1c1-124">Le API di applicazioni (in esecuzione sul web hello o in un dispositivo) che quelli di accesso web</span><span class="sxs-lookup"><span data-stu-id="9b1c1-124">Applications (running either on hello web or on a device) that access those web APIs</span></span>

<span data-ttu-id="9b1c1-125">In questo passaggio, si sta registrando l'API web hello in esecuzione in locale per test di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-125">In this step, you're registering hello web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="9b1c1-126">L'API web è in genere, un servizio REST che è una funzionalità offerta che si desidera tooaccess un'app.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-126">Normally, this web API is a REST service that's offering functionality that you want an app tooaccess.</span></span> <span data-ttu-id="9b1c1-127">Azure AD contribuisce alla protezione di qualsiasi endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="9b1c1-128">Si presuppone che si sta registrando hello API REST di attività a cui fa riferimento in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-128">We're assuming that you're registering hello TODO REST API referenced earlier.</span></span> <span data-ttu-id="9b1c1-129">Ma questo procedimento funziona per qualsiasi API web che si desidera proteggere toohelp Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-129">But this works for any web API that you want Azure Active Directory toohelp protect.</span></span>

1. <span data-ttu-id="9b1c1-130">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-130">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b1c1-131">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-131">On hello top bar, click your account.</span></span> <span data-ttu-id="9b1c1-132">In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-132">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="9b1c1-133">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-133">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9b1c1-134">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9b1c1-135">Immettere un nome descrittivo per l'applicazione hello (ad esempio, **TodoListService**), selezionare **applicazione Web e/o API Web**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-135">Enter a friendly name for hello application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="9b1c1-136">Per hello sign-on URL, immettere l'URL di base hello per esempio hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-136">For hello sign-on URL, enter hello base URL for hello sample.</span></span> <span data-ttu-id="9b1c1-137">Per impostazione predefinita, tale valore è `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="9b1c1-138">Fare clic su **OK** registrazione hello toocomplete.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-138">Click **OK** toocomplete hello registration.</span></span>
8. <span data-ttu-id="9b1c1-139">In hello portale di Azure, visitare tooyour pagina dell'applicazione, trovare il valore dell'ID applicazione hello e copiarlo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-139">While still in hello Azure portal, go tooyour application page, find hello application ID value, and copy it.</span></span> <span data-ttu-id="9b1c1-140">Servirà in un secondo momento durante la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="9b1c1-141">Da hello **impostazioni** -> **proprietà** pagina, aggiornare l'URI ID app hello - immettere `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-141">From hello **Settings** -> **Properties** page, update hello app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="9b1c1-142">Sostituire `<your_tenant_name>` con nome hello del tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-142">Replace `<your_tenant_name>` with hello name of your Azure AD tenant.</span></span>

## <a name="step-3-register-hello-sample-android-native-client-application"></a><span data-ttu-id="9b1c1-143">Passaggio 3: Registrare un'applicazione hello esempio Android Native Client</span><span class="sxs-lookup"><span data-stu-id="9b1c1-143">Step 3: Register hello sample Android Native Client application</span></span>
<span data-ttu-id="9b1c1-144">È necessario registrare l'applicazione Web in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-144">You must register your web application in this sample.</span></span> <span data-ttu-id="9b1c1-145">In questo modo toocommunicate l'applicazione con l'API web appena registrato hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-145">This allows your application toocommunicate with hello just-registered web API.</span></span> <span data-ttu-id="9b1c1-146">Azure AD rifiuterà tooeven consentire tooask l'applicazione per l'accesso a meno che non è registrato.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-146">Azure AD will refuse tooeven allow your application tooask for sign-in unless it's registered.</span></span> <span data-ttu-id="9b1c1-147">Che fa parte di sicurezza hello del modello di hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-147">That's part of hello security of hello model.</span></span>

<span data-ttu-id="9b1c1-148">Si presuppone che si sta registrando l'applicazione di esempio hello citata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-148">We're assuming that you're registering hello sample application referenced earlier.</span></span> <span data-ttu-id="9b1c1-149">ma questa procedura è applicabile a qualsiasi app in fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1c1-150">Si procede all'inserimento di un'applicazione e di un'API Web in un tenant,</span><span class="sxs-lookup"><span data-stu-id="9b1c1-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="9b1c1-151">perché è possibile compilare un'app che accede a un'API esterna registrata in Azure AD da un altro tenant.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="9b1c1-152">In questo caso, i clienti sarà richiesto di utilizzare toohello tooconsent di hello API in un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-152">If you do that, your customers will be prompted tooconsent toohello use of hello API in hello application.</span></span> <span data-ttu-id="9b1c1-153">Active Directory Authentication Library per iOS gestisce automaticamente la richiesta di consenso.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="9b1c1-154">Esplorare le funzionalità più avanzate, si noterà che si tratta di una parte importante della suite di hello lavoro tooaccess necessari hello di APIs di Microsoft Azure e Office, nonché qualsiasi altro provider di servizio.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-154">As we explore more advanced features, you'll see that this is an important part of hello work needed tooaccess hello suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="9b1c1-155">Per il momento, perché è stato registrato l'API web sia l'applicazione sottoposta a hello stesso tenant, non verrà visualizzata alcuna richiesta di consenso dell'utente.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-155">For now, because you registered both your web API and your application under hello same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="9b1c1-156">Ciò avviene in genere hello se si sta sviluppando un'applicazione solo per toouse la propria società.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-156">This is usually hello case if you're developing an application just for your own company toouse.</span></span>

1. <span data-ttu-id="9b1c1-157">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-157">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="9b1c1-158">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-158">On hello top bar, click your account.</span></span> <span data-ttu-id="9b1c1-159">In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-159">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="9b1c1-160">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-160">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="9b1c1-161">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="9b1c1-162">Immettere un nome descrittivo per l'applicazione hello (ad esempio, **TodoListClient Android**), selezionare **applicazione Client nativa**, fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-162">Enter a friendly name for hello application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="9b1c1-163">URI di reindirizzamento hello, immettere `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-163">For hello redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="9b1c1-164">Fare clic su **Finish**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-164">Click **Finish**.</span></span>
7. <span data-ttu-id="9b1c1-165">Dalla pagina dell'applicazione hello, trovare il valore dell'ID applicazione hello e copiarlo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-165">From hello application page, find hello application ID value and copy it.</span></span> <span data-ttu-id="9b1c1-166">Servirà in un secondo momento durante la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="9b1c1-167">Da hello **impostazioni** selezionare **autorizzazioni obbligatorie** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-167">From hello **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="9b1c1-168">Individuare e selezionare TodoListService, aggiungere hello **accesso TodoListService** autorizzazione in **autorizzazioni delegate**, fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-168">Locate and select TodoListService, add hello **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="9b1c1-169">toobuild con Maven, è possibile utilizzare pom.xml al primo livello hello:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-169">toobuild with Maven, you can use pom.xml at hello top level:</span></span>

1. <span data-ttu-id="9b1c1-170">Clonare il repository in una directory di propria scelta:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="9b1c1-171">Seguire i passaggi hello hello [tooset prerequisiti dell'ambiente di Maven per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-171">Follow hello steps in hello [prerequisites tooset up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="9b1c1-172">Configurare l'emulatore hello con SDK 19.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-172">Set up hello emulator with SDK 19.</span></span>
4. <span data-ttu-id="9b1c1-173">Passare cartella radice toohello in cui è stato clonato repository hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-173">Go toohello root folder where you cloned hello repo.</span></span>
5. <span data-ttu-id="9b1c1-174">Eseguire questo comando: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="9b1c1-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="9b1c1-175">Modificare hello directory toohello avvio rapido-esempio:`cd samples\hello`</span><span class="sxs-lookup"><span data-stu-id="9b1c1-175">Change hello directory toohello Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="9b1c1-176">Eseguire questo comando: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="9b1c1-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="9b1c1-177">Avvio dell'applicazione hello dovrebbe.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-177">You should see hello app starting.</span></span>
8. <span data-ttu-id="9b1c1-178">Immettere tootry le credenziali utente di test.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-178">Enter test user credentials tootry.</span></span>

<span data-ttu-id="9b1c1-179">Verranno inviati pacchetti JAR accanto pacchetto AAR hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-179">JAR packages will be submitted beside hello AAR package.</span></span>

## <a name="step-4-download-hello-android-adal-and-add-it-tooyour-eclipse-workspace"></a><span data-ttu-id="9b1c1-180">Passaggio 4: Scaricare Android ADAL hello e aggiungerlo come area di lavoro Eclipse tooyour</span><span class="sxs-lookup"><span data-stu-id="9b1c1-180">Step 4: Download hello Android ADAL and add it tooyour Eclipse workspace</span></span>
<span data-ttu-id="9b1c1-181">È stata semplificata per si toohave più opzioni toouse ADAL nel progetto Android:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-181">We've made it easy for you toohave multiple options toouse ADAL in your Android project:</span></span>

* <span data-ttu-id="9b1c1-182">È possibile utilizzare questa libreria tooimport di codice sorgente hello in applicazione tooyour Eclipse e collegamento.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-182">You can use hello source code tooimport this library into Eclipse and link tooyour application.</span></span>
* <span data-ttu-id="9b1c1-183">Se si usa Android Studio, è possibile utilizzare hello AAR pacchetto formato e riferimento hello i file binari.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-183">If you're using Android Studio, you can use hello AAR package format and reference hello binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="9b1c1-184">Opzione 1: Zip del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="9b1c1-184">Option 1: Source Zip</span></span>
<span data-ttu-id="9b1c1-185">Fare clic su una copia del codice sorgente hello, toodownload **ZIP di Download** hello destra della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-185">toodownload a copy of hello source code, click **Download ZIP** on hello right side of hello page.</span></span> <span data-ttu-id="9b1c1-186">In alternativa, [eseguire il download da GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="9b1c1-187">Opzione 2: Codice sorgente tramite Git</span><span class="sxs-lookup"><span data-stu-id="9b1c1-187">Option 2: Source via Git</span></span>
<span data-ttu-id="9b1c1-188">codice sorgente di hello tooget di hello SDK tramite Git, digitare:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-188">tooget hello source code of hello SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="9b1c1-189">Opzione 3: File binari tramite Gradle</span><span class="sxs-lookup"><span data-stu-id="9b1c1-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="9b1c1-190">È possibile ottenere i file binari hello dal repository centrale di Maven hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-190">You can get hello binaries from hello Maven central repo.</span></span> <span data-ttu-id="9b1c1-191">pacchetto AAR Hello può essere inclusi come indicato di seguito nel progetto in Android Studio:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-191">hello AAR package can be included as follows in your project in Android Studio:</span></span>

```gradle
repositories {
    mavenCentral()
    flatDir {
        dirs 'libs'
    }
    maven {
        url "YourLocalMavenRepoPath\\.m2\\repository"
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile('com.microsoft.aad:adal:1.1.1') {
        exclude group: 'com.android.support'
    } // Recent version is 1.1.1
}
```

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="9b1c1-192">Opzione 4: AAR tramite Maven</span><span class="sxs-lookup"><span data-stu-id="9b1c1-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="9b1c1-193">Se si usa hello M2Eclipse plug-in, è possibile specificare una dipendenza hello nel file pom.xml:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-193">If you're using hello M2Eclipse plug-in, you can specify hello dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-hello-libs-folder"></a><span data-ttu-id="9b1c1-194">Opzione 5: Pacchetto JAR cartella di librerie hello</span><span class="sxs-lookup"><span data-stu-id="9b1c1-194">Option 5: JAR package inside hello libs folder</span></span>
<span data-ttu-id="9b1c1-195">È possibile ottenere i file JAR hello dal repository di Maven hello e rilasciarlo hello **librerie** cartella nel progetto.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-195">You can get hello JAR file from hello Maven repo and drop it into hello **libs** folder in your project.</span></span> <span data-ttu-id="9b1c1-196">Progetto tooyour di toocopy hello risorse necessarie, è necessario perché i pacchetti hello JAR non li includono.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-196">You need toocopy hello required resources tooyour project as well, because hello JAR packages don't include them.</span></span>

## <a name="step-5-add-references-tooandroid-adal-tooyour-project"></a><span data-ttu-id="9b1c1-197">Passaggio 5: Aggiungere progetti tooyour ADAL tooAndroid di riferimenti</span><span class="sxs-lookup"><span data-stu-id="9b1c1-197">Step 5: Add references tooAndroid ADAL tooyour project</span></span>
1. <span data-ttu-id="9b1c1-198">Aggiungere un progetto di riferimento tooyour e specificarlo come una libreria Android.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-198">Add a reference tooyour project and specify it as an Android library.</span></span> <span data-ttu-id="9b1c1-199">Se non si è sicuri come toodo, è possibile ottenere ulteriori informazioni su hello [sito Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-199">If you're uncertain how toodo this, you can get more information on hello [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="9b1c1-200">Aggiungere una dipendenza di progetto hello per il debug nelle impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-200">Add hello project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="9b1c1-201">Aggiornare tooinclude di file AndroidManifest.xml del progetto:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-201">Update your project's AndroidManifest.xml file tooinclude:</span></span>

        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <application
            android:allowBackup="true"
            android:debuggable="true"
            android:icon="@drawable/ic_launcher"
            android:label="@string/app_name"
            android:theme="@style/AppTheme" >

            <activity
                android:name="com.microsoft.aad.adal.AuthenticationActivity"
                android:label="@string/title_login_hello_app" >
            </activity>
            ....
        <application/>

4. <span data-ttu-id="9b1c1-202">Creare un'istanza di AuthenticationContext nell'attività principale.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="9b1c1-203">Dettagli Hello di questa chiamata esulano dall'ambito di hello di questo argomento, ma è possibile ottenere un buon inizio esaminando hello [esempio Android Native Client](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-203">hello details of this call are beyond hello scope of this topic, but you can get a good start by looking at hello [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="9b1c1-204">Nell'esempio seguente di hello, SharedPreferences è cache predefinita hello e autorità è nel formato hello `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-204">In hello following example, SharedPreferences is hello default cache, and Authority is in hello form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="9b1c1-205">Copiare questo codice blocco toohandle hello fine AuthenticationActivity utente hello immette le credenziali e riceve un codice di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-205">Copy this code block toohandle hello end of AuthenticationActivity after hello user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="9b1c1-206">tooask per un token, definire un callback:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-206">tooask for a token, define a callback:</span></span>

        private AuthenticationCallback<AuthenticationResult> callback = new AuthenticationCallback<AuthenticationResult>() {

            @Override
            public void onError(Exception exc) {
                if (exc instanceof AuthenticationException) {
                    textViewStatus.setText("Cancelled");
                    Log.d(TAG, "Cancelled");
                } else {
                    textViewStatus.setText("Authentication error:" + exc.getMessage());
                    Log.d(TAG, "Authentication error:" + exc.getMessage());
                }
            }

            @Override
            public void onSuccess(AuthenticationResult result) {
                mResult = result;

                if (result == null || result.getAccessToken() == null
                        || result.getAccessToken().isEmpty()) {
                    textViewStatus.setText("Token is empty");
                    Log.d(TAG, "Token is empty");
                } else {
                    // request is successful
                    Log.d(TAG, "Status:" + result.getStatus() + " Expired:"
                            + result.getExpiresOn().toString());
                    textViewStatus.setText(PASSED);
                }
            }
        };

7. <span data-ttu-id="9b1c1-207">Infine, richiedere il token usando il callback:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="9b1c1-208">Di seguito è riportata una spiegazione dei parametri di hello:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-208">Here's an explanation of hello parameters:</span></span>

* <span data-ttu-id="9b1c1-209">*risorsa* è obbligatorio e si sta tentando di tooaccess di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-209">*resource* is required and is hello resource you're trying tooaccess.</span></span>
* <span data-ttu-id="9b1c1-210">*clientid* è obbligatorio e viene fornito da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="9b1c1-211">*RedirectUri* non è necessario toobe fornito per chiamata acquireToken hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-211">*RedirectUri* is not required toobe provided for hello acquireToken call.</span></span> <span data-ttu-id="9b1c1-212">È possibile configurarlo come nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="9b1c1-213">*PromptBehavior* consente tooask per cache di hello tooskip credenziali e i cookie.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-213">*PromptBehavior* helps tooask for credentials tooskip hello cache and cookie.</span></span>
* <span data-ttu-id="9b1c1-214">*callback* viene chiamato dopo che il codice di autorizzazione hello verrà scambiato per un token.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-214">*callback* is called after hello authorization code is exchanged for a token.</span></span> <span data-ttu-id="9b1c1-215">Ha un oggetto AuthenticationResult, che include un token di accesso, la data di scadenza e le informazioni sul token ID.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="9b1c1-216">*acquireTokenSilent* è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="9b1c1-217">È possibile chiamarlo toohandle la memorizzazione nella cache e l'aggiornamento del token.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-217">You can call it toohandle caching and token refresh.</span></span> <span data-ttu-id="9b1c1-218">Fornisce inoltre la versione di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-218">It also provides hello sync version.</span></span> <span data-ttu-id="9b1c1-219">Accetta *userId* come parametro.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="9b1c1-220">Tramite questa procedura dettagliata, è necessario quali è necessario integrare con Azure Active Directory toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-220">By using this walkthrough, you should have what you need toosuccessfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="9b1c1-221">Per ulteriori esempi di questo utilizzo, visitare hello AzureADSamples / repository in GitHub.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-221">For more examples of this working, visit hello AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="9b1c1-222">Informazioni importanti</span><span class="sxs-lookup"><span data-stu-id="9b1c1-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="9b1c1-223">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="9b1c1-223">Customization</span></span>
<span data-ttu-id="9b1c1-224">Le risorse dell'applicazione possono sovrascrivere le risorse del progetto di libreria.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="9b1c1-225">Ciò si verifica durante la compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-225">This happens when your app is being built.</span></span> <span data-ttu-id="9b1c1-226">Per questo motivo, è possibile personalizzare l'autenticazione attività layout hello desiderato.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-226">For this reason, you can customize authentication activity layout hello way you want.</span></span> <span data-ttu-id="9b1c1-227">ID di hello tookeep assicurarsi di controlli hello che ADAL Usa (WebView).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-227">Be sure tookeep hello ID of hello controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="9b1c1-228">Gestore</span><span class="sxs-lookup"><span data-stu-id="9b1c1-228">Broker</span></span>
<span data-ttu-id="9b1c1-229">app portale aziendale di Microsoft Intune Hello fornisce il componente di Service broker hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-229">hello Microsoft Intune Company Portal app provides hello broker component.</span></span> <span data-ttu-id="9b1c1-230">Hello account viene creato in ad AccountManager.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-230">hello account is created in AccountManager.</span></span> <span data-ttu-id="9b1c1-231">tipo di account di Hello è "workaccount".</span><span class="sxs-lookup"><span data-stu-id="9b1c1-231">hello account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="9b1c1-232">AccountManager consente solo un singolo account Single Sign-On (SSO).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="9b1c1-233">Crea un cookie SSO per utente hello dopo aver completato una sfida di dispositivo hello per una delle App hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-233">It creates an SSO cookie for hello user after completing hello device challenge for one of hello apps.</span></span>

<span data-ttu-id="9b1c1-234">Libreria ADAL Usa account di Service broker hello se viene creato un account utente in questo autenticatore e si sceglie di non tooskip è.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-234">ADAL uses hello broker account if one user account is created at this authenticator and you choose not tooskip it.</span></span> <span data-ttu-id="9b1c1-235">È possibile ignorare l'utente di Service broker hello con:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-235">You can skip hello broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="9b1c1-236">È necessario tooregister un RedirectUri speciali per l'utilizzo di Service broker.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-236">You need tooregister a special RedirectUri for broker usage.</span></span> <span data-ttu-id="9b1c1-237">Valore di RedirectUri è nel formato hello `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-237">RedirectUri is in hello format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="9b1c1-238">È possibile ottenere il valore di RedirectUri dell'App tramite brokerRedirectPrint.ps1 script hello o hello API chiamata mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-238">You can get your RedirectUri for your app by using hello script brokerRedirectPrint.ps1 or hello API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="9b1c1-239">firma di Hello è tooyour correlati i certificati di firma.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-239">hello signature is related tooyour signing certificates.</span></span>

<span data-ttu-id="9b1c1-240">modello broker corrente Hello è per un utente.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-240">hello current broker model is for one user.</span></span> <span data-ttu-id="9b1c1-241">AuthenticationContext consente hello API metodo tooget hello broker.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-241">AuthenticationContext provides hello API method tooget hello broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="9b1c1-242">Il manifesto dell'applicazione deve avere autorizzazioni toouse ad AccountManager account seguente hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-242">Your app manifest should have hello following permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="9b1c1-243">Per informazioni dettagliate, vedere hello [ad AccountManager informazioni sul sito Android hello](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-243">For details, see hello [AccountManager information on hello Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="9b1c1-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="9b1c1-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="9b1c1-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="9b1c1-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="9b1c1-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="9b1c1-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="9b1c1-247">URL dell'autorità e AD FS</span><span class="sxs-lookup"><span data-stu-id="9b1c1-247">Authority URL and AD FS</span></span>
<span data-ttu-id="9b1c1-248">Active Directory Federation Services (ADFS) non è riconosciuto come servizio token di sicurezza, di produzione, pertanto è necessario tooturn di individuazione di istanza e passare false nel costruttore AuthenticationContext hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need tooturn of instance discovery and pass false at hello AuthenticationContext constructor.</span></span>

<span data-ttu-id="9b1c1-249">URL dell'autorità Hello richiede un'istanza del servizio token di sicurezza e un [nome tenant](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-249">hello authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="9b1c1-250">Esecuzione di query sugli elementi della cache</span><span class="sxs-lookup"><span data-stu-id="9b1c1-250">Querying cache items</span></span>
<span data-ttu-id="9b1c1-251">ADAL fornisce una cache predefinita in SharedPrefrecens con alcune semplici funzioni di query nella cache.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="9b1c1-252">È possibile ottenere corrente cache di hello da AuthenticationContext utilizzando:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-252">You can get hello current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="9b1c1-253">È anche possibile fornire l'implementazione della cache, se si desidera toocustomize è.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-253">You can also provide your cache implementation, if you want toocustomize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="9b1c1-254">Comportamento della richiesta</span><span class="sxs-lookup"><span data-stu-id="9b1c1-254">Prompt behavior</span></span>
<span data-ttu-id="9b1c1-255">ADAL fornisce un comportamento dell'opzione toospecify prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-255">ADAL provides an option toospecify prompt behavior.</span></span> <span data-ttu-id="9b1c1-256">Se non è valido il token di aggiornamento hello e sono necessarie le credenziali utente, PromptBehavior.Auto visualizzerà hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-256">PromptBehavior.Auto will show hello UI if hello refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="9b1c1-257">PromptBehavior.Always ignorerà l'utilizzo della cache di hello e Mostra sempre hello dell'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-257">PromptBehavior.Always will skip hello cache usage and always show hello UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="9b1c1-258">Richiesta invisibile all'utente dei token dalla cache e aggiornamento</span><span class="sxs-lookup"><span data-stu-id="9b1c1-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="9b1c1-259">Una richiesta di token invisibile all'utente non usa hello popup dell'interfaccia utente e non richiede un'attività.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-259">A silent token request does not use hello UI pop-up and does not require an activity.</span></span> <span data-ttu-id="9b1c1-260">Restituisce un token dalla cache di hello, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-260">It returns a token from hello cache if available.</span></span> <span data-ttu-id="9b1c1-261">Se il token di hello è scaduto, questo metodo tenta toorefresh è.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-261">If hello token is expired, this method tries toorefresh it.</span></span> <span data-ttu-id="9b1c1-262">Se il token di aggiornamento hello è scaduto o non è riuscito, viene restituito AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-262">If hello refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="9b1c1-263">Con questo metodo è anche possibile effettuare una chiamata di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="9b1c1-264">È possibile impostare toocallback null o usare acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-264">You can set null toocallback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="9b1c1-265">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="9b1c1-265">Diagnostics</span></span>
<span data-ttu-id="9b1c1-266">Si tratta di fonti principali di hello di informazioni per la diagnosi dei problemi:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-266">These are hello primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="9b1c1-267">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="9b1c1-267">Exceptions</span></span>
* <span data-ttu-id="9b1c1-268">Log</span><span class="sxs-lookup"><span data-stu-id="9b1c1-268">Logs</span></span>
* <span data-ttu-id="9b1c1-269">Tracce di rete</span><span class="sxs-lookup"><span data-stu-id="9b1c1-269">Network traces</span></span>

<span data-ttu-id="9b1c1-270">Si noti che gli ID di correlazione sono diagnostica toohello centrale nella libreria hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-270">Note that correlation IDs are central toohello diagnostics in hello library.</span></span> <span data-ttu-id="9b1c1-271">Se si desidera toocorrelate un ADAL richiesta con altre operazioni nel codice, è possibile impostare l'ID di correlazione in base a una richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-271">You can set your correlation IDs on a per-request basis if you want toocorrelate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="9b1c1-272">Se non si imposta un ID di correlazione, ADAL genererà un valore casuale.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="9b1c1-273">Tutti i messaggi di log e chiamate di rete verranno quindi contrassegnate con l'ID di correlazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-273">All log messages and network calls will then be stamped with hello correlation ID.</span></span> <span data-ttu-id="9b1c1-274">modifiche ID generate automaticamente Hello in ciascuna richiesta.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-274">hello self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="9b1c1-275">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="9b1c1-275">Exceptions</span></span>
<span data-ttu-id="9b1c1-276">Le eccezioni sono hello innanzitutto diagnostica.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-276">Exceptions are hello first diagnostic.</span></span> <span data-ttu-id="9b1c1-277">Si tenta di tooprovide utili messaggi di errore.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-277">We try tooprovide helpful error messages.</span></span> <span data-ttu-id="9b1c1-278">ma se qualcuno non dovesse esserlo, registrare il problema e segnalarlo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="9b1c1-279">Includere le informazioni relative al dispositivo, ad esempio modello e numero di SDK.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="9b1c1-280">Log</span><span class="sxs-lookup"><span data-stu-id="9b1c1-280">Logs</span></span>
<span data-ttu-id="9b1c1-281">È possibile configurare hello libreria toogenerate messaggi di log che è possibile utilizzare toohelp diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-281">You can configure hello library toogenerate log messages that you can use toohelp diagnose issues.</span></span> <span data-ttu-id="9b1c1-282">Per configurare la registrazione, chiamata seguente hello tooconfigure un callback che ADAL utilizzerà toohand off ogni messaggio del log appena generato.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-282">You configure logging by making hello following call tooconfigure a callback that ADAL will use toohand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this toolog file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="9b1c1-283">I messaggi possono essere scritti tooa file di log personalizzato, come illustrato nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-283">Messages can be written tooa custom log file, as shown in hello following code.</span></span> <span data-ttu-id="9b1c1-284">Non esiste purtroppo un metodo standard per ottenere i log da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="9b1c1-285">A questo scopo, sono disponibili alcuni servizi che possono risultare utili.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-285">There are some services that can help you with this.</span></span> <span data-ttu-id="9b1c1-286">È anche possibile inventare personalizzati, ad esempio l'invio server tooa di file hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-286">You can also invent your own, such as sending hello file tooa server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="9b1c1-287">Questi sono i livelli di registrazione hello:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-287">These are hello logging levels:</span></span>
* <span data-ttu-id="9b1c1-288">Errore (eccezioni)</span><span class="sxs-lookup"><span data-stu-id="9b1c1-288">Error (exceptions)</span></span>
* <span data-ttu-id="9b1c1-289">Avviso (avviso)</span><span class="sxs-lookup"><span data-stu-id="9b1c1-289">Warn (warning)</span></span>
* <span data-ttu-id="9b1c1-290">Info (a scopo informativo)</span><span class="sxs-lookup"><span data-stu-id="9b1c1-290">Info (information purposes)</span></span>
* <span data-ttu-id="9b1c1-291">Dettagliato (altri dettagli)</span><span class="sxs-lookup"><span data-stu-id="9b1c1-291">Verbose (more details)</span></span>

<span data-ttu-id="9b1c1-292">Impostare il livello di registrazione hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-292">You set hello log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="9b1c1-293">Tutti i messaggi di log vengono inviati toologcat, nei callback di log personalizzato tooany aggiunta.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-293">All log messages are sent toologcat, in addition tooany custom log callbacks.</span></span>
<span data-ttu-id="9b1c1-294">È possibile ottenere un file di log tooa da logcat come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-294">You can get a log tooa file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="9b1c1-295">Per informazioni dettagliate sui comandi adb, vedere hello [logcat informazioni sul sito Android hello](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-295">For details about adb commands, see hello [logcat information on hello Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="9b1c1-296">Tracce di rete</span><span class="sxs-lookup"><span data-stu-id="9b1c1-296">Network traces</span></span>
<span data-ttu-id="9b1c1-297">È possibile utilizzare vari strumenti toocapture hello il traffico HTTP che genera l'errore ADAL.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-297">You can use various tools toocapture hello HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="9b1c1-298">Questo è particolarmente utile se si ha familiarità con il protocollo OAuth hello o se è necessario tooprovide informazioni di diagnostica tooMicrosoft o altri canali di supporto.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-298">This is most useful if you're familiar with hello OAuth protocol or if you need tooprovide diagnostic information tooMicrosoft or other support channels.</span></span>

<span data-ttu-id="9b1c1-299">Fiddler è uno strumento traccia HTTP estremamente semplice hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-299">Fiddler is hello easiest HTTP tracing tool.</span></span> <span data-ttu-id="9b1c1-300">Seguente hello utilizzare collegamenti tooset, configurarlo toocorrectly record ADAL traffico di rete.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-300">Use hello following links tooset it up toocorrectly record ADAL network traffic.</span></span> <span data-ttu-id="9b1c1-301">Per uno strumento di traccia come Fiddler o Charles toobe utile, è necessario configurare il traffico SSL toorecord non crittografato.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-301">For a tracing tool like Fiddler or Charles toobe useful, you must configure it toorecord unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="9b1c1-302">Le tracce generate in questo modo possono contenere informazioni con privilegi elevati, ad esempio token di accesso, nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="9b1c1-303">Se si usano account di produzione, non condividere queste tracce con terze parti.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="9b1c1-304">Se è necessario toosupply toosomeone una traccia in supporto tooget ordine, riprodurre il problema di hello utilizzando un account temporaneo con nomi utente e password che si desidera condividere.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-304">If you need toosupply a trace toosomeone in order tooget support, reproduce hello issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="9b1c1-305">Dal sito Web di Telerik hello: [impostazione backup Fiddler per Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span><span class="sxs-lookup"><span data-stu-id="9b1c1-305">From hello Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="9b1c1-306">Vedere [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler) (Configurare le regole di Fiddler per ADAL) in GitHub</span><span class="sxs-lookup"><span data-stu-id="9b1c1-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="9b1c1-307">Modalità della finestra di dialogo</span><span class="sxs-lookup"><span data-stu-id="9b1c1-307">Dialog mode</span></span>
<span data-ttu-id="9b1c1-308">metodo acquireToken Hello senza attività supporta un prompt dei comandi di finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-308">hello acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="9b1c1-309">Crittografia</span><span class="sxs-lookup"><span data-stu-id="9b1c1-309">Encryption</span></span>
<span data-ttu-id="9b1c1-310">ADAL crittografa i token hello e memorizzarlo in SharedPreferences per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-310">ADAL encrypts hello tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="9b1c1-311">È possibile esaminare i dettagli di hello toosee di hello StorageHelper classe.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-311">You can look at hello StorageHelper class toosee hello details.</span></span> <span data-ttu-id="9b1c1-312">Android ha introdotto Android Keystore 4.3 (API 18) per l'archiviazione protetta delle chiavi private.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="9b1c1-313">ADAL lo usa per API 18 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="9b1c1-314">Se si desidera toouse ADAL per le versioni precedenti di SDK, è necessario tooprovide una chiave segreta in AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-314">If you want toouse ADAL for lower SDK versions, you need tooprovide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="9b1c1-315">Richiesta di connessione di OAuth2</span><span class="sxs-lookup"><span data-stu-id="9b1c1-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="9b1c1-316">classe AuthenticationParameters Hello fornisce funzionalità tooget authorization_uri da hello OAuth2 richiesta di connessione.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-316">hello AuthenticationParameters class provides functionality tooget authorization_uri from hello OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="9b1c1-317">Cookie di sessione in WebView</span><span class="sxs-lookup"><span data-stu-id="9b1c1-317">Session cookies in WebView</span></span>
<span data-ttu-id="9b1c1-318">Android WebView non cancella i cookie di sessione si chiude l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-318">Android WebView does not clear session cookies after hello app is closed.</span></span> <span data-ttu-id="9b1c1-319">È possibile gestire questa operazione usando questo codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="9b1c1-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="9b1c1-320">Per informazioni dettagliate sui cookie, vedere hello [CookieSyncManager informazioni sul sito Android hello](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-320">For details about cookies, see hello [CookieSyncManager information on hello Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="9b1c1-321">Override delle risorse</span><span class="sxs-lookup"><span data-stu-id="9b1c1-321">Resource overrides</span></span>
<span data-ttu-id="9b1c1-322">libreria ADAL Hello include stringhe in inglese per i messaggi ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-322">hello ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="9b1c1-323">L'applicazione deve sovrascriverle, se si vogliono usare stringhe localizzate.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="9b1c1-324">Finestra di dialogo NTLM</span><span class="sxs-lookup"><span data-stu-id="9b1c1-324">NTLM dialog box</span></span>
<span data-ttu-id="9b1c1-325">Versione di ADAL 1.1.0 supporta una finestra di dialogo NTLM che viene elaborata tramite l'evento onReceivedHttpAuthRequest hello da WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through hello onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="9b1c1-326">È possibile personalizzare il layout di hello e stringhe per la finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="9b1c1-326">You can customize hello layout and strings for hello dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="9b1c1-327">Accesso Single Sign-On tra app</span><span class="sxs-lookup"><span data-stu-id="9b1c1-327">Cross-app SSO</span></span>
<span data-ttu-id="9b1c1-328">Informazioni su [come tooenable SSO tra app in Android tramite ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="9b1c1-328">Learn [how tooenable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
