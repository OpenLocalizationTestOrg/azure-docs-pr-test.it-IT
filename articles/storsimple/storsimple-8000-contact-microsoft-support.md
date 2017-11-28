---
title: aaaCreate ticket di supporto o case per StorSimple serie 8000 | Documenti Microsoft
description: Informazioni su come toolog supporta la richiesta e avviare una sessione di supporto nel dispositivo serie StorSimple 8000.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: alkohli;
ms.openlocfilehash: 832e3ac739dafa6dd8c24aaea38aef9c6f1b27b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="9265e-103">Contattare il supporto tecnico Microsoft</span><span class="sxs-lookup"><span data-stu-id="9265e-103">Contact Microsoft Support</span></span>

<span data-ttu-id="9265e-104">Gestione di dispositivi StorSimple Hello fornisce funzionalità di hello troppo**registrare una nuova richiesta di supporto** nel Pannello di riepilogo servizio hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-104">hello StorSimple Device Manager provides hello capability too**log a new support request** within hello service summary blade.</span></span> <span data-ttu-id="9265e-105">Se si verificano problemi con la soluzione StorSimple, è possibile creare una richiesta di servizio per il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="9265e-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="9265e-106">In una sessione in linea con il tecnico del supporto, è necessario anche toostart una sessione di supporto nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9265e-106">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="9265e-107">In questo articolo viene descritto:</span><span class="sxs-lookup"><span data-stu-id="9265e-107">This article walks you through:</span></span>

* <span data-ttu-id="9265e-108">Come richiedere toocreate un supporto.</span><span class="sxs-lookup"><span data-stu-id="9265e-108">How toocreate a support request.</span></span>
* <span data-ttu-id="9265e-109">Come supporto toomanage richiesta ciclo di vita da nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-109">How toomanage a support request lifecycle from within hello portal.</span></span>
* <span data-ttu-id="9265e-110">Toostart una sessione di supporto nella hello come interfaccia di Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9265e-110">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="9265e-111">Hello revisione [StorSimple 8000 Series supporto SLA e le informazioni](https://msdn.microsoft.com/library/mt433077.aspx) prima di creare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="9265e-111">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="9265e-112">Creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="9265e-112">Create a support request</span></span>

