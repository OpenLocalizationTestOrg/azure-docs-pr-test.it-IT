---
title: Creare il ticket di supporto o il case per StorSimple serie 8000 | Microsoft Docs
description: Informazioni su come registrare una richiesta di supporto e avviare una sessione di supporto nel dispositivo StorSimple serie 8000.
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
ms.openlocfilehash: 4b5a14237ce79100f980b2186b2c3c887abaa296
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="contact-microsoft-support"></a><span data-ttu-id="21909-103">Contattare il supporto tecnico Microsoft</span><span class="sxs-lookup"><span data-stu-id="21909-103">Contact Microsoft Support</span></span>

<span data-ttu-id="21909-104">Gestione dispositivi StorSimple offre la possibilità di **registrare una nuova richiesta di supporto** all'interno del pannello di riepilogo servizio.</span><span class="sxs-lookup"><span data-stu-id="21909-104">The StorSimple Device Manager provides the capability to **log a new support request** within the service summary blade.</span></span> <span data-ttu-id="21909-105">Se si verificano problemi con la soluzione StorSimple, è possibile creare una richiesta di servizio per il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="21909-105">If you encounter any issues with your StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="21909-106">In una sessione online con il supporto tecnico, è necessario anche avviare una sessione di supporto nel dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21909-106">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="21909-107">In questo articolo viene descritto:</span><span class="sxs-lookup"><span data-stu-id="21909-107">This article walks you through:</span></span>

* <span data-ttu-id="21909-108">Come creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="21909-108">How to create a support request.</span></span>
* <span data-ttu-id="21909-109">Come gestire una richiesta di supporto relativa al ciclo di vita all'interno del portale.</span><span class="sxs-lookup"><span data-stu-id="21909-109">How to manage a support request lifecycle from within the portal.</span></span>
* <span data-ttu-id="21909-110">Come avviare una sessione di supporto nell'interfaccia Windows PowerShell del dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21909-110">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="21909-111">Esaminare [Informazioni e contratti di servizio di supporto tecnico della serie 8000 di StorSimple](https://msdn.microsoft.com/library/mt433077.aspx) prima di creare una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="21909-111">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="21909-112">Creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="21909-112">Create a support request</span></span>

<span data-ttu-id="21909-113">In base al [piano di supporto](https://azure.microsoft.com/support/plans/) è possibile creare ticket di supporto per un problema sul dispositivo StorSimple direttamente dal pannello di riepilogo del servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21909-113">Depending upon your [support plan](https://azure.microsoft.com/support/plans/), you can create support tickets for an issue on your StorSimple device directly from the StorSimple Device Manager service summary blade.</span></span> <span data-ttu-id="21909-114">Per creare una richiesta di supporto, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="21909-114">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="21909-115">Per creare una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="21909-115">To create a support request</span></span>

1. <span data-ttu-id="21909-116">Passare al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21909-116">Go to your StorSimple Device Manager service.</span></span> <span data-ttu-id="21909-117">Nelle impostazioni del pannello di riepilogo servizio passare alla sezione **SUPPORTO E RISOLUZIONE DEI PROBLEMI** e quindi fare clic su **Nuova richiesta di supporto**.</span><span class="sxs-lookup"><span data-stu-id="21909-117">In the service summary blade settings, go to **SUPPORT + TROUBLESHOOTING** section and then click **New support request**.</span></span>
     
    ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport1.png)
   
2. <span data-ttu-id="21909-119">Nel pannello **Nuova richiesta di supporto** selezionare **Informazioni di base**.</span><span class="sxs-lookup"><span data-stu-id="21909-119">In the **New support request** blade, select **Basics**.</span></span> <span data-ttu-id="21909-120">Nel pannello **Informazioni di base** attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="21909-120">In the **Basics** blade, do the following steps:</span></span>
   1. <span data-ttu-id="21909-121">Dall'elenco a discesa **Tipo di problema** selezionare **Tecnico**.</span><span class="sxs-lookup"><span data-stu-id="21909-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="21909-122">Vengono scelti automaticamente i valori correnti di **sottoscrizione**, tipo di **servizio** e **risorsa** (servizio Gestione dispositivi StorSimple).</span><span class="sxs-lookup"><span data-stu-id="21909-122">The current **Subscription**, **Service** type, and the **Resource** (StorSimple Device Manager service) are automatically chosen.</span></span> 
   3. <span data-ttu-id="21909-123">Scegliere un **piano di supporto** dall'elenco a discesa se alla sottoscrizione sono associati più piani.</span><span class="sxs-lookup"><span data-stu-id="21909-123">Select a **Support plan** from the drop-down list if you have multiple plans associated with your subscription.</span></span> <span data-ttu-id="21909-124">È necessario un piano di supporto a pagamento per poter abilitare il supporto tecnico.</span><span class="sxs-lookup"><span data-stu-id="21909-124">You need a paid support plan to enable Technical Support.</span></span>
   4. <span data-ttu-id="21909-125">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="21909-125">Click **Next**.</span></span>

       ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport2.png)

