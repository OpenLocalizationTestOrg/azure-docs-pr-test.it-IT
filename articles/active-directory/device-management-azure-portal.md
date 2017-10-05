---
title: Gestione dei dispositivi tramite il portale di Azure - Anteprima | Microsoft Docs
description: Informazioni su come usare il portale di Azure per gestire i dispositivi.
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
ms.openlocfilehash: 4b46e1627a229b0649d9ccd2550cd28fda9849f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="managing-devices-using-the-azure-portal---preview"></a><span data-ttu-id="25c89-103">Gestione dei dispositivi tramite il portale di Azure - Anteprima</span><span class="sxs-lookup"><span data-stu-id="25c89-103">Managing devices using the Azure portal - preview</span></span>

>[!NOTE]
><span data-ttu-id="25c89-104">Questa funzionalità è attualmente disponibile in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="25c89-104">This capability currently is in public preview.</span></span> <span data-ttu-id="25c89-105">Potrebbe essere necessario ripristinare o rimuovere eventuali modifiche.</span><span class="sxs-lookup"><span data-stu-id="25c89-105">Be prepared to revert or remove any changes.</span></span> <span data-ttu-id="25c89-106">La funzionalità è disponibile in tutte le sottoscrizioni di Azure Active Directory (Azure AD) durante l'anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="25c89-106">The feature is available in any Azure Active Directory (Azure AD) subscription during public preview.</span></span> <span data-ttu-id="25c89-107">Quando la funzionalità sarà disponibile a livello generale, alcuni aspetti potrebbero tuttavia richiedere una sottoscrizione Azure Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="25c89-107">However, when the feature becomes generally available, some aspects of the feature might require an Azure Active Directory premium subscription.</span></span>


<span data-ttu-id="25c89-108">Tramite la gestione dei dispositivi in Azure Active Directory (Azure AD) è possibile garantire che gli utenti accedano alle risorse da dispositivi che soddisfano gli standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="25c89-108">With device management in Azure Active Directory (Azure AD), you can ensure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="25c89-109">In questo argomento:</span><span class="sxs-lookup"><span data-stu-id="25c89-109">This topic:</span></span>

- <span data-ttu-id="25c89-110">Si presuppone che l'utente abbia familiarità con quanto descritto in [Introduzione alla gestione dei dispositivi in Azure Active Directory](device-management-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="25c89-110">Assumes that you are familiar with the [introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>

- <span data-ttu-id="25c89-111">Vengono fornite informazioni sulla gestione dei dispositivi tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="25c89-111">Provides you with information about managing your devices using the Azure portal</span></span>


<span data-ttu-id="25c89-112">Per gestire i dispositivi nel portale di Azure, è necessario fare clic su **Dispositivi** nella sezione **Gestisci** del pannello **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="25c89-112">To manage devices in the Azure portal, you need to click **Devices** in the **Manage** section of the the **Azure Active Directory** blade.</span></span>

![Gestire un dispositivo Intune](./media/device-management-azure-portal/11.png)




## <a name="configure-device-settings"></a><span data-ttu-id="25c89-114">Configurare le impostazioni dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="25c89-114">Configure device settings</span></span>

<span data-ttu-id="25c89-115">Per gestire i dispositivi tramite il portale di Azure, è necessario che i dispositivi siano registrati o aggiunti in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-115">To manage your devices using the Azure portal, they need to be either registered or joined to Azure AD.</span></span> <span data-ttu-id="25c89-116">Un amministratore può ottimizzare il processo di registrazione e aggiunta dei dispositivi configurando le relative impostazioni.</span><span class="sxs-lookup"><span data-stu-id="25c89-116">As an administrator, you can fine-tune the process of registering and joining devices by configuring the device settings.</span></span>

![Gestire un dispositivo Intune](./media/device-management-azure-portal/22.png)


<span data-ttu-id="25c89-118">Il pannello delle impostazioni dei dispositivi consente di configurare:</span><span class="sxs-lookup"><span data-stu-id="25c89-118">The device settings blade enables you to configure:</span></span>

