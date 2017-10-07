---
title: aaaAccessing le app da qualsiasi dispositivo | Documenti Microsoft
description: Informazioni su quali client sono supportate per Azure RemoteApp e come tooaccess app.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: fb7bd17d-7aa8-43fd-9278-f96e0e9308e4
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 15985b40d870e3155d4132063bf5b9677ff9afed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-your-apps-in-azure-remoteapp"></a><span data-ttu-id="0c2f9-103">Accesso alle app in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="0c2f9-103">Accessing your apps in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="0c2f9-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="0c2f9-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="0c2f9-106">Uno dei meraviglie hello di Azure RemoteApp è che si possono accedere le applicazioni da uno qualsiasi dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-106">One of hello beauties of Azure RemoteApp is that you can access apps from any of your devices.</span></span> <span data-ttu-id="0c2f9-107">Ancor meglio, è possibile iniziare a lavorare su un dispositivo e quindi fluire tooa secondo dispositivo e scegliere in alto a destra in cui è stata interrotta.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-107">Even better, you can start working on one device and then seamlessly transition tooa second device and pick up right where you left off.</span></span> <span data-ttu-id="0c2f9-108">tooget avviato è necessario client in modo toodownload hello appropriato per il dispositivo e accedere toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-108">tooget started you need toodownload hello appropriate client for your device and sign in toohello service.</span></span>

<span data-ttu-id="0c2f9-109">In questo argomento verrà esaminato il client di hello attualmente supportati e come toodownload li prima si illustrano come toosign in tooRemoteApp da ognuno di hello client.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-109">In this topic, we'll review hello clients currently supported and how toodownload them before I show you how toosign in tooRemoteApp from each of hello clients.</span></span>

## <a name="supported-clients"></a><span data-ttu-id="0c2f9-110">Client supportati</span><span class="sxs-lookup"><span data-stu-id="0c2f9-110">Supported clients</span></span>
<span data-ttu-id="0c2f9-111">È possibile accedere RemoteApp attenendosi alla procedura di hello seguente se il dispositivo è in esecuzione uno di questi sistemi operativi:</span><span class="sxs-lookup"><span data-stu-id="0c2f9-111">You can access RemoteApp using hello steps below if your device is running one of these operating systems:</span></span>

* <span data-ttu-id="0c2f9-112">Windows 10</span><span class="sxs-lookup"><span data-stu-id="0c2f9-112">Windows 10</span></span> 
* <span data-ttu-id="0c2f9-113">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="0c2f9-113">Windows 8.1</span></span>
* <span data-ttu-id="0c2f9-114">Windows 8</span><span class="sxs-lookup"><span data-stu-id="0c2f9-114">Windows 8</span></span>
* <span data-ttu-id="0c2f9-115">Windows 7 Service Pack 1</span><span class="sxs-lookup"><span data-stu-id="0c2f9-115">Windows 7 Service Pack 1</span></span>
* <span data-ttu-id="0c2f9-116">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="0c2f9-116">Windows Phone 8.1</span></span>
* <span data-ttu-id="0c2f9-117">iOS</span><span class="sxs-lookup"><span data-stu-id="0c2f9-117">iOS</span></span>
* <span data-ttu-id="0c2f9-118">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="0c2f9-118">Mac OS X</span></span>
* <span data-ttu-id="0c2f9-119">Android</span><span class="sxs-lookup"><span data-stu-id="0c2f9-119">Android</span></span>

 <span data-ttu-id="0c2f9-120">Thin client? Hello seguente thin client con Windows Embedded supportato:</span><span class="sxs-lookup"><span data-stu-id="0c2f9-120">What about thin clients? hello following Windows Embedded thin clients are supported:</span></span>