<span data-ttu-id="9265e-113">A seconda del [piano di supporto](https://azure.microsoft.com/support/plans/), è possibile creare ticket di supporto per un problema nel dispositivo StorSimple direttamente dal pannello riepilogo servizio di gestione di dispositivi StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from hello StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="9265e-114">Eseguire hello seguendo i passaggi toocreate una richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="9265e-114">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="9265e-115">toocreate una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="9265e-115">toocreate a support request</span></span>

1. <span data-ttu-id="9265e-116">Passare il servizio di gestione di dispositivi StorSimple tooyour.</span><span class="sxs-lookup"><span data-stu-id="9265e-116">Go tooyour StorSimple Device Manager service.</span></span> <span data-ttu-id="9265e-117">Nelle impostazioni del pannello riepilogo servizio hello, andare troppo**supporto + TROUBLESHOOTING** sezione e quindi fare clic su **nuova richiesta di assistenza**.</span><span class="sxs-lookup"><span data-stu-id="9265e-117">In hello service summary blade settings, go too**SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="9265e-119">In hello **nuova richiesta di assistenza** pannello seleziona **nozioni di base**.</span><span class="sxs-lookup"><span data-stu-id="9265e-119">In hello **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="9265e-120">In hello **nozioni di base** pannello hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9265e-120">In hello **Basics** blade, do hello following steps:</span></span>
   1. <span data-ttu-id="9265e-121">Da hello **rilascio tipo** elenco a discesa, seleziona **tecniche**.</span><span class="sxs-lookup"><span data-stu-id="9265e-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="9265e-122">Hello corrente **sottoscrizione**, **servizio** tipo e hello **risorse** (servizio di gestione di dispositivi StorSimple) vengono automaticamente scelti.</span><span class="sxs-lookup"><span data-stu-id="9265e-122">hello current **Subscription**, **Service** type, and hello **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="9265e-123">Selezionare un **piano di supporto** dall'elenco a discesa hello se si dispone di più piani associati alla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9265e-123">Select a **Support plan** from hello drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="9265e-124">È necessario un tooenable piano di supporto a pagamento il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="9265e-124">You need a paid support plan tooenable Technical Support.</span></span>
   4. <span data-ttu-id="9265e-125">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9265e-125">Click **Next**.</span></span>

       ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="9265e-127">In hello **nuova richiesta di assistenza** pannello seleziona **passaggio 2 problema**.</span><span class="sxs-lookup"><span data-stu-id="9265e-127">In hello **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="9265e-128">In hello **problema** pannello hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9265e-128">In hello **Problem** blade, do hello following steps:</span></span>
    
    1. <span data-ttu-id="9265e-129">Scegliere hello **gravità**.</span><span class="sxs-lookup"><span data-stu-id="9265e-129">Choose hello **Severity**.</span></span>
    2. <span data-ttu-id="9265e-130">Specificare se il problema di hello è toohello correlati accessorio o hello del servizio di gestione di dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="9265e-130">Specify if hello issue is related toohello appliance or hello StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="9265e-131">Scegliere un **categoria** per questo problema e fornire più **dettagli** problema hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-131">Choose a **Category** for this issue and provide more **Details** about hello issue.</span></span>
    4. <span data-ttu-id="9265e-132">Fornire hello data e ora inizio problema hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-132">Provide hello start date and time for hello problem.</span></span>
    5. <span data-ttu-id="9265e-133">In hello **caricamento del File**, fare clic su hello cartella icona toobrowse tooyour pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="9265e-133">In hello **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
    6. <span data-ttu-id="9265e-134">Selezionare **Condividi informazioni diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="9265e-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="9265e-135">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="9265e-135">Click **Next**.</span></span>

       ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="9265e-137">In hello **nuova richiesta di assistenza** pannello, fare clic su **le informazioni di contatto di passaggio 3**.</span><span class="sxs-lookup"><span data-stu-id="9265e-137">In hello **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="9265e-138">In hello **le informazioni di contatto** pannello hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="9265e-138">In hello **Contact information** blade, do hello following steps:</span></span>

    1. <span data-ttu-id="9265e-139">In hello **opzioni di contatto**, fornire il metodo di contatto preferito (telefono o posta elettronica) e hello language.</span><span class="sxs-lookup"><span data-stu-id="9265e-139">In hello **Contact options**, provide your preferred contact method (phone or email) and hello language.</span></span> <span data-ttu-id="9265e-140">tempo di risposta Hello viene selezionato automaticamente in base al piano di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="9265e-140">hello response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="9265e-141">Nelle informazioni di contatto hello, specificare nome, posta elettronica, contatti facoltativo, paese.</span><span class="sxs-lookup"><span data-stu-id="9265e-141">In hello Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="9265e-142">Seleziona hello **Salva le modifiche di contatto per le richieste di supporto futuro** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="9265e-142">Select hello **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="9265e-143">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="9265e-143">Click **Create**.</span></span>
   
        ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="9265e-145">Supporto Microsoft utilizzerà questo tooreach informazioni out tooyou per ulteriori informazioni, diagnosi e risoluzione.</span><span class="sxs-lookup"><span data-stu-id="9265e-145">Microsoft Support will use this information tooreach out tooyou for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="9265e-146">Dopo l'invio della richiesta, un tecnico del supporto contatterà l'utente appena possibile tooproceed con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="9265e-146">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="9265e-147">Gestire una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="9265e-147">Manage a support request</span></span>

<span data-ttu-id="9265e-148">Dopo aver creato un ticket di supporto, è possibile gestire hello del ciclo di vita del ticket hello nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-148">After creating a support ticket, you can manage hello lifecycle of hello ticket from within hello portal.</span></span>

#### <a name="toomanage-your-support-requests"></a><span data-ttu-id="9265e-149">richiede il supporto toomanage</span><span class="sxs-lookup"><span data-stu-id="9265e-149">toomanage your support requests</span></span>

1. <span data-ttu-id="9265e-150">tooget toohello della Guida e supporto pagina, spostarsi troppo**Sfoglia > Guida e supporto**.</span><span class="sxs-lookup"><span data-stu-id="9265e-150">tooget toohello help and support page, navigate too**Browse > Help + support**.</span></span>

    ![Gestire le richieste di supporto](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="9265e-152">Un elenco tabulare del supporto di hello tutte le richieste viene visualizzato in hello **Guida e supporto** blade.</span><span class="sxs-lookup"><span data-stu-id="9265e-152">A tabular listing of All hello support requests is displayed in hello **Help + support** blade.</span></span>

    ![Gestire le richieste di supporto](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="9265e-154">Selezionare e fare clic su una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="9265e-154">Select and click a support request.</span></span> <span data-ttu-id="9265e-155">È possibile visualizzare lo stato di hello e dettagli hello per questa richiesta.</span><span class="sxs-lookup"><span data-stu-id="9265e-155">You can view hello status and hello details for this request.</span></span> <span data-ttu-id="9265e-156">Fare clic su **+ nuovo messaggio** se si desidera toofollow per la richiesta.</span><span class="sxs-lookup"><span data-stu-id="9265e-156">Click **+ New message** if you want toofollow up on this request.</span></span>

    ![Gestire le richieste di supporto](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="9265e-158">Avviare una sessione di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="9265e-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="9265e-159">tootroubleshoot eventuali problemi che potrebbero verificarsi con il dispositivo di StorSimple hello, sarà necessario tooengage con il team di supporto Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-159">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="9265e-160">Supporto Microsoft potrebbe essere necessario un toolog di sessione di supporto nel dispositivo tooyour toouse.</span><span class="sxs-lookup"><span data-stu-id="9265e-160">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span>

<span data-ttu-id="9265e-161">Eseguire l'esempio hello passaggi toostart una sessione di supporto:</span><span class="sxs-lookup"><span data-stu-id="9265e-161">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="9265e-162">toostart una sessione di supporto</span><span class="sxs-lookup"><span data-stu-id="9265e-162">toostart a support session</span></span>

1. <span data-ttu-id="9265e-163">Hello dispositivo per l'accesso direttamente tramite la console seriale hello o tramite una sessione telnet da un computer remoto.</span><span class="sxs-lookup"><span data-stu-id="9265e-163">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="9265e-164">toodo, seguire la procedura seguente hello in [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="9265e-164">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="9265e-165">Nella sessione hello aperta, premere hello **invio** chiave tooget un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="9265e-165">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="9265e-166">Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="9265e-166">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="9265e-167">Al prompt dei comandi hello, digitare hello seguenti password:</span><span class="sxs-lookup"><span data-stu-id="9265e-167">At hello prompt, type hello following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="9265e-168">Al prompt dei comandi hello, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9265e-168">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="9265e-169">Verrà visualizzata una stringa crittografata tooyou.</span><span class="sxs-lookup"><span data-stu-id="9265e-169">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="9265e-170">Copiare la stringa in un editor di testo, ad esempio Blocco note.</span><span class="sxs-lookup"><span data-stu-id="9265e-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="9265e-171">Salvare la stringa e inviarla in un tooMicrosoft messaggio di posta elettronica supporto.</span><span class="sxs-lookup"><span data-stu-id="9265e-171">Save this string and send it in an email message tooMicrosoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9265e-172">È possibile disabilitare l'accesso del supporto eseguendo `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="9265e-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="9265e-173">dispositivo StorSimple Hello tenterà anche accesso al supporto toodisable 8 ore dopo l'avvio della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="9265e-173">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="9265e-174">È una migliore toochange pratica le credenziali del dispositivo StorSimple dopo l'avvio di una sessione di supporto.</span><span class="sxs-lookup"><span data-stu-id="9265e-174">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9265e-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9265e-175">Next steps</span></span>

<span data-ttu-id="9265e-176">Informazioni su come troppo[diagnosticare e risolvere dispositivo serie di problemi correlati tooyour StorSimple 8000](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="9265e-176">Learn how too[diagnose and solve problems related tooyour StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
