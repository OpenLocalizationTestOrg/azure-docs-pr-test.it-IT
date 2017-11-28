---
title: "aaaYou non è possibile accedervi da qui in hello portale di Azure da un dispositivo Windows | Documenti Microsoft"
description: "Informazioni su dove non è possibile da qui arriva da get e ciò che è possibile controllare tooavoid in esecuzione in questa finestra di dialogo."
services: active-directory
keywords: accesso condizionale basato su dispositivo, registrazione dispositivo, abilitare registrazione dispositivo, registrazione dispositivo e software MDM
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 8ad0156c-0812-4855-8563-6fbff6194174
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: eda2aa10fbff5b3e515723219f61c1cb6f634e29
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="you-cant-get-there-from-here-on-a-windows-device"></a><span data-ttu-id="3bac8-104">Messaggio "Non è possibile accedervi da qui" in un dispositivo Windows</span><span class="sxs-lookup"><span data-stu-id="3bac8-104">You can't get there from here on a Windows device</span></span>

<span data-ttu-id="3bac8-105">Durante un tentativo di accedere ad esempio alla Intranet SharePoint Online dell'organizzazione può essere visualizzata una pagina con il messaggio *Non è possibile accedervi da qui*.</span><span class="sxs-lookup"><span data-stu-id="3bac8-105">During an attempt to, for example, access your organization's SharePoint Online intranet you might run into a page that states that *you can't get there from here*.</span></span> <span data-ttu-id="3bac8-106">Viene visualizzata questa pagina perché l'amministratore ha configurato un criterio di accesso condizionale che impedisce l'accesso tooyour risorse aziendali in determinate condizioni.</span><span class="sxs-lookup"><span data-stu-id="3bac8-106">You are seeing this page, because your administrator has configured a conditional access policy that prevents access tooyour organization's resources under certain conditions.</span></span> <span data-ttu-id="3bac8-107">Anche se potrebbe essere necessario toocontact helpdesk o l'amministratore tooget risolto questo problema, esistono alcuni aspetti, che è possibile provare manualmente, prima di tutto.</span><span class="sxs-lookup"><span data-stu-id="3bac8-107">While it might be necessary toocontact helpdesk or your administrator tooget this problem solved, there are a few things you can try out yourself, first.</span></span>

<span data-ttu-id="3bac8-108">Se si utilizza un **Windows** dispositivo, è consigliabile controllare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="3bac8-108">If you are using a **Windows** device, you should check hello following:</span></span>

- <span data-ttu-id="3bac8-109">Il browser usato è supportato?</span><span class="sxs-lookup"><span data-stu-id="3bac8-109">Are you using a supported browser?</span></span>

- <span data-ttu-id="3bac8-110">Viene eseguita una versione supportata di Windows nel dispositivo?</span><span class="sxs-lookup"><span data-stu-id="3bac8-110">Are you running a supported version of Windows on your device?</span></span>

- <span data-ttu-id="3bac8-111">Il dispositivo è conforme?</span><span class="sxs-lookup"><span data-stu-id="3bac8-111">Is your device compliant?</span></span>






## <a name="supported-browser"></a><span data-ttu-id="3bac8-112">Browser supportati</span><span class="sxs-lookup"><span data-stu-id="3bac8-112">Supported browser</span></span>

<span data-ttu-id="3bac8-113">Se l'amministratore ha configurato un criterio di accesso condizionale, è possibile accedere alle risorse dell'organizzazione solo usando un browser supportato.</span><span class="sxs-lookup"><span data-stu-id="3bac8-113">If your administrator has configured a conditional access policy, you can only access your organization's resources by using a supported browser.</span></span> <span data-ttu-id="3bac8-114">In un dispositivo Windows sono supportati solo **Internet Explorer** ed **Microsoft Edge**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-114">On a Windows device, only **Internet Explorer** and **Edge** are supported.</span></span>