* <span data-ttu-id="0c2f9-121">Windows Embedded Standard 7</span><span class="sxs-lookup"><span data-stu-id="0c2f9-121">Windows Embedded Standard 7</span></span>
* <span data-ttu-id="0c2f9-122">Windows Embedded 8 Standard</span><span class="sxs-lookup"><span data-stu-id="0c2f9-122">Windows Embedded 8 Standard</span></span>
* <span data-ttu-id="0c2f9-123">Windows Embedded 8.1 Industry Pro</span><span class="sxs-lookup"><span data-stu-id="0c2f9-123">Windows Embedded 8.1 Industry Pro</span></span>
* <span data-ttu-id="0c2f9-124">Windows 10 IoT Enterprise</span><span class="sxs-lookup"><span data-stu-id="0c2f9-124">Windows 10 IoT Enterprise</span></span>

## <a name="downloading-hello-client"></a><span data-ttu-id="0c2f9-125">Download di client hello</span><span class="sxs-lookup"><span data-stu-id="0c2f9-125">Downloading hello client</span></span>
<span data-ttu-id="0c2f9-126">Indipendentemente dalla piattaforma in uso, client hello è necessario tooaccess RemoteApp è reperibile in hello [download del client Desktop remoto](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) pagina.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-126">No matter what platform you are using, hello client you need tooaccess RemoteApp can be found on hello [Remote Desktop client download](https://www.remoteapp.windowsazure.com/ClientDownload/AllClients.aspx) page.</span></span>

<span data-ttu-id="0c2f9-127">Facendo clic su collegamenti differenti di hello verranno avviare direttamente il download client hello o invierà toohello pagina di download del client nell'archivio di app hello per quella piattaforma.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-127">Clicking hello different links will either directly start downloading hello client or will send you toohello client download page in hello app store for that platform.</span></span> <span data-ttu-id="0c2f9-128">Installare il client di hello seguendo le istruzioni di hello nella schermata Ciao.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-128">Install hello client by following hello instructions on hello screen.</span></span>

<span data-ttu-id="0c2f9-129">Dopo aver installato il client hello sul dispositivo e ha avviata, passare una sezione corrispondente toohello toolearn come toosign in tooRemoteApp dal client.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-129">Once you have installed hello client on your device and launched it, jump toohello corresponding section below toolearn how toosign in tooRemoteApp from that client.</span></span>

## <a name="android"></a><span data-ttu-id="0c2f9-130">Android</span><span class="sxs-lookup"><span data-stu-id="0c2f9-130">Android</span></span>
<span data-ttu-id="0c2f9-131">Dopo aver installato app Desktop remoto Microsoft hello da hello Google Play store, è possibile trovare nell'elenco delle app in **Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-131">Once you have installed hello Microsoft Remote Desktop app from hello Google Play store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="0c2f9-132">Avvio applicazione hello offre tooan Center di connessione vuota, a meno che non si sta già utilizzando app hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-132">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="0c2f9-133">tooget avviato con Azure RemoteApp, pulsante Aggiungi tap hello **"" +""** e toccare **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-133">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Azure RemoteApp**.</span></span>    
   
     ![Centro connessioni vuoto](./media/remoteapp-clients/Android1.png)
2. <span data-ttu-id="0c2f9-135">È necessario toosign con il servizio di hello tooaccess indirizzo e-mail.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-135">You need toosign in with your email address tooaccess hello service.</span></span> <span data-ttu-id="0c2f9-136">Toccare **Get started**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-136">Tap **Get started**.</span></span>
   
    ![Prompt di accesso](./media/remoteapp-clients/Android2.png)
3. <span data-ttu-id="0c2f9-138">Nella pagina successiva di hello, digitare il **indirizzo di posta elettronica** e toccare **continua**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-138">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="0c2f9-139">Questo processo hello accesso tramite Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-139">This begins hello sign-in process using Azure Active Directory.</span></span>
   
    ![Pagina iniziale di Azure Active Directory](./media/remoteapp-clients/Android3.png)
