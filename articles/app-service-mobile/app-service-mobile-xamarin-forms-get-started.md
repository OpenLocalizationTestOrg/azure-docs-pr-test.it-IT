---
title: Introduzione alle app per dispositivi mobili in Xamarin.Forms
description: Seguire questa esercitazione per iniziare a usare le app per dispositivi mobili per lo sviluppo per Xamarin.Forms.
services: app-service\mobile
documentationcenter: xamarin
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 5e692220-cc89-4548-96c8-35259722acf5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ee12caaad4095cff6dae3282f747ae804f93db81
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="dbde6-103">Creare un'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="dbde6-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="dbde6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="dbde6-104">Overview</span></span>
<span data-ttu-id="dbde6-105">Questa esercitazione illustra come aggiungere un servizio back-end basato sul cloud a un'app per dispositivi mobili Xamarin.Forms mediante la funzionalità App per dispositivi mobili del Servizio app di Azure come back-end.</span><span class="sxs-lookup"><span data-stu-id="dbde6-105">This tutorial shows you how to add a cloud-based back-end service to a Xamarin.Forms mobile app by using the Mobile Apps feature of Azure App Service as the back end.</span></span> <span data-ttu-id="dbde6-106">Vengono creati un nuovo back-end di app per dispositivi mobili e una semplice app Xamarin.Forms di tipo elenco attività che archivia dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbde6-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="dbde6-107">Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni relative alle app per dispositivi mobili per Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="dbde6-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dbde6-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="dbde6-108">Prerequisites</span></span>
<span data-ttu-id="dbde6-109">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="dbde6-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="dbde6-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="dbde6-110">An active Azure account.</span></span> <span data-ttu-id="dbde6-111">Se non è disponibile un account, è possibile iscriversi per accedere a una versione di valutazione di Azure e ottenere un massimo di 10 app per dispositivi mobili gratuite che potranno essere usate anche dopo il termine del periodo di valutazione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-111">If you don't have an account, you can sign up for an Azure trial and get up to 10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="dbde6-112">Per altre informazioni, vedere [Versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="dbde6-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="dbde6-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="dbde6-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="dbde6-114">Per informazioni, vedere la pagina [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbde6-114">For information, see the [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="dbde6-115">Un computer Mac in cui siano stati installati Xcode v7.0 o versione successiva e Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="dbde6-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="dbde6-116">Per informazioni, vedere [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="dbde6-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="dbde6-117">Creare un nuovo back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="dbde6-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="dbde6-118">Per creare un nuovo back-end di App per dispositivi mobili, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dbde6-118">To create a new Mobile Apps back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="dbde6-119">È stato configurato un back-end di App per dispositivi mobili che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="dbde6-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="dbde6-120">Scaricare quindi in progetto server per un semplice back-end di tipo elenco attività e pubblicarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbde6-120">Next, you download a server project for a simple to-do list back end and then publish it to Azure.</span></span>

## <a name="configure-the-server-project"></a><span data-ttu-id="dbde6-121">Configurare il progetto server</span><span class="sxs-lookup"><span data-stu-id="dbde6-121">Configure the server project</span></span>

<span data-ttu-id="dbde6-122">Per configurare il progetto server per l'uso del back-end Node.js o .NET, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dbde6-122">To configure the server project to use either the Node.js or .NET back end, do the following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-the-xamarinforms-solution"></a><span data-ttu-id="dbde6-123">Scaricare ed eseguire la soluzione Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="dbde6-123">Download and run the Xamarin.Forms solution</span></span>

<span data-ttu-id="dbde6-124">È possibile scaricare la soluzione in due modi.</span><span class="sxs-lookup"><span data-stu-id="dbde6-124">You can download the solution in either of two ways.</span></span> <span data-ttu-id="dbde6-125">Scaricarla in un computer Mac e aprirla in Xamarin Studio oppure scaricarla in un computer Windows e aprirla in Visual Studio usando un computer Mac connesso alla rete per la compilazione dell'app iOS.</span><span class="sxs-lookup"><span data-stu-id="dbde6-125">Download it to a Mac and open it in Xamarin Studio, or download it to a Windows computer and open it in Visual Studio by using a networked Mac for building the iOS app.</span></span> <span data-ttu-id="dbde6-126">Per altre informazioni, vedere [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="dbde6-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="dbde6-127">In un computer Mac o Windows seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="dbde6-127">On a Mac or Windows computer, do the following:</span></span>

1. <span data-ttu-id="dbde6-128">Accedere al [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="dbde6-128">Go to the [Azure portal].</span></span>

2. <span data-ttu-id="dbde6-129">Nel pannello **Impostazioni** per l'app per dispositivi mobili in **Dispositivi mobili** selezionare **Introduzione** > **Xamarin.Forms**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-129">On the **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="dbde6-130">In **Passaggio 3** selezionare  **Crea una nuova app** e quindi selezionare **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="dbde6-131">Questa azione scarica un progetto che contiene un'applicazione client connessa all'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="dbde6-131">This action downloads a project that contains a client application that's connected to your mobile app.</span></span> <span data-ttu-id="dbde6-132">Salvare il file del progetto compresso nel computer locale e prendere nota del percorso.</span><span class="sxs-lookup"><span data-stu-id="dbde6-132">Save the compressed project file to your local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="dbde6-133">Estrarre il progetto scaricato e aprirlo in Xamarin Studio (Mac) o in Visual Studio (Windows).</span><span class="sxs-lookup"><span data-stu-id="dbde6-133">Extract the project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Progetto estratto in Xamarin Studio][9]

   ![Progetto estratto in Visual Studio][8]

## <a name="optional-run-the-ios-project"></a><span data-ttu-id="dbde6-136">(Facoltativo) Eseguire il progetto iOS</span><span class="sxs-lookup"><span data-stu-id="dbde6-136">(Optional) Run the iOS project</span></span>
<span data-ttu-id="dbde6-137">In questa sezione viene eseguito il progetto iOS per Xamarin per dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="dbde6-137">In this section, you run the Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="dbde6-138">Se non si usano dispositivi iOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="dbde6-139">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="dbde6-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="dbde6-140">Fare clic con il pulsante destro del mouse sul progetto iOS e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-140">Right-click the iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="dbde6-141">Scegliere **Start Debugging** (Avvia debug) dal menu **Run** (Esegui) per compilare il progetto e avviare l'app nell'emulatore iPhone.</span><span class="sxs-lookup"><span data-stu-id="dbde6-141">On the **Run** menu, select **Start Debugging** to build the project and start the app in the iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="dbde6-142">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dbde6-142">In Visual Studio</span></span>
1. <span data-ttu-id="dbde6-143">Fare clic con il pulsante destro del mouse sul progetto iOS e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-143">Right-click the iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="dbde6-144">Scegliere **Configuration Manager** dal menu **Compila**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-144">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="dbde6-145">Nella finestra di dialogo **Configuration Manager** selezionare le caselle di controllo **Compila** e **Distribuisci** accanto al progetto iOS.</span><span class="sxs-lookup"><span data-stu-id="dbde6-145">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the iOS project.</span></span>

4. <span data-ttu-id="dbde6-146">Per compilare il progetto e avviare l'app nell'emulatore iPhone, premere il tasto **F5**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-146">To build the project and start the app in the iPhone emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbde6-147">In caso di problemi di compilazione del progetto, eseguire Gestione pacchetti NuGet ed effettuare l'aggiornamento alla versione più recente dei pacchetti per il supporto Xamarin.</span><span class="sxs-lookup"><span data-stu-id="dbde6-147">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="dbde6-148">L'aggiornamento alle versioni più recenti per i progetti di avvio rapido potrebbe risultare lento.</span><span class="sxs-lookup"><span data-stu-id="dbde6-148">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="dbde6-149">Nell'app digitare un testo significativo, ad esempio *Learn Xamarin*, e quindi selezionare il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="dbde6-149">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="dbde6-150">Questa azione invia una richiesta POST al nuovo back-end di App per dispositivi mobili ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbde6-150">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="dbde6-151">I dati della richiesta vengono inseriti nella tabella TodoItem.</span><span class="sxs-lookup"><span data-stu-id="dbde6-151">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="dbde6-152">Gli elementi archiviati nella tabella vengono restituiti dal back-end di App per dispositivi mobili e i dati vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="dbde6-152">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dbde6-153">Il codice che accede al back-end di App per dispositivi mobili è disponibile nel file TodoItemManager.cs C# del progetto di libreria di classi portabile della soluzione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-153">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-android-project"></a><span data-ttu-id="dbde6-154">(Facoltativo) Eseguire il progetto Android</span><span class="sxs-lookup"><span data-stu-id="dbde6-154">(Optional) Run the Android project</span></span>
<span data-ttu-id="dbde6-155">In questa sezione viene eseguito il progetto Xamarin droid per Android.</span><span class="sxs-lookup"><span data-stu-id="dbde6-155">In this section, you run the Xamarin droid project for Android.</span></span> <span data-ttu-id="dbde6-156">Se non si usano dispositivi Android, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="dbde6-157">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="dbde6-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="dbde6-158">Fare clic con il pulsante destro del mouse sul progetto Android e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-158">Right-click the Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="dbde6-159">Per compilare il progetto e avviare l'app in un emulatore Android, dal menu **Run** (Esegui) scegliere **Start Debugging** (Avvia debug).</span><span class="sxs-lookup"><span data-stu-id="dbde6-159">To build the project and start the app in an Android emulator, on the **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="dbde6-160">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dbde6-160">In Visual Studio</span></span>

1. <span data-ttu-id="dbde6-161">Fare clic con il pulsante destro del mouse sul progetto Android (Droid) e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-161">Right-click the Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="dbde6-162">Scegliere **Configuration Manager** dal menu **Compila**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-162">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="dbde6-163">Nella finestra di dialogo **Configuration Manager** selezionare le caselle di controllo **Compila** e **Distribuisci** accanto al progetto Android.</span><span class="sxs-lookup"><span data-stu-id="dbde6-163">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Android project.</span></span>

4. <span data-ttu-id="dbde6-164">Per compilare il progetto e avviare l'app in un emulatore Android, fare clic sul tasto **F5**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-164">To build the project and start the app in an Android emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbde6-165">In caso di problemi di compilazione del progetto, eseguire Gestione pacchetti NuGet ed effettuare l'aggiornamento alla versione più recente dei pacchetti per il supporto Xamarin.</span><span class="sxs-lookup"><span data-stu-id="dbde6-165">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="dbde6-166">L'aggiornamento alle versioni più recenti per i progetti di avvio rapido potrebbe risultare lento.</span><span class="sxs-lookup"><span data-stu-id="dbde6-166">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="dbde6-167">Nell'app digitare un testo significativo, ad esempio *Learn Xamarin*, e quindi selezionare il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="dbde6-167">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="dbde6-168">Questa azione invia una richiesta POST al nuovo back-end di App per dispositivi mobili ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbde6-168">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="dbde6-169">I dati della richiesta vengono inseriti nella tabella TodoItem.</span><span class="sxs-lookup"><span data-stu-id="dbde6-169">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="dbde6-170">Gli elementi archiviati nella tabella vengono restituiti dal back-end di App per dispositivi mobili e i dati vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="dbde6-170">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="dbde6-171">Il codice che accede al back-end di App per dispositivi mobili è disponibile nel file TodoItemManager.cs C# del progetto di libreria di classi portabile della soluzione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-171">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-the-windows-project"></a><span data-ttu-id="dbde6-172">(Facoltativo) Eseguire il progetto Windows</span><span class="sxs-lookup"><span data-stu-id="dbde6-172">(Optional) Run the Windows project</span></span>

<span data-ttu-id="dbde6-173">In questa sezione viene eseguito il progetto Xamarin WinApp per dispositivi Windows.</span><span class="sxs-lookup"><span data-stu-id="dbde6-173">In this section, you run the Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="dbde6-174">Se non si usano dispositivi Windows, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="dbde6-175">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dbde6-175">In Visual Studio</span></span>

1. <span data-ttu-id="dbde6-176">Fare clic con il pulsante destro del mouse sul progetto Windows e quindi scegliere **Imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-176">Right-click any of the Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="dbde6-177">Scegliere **Configuration Manager** dal menu **Compila**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-177">On the **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="dbde6-178">Nella finestra di dialogo **Configuration Manager** selezionare le caselle di controllo **Compila** e **Distribuisci** accanto al progetto Windows scelto.</span><span class="sxs-lookup"><span data-stu-id="dbde6-178">In the **Configuration Manager** dialog box, select the **Build** and **Deploy** check boxes next to the Windows project that you chose.</span></span>

4. <span data-ttu-id="dbde6-179">Per compilare il progetto e avviare l'app nell'emulatore Windows, premere il tasto **F5**.</span><span class="sxs-lookup"><span data-stu-id="dbde6-179">To build the project and start the app in a Windows emulator, select the **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="dbde6-180">In caso di problemi di compilazione del progetto, eseguire Gestione pacchetti NuGet ed effettuare l'aggiornamento alla versione più recente dei pacchetti per il supporto Xamarin.</span><span class="sxs-lookup"><span data-stu-id="dbde6-180">If you have problems building the project, run the NuGet package manager and update to the latest version of the Xamarin support packages.</span></span> <span data-ttu-id="dbde6-181">L'aggiornamento alle versioni più recenti per i progetti di avvio rapido potrebbe risultare lento.</span><span class="sxs-lookup"><span data-stu-id="dbde6-181">Quickstart projects might be slow to update to the latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="dbde6-182">Nell'app digitare un testo significativo, ad esempio *Learn Xamarin*, e quindi selezionare il segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="dbde6-182">In the app, type meaningful text, such as *Learn Xamarin*, and then select the plus sign (**+**).</span></span>

    <span data-ttu-id="dbde6-183">Questa azione invia una richiesta POST al nuovo back-end di App per dispositivi mobili ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="dbde6-183">This action sends a post request to the new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="dbde6-184">I dati della richiesta vengono inseriti nella tabella TodoItem.</span><span class="sxs-lookup"><span data-stu-id="dbde6-184">Data from the request is inserted into the TodoItem table.</span></span> <span data-ttu-id="dbde6-185">Gli elementi archiviati nella tabella vengono restituiti dal back-end di App per dispositivi mobili e i dati vengono visualizzati nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="dbde6-185">Items that are stored in the table are returned by the Mobile Apps back end, and the data is displayed in the list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="dbde6-186">Il codice che accede al back-end di App per dispositivi mobili è disponibile nel file TodoItemManager.cs C# del progetto di libreria di classi portabile della soluzione.</span><span class="sxs-lookup"><span data-stu-id="dbde6-186">You'll find the code that accesses your Mobile Apps back end in the TodoItemManager.cs C# file of the portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="dbde6-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dbde6-187">Next steps</span></span>

* [<span data-ttu-id="dbde6-188">Aggiungere l'autenticazione all'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="dbde6-188">Add authentication to your app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="dbde6-189">: informazioni sull'autenticazione degli utenti dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="dbde6-189">Learn how to authenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="dbde6-190">Aggiungere notifiche push all'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="dbde6-190">Add push notifications to your app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="dbde6-191">Informazioni su come aggiungere il supporto per le notifiche push all'app e configurare il back-end dell'app per dispositivi mobili per usare Hub di notifica di Azure per l'invio di notifiche push.</span><span class="sxs-lookup"><span data-stu-id="dbde6-191">Learn how to add push notifications support to your app and configure your Mobile Apps back end to use Azure Notification Hubs to send the push notifications.</span></span>

* [<span data-ttu-id="dbde6-192">Abilitare la sincronizzazione offline per l'app per dispositivi mobili Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="dbde6-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="dbde6-193">Informazioni su come aggiungere il supporto offline all'app usando il back-end di un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="dbde6-193">Learn how to add offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="dbde6-194">La sincronizzazione offline consente di visualizzare, aggiungere o modificare i dati dell'app per dispositivi mobili, anche se non è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="dbde6-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="dbde6-195">Usare il client gestito per le App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="dbde6-195">Use the managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="dbde6-196">: informazioni su come usare l'SDK del client gestito nell'app Xamarin.</span><span class="sxs-lookup"><span data-stu-id="dbde6-196">Learn how to work with the managed client SDK in your Xamarin app.</span></span>

<!-- Anchors. -->
[Get started with Mobile Apps back ends]:#getting-started
[Create a new Mobile Apps back end]:#create-new-service
[Next steps]:#next-steps


<!-- Images. -->
[6]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart.png
[8]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-vs.png
[9]: ./media/app-service-mobile-xamarin-forms-get-started/xamarin-forms-quickstart-xs.png
[10]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-ios.png
[11]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-android.png
[12]: ./media/app-service-mobile-xamarin-forms-get-started/mobile-quickstart-startup-windows.png


<!-- URLs. -->
[Visual Studio Professional 2013]: https://go.microsoft.com/fwLink/p/?LinkID=257546
[Mobile app SDK]: http://go.microsoft.com/fwlink/?LinkId=257545
[portale di Azure]: https://portal.azure.com/
