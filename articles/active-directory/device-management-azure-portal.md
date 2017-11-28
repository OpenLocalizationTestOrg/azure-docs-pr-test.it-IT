---
title: i dispositivi aaaManaging usando hello portale di Azure - anteprima | Documenti Microsoft
description: Informazioni su come toouse hello dispositivi toomanage portale Azure.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: a39d14e4ce8bb79f0223a9de40d5f1259a869927
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-devices-using-hello-azure-portal---preview"></a><span data-ttu-id="1b84a-103">Gestendo i dispositivi con hello portale di Azure - anteprima</span><span class="sxs-lookup"><span data-stu-id="1b84a-103">Managing devices using hello Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="1b84a-104">Questa funzionalità è attualmente disponibile in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="1b84a-104">This capability currently is in public preview.</span></span> <span data-ttu-id="1b84a-105">Essere preparati toorevert o rimuovere tutte le modifiche.</span><span class="sxs-lookup"><span data-stu-id="1b84a-105">Be prepared toorevert or remove any changes.</span></span> <span data-ttu-id="1b84a-106">funzionalità di Hello è disponibile in alcuna sottoscrizione di Azure Active Directory (Azure AD) durante l'anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="1b84a-106">hello feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="1b84a-107">Tuttavia, quando la funzionalità hello diventa disponibile in genere, alcuni aspetti della funzionalità hello potrebbero richiedere una sottoscrizione di Azure Active Directory premium.</span><span class="sxs-lookup"><span data-stu-id="1b84a-107">However, when hello feature becomes generally available, some aspects of hello feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="1b84a-108">Tramite la gestione dei dispositivi in Azure Active Directory (Azure AD) è possibile garantire che gli utenti accedano alle risorse da dispositivi che soddisfano gli standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="1b84a-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="1b84a-109">In questo argomento:</span><span class="sxs-lookup"><span data-stu-id="1b84a-109">This topic:</span></span>