4. <span data-ttu-id="0c2f9-141">Seguire le istruzioni di hello hello schermata toosign con l'account di Microsoft (precedentemente denominato "LiveID") o un ID organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-141">Follow hello instructions on hello screen toosign in with your Microsoft account (previously called "LiveID") or organization ID.</span></span> <span data-ttu-id="0c2f9-142">Una volta effettuato l'accesso, possono essere presentati con una pagina che elenca tutti gli inviti hello ricevuti.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-142">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="0c2f9-143">Se si, selezionare gli inviti hello attendibili e toccare **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-143">If you are, select hello invitations you trust and tap **Done**.</span></span>    
   
    ![Pagina degli inviti](./media/remoteapp-clients/Android4.png)
5. <span data-ttu-id="0c2f9-145">Dopo aver accettato l'inviti, elenco hello di App ha accesso toowill dispositivo tooyour scaricato e ha reso disponibile nel Centro connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-145">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="0c2f9-146">Toccare un hello App toostart utilizzarlo.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-146">Tap one of hello apps toostart using it.</span></span>
   
    ![Centro connessioni con un feed](./media/remoteapp-clients/Android5.png)
6. <span data-ttu-id="0c2f9-148">Se non hai ancora un invito, è comunque possibile provare servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-148">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="0c2f9-149">toodo in tal caso, toccare **passare valutazione toofree** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-149">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Prompt dei feed dimostrativi](./media/remoteapp-clients/Android6.png)
7. <span data-ttu-id="0c2f9-151">Che consente di accedere a set di base tooa di tooget App con RemoteApp è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-151">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Feed dimostrativo per Azure RemoteApp](./media/remoteapp-clients/Android7.png)

## <a name="ios"></a><span data-ttu-id="0c2f9-153">iOS</span><span class="sxs-lookup"><span data-stu-id="0c2f9-153">iOS</span></span>
<span data-ttu-id="0c2f9-154">Dopo aver installato app Desktop remoto Microsoft hello dall'archivio di App hello, è possibile trovare nell'elenco delle app in **Client desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-154">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **RD Client**.</span></span>

1. <span data-ttu-id="0c2f9-155">Avvio applicazione hello offre tooan Center di connessione vuota, a meno che non si sta già utilizzando app hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-155">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="0c2f9-156">tooget avviato con Azure RemoteApp, pulsante Aggiungi tap hello **"" +""** e toccare **aggiungere Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-156">tooget started with Azure RemoteApp, tap hello add button **""+""** and tap **Add Azure RemoteApp**.</span></span>
   
    ![Centro connessioni vuoto](./media/remoteapp-clients/IOS1.png)
2. <span data-ttu-id="0c2f9-158">È necessario toosign con il servizio di posta elettronica indirizzo tooaccess hello, toostart questo processo, un tipo nel **indirizzo di posta elettronica** e toccare **continua**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-158">You need toosign in with your email address tooaccess hello service, toostart that process, type in your **email address** and tap **Continue**.</span></span>
   
    ![Prompt di accesso](./media/remoteapp-clients/picture1.png)
3. <span data-ttu-id="0c2f9-160">Seguire le istruzioni di hello hello schermata toosign con l'account Microsoft (LiveID) o un ID organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-160">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0c2f9-161">Una volta effettuato l'accesso, possono essere presentati con una pagina che elenca tutti gli inviti hello ricevuti.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-161">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="0c2f9-162">Se si, selezionare gli inviti hello attendibili e toccare **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-162">If you are, select hello invitations you trust and tap **Done**.</span></span>
   
    ![Pagina degli inviti](./media/remoteapp-clients/IOS3.png)
4. <span data-ttu-id="0c2f9-164">Dopo aver accettato l'inviti, elenco hello di App ha accesso toowill dispositivo tooyour scaricato e ha reso disponibile nel Centro connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-164">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="0c2f9-165">Toccare una delle toolaunch App hello e iniziare a utilizzare il.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-165">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro connessioni con un feed](./media/remoteapp-clients/IOS4.png)
5. <span data-ttu-id="0c2f9-167">Se non hai ancora un invito, è comunque possibile provare servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-167">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="0c2f9-168">toodo in tal caso, toccare **passare valutazione toofree** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-168">toodo so, tap **Go toofree trial** when prompted.</span></span>
   
    ![Prompt dei feed dimostrativi](./media/remoteapp-clients/IOS5.png)