- <span data-ttu-id="25c89-119">**Gli utenti possono aggiungere dispositivi ad Azure AD**: questa impostazione consente di selezionare gli utenti che possono aggiungere dispositivi ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-119">**Users may join devices to Azure AD** - This settings enables you to select the users who can join devices to Azure AD.</span></span> <span data-ttu-id="25c89-120">L'impostazione predefinita è **Tutti**.</span><span class="sxs-lookup"><span data-stu-id="25c89-120">The default is **All**.</span></span>

- <span data-ttu-id="25c89-121">**Amministratori locali aggiuntivi su dispositivi aggiunti ad Azure AD**: è possibile selezionare gli utenti a cui vengono concessi i diritti di amministratore locale per un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25c89-121">**Additional local administrators on Azure AD joined devices** - You can select the users that are granted local administrator rights on a device.</span></span> <span data-ttu-id="25c89-122">Gli utenti aggiunti in questa posizione vengono aggiunti al ruolo *Amministratori di dispositivi* in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-122">Users added here are added to the *Device Administrators* role in Azure AD.</span></span> <span data-ttu-id="25c89-123">Agli amministratori globali di Azure AD e ai proprietari dei dispositivi vengono concessi i diritti di amministratore locale per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="25c89-123">Global administrators in Azure AD and device owners are granted local administrator rights by default.</span></span> <span data-ttu-id="25c89-124">Questa opzione è una funzionalità dell'edizione Premium disponibile tramite prodotti come Azure AD Premium o Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="25c89-124">This option is a premium edition capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span> 

- <span data-ttu-id="25c89-125">**Gli utenti possono registrare i propri dispositivi in Azure AD**: è necessario configurare questa impostazione per consentire la registrazione dei dispositivi con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-125">**Users may register their devices with Azure AD** - You need to configure this setting to allow devices to be registered with Azure AD.</span></span> <span data-ttu-id="25c89-126">Se si seleziona **Nessuno**, ai dispositivi non è consentito eseguire la registrazione se non sono aggiunti ad Azure AD o all'identità ibrida di AD Azure.</span><span class="sxs-lookup"><span data-stu-id="25c89-126">If you select **None**, devices are not allowed to register when they are not Azure AD joined or hybrid Azure AD joined.</span></span> <span data-ttu-id="25c89-127">L'iscrizione a Microsoft Intune o Gestione dispositivi mobili per Office 365 richiede la registrazione.</span><span class="sxs-lookup"><span data-stu-id="25c89-127">Enrollment with Microsoft Intune or Mobile Device Management (MDM) for Office 365 requires registration.</span></span> <span data-ttu-id="25c89-128">Se è stato configurato uno di questi servizi, sarà selezionata l'opzione **TUTTI**, mentre l'opzione **NESSUNO** sarà disabilitata.</span><span class="sxs-lookup"><span data-stu-id="25c89-128">If you have configured either of these services, **ALL** is selected and **NONE** is not available..</span></span>

- <span data-ttu-id="25c89-129">**Richiedi Multi-factor Auth per aggiungere i dispositivi**: è possibile scegliere se richiedere agli utenti di fornire un secondo fattore di autenticazione per aggiungere il dispositivo ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-129">**Require Multi-Factor Auth to join devices** - You can choose whether users are required to provide a second authentication factor to join their device to Azure AD.</span></span> <span data-ttu-id="25c89-130">Il valore predefinito è **No**.</span><span class="sxs-lookup"><span data-stu-id="25c89-130">The default is **No**.</span></span> <span data-ttu-id="25c89-131">Si consiglia di richiedere l'autenticazione a più fattori quando si registra un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25c89-131">We recommend requiring multi-factor authentication when registering a device.</span></span> <span data-ttu-id="25c89-132">Per abilitare l'autenticazione a più fattori per questo servizio, è necessario verificare che tale tipo di autenticazione sia configurato per gli utenti che registrano i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="25c89-132">Before you enable multi-factor authentication for this service, you must ensure that multi-factor authentication is configured for the users that register their devices.</span></span> <span data-ttu-id="25c89-133">Per altre informazioni sui diversi servizi di autenticazione a più fattori di Azure, vedere [Introduzione ad Azure Multi-Factor Authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="25c89-133">For more information on different Azure multi-factor authentication services, see [getting started with Azure multi-factor authentication](../multi-factor-authentication/multi-factor-authentication-get-started.md).</span></span> 