3. <span data-ttu-id="21909-127">Nel pannello **Nuova richiesta di supporto** selezionare **Passaggio 2 - Problema**.</span><span class="sxs-lookup"><span data-stu-id="21909-127">In the **New support request** blade, select **Step 2 Problem**.</span></span> <span data-ttu-id="21909-128">Nel pannello **Problema** attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="21909-128">In the **Problem** blade, do the following steps:</span></span>
    
    1. <span data-ttu-id="21909-129">Scegliere il livello di **Gravità**.</span><span class="sxs-lookup"><span data-stu-id="21909-129">Choose the **Severity**.</span></span>
    2. <span data-ttu-id="21909-130">Specificare se il problema è correlato al dispositivo o al servizio Gestione dispositivi StorSimple.</span><span class="sxs-lookup"><span data-stu-id="21909-130">Specify if the issue is related to the appliance or the StorSimple Device Manager service.</span></span>
    3. <span data-ttu-id="21909-131">Scegliere una **Categoria** per il problema e fornire maggiori **Dettagli**.</span><span class="sxs-lookup"><span data-stu-id="21909-131">Choose a **Category** for this issue and provide more **Details** about the issue.</span></span>
    4. <span data-ttu-id="21909-132">Specificare la data e l'ora di inizio del problema.</span><span class="sxs-lookup"><span data-stu-id="21909-132">Provide the start date and time for the problem.</span></span>
    5. <span data-ttu-id="21909-133">In **Caricamento file**fare clic sull'icona della cartella per selezionare il pacchetto di supporto.</span><span class="sxs-lookup"><span data-stu-id="21909-133">In the **File upload**, click the folder icon to browse to your support package.</span></span>
    6. <span data-ttu-id="21909-134">Selezionare **Condividi informazioni diagnostica**.</span><span class="sxs-lookup"><span data-stu-id="21909-134">Check **Share diagnostic information**.</span></span>
    7. <span data-ttu-id="21909-135">Fare clic su **Avanti**.</span><span class="sxs-lookup"><span data-stu-id="21909-135">Click **Next**.</span></span>

       ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport3.png) 

4. <span data-ttu-id="21909-137">Nel pannello **Nuova richiesta di assistenza** fare clic su **Passaggio 3 - Informazioni di contatto**.</span><span class="sxs-lookup"><span data-stu-id="21909-137">In the **New support request** blade, click **Step 3 Contact information**.</span></span> <span data-ttu-id="21909-138">Nel pannello **Informazioni di contatto**, attenersi alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="21909-138">In the **Contact information** blade, do the following steps:</span></span>

    1. <span data-ttu-id="21909-139">In **Opzioni contatti**, fornire il metodo di contatto preferito (telefono o posta elettronica) e la lingua.</span><span class="sxs-lookup"><span data-stu-id="21909-139">In the **Contact options**, provide your preferred contact method (phone or email) and the language.</span></span> <span data-ttu-id="21909-140">Il tempo di risposta viene selezionato automaticamente in base al piano di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="21909-140">The response time is automatically selected based on your subscription plan.</span></span>
    2. <span data-ttu-id="21909-141">In Informazioni di contatto specificare nome, posta elettronica, contatto facoltativo, paese.</span><span class="sxs-lookup"><span data-stu-id="21909-141">In the Contact information, provide your name, email, optional contact, country.</span></span> <span data-ttu-id="21909-142">Selezionare la casella di controllo **Salva modifiche di contatto per le richieste di supporto future** .</span><span class="sxs-lookup"><span data-stu-id="21909-142">Select the **Save contact changes for future support requests** check box.</span></span>
    3. <span data-ttu-id="21909-143">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="21909-143">Click **Create**.</span></span>
   
        ![Contattare il supporto tecnico Microsoft tramite il nuovo portale](./media/storsimple-8000-contact-microsoft-support/contactsupport5.png)   

    <span data-ttu-id="21909-145">Il supporto Microsoft userà queste informazioni per contattare l'utente per altre informazioni, la diagnostica e la risoluzione.</span><span class="sxs-lookup"><span data-stu-id="21909-145">Microsoft Support will use this information to reach out to you for further information, diagnosis, and resolution.</span></span>
<span data-ttu-id="21909-146">Dopo avere inviato la richiesta, si verrà presto contattati da un tecnico del supporto per procedere con la richiesta.</span><span class="sxs-lookup"><span data-stu-id="21909-146">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="manage-a-support-request"></a><span data-ttu-id="21909-147">Gestire una richiesta di supporto</span><span class="sxs-lookup"><span data-stu-id="21909-147">Manage a support request</span></span>

<span data-ttu-id="21909-148">Dopo la creazione del ticket di supporto, sarà possibile gestire il ciclo di vita del ticket dal portale.</span><span class="sxs-lookup"><span data-stu-id="21909-148">After creating a support ticket, you can manage the lifecycle of the ticket from within the portal.</span></span>

#### <a name="to-manage-your-support-requests"></a><span data-ttu-id="21909-149">Per gestire le richieste di supporto</span><span class="sxs-lookup"><span data-stu-id="21909-149">To manage your support requests</span></span>