6. <span data-ttu-id="0c2f9-170">Che consente di accedere a set di base tooa di tooget App con RemoteApp è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-170">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Feed dimostrativo per Azure RemoteApp](./media/remoteapp-clients/IOS6.png)

## <a name="mac-os-x"></a><span data-ttu-id="0c2f9-172">Mac OS X</span><span class="sxs-lookup"><span data-stu-id="0c2f9-172">Mac OS X</span></span>
<span data-ttu-id="0c2f9-173">Dopo aver installato app Desktop remoto Microsoft hello dall'archivio di App hello, è possibile trovare nell'elenco delle app in **Desktop remoto Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-173">Once you have installed hello Microsoft Remote Desktop app from hello App store, you can find it in your app list under **Microsoft Remote Desktop**.</span></span>

1. <span data-ttu-id="0c2f9-174">Avvio applicazione hello offre tooan Center di connessione vuota, a meno che non si sta già utilizzando app hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-174">Launching hello app brings you tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="0c2f9-175">tooget avviato con Azure RemoteApp, fare clic su hello **Azure RemoteApp** pulsante.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-175">tooget started with Azure RemoteApp, click hello **Azure RemoteApp** button.</span></span>
   
    ![Centro connessioni vuoto](./media/remoteapp-clients/Mac1.png)
2. <span data-ttu-id="0c2f9-177">È necessario toosign con il servizio di posta elettronica indirizzo tooaccess hello, toostart che elaborano, toccare **iniziare**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-177">You need toosign in with your email address tooaccess hello service, toostart that process, tap **Get Started**.</span></span>
   
    ![Prompt di accesso](./media/remoteapp-clients/Mac2.png)
3. <span data-ttu-id="0c2f9-179">Nella pagina successiva di hello, digitare il **indirizzo di posta elettronica** e toccare **continua**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-179">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="0c2f9-180">Consente di iniziare hello Accedi processo usando Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-180">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Pagina iniziale di Azure Active Directory](./media/remoteapp-clients/picture2.png)
4. <span data-ttu-id="0c2f9-182">Seguire le istruzioni di hello hello schermata toosign con l'account Microsoft (LiveID) o un ID organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-182">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0c2f9-183">Una volta effettuato l'accesso, possono essere presentati con una pagina che elenca tutti gli inviti hello ricevuti.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-183">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="0c2f9-184">Se si, selezionare gli inviti hello attendibili e chiudere una finestra di dialogo hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-184">If you are, select hello invitations you trust and close hello dialog.</span></span>
   
    ![Pagina degli inviti](./media/remoteapp-clients/Mac4.png)
5. <span data-ttu-id="0c2f9-186">Dopo aver accettato l'inviti, elenco hello di App ha accesso toowill dispositivo tooyour scaricato e ha reso disponibile nel Centro connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-186">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="0c2f9-187">Fare doppio clic su uno dei toolaunch App hello e iniziare a utilizzare il.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-187">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro connessioni con un feed](./media/remoteapp-clients/Mac5.png)
6. <span data-ttu-id="0c2f9-189">Se non hai ancora un invito, è comunque possibile provare servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-189">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="0c2f9-190">toodo in tal caso, fare clic su **passare valutazione toofree** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-190">toodo so, click **Go toofree trial** when prompted.</span></span>
   
    ![Prompt dei feed dimostrativi](./media/remoteapp-clients/Mac6.png)
7. <span data-ttu-id="0c2f9-192">Che consente di accedere a set di base tooa di tooget App con RemoteApp è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-192">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Feed dimostrativo per Azure RemoteApp](./media/remoteapp-clients/Mac7.png)

