---
title: Introduzione a Cordova per Azure AD | Microsoft Docs
description: Come compilare un'applicazione Cordova che si integra con Azure AD per l'accesso e chiama le API protette di Azure AD usando OAuth.
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
ms.openlocfilehash: d9f53148787729d29a0a89cce1b8b2b83ba228f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="integrate-azure-ad-with-an-apache-cordova-app"></a><span data-ttu-id="b90ae-103">Integrare Azure AD con un'app Apache Cordova</span><span class="sxs-lookup"><span data-stu-id="b90ae-103">Integrate Azure AD with an Apache Cordova app</span></span>
[!INCLUDE [active-directory-devquickstarts-switcher](../../../includes/active-directory-devquickstarts-switcher.md)]

[!INCLUDE [active-directory-devguide](../../../includes/active-directory-devguide.md)]

<span data-ttu-id="b90ae-104">È possibile usare Apache Cordova per sviluppare applicazioni HTML5/JavaScript che possono essere eseguite su dispositivi mobili come applicazioni native complete.</span><span class="sxs-lookup"><span data-stu-id="b90ae-104">You can use Apache Cordova to develop HTML5/JavaScript applications that can run on mobile devices as full-fledged native applications.</span></span> <span data-ttu-id="b90ae-105">Con Azure Active Directory (Azure AD) è possibile aggiungere funzionalità di autenticazione di livello aziendale alle applicazioni Cordova.</span><span class="sxs-lookup"><span data-stu-id="b90ae-105">With Azure Active Directory (Azure AD), you can add enterprise-grade authentication capabilities to your Cordova applications.</span></span>

<span data-ttu-id="b90ae-106">Un plug-in Cordova esegue il wrapping di SDK nativi di Azure AD in iOS, Android, Windows Store e Windows Phone.</span><span class="sxs-lookup"><span data-stu-id="b90ae-106">A Cordova plug-in wraps Azure AD native SDKs on iOS, Android, Windows Store, and Windows Phone.</span></span> <span data-ttu-id="b90ae-107">Usando questo plug-in è possibile migliorare l'applicazione, in modo da supportare l'accesso con gli account Active Directory di Windows Server degli utenti, ottenere l'accesso alle API di Office 365 e Azure e contribuire alla protezione delle chiamate all'API Web personalizzata.</span><span class="sxs-lookup"><span data-stu-id="b90ae-107">By using that plug-in, you can enhance your application to support sign-in with your users' Windows Server Active Directory accounts, gain access to Office 365 and Azure APIs, and even help protect calls to your own custom web API.</span></span>

<span data-ttu-id="b90ae-108">In questa esercitazione viene usato il plug-in Apache Cordova per Active Directory Authentication Library (ADAL) per migliorare una semplice app aggiungendo le funzionalità seguenti:</span><span class="sxs-lookup"><span data-stu-id="b90ae-108">In this tutorial, we'll use the Apache Cordova plug-in for Active Directory Authentication Library (ADAL) to improve a simple app by adding the following features:</span></span>

* <span data-ttu-id="b90ae-109">Sono sufficienti poche righe di codice per autenticare un utente e ottenere un token.</span><span class="sxs-lookup"><span data-stu-id="b90ae-109">With just a few lines of code, authenticate a user and obtain a token.</span></span>
* <span data-ttu-id="b90ae-110">Usare il token per richiamare l'API Graph per eseguire query sulla directory e visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="b90ae-110">Use that token to invoke the Graph API to query that directory and display the results.</span></span>  
* <span data-ttu-id="b90ae-111">Usare la cache dei token di ADAL per ridurre al minimo le richieste di autenticazione per l'utente.</span><span class="sxs-lookup"><span data-stu-id="b90ae-111">Use the ADAL token cache to minimize authentication prompts for the user.</span></span>

<span data-ttu-id="b90ae-112">Per apportare i miglioramenti, è necessario eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="b90ae-112">To make those improvements, you need to:</span></span>

1. <span data-ttu-id="b90ae-113">Registrare un'applicazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b90ae-113">Register an application with Azure AD.</span></span>
2. <span data-ttu-id="b90ae-114">Aggiungere codice all'app per la richiesta di token.</span><span class="sxs-lookup"><span data-stu-id="b90ae-114">Add code to your app to request tokens.</span></span>
3. <span data-ttu-id="b90ae-115">Aggiungere codice per usare il token per eseguire query sull'API Graph e visualizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="b90ae-115">Add code to use the token for querying the Graph API and display results.</span></span>
4. <span data-ttu-id="b90ae-116">Creare il progetto di distribuzione di Cordova con tutte le piattaforme di destinazione desiderate e il plug-in ADAL per Cordova, quindi testare la soluzione negli emulatori.</span><span class="sxs-lookup"><span data-stu-id="b90ae-116">Create the Cordova deployment project with all the platforms you want to target, add the Cordova ADAL plug-in, and test the solution in emulators.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b90ae-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b90ae-117">Prerequisites</span></span>
<span data-ttu-id="b90ae-118">Per completare questa esercitazione, sono necessari:</span><span class="sxs-lookup"><span data-stu-id="b90ae-118">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="b90ae-119">Tenant di Azure AD nel quale è disponibile un account con diritti per lo sviluppo di app.</span><span class="sxs-lookup"><span data-stu-id="b90ae-119">An Azure AD tenant where you have an account with app development rights.</span></span>
* <span data-ttu-id="b90ae-120">Ambiente di sviluppo configurato per l'uso di Apache Cordova.</span><span class="sxs-lookup"><span data-stu-id="b90ae-120">A development environment that's configured to use Apache Cordova.</span></span>  