- <span data-ttu-id="1b84a-110">Si presuppone che abbia familiarità con hello [gestione toodevice introduzione in Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="1b84a-110">Assumes that you are familiar with hello [introduction toodevice management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="1b84a-111">Vengono fornite con informazioni sulla gestione dei dispositivi utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="1b84a-111">Provides you with information about managing your devices using hello Azure portal</span></span>


<span data-ttu-id="1b84a-112">dispositivi toomanage in hello portale di Azure, è necessario tooclick **dispositivi** in hello **Gestisci** sezione di hello hello **Azure Active Directory** blade.</span><span class="sxs-lookup"><span data-stu-id="1b84a-112">toomanage devices in hello Azure portal, you need tooclick **Devices** in hello **Manage** section of hello hello **Azure Active Directory** blade.</span></span>

![Gestire un dispositivo Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="1b84a-114">Configurare le impostazioni dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="1b84a-114">Configure device settings</span></span>

<span data-ttu-id="1b84a-115">i dispositivi con hello portale di Azure, è necessario toobe toomanage registrato o unita tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b84a-115">toomanage your devices using hello Azure portal, they need toobe either registered or joined tooAzure AD.</span></span> <span data-ttu-id="1b84a-116">Come amministratore, è possibile ottimizzare il processo di hello di registrazione e l'unione dei dispositivi, configurare le impostazioni di dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-116">As an administrator, you can fine-tune hello process of registering and joining devices by configuring hello device settings.</span></span>

![Gestire un dispositivo Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="1b84a-118">pannello delle impostazioni di dispositivo Hello consente tooconfigure:</span><span class="sxs-lookup"><span data-stu-id="1b84a-118">hello device settings blade enables you tooconfigure:</span></span>

- <span data-ttu-id="1b84a-119">**Gli utenti possono aggiungere dispositivi tooAzure AD** - questa impostazioni consente agli utenti di hello tooselect in grado di aggiungere dispositivi tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-119">**Users may join devices tooAzure AD** - This settings enables you tooselect hello users who can join devices tooAzure AD.</span></span> <span data-ttu-id="1b84a-120">valore predefinito di Hello è **tutti**.</span><span class="sxs-lookup"><span data-stu-id="1b84a-120">hello default is **All**.</span></span>

- <span data-ttu-id="1b84a-121">**Altri amministratori locali in Azure AD i dispositivi appartenenti** -è possibile selezionare gli utenti di hello che vengono concessi diritti di amministratore locale su un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b84a-121">**Additional local administrators on Azure AD joined devices** - You can select hello users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="1b84a-122">Gli utenti aggiunti vengono aggiunti toohello *amministratori dispositivo* ruolo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-122">Users added here are added toohello *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="1b84a-123">Agli amministratori globali di Azure AD e ai proprietari dei dispositivi vengono concessi i diritti di amministratore locale per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="1b84a-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="1b84a-124">Questa opzione è una funzionalità di edizione premium disponibile tramite prodotti, come Azure AD Premium o Enterprise Mobility Suite (EMS) hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-124">This option is a premium edition capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="1b84a-125">**Gli utenti possono registrare i propri dispositivi con Azure AD** -è necessario tooconfigure toobe di dispositivi tooallow questa impostazione è registrato con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-125">**Users may register their devices with Azure AD** - You need tooconfigure this setting tooallow devices toobe registered with Azure AD.</span></span> <span data-ttu-id="1b84a-126">Se si seleziona **Nessuno**, i dispositivi non sono consentiti tooregister quando non sono parte di Azure AD o ibrida aggiunto AD Azure.</span><span class="sxs-lookup"><span data-stu-id="1b84a-126">If you select **None**, devices are not allowed tooregister when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="1b84a-127">L'iscrizione a Microsoft Intune o Gestione dispositivi mobili per Office 365 richiede la registrazione.</span><span class="sxs-lookup"><span data-stu-id="1b84a-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="1b84a-128">Se è stato configurato uno di questi servizi, sarà selezionata l'opzione **TUTTI**, mentre l'opzione **NESSUNO** sarà disabilitata.</span><span class="sxs-lookup"><span data-stu-id="1b84a-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="1b84a-129">**Richiedi multi-Factor Authentication toojoin dispositivi** -è possibile scegliere se gli utenti sono necessari tooprovide una seconda autenticazione fattori toojoin loro tooAzure dispositivo Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1b84a-129">**Require Multi-Factor Auth toojoin devices** - You can choose whether users are required tooprovide a second authentication factor toojoin their device tooAzure AD.</span></span> <span data-ttu-id="1b84a-130">valore predefinito di Hello è **n**.</span><span class="sxs-lookup"><span data-stu-id="1b84a-130">hello default is **No**.</span></span> <span data-ttu-id="1b84a-131">Si consiglia di richiedere l'autenticazione a più fattori quando si registra un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="1b84a-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="1b84a-132">Prima di abilitare multi-factor authentication per questo servizio, è necessario assicurarsi che l'autenticazione a più fattori è configurato per gli utenti di hello che registrano i propri dispositivi.</span><span class="sxs-lookup"><span data-stu-id="1b84a-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for hello users that register their devices.</span></span> <span data-ttu-id="1b84a-133">Per altre informazioni sui diversi servizi di autenticazione a più fattori di Azure, vedere [Introduzione ad Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1b84a-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="1b84a-134">**Numero massimo di dispositivi** -questa impostazione consente massimo hello tooselect di dispositivi che un utente può disporre di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-134">**Maximum number of devices** - This setting enables you tooselect hello maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="1b84a-135">Se un utente raggiunge questa quota, non sono in altri dispositivi in grado di tooadd fino a quando una o più dispositivi esistenti hello vengono rimossi.</span><span class="sxs-lookup"><span data-stu-id="1b84a-135">If a user reaches this quota, they are not be able tooadd additional devices until one or more of hello existing devices are removed.</span></span> <span data-ttu-id="1b84a-136">offerta dispositivo Hello viene conteggiata per tutti i dispositivi che sono parte di Azure AD o Azure AD attualmente registrata.</span><span class="sxs-lookup"><span data-stu-id="1b84a-136">hello device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="1b84a-137">valore predefinito di Hello è **20**.</span><span class="sxs-lookup"><span data-stu-id="1b84a-137">hello default value is **20**.</span></span>

- <span data-ttu-id="1b84a-138">**Gli utenti possono sincronizzare le impostazioni e dati delle app tra dispositivi** -per impostazione predefinita, questa impostazione è troppo**Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="1b84a-138">**Users may sync settings and app data across devices** - By default, this setting is set too**NONE**.</span></span> <span data-ttu-id="1b84a-139">Selezionare utenti specifici o gruppi o tutti consente le impostazioni dell'utente hello e app dati toosync tra i propri dispositivi Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1b84a-139">Selecting specific users or groups or ALL allows hello user’s settings and app data toosync across their Windows 10 devices.</span></span> <span data-ttu-id="1b84a-140">Leggere altre informazioni sul funzionamento della sincronizzazione in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="1b84a-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="1b84a-141">Questa opzione è delle funzionalità disponibile tramite prodotti, come Azure AD Premium o Enterprise Mobility Suite (EMS) hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-141">This option is a premium capability available through products such as Azure AD Premium or hello Enterprise Mobility Suite (EMS).</span></span>
 
    ![Gestire un dispositivo Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="1b84a-143">Individuare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="1b84a-143">Locate devices</span></span>

<span data-ttu-id="1b84a-144">Come amministratore, nel portale di Azure hello sono disponibili due opzioni toolocate registrato e aggiunto i dispositivi:</span><span class="sxs-lookup"><span data-stu-id="1b84a-144">As an administrator, in hello Azure portal, you have two options toolocate registered and joined devices:</span></span>

- <span data-ttu-id="1b84a-145">**Tutti i dispositivi** in hello **Gestisci** sezione di hello **dispositivi** pannello</span><span class="sxs-lookup"><span data-stu-id="1b84a-145">**All devices** in hello **Manage** section of hello **Devices** blade</span></span>  

    ![Tutti i dispositivi](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="1b84a-147">**Dispositivi** in hello **Gestisci** sezione di un **utente** pannello</span><span class="sxs-lookup"><span data-stu-id="1b84a-147">**Devices** in hello **Manage** section of a **User** blade</span></span>
 
    ![Tutti i dispositivi](./media/device-management-azure-portal/43.png)



<span data-ttu-id="1b84a-149">Con entrambe le opzioni, è possibile ottenere la visualizzazione tooa che:</span><span class="sxs-lookup"><span data-stu-id="1b84a-149">With both options, you can get tooa view that:</span></span>


- <span data-ttu-id="1b84a-150">Consente di toosearch per i dispositivi con nome visualizzato hello come filtro.</span><span class="sxs-lookup"><span data-stu-id="1b84a-150">Enables you toosearch for devices using hello display name as filter.</span></span>

- <span data-ttu-id="1b84a-151">Fornisce una panoramica dettagliata dei dispositivi registrati e aggiunti</span><span class="sxs-lookup"><span data-stu-id="1b84a-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="1b84a-152">Consente di tooperform delle attività di gestione comuni di dispositivi</span><span class="sxs-lookup"><span data-stu-id="1b84a-152">Enables you tooperform common device management tasks</span></span>
   

![Tutti i dispositivi](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="1b84a-154">Attività di gestione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="1b84a-154">Device management tasks</span></span>

<span data-ttu-id="1b84a-155">Come amministratore, è possibile gestire hello registrato o aggiunto i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="1b84a-155">As an administrator, you can manage hello registered or joined devices.</span></span> <span data-ttu-id="1b84a-156">Questa sezione fornisce informazioni sulle attività comuni di gestione dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="1b84a-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="1b84a-157">**Gestire un dispositivo Intune**: un amministratore di Intune può gestire i dispositivi contrassegnati come **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="1b84a-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="1b84a-158">L'amministratore può visualizzare un dispositivo aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="1b84a-158">An administrator can see additional device</span></span> 

![Gestire un dispositivo Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="1b84a-160">**Abilitare o disabilitare un dispositivo Azure AD**</span><span class="sxs-lookup"><span data-stu-id="1b84a-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="1b84a-161">tooenable o disattivare un dispositivo, è necessario toobe un amministratore globale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-161">tooenable or disable a device, you need toobe a global administrator in Azure  AD.</span></span> <span data-ttu-id="1b84a-162">La disabilitazione di un dispositivo ne impedisce l'accesso alle risorse di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="1b84a-163">dispositivo hello toodisable, è possibile fare clic su *...*</span><span class="sxs-lookup"><span data-stu-id="1b84a-163">toodisable hello device, you can either click *…*</span></span> <span data-ttu-id="1b84a-164">Fare clic su dispositivo hello per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="1b84a-164">click hello device for additional details.</span></span>

 
![Gestire un dispositivo Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="1b84a-166">La disabilitazione di un dispositivo cambia lo stato di hello in hello **abilitato** colonna troppo**n**.</span><span class="sxs-lookup"><span data-stu-id="1b84a-166">Disabling a device changes hello state in hello **ENABLED** column too**No**.</span></span>

![Disabilitare un dispositivo](./media/device-management-azure-portal/32.png)


<span data-ttu-id="1b84a-168">**Eliminare un dispositivo di Azure AD** -toodelete un dispositivo, è necessario toobe un amministratore globale di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-168">**Delete an Azure AD device** - toodelete a device, you need toobe a global administrator in Azure AD.</span></span>  
<span data-ttu-id="1b84a-169">L'eliminazione di un dispositivo comporta quanto segue:</span><span class="sxs-lookup"><span data-stu-id="1b84a-169">Deleting a device:</span></span>
 
- <span data-ttu-id="1b84a-170">Impedisce l'accesso del dispositivo alle risorse di Azure AD</span><span class="sxs-lookup"><span data-stu-id="1b84a-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="1b84a-171">Rimuove tutti i dettagli dispositivo toohello collegato, ad esempio, le chiavi di BitLocker per i dispositivi Windows</span><span class="sxs-lookup"><span data-stu-id="1b84a-171">Removes all details that are attached toohello device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="1b84a-172">È un'attività non reversibile e non è consigliata, a meno che non sia necessaria</span><span class="sxs-lookup"><span data-stu-id="1b84a-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="1b84a-173">Se un dispositivo è gestito da un'altra autorità di gestione (ad esempio Microsoft Intune), assicurarsi che il dispositivo hello è stato cancellato / ritirato prima di eliminarlo hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that hello device has been wiped / retired before deleting hello device in Azure AD.</span></span>

<span data-ttu-id="1b84a-174">È possibile selezionare "…"</span><span class="sxs-lookup"><span data-stu-id="1b84a-174">You can either select “…”</span></span> <span data-ttu-id="1b84a-175">toodelete hello dispositivo oppure fare clic sul dispositivo hello per altri dettagli</span><span class="sxs-lookup"><span data-stu-id="1b84a-175">toodelete hello device or click on hello device for additional details</span></span>
 
![Eliminare un dispositivo](./media/device-management-azure-portal/34.png)


<span data-ttu-id="1b84a-177">**Consente di visualizzare o copiare l'ID dispositivo** -è possibile utilizzare un dispositivo ID tooverify hello dispositivo ID dettagli sul dispositivo di hello o utilizzo di PowerShell durante la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="1b84a-177">**View or copy device ID** - You can use a device ID tooverify hello device ID details on hello device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="1b84a-178">copia di hello tooaccess opzione, fare clic su dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-178">tooaccess hello copy option, click hello device.</span></span>

![Visualizzare l'ID dispositivo](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="1b84a-180">**Consente di visualizzare o copiare le chiavi BitLocker** -se si è un amministratore, è possibile visualizzare e hello copia BitLocker chiavi toohelp utenti toorecover le unità crittografata.</span><span class="sxs-lookup"><span data-stu-id="1b84a-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy hello BitLocker keys toohelp users toorecover their encrypted drive.</span></span> <span data-ttu-id="1b84a-181">Queste chiavi sono disponibili solo per i dispositivi Windows crittografati e le cui chiavi sono archiviate in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1b84a-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="1b84a-182">È possibile copiare queste chiavi quando si accede ai dettagli del dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-182">You can copy these keys when accessing details of hello device.</span></span>
 
![Visualizzare le chiavi BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="1b84a-184">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="1b84a-184">Audit logs</span></span>


<span data-ttu-id="1b84a-185">le attività di Hello dispositivo sono disponibili tramite log attività hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-185">hello device activities are available through hello activity logs.</span></span> <span data-ttu-id="1b84a-186">Sono incluse attività attivata dal servizio Registrazione dispositivi di hello o dall'utente hello:</span><span class="sxs-lookup"><span data-stu-id="1b84a-186">This includes activities triggered by hello device registration service or by hello user:</span></span>

- <span data-ttu-id="1b84a-187">Creazione di un dispositivo e l'aggiunta di proprietari/gli utenti sul dispositivo hello</span><span class="sxs-lookup"><span data-stu-id="1b84a-187">Device creation and adding owners/users on hello device</span></span>

- <span data-ttu-id="1b84a-188">Modifica le impostazioni di toodevice</span><span class="sxs-lookup"><span data-stu-id="1b84a-188">Changes toodevice settings</span></span>

- <span data-ttu-id="1b84a-189">Funzionamento del dispositivo, ad esempio eliminazione o aggiornamento</span><span class="sxs-lookup"><span data-stu-id="1b84a-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="1b84a-190">Il toohello punto di ingresso dati di controllo è **log di controllo** in hello **attività** sezione di hello **dispositivi* blade.</span><span class="sxs-lookup"><span data-stu-id="1b84a-190">Your entry point toohello auditing data is **Audit logs** in hello **Activity** section of hello **Devices* blade.</span></span>

![Log di controllo](./media/device-management-azure-portal/61.png)


<span data-ttu-id="1b84a-192">Un log di controllo è una visualizzazione elenco predefinita che include:</span><span class="sxs-lookup"><span data-stu-id="1b84a-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="1b84a-193">Hello data e ora dell'occorrenza hello</span><span class="sxs-lookup"><span data-stu-id="1b84a-193">hello date and time of hello occurrence</span></span>

- <span data-ttu-id="1b84a-194">destinazioni Hello</span><span class="sxs-lookup"><span data-stu-id="1b84a-194">hello targets</span></span>

- <span data-ttu-id="1b84a-195">Hello iniziatore / attore (che) di un'attività</span><span class="sxs-lookup"><span data-stu-id="1b84a-195">hello initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="1b84a-196">attività Hello (novità)</span><span class="sxs-lookup"><span data-stu-id="1b84a-196">hello activity (what)</span></span>

![Log di controllo](./media/device-management-azure-portal/63.png)

<span data-ttu-id="1b84a-198">È possibile personalizzare una visualizzazione elenco hello facendo **colonne** nella barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="1b84a-198">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>
 
![Log di controllo](./media/device-management-azure-portal/64.png)


<span data-ttu-id="1b84a-200">toonarrow verso il basso hello segnalati livello tooa dati che funziona per l'utente, è possibile filtrare i dati di controllo hello utilizzando hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="1b84a-200">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="1b84a-201">Categoria</span><span class="sxs-lookup"><span data-stu-id="1b84a-201">Catergory</span></span>
- <span data-ttu-id="1b84a-202">Activity resource type (Tipo di risorsa dell'attività)</span><span class="sxs-lookup"><span data-stu-id="1b84a-202">Activity resource type</span></span>
- <span data-ttu-id="1b84a-203">Attività</span><span class="sxs-lookup"><span data-stu-id="1b84a-203">Activity</span></span>
- <span data-ttu-id="1b84a-204">Intervallo di date</span><span class="sxs-lookup"><span data-stu-id="1b84a-204">Date range</span></span>
- <span data-ttu-id="1b84a-205">Destinazione</span><span class="sxs-lookup"><span data-stu-id="1b84a-205">Target</span></span>
- <span data-ttu-id="1b84a-206">Azione avviata da (attore)</span><span class="sxs-lookup"><span data-stu-id="1b84a-206">Initiated By (Actor)</span></span>

<span data-ttu-id="1b84a-207">Inoltre toohello filtri, è possibile cercare voci specifiche.</span><span class="sxs-lookup"><span data-stu-id="1b84a-207">In addition toohello filters, you can search for specific entries.</span></span>

![Log di controllo](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="1b84a-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b84a-209">Next steps</span></span>

* [<span data-ttu-id="1b84a-210">Gestione toodevice introduzione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1b84a-210">Introduction toodevice management in Azure Active Directory</span></span>](device-management-introduction.md)