- <span data-ttu-id="25c89-134">**Numero massimo di dispositivi per utente**: questa impostazione consente di selezionare il numero massimo di dispositivi che un utente può avere in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-134">**Maximum number of devices** - This setting enables you to select the maximum number of devices that a user can have in Azure AD.</span></span> <span data-ttu-id="25c89-135">Se un utente raggiunge la quota specificata, non potrà aggiungere altri dispositivi fino a quando non vengono rimossi uno o più dispositivi esistenti.</span><span class="sxs-lookup"><span data-stu-id="25c89-135">If a user reaches this quota, they are not be able to add additional devices until one or more of the existing devices are removed.</span></span> <span data-ttu-id="25c89-136">La quota dei dispositivi viene calcolata considerando tutti i dispositivi attualmente aggiunti ad Azure AD o registrati in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-136">The device quote is counted for all devices that are either Azure AD joined or Azure AD registered today.</span></span> <span data-ttu-id="25c89-137">Il valore predefinito è **20**.</span><span class="sxs-lookup"><span data-stu-id="25c89-137">The default value is **20**.</span></span>

- <span data-ttu-id="25c89-138">**Gli utenti possono sincronizzare le impostazioni e i dati delle app su tutti i dispositivi**: per impostazione predefinita, il valore di questa opzione è **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="25c89-138">**Users may sync settings and app data across devices** - By default, this setting is set to **NONE**.</span></span> <span data-ttu-id="25c89-139">Se si selezionano utenti o gruppi specifici oppure l'opzione TUTTI, si consente la sincronizzazione delle impostazioni dell'utente e dei dati delle app tra i dispositivi Windows 10.</span><span class="sxs-lookup"><span data-stu-id="25c89-139">Selecting specific users or groups or ALL allows the user’s settings and app data to sync across their Windows 10 devices.</span></span> <span data-ttu-id="25c89-140">Leggere altre informazioni sul funzionamento della sincronizzazione in Windows 10.</span><span class="sxs-lookup"><span data-stu-id="25c89-140">Learn more on how sync works in Windows 10.</span></span>
<span data-ttu-id="25c89-141">Questa opzione è una funzionalità Premium disponibile tramite prodotti come Azure AD Premium o Enterprise Mobility Suite (EMS).</span><span class="sxs-lookup"><span data-stu-id="25c89-141">This option is a premium capability available through products such as Azure AD Premium or the Enterprise Mobility Suite (EMS).</span></span>
 
    ![Gestire un dispositivo Intune](./media/device-management-azure-portal/21.png)




## <a name="locate-devices"></a><span data-ttu-id="25c89-143">Individuare i dispositivi</span><span class="sxs-lookup"><span data-stu-id="25c89-143">Locate devices</span></span>

<span data-ttu-id="25c89-144">Un amministratore nel portale di Azure dispone di due opzioni per individuare i dispositivi registrati e aggiunti:</span><span class="sxs-lookup"><span data-stu-id="25c89-144">As an administrator, in the Azure portal, you have two options to locate registered and joined devices:</span></span>

- <span data-ttu-id="25c89-145">**Tutti i dispositivi** nella sezione **Gestisci** del pannello **Dispositivi**</span><span class="sxs-lookup"><span data-stu-id="25c89-145">**All devices** in the **Manage** section of the **Devices** blade</span></span>  

    ![Tutti i dispositivi](./media/device-management-azure-portal/41.png)


- <span data-ttu-id="25c89-147">**Dispositivi** nella sezione **Gestisci** di un pannello **Utente**</span><span class="sxs-lookup"><span data-stu-id="25c89-147">**Devices** in the **Manage** section of a **User** blade</span></span>
 
    ![Tutti i dispositivi](./media/device-management-azure-portal/43.png)



<span data-ttu-id="25c89-149">Con entrambe le opzioni, è possibile ottenere una vista che:</span><span class="sxs-lookup"><span data-stu-id="25c89-149">With both options, you can get to a view that:</span></span>


