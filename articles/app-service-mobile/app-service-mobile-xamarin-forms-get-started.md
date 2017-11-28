---
title: aaaGet avviato con l'App per dispositivi mobili con xamarin. Forms
description: Seguire questa esercitazione toostart tramite App per dispositivi mobili per lo sviluppo di xamarin. Forms
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
ms.openlocfilehash: af6b1c1ce4cf91c397552aa3d8ee40728129238c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-xamarinforms-app"></a><span data-ttu-id="2f2b2-103">Creare un'app Xamarin.Forms</span><span class="sxs-lookup"><span data-stu-id="2f2b2-103">Create a Xamarin.Forms app</span></span>
[!INCLUDE [app-service-mobile-selector-get-started](../../includes/app-service-mobile-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="2f2b2-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2f2b2-104">Overview</span></span>
<span data-ttu-id="2f2b2-105">Questa esercitazione viene illustrato come una servizio back-end basato su cloud tooa xamarin. Forms app per dispositivi mobili utilizzando tooadd hello funzionalità delle App per dispositivi mobili del servizio App di Azure come back-end hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-105">This tutorial shows you how tooadd a cloud-based back-end service tooa Xamarin.Forms mobile app by using hello Mobile Apps feature of Azure App Service as hello back end.</span></span> <span data-ttu-id="2f2b2-106">Vengono creati un nuovo back-end di app per dispositivi mobili e una semplice app Xamarin.Forms di tipo elenco attività che archivia dati delle app in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-106">You create both a new Mobile Apps back end and a simple to-do list Xamarin.Forms app that stores app data in Azure.</span></span>

<span data-ttu-id="2f2b2-107">Il completamento di questa esercitazione è un prerequisito per tutte le altre esercitazioni relative alle app per dispositivi mobili per Xamarin.Forms.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-107">Completing this tutorial is a prerequisite for all other Mobile Apps tutorials for Xamarin.Forms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f2b2-108">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f2b2-108">Prerequisites</span></span>
<span data-ttu-id="2f2b2-109">toocomplete questa esercitazione, è necessario hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f2b2-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="2f2b2-110">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-110">An active Azure account.</span></span> <span data-ttu-id="2f2b2-111">Se non si dispone di un account, è possibile iscriversi a una versione di valutazione di Azure e iniziare a too10 libero App per dispositivi mobili che è possibile continuare a usare anche il termine di valutazione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-111">If you don't have an account, you can sign up for an Azure trial and get up too10 free mobile apps that you can keep using even after your trial ends.</span></span> <span data-ttu-id="2f2b2-112">Per altre informazioni, vedere [Versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-112">For more information, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="2f2b2-113">Visual Studio con Xamarin.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-113">Visual Studio with Xamarin.</span></span> <span data-ttu-id="2f2b2-114">Per informazioni, vedere hello [impostare backup e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-114">For information, see hello [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) page.</span></span>

* <span data-ttu-id="2f2b2-115">Un computer Mac in cui siano stati installati Xcode v7.0 o versione successiva e Xamarin Studio Community.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-115">A Mac with Xcode v7.0 or later and Xamarin Studio Community installed.</span></span> <span data-ttu-id="2f2b2-116">Per informazioni, vedere [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) e [Configurazione, installazione e verifiche per gli utenti Mac](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-116">For information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx) and [Set up, install, and verify for Mac users](https://msdn.microsoft.com/library/mt488770.aspx) (MSDN).</span></span>

## <a name="create-a-new-mobile-apps-back-end"></a><span data-ttu-id="2f2b2-117">Creare un nuovo back-end di App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="2f2b2-117">Create a new Mobile Apps back end</span></span>

<span data-ttu-id="2f2b2-118">toocreate terminare una nuova App per dispositivi mobili nuovamente, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f2b2-118">toocreate a new Mobile Apps back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-dotnet-backend-create-new-service](../../includes/app-service-mobile-dotnet-backend-create-new-service.md)]

<span data-ttu-id="2f2b2-119">È stato configurato un back-end di App per dispositivi mobili che può essere usato dalle applicazioni client per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-119">You have now set up a Mobile Apps back end that your mobile client applications can use.</span></span> <span data-ttu-id="2f2b2-120">Successivamente, si scarica un progetto server per un back-end di elenco semplice di attività da eseguire e quindi pubblicarlo tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-120">Next, you download a server project for a simple to-do list back end and then publish it tooAzure.</span></span>

## <a name="configure-hello-server-project"></a><span data-ttu-id="2f2b2-121">Configurare il progetto server di hello</span><span class="sxs-lookup"><span data-stu-id="2f2b2-121">Configure hello server project</span></span>

<span data-ttu-id="2f2b2-122">tooconfigure hello server progetto toouse in hello Node.js o .NET back-end, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f2b2-122">tooconfigure hello server project toouse either hello Node.js or .NET back end, do hello following:</span></span>

[!INCLUDE [app-service-mobile-configure-new-backend](../../includes/app-service-mobile-configure-new-backend.md)]

## <a name="download-and-run-hello-xamarinforms-solution"></a><span data-ttu-id="2f2b2-123">Scaricare ed eseguire una soluzione xamarin. Forms hello</span><span class="sxs-lookup"><span data-stu-id="2f2b2-123">Download and run hello Xamarin.Forms solution</span></span>

<span data-ttu-id="2f2b2-124">È possibile scaricare la soluzione hello in uno dei due modi.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-124">You can download hello solution in either of two ways.</span></span> <span data-ttu-id="2f2b2-125">Scaricarlo tooa Mac e aprirlo in Xamarin Studio, o scaricarlo computer Windows tooa e aprirlo in Visual Studio tramite un Mac connesso alla rete per la compilazione di app iOS hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-125">Download it tooa Mac and open it in Xamarin Studio, or download it tooa Windows computer and open it in Visual Studio by using a networked Mac for building hello iOS app.</span></span> <span data-ttu-id="2f2b2-126">Per altre informazioni, vedere [Configurare e installare Visual Studio e Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-126">For more information, see [Set up and install Visual Studio and Xamarin](https://msdn.microsoft.com/library/mt613162.aspx).</span></span>

<span data-ttu-id="2f2b2-127">In un computer Mac o Windows hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f2b2-127">On a Mac or Windows computer, do hello following:</span></span>

1. <span data-ttu-id="2f2b2-128">Passare toohello [portale di Azure].</span><span class="sxs-lookup"><span data-stu-id="2f2b2-128">Go toohello [Azure portal].</span></span>

2. <span data-ttu-id="2f2b2-129">In hello **impostazioni** pannello per app per dispositivi mobili, in **Mobile**selezionare **iniziare** > **xamarin. Forms**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-129">On hello **Settings** blade for your mobile app, under **Mobile**, select **Get Started** > **Xamarin.Forms**.</span></span> <span data-ttu-id="2f2b2-130">In **Passaggio 3** selezionare  **Crea una nuova app** e quindi selezionare **Scarica**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-130">Under **step 3**, select  **Create a new app**, and then select **Download**.</span></span>

   <span data-ttu-id="2f2b2-131">Questa azione consente di scaricare un progetto che contiene un'applicazione client che è connesso tooyour app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-131">This action downloads a project that contains a client application that's connected tooyour mobile app.</span></span> <span data-ttu-id="2f2b2-132">Salvare computer locale tooyour file progetto compresso hello e prendere nota del dove salvarla.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-132">Save hello compressed project file tooyour local computer, and make a note of where you save it.</span></span>

3. <span data-ttu-id="2f2b2-133">Estrarre il progetto hello scaricato e aprirlo in Visual Studio (Windows) o di Xamarin Studio (Mac).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-133">Extract hello project that you downloaded, and then open it in Xamarin Studio (Mac) or Visual Studio (Windows).</span></span>

   ![Progetto estratto in Xamarin Studio][9]

   ![Progetto estratto in Visual Studio][8]

## <a name="optional-run-hello-ios-project"></a><span data-ttu-id="2f2b2-136">(Facoltativo) Eseguire il progetto di iOS hello</span><span class="sxs-lookup"><span data-stu-id="2f2b2-136">(Optional) Run hello iOS project</span></span>
<span data-ttu-id="2f2b2-137">In questa sezione si eseguirlo hello Xamarin iOS per i dispositivi iOS.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-137">In this section, you run hello Xamarin iOS project for iOS devices.</span></span> <span data-ttu-id="2f2b2-138">Se non si usano dispositivi iOS, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-138">You can skip this section if you are not working with iOS devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="2f2b2-139">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="2f2b2-139">In Xamarin Studio</span></span>
1. <span data-ttu-id="2f2b2-140">Fare clic sul progetto iOS hello e quindi selezionare **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-140">Right-click hello iOS project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="2f2b2-141">In hello **eseguire** dal menu **Avvia debug** toobuild hello progetto e avviare hello app nell'emulatore di iPhone hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-141">On hello **Run** menu, select **Start Debugging** toobuild hello project and start hello app in hello iPhone emulator.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="2f2b2-142">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f2b2-142">In Visual Studio</span></span>
1. <span data-ttu-id="2f2b2-143">Fare clic sul progetto iOS hello e quindi selezionare **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-143">Right-click hello iOS project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="2f2b2-144">In hello **compilare** dal menu **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-144">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="2f2b2-145">In hello **Configuration Manager** la finestra di dialogo, seleziona hello **compilare** e **Distribuisci** progetto iOS toohello successivo di caselle di controllo.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-145">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello iOS project.</span></span>

4. <span data-ttu-id="2f2b2-146">toobuild hello progetto e avviare hello app nell'emulatore iPhone hello, seleziona hello **F5** chiave.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-146">toobuild hello project and start hello app in hello iPhone emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f2b2-147">Se si verificano problemi di compilazione progetto hello, eseguire hello manager e aggiornamento toohello ultima versione del pacchetto NuGet di pacchetti di supporto Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-147">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="2f2b2-148">Progetti di avvio rapido potrebbero essere lento tooupdate toohello ultime versioni.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-148">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="2f2b2-149">Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, e quindi selezionare hello sul segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-149">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][10]

    <span data-ttu-id="2f2b2-150">Questa azione Invia un toohello richiesta post che nuova App per dispositivi mobili di back-end che è ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-150">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="2f2b2-151">Dati richiesta hello viene inseriti nella tabella TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-151">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="2f2b2-152">Gli elementi archiviati nella tabella hello vengono restituiti per hello terminare nuovamente App per dispositivi mobili e hello dati vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-152">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2f2b2-153">È disponibile codice hello che accede l'App per dispositivi mobili di back-end in hello file TodoItemManager.cs c# del progetto di libreria di classi portabile hello della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-153">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-android-project"></a><span data-ttu-id="2f2b2-154">(Facoltativo) Esegui progetto Android hello</span><span class="sxs-lookup"><span data-stu-id="2f2b2-154">(Optional) Run hello Android project</span></span>
<span data-ttu-id="2f2b2-155">In questa sezione si esegue il progetto di hello Xamarin droid per Android.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-155">In this section, you run hello Xamarin droid project for Android.</span></span> <span data-ttu-id="2f2b2-156">Se non si usano dispositivi Android, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-156">You can skip this section if you are not working with Android devices.</span></span>

#### <a name="in-xamarin-studio"></a><span data-ttu-id="2f2b2-157">In Xamarin Studio</span><span class="sxs-lookup"><span data-stu-id="2f2b2-157">In Xamarin Studio</span></span>

1. <span data-ttu-id="2f2b2-158">Fare clic sul progetto Android hello e quindi selezionare **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-158">Right-click hello Android project, and then select **Set As Startup Project**.</span></span>

2. <span data-ttu-id="2f2b2-159">toobuild hello progetto e avviare l'applicazione hello in un emulatore Android hello **eseguire** dal menu **Avvia debug**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-159">toobuild hello project and start hello app in an Android emulator, on hello **Run** menu, select **Start Debugging**.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="2f2b2-160">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f2b2-160">In Visual Studio</span></span>

1. <span data-ttu-id="2f2b2-161">Fare clic sul progetto Android (Droid) hello e quindi selezionare **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-161">Right-click hello Android (Droid) project, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="2f2b2-162">In hello **compilare** dal menu **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-162">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="2f2b2-163">In hello **Configuration Manager** la finestra di dialogo, seleziona hello **compilare** e **Distribuisci** progetto Android toohello Avanti caselle di controllo.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-163">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Android project.</span></span>

4. <span data-ttu-id="2f2b2-164">toobuild hello progetto e avviare l'applicazione hello in un emulatore Android, seleziona hello **F5** chiave.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-164">toobuild hello project and start hello app in an Android emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f2b2-165">Se si verificano problemi di compilazione progetto hello, eseguire hello manager e aggiornamento toohello ultima versione del pacchetto NuGet di pacchetti di supporto Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-165">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="2f2b2-166">Progetti di avvio rapido potrebbero essere lento tooupdate toohello ultime versioni.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-166">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="2f2b2-167">Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, e quindi selezionare hello sul segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-167">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    ![][11]
    
    <span data-ttu-id="2f2b2-168">Questa azione Invia un toohello richiesta post che nuova App per dispositivi mobili di back-end che è ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-168">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="2f2b2-169">Dati richiesta hello viene inseriti nella tabella TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-169">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="2f2b2-170">Gli elementi archiviati nella tabella hello vengono restituiti per hello terminare nuovamente App per dispositivi mobili e hello dati vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-170">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="2f2b2-171">È disponibile codice hello che accede l'App per dispositivi mobili di back-end in hello file TodoItemManager.cs c# del progetto di libreria di classi portabile hello della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-171">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="optional-run-hello-windows-project"></a><span data-ttu-id="2f2b2-172">(Facoltativo) Eseguire il progetto di Windows hello</span><span class="sxs-lookup"><span data-stu-id="2f2b2-172">(Optional) Run hello Windows project</span></span>

<span data-ttu-id="2f2b2-173">In questa sezione si esegue hello progetto Xamarin WinApp per i dispositivi Windows.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-173">In this section, you run hello Xamarin WinApp project for Windows devices.</span></span> <span data-ttu-id="2f2b2-174">Se non si usano dispositivi Windows, è possibile ignorare questa sezione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-174">You can skip this section if you are not working with Windows devices.</span></span>

#### <a name="in-visual-studio"></a><span data-ttu-id="2f2b2-175">In Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f2b2-175">In Visual Studio</span></span>

1. <span data-ttu-id="2f2b2-176">Fare doppio clic su uno qualsiasi dei progetti di Windows hello e quindi selezionare **imposta come progetto di avvio**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-176">Right-click any of hello Windows projects, and then select **Set as StartUp Project**.</span></span>

2. <span data-ttu-id="2f2b2-177">In hello **compilare** dal menu **Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-177">On hello **Build** menu, select **Configuration Manager**.</span></span>

3. <span data-ttu-id="2f2b2-178">In hello **Configuration Manager** la finestra di dialogo, seleziona hello **compilare** e **Distribuisci** caselle di controllo toohello Windows progetto successivo che si è scelto.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-178">In hello **Configuration Manager** dialog box, select hello **Build** and **Deploy** check boxes next toohello Windows project that you chose.</span></span>

4. <span data-ttu-id="2f2b2-179">toobuild hello progetto e avviare l'applicazione hello in un emulatore di Windows, seleziona hello **F5** chiave.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-179">toobuild hello project and start hello app in a Windows emulator, select hello **F5** key.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f2b2-180">Se si verificano problemi di compilazione progetto hello, eseguire hello manager e aggiornamento toohello ultima versione del pacchetto NuGet di pacchetti di supporto Xamarin hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-180">If you have problems building hello project, run hello NuGet package manager and update toohello latest version of hello Xamarin support packages.</span></span> <span data-ttu-id="2f2b2-181">Progetti di avvio rapido potrebbero essere lento tooupdate toohello ultime versioni.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-181">Quickstart projects might be slow tooupdate toohello latest versions.</span></span>    
   >
   >

5. <span data-ttu-id="2f2b2-182">Nell'app hello, digitare un testo significativo, ad esempio *informazioni su Xamarin*, e quindi selezionare hello sul segno più (**+**).</span><span class="sxs-lookup"><span data-stu-id="2f2b2-182">In hello app, type meaningful text, such as *Learn Xamarin*, and then select hello plus sign (**+**).</span></span>

    <span data-ttu-id="2f2b2-183">Questa azione Invia un toohello richiesta post che nuova App per dispositivi mobili di back-end che è ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-183">This action sends a post request toohello new Mobile Apps back end that's hosted in Azure.</span></span> <span data-ttu-id="2f2b2-184">Dati richiesta hello viene inseriti nella tabella TodoItem hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-184">Data from hello request is inserted into hello TodoItem table.</span></span> <span data-ttu-id="2f2b2-185">Gli elementi archiviati nella tabella hello vengono restituiti per hello terminare nuovamente App per dispositivi mobili e hello dati vengono visualizzati nell'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-185">Items that are stored in hello table are returned by hello Mobile Apps back end, and hello data is displayed in hello list.</span></span>
    
    ![][12]
    
    > [!NOTE]
    > <span data-ttu-id="2f2b2-186">È disponibile codice hello che accede l'App per dispositivi mobili di back-end in hello file TodoItemManager.cs c# del progetto di libreria di classi portabile hello della soluzione.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-186">You'll find hello code that accesses your Mobile Apps back end in hello TodoItemManager.cs C# file of hello portable class library project of your solution.</span></span>
    >
    >

## <a name="next-steps"></a><span data-ttu-id="2f2b2-187">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f2b2-187">Next steps</span></span>

* [<span data-ttu-id="2f2b2-188">Aggiungere app tooyour authentication</span><span class="sxs-lookup"><span data-stu-id="2f2b2-188">Add authentication tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-users.md)  
  <span data-ttu-id="2f2b2-189">Informazioni su come gli utenti tooauthenticate dell'app con un provider di identità.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-189">Learn how tooauthenticate users of your app with an identity provider.</span></span>

* [<span data-ttu-id="2f2b2-190">Aggiungere app tooyour di notifiche push</span><span class="sxs-lookup"><span data-stu-id="2f2b2-190">Add push notifications tooyour app</span></span>](app-service-mobile-xamarin-forms-get-started-push.md)  
  <span data-ttu-id="2f2b2-191">Informazioni su come le notifiche push tooadd supportano tooyour app e configurare le notifiche di push di App per dispositivi mobili back-end toouse gli hub di notifica di Azure toosend hello.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-191">Learn how tooadd push notifications support tooyour app and configure your Mobile Apps back end toouse Azure Notification Hubs toosend hello push notifications.</span></span>

* [<span data-ttu-id="2f2b2-192">Abilitare la sincronizzazione offline per l'app</span><span class="sxs-lookup"><span data-stu-id="2f2b2-192">Enable offline sync for your app</span></span>](app-service-mobile-xamarin-forms-get-started-offline-data.md)  
  <span data-ttu-id="2f2b2-193">Informazioni su come tooadd supporto offline per l'app usando un App per dispositivi mobili back-end.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-193">Learn how tooadd offline support for your app by using a Mobile Apps back end.</span></span> <span data-ttu-id="2f2b2-194">La sincronizzazione offline consente di visualizzare, aggiungere o modificare i dati dell'app per dispositivi mobili, anche se non è presente alcuna connessione di rete.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-194">With offline sync, you can view, add, or modify your mobile app's data, even when there is no network connection.</span></span>

* [<span data-ttu-id="2f2b2-195">Usare i client gestiti hello per App per dispositivi mobili</span><span class="sxs-lookup"><span data-stu-id="2f2b2-195">Use hello managed client for Mobile Apps</span></span>](app-service-mobile-dotnet-how-to-use-client-library.md)  
  <span data-ttu-id="2f2b2-196">Informazioni su come toowork con hello gestita client SDK nell'app Xamarin.</span><span class="sxs-lookup"><span data-stu-id="2f2b2-196">Learn how toowork with hello managed client SDK in your Xamarin app.</span></span>

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
