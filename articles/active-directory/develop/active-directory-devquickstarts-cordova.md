---
title: aaaAzure AD Cordova introduzione | Documenti Microsoft
description: Come toobuild un'applicazione Cordova che si integra con Azure AD per l'accesso e chiama le API di protetto AD Azure tramite OAuth.
services: active-directory
documentationcenter: 
author: vibronet
manager: mbaldwin
editor: 
ms.assetid: b1a8d7bd-7ad6-44d5-8ccb-5255bb623345
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 01/07/2017
ms.author: vittorib
ms.custom: aaddev
ms.openlocfilehash: 573ed638c2180c5231648bcb8c49ceb6f53296f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="caa11-103">Integrare Azure AD con un'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="caa11-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="caa11-104">È possibile utilizzare Apache Cordova toodevelop HTML5/JavaScript applicazioni eseguibili nei dispositivi mobili come applicazioni native complete.</span><span class="sxs-lookup"><span data-stu-id="caa11-104">You can use Apache Cordova toodevelop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="caa11-105">Con Azure Active Directory (Azure AD), è possibile aggiungere applicazioni di Cordova tooyour funzionalità autenticazione aziendale.</span><span class="sxs-lookup"><span data-stu-id="caa11-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities tooyour Cordova applications.</span></span>

<span data-ttu-id="caa11-106">Un plug-in Cordova esegue il wrapping di SDK nativi di Azure AD in iOS, Android, Windows Store e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="caa11-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="caa11-107">Utilizzando, plug-in, è possibile migliorare l'applicazione toosupport Accedi con account di Windows Server Active Directory degli utenti, ottenere accesso tooOffice 365 e API di Azure e anche proteggere chiamate tooyour proprio personalizzato API web.</span><span class="sxs-lookup"><span data-stu-id="caa11-107">By using that plug-in, you can enhance your application toosupport sign-in with your users' Windows Server Active Directory accounts, gain access tooOffice 365 and Azure APIs, and even help protect calls tooyour own custom web API.</span></span>

<span data-ttu-id="caa11-108">In questa esercitazione si userà hello Apache Cordova plug-in per Active Directory Authentication Library (ADAL) tooimprove una semplice app aggiungendo hello seguenti caratteristiche:</span><span class="sxs-lookup"><span data-stu-id="caa11-108">In this tutorial, we'll use hello Apache Cordova plug-in for Active Directory Authentication Library (ADAL) tooimprove a simple app by adding hello following features:</span></span>

* <span data-ttu-id="caa11-109">Sono sufficienti poche righe di codice per autenticare un utente e ottenere un token.</span><span class="sxs-lookup"><span data-stu-id="caa11-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="caa11-110">Utilizzare tale tooquery di API Graph hello tooinvoke token tale directory e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-110">Use that token tooinvoke hello Graph API tooquery that directory and display hello results.</span></span>  
* <span data-ttu-id="caa11-111">Utilizzare l'autenticazione ADAL cache dei token di hello toominimize richiesto per l'utente hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-111">Use hello ADAL token cache toominimize authentication prompts for hello user.</span></span>

<span data-ttu-id="caa11-112">toomake questi miglioramenti, è necessario:</span><span class="sxs-lookup"><span data-stu-id="caa11-112">toomake those improvements, you need to:</span></span>

1. <span data-ttu-id="caa11-113">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caa11-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="caa11-114">Aggiungere codice tooyour app toorequest token.</span><span class="sxs-lookup"><span data-stu-id="caa11-114">Add code tooyour app toorequest tokens.</span></span>
3. <span data-ttu-id="caa11-115">Aggiungere codice toouse hello token per l'esecuzione di query hello API Graph e visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="caa11-115">Add code toouse hello token for querying hello Graph API and display results.</span></span>
4. <span data-ttu-id="caa11-116">Crea progetto di distribuzione Cordova hello con tutte le piattaforme hello si desidera tootarget, hello Cordova ADAL plug-in aggiungere e testare soluzioni hello in emulatori.</span><span class="sxs-lookup"><span data-stu-id="caa11-116">Create hello Cordova deployment project with all hello platforms you want tootarget, add hello Cordova ADAL plug-in, and test hello solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="caa11-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="caa11-117">Prerequisites</span></span>
<span data-ttu-id="caa11-118">toocomplete questa esercitazione, è necessario:</span><span class="sxs-lookup"><span data-stu-id="caa11-118">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="caa11-119">Tenant di Azure AD nel quale è disponibile un account con diritti per lo sviluppo di app.</span><span class="sxs-lookup"><span data-stu-id="caa11-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="caa11-120">Un ambiente di sviluppo configurato toouse Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="caa11-120">A development environment that's configured toouse Apache Cordova.</span></span>  

