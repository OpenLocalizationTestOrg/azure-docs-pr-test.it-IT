---
title: Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio | Microsoft Docs
description: Registrare con Azure Active Directory i dispositivi Windows aggiunti a un dominio in modo automatico e invisibile all'utente.
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
ms.openlocfilehash: 38750050e8525272079e1f3a5509da1e8f0a557b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a><span data-ttu-id="8e523-103">Introduzione a Registrazione dispositivo Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e523-103">Get started with Azure Active Directory device registration</span></span>

<span data-ttu-id="8e523-104">Registrazione dispositivo Azure Active Directory rappresenta il fondamento per gli scenari di accesso condizionale basato su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e523-104">Azure Active Directory device registration is the foundation for device-based conditional access scenarios.</span></span> <span data-ttu-id="8e523-105">Quando un dispositivo viene registrato, Registrazione dispositivo Azure Active Directory fornisce al dispositivo un'identità che viene usata per autenticare il dispositivo quando l'utente esegue l'accesso.</span><span class="sxs-lookup"><span data-stu-id="8e523-105">When a device is registered, Azure Active Directory device registration provides the device with an identity which is used to authenticate the device when the user signs in.</span></span> <span data-ttu-id="8e523-106">Il dispositivo autenticato e gli attributi del dispositivo possono quindi essere usati per imporre criteri di accesso condizionale per le applicazioni locali e ospitate nel cloud.</span><span class="sxs-lookup"><span data-stu-id="8e523-106">The authenticated device, and the attributes of the device, can then be used to enforce conditional access policies for applications that are hosted in the cloud and on-premises.</span></span>

<span data-ttu-id="8e523-107">Insieme a una soluzione di gestione dei dispositivi mobili (MDM) come Microsoft Intune, gli attributi del dispositivo in Azure Active Directory vengono aggiornati con informazioni aggiuntive sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e523-107">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure Active Directory are updated with additional information about the device.</span></span> <span data-ttu-id="8e523-108">Ciò permette di creare regole di accesso condizionale che subordinano l'accesso dai dispositivi al rispetto dei propri standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="8e523-108">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="8e523-109">Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere l'articolo "Registrare i dispositivi per la gestione in Intune".</span><span class="sxs-lookup"><span data-stu-id="8e523-109">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune.</span></span>
<span data-ttu-id="8e523-110">Gli scenari consentiti da Registrazione dispositivo Azure Active Directory includono il supporto per dispositivi iOS, Android e Windows.</span><span class="sxs-lookup"><span data-stu-id="8e523-110">Scenarios enabled by Azure Active Directory Device Registration Azure Active Directory Device Registration includes support for iOS, Android, and Windows devices.</span></span> <span data-ttu-id="8e523-111">È possibile che i singoli scenari in cui viene usato il servizio Registrazione dispositivo di Azure AD prevedano requisiti più specifici e il supporto di determinate piattaforme.</span><span class="sxs-lookup"><span data-stu-id="8e523-111">The individual scenarios that utilize Azure AD Device Registration may have more specific requirements and platform support.</span></span> 

<span data-ttu-id="8e523-112">Questi scenari sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="8e523-112">These scenarios are as follows:</span></span>

- <span data-ttu-id="8e523-113">**Accesso condizionale per applicazioni di Office 365 con Microsoft Intune:** gli amministratori IT possono effettuare il provisioning dei criteri di accesso condizionale dei dispositivi per proteggere le risorse aziendali, consentendo allo stesso tempo agli Information Worker che usano dispositivi compatibili di accedere ai servizi.</span><span class="sxs-lookup"><span data-stu-id="8e523-113">**Conditional access for Office 365 applications with Microsoft Intune:** IT admins can provision conditional access device policies to secure corporate resources, while at the same time allowing information workers on compliant devices to access the services.</span></span> <span data-ttu-id="8e523-114">Per altre informazioni, vedere Criteri di accesso condizionale dei dispositivi per i servizi di Office 365.</span><span class="sxs-lookup"><span data-stu-id="8e523-114">For more information, see Conditional Access Device Policies for Office 365 services.</span></span>