- <span data-ttu-id="25c89-150">Consente di cercare i dispositivi usando il nome visualizzato come filtro.</span><span class="sxs-lookup"><span data-stu-id="25c89-150">Enables you to search for devices using the display name as filter.</span></span>

- <span data-ttu-id="25c89-151">Fornisce una panoramica dettagliata dei dispositivi registrati e aggiunti</span><span class="sxs-lookup"><span data-stu-id="25c89-151">Provides you with detailed overview of registered and joined devices</span></span>

- <span data-ttu-id="25c89-152">Consente di eseguire attività comuni di gestione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="25c89-152">Enables you to perform common device management tasks</span></span>
   

![Tutti i dispositivi](./media/device-management-azure-portal/51.png)


## <a name="device-management-tasks"></a><span data-ttu-id="25c89-154">Attività di gestione dei dispositivi</span><span class="sxs-lookup"><span data-stu-id="25c89-154">Device management tasks</span></span>

<span data-ttu-id="25c89-155">L'amministratore può gestire i dispositivi registrati o aggiunti.</span><span class="sxs-lookup"><span data-stu-id="25c89-155">As an administrator, you can manage the registered or joined devices.</span></span> <span data-ttu-id="25c89-156">Questa sezione fornisce informazioni sulle attività comuni di gestione dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="25c89-156">This section provides you with information about common device management tasks.</span></span>


<span data-ttu-id="25c89-157">**Gestire un dispositivo Intune**: un amministratore di Intune può gestire i dispositivi contrassegnati come **Microsoft Intune**.</span><span class="sxs-lookup"><span data-stu-id="25c89-157">**Manage an Intune device** - If you are an Intune administrator, you can manage devices marked as **Microsoft Intune**.</span></span> <span data-ttu-id="25c89-158">L'amministratore può visualizzare un dispositivo aggiuntivo</span><span class="sxs-lookup"><span data-stu-id="25c89-158">An administrator can see additional device</span></span> 

![Gestire un dispositivo Intune](./media/device-management-azure-portal/31.png)


<span data-ttu-id="25c89-160">**Abilitare o disabilitare un dispositivo Azure AD**</span><span class="sxs-lookup"><span data-stu-id="25c89-160">**Enable / disable an Azure AD device**</span></span>

<span data-ttu-id="25c89-161">Per abilitare o disabilitare un dispositivo, è necessario essere un amministratore globale in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-161">To enable or disable a device, you need to be a global administrator in Azure  AD.</span></span> <span data-ttu-id="25c89-162">La disabilitazione di un dispositivo ne impedisce l'accesso alle risorse di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-162">Disabling a device prevents a device from accessing your Azure AD resources.</span></span>  <span data-ttu-id="25c89-163">Per disabilitare il dispositivo, è possibile fare clic su *...*</span><span class="sxs-lookup"><span data-stu-id="25c89-163">To disable the device, you can either click *…*</span></span> <span data-ttu-id="25c89-164">o fare clic sul dispositivo per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="25c89-164">click the device for additional details.</span></span>

 
![Gestire un dispositivo Intune](./media/device-management-azure-portal/33.png)

<span data-ttu-id="25c89-166">Se un dispositivo viene disabilitato, lo stato nella colonna **ABILITATO** viene impostato su **No**.</span><span class="sxs-lookup"><span data-stu-id="25c89-166">Disabling a device changes the state in the **ENABLED** column to **No**.</span></span>

![Disabilitare un dispositivo](./media/device-management-azure-portal/32.png)


<span data-ttu-id="25c89-168">**Eliminare un dispositivo Azure AD**: per eliminare un dispositivo, è necessario essere un amministratore globale in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-168">**Delete an Azure AD device** - To delete a device, you need to be a global administrator in Azure AD.</span></span>  
<span data-ttu-id="25c89-169">L'eliminazione di un dispositivo comporta quanto segue:</span><span class="sxs-lookup"><span data-stu-id="25c89-169">Deleting a device:</span></span>
 