<span data-ttu-id="caa11-121">Se si dispone sia già configurato, procedere direttamente toostep 1.</span><span class="sxs-lookup"><span data-stu-id="caa11-121">If you have both already set up, proceed directly toostep 1.</span></span>

<span data-ttu-id="caa11-122">Se non si dispone di un tenant di Azure AD, usare hello [istruzioni su come tooget uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="caa11-122">If you don't have an Azure AD tenant, use hello [instructions on how tooget one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="caa11-123">Se non si dispone di Apache Cordova configurare nel computer, installare l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="caa11-123">If you don't have Apache Cordova set up on your machine, install hello following:</span></span>

* [<span data-ttu-id="caa11-124">Git</span><span class="sxs-lookup"><span data-stu-id="caa11-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="caa11-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="caa11-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="caa11-126">[Interfaccia della riga di comando di Cordova](https://cordova.apache.org/) (può essere installata facilmente tramite Gestione pacchetti NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="caa11-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="caa11-127">Hello installazioni precedenti dovrebbe funzionare sia sui PC hello hello Mac.</span><span class="sxs-lookup"><span data-stu-id="caa11-127">hello preceding installations should work both on hello PC and on hello Mac.</span></span>

<span data-ttu-id="caa11-128">Ogni piattaforma di destinazione ha prerequisiti diversi:</span><span class="sxs-lookup"><span data-stu-id="caa11-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="caa11-129">toobuild ed eseguire un'app per PC o Tablet PC di Windows o Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="caa11-129">toobuild and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="caa11-130">Installare [Visual Studio 2013 per Windows con Update 2 o versione successiva](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express o altra versione) oppure [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="caa11-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="caa11-131">toobuild ed eseguire un'app per iOS:</span><span class="sxs-lookup"><span data-stu-id="caa11-131">toobuild and run an app for iOS:</span></span>

  * <span data-ttu-id="caa11-132">Installare Xcode 6.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="caa11-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="caa11-133">Scaricarlo dal hello [sito per sviluppatori Apple](http://developer.apple.com/downloads) o hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="caa11-133">Download it from hello [Apple Developer site](http://developer.apple.com/downloads) or hello [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="caa11-134">Installare [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="caa11-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="caa11-135">È possibile utilizzare le app iOS toostart nel simulatore iOS da riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-135">You can use it toostart iOS apps in iOS Simulator from hello command line.</span></span> <span data-ttu-id="caa11-136">(È possibile installare facilmente tramite terminal hello: `npm install -g ios-sim`.)</span><span class="sxs-lookup"><span data-stu-id="caa11-136">(You can easily install it via hello terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="caa11-137">toobuild ed eseguire un'app per Android:</span><span class="sxs-lookup"><span data-stu-id="caa11-137">toobuild and run an app for Android:</span></span>

  * <span data-ttu-id="caa11-138">Installare [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="caa11-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="caa11-139">Assicurarsi che `JAVA_HOME` (variabile di ambiente) è impostato correttamente in base a percorso di installazione di JDK toohello (ad esempio, c:\Programmi\Microsoft Files\Java\jdk1.7.0_75).</span><span class="sxs-lookup"><span data-stu-id="caa11-139">Make sure `JAVA_HOME` (environment variable) is correctly set according toohello JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="caa11-140">Installare [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) e aggiungere hello `<android-sdk-location>\tools` tooyour percorso (ad esempio, C:\tools\Android\android-sdk\tools) `PATH` variabile di ambiente.</span><span class="sxs-lookup"><span data-stu-id="caa11-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add hello `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) tooyour `PATH` environment variable.</span></span>
  * <span data-ttu-id="caa11-141">Apri Android SDK Manager (ad esempio, tramite terminal hello: `android`) e installare:</span><span class="sxs-lookup"><span data-stu-id="caa11-141">Open Android SDK Manager (for example, via hello terminal: `android`) and install:</span></span>
    * <span data-ttu-id="caa11-142">*Android 5.0.1 (API 21)* Platform SDK</span><span class="sxs-lookup"><span data-stu-id="caa11-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="caa11-143">*Android SDK Build Tools* 19.1.0 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="caa11-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="caa11-144">*Android Support Repository* (funzionalità aggiuntive)</span><span class="sxs-lookup"><span data-stu-id="caa11-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="caa11-145">Hello, Android SDK non fornisce a qualsiasi istanza dell'emulatore predefinito.</span><span class="sxs-lookup"><span data-stu-id="caa11-145">hello Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="caa11-146">Crearne una eseguendo `android avd` da terminal hello e quindi selezionando **crea**, se si desidera toorun app per Android hello in un emulatore.</span><span class="sxs-lookup"><span data-stu-id="caa11-146">Create one by running `android avd` from hello terminal and then selecting **Create**, if you want toorun hello Android app on an emulator.</span></span> <span data-ttu-id="caa11-147">È consigliabile usare un' API di livello 19 o superiore.</span><span class="sxs-lookup"><span data-stu-id="caa11-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="caa11-148">Per ulteriori informazioni sulle opzioni di creazione e l'emulatore Android hello, vedere [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) nel sito Android hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-148">For more information about hello Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on hello Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="caa11-149">Passaggio 1: Registrare un'applicazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa11-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="caa11-150">Questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="caa11-150">This step is optional.</span></span> <span data-ttu-id="caa11-151">In questa esercitazione vengono pre-provisioning di valori che è possibile utilizzare toosee hello esempio nell'azione senza effettuare alcun provisioning nel proprio tenant.</span><span class="sxs-lookup"><span data-stu-id="caa11-151">This tutorial provides pre-provisioned values that you can use toosee hello sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="caa11-152">Tuttavia, è consigliabile eseguire questo passaggio e acquisire familiarità con il processo di hello, perché sarà necessaria la creazione di applicazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="caa11-152">However, we recommend that you do perform this step and become familiar with hello process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="caa11-153">Azure AD rilascia token tooonly noto di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="caa11-153">Azure AD issues tokens tooonly known applications.</span></span> <span data-ttu-id="caa11-154">Prima di poter utilizzare Azure AD dall'app, è necessario toocreate una voce per tale nel tenant.</span><span class="sxs-lookup"><span data-stu-id="caa11-154">Before you can use Azure AD from your app, you need toocreate an entry for it in your tenant.</span></span> <span data-ttu-id="caa11-155">tooregister una nuova applicazione nel tenant di:</span><span class="sxs-lookup"><span data-stu-id="caa11-155">tooregister a new application in your tenant:</span></span>

1. <span data-ttu-id="caa11-156">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="caa11-156">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="caa11-157">Nella barra superiore hello, fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="caa11-157">On hello top bar, click your account.</span></span> <span data-ttu-id="caa11-158">In hello **Directory** scegliere tenant hello Azure Active Directory in cui si desidera tooregister l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="caa11-158">In hello **Directory** list, choose hello Azure AD tenant where you want tooregister your application.</span></span>
3. <span data-ttu-id="caa11-159">Fare clic su **più servizi** in hello riquadro sinistro e quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="caa11-159">Click **More Services** in hello left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="caa11-160">Fare clic su **Registrazioni per l'app** e scegliere **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="caa11-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="caa11-161">Seguire le istruzioni di hello e creare un **applicazione Client nativa**.</span><span class="sxs-lookup"><span data-stu-id="caa11-161">Follow hello prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="caa11-162">Benché le app Cordova siano basate su HTML, verrà creata un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="caa11-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="caa11-163">Hello **applicazione Client nativa** opzione deve essere selezionata o un'applicazione hello non funzionerà.)</span><span class="sxs-lookup"><span data-stu-id="caa11-163">hello **Native Client Application** option must be selected, or hello application won't work.)</span></span>
  * <span data-ttu-id="caa11-164">**Nome** descrive toousers l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="caa11-164">**Name** describes your application toousers.</span></span>
  * <span data-ttu-id="caa11-165">**URI di reindirizzamento** è hello URI utilizzato tooreturn token tooyour app.</span><span class="sxs-lookup"><span data-stu-id="caa11-165">**Redirect URI** is hello URI that's used tooreturn tokens tooyour app.</span></span> <span data-ttu-id="caa11-166">Immettere **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="caa11-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="caa11-167">Dopo aver completato la registrazione, Azure AD le assegna un'app di tooyour ID applicazione univoco.</span><span class="sxs-lookup"><span data-stu-id="caa11-167">After you finish registration, Azure AD assigns a unique application ID tooyour app.</span></span> <span data-ttu-id="caa11-168">È necessario che questo valore nelle sezioni successive di hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-168">You’ll need this value in hello next sections.</span></span> <span data-ttu-id="caa11-169">È possibile trovarlo nella scheda applicazione hello di hello app appena creata.</span><span class="sxs-lookup"><span data-stu-id="caa11-169">You can find it on hello application tab of hello newly created app.</span></span>

<span data-ttu-id="caa11-170">toorun `DirSearchClient Sample`, concedere hello appena creato app autorizzazione tooquery hello Azure AD Graph API:</span><span class="sxs-lookup"><span data-stu-id="caa11-170">toorun `DirSearchClient Sample`, grant hello newly created app permission tooquery hello Azure AD Graph API:</span></span>

1. <span data-ttu-id="caa11-171">Da hello **impostazioni** selezionare **autorizzazioni obbligatorie**e quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="caa11-171">From hello **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="caa11-172">Per hello applicazione Azure Active Directory, selezionare **Microsoft Graph** come hello API e aggiungere hello **directory hello accesso come utente connesso di hello** autorizzazione in **delegati Autorizzazioni**.</span><span class="sxs-lookup"><span data-stu-id="caa11-172">For hello Azure Active Directory application, select **Microsoft Graph** as hello API and add hello **Access hello directory as hello signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="caa11-173">In questo modo hello di tooquery l'applicazione API Graph per gli utenti.</span><span class="sxs-lookup"><span data-stu-id="caa11-173">This enables your application tooquery hello Graph API for users.</span></span>

## <a name="step-2-clone-hello-sample-app-repository"></a><span data-ttu-id="caa11-174">Passaggio 2: Clonare il repository di app di esempio hello</span><span class="sxs-lookup"><span data-stu-id="caa11-174">Step 2: Clone hello sample app repository</span></span>
<span data-ttu-id="caa11-175">La shell o la riga di comando, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="caa11-175">From your shell or command line, type hello following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-hello-cordova-app"></a><span data-ttu-id="caa11-176">Passaggio 3: Creare app di Cordova hello</span><span class="sxs-lookup"><span data-stu-id="caa11-176">Step 3: Create hello Cordova app</span></span>
<span data-ttu-id="caa11-177">Esistono più modi toocreate Cordova applicazioni.</span><span class="sxs-lookup"><span data-stu-id="caa11-177">There are multiple ways toocreate Cordova applications.</span></span> <span data-ttu-id="caa11-178">In questa esercitazione verrà utilizzata l'interfaccia della riga di comando di Cordova hello (CLI).</span><span class="sxs-lookup"><span data-stu-id="caa11-178">In this tutorial, we'll use hello Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="caa11-179">La shell o la riga di comando, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="caa11-179">From your shell or command line, type hello following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="caa11-180">Tale comando Crea struttura di cartelle hello e lo scaffolding per progetto Cordova hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-180">That command creates hello folder structure and scaffolding for hello Cordova project.</span></span>

2. <span data-ttu-id="caa11-181">Spostare la nuova cartella di DirSearchClient toohello:</span><span class="sxs-lookup"><span data-stu-id="caa11-181">Move toohello new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="caa11-182">Copiare il contenuto di hello del progetto di avvio hello nella sottocartella www hello tramite un gestore di file o hello comando nella shell seguente:</span><span class="sxs-lookup"><span data-stu-id="caa11-182">Copy hello content of hello starter project in hello www subfolder by using a file manager or hello following command in your shell:</span></span>

  * <span data-ttu-id="caa11-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="caa11-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="caa11-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="caa11-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="caa11-185">Aggiungere whitelist hello plug-in.</span><span class="sxs-lookup"><span data-stu-id="caa11-185">Add hello whitelist plug-in.</span></span> <span data-ttu-id="caa11-186">Ciò è necessario per richiamare hello API Graph.</span><span class="sxs-lookup"><span data-stu-id="caa11-186">This is necessary for invoking hello Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="caa11-187">Aggiungere tutte le piattaforme che si desidera toosupport hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-187">Add all hello platforms that you want toosupport.</span></span> <span data-ttu-id="caa11-188">toohave un esempio funzionante, è necessario tooexecute almeno uno dei seguenti comandi hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-188">toohave a working sample, you need tooexecute at least one of hello following commands.</span></span> <span data-ttu-id="caa11-189">Si noti che non essere in grado di tooemulate iOS in Windows o di emulazione di Windows sul Mac.</span><span class="sxs-lookup"><span data-stu-id="caa11-189">Note that you won't be able tooemulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="caa11-190">Aggiungere hello ADAL per progetto tooyour plug-in Cordova:</span><span class="sxs-lookup"><span data-stu-id="caa11-190">Add hello ADAL for Cordova plug-in tooyour project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-tooauthenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="caa11-191">Passaggio 4: Aggiungere utenti tooauthenticate codice e ottenere i token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="caa11-191">Step 4: Add code tooauthenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="caa11-192">un'applicazione Hello sviluppata in questa esercitazione fornirà una funzionalità di ricerca di directory semplice.</span><span class="sxs-lookup"><span data-stu-id="caa11-192">hello application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="caa11-193">utente Hello, digitare l'alias di hello di qualsiasi utente nella directory hello e visualizzare alcuni attributi di base.</span><span class="sxs-lookup"><span data-stu-id="caa11-193">hello user can then type hello alias of any user in hello directory and visualize some basic attributes.</span></span> <span data-ttu-id="caa11-194">progetto iniziale Hello contiene definizione hello dell'interfaccia utente di base hello dell'app di hello (in www/index.html) e lo scaffolding di hello che collega evento app di base di cicli, le associazioni dell'interfaccia utente e comporta la logica di visualizzazione (in www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="caa11-194">hello starter project contains hello definition of hello basic user interface of hello app (in www/index.html) and hello scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="caa11-195">Hello unica attività a sinistra per l'utente è tooadd hello logica che implementa l'attività di identità.</span><span class="sxs-lookup"><span data-stu-id="caa11-195">hello only task left for you is tooadd hello logic that implements identity tasks.</span></span>

<span data-ttu-id="caa11-196">Hello innanzitutto, è necessario toodo nel codice è introdurre valori di protocollo hello Azure AD viene utilizzato per identificare l'app e hello risorse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="caa11-196">hello first thing you need toodo in your code is introduce hello protocol values that Azure AD uses for identifying your app and hello resources that you target.</span></span> <span data-ttu-id="caa11-197">Questi valori sono le richieste di token hello tooconstruct utilizzati in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="caa11-197">Those values will be used tooconstruct hello token requests later on.</span></span> <span data-ttu-id="caa11-198">Inserire il seguente frammento di codice all'inizio di hello del file di index.js hello hello:</span><span class="sxs-lookup"><span data-stu-id="caa11-198">Insert hello following snippet at hello top of hello index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="caa11-199">Hello `redirectUri` e `clientId` valori devono corrispondere i valori hello che descrivono l'app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="caa11-199">hello `redirectUri` and `clientId` values should match hello values that describe your app in Azure AD.</span></span> <span data-ttu-id="caa11-200">È possibile trovarli da hello **configura** scheda hello portale di Azure, come descritto nel passaggio 1, più indietro in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="caa11-200">You can find those from hello **Configure** tab in hello Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="caa11-201">Se si è scelto di non registra una nuova app nel proprio tenant, è possibile semplicemente incollare i valori hello preconfigurato come è.</span><span class="sxs-lookup"><span data-stu-id="caa11-201">If you opted for not registering a new app in your own tenant, you can simply paste hello preconfigured values as is.</span></span> <span data-ttu-id="caa11-202">È quindi possibile visualizzare hello esempio in esecuzione, anche se è consigliabile creare sempre una voce personalizzata per le app che sono concepite per la produzione.</span><span class="sxs-lookup"><span data-stu-id="caa11-202">You can then see hello sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="caa11-203">Successivamente, aggiungere il codice di richiesta di token hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-203">Next, add hello token request code.</span></span> <span data-ttu-id="caa11-204">Inserisci hello seguente frammento di codice tra hello `search` e `renderData` definizioni:</span><span class="sxs-lookup"><span data-stu-id="caa11-204">Insert hello following snippet between hello `search` and `renderData` definitions:</span></span>

```javascript
    // Shows hello user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="caa11-205">Si esaminerà ora la funzione suddividendola nelle due parti principali.</span><span class="sxs-lookup"><span data-stu-id="caa11-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="caa11-206">In questo esempio è progettato toowork con un tenant, come toobeing anziché legata tooa uno.</span><span class="sxs-lookup"><span data-stu-id="caa11-206">This sample is designed toowork with any tenant, as opposed toobeing tied tooa particular one.</span></span> <span data-ttu-id="caa11-207">Usa hello endpoint "/ comuni", che consente a qualsiasi account hello utente tooenter al momento dell'autenticazione e indirizza il tenant di hello richiesta toohello cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="caa11-207">It uses hello "/common" endpoint, which allows hello user tooenter any account at authentication time and directs hello request toohello tenant where it belongs.</span></span>

<span data-ttu-id="caa11-208">La prima parte del metodo hello controlla hello cache ADAL toosee se un token è già archiviato.</span><span class="sxs-lookup"><span data-stu-id="caa11-208">This first part of hello method inspects hello ADAL cache toosee if a token is already stored.</span></span> <span data-ttu-id="caa11-209">In questo caso, il metodo di hello Usa tenant hello token hello provenienza per reinizializzare ADAL.</span><span class="sxs-lookup"><span data-stu-id="caa11-209">If so, hello method uses hello tenants where hello token came from for reinitializing ADAL.</span></span> <span data-ttu-id="caa11-210">Ciò è necessario tooavoid prompt aggiuntivo, perché hello uso di "/ comuni" genera sempre porre hello utente tooenter un nuovo account.</span><span class="sxs-lookup"><span data-stu-id="caa11-210">This is necessary tooavoid extra prompts, because hello use of "/common" always results in asking hello user tooenter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="caa11-211">seconda parte di Hello del metodo hello esegue una richiesta di token corretto hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-211">hello second part of hello method performs hello proper token request.</span></span> <span data-ttu-id="caa11-212">Hello `acquireTokenSilentAsync` metodo chiede tooreturn ADAL un token specificato hello risorsa senza visualizzare alcun UX.</span><span class="sxs-lookup"><span data-stu-id="caa11-212">hello `acquireTokenSilentAsync` method asks ADAL tooreturn a token for hello specified resource without showing any UX.</span></span> <span data-ttu-id="caa11-213">Ciò può verificarsi se cache di hello dispone già di un token di accesso appropriato archiviato, o se un token di aggiornamento può essere utilizzato tooget un nuovo token di accesso senza che venga visualizzato un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="caa11-213">That can happen if hello cache already has a suitable access token stored, or if a refresh token can be used tooget a new access token without showing any prompt.</span></span> <span data-ttu-id="caa11-214">Se il tentativo ha esito negativo, è il fallback `acquireTokenAsync`-che chiederà visibilmente tooauthenticate utente hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt hello user tooauthenticate.</span></span>

```javascript
            // Attempt tooauthorize hello user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers hello authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed tooauthenticate: " + err);
                });
            });
```
<span data-ttu-id="caa11-215">Ora che abbiamo token hello, è infine possibile richiamare l'API Graph hello e query di ricerca hello che si desidera eseguire.</span><span class="sxs-lookup"><span data-stu-id="caa11-215">Now that we have hello token, we can finally invoke hello Graph API and perform hello search query that we want.</span></span> <span data-ttu-id="caa11-216">Inserisci hello seguente frammento di codice di sotto di hello `authenticate` definizione:</span><span class="sxs-lookup"><span data-stu-id="caa11-216">Insert hello following snippet below hello `authenticate` definition:</span></span>

```javascript
// Makes an API call tooreceive hello user list
    requestData: function (authResult, searchText) {
        var req = new XMLHttpRequest();
        var url = resourceUri + "/" + authResult.tenantId + "/users?api-version=" + graphApiVersion;
        url = searchText ? url + "&$filter=mailNickname eq '" + searchText + "'" : url + "&$top=10";

        req.open("GET", url, true);
        req.setRequestHeader('Authorization', 'Bearer ' + authResult.accessToken);

        req.onload = function(e) {
            if (e.target.status >= 200 && e.target.status < 300) {
                app.renderData(JSON.parse(e.target.response));
                return;
            }
            app.error('Data request failed: ' + e.target.response);
        };
        req.onerror = function(e) {
            app.error('Data request failed: ' + e.error);
        }

        req.send();
    },

```
<span data-ttu-id="caa11-217">file punto di partenza Hello fornire un'esperienza utente semplice per l'immissione di un alias utente in una casella di testo.</span><span class="sxs-lookup"><span data-stu-id="caa11-217">hello starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="caa11-218">Questo metodo utilizza tale valore tooconstruct una query, combinarla con il token di accesso di hello, inviarlo tooMicrosoft grafico e analizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-218">This method uses that value tooconstruct a query, combine it with hello access token, send it tooMicrosoft Graph, and parse hello results.</span></span> <span data-ttu-id="caa11-219">Hello `renderData` (metodo), già presente nel file di punto di partenza hello, si occupa della visualizzazione dei risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-219">hello `renderData` method, already present in hello starting-point file, takes care of visualizing hello results.</span></span>

## <a name="step-5-run-hello-app"></a><span data-ttu-id="caa11-220">Passaggio 5: Eseguire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="caa11-220">Step 5: Run hello app</span></span>
<span data-ttu-id="caa11-221">L'app è toorun pronto.</span><span class="sxs-lookup"><span data-stu-id="caa11-221">Your app is finally ready toorun.</span></span> <span data-ttu-id="caa11-222">Il funzionamento è semplice: quando viene avviata l'applicazione hello, immettere l'alias dell'utente hello si desidera ripristinare toolook hello e quindi fare clic su pulsante hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-222">Operating it is simple: when hello app starts, enter hello alias of hello user you want toolook up, and then click hello button.</span></span> <span data-ttu-id="caa11-223">Viene richiesto di autenticarsi.</span><span class="sxs-lookup"><span data-stu-id="caa11-223">You're prompted for authentication.</span></span> <span data-ttu-id="caa11-224">Dopo l'autenticazione e la ricerca ha esito positivo, vengono visualizzati gli attributi di hello di hello ricercata utente.</span><span class="sxs-lookup"><span data-stu-id="caa11-224">Upon successful authentication and successful search, hello attributes of hello searched user are displayed.</span></span>

<span data-ttu-id="caa11-225">Le esecuzioni successive verranno eseguite hello ricerca senza visualizzare alcun messaggio, grazie toohello presenza di hello precedentemente acquisito token nella cache.</span><span class="sxs-lookup"><span data-stu-id="caa11-225">Subsequent runs will perform hello search without showing any prompt, thanks toohello presence of hello previously acquired token in cache.</span></span>

<span data-ttu-id="caa11-226">Hello passaggi concreto per l'esecuzione di app hello variano a seconda della piattaforma.</span><span class="sxs-lookup"><span data-stu-id="caa11-226">hello concrete steps for running hello app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="caa11-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="caa11-227">Windows 10</span></span>
   <span data-ttu-id="caa11-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="caa11-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="caa11-229">Dispositivi mobili (richiede un tooa di dispositivo connesso PC Windows 10 Mobile):`cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="caa11-229">Mobile (requires a Windows 10 Mobile device connected tooa PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="caa11-230">Durante la prima esecuzione di hello, potrebbe essere richiesto toosign in per una licenza per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="caa11-230">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="caa11-231">Per altre informazioni, vedere [Licenza per sviluppatori](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="caa11-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="caa11-232">Tablet/PC con Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="caa11-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="caa11-233">Durante la prima esecuzione di hello, potrebbe essere richiesto toosign in per una licenza per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="caa11-233">During hello first run, you might be asked toosign in for a developer license.</span></span> <span data-ttu-id="caa11-234">Per altre informazioni, vedere [Licenza per sviluppatori](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="caa11-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="caa11-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="caa11-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="caa11-236">toorun in un dispositivo collegato:`cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="caa11-236">toorun on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="caa11-237">toorun sull'emulatore predefinito hello:`cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="caa11-237">toorun on hello default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="caa11-238">Utilizzare `cordova run windows --list -- --phone` toosee tutte le destinazioni disponibili e `cordova run windows --target=<target_name> -- --phone` toorun un'applicazione hello in un emulatore o un dispositivo specifico (ad esempio, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span><span class="sxs-lookup"><span data-stu-id="caa11-238">Use `cordova run windows --list -- --phone` toosee all available targets and `cordova run windows --target=<target_name> -- --phone` toorun hello application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="caa11-239">Android</span><span class="sxs-lookup"><span data-stu-id="caa11-239">Android</span></span>
   <span data-ttu-id="caa11-240">toorun in un dispositivo collegato:`cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="caa11-240">toorun on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="caa11-241">toorun sull'emulatore predefinito hello:`cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="caa11-241">toorun on hello default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="caa11-242">Assicurarsi di che aver creato un'istanza dell'emulatore con AVD Manager, come descritto in precedenza nella sezione "Prerequisiti" hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in hello "Prerequisites" section.</span></span>

   <span data-ttu-id="caa11-243">Utilizzare `cordova run android --list` toosee tutte le destinazioni disponibili e `cordova run android --target=<target_name>` toorun un'applicazione hello in un emulatore o un dispositivo specifico (ad esempio, `cordova run android --target="Nexus4_emulator"`).</span><span class="sxs-lookup"><span data-stu-id="caa11-243">Use `cordova run android --list` toosee all available targets and `cordova run android --target=<target_name>` toorun hello application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="caa11-244">iOS</span><span class="sxs-lookup"><span data-stu-id="caa11-244">iOS</span></span>
   <span data-ttu-id="caa11-245">toorun in un dispositivo collegato:`cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="caa11-245">toorun on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="caa11-246">toorun sull'emulatore predefinito hello:`cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="caa11-246">toorun on hello default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="caa11-247">Assicurarsi di avere hello `ios-sim` toorun pacchetto installato in un emulatore hello.</span><span class="sxs-lookup"><span data-stu-id="caa11-247">Make sure you have hello `ios-sim` package installed toorun on hello emulator.</span></span> <span data-ttu-id="caa11-248">Per ulteriori informazioni, vedere la sezione Prerequisiti"hello" sezione.</span><span class="sxs-lookup"><span data-stu-id="caa11-248">For more information, see hello "Prerequisites" section.</span></span>

    Use `cordova run ios --list` toosee all available targets and `cordova run ios --target=<target_name>` toorun hello application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` toosee additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="caa11-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="caa11-249">Next steps</span></span>
<span data-ttu-id="caa11-250">Per riferimento, è disponibile in: esempio hello completata (senza i valori di configurazione) [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="caa11-250">For reference, hello completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="caa11-251">È possibile ora gli scenari di spostamento in toomore avanzate (e più interessante).</span><span class="sxs-lookup"><span data-stu-id="caa11-251">You can now move on toomore advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="caa11-252">Potrebbe essere necessario tootry: [proteggere un'API Web Node. js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="caa11-252">You might want tootry: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