- <span data-ttu-id="8e523-115">**Accesso condizionale alle applicazioni ospitate in locale:** è possibile usare i dispositivi registrati con criteri di accesso per le applicazioni configurate per l'uso di AD FS con Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="8e523-115">**Conditional access to applications that are hosted on-premises:** You can use registered devices with access policies for applications that are configured to use AD FS with Windows Server 2012 R2.</span></span> <span data-ttu-id="8e523-116">Per altre informazioni su come configurare l'accesso condizionale in locale, vedere [Configurazione dell'accesso condizionale locale usando il servizio Registrazione dispositivo di Azure Active Directory](active-directory-device-registration-on-premises-setup.md).</span><span class="sxs-lookup"><span data-stu-id="8e523-116">For more information about setting up conditional access for on-premises, see [Setting up On-premises Conditional Access using Azure Active Directory device registration](active-directory-device-registration-on-premises-setup.md).</span></span>

## <a name="setting-up-azure-active-directory-device-registration"></a><span data-ttu-id="8e523-117">Configurazione della Registrazione dispositivo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e523-117">Setting up Azure Active Directory Device Registration</span></span>

<span data-ttu-id="8e523-118">Per configurare il servizio Registrazione dispositivo, è possibile procedere in diversi modi:</span><span class="sxs-lookup"><span data-stu-id="8e523-118">To setup device registration, you have multiple options:</span></span>

- <span data-ttu-id="8e523-119">Registrazione dei dispositivi quando vengono aggiunti a un dominio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e523-119">Devices can register when joined to Azure AD domain.</span></span> <span data-ttu-id="8e523-120">Per altre informazioni, è possibile approfondire gli argomenti relativi all'aggiunta ad Azure AD e alle impostazioni necessarie per l'aggiunta di utenti a un dominio di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e523-120">For more on this topic, you can Learn more about Azure AD Join and the settings required for users to join Azure AD domain.</span></span>

- <span data-ttu-id="8e523-121">Registrazione dei dispositivi quando gli utenti aggiungono account aziendali o dell'istituto di istruzione a Windows in un dispositivo personale o quando i dispositivi mobili si connettono a risorse di lavoro che richiedono la registrazione.</span><span class="sxs-lookup"><span data-stu-id="8e523-121">Devices can be registered when users add work or school accounts to Windows on a personal device or when mobile devices connect to a work resources requiring registration.</span></span> <span data-ttu-id="8e523-122">A tale scopo, è necessario abilitare Registrazione dispositivo Azure AD nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="8e523-122">To ensure this, you must enable Azure AD Device Registration in the Azure Portal.</span></span> 

- <span data-ttu-id="8e523-123">Registrazione automatica dei dispositivi per i computer aggiunti a un dominio tradizionale.</span><span class="sxs-lookup"><span data-stu-id="8e523-123">Devices can be registered using automatic device registration for traditional domain-joined machines.</span></span> <span data-ttu-id="8e523-124">È necessario configurare Azure AD Connect prima di proseguire con la registrazione automatica dei dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8e523-124">To ensure this, you must first Setup Azure AD Connect before you continue with automatic device registration.</span></span>

<span data-ttu-id="8e523-125">Per le istruzioni più aggiornate, vedere [Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="8e523-125">For latest instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>  
<span data-ttu-id="8e523-126">È anche possibile visualizzare e abilitare/disabilitare i dispositivi registrati usando il portale amministratore in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e523-126">You can also review and enable or disable registered devices using the Administrator Portal in Azure Active Directory.</span></span>

## <a name="enable-the-azure-active-directory-device-registration-service"></a><span data-ttu-id="8e523-127">Abilitare il servizio Registrazione dispositivo Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e523-127">Enable the Azure Active Directory device registration service</span></span>

<span data-ttu-id="8e523-128">**Per abilitare il servizio Registrazione dispositivo Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="8e523-128">**To enable the Azure Active Directory device registration service:**</span></span>

1.  <span data-ttu-id="8e523-129">Accedere al portale di Microsoft Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8e523-129">Sign in to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="8e523-130">Nel riquadro sinistro selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e523-130">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="8e523-131">Selezionare la propria directory nella scheda Directory.</span><span class="sxs-lookup"><span data-stu-id="8e523-131">On the Directory tab, select your directory.</span></span>

4.  <span data-ttu-id="8e523-132">Fare clic su **Configure**.</span><span class="sxs-lookup"><span data-stu-id="8e523-132">Click **Configure**.</span></span>

5.  <span data-ttu-id="8e523-133">Scorrere fino a **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8e523-133">Scroll to **Devices**.</span></span>

6.  <span data-ttu-id="8e523-134">Selezionare Tutti per Gli utenti possono registrare i propri dispositivi in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8e523-134">Select ALL for USERS MAY REGISTER THEIR DEVICES WITH AZURE AD.</span></span>

7.  <span data-ttu-id="8e523-135">Selezionare il numero massimo di dispositivi da autorizzare per l'utente.</span><span class="sxs-lookup"><span data-stu-id="8e523-135">Select the maximum number of devices you want to authorize per user.</span></span>

<span data-ttu-id="8e523-136">L'iscrizione a Microsoft Intune o Gestione dei dispositivi mobili per Office 365 richiede la registrazione del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e523-136">The enrollment with Microsoft Intune or Mobile Device Management for Office 365 requires device registration.</span></span> <span data-ttu-id="8e523-137">Se è stato configurato uno di questi servizi, sarà selezionata l'opzione **Tutti** e disabilitata l'opzione **Nessuno**.</span><span class="sxs-lookup"><span data-stu-id="8e523-137">If you have configured either of these services, **ALL** is selected and **NONE** is disabled.</span></span> <span data-ttu-id="8e523-138">Assicurarsi che siano configurati correttamente e di avere le licenze appropriate.</span><span class="sxs-lookup"><span data-stu-id="8e523-138">Please ensure that they are configured correctly and have the appropriate licensing.</span></span>

<span data-ttu-id="8e523-139">Per impostazione predefinita, l'autenticazione a due fattori non è abilitata per il servizio.</span><span class="sxs-lookup"><span data-stu-id="8e523-139">By default, two-factor authentication is not enabled for the service.</span></span> <span data-ttu-id="8e523-140">L'autenticazione a due fattori è tuttavia consigliabile quando si registra un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="8e523-140">However, two-factor authentication is recommended when registering a device.</span></span>

- <span data-ttu-id="8e523-141">Prima di richiedere l'autenticazione a due fattori per questo servizio, è necessario configurare un provider di autenticazione a due fattori in Azure Active Directory e configurare gli account utente per Multi-Factor Authentication. Vedere Aggiunta di Multi-Factor Authentication ad Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8e523-141">Before requiring two-factor authentication for this service, you must configure a two-factor authentication provider in Azure Active Directory and configure your user accounts for Multi-Factor Authentication, see Adding Multi-Factor Authentication to Azure Active Directory</span></span>

- <span data-ttu-id="8e523-142">Se si usa AD FS con Windows Server 2012 R2, è necessario configurare un modulo di autenticazione a due fattori in AD FS. Vedere l'articolo relativo all'uso di Multi-Factor Authentication con Active Directory Federation Services.</span><span class="sxs-lookup"><span data-stu-id="8e523-142">If you are using AD FS with Windows Server 2012 R2, you must configure a two-factor authentication module in AD FS, see Using Multi-Factor Authentication with Active Directory Federation Services.</span></span>

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a><span data-ttu-id="8e523-143">Visualizzare e gestire gli oggetti dispositivo di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8e523-143">View and manage device objects in Azure Active Directory</span></span>

<span data-ttu-id="8e523-144">Nel portale dell'amministratore di Azure è possibile visualizzare, bloccare e sbloccare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8e523-144">From the Azure Administrator portal, you can view, block, and unblock devices.</span></span> <span data-ttu-id="8e523-145">Un dispositivo bloccato non avrà più accesso alle applicazioni configurate per consentire solo i dispositivi registrati.</span><span class="sxs-lookup"><span data-stu-id="8e523-145">A device that is blocked will no longer have access to applications that are configured to allow only registered devices.</span></span>

<span data-ttu-id="8e523-146">**Per visualizzare e gestire oggetti dispositivo in Azure Active Directory:**</span><span class="sxs-lookup"><span data-stu-id="8e523-146">**To view and manage device objects in Azure Active Directory:**</span></span>
 
1.  <span data-ttu-id="8e523-147">Accedere al portale di Microsoft Azure come amministratore.</span><span class="sxs-lookup"><span data-stu-id="8e523-147">Log on to the Microsoft Azure portal as administrator.</span></span>

2.  <span data-ttu-id="8e523-148">Nel riquadro sinistro selezionare **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="8e523-148">On the left pane, select **Active Directory**.</span></span>

3.  <span data-ttu-id="8e523-149">Selezionare la propria directory.</span><span class="sxs-lookup"><span data-stu-id="8e523-149">Select your directory.</span></span>

4.  <span data-ttu-id="8e523-150">Selezionare **Utenti**.</span><span class="sxs-lookup"><span data-stu-id="8e523-150">Select **Users**.</span></span> 

5.  <span data-ttu-id="8e523-151">Fare clic sull'utente per il quale si vogliono visualizzare i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="8e523-151">Click the user for which you want to see the devices.</span></span>

6.  <span data-ttu-id="8e523-152">Selezionare **Dispositivi**.</span><span class="sxs-lookup"><span data-stu-id="8e523-152">Select **Devices**.</span></span>

7.  <span data-ttu-id="8e523-153">Selezionare **Dispositivi registrati**.</span><span class="sxs-lookup"><span data-stu-id="8e523-153">Select **Registered Devices**.</span></span>

<span data-ttu-id="8e523-154">A questo punto è possibile esaminare, bloccare o sbloccare i dispositivi registrati dell'utente.</span><span class="sxs-lookup"><span data-stu-id="8e523-154">Now, you can review, block, or unblock the user's registered devices.</span></span>
<span data-ttu-id="8e523-155">I dispositivi Windows 10 aggiunti a un dominio locale e registrati automaticamente non vengono visualizzati nella scheda Utenti.</span><span class="sxs-lookup"><span data-stu-id="8e523-155">Windows 10 devices that are on-premises domain-joined and automatically registered do not appear under the Users tab.</span></span> <span data-ttu-id="8e523-156">Usare il comando di PowerShell Get-MsolDevice per trovare tutti i dispositivi dell'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="8e523-156">Please use the Get-MsolDevice PowerShell command to find all your enterprise devices.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="8e523-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8e523-157">Next steps</span></span>

<span data-ttu-id="8e523-158">Per altre informazioni, vedere [Come configurare la registrazione automatica dei dispositivi Windows con Azure Active Directory aggiunti a un dominio](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="8e523-158">To setup automated device registration, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span></span>