- <span data-ttu-id="25c89-170">Impedisce l'accesso del dispositivo alle risorse di Azure AD</span><span class="sxs-lookup"><span data-stu-id="25c89-170">Prevents a device from accessing your Azure AD resources</span></span> 

- <span data-ttu-id="25c89-171">Rimuove tutti i dettagli collegati al dispositivo, ad esempio, le chiavi BitLocker per i dispositivi Windows</span><span class="sxs-lookup"><span data-stu-id="25c89-171">Removes all details that are attached to the device, for example, BitLocker keys for Windows devices</span></span>  

- <span data-ttu-id="25c89-172">È un'attività non reversibile e non è consigliata, a meno che non sia necessaria</span><span class="sxs-lookup"><span data-stu-id="25c89-172">Represents a non-recoverable activity and is not recommended unless it is required</span></span>

<span data-ttu-id="25c89-173">Se un dispositivo è gestito da un'altra autorità di gestione (ad esempio Microsoft Intune), assicurarsi che sia stato cancellato o disattivato prima di eliminarlo in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-173">If a device is managed by another management authority (e.g. Microsoft Intune), please make sure that the device has been wiped / retired before deleting the device in Azure AD.</span></span>

<span data-ttu-id="25c89-174">È possibile selezionare "…"</span><span class="sxs-lookup"><span data-stu-id="25c89-174">You can either select “…”</span></span> <span data-ttu-id="25c89-175">per eliminare il dispositivo oppure fare clic sul dispositivo per altri dettagli</span><span class="sxs-lookup"><span data-stu-id="25c89-175">to delete the device or click on the device for additional details</span></span>
 
![Eliminare un dispositivo](./media/device-management-azure-portal/34.png)


<span data-ttu-id="25c89-177">**Visualizzare o copiare l'ID dispositivo**: è possibile usare l'ID di un dispositivo per verificare i relativi dettagli nel dispositivo o per l'uso in PowerShell in fase di risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="25c89-177">**View or copy device ID** - You can use a device ID to verify the device ID details on the device or using PowerShell during troubleshooting.</span></span> <span data-ttu-id="25c89-178">Per accedere all'opzione di copia, fare clic sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25c89-178">To access the copy option, click the device.</span></span>