<span data-ttu-id="3bac8-115">È possibile identificare facilmente se è Impossibile accedere a una risorsa a causa del browser non supportata tooan osservando hello dettagli sezione della pagina di errore hello:</span><span class="sxs-lookup"><span data-stu-id="3bac8-115">You can easily identify whether you can't access a resource due tooan unsupported browser by looking at hello details section of hello error page:</span></span>

<span data-ttu-id="3bac8-116">![Messaggi "Non è possibile accedervi da qui" per browser non supportati](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="3bac8-116">!["You can't get there from here" message for unsupported browsers](./media/active-directory-conditional-access-device-remediation/02.png "Scenario")</span></span>

<span data-ttu-id="3bac8-117">monitoraggio e aggiornamento solo di Hello è toouse un browser che supporta l'applicazione hello per la piattaforma del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3bac8-117">hello only remediation is toouse a browser that hello application supports for your device platform.</span></span> <span data-ttu-id="3bac8-118">Per un elenco completo dei browser supportati, vedere [Browser supportati](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span><span class="sxs-lookup"><span data-stu-id="3bac8-118">For a complete list of supported browsers, see [supported browsers](active-directory-conditional-access-supported-apps.md#supported-browsers-for-device-based-policies).</span></span>  


## <a name="supported-versions-of-windows"></a><span data-ttu-id="3bac8-119">Versioni di Windows supportate</span><span class="sxs-lookup"><span data-stu-id="3bac8-119">Supported versions of Windows</span></span>

<span data-ttu-id="3bac8-120">esempio Hello deve essere soddisfatte sul sistema operativo di Windows hello nel dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3bac8-120">hello following must be true about hello Windows operating system on your device:</span></span> 

- <span data-ttu-id="3bac8-121">Se si esegue un sistema operativo desktop di Windows sul dispositivo, è necessario toobe Windows 7 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3bac8-121">If you are running a Windows desktop operating system on your device, it needs toobe Windows 7 or later.</span></span>
- <span data-ttu-id="3bac8-122">Se si esegue un sistema operativo Windows server nel dispositivo, è necessario toobe Windows Server 2008 R2 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="3bac8-122">If you are running a Windows server operating system on your device, it needs toobe Windows Server 2008 R2 or later.</span></span> 


## <a name="compliant-device"></a><span data-ttu-id="3bac8-123">Dispositivo conforme</span><span class="sxs-lookup"><span data-stu-id="3bac8-123">Compliant device</span></span>

<span data-ttu-id="3bac8-124">L'amministratore potrebbe aver configurato un criterio di accesso condizionale che consente accesso tooyour risorse aziendali solo da dispositivi conformi.</span><span class="sxs-lookup"><span data-stu-id="3bac8-124">Your administrator might have configured a conditional access policy that allows access tooyour organization's resources only from compliant devices.</span></span> <span data-ttu-id="3bac8-125">Active Directory locale toobe conforme, che il dispositivo deve essere uno tooyour unita in join o aggiunto tooyour Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3bac8-125">toobe compliant, your device must be either joined tooyour on-premises Active Directory or joined tooyour Azure Active Directory.</span></span>

<span data-ttu-id="3bac8-126">È possibile identificare facilmente se è possibile accedere a una risorsa a causa di dispositivo tooa che non è conforme con la ricerca nella sezione dettagli hello hello della pagina di errore:</span><span class="sxs-lookup"><span data-stu-id="3bac8-126">You can easily identify whether you can't access a resource due tooa device that is not compliant by looking at hello details section of hello error page:</span></span>
 
<span data-ttu-id="3bac8-127">![Messaggi "Non è possibile accedervi da qui" per dispositivi non registrati](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span><span class="sxs-lookup"><span data-stu-id="3bac8-127">!["You can't get there from here" messages for unregistered devices](./media/active-directory-conditional-access-device-remediation/01.png "Scenario")</span></span>


### <a name="is-your-device-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="3bac8-128">È tooan i dispositivi aggiunti a un Active Directory locale?</span><span class="sxs-lookup"><span data-stu-id="3bac8-128">Is your device joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="3bac8-129">**Se si aggiunge il dispositivo tooan locale di Active Directory dell'organizzazione:**</span><span class="sxs-lookup"><span data-stu-id="3bac8-129">**If your device is joined tooan on-premises Active Directory in your organization:**</span></span>

1. <span data-ttu-id="3bac8-130">Assicurarsi di eseguire l'accesso tooWindows utilizzando l'account aziendale (l'account di Active Directory).</span><span class="sxs-lookup"><span data-stu-id="3bac8-130">Make sure that you sign in tooWindows by using your work account (your Active Directory account).</span></span>
2. <span data-ttu-id="3bac8-131">Connettersi alla rete aziendale tramite una rete privata virtuale (VPN) o DirectAccess tooyour.</span><span class="sxs-lookup"><span data-stu-id="3bac8-131">Connect tooyour corporate network via a virtual private network (VPN) or DirectAccess.</span></span>
3. <span data-ttu-id="3bac8-132">Dopo essersi connessi, premere il tasto logo Windows hello + toolock chiave hello L la sessione di Windows.</span><span class="sxs-lookup"><span data-stu-id="3bac8-132">After you are connected, press hello Windows logo key + hello L key toolock your Windows session.</span></span>
4. <span data-ttu-id="3bac8-133">Sbloccare la sessione di Windows immettendo le credenziali dell'account aziendale.</span><span class="sxs-lookup"><span data-stu-id="3bac8-133">Unlock your Windows session by entering your work account credentials.</span></span>
5. <span data-ttu-id="3bac8-134">Attendere alcuni minuti e riprovare in seguito tooaccess hello applicazione o servizio.</span><span class="sxs-lookup"><span data-stu-id="3bac8-134">Wait for a minute, and then try again tooaccess hello application or service.</span></span>
6. <span data-ttu-id="3bac8-135">Se viene visualizzato hello stessa pagina, fare clic su hello **ulteriori dettagli** collegamento e quindi contattare l'amministratore con i dettagli di hello.</span><span class="sxs-lookup"><span data-stu-id="3bac8-135">If you see hello same page, click hello **More details** link, and then contact your administrator with hello details.</span></span>


### <a name="is-your-device-not-joined-tooan-on-premises-active-directory"></a><span data-ttu-id="3bac8-136">È tooan il dispositivo non unito in join Active Directory locale?</span><span class="sxs-lookup"><span data-stu-id="3bac8-136">Is your device not joined tooan on-premises Active Directory?</span></span>

<span data-ttu-id="3bac8-137">Se non è stato aggiunto il dispositivo tooan Active Directory locale e viene eseguito Windows 10, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="3bac8-137">If your device is not joined tooan on-premises Active Directory and runs Windows 10, you have two options:</span></span>

* <span data-ttu-id="3bac8-138">Eseguire l'aggiunta ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="3bac8-138">Run Azure AD Join</span></span>
* <span data-ttu-id="3bac8-139">Aggiungere il proprio lavoro o dell'istituto di istruzione tooWindows account</span><span class="sxs-lookup"><span data-stu-id="3bac8-139">Add your work or school account tooWindows</span></span>

<span data-ttu-id="3bac8-140">Per informazioni sulle differenze tra queste opzioni, vedere [Uso di dispositivi Windows 10 in azienda](active-directory-azureadjoin-windows10-devices.md).</span><span class="sxs-lookup"><span data-stu-id="3bac8-140">For information about how these options are different, see [Using Windows 10 devices in your workplace](active-directory-azureadjoin-windows10-devices.md).</span></span>  
<span data-ttu-id="3bac8-141">Se il dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3bac8-141">If your device:</span></span>

- <span data-ttu-id="3bac8-142">Appartiene tooyour organizzazione, è consigliabile eseguire l'aggiunta di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3bac8-142">Belongs tooyour organization, you should run Azure AD Join.</span></span>
- <span data-ttu-id="3bac8-143">È un dispositivo personale o un dispositivo Windows phone, è necessario aggiungere il proprio lavoro o dell'istituto di istruzione tooWindows account</span><span class="sxs-lookup"><span data-stu-id="3bac8-143">Is a personal device or a Windows phone, you should add your work or school account tooWindows</span></span> 



#### <a name="azure-ad-join-on-windows-10"></a><span data-ttu-id="3bac8-144">Aggiunta ad Azure AD in Windows 10</span><span class="sxs-lookup"><span data-stu-id="3bac8-144">Azure AD Join on Windows 10</span></span>

<span data-ttu-id="3bac8-145">Hello toojoin passaggi sono i tooAzure dispositivo AD legati versione hello di Windows 10 in esecuzione su di esso.</span><span class="sxs-lookup"><span data-stu-id="3bac8-145">hello steps toojoin your device tooAzure AD are tied hello version of Windows 10 you are running on it.</span></span> <span data-ttu-id="3bac8-146">versione di hello toodetermine del sistema operativo Windows 10, eseguire hello **winver** comando:</span><span class="sxs-lookup"><span data-stu-id="3bac8-146">toodetermine hello version of your Windows 10 operating system, run hello **winver** command:</span></span> 

![Versione di Windows](./media/active-directory-conditional-access-device-remediation/03.png )


<span data-ttu-id="3bac8-148">**Windows 10 Anniversary Update (versione 1607):**</span><span class="sxs-lookup"><span data-stu-id="3bac8-148">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="3bac8-149">Aprire hello **impostazioni** app.</span><span class="sxs-lookup"><span data-stu-id="3bac8-149">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="3bac8-150">Fare clic su **Account** > **Accedi all'azienda o all'istituto di istruzione**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-150">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="3bac8-151">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-151">Click **Connect**.</span></span>
4. <span data-ttu-id="3bac8-152">Fare clic su **Join questa tooAzure dispositivo AD**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-152">Click **Join this device tooAzure AD**.</span></span>
5. <span data-ttu-id="3bac8-153">Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="3bac8-153">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
6. <span data-ttu-id="3bac8-154">Disconnettersi e quindi eseguire l'accesso con l'account aziendale.</span><span class="sxs-lookup"><span data-stu-id="3bac8-154">Sign out, and then sign in with your work account.</span></span>
7. <span data-ttu-id="3bac8-155">Provare di nuovo un'applicazione hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3bac8-155">Try again tooaccess hello application.</span></span>

<span data-ttu-id="3bac8-156">**Aggiornamento di novembre 2015 di Windows 10 (versione 1511):**</span><span class="sxs-lookup"><span data-stu-id="3bac8-156">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="3bac8-157">Aprire hello **impostazioni** app.</span><span class="sxs-lookup"><span data-stu-id="3bac8-157">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="3bac8-158">Fare clic su **Sistema** > **Informazioni**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-158">Click **System** > **About**.</span></span>
3. <span data-ttu-id="3bac8-159">Fare clic su **Aggiungi ad Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-159">Click **Join Azure AD**.</span></span>
4. <span data-ttu-id="3bac8-160">Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="3bac8-160">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="3bac8-161">Disconnettersi e quindi eseguire l'accesso con l'account aziendale (l'account Azure AD).</span><span class="sxs-lookup"><span data-stu-id="3bac8-161">Sign out, and then sign in with your work account (your Azure AD account).</span></span>
6. <span data-ttu-id="3bac8-162">Provare di nuovo un'applicazione hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3bac8-162">Try again tooaccess hello application.</span></span>


#### <a name="workplace-join-on-windows-81"></a><span data-ttu-id="3bac8-163">Workplace Join in Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3bac8-163">Workplace Join on Windows 8.1</span></span>

<span data-ttu-id="3bac8-164">Se il dispositivo non è aggiunto al dominio e viene eseguito Windows 8.1, toodo un'area di lavoro e registrarsi in Microsoft Intune, hello i passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3bac8-164">If your device is not domain-joined and runs Windows 8.1, toodo a Workplace Join and enroll in Microsoft Intune, do hello following steps:</span></span>

1. <span data-ttu-id="3bac8-165">Aprire **Impostazioni PC**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-165">Open **PC Settings**.</span></span>
2. <span data-ttu-id="3bac8-166">Fare clic su **Rete** > **Rete aziendale**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-166">Click **Network** > **Workplace**.</span></span>
3. <span data-ttu-id="3bac8-167">Fare clic su **Accedi**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-167">Click **Join**.</span></span>
4. <span data-ttu-id="3bac8-168">Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="3bac8-168">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="3bac8-169">Fare clic su **Attiva**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-169">Click **Turn on**.</span></span>
6. <span data-ttu-id="3bac8-170">Provare di nuovo un'applicazione hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3bac8-170">Try again tooaccess hello application.</span></span>



#### <a name="add-your-work-or-school-account-toowindows"></a><span data-ttu-id="3bac8-171">Aggiungere il proprio lavoro o dell'istituto di istruzione tooWindows account</span><span class="sxs-lookup"><span data-stu-id="3bac8-171">Add your work or school account tooWindows</span></span> 


<span data-ttu-id="3bac8-172">**Windows 10 Anniversary Update (versione 1607):**</span><span class="sxs-lookup"><span data-stu-id="3bac8-172">**Windows 10 Anniversary Update (Version 1607):**</span></span>

1. <span data-ttu-id="3bac8-173">Aprire hello **impostazioni** app.</span><span class="sxs-lookup"><span data-stu-id="3bac8-173">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="3bac8-174">Fare clic su **Account** > **Accedi all'azienda o all'istituto di istruzione**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-174">Click **Accounts** > **Access work or school**.</span></span>
3. <span data-ttu-id="3bac8-175">Fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-175">Click **Connect**.</span></span>
4. <span data-ttu-id="3bac8-176">Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="3bac8-176">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="3bac8-177">Provare di nuovo un'applicazione hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3bac8-177">Try again tooaccess hello application.</span></span>


<span data-ttu-id="3bac8-178">**Aggiornamento di novembre 2015 di Windows 10 (versione 1511):**</span><span class="sxs-lookup"><span data-stu-id="3bac8-178">**Windows 10 November 2015 Update (Version 1511):**</span></span>

1. <span data-ttu-id="3bac8-179">Aprire hello **impostazioni** app.</span><span class="sxs-lookup"><span data-stu-id="3bac8-179">Open hello **Settings** app.</span></span>
2. <span data-ttu-id="3bac8-180">Fare clic su **Account** > **Your accounts** (Account personali).</span><span class="sxs-lookup"><span data-stu-id="3bac8-180">Click **Accounts** > **Your accounts**.</span></span>
3. <span data-ttu-id="3bac8-181">Fare clic su **Aggiungi account aziendale o dell'istituto di istruzione**.</span><span class="sxs-lookup"><span data-stu-id="3bac8-181">Click **Add work or school account**.</span></span>
4. <span data-ttu-id="3bac8-182">Autenticare tooyour organizzazione, fornire l'autenticazione a più fattori se richiesto, quindi seguire i passaggi di hello che vengono visualizzati.</span><span class="sxs-lookup"><span data-stu-id="3bac8-182">Authenticate tooyour organization, provide multi-factor authentication if prompted, and then follow hello steps that are shown.</span></span>
5. <span data-ttu-id="3bac8-183">Provare di nuovo un'applicazione hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="3bac8-183">Try again tooaccess hello application.</span></span>





## <a name="next-steps"></a><span data-ttu-id="3bac8-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3bac8-184">Next steps</span></span>
[<span data-ttu-id="3bac8-185">Accesso condizionale di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3bac8-185">Azure Active Directory conditional access</span></span>](active-directory-conditional-access.md)