<span data-ttu-id="b90ae-121">Se entrambi questi elementi sono già configurati, andare direttamente al passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="b90ae-121">If you have both already set up, proceed directly to step 1.</span></span>

<span data-ttu-id="b90ae-122">Se non è disponibile un tenant di Azure AD, vedere le [istruzioni su come ottenerne uno](active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b90ae-122">If you don't have an Azure AD tenant, use the [instructions on how to get one](active-directory-howto-tenant.md).</span></span>

<span data-ttu-id="b90ae-123">Se nel computer in uso non è configurato Apache Cordova, installare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="b90ae-123">If you don't have Apache Cordova set up on your machine, install the following:</span></span>

* [<span data-ttu-id="b90ae-124">Git</span><span class="sxs-lookup"><span data-stu-id="b90ae-124">Git</span></span>](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
* [<span data-ttu-id="b90ae-125">Node.JS</span><span class="sxs-lookup"><span data-stu-id="b90ae-125">Node.js</span></span>](https://nodejs.org/download/)
* <span data-ttu-id="b90ae-126">[Interfaccia della riga di comando di Cordova](https://cordova.apache.org/) (può essere installata facilmente tramite Gestione pacchetti NPM: `npm install -g cordova`)</span><span class="sxs-lookup"><span data-stu-id="b90ae-126">[Cordova CLI](https://cordova.apache.org/) (can be easily installed via NPM package manager: `npm install -g cordova`)</span></span>

<span data-ttu-id="b90ae-127">Le installazioni precedenti dovrebbero funzionare sia su PC che su Mac.</span><span class="sxs-lookup"><span data-stu-id="b90ae-127">The preceding installations should work both on the PC and on the Mac.</span></span>

<span data-ttu-id="b90ae-128">Ogni piattaforma di destinazione ha prerequisiti diversi:</span><span class="sxs-lookup"><span data-stu-id="b90ae-128">Each target platform has different prerequisites:</span></span>

* <span data-ttu-id="b90ae-129">Per compilare ed eseguire un'app per Windows Tablet/PC o Windows Phone:</span><span class="sxs-lookup"><span data-stu-id="b90ae-129">To build and run an app for Windows Tablet/PC or Windows Phone:</span></span>
  * <span data-ttu-id="b90ae-130">Installare [Visual Studio 2013 per Windows con Update 2 o versione successiva](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express o altra versione) oppure [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span><span class="sxs-lookup"><span data-stu-id="b90ae-130">Install [Visual Studio 2013 for Windows with Update 2 or later](http://www.visualstudio.com/downloads/download-visual-studio-vs#d-express-windows-8) (Express or another version) or [Visual Studio 2015](https://www.visualstudio.com/downloads/download-visual-studio-vs#d-community).</span></span>

* <span data-ttu-id="b90ae-131">Per compilare ed eseguire un'app per iOS:</span><span class="sxs-lookup"><span data-stu-id="b90ae-131">To build and run an app for iOS:</span></span>

  * <span data-ttu-id="b90ae-132">Installare Xcode 6.x o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b90ae-132">Install Xcode 6.x or later.</span></span> <span data-ttu-id="b90ae-133">Scaricarlo dal [sito Apple Developer](http://developer.apple.com/downloads) o da [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span><span class="sxs-lookup"><span data-stu-id="b90ae-133">Download it from the [Apple Developer site](http://developer.apple.com/downloads) or the [Mac App Store](http://itunes.apple.com/us/app/xcode/id497799835?mt=12).</span></span>
  * <span data-ttu-id="b90ae-134">Installare [ios-sim](https://www.npmjs.org/package/ios-sim).</span><span class="sxs-lookup"><span data-stu-id="b90ae-134">Install [ios-sim](https://www.npmjs.org/package/ios-sim).</span></span> <span data-ttu-id="b90ae-135">È possibile usarlo per avviare le app iOS nel simulatore iOS dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="b90ae-135">You can use it to start iOS apps in iOS Simulator from the command line.</span></span> <span data-ttu-id="b90ae-136">È possibile installarlo con facilità tramite il terminale: `npm install -g ios-sim`.</span><span class="sxs-lookup"><span data-stu-id="b90ae-136">(You can easily install it via the terminal: `npm install -g ios-sim`.)</span></span>
* <span data-ttu-id="b90ae-137">Per compilare ed eseguire un'app per Android:</span><span class="sxs-lookup"><span data-stu-id="b90ae-137">To build and run an app for Android:</span></span>

  * <span data-ttu-id="b90ae-138">Installare [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="b90ae-138">Install [Java Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or later.</span></span> <span data-ttu-id="b90ae-139">Assicurarsi che la variabile di ambiente `JAVA_HOME` sia impostata correttamente in base al percorso di installazione di JDK, ad esempio, C:\Programmi\Java\jdk1.7.0_75.</span><span class="sxs-lookup"><span data-stu-id="b90ae-139">Make sure `JAVA_HOME` (environment variable) is correctly set according to the JDK installation path (for example, C:\Program Files\Java\jdk1.7.0_75).</span></span>
  * <span data-ttu-id="b90ae-140">Installare [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) e aggiungere il percorso `<android-sdk-location>\tools`, ad esempio C:\tools\Android\android-sdk\tools, alla variabile di ambiente `PATH`.</span><span class="sxs-lookup"><span data-stu-id="b90ae-140">Install [Android SDK](http://developer.android.com/sdk/installing/index.html?pkg=tools) and add the `<android-sdk-location>\tools` location (for example, C:\tools\Android\android-sdk\tools) to your `PATH` environment variable.</span></span>
  * <span data-ttu-id="b90ae-141">Aprire Android SDK Manager, ad esempio, tramite il terminale `android`, e installare:</span><span class="sxs-lookup"><span data-stu-id="b90ae-141">Open Android SDK Manager (for example, via the terminal: `android`) and install:</span></span>
    * <span data-ttu-id="b90ae-142">*Android 5.0.1 (API 21)* Platform SDK</span><span class="sxs-lookup"><span data-stu-id="b90ae-142">*Android 5.0.1 (API 21)* platform SDK</span></span>
    * <span data-ttu-id="b90ae-143">*Android SDK Build Tools* 19.1.0 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="b90ae-143">*Android SDK Build Tools* version 19.1.0 or later</span></span>
    * <span data-ttu-id="b90ae-144">*Android Support Repository* (funzionalità aggiuntive)</span><span class="sxs-lookup"><span data-stu-id="b90ae-144">*Android Support Repository* (Extras)</span></span>

  <span data-ttu-id="b90ae-145">Android SDK non fornisce alcuna istanza dell'emulatore predefinito.</span><span class="sxs-lookup"><span data-stu-id="b90ae-145">The Android SDK doesn't provide any default emulator instance.</span></span> <span data-ttu-id="b90ae-146">Crearne una eseguendo `android avd` dal terminale e quindi selezionare **Create** (Crea) per eseguire l'app Android nell'emulatore.</span><span class="sxs-lookup"><span data-stu-id="b90ae-146">Create one by running `android avd` from the terminal and then selecting **Create**, if you want to run the Android app on an emulator.</span></span> <span data-ttu-id="b90ae-147">È consigliabile usare un' API di livello 19 o superiore.</span><span class="sxs-lookup"><span data-stu-id="b90ae-147">We recommend an API level of 19 or higher.</span></span> <span data-ttu-id="b90ae-148">Per altre informazioni sull'emulatore Android e sulle opzioni di creazione, vedere [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) nel sito Android.</span><span class="sxs-lookup"><span data-stu-id="b90ae-148">For more information about the Android emulator and creation options, see [AVD Manager](http://developer.android.com/tools/help/avd-manager.html) on the Android site.</span></span>

## <a name="step-1-register-an-application-with-azure-ad"></a><span data-ttu-id="b90ae-149">Passaggio 1: Registrare un'applicazione con Azure AD</span><span class="sxs-lookup"><span data-stu-id="b90ae-149">Step 1: Register an application with Azure AD</span></span>
<span data-ttu-id="b90ae-150">Questo passaggio è facoltativo.</span><span class="sxs-lookup"><span data-stu-id="b90ae-150">This step is optional.</span></span> <span data-ttu-id="b90ae-151">L'esercitazione fornisce valori di cui è stato effettuato preventivamente il provisioning, che consentono di vedere l'esempio in azione senza effettuare alcun provisioning nel proprio tenant.</span><span class="sxs-lookup"><span data-stu-id="b90ae-151">This tutorial provides pre-provisioned values that you can use to see the sample in action without doing any provisioning in your own tenant.</span></span> <span data-ttu-id="b90ae-152">È tuttavia consigliabile eseguire questo passaggio e acquisire familiarità con il processo, perché sarà necessario quando si creano applicazioni personalizzate.</span><span class="sxs-lookup"><span data-stu-id="b90ae-152">However, we recommend that you do perform this step and become familiar with the process, because it will be required when you create your own applications.</span></span>

<span data-ttu-id="b90ae-153">Azure AD rilascia token solo alle applicazioni note.</span><span class="sxs-lookup"><span data-stu-id="b90ae-153">Azure AD issues tokens to only known applications.</span></span> <span data-ttu-id="b90ae-154">Prima di poter usare Azure AD dall'app, è necessario creare una voce nel proprio tenant.</span><span class="sxs-lookup"><span data-stu-id="b90ae-154">Before you can use Azure AD from your app, you need to create an entry for it in your tenant.</span></span> <span data-ttu-id="b90ae-155">Per registrare una nuova applicazione nel tenant:</span><span class="sxs-lookup"><span data-stu-id="b90ae-155">To register a new application in your tenant:</span></span>

1. <span data-ttu-id="b90ae-156">Accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b90ae-156">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b90ae-157">Nella barra superiore fare clic sull'account.</span><span class="sxs-lookup"><span data-stu-id="b90ae-157">On the top bar, click your account.</span></span> <span data-ttu-id="b90ae-158">Nell'elenco di **Directory** scegliere il tenant di Azure AD in cui si vuole registrare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b90ae-158">In the **Directory** list, choose the Azure AD tenant where you want to register your application.</span></span>
3. <span data-ttu-id="b90ae-159">Fare clic su **More Services** (Altri servizi) nel riquadro sinistro, quindi selezionare **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="b90ae-159">Click **More Services** in the left pane, and then select **Azure Active Directory**.</span></span>
4. <span data-ttu-id="b90ae-160">Fare clic su **Registrazioni per l'app**, quindi selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b90ae-160">Click **App registrations**, and then select **Add**.</span></span>
5. <span data-ttu-id="b90ae-161">Seguire le istruzioni e creare un'**Applicazione client nativa**.</span><span class="sxs-lookup"><span data-stu-id="b90ae-161">Follow the prompts and create a **Native Client Application**.</span></span> <span data-ttu-id="b90ae-162">Benché le app Cordova siano basate su HTML, verrà creata un'applicazione client nativa.</span><span class="sxs-lookup"><span data-stu-id="b90ae-162">(Although Cordova apps are HTML based, we're creating a native client application here.</span></span> <span data-ttu-id="b90ae-163">L'opzione **Applicazione client nativa** deve essere selezionata per consentire il funzionamento dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b90ae-163">The **Native Client Application** option must be selected, or the application won't work.)</span></span>
  * <span data-ttu-id="b90ae-164">**Nome** descrive l'applicazione agli utenti.</span><span class="sxs-lookup"><span data-stu-id="b90ae-164">**Name** describes your application to users.</span></span>
  * <span data-ttu-id="b90ae-165">**URI di reindirizzamento** è l'URI usato per restituire i token all'app.</span><span class="sxs-lookup"><span data-stu-id="b90ae-165">**Redirect URI** is the URI that's used to return tokens to your app.</span></span> <span data-ttu-id="b90ae-166">Immettere **http://MyDirectorySearcherApp**.</span><span class="sxs-lookup"><span data-stu-id="b90ae-166">Enter **http://MyDirectorySearcherApp**.</span></span>

<span data-ttu-id="b90ae-167">Al termine della registrazione, Azure AD assegna un ID applicazione univoco all'app.</span><span class="sxs-lookup"><span data-stu-id="b90ae-167">After you finish registration, Azure AD assigns a unique application ID to your app.</span></span> <span data-ttu-id="b90ae-168">Questo valore servirà nelle sezioni successive.</span><span class="sxs-lookup"><span data-stu-id="b90ae-168">You’ll need this value in the next sections.</span></span> <span data-ttu-id="b90ae-169">È possibile trovarlo nella scheda applicazione dell'app appena creata.</span><span class="sxs-lookup"><span data-stu-id="b90ae-169">You can find it on the application tab of the newly created app.</span></span>

<span data-ttu-id="b90ae-170">Per eseguire `DirSearchClient Sample`, assegnare all'app appena creata l'autorizzazione ad eseguire query nell'API Graph di Azure AD:</span><span class="sxs-lookup"><span data-stu-id="b90ae-170">To run `DirSearchClient Sample`, grant the newly created app permission to query the Azure AD Graph API:</span></span>

1. <span data-ttu-id="b90ae-171">Nella pagina **Impostazioni** selezionare **Autorizzazioni necessarie** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="b90ae-171">From the **Settings** page, select **Required Permissions**, and then select **Add**.</span></span>  
2. <span data-ttu-id="b90ae-172">Per l'applicazione Azure Active Directory, selezionare **Microsoft Graph** come API e aggiungere l'autorizzazione **Access the directory as the signed-in user** (Accesso alla directory come utente connesso) in **Autorizzazioni delegate**.</span><span class="sxs-lookup"><span data-stu-id="b90ae-172">For the Azure Active Directory application, select **Microsoft Graph** as the API and add the **Access the directory as the signed-in user** permission under **Delegated Permissions**.</span></span>  <span data-ttu-id="b90ae-173">In questo modo l'applicazione può cercare gli utenti nell'API Graph.</span><span class="sxs-lookup"><span data-stu-id="b90ae-173">This enables your application to query the Graph API for users.</span></span>

## <a name="step-2-clone-the-sample-app-repository"></a><span data-ttu-id="b90ae-174">Passaggio 2: Clonare il repository di app di esempio</span><span class="sxs-lookup"><span data-stu-id="b90ae-174">Step 2: Clone the sample app repository</span></span>
<span data-ttu-id="b90ae-175">Dalla shell o dalla riga di comando digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b90ae-175">From your shell or command line, type the following command:</span></span>

    git clone -b skeleton https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova.git

## <a name="step-3-create-the-cordova-app"></a><span data-ttu-id="b90ae-176">Passaggio 3: Creare l'app Cordova</span><span class="sxs-lookup"><span data-stu-id="b90ae-176">Step 3: Create the Cordova app</span></span>
<span data-ttu-id="b90ae-177">Esistono diversi metodi per la creazione di applicazioni Cordova.</span><span class="sxs-lookup"><span data-stu-id="b90ae-177">There are multiple ways to create Cordova applications.</span></span> <span data-ttu-id="b90ae-178">In questa esercitazione si userà l'interfaccia della riga di comando (CLI) di Cordova.</span><span class="sxs-lookup"><span data-stu-id="b90ae-178">In this tutorial, we'll use the Cordova command-line interface (CLI).</span></span>

1. <span data-ttu-id="b90ae-179">Dalla shell o dalla riga di comando digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b90ae-179">From your shell or command line, type the following command:</span></span>

        cordova create DirSearchClient

   <span data-ttu-id="b90ae-180">Questo comando crea la struttura di cartelle e lo scaffolding per il progetto Cordova.</span><span class="sxs-lookup"><span data-stu-id="b90ae-180">That command creates the folder structure and scaffolding for the Cordova project.</span></span>

2. <span data-ttu-id="b90ae-181">Passare alla nuova cartella DirSearchClient:</span><span class="sxs-lookup"><span data-stu-id="b90ae-181">Move to the new DirSearchClient folder:</span></span>

        cd .\DirSearchClient

3. <span data-ttu-id="b90ae-182">Copiare il contenuto del progetto di partenza nella sottocartella www usando File Manager o il comando seguente nella shell:</span><span class="sxs-lookup"><span data-stu-id="b90ae-182">Copy the content of the starter project in the www subfolder by using a file manager or the following command in your shell:</span></span>

  * <span data-ttu-id="b90ae-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span><span class="sxs-lookup"><span data-stu-id="b90ae-183">Windows: `xcopy ..\NativeClient-MultiTarget-Cordova\DirSearchClient www /E /Y`</span></span>
  * <span data-ttu-id="b90ae-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span><span class="sxs-lookup"><span data-stu-id="b90ae-184">Mac: `cp -r  ../NativeClient-MultiTarget-Cordova/DirSearchClient/* www`</span></span>

4. <span data-ttu-id="b90ae-185">Aggiungere il plug-in relativo all'elenco elementi consentiti.</span><span class="sxs-lookup"><span data-stu-id="b90ae-185">Add the whitelist plug-in.</span></span> <span data-ttu-id="b90ae-186">Questa operazione è necessaria per richiamare l'API Graph.</span><span class="sxs-lookup"><span data-stu-id="b90ae-186">This is necessary for invoking the Graph API.</span></span>

        cordova plugin add cordova-plugin-whitelist

5. <span data-ttu-id="b90ae-187">Aggiungere tutte le piattaforme che si prevede di supportare.</span><span class="sxs-lookup"><span data-stu-id="b90ae-187">Add all the platforms that you want to support.</span></span> <span data-ttu-id="b90ae-188">Per avere un esempio funzionante, è necessario eseguire almeno uno dei comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b90ae-188">To have a working sample, you need to execute at least one of the following commands.</span></span> <span data-ttu-id="b90ae-189">Si noti che non sarà possibile emulare iOS in Windows o emulare Windows in Mac.</span><span class="sxs-lookup"><span data-stu-id="b90ae-189">Note that you won't be able to emulate iOS on Windows or emulate Windows on a Mac.</span></span>

        cordova platform add android
        cordova platform add ios
        cordova platform add windows

6. <span data-ttu-id="b90ae-190">Aggiungere il plug-in ADAL per Cordova al progetto:</span><span class="sxs-lookup"><span data-stu-id="b90ae-190">Add the ADAL for Cordova plug-in to your project:</span></span>

        cordova plugin add cordova-plugin-ms-adal

## <a name="step-4-add-code-to-authenticate-users-and-obtain-tokens-from-azure-ad"></a><span data-ttu-id="b90ae-191">Passaggio 4: Aggiungere codice per autenticare gli utenti e ottenere i token da Azure AD</span><span class="sxs-lookup"><span data-stu-id="b90ae-191">Step 4: Add code to authenticate users and obtain tokens from Azure AD</span></span>
<span data-ttu-id="b90ae-192">L'applicazione sviluppata in questa esercitazione fornirà una semplice funzionalità di ricerca nella directory.</span><span class="sxs-lookup"><span data-stu-id="b90ae-192">The application that you're developing in this tutorial will provide a simple directory search feature.</span></span> <span data-ttu-id="b90ae-193">L'utente può quindi digitare l'alias di qualsiasi utente nella directory e visualizzare alcuni attributi di base.</span><span class="sxs-lookup"><span data-stu-id="b90ae-193">The user can then type the alias of any user in the directory and visualize some basic attributes.</span></span> <span data-ttu-id="b90ae-194">Il progetto iniziale contiene la definizione dell'interfaccia utente di base dell'app (in www/index.html) e lo scaffolding che collega i cicli degli eventi dell'app di base, i binding dell'interfaccia utente e la logica di visualizzazione dei risultati (in www/js/index.js).</span><span class="sxs-lookup"><span data-stu-id="b90ae-194">The starter project contains the definition of the basic user interface of the app (in www/index.html) and the scaffolding that wires up basic app event cycles, user interface bindings, and results display logic (in www/js/index.js).</span></span> <span data-ttu-id="b90ae-195">L'unica cosa affidata allo sviluppatore è l'aggiunta della logica che implementa le attività relative all'identità.</span><span class="sxs-lookup"><span data-stu-id="b90ae-195">The only task left for you is to add the logic that implements identity tasks.</span></span>

<span data-ttu-id="b90ae-196">La prima cosa da fare nel codice consiste nell'introdurre i valori di protocollo usati da Azure AD per l'identificazione dell'app e delle risorse di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b90ae-196">The first thing you need to do in your code is introduce the protocol values that Azure AD uses for identifying your app and the resources that you target.</span></span> <span data-ttu-id="b90ae-197">Questi valori verranno usati in seguito per costruire le richieste di token.</span><span class="sxs-lookup"><span data-stu-id="b90ae-197">Those values will be used to construct the token requests later on.</span></span> <span data-ttu-id="b90ae-198">Inserire il frammento seguente all'inizio del file index.js:</span><span class="sxs-lookup"><span data-stu-id="b90ae-198">Insert the following snippet at the top of the index.js file:</span></span>

```javascript
var authority = "https://login.microsoftonline.com/common",
    redirectUri = "http://MyDirectorySearcherApp",
    resourceUri = "https://graph.windows.net",
    clientId = "a5d92493-ae5a-4a9f-bcbf-9f1d354067d3",
    graphApiVersion = "2013-11-08";
```

<span data-ttu-id="b90ae-199">I valori `redirectUri` e `clientId` devono corrispondere ai valori che descrivono l'app in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="b90ae-199">The `redirectUri` and `clientId` values should match the values that describe your app in Azure AD.</span></span> <span data-ttu-id="b90ae-200">È possibile trovarli nella scheda **Configura** nel portale di Azure, come descritto in precedenza nel Passaggio 1 di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b90ae-200">You can find those from the **Configure** tab in the Azure portal, as described in step 1 earlier in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="b90ae-201">Se si è scelto di non registrare una nuova app nel tenant, è sufficiente incollare i valori preconfigurati senza modifica.</span><span class="sxs-lookup"><span data-stu-id="b90ae-201">If you opted for not registering a new app in your own tenant, you can simply paste the preconfigured values as is.</span></span> <span data-ttu-id="b90ae-202">È quindi possibile visualizzare l'esecuzione dell'esempio, anche se occorre creare sempre una voce personalizzata per le app destinate alla produzione.</span><span class="sxs-lookup"><span data-stu-id="b90ae-202">You can then see the sample running, though you should always create your own entry for your apps that are meant for production.</span></span>

<span data-ttu-id="b90ae-203">Aggiungere quindi il codice di richiesta del token.</span><span class="sxs-lookup"><span data-stu-id="b90ae-203">Next, add the token request code.</span></span> <span data-ttu-id="b90ae-204">Inserire il frammento seguente tra le definizioni `search`e `renderData`:</span><span class="sxs-lookup"><span data-stu-id="b90ae-204">Insert the following snippet between the `search` and `renderData` definitions:</span></span>

```javascript
    // Shows the user authentication dialog box if required
    authenticate: function (authCompletedCallback) {

        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
        });

    },
```
<span data-ttu-id="b90ae-205">Si esaminerà ora la funzione suddividendola nelle due parti principali.</span><span class="sxs-lookup"><span data-stu-id="b90ae-205">Let's examine that function by breaking it down in its two main parts.</span></span>
<span data-ttu-id="b90ae-206">Questo esempio è progettato per funzionare con qualsiasi tenant, invece di essere associato a uno in particolare.</span><span class="sxs-lookup"><span data-stu-id="b90ae-206">This sample is designed to work with any tenant, as opposed to being tied to a particular one.</span></span> <span data-ttu-id="b90ae-207">Usa l'endpoint "/common" che consente all'utente di immettere qualsiasi account al momento dell'autenticazione e indirizza la richiesta al tenant di appartenenza.</span><span class="sxs-lookup"><span data-stu-id="b90ae-207">It uses the "/common" endpoint, which allows the user to enter any account at authentication time and directs the request to the tenant where it belongs.</span></span>

<span data-ttu-id="b90ae-208">La prima parte del metodo esamina la cache ADAL per verificare se è già stato archiviato un token.</span><span class="sxs-lookup"><span data-stu-id="b90ae-208">This first part of the method inspects the ADAL cache to see if a token is already stored.</span></span> <span data-ttu-id="b90ae-209">In tale caso, il metodo usa i tenant di provenienza del token per la reinizializzazione di ADAL.</span><span class="sxs-lookup"><span data-stu-id="b90ae-209">If so, the method uses the tenants where the token came from for reinitializing ADAL.</span></span> <span data-ttu-id="b90ae-210">Questo approccio è necessario per evitare richieste aggiuntive, in quanto l'uso di "/common" comporta sempre la richiesta all'utente di immettere un nuovo account.</span><span class="sxs-lookup"><span data-stu-id="b90ae-210">This is necessary to avoid extra prompts, because the use of "/common" always results in asking the user to enter a new account.</span></span>

```javascript
        app.context = new Microsoft.ADAL.AuthenticationContext(authority);
        app.context.tokenCache.readItems().then(function (items) {
            if (items.length > 0) {
                authority = items[0].authority;
                app.context = new Microsoft.ADAL.AuthenticationContext(authority);
            }
```
<span data-ttu-id="b90ae-211">La seconda parte del metodo esegue la richiesta di token vera e propria.</span><span class="sxs-lookup"><span data-stu-id="b90ae-211">The second part of the method performs the proper token request.</span></span> <span data-ttu-id="b90ae-212">Il metodo `acquireTokenSilentAsync` chiede ad ADAL di restituire un token per la risorsa specificata senza mostrare alcuna esperienza utente.</span><span class="sxs-lookup"><span data-stu-id="b90ae-212">The `acquireTokenSilentAsync` method asks ADAL to return a token for the specified resource without showing any UX.</span></span> <span data-ttu-id="b90ae-213">Ciò può verificarsi se nella cache è già archiviato un token di accesso appropriato o se è presente un token di aggiornamento che può essere usato per ottenere un nuovo token di accesso senza mostrare alcuna richiesta.</span><span class="sxs-lookup"><span data-stu-id="b90ae-213">That can happen if the cache already has a suitable access token stored, or if a refresh token can be used to get a new access token without showing any prompt.</span></span> <span data-ttu-id="b90ae-214">Se il tentativo non riesce, si eseguirà il fallback a `acquireTokenAsync`, che richiederà in modo visibile all'utente di autenticarsi.</span><span class="sxs-lookup"><span data-stu-id="b90ae-214">If that attempt fails, we fall back on `acquireTokenAsync`--which will visibly prompt the user to authenticate.</span></span>

```javascript
            // Attempt to authorize the user silently
            app.context.acquireTokenSilentAsync(resourceUri, clientId)
            .then(authCompletedCallback, function () {
                // We require user credentials, so this triggers the authentication dialog box
                app.context.acquireTokenAsync(resourceUri, clientId, redirectUri)
                .then(authCompletedCallback, function (err) {
                    app.error("Failed to authenticate: " + err);
                });
            });
```
<span data-ttu-id="b90ae-215">Dopo avere ottenuto il token, si potrà finalmente richiamare l'API Graph ed eseguire la query di ricerca specifica.</span><span class="sxs-lookup"><span data-stu-id="b90ae-215">Now that we have the token, we can finally invoke the Graph API and perform the search query that we want.</span></span> <span data-ttu-id="b90ae-216">Inserire il frammento seguente sotto la definizione di `authenticate`:</span><span class="sxs-lookup"><span data-stu-id="b90ae-216">Insert the following snippet below the `authenticate` definition:</span></span>

```javascript
// Makes an API call to receive the user list
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
<span data-ttu-id="b90ae-217">I file usati come punto di partenza hanno fornito un'esperienza utente essenziale per l'immissione dell'alias di un utente in una casella di testo.</span><span class="sxs-lookup"><span data-stu-id="b90ae-217">The starting-point files supplied a simple UX for entering a user's alias in a text box.</span></span> <span data-ttu-id="b90ae-218">Questo metodo usa tale valore per costruire una query, combinarla con il token di accesso, inviarla a Microsoft Graph e analizzare i risultati.</span><span class="sxs-lookup"><span data-stu-id="b90ae-218">This method uses that value to construct a query, combine it with the access token, send it to Microsoft Graph, and parse the results.</span></span> <span data-ttu-id="b90ae-219">Il metodo `renderData`, già presente nel file usato come punto di partenza, si occupa della visualizzazione dei risultati.</span><span class="sxs-lookup"><span data-stu-id="b90ae-219">The `renderData` method, already present in the starting-point file, takes care of visualizing the results.</span></span>

## <a name="step-5-run-the-app"></a><span data-ttu-id="b90ae-220">Passaggio 5: Eseguire l'app</span><span class="sxs-lookup"><span data-stu-id="b90ae-220">Step 5: Run the app</span></span>
<span data-ttu-id="b90ae-221">L'app è finalmente pronta per essere eseguita.</span><span class="sxs-lookup"><span data-stu-id="b90ae-221">Your app is finally ready to run.</span></span> <span data-ttu-id="b90ae-222">Il funzionamento è semplice: dopo l'avvio dell'app, immettere l'alias dell'utente che si vuole cercare, quindi fare clic sul pulsante.</span><span class="sxs-lookup"><span data-stu-id="b90ae-222">Operating it is simple: when the app starts, enter the alias of the user you want to look up, and then click the button.</span></span> <span data-ttu-id="b90ae-223">Viene richiesto di autenticarsi.</span><span class="sxs-lookup"><span data-stu-id="b90ae-223">You're prompted for authentication.</span></span> <span data-ttu-id="b90ae-224">Dopo l'autenticazione e il completamento della ricerca, vengono visualizzati gli attributi relativi all'utente cercato.</span><span class="sxs-lookup"><span data-stu-id="b90ae-224">Upon successful authentication and successful search, the attributes of the searched user are displayed.</span></span>

<span data-ttu-id="b90ae-225">Le esecuzioni successive verranno eseguite senza visualizzare alcuna richiesta, grazie alla presenza nella cache del token acquisito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b90ae-225">Subsequent runs will perform the search without showing any prompt, thanks to the presence of the previously acquired token in cache.</span></span>

<span data-ttu-id="b90ae-226">I passaggi concreti per l'esecuzione dell'app variano in base alla piattaforma.</span><span class="sxs-lookup"><span data-stu-id="b90ae-226">The concrete steps for running the app vary by platform.</span></span>

### <a name="windows-10"></a><span data-ttu-id="b90ae-227">Windows 10</span><span class="sxs-lookup"><span data-stu-id="b90ae-227">Windows 10</span></span>
   <span data-ttu-id="b90ae-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span><span class="sxs-lookup"><span data-stu-id="b90ae-228">Tablet/PC: `cordova run windows --archs=x64 -- --appx=uap`</span></span>

   <span data-ttu-id="b90ae-229">Dispositivi mobili (richiede un dispositivo Windows 10 Mobile connesso a un PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span><span class="sxs-lookup"><span data-stu-id="b90ae-229">Mobile (requires a Windows 10 Mobile device connected to a PC): `cordova run windows --archs=arm -- --appx=uap --phone`</span></span>

   > [!NOTE]
   > <span data-ttu-id="b90ae-230">Durante la prima esecuzione è possibile che venga richiesto di accedere per ottenere una licenza per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="b90ae-230">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="b90ae-231">Per altre informazioni, vedere [Licenza per sviluppatori](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="b90ae-231">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-81-tabletpc"></a><span data-ttu-id="b90ae-232">Tablet/PC con Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="b90ae-232">Windows 8.1 Tablet/PC</span></span>
   `cordova run windows`

   > [!NOTE]
   > <span data-ttu-id="b90ae-233">Durante la prima esecuzione è possibile che venga richiesto di accedere per ottenere una licenza per sviluppatori.</span><span class="sxs-lookup"><span data-stu-id="b90ae-233">During the first run, you might be asked to sign in for a developer license.</span></span> <span data-ttu-id="b90ae-234">Per altre informazioni, vedere [Licenza per sviluppatori](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span><span class="sxs-lookup"><span data-stu-id="b90ae-234">For more information, see [Developer license](https://msdn.microsoft.com/library/windows/apps/hh974578.aspx).</span></span>

### <a name="windows-phone-81"></a><span data-ttu-id="b90ae-235">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="b90ae-235">Windows Phone 8.1</span></span>
   <span data-ttu-id="b90ae-236">Per l'esecuzione su un dispositivo connesso: `cordova run windows --device -- --phone`</span><span class="sxs-lookup"><span data-stu-id="b90ae-236">To run on a connected device: `cordova run windows --device -- --phone`</span></span>

   <span data-ttu-id="b90ae-237">Per l'esecuzione nell'emulatore predefinito: `cordova emulate windows -- --phone`</span><span class="sxs-lookup"><span data-stu-id="b90ae-237">To run on the default emulator: `cordova emulate windows -- --phone`</span></span>

   <span data-ttu-id="b90ae-238">Usare `cordova run windows --list -- --phone` per vedere tutte le destinazioni disponibili e `cordova run windows --target=<target_name> -- --phone` per eseguire l'applicazione su un dispositivo o un emulatore specifico, ad esempio, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`.</span><span class="sxs-lookup"><span data-stu-id="b90ae-238">Use `cordova run windows --list -- --phone` to see all available targets and `cordova run windows --target=<target_name> -- --phone` to run the application on a specific device or emulator (for example, `cordova run windows --target="Emulator 8.1 720P 4.7 inch" -- --phone`).</span></span>

### <a name="android"></a><span data-ttu-id="b90ae-239">Android</span><span class="sxs-lookup"><span data-stu-id="b90ae-239">Android</span></span>
   <span data-ttu-id="b90ae-240">Per l'esecuzione su un dispositivo connesso: `cordova run android --device`</span><span class="sxs-lookup"><span data-stu-id="b90ae-240">To run on a connected device: `cordova run android --device`</span></span>

   <span data-ttu-id="b90ae-241">Per l'esecuzione nell'emulatore predefinito: `cordova emulate android`</span><span class="sxs-lookup"><span data-stu-id="b90ae-241">To run on the default emulator: `cordova emulate android`</span></span>

   <span data-ttu-id="b90ae-242">Assicurarsi di avere creato l'istanza dell'emulatore con AVD Manager, come indicato nella sezione Prerequisiti.</span><span class="sxs-lookup"><span data-stu-id="b90ae-242">Make sure you've created an emulator instance by using AVD Manager, as described earlier in the "Prerequisites" section.</span></span>

   <span data-ttu-id="b90ae-243">Usare `cordova run android --list` per vedere tutte le destinazioni disponibili e `cordova run android --target=<target_name>` per eseguire l'applicazione su un dispositivo o un emulatore specifico, ad esempio, `cordova run android --target="Nexus4_emulator"`.</span><span class="sxs-lookup"><span data-stu-id="b90ae-243">Use `cordova run android --list` to see all available targets and `cordova run android --target=<target_name>` to run the application on a specific device or emulator (for example, `cordova run android --target="Nexus4_emulator"`).</span></span>

### <a name="ios"></a><span data-ttu-id="b90ae-244">iOS</span><span class="sxs-lookup"><span data-stu-id="b90ae-244">iOS</span></span>
   <span data-ttu-id="b90ae-245">Per l'esecuzione su un dispositivo connesso: `cordova run ios --device`</span><span class="sxs-lookup"><span data-stu-id="b90ae-245">To run on a connected device: `cordova run ios --device`</span></span>

   <span data-ttu-id="b90ae-246">Per l'esecuzione nell'emulatore predefinito: `cordova emulate ios`</span><span class="sxs-lookup"><span data-stu-id="b90ae-246">To run on the default emulator: `cordova emulate ios`</span></span>

   > [!NOTE]
   > <span data-ttu-id="b90ae-247">Assicurarsi che il pacchetto `ios-sim` sia installato per l'esecuzione sull'emulatore.</span><span class="sxs-lookup"><span data-stu-id="b90ae-247">Make sure you have the `ios-sim` package installed to run on the emulator.</span></span> <span data-ttu-id="b90ae-248">Per altre informazioni, vedere la sezione "Prerequisiti".</span><span class="sxs-lookup"><span data-stu-id="b90ae-248">For more information, see the "Prerequisites" section.</span></span>

    Use `cordova run ios --list` to see all available targets and `cordova run ios --target=<target_name>` to run the application on specific device or emulator (for example, `cordova run android --target="iPhone-6"`).

    Use `cordova run --help` to see additional build and run options.

## <a name="next-steps"></a><span data-ttu-id="b90ae-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b90ae-249">Next steps</span></span>
<span data-ttu-id="b90ae-250">Come riferimento, l'esempio completo, senza valori di configurazione, è disponibile in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span><span class="sxs-lookup"><span data-stu-id="b90ae-250">For reference, the completed sample (without your configuration values) is available in [GitHub](https://github.com/AzureADQuickStarts/NativeClient-MultiTarget-Cordova/tree/complete/DirSearchClient).</span></span>

<span data-ttu-id="b90ae-251">A questo punto è possibile passare a scenari più avanzati e più interessanti.</span><span class="sxs-lookup"><span data-stu-id="b90ae-251">You can now move on to more advanced (and more interesting) scenarios.</span></span> <span data-ttu-id="b90ae-252">Vedere [Proteggere un'API Web Node.js con Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b90ae-252">You might want to try: [Secure a Node.js Web API with Azure AD](active-directory-devquickstarts-webapi-nodejs.md).</span></span>

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