![Visualizzare l'ID dispositivo](./media/device-management-azure-portal/35.png)
  

<span data-ttu-id="25c89-180">**Visualizzare o copiare le chiavi BitLocker**: un amministratore può visualizzare e copiare le chiavi BitLocker per aiutare gli utenti a recuperare l'unità crittografata.</span><span class="sxs-lookup"><span data-stu-id="25c89-180">**View or copy BitLocker keys** - If you are an administrator, you can view and copy the BitLocker keys to help users to recover their encrypted drive.</span></span> <span data-ttu-id="25c89-181">Queste chiavi sono disponibili solo per i dispositivi Windows crittografati e le cui chiavi sono archiviate in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="25c89-181">These keys are only available for Windows devices that are encrypted and have their keys stored in Azure AD.</span></span> <span data-ttu-id="25c89-182">È possibile copiare queste chiavi quando si accede ai dettagli del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="25c89-182">You can copy these keys when accessing details of the device.</span></span>
 
![Visualizzare le chiavi BitLocker](./media/device-management-azure-portal/36.png)



## <a name="audit-logs"></a><span data-ttu-id="25c89-184">Log di controllo</span><span class="sxs-lookup"><span data-stu-id="25c89-184">Audit logs</span></span>


<span data-ttu-id="25c89-185">Le attività del dispositivo sono disponibili tramite i log attività.</span><span class="sxs-lookup"><span data-stu-id="25c89-185">The device activities are available through the activity logs.</span></span> <span data-ttu-id="25c89-186">I log includono le attività avviate dal servizio di registrazione dispositivo o dall'utente:</span><span class="sxs-lookup"><span data-stu-id="25c89-186">This includes activities triggered by the device registration service or by the user:</span></span>

- <span data-ttu-id="25c89-187">Creazione di un dispositivo e aggiunta di proprietari/utenti nel dispositivo</span><span class="sxs-lookup"><span data-stu-id="25c89-187">Device creation and adding owners/users on the device</span></span>

- <span data-ttu-id="25c89-188">Modifiche alle impostazioni del dispositivo</span><span class="sxs-lookup"><span data-stu-id="25c89-188">Changes to device settings</span></span>

- <span data-ttu-id="25c89-189">Funzionamento del dispositivo, ad esempio eliminazione o aggiornamento</span><span class="sxs-lookup"><span data-stu-id="25c89-189">Device operations such as deleting or updating a device</span></span>
 
<span data-ttu-id="25c89-190">Il punto di ingresso ai dati di controllo è **Log di controllo** nella sezione **Attività** del pannello **Dispositivi*.</span><span class="sxs-lookup"><span data-stu-id="25c89-190">Your entry point to the auditing data is **Audit logs** in the **Activity** section of the **Devices* blade.</span></span>

![Log di controllo](./media/device-management-azure-portal/61.png)


<span data-ttu-id="25c89-192">Un log di controllo è una visualizzazione elenco predefinita che include:</span><span class="sxs-lookup"><span data-stu-id="25c89-192">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="25c89-193">Data e ora dell'occorrenza.</span><span class="sxs-lookup"><span data-stu-id="25c89-193">the date and time of the occurrence</span></span>

- <span data-ttu-id="25c89-194">Destinazioni</span><span class="sxs-lookup"><span data-stu-id="25c89-194">the targets</span></span>

- <span data-ttu-id="25c89-195">Iniziatore/attore di un'attività (chi)</span><span class="sxs-lookup"><span data-stu-id="25c89-195">the initiator / actor (who) of an activity</span></span>

- <span data-ttu-id="25c89-196">Attività (cosa)</span><span class="sxs-lookup"><span data-stu-id="25c89-196">the activity (what)</span></span>

![Log di controllo](./media/device-management-azure-portal/63.png)

<span data-ttu-id="25c89-198">Per personalizzare la visualizzazione elenco, fare clic su **Colonne** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="25c89-198">You can customize the list view by clicking **Columns** in the toolbar.</span></span>
 
![Log di controllo](./media/device-management-azure-portal/64.png)


<span data-ttu-id="25c89-200">Per limitare i dati segnalati in base alle esigenze, è possibile filtrare i dati di controllo usando i campi seguenti:</span><span class="sxs-lookup"><span data-stu-id="25c89-200">To narrow down the reported data to a level that works for you, you can filter the audit data using the following fields:</span></span>

- <span data-ttu-id="25c89-201">Categoria</span><span class="sxs-lookup"><span data-stu-id="25c89-201">Catergory</span></span>
- <span data-ttu-id="25c89-202">Activity resource type (Tipo di risorsa dell'attività)</span><span class="sxs-lookup"><span data-stu-id="25c89-202">Activity resource type</span></span>
- <span data-ttu-id="25c89-203">Attività</span><span class="sxs-lookup"><span data-stu-id="25c89-203">Activity</span></span>
- <span data-ttu-id="25c89-204">Intervallo di date</span><span class="sxs-lookup"><span data-stu-id="25c89-204">Date range</span></span>
- <span data-ttu-id="25c89-205">Destinazione</span><span class="sxs-lookup"><span data-stu-id="25c89-205">Target</span></span>
- <span data-ttu-id="25c89-206">Azione avviata da (attore)</span><span class="sxs-lookup"><span data-stu-id="25c89-206">Initiated By (Actor)</span></span>

<span data-ttu-id="25c89-207">Oltre a usare i filtri, è possibile cercare voci specifiche.</span><span class="sxs-lookup"><span data-stu-id="25c89-207">In addition to the filters, you can search for specific entries.</span></span>

![Log di controllo](./media/device-management-azure-portal/65.png)

## <a name="next-steps"></a><span data-ttu-id="25c89-209">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="25c89-209">Next steps</span></span>

* <span data-ttu-id="25c89-210">[Introduction to device management in Azure Active Directory](device-management-introduction.md) (Introduzione alla gestione dei dispositivi in Azure Active Directory)</span><span class="sxs-lookup"><span data-stu-id="25c89-210">[Introduction to device management in Azure Active Directory](device-management-introduction.md)</span></span>



