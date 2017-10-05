---
title: Introduzione ad Android per Azure AD | Microsoft Docs
description: Come compilare un'applicazione Android che si integra con Azure AD per l'accesso e chiama le API protette di Azure AD usando OAuth.
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
ms.openlocfilehash: 746cad19093fd2a1ad23ddd9412394f8d9da331c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-into-an-android-app"></a><span data-ttu-id="07524-103">Integrare Azure AD in un'app per Android</span><span class="sxs-lookup"><span data-stu-id="07524-103">Integrate Azure AD into an Android app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

> [!TIP]
> <span data-ttu-id="07524-104">È consigliabile provare l'anteprima del nuovo [portale per sviluppatori](https://identity.microsoft.com/Docs/Android) che consentirà di imparare a usare Azure AD in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="07524-104">Try the preview of our new [developer portal](https://identity.microsoft.com/Docs/Android), which will help you get up and running with Azure AD in just a few minutes.</span></span> <span data-ttu-id="07524-105">Il portale per sviluppatori guida l'utente nel processo di registrazione di un'app e di integrazione di Azure AD nel codice.</span><span class="sxs-lookup"><span data-stu-id="07524-105">The developer portal will walk you through the process of registering an app and integrating Azure AD into your code.</span></span> <span data-ttu-id="07524-106">Al termine si ottiene una semplice applicazione in grado di autenticare gli utenti nel tenant e un back-end che può accettare i token ed eseguire la convalida.</span><span class="sxs-lookup"><span data-stu-id="07524-106">When you’re finished, you'll have a simple application that can authenticate users in your tenant and a back end that can accept tokens and perform validation.</span></span>
>
>

<span data-ttu-id="07524-107">Se si sta sviluppando un'applicazione desktop, Azure Active Directory (Azure AD) semplifica e facilita l'autenticazione degli utenti tramite gli account Active Directory locali.</span><span class="sxs-lookup"><span data-stu-id="07524-107">If you're developing a desktop application, Azure Active Directory (Azure AD) makes it simple and straightforward for you to authenticate your users by using their on-premises Active Directory accounts.</span></span> <span data-ttu-id="07524-108">Consente inoltre all'applicazione di usare in modo sicuro qualsiasi API Web protetta da Azure AD, ad esempio le API di Office 365 o l'API di Azure.</span><span class="sxs-lookup"><span data-stu-id="07524-108">It also enables your application to securely consume any web API protected by Azure AD, such as the Office 365 APIs or the Azure API.</span></span>

<span data-ttu-id="07524-109">Per i client Android che devono accedere a risorse protette, Azure AD fornisce Active Directory Authentication Library (ADAL).</span><span class="sxs-lookup"><span data-stu-id="07524-109">For Android clients that need to access protected resources, Azure AD provides the Active Directory Authentication Library (ADAL).</span></span> <span data-ttu-id="07524-110">La funzione di ADAL è di permettere all'app di ottenere facilmente i token di accesso.</span><span class="sxs-lookup"><span data-stu-id="07524-110">The sole purpose of ADAL is to make it easy for your app to get access tokens.</span></span> <span data-ttu-id="07524-111">Per illustrare la semplicità del processo, verrà compilata un'applicazione Android To-Do List che esegue le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="07524-111">To demonstrate how easy it is, we’ll build an Android To-Do List application that:</span></span>

* <span data-ttu-id="07524-112">Ottiene i token di accesso per la chiamata all'API To-Do List con il [protocollo di autenticazione OAuth 2.0](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span><span class="sxs-lookup"><span data-stu-id="07524-112">Gets access tokens for calling a To-Do List API by using the [OAuth 2.0 authentication protocol](https://msdn.microsoft.com/library/azure/dn645545.aspx).</span></span>
* <span data-ttu-id="07524-113">Ottiene l'elenco attività (To-Do List) dell'utente.</span><span class="sxs-lookup"><span data-stu-id="07524-113">Gets a user's to-do list.</span></span>
* <span data-ttu-id="07524-114">Disconnette gli utenti.</span><span class="sxs-lookup"><span data-stu-id="07524-114">Signs out users.</span></span>

<span data-ttu-id="07524-115">Per iniziare, è necessario un tenant di Azure AD in cui poter creare gli utenti e registrare un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-115">To get started, you need an Azure AD tenant in which you can create users and register an application.</span></span> <span data-ttu-id="07524-116">Se non si ha già un tenant, vedere le [informazioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="07524-116">If you don't already have a tenant, [learn how to get one](active-directory-howto-tenant.md).</span></span>

## <a name="step-1-download-and-run-the-nodejs-rest-api-todo-sample-server"></a><span data-ttu-id="07524-117">Passaggio 1: Scaricare ed eseguire il server di esempio dell'API REST TODO per Node.js</span><span class="sxs-lookup"><span data-stu-id="07524-117">Step 1: Download and run the Node.js REST API TODO sample server</span></span>
<span data-ttu-id="07524-118">L'esempio dell'API REST TODO per Node.js è scritto specificamente per funzionare con l'esempio esistente per la compilazione di una singola API REST To-Do del tenant per Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07524-118">The Node.js REST API TODO sample is written specifically to work against our existing sample for building a single-tenant To-Do REST API for Azure AD.</span></span> <span data-ttu-id="07524-119">Questo è un prerequisito per l'Avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="07524-119">This is a prerequisite for the Quick Start.</span></span>

