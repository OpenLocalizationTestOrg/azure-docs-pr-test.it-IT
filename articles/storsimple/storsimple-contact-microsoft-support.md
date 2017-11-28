---
title: ticket di supporto per StorSimple serie 8000 aaaLog | Documenti Microsoft
description: Informazioni su come toocreate un supporto richiesta e avviare una sessione di supporto nel dispositivo StorSimple.
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: e1a3aa3c56e036c782c4fb502c477dc0feaa0ccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="82a5e-103">Contattare il supporto tecnico Microsoft per il dispositivo StorSimple in uso</span><span class="sxs-lookup"><span data-stu-id="82a5e-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="82a5e-104">Se si verificano problemi con la soluzione Microsoft Azure StorSimple, è possibile creare una richiesta di servizio per il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="82a5e-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="82a5e-105">In una sessione in linea con il tecnico del supporto, è necessario anche toostart una sessione di supporto nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82a5e-105">In an online session with your support engineer, you may also need toostart a support session on your StorSimple device.</span></span> <span data-ttu-id="82a5e-106">In questo articolo viene descritto:</span><span class="sxs-lookup"><span data-stu-id="82a5e-106">This article walks you through:</span></span>

* <span data-ttu-id="82a5e-107">Come richiedere toocreate un supporto.</span><span class="sxs-lookup"><span data-stu-id="82a5e-107">How toocreate a support request.</span></span>
* <span data-ttu-id="82a5e-108">Toostart una sessione di supporto nella hello come interfaccia di Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="82a5e-108">How toostart a support session in hello Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="82a5e-109">Hello revisione [StorSimple 8000 Series supporto SLA e le informazioni](https://msdn.microsoft.com/library/mt433077.aspx) prima di creare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="82a5e-109">Review hello [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="82a5e-110">Creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="82a5e-110">Create a support request</span></span>
<span data-ttu-id="82a5e-111">Eseguire hello seguendo i passaggi toocreate una richiesta di supporto:</span><span class="sxs-lookup"><span data-stu-id="82a5e-111">Perform hello following steps toocreate a support request:</span></span>

#### <a name="toocreate-a-support-request"></a><span data-ttu-id="82a5e-112">toocreate una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="82a5e-112">toocreate a support request</span></span>
1. <span data-ttu-id="82a5e-113">In hello [portale di Azure classico](https://manage.windowsazure.com/), hello angolo superiore destro, scegliere il nome di account e quindi fare clic su **contattare il supporto tecnico Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-113">In hello [Azure classic portal](https://manage.windowsazure.com/), in hello upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Contattare il supporto tecnico Microsoft tramite il portale di gestione](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="82a5e-115">Sarà reindirizzato toohello nuovo portale di Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="82a5e-115">You will be redirected toohello new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="82a5e-116">Fare clic su hello **nuova richiesta di assistenza** riquadro.</span><span class="sxs-lookup"><span data-stu-id="82a5e-116">Click hello **New support request** tile.</span></span>
   
    ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="82a5e-118">Sul lato destro di hello della schermata ciao, hello **nuova richiesta di assistenza** verrà visualizzato il riquadro.</span><span class="sxs-lookup"><span data-stu-id="82a5e-118">On hello right side of hello screen, hello **New support request** pane appears.</span></span> 
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="82a5e-120">In hello **nozioni di base** della finestra di dialogo hello completo seguente:</span><span class="sxs-lookup"><span data-stu-id="82a5e-120">In hello **Basics** dialog box, complete hello following:</span></span>                                
   
   1. <span data-ttu-id="82a5e-121">Da hello **rilascio tipo** elenco a discesa, seleziona **tecniche**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-121">From hello **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="82a5e-122">Selezionare un **sottoscrizione** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-122">Select a **Subscription** from hello drop-down list.</span></span>
   3. <span data-ttu-id="82a5e-123">Da hello **servizio** elenco a discesa, seleziona **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-123">From hello **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="82a5e-124">Selezionare un **piano di supporto** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-124">Select a **Support plan** from hello drop-down list.</span></span> <span data-ttu-id="82a5e-125">È necessario un tooenable piano di supporto a pagamento il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="82a5e-125">You need a paid support plan tooenable Technical Support.</span></span>
4. <span data-ttu-id="82a5e-126">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-126">Click **Next**.</span></span> <span data-ttu-id="82a5e-127">Hello **problema** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="82a5e-127">hello **Problem** dialog box appears.</span></span>
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="82a5e-129">In hello **problema** della finestra di dialogo hello completo seguente:</span><span class="sxs-lookup"><span data-stu-id="82a5e-129">In hello **Problem** dialog box, complete hello following:</span></span>
   
   1. <span data-ttu-id="82a5e-130">Selezionare un **gravità** livello dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-130">Select a **Severity** level from hello drop-down list.</span></span>
   2. <span data-ttu-id="82a5e-131">Selezionare un **tipo di problema** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-131">Select a **Problem type** from hello drop-down list.</span></span>
   3. <span data-ttu-id="82a5e-132">Selezionare un **categoria** dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-132">Select a **Category** from hello drop-down list.</span></span> 
   4. <span data-ttu-id="82a5e-133">In hello **dettagli** casella, una breve descrizione del problema.</span><span class="sxs-lookup"><span data-stu-id="82a5e-133">In hello **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="82a5e-134">In hello **tempo** casella, indicare hello data, ora e fuso orario corrispondente toohello occorrenza più recente del problema.</span><span class="sxs-lookup"><span data-stu-id="82a5e-134">In hello **Time frame** box, indicate hello date, time, and time zone that corresponds toohello most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="82a5e-135">In **caricamento del File**, fare clic su hello cartella icona toobrowse tooyour pacchetto per il supporto.</span><span class="sxs-lookup"><span data-stu-id="82a5e-135">Under **File upload**, click hello folder icon toobrowse tooyour support package.</span></span>
   7. <span data-ttu-id="82a5e-136">Seleziona hello **condividere le informazioni di diagnostica** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="82a5e-136">Select hello **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="82a5e-137">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-137">Click **Next**.</span></span> <span data-ttu-id="82a5e-138">Hello **le informazioni di contatto** viene visualizzata la finestra di dialogo.</span><span class="sxs-lookup"><span data-stu-id="82a5e-138">hello **Contact information** dialog box appears.</span></span>
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="82a5e-140">Immettere le informazioni di contatto e selezionare un metodo di contatto (telefono o posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="82a5e-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="82a5e-141">Seleziona hello **Salva le modifiche di contatto per le richieste di supporto futuro** casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="82a5e-141">Select hello **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="82a5e-142">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-142">Click **Create**.</span></span>

<span data-ttu-id="82a5e-143">Dopo l'invio della richiesta, un tecnico del supporto contatterà l'utente appena possibile tooproceed con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="82a5e-143">After you have submitted your request, a Support engineer will contact you as soon as possible tooproceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="82a5e-144">Avviare una sessione di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="82a5e-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="82a5e-145">tootroubleshoot eventuali problemi che potrebbero verificarsi con il dispositivo di StorSimple hello, sarà necessario tooengage con il team di supporto Microsoft hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-145">tootroubleshoot any issues that you might experience with hello StorSimple device, you will need tooengage with hello Microsoft Support team.</span></span> <span data-ttu-id="82a5e-146">Supporto Microsoft potrebbe essere necessario un toolog di sessione di supporto nel dispositivo tooyour toouse.</span><span class="sxs-lookup"><span data-stu-id="82a5e-146">Microsoft Support may need toouse a support session toolog on tooyour device.</span></span> 

<span data-ttu-id="82a5e-147">Eseguire l'esempio hello passaggi toostart una sessione di supporto:</span><span class="sxs-lookup"><span data-stu-id="82a5e-147">Perform hello following steps toostart a support session:</span></span>

#### <a name="toostart-a-support-session"></a><span data-ttu-id="82a5e-148">toostart una sessione di supporto</span><span class="sxs-lookup"><span data-stu-id="82a5e-148">toostart a support session</span></span>
1. <span data-ttu-id="82a5e-149">Hello dispositivo per l'accesso direttamente tramite la console seriale hello o tramite una sessione telnet da un computer remoto.</span><span class="sxs-lookup"><span data-stu-id="82a5e-149">Access hello device directly by using hello serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="82a5e-150">toodo, seguire la procedura seguente hello in [console seriale del dispositivo usare PuTTY tooconnect toohello](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="82a5e-150">toodo this, follow hello steps in [Use PuTTY tooconnect toohello device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="82a5e-151">Nella sessione hello aperta, premere hello **invio** chiave tooget un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="82a5e-151">In hello session that opens, press hello **Enter** key tooget a command prompt.</span></span>
3. <span data-ttu-id="82a5e-152">Nel menu della console seriale hello, selezionare l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="82a5e-152">In hello serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="82a5e-153">Al prompt dei comandi hello, digitare hello seguenti password:</span><span class="sxs-lookup"><span data-stu-id="82a5e-153">At hello prompt, type hello following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="82a5e-154">Al prompt dei comandi hello, digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="82a5e-154">At hello prompt, type hello following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="82a5e-155">Verrà visualizzata una stringa crittografata tooyou.</span><span class="sxs-lookup"><span data-stu-id="82a5e-155">An encrypted string will be presented tooyou.</span></span> <span data-ttu-id="82a5e-156">Copiare la stringa in un editor di testo, ad esempio Blocco note.</span><span class="sxs-lookup"><span data-stu-id="82a5e-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="82a5e-157">Salvare la stringa e inviarla in un tooMicrosoft messaggio di posta elettronica supporto.</span><span class="sxs-lookup"><span data-stu-id="82a5e-157">Save this string and send it in an email message tooMicrosoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="82a5e-158">È possibile disabilitare l'accesso del supporto eseguendo `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="82a5e-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="82a5e-159">dispositivo StorSimple Hello tenterà anche accesso al supporto toodisable 8 ore dopo l'avvio della sessione hello.</span><span class="sxs-lookup"><span data-stu-id="82a5e-159">hello StorSimple device will also attempt toodisable support access 8 hours after hello session was initiated.</span></span> <span data-ttu-id="82a5e-160">È una migliore toochange pratica le credenziali del dispositivo StorSimple dopo l'avvio di una sessione di supporto.</span><span class="sxs-lookup"><span data-stu-id="82a5e-160">It is a best practice toochange your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

