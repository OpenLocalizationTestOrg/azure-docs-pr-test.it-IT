---
title: aaaHow tooconfigure la registrazione automatica dei dispositivi appartenenti a un dominio di Windows con Azure Active Directory | Documenti Microsoft
description: Configurare i server appartenenti a un dominio Windows dispositivi tooregister automatico e invisibile con Azure Active Directory.
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 1d736eba734418231f12e23a8fc1a93405f129c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="d54d7-103">Introduzione a Registrazione dispositivo Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d54d7-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="d54d7-104">Registrazione dispositivo di Azure Active Directory è foundation hello per gli scenari di accesso condizionale basato su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d54d7-104">Azure Active Directory device registration is hello foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="d54d7-105">Quando un dispositivo viene registrato, registrazione dispositivo Azure Active Directory fornisce dispositivo hello con un'identità che è dispositivo hello tooauthenticate usato quando hello utente accede.</span><span class="sxs-lookup"><span data-stu-id="d54d7-105">When a device is registered, Azure Active Directory device registration provides hello device with an identity which is used tooauthenticate hello device when hello user signs in.</span></span> <span data-ttu-id="d54d7-106">dispositivo Hello autenticato e gli attributi di hello del dispositivo hello, possono quindi essere tooenforce utilizzato Criteri di accesso condizionale per le applicazioni ospitate nel cloud hello e locale.</span><span class="sxs-lookup"><span data-stu-id="d54d7-106">hello authenticated device, and hello attributes of hello device, can then be used tooenforce conditional access policies for applications that are hosted in hello cloud and on-premises.</span></span>

<span data-ttu-id="d54d7-107">Se combinato con una soluzione di management(MDM) di dispositivi mobili, ad esempio Microsoft Intune, sugli attributi del dispositivo hello in Azure Active Directory vengono aggiornati con informazioni aggiuntive sul dispositivo di hello.</span><span class="sxs-lookup"><span data-stu-id="d54d7-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure Active Directory are updated with additional information about hello device.</span></span> <span data-ttu-id="d54d7-108">Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="d54d7-108">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="d54d7-109">Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere l'articolo "Registrare i dispositivi per la gestione in Intune".</span><span class="sxs-lookup"><span data-stu-id="d54d7-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="d54d7-110">Gli scenari consentiti da Registrazione dispositivo Azure Active Directory includono il supporto per dispositivi iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="d54d7-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="d54d7-111">Hello singoli scenari in cui viene utilizzata la registrazione del dispositivo di Azure Active Directory potrebbero essere più specifici requisiti e piattaforme supportano.</span><span class="sxs-lookup"><span data-stu-id="d54d7-111">hello individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="d54d7-112">Questi scenari sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="d54d7-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="d54d7-113">**Accesso condizionale per applicazioni di Office 365 con Microsoft Intune:** gli amministratori IT possono effettuare il provisioning di accesso condizionale dispositivo criteri toosecure alle risorse aziendali, mentre in hello la stessa ora che consente agli information worker su dispositivi conformi servizi di hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="d54d7-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies toosecure corporate resources, while at hello same time allowing information workers on compliant devices tooaccess hello services.</span></span> <span data-ttu-id="d54d7-114">Per altre informazioni, vedere Criteri di accesso condizionale dei dispositivi per i servizi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="d54d7-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="d54d7-115">**Tooapplications di accesso condizionale che sono ospitati in locale:** è possibile utilizzare i dispositivi registrati con criteri di accesso per le applicazioni che vengono configurate toouse AD FS con Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="d54d7-115">**Conditional access tooapplications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured toouse AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="d54d7-116">Per altre informazioni su come configurare l'accesso condizionale in locale, vedere [Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d54d7-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="d54d7-117">Configurazione della Registrazione dispositivo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d54d7-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="d54d7-118">registrazione dei dispositivi toosetup, sono disponibili diverse opzioni:</span><span class="sxs-lookup"><span data-stu-id="d54d7-118">toosetup device registration, you have multiple options:</span></span>

- <span data-ttu-id="d54d7-119">Possono registrare dispositivi quando dominio unita in join tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d54d7-119">Devices can register when joined tooAzure AD domain.</span></span> <span data-ttu-id="d54d7-120">Per ulteriori informazioni su questo argomento, è possibile ulteriori informazioni sulle impostazioni di aggiunta ad Azure AD e hello necessari per il dominio di Azure AD toojoin gli utenti.</span><span class="sxs-lookup"><span data-stu-id="d54d7-120">For more on this topic, you can Learn more about Azure AD Join and hello settings required for users toojoin Azure AD domain.</span></span>

- <span data-ttu-id="d54d7-121">È possibile registrare dispositivi quando gli utenti di aggiungere lavoro o scuola account tooWindows in un dispositivo personale o quando i dispositivi mobili si connettono alle risorse di lavoro tooa richiedere la registrazione.</span><span class="sxs-lookup"><span data-stu-id="d54d7-121">Devices can be registered when users add work or school accounts tooWindows on a personal device or when mobile devices connect tooa work resources requiring registration.</span></span> <span data-ttu-id="d54d7-122">tooensure, è necessario abilitare registrazione dispositivo di Azure Active Directory nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d54d7-122">tooensure this, you must enable Azure AD Device Registration in hello Azure Portal.</span></span> 