<span data-ttu-id="07524-120">Per informazioni sulla procedura di configurazione di questa funzionalità, vedere gli esempi esistenti in [Servizio API REST di esempio per Microsoft Azure Active Directory per Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="07524-120">For information on how to set this up, see our existing samples in [Microsoft Azure Active Directory Sample REST API Service for Node.js](active-directory-devquickstarts-webapi-nodejs.md).</span></span>


## <a name="step-2-register-your-web-api-with-your-azure-ad-tenant"></a><span data-ttu-id="07524-121">Passaggio 2: Registrare l'API Web con il tenant di Azure AD</span><span class="sxs-lookup"><span data-stu-id="07524-121">Step 2: Register your web API with your Azure AD tenant</span></span>
<span data-ttu-id="07524-122">Active Directory supporta l'aggiunta di due tipi di applicazioni:</span><span class="sxs-lookup"><span data-stu-id="07524-122">Active Directory supports adding two types of applications:</span></span>

- <span data-ttu-id="07524-123">API Web che offre servizi agli utenti</span><span class="sxs-lookup"><span data-stu-id="07524-123">Web APIs that offer services to users</span></span>
- <span data-ttu-id="07524-124">Applicazioni, in esecuzione sul Web o in un dispositivo, che accedono a queste API Web</span><span class="sxs-lookup"><span data-stu-id="07524-124">Applications (running either on the web or on a device) that access those web APIs</span></span>

<span data-ttu-id="07524-125">In questo passaggio si registra l'API Web in esecuzione in locale per il test di questo esempio.</span><span class="sxs-lookup"><span data-stu-id="07524-125">In this step, you're registering the web API that you're running locally for testing this sample.</span></span> <span data-ttu-id="07524-126">In genere questa API Web è un servizio REST che offre le funzionalità a cui un'app deve accedere.</span><span class="sxs-lookup"><span data-stu-id="07524-126">Normally, this web API is a REST service that's offering functionality that you want an app to access.</span></span> <span data-ttu-id="07524-127">Azure AD contribuisce alla protezione di qualsiasi endpoint.</span><span class="sxs-lookup"><span data-stu-id="07524-127">Azure AD can help protect any endpoint.</span></span>

<span data-ttu-id="07524-128">Si presuppone che venga eseguita la registrazione dell'API REST TODO indicata in precedenza,</span><span class="sxs-lookup"><span data-stu-id="07524-128">We're assuming that you're registering the TODO REST API referenced earlier.</span></span> <span data-ttu-id="07524-129">ma questa procedura è applicabile a qualsiasi API Web che si vuole proteggere con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07524-129">But this works for any web API that you want Azure Active Directory to help protect.</span></span>

1. <span data-ttu-id="07524-130">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07524-130">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="07524-131">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="07524-131">On the top bar, click your account.</span></span> <span data-ttu-id="07524-132">Nell'elenco di **Directory** scegliere il tenant di Azure AD in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-132">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="07524-133">Fare clic su **More Services** (Altri servizi) nel riquadro sinistro, quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07524-133">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="07524-134">Fare clic su **Registrazioni per l'app**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07524-134">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="07524-135">Immettere un nome descrittivo per l'applicazione, ad esempio **TodoListService**, selezionare **Applicazione Web e/o API Web**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="07524-135">Enter a friendly name for the application (for example, **TodoListService**), select **Web Application and/or Web API**, and click **Next**.</span></span>
6. <span data-ttu-id="07524-136">Per l'URL di accesso immettere l'URL di base per l'esempio.</span><span class="sxs-lookup"><span data-stu-id="07524-136">For the sign-on URL, enter the base URL for the sample.</span></span> <span data-ttu-id="07524-137">Per impostazione predefinita, tale valore è `https://localhost:8080`.</span><span class="sxs-lookup"><span data-stu-id="07524-137">By default, this is `https://localhost:8080`.</span></span>
7. <span data-ttu-id="07524-138">Fare clic su **OK** per completare la registrazione.</span><span class="sxs-lookup"><span data-stu-id="07524-138">Click **OK** to complete the registration.</span></span>
8. <span data-ttu-id="07524-139">Nel portale di Azure passare alla pagina dell'applicazione, individuare il valore dell'ID applicazione e copiarlo.</span><span class="sxs-lookup"><span data-stu-id="07524-139">While still in the Azure portal, go to your application page, find the application ID value, and copy it.</span></span> <span data-ttu-id="07524-140">Servirà in un secondo momento durante la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-140">You'll need this later when configuring your application.</span></span>
9. <span data-ttu-id="07524-141">Dalla pagina **Impostazioni** -> **Proprietà** aggiornare l'URI dell'ID app. Immettere `https://<your_tenant_name>/TodoListService`.</span><span class="sxs-lookup"><span data-stu-id="07524-141">From the **Settings** -> **Properties** page, update the app ID URI - enter `https://<your_tenant_name>/TodoListService`.</span></span> <span data-ttu-id="07524-142">Sostituire `<your_tenant_name>` con il nome del tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07524-142">Replace `<your_tenant_name>` with the name of your Azure AD tenant.</span></span>

## <a name="step-3-register-the-sample-android-native-client-application"></a><span data-ttu-id="07524-143">Passaggio 3: Registrare l'applicazione client nativa Android di esempio</span><span class="sxs-lookup"><span data-stu-id="07524-143">Step 3: Register the sample Android Native Client application</span></span>
<span data-ttu-id="07524-144">È necessario registrare l'applicazione Web in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="07524-144">You must register your web application in this sample.</span></span> <span data-ttu-id="07524-145">In questo modo l'applicazione può comunicare con l'API Web appena registrata.</span><span class="sxs-lookup"><span data-stu-id="07524-145">This allows your application to communicate with the just-registered web API.</span></span> <span data-ttu-id="07524-146">Se l'applicazione non è registrata, Azure AD non le consentirà nemmeno di chiedere di effettuare l'accesso.</span><span class="sxs-lookup"><span data-stu-id="07524-146">Azure AD will refuse to even allow your application to ask for sign-in unless it's registered.</span></span> <span data-ttu-id="07524-147">Questo fa parte della sicurezza del modello.</span><span class="sxs-lookup"><span data-stu-id="07524-147">That's part of the security of the model.</span></span>

<span data-ttu-id="07524-148">Si presuppone che venga eseguita la registrazione dell'applicazione di esempio indicata in precedenza,</span><span class="sxs-lookup"><span data-stu-id="07524-148">We're assuming that you're registering the sample application referenced earlier.</span></span> <span data-ttu-id="07524-149">ma questa procedura è applicabile a qualsiasi app in fase di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="07524-149">But this procedure works for any app that you're developing.</span></span>

> [!NOTE]
> <span data-ttu-id="07524-150">Si procede all'inserimento di un'applicazione e di un'API Web in un tenant,</span><span class="sxs-lookup"><span data-stu-id="07524-150">You might wonder why you're putting both an application and a web API in one tenant.</span></span> <span data-ttu-id="07524-151">perché è possibile compilare un'app che accede a un'API esterna registrata in Azure AD da un altro tenant.</span><span class="sxs-lookup"><span data-stu-id="07524-151">As you might have guessed, you can build an app that accesses an external API that is registered in Azure AD from another tenant.</span></span> <span data-ttu-id="07524-152">In tal caso, ai clienti verrà richiesto di acconsentire all'uso dell'API nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-152">If you do that, your customers will be prompted to consent to the use of the API in the application.</span></span> <span data-ttu-id="07524-153">Active Directory Authentication Library per iOS gestisce automaticamente la richiesta di consenso.</span><span class="sxs-lookup"><span data-stu-id="07524-153">Active Directory Authentication Library for iOS takes care of this consent for you.</span></span> <span data-ttu-id="07524-154">Iniziando a esaminare funzionalità più avanzate, si può immaginare come questa sia una parte importante del lavoro necessario per accedere alla gamma di API Microsoft da Azure e da Office, oltre che da altri provider di servizi.</span><span class="sxs-lookup"><span data-stu-id="07524-154">As we explore more advanced features, you'll see that this is an important part of the work needed to access the suite of Microsoft APIs from Azure and Office, as well as any other service provider.</span></span> <span data-ttu-id="07524-155">Per ora, poiché sia l'API Web che l'applicazione sono state registrate nello stesso tenant, non verrà visualizzata alcuna richiesta di consenso.</span><span class="sxs-lookup"><span data-stu-id="07524-155">For now, because you registered both your web API and your application under the same tenant, you won't see any prompts for consent.</span></span> <span data-ttu-id="07524-156">Di solito ciò avviene se si sta sviluppando un'applicazione che verrà usata solo in azienda.</span><span class="sxs-lookup"><span data-stu-id="07524-156">This is usually the case if you're developing an application just for your own company to use.</span></span>

1. <span data-ttu-id="07524-157">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07524-157">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="07524-158">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="07524-158">On the top bar, click your account.</span></span> <span data-ttu-id="07524-159">Nell'elenco di **Directory** scegliere il tenant di Azure AD in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-159">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="07524-160">Fare clic su **More Services** (Altri servizi) nel riquadro sinistro, quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="07524-160">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="07524-161">Fare clic su **Registrazioni per l'app**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07524-161">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="07524-162">Immettere un nome descrittivo per l'applicazione, ad esempio **TodoListClient-Android**, selezionare **Applicazione client nativa**, quindi fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="07524-162">Enter a friendly name for the application (for example, **TodoListClient-Android**), select **Native Client Application**, and click **Next**.</span></span>
6. <span data-ttu-id="07524-163">Per l'URI di reindirizzamento, immettere `http://TodoListClient`.</span><span class="sxs-lookup"><span data-stu-id="07524-163">For the redirect URI, enter `http://TodoListClient`.</span></span> <span data-ttu-id="07524-164">Fare clic su **Fine**.</span><span class="sxs-lookup"><span data-stu-id="07524-164">Click **Finish**.</span></span>
7. <span data-ttu-id="07524-165">Nella pagina dell'applicazione trovare il valore dell'ID applicazione e copiarlo.</span><span class="sxs-lookup"><span data-stu-id="07524-165">From the application page, find the application ID value and copy it.</span></span> <span data-ttu-id="07524-166">Servirà in un secondo momento durante la configurazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-166">You'll need this later when configuring your application.</span></span>
8. <span data-ttu-id="07524-167">Nella pagina **Impostazioni** selezionare **Autorizzazioni necessarie** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="07524-167">From the **Settings** page, select **Required Permissions** and select **Add**.</span></span>  <span data-ttu-id="07524-168">Individuare e selezionare TodoListService, aggiungere l'autorizzazione di **Access TodoListService** in **Autorizzazioni delegate** e fare clic su **Operazione completata**.</span><span class="sxs-lookup"><span data-stu-id="07524-168">Locate and select TodoListService, add the **Access TodoListService** permission under **Delegated Permissions**, and click **Done**.</span></span>

<span data-ttu-id="07524-169">Per compilare con Maven, è possibile usare pom.xml al livello principale:</span><span class="sxs-lookup"><span data-stu-id="07524-169">To build with Maven, you can use pom.xml at the top level:</span></span>

1. <span data-ttu-id="07524-170">Clonare il repository in una directory di propria scelta:</span><span class="sxs-lookup"><span data-stu-id="07524-170">Clone this repo into a directory of your choice:</span></span>

  `$ git clone git@github.com:AzureADSamples/NativeClient-Android.git`  
2. <span data-ttu-id="07524-171">Seguire la procedura illustrata nei [prerequisiti per la configurazione dell'ambiente Maven per Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span><span class="sxs-lookup"><span data-stu-id="07524-171">Follow the steps in the [prerequisites to set up your Maven environment for Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android/wiki/Setting-up-maven-environment-for-Android).</span></span>
3. <span data-ttu-id="07524-172">Configurare l'emulatore con SDK 19.</span><span class="sxs-lookup"><span data-stu-id="07524-172">Set up the emulator with SDK 19.</span></span>
4. <span data-ttu-id="07524-173">Passare alla cartella radice in cui è stato clonato il repository.</span><span class="sxs-lookup"><span data-stu-id="07524-173">Go to the root folder where you cloned the repo.</span></span>
5. <span data-ttu-id="07524-174">Eseguire questo comando: `mvn clean install`</span><span class="sxs-lookup"><span data-stu-id="07524-174">Run this command: `mvn clean install`</span></span>
6. <span data-ttu-id="07524-175">Passare alla directory dell'esempio di Avvio rapido: `cd samples\hello`.</span><span class="sxs-lookup"><span data-stu-id="07524-175">Change the directory to the Quick Start sample: `cd samples\hello`</span></span>
7. <span data-ttu-id="07524-176">Eseguire questo comando: `mvn android:deploy android:run`</span><span class="sxs-lookup"><span data-stu-id="07524-176">Run this command: `mvn android:deploy android:run`</span></span>

   <span data-ttu-id="07524-177">Dovrebbe essere visualizzato l'avvio dell'app.</span><span class="sxs-lookup"><span data-stu-id="07524-177">You should see the app starting.</span></span>
8. <span data-ttu-id="07524-178">Immettere le credenziali dell'utente test per provare.</span><span class="sxs-lookup"><span data-stu-id="07524-178">Enter test user credentials to try.</span></span>

<span data-ttu-id="07524-179">Oltre al pacchetto AAR, verranno inviati i pacchetti JAR.</span><span class="sxs-lookup"><span data-stu-id="07524-179">JAR packages will be submitted beside the AAR package.</span></span>

## <a name="step-4-download-the-android-adal-and-add-it-to-your-eclipse-workspace"></a><span data-ttu-id="07524-180">Passaggio 4: Scaricare ADAL per Android e aggiungerlo all'area di lavoro di Eclipse</span><span class="sxs-lookup"><span data-stu-id="07524-180">Step 4: Download the Android ADAL and add it to your Eclipse workspace</span></span>
<span data-ttu-id="07524-181">Per semplificare l'operazione, sono disponibili più opzioni per usare ADAL nel progetto Android:</span><span class="sxs-lookup"><span data-stu-id="07524-181">We've made it easy for you to have multiple options to use ADAL in your Android project:</span></span>

* <span data-ttu-id="07524-182">È possibile usare il codice sorgente per importare la libreria in Eclipse e collegarla all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="07524-182">You can use the source code to import this library into Eclipse and link to your application.</span></span>
* <span data-ttu-id="07524-183">Se si usa Android Studio, è possibile usare il formato di pacchetto AAR e fare riferimento ai file binari.</span><span class="sxs-lookup"><span data-stu-id="07524-183">If you're using Android Studio, you can use the AAR package format and reference the binaries.</span></span>

### <a name="option-1-source-zip"></a><span data-ttu-id="07524-184">Opzione 1: Zip del codice sorgente</span><span class="sxs-lookup"><span data-stu-id="07524-184">Option 1: Source Zip</span></span>
<span data-ttu-id="07524-185">Per scaricare una copia del codice sorgente, fare clic su **Download ZIP** (Scarica ZIP) nel lato destro della pagina.</span><span class="sxs-lookup"><span data-stu-id="07524-185">To download a copy of the source code, click **Download ZIP** on the right side of the page.</span></span> <span data-ttu-id="07524-186">In alternativa, [eseguire il download da GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span><span class="sxs-lookup"><span data-stu-id="07524-186">Or you can [download from GitHub](https://github.com/AzureAD/azure-activedirectory-library-for-android/archive/v1.0.9.tar.gz).</span></span>

### <a name="option-2-source-via-git"></a><span data-ttu-id="07524-187">Opzione 2: Codice sorgente tramite Git</span><span class="sxs-lookup"><span data-stu-id="07524-187">Option 2: Source via Git</span></span>
<span data-ttu-id="07524-188">Per ottenere il codice sorgente dell'SDK tramite Git, digitare:</span><span class="sxs-lookup"><span data-stu-id="07524-188">To get the source code of the SDK via Git, type:</span></span>

    git clone git@github.com:AzureAD/azure-activedirectory-library-for-android.git
    cd ./azure-activedirectory-library-for-android/src

### <a name="option-3-binaries-via-gradle"></a><span data-ttu-id="07524-189">Opzione 3: File binari tramite Gradle</span><span class="sxs-lookup"><span data-stu-id="07524-189">Option 3: Binaries via Gradle</span></span>
<span data-ttu-id="07524-190">È possibile ottenere i file binari dal repository centrale di Maven.</span><span class="sxs-lookup"><span data-stu-id="07524-190">You can get the binaries from the Maven central repo.</span></span> <span data-ttu-id="07524-191">Il pacchetto AAR può essere incluso come segue nel progetto in Android Studio:</span><span class="sxs-lookup"><span data-stu-id="07524-191">The AAR package can be included as follows in your project in Android Studio:</span></span>

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

### <a name="option-4-aar-via-maven"></a><span data-ttu-id="07524-192">Opzione 4: AAR tramite Maven</span><span class="sxs-lookup"><span data-stu-id="07524-192">Option 4: AAR via Maven</span></span>
<span data-ttu-id="07524-193">Se si usa il plug-in M2Eclipse, è possibile specificare la dipendenza nel file pom.xml:</span><span class="sxs-lookup"><span data-stu-id="07524-193">If you're using the M2Eclipse plug-in, you can specify the dependency in your pom.xml file:</span></span>

```xml
<dependency>
    <groupId>com.microsoft.aad</groupId>
    <artifactId>adal</artifactId>
    <version>1.1.1</version>
    <type>aar</type>
</dependency>
```


### <a name="option-5-jar-package-inside-the-libs-folder"></a><span data-ttu-id="07524-194">Opzione 5: Pacchetto JAR nella cartella libs</span><span class="sxs-lookup"><span data-stu-id="07524-194">Option 5: JAR package inside the libs folder</span></span>
<span data-ttu-id="07524-195">È possibile ottenere il file JAR dal repository Maven e inserirlo nella cartella **libs** del progetto.</span><span class="sxs-lookup"><span data-stu-id="07524-195">You can get the JAR file from the Maven repo and drop it into the **libs** folder in your project.</span></span> <span data-ttu-id="07524-196">È necessario copiare anche le risorse necessarie per il progetto, perché non sono incluse nei pacchetti JAR.</span><span class="sxs-lookup"><span data-stu-id="07524-196">You need to copy the required resources to your project as well, because the JAR packages don't include them.</span></span>

## <a name="step-5-add-references-to-android-adal-to-your-project"></a><span data-ttu-id="07524-197">Passaggio 5: Aggiungere i riferimenti ad ADAL per Android nel progetto</span><span class="sxs-lookup"><span data-stu-id="07524-197">Step 5: Add references to Android ADAL to your project</span></span>
1. <span data-ttu-id="07524-198">Aggiungere un riferimento al progetto e specificarlo come una libreria Android.</span><span class="sxs-lookup"><span data-stu-id="07524-198">Add a reference to your project and specify it as an Android library.</span></span> <span data-ttu-id="07524-199">In caso di dubbi su questa operazione, è possibile ottenere altre informazioni nel [sito Android Studio](http://developer.android.com/tools/projects/projects-eclipse.html).</span><span class="sxs-lookup"><span data-stu-id="07524-199">If you're uncertain how to do this, you can get more information on the [Android Studio site](http://developer.android.com/tools/projects/projects-eclipse.html).</span></span>
2. <span data-ttu-id="07524-200">Aggiungere la dipendenza del progetto per il debug alle impostazioni del progetto.</span><span class="sxs-lookup"><span data-stu-id="07524-200">Add the project dependency for debugging into your project settings.</span></span>
3. <span data-ttu-id="07524-201">Aggiornare il file AndroidManifest.xml del progetto includendo:</span><span class="sxs-lookup"><span data-stu-id="07524-201">Update your project's AndroidManifest.xml file to include:</span></span>

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

4. <span data-ttu-id="07524-202">Creare un'istanza di AuthenticationContext nell'attività principale.</span><span class="sxs-lookup"><span data-stu-id="07524-202">Create an instance of AuthenticationContext at your main activity.</span></span> <span data-ttu-id="07524-203">I dettagli di questa chiamata non rientrano dell'ambito di questo argomento, ma come punto di partenza è possibile vedere l'[esempio relativo al client nativo Android](https://github.com/AzureADSamples/NativeClient-Android).</span><span class="sxs-lookup"><span data-stu-id="07524-203">The details of this call are beyond the scope of this topic, but you can get a good start by looking at the [Android Native Client sample](https://github.com/AzureADSamples/NativeClient-Android).</span></span> <span data-ttu-id="07524-204">Nell'esempio seguente SharedPreferences è la cache predefinita e il formato di Authority è `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span><span class="sxs-lookup"><span data-stu-id="07524-204">In the following example, SharedPreferences is the default cache, and Authority is in the form of `https://login.microsoftonline.com/yourtenant.onmicrosoft.com`:</span></span>

    `mContext = new AuthenticationContext(MainActivity.this, authority, true); // mContext is a field in your activity`

5. <span data-ttu-id="07524-205">Copiare il blocco di codice per gestire la fine di AuthenticationActivity dopo che l'utente ha immesso le credenziali e ricevuto un codice di autorizzazione:</span><span class="sxs-lookup"><span data-stu-id="07524-205">Copy this code block to handle the end of AuthenticationActivity after the user enters credentials and receives an authorization code:</span></span>

        @Override
         protected void onActivityResult(int requestCode, int resultCode, Intent data) {
             super.onActivityResult(requestCode, resultCode, data);
             if (mContext != null) {
                mContext.onActivityResult(requestCode, resultCode, data);
             }
         }

6. <span data-ttu-id="07524-206">Per richiedere un token, definire un callback:</span><span class="sxs-lookup"><span data-stu-id="07524-206">To ask for a token, define a callback:</span></span>

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

7. <span data-ttu-id="07524-207">Infine, richiedere il token usando il callback:</span><span class="sxs-lookup"><span data-stu-id="07524-207">Finally, ask for a token by using that callback:</span></span>

    `mContext.acquireToken(MainActivity.this, resource, clientId, redirect, user_loginhint, PromptBehavior.Auto, "",
                   callback);`

<span data-ttu-id="07524-208">Ecco una descrizione dei parametri:</span><span class="sxs-lookup"><span data-stu-id="07524-208">Here's an explanation of the parameters:</span></span>

* <span data-ttu-id="07524-209">*resource* è obbligatorio ed è la risorsa a cui si sta tentando di accedere.</span><span class="sxs-lookup"><span data-stu-id="07524-209">*resource* is required and is the resource you're trying to access.</span></span>
* <span data-ttu-id="07524-210">*clientid* è obbligatorio e viene fornito da Azure AD.</span><span class="sxs-lookup"><span data-stu-id="07524-210">*clientid* is required and comes from Azure AD.</span></span>
* <span data-ttu-id="07524-211">*RedirectUri* non è obbligatorio specificarlo per la chiamata acquireToken.</span><span class="sxs-lookup"><span data-stu-id="07524-211">*RedirectUri* is not required to be provided for the acquireToken call.</span></span> <span data-ttu-id="07524-212">È possibile configurarlo come nome del pacchetto.</span><span class="sxs-lookup"><span data-stu-id="07524-212">You can set it up as your package name.</span></span>
* <span data-ttu-id="07524-213">*PromptBehavior* facilita la richiesta delle credenziali per ignorare cache e cookie.</span><span class="sxs-lookup"><span data-stu-id="07524-213">*PromptBehavior* helps to ask for credentials to skip the cache and cookie.</span></span>
* <span data-ttu-id="07524-214">*callback* viene chiamato dopo lo scambio del codice di autorizzazione con un token.</span><span class="sxs-lookup"><span data-stu-id="07524-214">*callback* is called after the authorization code is exchanged for a token.</span></span> <span data-ttu-id="07524-215">Ha un oggetto AuthenticationResult, che include un token di accesso, la data di scadenza e le informazioni sul token ID.</span><span class="sxs-lookup"><span data-stu-id="07524-215">It has an object of AuthenticationResult, which has access token, date expired, and ID token information.</span></span>
* <span data-ttu-id="07524-216">*acquireTokenSilent* è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="07524-216">*acquireTokenSilent* is optional.</span></span> <span data-ttu-id="07524-217">È possibile chiamarlo per gestire la memorizzazione nella cache e l'aggiornamento del token.</span><span class="sxs-lookup"><span data-stu-id="07524-217">You can call it to handle caching and token refresh.</span></span> <span data-ttu-id="07524-218">Fornisce anche la versione di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="07524-218">It also provides the sync version.</span></span> <span data-ttu-id="07524-219">Accetta *userId* come parametro.</span><span class="sxs-lookup"><span data-stu-id="07524-219">It accepts *userId* as a parameter.</span></span>

        mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="07524-220">Tramite questa procedura dettagliata si dovrebbero avere tutte le informazioni necessarie per una corretta integrazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="07524-220">By using this walkthrough, you should have what you need to successfully integrate with Azure Active Directory.</span></span> <span data-ttu-id="07524-221">Per altre informazioni sull'esecuzione di queste operazioni, visitare il repository AzureADSamples/ su GitHub.</span><span class="sxs-lookup"><span data-stu-id="07524-221">For more examples of this working, visit the AzureADSamples/ repository on GitHub.</span></span>

## <a name="important-information"></a><span data-ttu-id="07524-222">Informazioni importanti</span><span class="sxs-lookup"><span data-stu-id="07524-222">Important information</span></span>
### <a name="customization"></a><span data-ttu-id="07524-223">Personalizzazione</span><span class="sxs-lookup"><span data-stu-id="07524-223">Customization</span></span>
<span data-ttu-id="07524-224">Le risorse dell'applicazione possono sovrascrivere le risorse del progetto di libreria.</span><span class="sxs-lookup"><span data-stu-id="07524-224">Your application resources can overwrite library project resources.</span></span> <span data-ttu-id="07524-225">Ciò si verifica durante la compilazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="07524-225">This happens when your app is being built.</span></span> <span data-ttu-id="07524-226">Per questo motivo, è possibile personalizzare il layout dell'attività di autenticazione come si preferisce.</span><span class="sxs-lookup"><span data-stu-id="07524-226">For this reason, you can customize authentication activity layout the way you want.</span></span> <span data-ttu-id="07524-227">È necessario accertarsi che venga mantenuto l'ID dei controlli usati da ADAL (Webview).</span><span class="sxs-lookup"><span data-stu-id="07524-227">Be sure to keep the ID of the controls that ADAL uses (WebView).</span></span>

### <a name="broker"></a><span data-ttu-id="07524-228">Gestore</span><span class="sxs-lookup"><span data-stu-id="07524-228">Broker</span></span>
<span data-ttu-id="07524-229">L'app Portale aziendale di Microsoft Intune fornisce il componente broker.</span><span class="sxs-lookup"><span data-stu-id="07524-229">The Microsoft Intune Company Portal app provides the broker component.</span></span> <span data-ttu-id="07524-230">L'account viene creato in AccountManager.</span><span class="sxs-lookup"><span data-stu-id="07524-230">The account is created in AccountManager.</span></span> <span data-ttu-id="07524-231">Il tipo di account è "com.microsoft.workaccount".</span><span class="sxs-lookup"><span data-stu-id="07524-231">The account type is "com.microsoft.workaccount."</span></span> <span data-ttu-id="07524-232">AccountManager consente solo un singolo account Single Sign-On (SSO).</span><span class="sxs-lookup"><span data-stu-id="07524-232">AccountManager allows only a single SSO account.</span></span> <span data-ttu-id="07524-233">Dopo il completamento della richiesta di verifica del dispositivo per una delle app, viene creato un cookie SSO per questo utente.</span><span class="sxs-lookup"><span data-stu-id="07524-233">It creates an SSO cookie for the user after completing the device challenge for one of the apps.</span></span>

<span data-ttu-id="07524-234">ADAL usa l'account broker, se è stato creato un account utente per questo autenticatore e si è scelto di non ignorarlo.</span><span class="sxs-lookup"><span data-stu-id="07524-234">ADAL uses the broker account if one user account is created at this authenticator and you choose not to skip it.</span></span> <span data-ttu-id="07524-235">È possibile ignorare l'utente broker usando:</span><span class="sxs-lookup"><span data-stu-id="07524-235">You can skip the broker user with:</span></span>

   `AuthenticationSettings.Instance.setSkipBroker(true);`

<span data-ttu-id="07524-236">È necessario registrare un URI di reindirizzamento speciale per l'utilizzo da parte del broker.</span><span class="sxs-lookup"><span data-stu-id="07524-236">You need to register a special RedirectUri for broker usage.</span></span> <span data-ttu-id="07524-237">L'URI di reindirizzamento è nel formato `msauth://packagename/Base64UrlencodedSignature`.</span><span class="sxs-lookup"><span data-stu-id="07524-237">RedirectUri is in the format of `msauth://packagename/Base64UrlencodedSignature`.</span></span> <span data-ttu-id="07524-238">È possibile ottenere l'URI di reindirizzamento per l'app usando lo script brokerRedirectPrint.ps1 o la chiamata API mContext.getBrokerRedirectUri.</span><span class="sxs-lookup"><span data-stu-id="07524-238">You can get your RedirectUri for your app by using the script brokerRedirectPrint.ps1 or the API call mContext.getBrokerRedirectUri.</span></span> <span data-ttu-id="07524-239">La firma è correlata ai certificati di firma.</span><span class="sxs-lookup"><span data-stu-id="07524-239">The signature is related to your signing certificates.</span></span>

<span data-ttu-id="07524-240">Il modello di broker attuale è per un solo utente.</span><span class="sxs-lookup"><span data-stu-id="07524-240">The current broker model is for one user.</span></span> <span data-ttu-id="07524-241">AuthenticationContext fornisce il metodo API per ottenere l'utente broker.</span><span class="sxs-lookup"><span data-stu-id="07524-241">AuthenticationContext provides the API method to get the broker user.</span></span>

   `String brokerAccount =  mContext.getBrokerUser(); //Broker user is returned if account is valid.`

<span data-ttu-id="07524-242">Il manifesto dell'app deve avere le autorizzazioni seguenti per usare gli account di AccountManager.</span><span class="sxs-lookup"><span data-stu-id="07524-242">Your app manifest should have the following permissions to use AccountManager accounts.</span></span> <span data-ttu-id="07524-243">Per informazioni dettagliate, vedere le [Informazioni su AccountManager nel sito Android](http://developer.android.com/reference/android/accounts/AccountManager.html).</span><span class="sxs-lookup"><span data-stu-id="07524-243">For details, see the [AccountManager information on the Android site](http://developer.android.com/reference/android/accounts/AccountManager.html).</span></span>

* <span data-ttu-id="07524-244">GET_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="07524-244">GET_ACCOUNTS</span></span>
* <span data-ttu-id="07524-245">USE_CREDENTIALS</span><span class="sxs-lookup"><span data-stu-id="07524-245">USE_CREDENTIALS</span></span>
* <span data-ttu-id="07524-246">MANAGE_ACCOUNTS</span><span class="sxs-lookup"><span data-stu-id="07524-246">MANAGE_ACCOUNTS</span></span>

### <a name="authority-url-and-ad-fs"></a><span data-ttu-id="07524-247">URL dell'autorità e AD FS</span><span class="sxs-lookup"><span data-stu-id="07524-247">Authority URL and AD FS</span></span>
<span data-ttu-id="07524-248">Active Directory Federation Services (AD FS) non è riconosciuto come servizio token di sicurezza di produzione, quindi è necessario disattivare l'individuazione dell'istanza e passare false al costruttore AuthenticationContext.</span><span class="sxs-lookup"><span data-stu-id="07524-248">Active Directory Federation Services (AD FS) is not recognized as production STS, so you need to turn of instance discovery and pass false at the AuthenticationContext constructor.</span></span>

<span data-ttu-id="07524-249">L'URL dell'autorità richiede un'istanza del servizio token di sicurezza e il nome del [tenant](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span><span class="sxs-lookup"><span data-stu-id="07524-249">The authority URL needs an STS instance and a [tenant name](https://login.microsoftonline.com/yourtenant.onmicrosoft.com).</span></span>

### <a name="querying-cache-items"></a><span data-ttu-id="07524-250">Esecuzione di query sugli elementi della cache</span><span class="sxs-lookup"><span data-stu-id="07524-250">Querying cache items</span></span>
<span data-ttu-id="07524-251">ADAL fornisce una cache predefinita in SharedPrefrecens con alcune semplici funzioni di query nella cache.</span><span class="sxs-lookup"><span data-stu-id="07524-251">ADAL provides a default cache in SharedPreferences with some simple cache query functions.</span></span> <span data-ttu-id="07524-252">È possibile ottenere la cache corrente da AuthenticationContext con:</span><span class="sxs-lookup"><span data-stu-id="07524-252">You can get the current cache from AuthenticationContext by using:</span></span>

    ITokenCacheStore cache = mContext.getCache();

<span data-ttu-id="07524-253">È anche possibile fornire l'implementazione della cache, se si desidera personalizzarla.</span><span class="sxs-lookup"><span data-stu-id="07524-253">You can also provide your cache implementation, if you want to customize it.</span></span>

    mContext = new AuthenticationContext(MainActivity.this, authority, true, yourCache);

### <a name="prompt-behavior"></a><span data-ttu-id="07524-254">Comportamento della richiesta</span><span class="sxs-lookup"><span data-stu-id="07524-254">Prompt behavior</span></span>
<span data-ttu-id="07524-255">ADAL include un'opzione per specificare il comportamento delle richieste.</span><span class="sxs-lookup"><span data-stu-id="07524-255">ADAL provides an option to specify prompt behavior.</span></span> <span data-ttu-id="07524-256">Se il token di aggiornamento non è valido e sono richieste le credenziali utente, PromptBehavior.Auto visualizzerà l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="07524-256">PromptBehavior.Auto will show the UI if the refresh token is invalid and user credentials are required.</span></span> <span data-ttu-id="07524-257">PromptBehavior.Always ignorerà l'utilizzo della cache e visualizzerà sempre l'interfaccia utente.</span><span class="sxs-lookup"><span data-stu-id="07524-257">PromptBehavior.Always will skip the cache usage and always show the UI.</span></span>

### <a name="silent-token-request-from-cache-and-refresh"></a><span data-ttu-id="07524-258">Richiesta invisibile all'utente dei token dalla cache e aggiornamento</span><span class="sxs-lookup"><span data-stu-id="07524-258">Silent token request from cache and refresh</span></span>
<span data-ttu-id="07524-259">Una richiesta di token invisibile all'utente non usa il popup dell'interfaccia utente e non richiede alcuna attività.</span><span class="sxs-lookup"><span data-stu-id="07524-259">A silent token request does not use the UI pop-up and does not require an activity.</span></span> <span data-ttu-id="07524-260">Restituisce un token dalla cache, se disponibile.</span><span class="sxs-lookup"><span data-stu-id="07524-260">It returns a token from the cache if available.</span></span> <span data-ttu-id="07524-261">Se il token è scaduto, questo metodo prova ad aggiornarlo.</span><span class="sxs-lookup"><span data-stu-id="07524-261">If the token is expired, this method tries to refresh it.</span></span> <span data-ttu-id="07524-262">Se il token di aggiornamento è scaduto o non è riuscito, restituisce AuthenticationException.</span><span class="sxs-lookup"><span data-stu-id="07524-262">If the refresh token is expired or failed, it returns AuthenticationException.</span></span>

    Future<AuthenticationResult> result = mContext.acquireTokenSilent(resource, clientid, userId, callback );

<span data-ttu-id="07524-263">Con questo metodo è anche possibile effettuare una chiamata di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="07524-263">You can also make a sync call by using this method.</span></span> <span data-ttu-id="07524-264">È possibile impostare Null per il callback o usare acquireTokenSilentSync.</span><span class="sxs-lookup"><span data-stu-id="07524-264">You can set null to callback or use acquireTokenSilentSync.</span></span>

### <a name="diagnostics"></a><span data-ttu-id="07524-265">Diagnostica</span><span class="sxs-lookup"><span data-stu-id="07524-265">Diagnostics</span></span>
<span data-ttu-id="07524-266">Di seguito sono riportate le fonti di informazioni principali per la diagnostica dei problemi:</span><span class="sxs-lookup"><span data-stu-id="07524-266">These are the primary sources of information for diagnosing issues:</span></span>

* <span data-ttu-id="07524-267">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="07524-267">Exceptions</span></span>
* <span data-ttu-id="07524-268">Log</span><span class="sxs-lookup"><span data-stu-id="07524-268">Logs</span></span>
* <span data-ttu-id="07524-269">Tracce di rete</span><span class="sxs-lookup"><span data-stu-id="07524-269">Network traces</span></span>

<span data-ttu-id="07524-270">Si noti che gli ID di correlazione sono fondamentali per la diagnostica della libreria.</span><span class="sxs-lookup"><span data-stu-id="07524-270">Note that correlation IDs are central to the diagnostics in the library.</span></span> <span data-ttu-id="07524-271">È possibile impostare gli ID di correlazione per le singole richieste, se si vuole correlare una richiesta ADAL con altre operazioni presenti nel codice.</span><span class="sxs-lookup"><span data-stu-id="07524-271">You can set your correlation IDs on a per-request basis if you want to correlate an ADAL request with other operations in your code.</span></span> <span data-ttu-id="07524-272">Se non si imposta un ID di correlazione, ADAL genererà un valore casuale.</span><span class="sxs-lookup"><span data-stu-id="07524-272">If you don't set a correlation ID, ADAL will generate a random one.</span></span> <span data-ttu-id="07524-273">Tutti i messaggi di log e le chiamate di rete verranno quindi contrassegnate con l'ID di correlazione.</span><span class="sxs-lookup"><span data-stu-id="07524-273">All log messages and network calls will then be stamped with the correlation ID.</span></span> <span data-ttu-id="07524-274">L'ID generato automaticamente cambia per ogni richiesta.</span><span class="sxs-lookup"><span data-stu-id="07524-274">The self-generated ID changes on each request.</span></span>

#### <a name="exceptions"></a><span data-ttu-id="07524-275">Eccezioni</span><span class="sxs-lookup"><span data-stu-id="07524-275">Exceptions</span></span>
<span data-ttu-id="07524-276">Le eccezioni costituiscono il primo elemento di diagnostica.</span><span class="sxs-lookup"><span data-stu-id="07524-276">Exceptions are the first diagnostic.</span></span> <span data-ttu-id="07524-277">Vengono forniti messaggi di errore che dovrebbero risultare utili,</span><span class="sxs-lookup"><span data-stu-id="07524-277">We try to provide helpful error messages.</span></span> <span data-ttu-id="07524-278">ma se qualcuno non dovesse esserlo, registrare il problema e segnalarlo.</span><span class="sxs-lookup"><span data-stu-id="07524-278">If you find one that is not helpful, please file an issue and let us know.</span></span> <span data-ttu-id="07524-279">Includere le informazioni relative al dispositivo, ad esempio modello e numero di SDK.</span><span class="sxs-lookup"><span data-stu-id="07524-279">Include device information such as model and SDK number.</span></span>

#### <a name="logs"></a><span data-ttu-id="07524-280">Log</span><span class="sxs-lookup"><span data-stu-id="07524-280">Logs</span></span>
<span data-ttu-id="07524-281">È possibile configurare la libreria in modo che vengano generati messaggi di log che possono risultare utili per diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="07524-281">You can configure the library to generate log messages that you can use to help diagnose issues.</span></span> <span data-ttu-id="07524-282">Per configurare la registrazione, eseguire la chiamata seguente per configurare un callback che ADAL userà per presentare ogni messaggio di log generato.</span><span class="sxs-lookup"><span data-stu-id="07524-282">You configure logging by making the following call to configure a callback that ADAL will use to hand off each log message as it's generated.</span></span>

    Logger.getInstance().setExternalLogger(new ILogger() {
        @Override
        public void Log(String tag, String message, String additionalMessage, LogLevel level, ADALError errorCode) {
        ...
        // You can write this to log file depending on level or error code.
        writeToLogFile(getApplicationContext(), tag +":" + message + "-" + additionalMessage);
        }
    }

<span data-ttu-id="07524-283">I messaggi possono essere scritti in un file di log personalizzato, come illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="07524-283">Messages can be written to a custom log file, as shown in the following code.</span></span> <span data-ttu-id="07524-284">Non esiste purtroppo un metodo standard per ottenere i log da un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="07524-284">Unfortunately, there is no standard way of getting logs from a device.</span></span> <span data-ttu-id="07524-285">A questo scopo, sono disponibili alcuni servizi che possono risultare utili.</span><span class="sxs-lookup"><span data-stu-id="07524-285">There are some services that can help you with this.</span></span> <span data-ttu-id="07524-286">È anche possibile crearne di personalizzati, ad esempio per l'invio del file a un server.</span><span class="sxs-lookup"><span data-stu-id="07524-286">You can also invent your own, such as sending the file to a server.</span></span>

    private syncronized void writeToLogFile(Context ctx, String msg) {
       File directory = ctx.getDir(ctx.getPackageName(), Context.MODE_PRIVATE);
       File logFile = new File(directory, "logfile");
       FileOutputStream outputStream = new FileOutputStream(logFile, true);
       OutputStreamWriter osw = new OutputStreamWriter(outputStream);
       osw.write(msg);
       osw.flush();
       osw.close();
    }

<span data-ttu-id="07524-287">Ecco i livelli di registrazione:</span><span class="sxs-lookup"><span data-stu-id="07524-287">These are the logging levels:</span></span>
* <span data-ttu-id="07524-288">Errore (eccezioni)</span><span class="sxs-lookup"><span data-stu-id="07524-288">Error (exceptions)</span></span>
* <span data-ttu-id="07524-289">Avviso (avviso)</span><span class="sxs-lookup"><span data-stu-id="07524-289">Warn (warning)</span></span>
* <span data-ttu-id="07524-290">Info (a scopo informativo)</span><span class="sxs-lookup"><span data-stu-id="07524-290">Info (information purposes)</span></span>
* <span data-ttu-id="07524-291">Dettagliato (altri dettagli)</span><span class="sxs-lookup"><span data-stu-id="07524-291">Verbose (more details)</span></span>

<span data-ttu-id="07524-292">Il livello di registrazione viene impostato nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="07524-292">You set the log level like this:</span></span>

    Logger.getInstance().setLogLevel(Logger.LogLevel.Verbose);

 <span data-ttu-id="07524-293">Tutti i messaggi di log vengono inviati a logcat, oltre agli eventuali callback di log personalizzati.</span><span class="sxs-lookup"><span data-stu-id="07524-293">All log messages are sent to logcat, in addition to any custom log callbacks.</span></span>
<span data-ttu-id="07524-294">È possibile ottenere un log in un file da logcat, come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="07524-294">You can get a log to a file from logcat as follows:</span></span>

    adb logcat > "C:\logmsg\logfile.txt"

 <span data-ttu-id="07524-295">Per informazioni dettagliate sui comandi adb, vedere le [informazioni relative a logcat nel sito Android](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span><span class="sxs-lookup"><span data-stu-id="07524-295">For details about adb commands, see the [logcat information on the Android site](https://developer.android.com/tools/debugging/debugging-log.html#startingLogcat).</span></span>

#### <a name="network-traces"></a><span data-ttu-id="07524-296">Tracce di rete</span><span class="sxs-lookup"><span data-stu-id="07524-296">Network traces</span></span>
<span data-ttu-id="07524-297">Per acquisire il traffico HTTP generato da ADAL sono disponibili diversi strumenti.</span><span class="sxs-lookup"><span data-stu-id="07524-297">You can use various tools to capture the HTTP traffic that ADAL generates.</span></span>  <span data-ttu-id="07524-298">Ciò è particolarmente utile se si ha familiarità con il protocollo OAuth o se è necessario fornire informazioni di diagnostica a Microsoft o altri canali di supporto.</span><span class="sxs-lookup"><span data-stu-id="07524-298">This is most useful if you're familiar with the OAuth protocol or if you need to provide diagnostic information to Microsoft or other support channels.</span></span>

<span data-ttu-id="07524-299">Fiddler è lo strumento di traccia HTTP più semplice.</span><span class="sxs-lookup"><span data-stu-id="07524-299">Fiddler is the easiest HTTP tracing tool.</span></span> <span data-ttu-id="07524-300">Usare i collegamenti seguenti per configurarlo in modo che registri correttamente il traffico di rete ADAL.</span><span class="sxs-lookup"><span data-stu-id="07524-300">Use the following links to set it up to correctly record ADAL network traffic.</span></span> <span data-ttu-id="07524-301">Per usare in modo ottimale uno strumento di traccia come Fiddler o Charles, è necessario configurarlo per la registrazione del traffico SSL non crittografato.</span><span class="sxs-lookup"><span data-stu-id="07524-301">For a tracing tool like Fiddler or Charles to be useful, you must configure it to record unencrypted SSL traffic.</span></span>  

> [!NOTE]
> <span data-ttu-id="07524-302">Le tracce generate in questo modo possono contenere informazioni con privilegi elevati, ad esempio token di accesso, nomi utente e password.</span><span class="sxs-lookup"><span data-stu-id="07524-302">Traces generated in this way might contain highly privileged information such as access tokens, usernames, and passwords.</span></span> <span data-ttu-id="07524-303">Se si usano account di produzione, non condividere queste tracce con terze parti.</span><span class="sxs-lookup"><span data-stu-id="07524-303">If you're using production accounts, do not share these traces with third parties.</span></span> <span data-ttu-id="07524-304">Se è necessario fornire una traccia a terzi per ottenere il supporto, riprodurre il problema con un account temporaneo usando nomi utente e password che è possibile condividere senza problemi.</span><span class="sxs-lookup"><span data-stu-id="07524-304">If you need to supply a trace to someone in order to get support, reproduce the issue by using a temporary account with usernames and passwords that you don't mind sharing.</span></span>

* <span data-ttu-id="07524-305">Vedere [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid) (Configurazione di Fiddler per Android) nel sito Web Telerik</span><span class="sxs-lookup"><span data-stu-id="07524-305">From the Telerik website: [Setting Up Fiddler For Android](http://docs.telerik.com/fiddler/configure-fiddler/tasks/ConfigureForAndroid)</span></span>
* <span data-ttu-id="07524-306">Vedere [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler) (Configurare le regole di Fiddler per ADAL) in GitHub</span><span class="sxs-lookup"><span data-stu-id="07524-306">From GitHub: [Configure Fiddler Rules For ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-android/wiki/How-to-listen-to-httpUrlConnection-in-Android-app-from-Fiddler)</span></span>

### <a name="dialog-mode"></a><span data-ttu-id="07524-307">Modalità della finestra di dialogo</span><span class="sxs-lookup"><span data-stu-id="07524-307">Dialog mode</span></span>
<span data-ttu-id="07524-308">Il metodo acquireToken senza attività supporta prompt della finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="07524-308">The acquireToken method without activity supports a dialog prompt.</span></span>

### <a name="encryption"></a><span data-ttu-id="07524-309">Crittografia</span><span class="sxs-lookup"><span data-stu-id="07524-309">Encryption</span></span>
<span data-ttu-id="07524-310">ADAL crittografa i token e li archivia in SharedPreferences per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="07524-310">ADAL encrypts the tokens and store in SharedPreferences by default.</span></span> <span data-ttu-id="07524-311">È possibile esaminare la classe StorageHelper per visualizzare i dettagli.</span><span class="sxs-lookup"><span data-stu-id="07524-311">You can look at the StorageHelper class to see the details.</span></span> <span data-ttu-id="07524-312">Android ha introdotto Android Keystore 4.3 (API 18) per l'archiviazione protetta delle chiavi private.</span><span class="sxs-lookup"><span data-stu-id="07524-312">Android introduced Android Keystore for 4.3 (API 18) secure storage of private keys.</span></span> <span data-ttu-id="07524-313">ADAL lo usa per API 18 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="07524-313">ADAL uses that for API 18 and higher.</span></span> <span data-ttu-id="07524-314">Se si vuole usare ADAL per versioni precedenti dell'SDK, è necessario fornire la chiave privata in AuthenticationSettings.INSTANCE.setSecretKey.</span><span class="sxs-lookup"><span data-stu-id="07524-314">If you want to use ADAL for lower SDK versions, you need to provide a secret key at AuthenticationSettings.INSTANCE.setSecretKey.</span></span>

### <a name="oauth2-bearer-challenge"></a><span data-ttu-id="07524-315">Richiesta di connessione di OAuth2</span><span class="sxs-lookup"><span data-stu-id="07524-315">OAuth2 bearer challenge</span></span>
<span data-ttu-id="07524-316">La classe AuthenticationParameters fornisce la funzionalità per ottenere authorization_uri dalla richiesta di connessione di OAuth2.</span><span class="sxs-lookup"><span data-stu-id="07524-316">The AuthenticationParameters class provides functionality to get authorization_uri from the OAuth2 bearer challenge.</span></span>

### <a name="session-cookies-in-webview"></a><span data-ttu-id="07524-317">Cookie di sessione in WebView</span><span class="sxs-lookup"><span data-stu-id="07524-317">Session cookies in WebView</span></span>
<span data-ttu-id="07524-318">Android WebView non cancella i cookie di sessione dopo la chiusura dell'app.</span><span class="sxs-lookup"><span data-stu-id="07524-318">Android WebView does not clear session cookies after the app is closed.</span></span> <span data-ttu-id="07524-319">È possibile gestire questa operazione usando questo codice di esempio:</span><span class="sxs-lookup"><span data-stu-id="07524-319">You can handle that by using this sample code:</span></span>

    CookieSyncManager.createInstance(getApplicationContext());
    CookieManager cookieManager = CookieManager.getInstance();
    cookieManager.removeSessionCookie();
    CookieSyncManager.getInstance().sync();

<span data-ttu-id="07524-320">Per informazioni dettagliate sui cookie, vedere le [informazioni su CookieSyncManager nel sito Android](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span><span class="sxs-lookup"><span data-stu-id="07524-320">For details about cookies, see the [CookieSyncManager information on the Android site](http://developer.android.com/reference/android/webkit/CookieSyncManager.html).</span></span>

### <a name="resource-overrides"></a><span data-ttu-id="07524-321">Override delle risorse</span><span class="sxs-lookup"><span data-stu-id="07524-321">Resource overrides</span></span>
<span data-ttu-id="07524-322">La libreria ADAL include stringhe in inglese per messaggi ProgressDialog.</span><span class="sxs-lookup"><span data-stu-id="07524-322">The ADAL library includes English strings for ProgressDialog messages.</span></span> <span data-ttu-id="07524-323">L'applicazione deve sovrascriverle, se si vogliono usare stringhe localizzate.</span><span class="sxs-lookup"><span data-stu-id="07524-323">Your application should overwrite them if you want localized strings.</span></span>

     <string name="app_loading">Loading...</string>
     <string name="broker_processing">Broker is processing</string>
     <string name="http_auth_dialog_username">Username</string>
     <string name="http_auth_dialog_password">Password</string>
     <string name="http_auth_dialog_title">Sign In</string>
     <string name="http_auth_dialog_login">Login</string>
     <string name="http_auth_dialog_cancel">Cancel</string>

### <a name="ntlm-dialog-box"></a><span data-ttu-id="07524-324">Finestra di dialogo NTLM</span><span class="sxs-lookup"><span data-stu-id="07524-324">NTLM dialog box</span></span>
<span data-ttu-id="07524-325">ADAL versione 1.1.0 supporta la finestra di dialogo NTLM che viene elaborata tramite l'evento onReceivedHttpAuthRequest da WebViewClient.</span><span class="sxs-lookup"><span data-stu-id="07524-325">ADAL version 1.1.0 supports an NTLM dialog box that is processed through the onReceivedHttpAuthRequest event from WebViewClient.</span></span> <span data-ttu-id="07524-326">È possibile personalizzare il layout e le stringhe per la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="07524-326">You can customize the layout and strings for the dialog box.</span></span>

### <a name="cross-app-sso"></a><span data-ttu-id="07524-327">Accesso Single Sign-On tra app</span><span class="sxs-lookup"><span data-stu-id="07524-327">Cross-app SSO</span></span>
<span data-ttu-id="07524-328">Informazioni su [Come abilitare l'accesso Single Sign-On tra app su Android usando ADAL](active-directory-sso-android.md).</span><span class="sxs-lookup"><span data-stu-id="07524-328">Learn [how to enable cross-app SSO on Android by using ADAL](active-directory-sso-android.md).</span></span>  

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