1. <span data-ttu-id="21909-150">Per visualizzare la pagina Guida e supporto, passare a **Sfoglia -> Guida e supporto**.</span><span class="sxs-lookup"><span data-stu-id="21909-150">To get to the help and support page, navigate to **Browse > Help + support**.</span></span>

    ![Gestire le richieste di supporto](./media/storsimple-8000-contact-microsoft-support/managesupport1.png)

2. <span data-ttu-id="21909-152">Nel pannello **Guida e supporto** viene visualizzato un elenco tabulare con tutte le richieste di supporto.</span><span class="sxs-lookup"><span data-stu-id="21909-152">A tabular listing of All the support requests is displayed in the **Help + support** blade.</span></span>

    ![Gestire le richieste di supporto](./media/storsimple-8000-contact-microsoft-support/managesupport2.png)

3. <span data-ttu-id="21909-154">Selezionare e fare clic su una richiesta di supporto.</span><span class="sxs-lookup"><span data-stu-id="21909-154">Select and click a support request.</span></span> <span data-ttu-id="21909-155">È possibile visualizzare lo stato e i dettagli della richiesta.</span><span class="sxs-lookup"><span data-stu-id="21909-155">You can view the status and the details for this request.</span></span> <span data-ttu-id="21909-156">Fare clic su **+ Nuovo messaggio** se si vuole seguire la richiesta.</span><span class="sxs-lookup"><span data-stu-id="21909-156">Click **+ New message** if you want to follow up on this request.</span></span>

    ![Gestire le richieste di supporto](./media/storsimple-8000-contact-microsoft-support/managesupport3.png)

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="21909-158">Avviare una sessione di supporto in Windows PowerShell per StorSimple</span><span class="sxs-lookup"><span data-stu-id="21909-158">Start a support session in Windows PowerShell for StorSimple</span></span>

<span data-ttu-id="21909-159">Per risolvere eventuali problemi che potrebbero verificarsi con il dispositivo StorSimple, sarà necessario contattare il team del supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="21909-159">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="21909-160">Il supporto tecnico Microsoft potrebbe utilizzare una sessione di supporto per l'accesso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="21909-160">Microsoft Support may need to use a support session to log on to your device.</span></span>

<span data-ttu-id="21909-161">Per avviare una sessione di supporto, attenersi alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="21909-161">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="21909-162">Per avviare una sessione di supporto</span><span class="sxs-lookup"><span data-stu-id="21909-162">To start a support session</span></span>

1. <span data-ttu-id="21909-163">Accedere al dispositivo direttamente tramite la console seriale o tramite una sessione telnet da un computer remoto.</span><span class="sxs-lookup"><span data-stu-id="21909-163">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="21909-164">A tale scopo, attenersi alle istruzioni riportate in [Utilizzare PuTTY per connettersi alla console seriale del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="21909-164">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="21909-165">Nella sessione che viene aperta, premere **Invio** per visualizzare un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="21909-165">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="21909-166">Nel menu della console seriale, scegliere l'opzione 1, **Accedi con accesso completo**.</span><span class="sxs-lookup"><span data-stu-id="21909-166">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="21909-167">Al prompt dei comandi, digitare la seguente password:</span><span class="sxs-lookup"><span data-stu-id="21909-167">At the prompt, type the following password:</span></span>
   
    `Password1`
5. <span data-ttu-id="21909-168">Al prompt dei comandi, digitare il seguente comando:</span><span class="sxs-lookup"><span data-stu-id="21909-168">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="21909-169">Verrà visualizzata una stringa crittografata.</span><span class="sxs-lookup"><span data-stu-id="21909-169">An encrypted string will be presented to you.</span></span> <span data-ttu-id="21909-170">Copiare la stringa in un editor di testo, ad esempio Blocco note.</span><span class="sxs-lookup"><span data-stu-id="21909-170">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="21909-171">Salvare la stringa e inviarla in un messaggio di posta elettronica al supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="21909-171">Save this string and send it in an email message to Microsoft Support.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21909-172">È possibile disabilitare l'accesso del supporto eseguendo `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="21909-172">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="21909-173">Il dispositivo StorSimple inoltre tenterà di disabilitare l'accesso del supporto dopo 8 ore dall'avvio della sessione.</span><span class="sxs-lookup"><span data-stu-id="21909-173">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="21909-174">È consigliabile modificare le credenziali del dispositivo StorSimple dopo l'avvio di una sessione di supporto.</span><span class="sxs-lookup"><span data-stu-id="21909-174">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>


## <a name="next-steps"></a><span data-ttu-id="21909-175">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="21909-175">Next steps</span></span>

<span data-ttu-id="21909-176">Informazioni su come [diagnosticare e risolvere i problemi relativi al dispositivo virtuale StorSimple serie 8000](storsimple-troubleshoot-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="21909-176">Learn how to [diagnose and solve problems related to your StorSimple 8000 series device](storsimple-troubleshoot-deployment.md)</span></span>
