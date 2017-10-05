---
title: Registrare i ticket di supporto per StorSimple serie 8000 | Documentazione Microsoft
description: Informazioni su come creare una richiesta di supporto e avviare una sessione di supporto nel dispositivo StorSimple.
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
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="2390e-103">Contattare il supporto tecnico Microsoft per il dispositivo StorSimple in uso</span><span class="sxs-lookup"><span data-stu-id="2390e-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="2390e-104">Se si verificano problemi con la soluzione Microsoft Azure StorSimple, è possibile creare una richiesta di servizio per il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="2390e-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="2390e-105">In una sessione online con il supporto tecnico, è necessario anche avviare una sessione di supporto nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2390e-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="2390e-106">In questo articolo viene descritto:</span><span class="sxs-lookup"><span data-stu-id="2390e-106">This article walks you through:</span></span>

* <span data-ttu-id="2390e-107">Come creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="2390e-107">How to create a support request.</span></span>
* <span data-ttu-id="2390e-108">Come avviare una sessione di supporto nell'interfaccia Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2390e-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="2390e-109">Esaminare [Informazioni e contratti di servizio di supporto tecnico della serie 8000 di StorSimple](https://msdn.microsoft.com/library/mt433077.aspx) prima di creare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="2390e-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="2390e-110">Creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="2390e-110">Create a support request</span></span>
<span data-ttu-id="2390e-111">Per creare una richiesta di supporto, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="2390e-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="2390e-112">Per creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="2390e-112">To create a support request</span></span>
1. <span data-ttu-id="2390e-113">Nell'angolo superiore destro del [portale classico di Azure](https://manage.windowsazure.com/)fare clic sul nome account e quindi su **Contatta il supporto Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="2390e-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Contattare il supporto tecnico Microsoft tramite il portale di gestione](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="2390e-115">Si verrà reindirizzati al nuovo portale di Azure, portal.azure.com.</span><span class="sxs-lookup"><span data-stu-id="2390e-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="2390e-116">Fare clic sul riquadro **Nuova richiesta di supporto** .</span><span class="sxs-lookup"><span data-stu-id="2390e-116">Click the **New support request** tile.</span></span>
   
    ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="2390e-118">Sul lato destro della schermata verrà visualizzato il riquadro **Nuova richiesta di supporto** .</span><span class="sxs-lookup"><span data-stu-id="2390e-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="2390e-120">Nella finestra di dialogo **Generale** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2390e-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="2390e-121">Dall'elenco a discesa **Tipo di problema** selezionare **Tecnico**.</span><span class="sxs-lookup"><span data-stu-id="2390e-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="2390e-122">Selezionare una **sottoscrizione** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2390e-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="2390e-123">Dall'elenco a discesa **Servizio** selezionare **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="2390e-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="2390e-124">Selezionare un **Piano di supporto** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2390e-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="2390e-125">È necessario un piano di supporto a pagamento per poter abilitare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="2390e-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="2390e-126">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2390e-126">Click **Next**.</span></span> <span data-ttu-id="2390e-127">Verrà visualizzata la finestra di dialogo **Problema** .</span><span class="sxs-lookup"><span data-stu-id="2390e-127">The **Problem** dialog box appears.</span></span>
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="2390e-129">Nella finestra di dialogo **Problema** eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2390e-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="2390e-130">Selezionare un livello di **Gravità** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2390e-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="2390e-131">Selezionare un **Tipo di problema** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2390e-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="2390e-132">Selezionare una **Categoria** dall'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="2390e-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="2390e-133">Nella casella **Dettagli** descrivere brevemente il problema.</span><span class="sxs-lookup"><span data-stu-id="2390e-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="2390e-134">Nella casella **Intervallo di tempo** indicare la data, l'ora e il fuso orario corrispondenti al momento in cui si è verificato il problema l'ultima volta.</span><span class="sxs-lookup"><span data-stu-id="2390e-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="2390e-135">In **Caricamento file**fare clic sull'icona della cartella per selezionare il pacchetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="2390e-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="2390e-136">Selezionare la casella di controllo **Condividi informazioni diagnostica** .</span><span class="sxs-lookup"><span data-stu-id="2390e-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="2390e-137">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="2390e-137">Click **Next**.</span></span> <span data-ttu-id="2390e-138">Verrà visualizzata la finestra di dialogo **Informazioni contatto** .</span><span class="sxs-lookup"><span data-stu-id="2390e-138">The **Contact information** dialog box appears.</span></span>
   
    ![Nuovo riquadro di richiesta di supporto](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="2390e-140">Immettere le informazioni di contatto e selezionare un metodo di contatto (telefono o posta elettronica).</span><span class="sxs-lookup"><span data-stu-id="2390e-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="2390e-141">Selezionare la casella di controllo **Salva modifiche di contatto per le richieste di supporto future** .</span><span class="sxs-lookup"><span data-stu-id="2390e-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="2390e-142">Fare clic su **Create**.</span><span class="sxs-lookup"><span data-stu-id="2390e-142">Click **Create**.</span></span>

<span data-ttu-id="2390e-143">Dopo avere inviato la richiesta, si verrà presto contattati da un tecnico del supporto per procedere con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="2390e-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="2390e-144">Avviare una sessione di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="2390e-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="2390e-145">Per risolvere eventuali problemi che potrebbero verificarsi con il dispositivo StorSimple, sarà necessario contattare il team del supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2390e-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="2390e-146">Il supporto tecnico Microsoft potrebbe utilizzare una sessione di supporto per l'accesso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="2390e-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="2390e-147">Per avviare una sessione di supporto, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="2390e-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="2390e-148">Per avviare una sessione di supporto</span><span class="sxs-lookup"><span data-stu-id="2390e-148">To start a support session</span></span>
1. <span data-ttu-id="2390e-149">Accedere al dispositivo direttamente tramite la console seriale o tramite una sessione telnet da un computer remoto.</span><span class="sxs-lookup"><span data-stu-id="2390e-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="2390e-150">A tale scopo, attenersi alle istruzioni riportate in [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="2390e-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="2390e-151">Nella sessione che viene aperta, premere **Invio** per visualizzare un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="2390e-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="2390e-152">Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="2390e-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="2390e-153">Al prompt dei comandi, digitare la seguente password:</span><span class="sxs-lookup"><span data-stu-id="2390e-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="2390e-154">Al prompt dei comandi, digitare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="2390e-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="2390e-155">Verrà visualizzata una stringa crittografata.</span><span class="sxs-lookup"><span data-stu-id="2390e-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="2390e-156">Copiare la stringa in un editor di testo, ad esempio Blocco note.</span><span class="sxs-lookup"><span data-stu-id="2390e-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="2390e-157">Salvare la stringa e inviarla in un messaggio di posta elettronica al supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2390e-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="2390e-158">È possibile disabilitare l'accesso del supporto eseguendo `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="2390e-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="2390e-159">Il dispositivo StorSimple inoltre tenterà di disabilitare l'accesso del supporto dopo 8 ore dall'avvio della sessione.</span><span class="sxs-lookup"><span data-stu-id="2390e-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="2390e-160">È consigliabile modificare le credenziali del dispositivo StorSimple dopo l'avvio di una sessione di supporto.</span><span class="sxs-lookup"><span data-stu-id="2390e-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