## <a name="windows-all-supported-versions-except-windows-phone"></a><span data-ttu-id="0c2f9-194">Windows (tutte le versioni supportate, ad eccezione di Windows Phone)</span><span class="sxs-lookup"><span data-stu-id="0c2f9-194">Windows (All supported versions except Windows Phone)</span></span>
<span data-ttu-id="0c2f9-195">Hello client viene avviato automaticamente al termine dell'installazione, tuttavia quando è necessario tooaccess è più tardi possono essere trovati nell'elenco delle app con nome hello **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-195">hello client launches automatically after it finishes installing, however when you need tooaccess it again later it can be found in your app list under hello name **Azure RemoteApp**.</span></span>

1. <span data-ttu-id="0c2f9-196">N seguito avvia hello client, hello prima pagina di benvenuto tooAzure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-196">Ater launching hello client, hello first page you see welcomes you tooAzure RemoteApp.</span></span> <span data-ttu-id="0c2f9-197">tooproceed, fare clic su **iniziare**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-197">tooproceed, click on **Get Started**.</span></span>
   
    ![Pagina iniziale del client di Azure RemoteApp hello](./media/remoteapp-clients/Windows1.png)
2. <span data-ttu-id="0c2f9-199">la pagina successiva di Hello avvia hello sign nel processo di Azure RemoteApp utilizza Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-199">hello next page starts hello sign in process for Azure RemoteApp using Azure Active Directory.</span></span> <span data-ttu-id="0c2f9-200">Questo processo dovrebbe essere familiare se utilizzati servizi Microsoft hello precedente.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-200">This process should look familiar if you have used Microsoft services in hello past.</span></span> <span data-ttu-id="0c2f9-201">Per iniziare, digitare il proprio **indirizzo e-mail** e fare clic su **Continua**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-201">Start by typing your **email address** and click **Continue**.</span></span>
   
    ![Prompt iniziale di Azure Active Directory](./media/remoteapp-clients/Windows2.png)
3. <span data-ttu-id="0c2f9-203">Seguire le istruzioni di hello hello schermata toosign con l'account Microsoft (LiveID) o un ID organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-203">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0c2f9-204">Una volta effettuato l'accesso, possono essere presentati con una pagina che elenca tutti gli inviti hello ricevuti.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-204">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="0c2f9-205">Se si, selezionare gli inviti hello attendibili e fare clic su **eseguita**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-205">If you are, select hello invitations you trust and click **Done**.</span></span>
   
    ![Pagina di inviti del client di Azure RemoteApp hello](./media/remoteapp-clients/Windows3.png)
4. <span data-ttu-id="0c2f9-207">Dopo aver accettato l'inviti, elenco hello di App ha accesso toowill dispositivo tooyour scaricato e ha reso disponibile nel Centro connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-207">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="0c2f9-208">Fare doppio clic su uno dei toolaunch App hello e iniziare a utilizzare il.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-208">Double-click one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro di connessione del client di Azure RemoteApp hello](./media/remoteapp-clients/Windows4.png)
5. <span data-ttu-id="0c2f9-210">Se non sono stati ancora ricevuti inviti,</span><span class="sxs-lookup"><span data-stu-id="0c2f9-210">If no one has sent you an invitation yet, don't worry we've got you covered!</span></span> <span data-ttu-id="0c2f9-211">Per testare il servizio di hello, sarà comunque possibile accesso tooa demo insieme.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-211">You'll still have access tooa demo collection so you can test out hello service.</span></span>
   
    ![Feed dimostrativo per Azure RemoteApp](./media/remoteapp-clients/Windows5.png)

## <a name="windows-phone-81"></a><span data-ttu-id="0c2f9-213">Windows Phone 8.1</span><span class="sxs-lookup"><span data-stu-id="0c2f9-213">Windows Phone 8.1</span></span>
<span data-ttu-id="0c2f9-214">Dopo aver installato app Desktop remoto Microsoft hello dall'archivio hello Windows Phone 8.1, è possibile trovare nell'elenco delle app in **Desktop remoto**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-214">Once you have installed hello Microsoft Remote Desktop app from hello Windows Phone 8.1 store, you can find it in your app list under **Remote Desktop**.</span></span>