- <span data-ttu-id="d54d7-123">Registrazione automatica dei dispositivi per i computer aggiunti a un dominio tradizionale.</span><span class="sxs-lookup"><span data-stu-id="d54d7-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="d54d7-124">tooensure, prima di continuare con la registrazione automatica dei dispositivi, è necessario prima il programma di installazione Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d54d7-124">tooensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="d54d7-125">Per istruzioni più recenti, vedere [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d54d7-125">For latest instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="d54d7-126">È anche possibile esaminare e abilitare o disabilitare i dispositivi registrati mediante hello portale dell'amministratore in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d54d7-126">You can also review and enable or disable registered devices using hello Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-hello-azure-active-directory-device-registration-service"></a><span data-ttu-id="d54d7-127">Abilitare il servizio registrazione dispositivo di Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="d54d7-127">Enable hello Azure Active Directory device registration service</span></span>

<span data-ttu-id="d54d7-128">**hello tooenable servizio Registrazione dispositivi di Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-128">**tooenable hello Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="d54d7-129">Accedi toohello portale Microsoft Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d54d7-129">Sign in toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="d54d7-130">Nel riquadro sinistro di hello selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-130">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="d54d7-131">Nella scheda Directory hello, selezionare la directory.</span><span class="sxs-lookup"><span data-stu-id="d54d7-131">On hello Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="d54d7-132">Fare clic su **Configure**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="d54d7-133">Scorrere troppo**dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-133">Scroll too**Devices**.</span></span>

6.  <span data-ttu-id="d54d7-134">Selezionare Tutti per Gli utenti possono registrare i propri dispositivi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d54d7-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="d54d7-135">Selezionare il numero massimo di hello di dispositivi desiderato tooauthorize per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="d54d7-135">Select hello maximum number of devices you want tooauthorize per user.</span></span>

<span data-ttu-id="d54d7-136">registrazione di Hello con Microsoft Intune o gestione dei dispositivi mobili per Office 365 richiede la registrazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d54d7-136">hello enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="d54d7-137">Se è stato configurato uno di questi servizi, sarà selezionata l'opzione **Tutti** e disabilitata l'opzione **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="d54d7-138">Verificare che siano configurati correttamente e che dispone della licenza hello appropriata.</span><span class="sxs-lookup"><span data-stu-id="d54d7-138">Please ensure that they are configured correctly and have hello appropriate licensing.</span></span>

<span data-ttu-id="d54d7-139">Per impostazione predefinita, l'autenticazione a due fattori non è abilitato per servizio hello.</span><span class="sxs-lookup"><span data-stu-id="d54d7-139">By default, two-factor authentication is not enabled for hello service.</span></span> <span data-ttu-id="d54d7-140">L'autenticazione a due fattori è tuttavia consigliabile quando si registra un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d54d7-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="d54d7-141">Prima di richiedere l'autenticazione a due fattori per questo servizio, è necessario configurare un provider di autenticazione a due fattori in Azure Active Directory e configurare gli account utente per multi-Factor Authentication, vedere Aggiunta di multi-Factor Authentication tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d54d7-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication tooAzure Active Directory</span></span>

- <span data-ttu-id="d54d7-142">Se si usa AD FS con Windows Server 2012 R2, è necessario configurare un modulo di autenticazione a due fattori in AD FS. Vedere l'articolo relativo all'uso di Multi-Factor Authentication con Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="d54d7-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="d54d7-143">Visualizzare e gestire gli oggetti dispositivo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d54d7-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="d54d7-144">Portale dell'amministratore di Azure hello possono visualizzare, bloccare e sbloccare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="d54d7-144">From hello Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="d54d7-145">Un dispositivo bloccato non sarà più possibile tooapplications di accesso che sono configurati tooallow solo i dispositivi registrati.</span><span class="sxs-lookup"><span data-stu-id="d54d7-145">A device that is blocked will no longer have access tooapplications that are configured tooallow only registered devices.</span></span>

<span data-ttu-id="d54d7-146">**tooview e gestire gli oggetti dispositivo in Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="d54d7-146">**tooview and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="d54d7-147">Accedere toohello portale Microsoft Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="d54d7-147">Log on toohello Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="d54d7-148">Nel riquadro sinistro di hello selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-148">On hello left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="d54d7-149">Selezionare la propria directory.</span><span class="sxs-lookup"><span data-stu-id="d54d7-149">Select your directory.</span></span>

4.  <span data-ttu-id="d54d7-150">Selezionare **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="d54d7-151">Fare clic su utente hello per cui si desidera dispositivi hello toosee.</span><span class="sxs-lookup"><span data-stu-id="d54d7-151">Click hello user for which you want toosee hello devices.</span></span>

6.  <span data-ttu-id="d54d7-152">Selezionare **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="d54d7-153">Selezionare **Dispositivi registrati**.</span><span class="sxs-lookup"><span data-stu-id="d54d7-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="d54d7-154">A questo punto, è possibile esaminare, bloccare o sbloccare i dispositivi registrati dell'utente hello.</span><span class="sxs-lookup"><span data-stu-id="d54d7-154">Now, you can review, block, or unblock hello user's registered devices.</span></span>
<span data-ttu-id="d54d7-155">I dispositivi Windows 10 che sono locali appartenenti a un dominio e registrati automaticamente non vengono visualizzati nella scheda utenti hello. Utilizzare toofind di comando PowerShell Get-MsolDevice hello tutti i dispositivi dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="d54d7-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under hello Users tab. Please use hello Get-MsolDevice PowerShell command toofind all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d54d7-156">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d54d7-156">Next steps</span></span>

<span data-ttu-id="d54d7-157">toosetup automatizzata registrazione dei dispositivi, vedere [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="d54d7-157">toosetup automated device registration, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