1. <span data-ttu-id="0c2f9-215">Avvio applicazione hello Importa direttamente tooan Center di connessione vuota, a meno che non si sta già utilizzando app hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-215">Launching hello app brings you directly tooan empty Connection Center, unless you've already been using hello app.</span></span> <span data-ttu-id="0c2f9-216">tooget avviato con Azure RemoteApp, pulsante Aggiungi tap hello **"" +""** in basso hello hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-216">tooget started with Azure RemoteApp, tap hello add button **""+""** at hello bottom of hello screen.</span></span>
   
    ![Centro connessioni vuoto](./media/remoteapp-clients/WinPhone1.png)
2. <span data-ttu-id="0c2f9-218">Quindi, toccare **Azure RemoteApp**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-218">Next, tap on **Azure RemoteApp**.</span></span>
   
    ![Pagina Aggiungi elemento ](./media/remoteapp-clients/WinPhone2.png)
3. <span data-ttu-id="0c2f9-220">È necessario toosign con il servizio di posta elettronica indirizzo tooaccess hello, toostart che elaborano, toccare **connettersi**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-220">You need toosign in with your email address tooaccess hello service, toostart that process, tap **connect**.</span></span>
   
    ![Prompt di accesso](./media/remoteapp-clients/WinPhone3.png)
4. <span data-ttu-id="0c2f9-222">Nella pagina successiva di hello, digitare il **indirizzo di posta elettronica** e toccare **continua**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-222">On hello next page, type in your **email address** and tap **Continue**.</span></span> <span data-ttu-id="0c2f9-223">Consente di iniziare hello Accedi processo usando Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-223">This begins hello sign in process using Azure Active Directory.</span></span>
   
    ![Pagina iniziale di Azure Active Directory](./media/remoteapp-clients/WinPhone4.png)
5. <span data-ttu-id="0c2f9-225">Seguire le istruzioni di hello hello schermata toosign con l'account Microsoft (LiveID) o un ID organizzazione.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-225">Follow hello instructions on hello screen toosign in with your Microsoft account (LiveID) or Organization ID.</span></span> <span data-ttu-id="0c2f9-226">Una volta effettuato l'accesso, possono essere presentati con una pagina che elenca tutti gli inviti hello ricevuti.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-226">Once signed in, you may be presented with a page listing all hello invitations you have received.</span></span> <span data-ttu-id="0c2f9-227">Se si, selezionare gli inviti hello attendibili e toccare **salvare**.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-227">If you are, select hello invitations you trust and tap **save**.</span></span>
   
    ![Pagina degli inviti](./media/remoteapp-clients/WinPhone5.png)
6. <span data-ttu-id="0c2f9-229">Dopo aver accettato l'inviti, elenco hello di App ha accesso toowill dispositivo tooyour scaricato e ha reso disponibile nel Centro connessioni di hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-229">After accepting your invitations, hello list of apps you have access toowill be downloaded tooyour device and made available in hello Connection Center.</span></span> <span data-ttu-id="0c2f9-230">Toccare una delle toolaunch App hello e iniziare a utilizzare il.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-230">Tap one of hello apps toolaunch it and start using it.</span></span>
   
    ![Centro connessioni con un feed](./media/remoteapp-clients/WinPhone6.png)
7. <span data-ttu-id="0c2f9-232">Se non hai ancora un invito, è comunque possibile provare servizio hello.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-232">If you do not have an invitation yet, you can still try out hello service.</span></span> <span data-ttu-id="0c2f9-233">toodo in tal caso, toccare **Sì** quando richiesto.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-233">toodo so, tap **yes** when prompted.</span></span>
   
    ![Prompt dei feed dimostrativi](./media/remoteapp-clients/WinPhone7.png)
8. <span data-ttu-id="0c2f9-235">Che consente di accedere a set di base tooa di tooget App con RemoteApp è stata avviata.</span><span class="sxs-lookup"><span data-stu-id="0c2f9-235">This will give you access tooa basic set of apps tooget you started with RemoteApp.</span></span>
   
    ![Feed dimostrativo per Azure RemoteApp](./media/remoteapp-clients/WinPhone8.png)

