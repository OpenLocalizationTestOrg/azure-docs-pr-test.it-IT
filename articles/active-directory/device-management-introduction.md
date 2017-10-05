---
title: Introduzione alla gestione dei dispositivi in Azure Active Directory | Microsoft Docs
description: Informazioni su come la gestione dei dispositivi consente di ottenere il controllo sui dispositivi che accedono alle risorse nell'ambiente.
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
ms.openlocfilehash: bebbdddf6b591ea7e36cbac38b568bce614bb335
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-device-management-in-azure-active-directory"></a><span data-ttu-id="7054b-103">Introduzione alla gestione dei dispositivi in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7054b-103">Introduction to device management in Azure Active Directory</span></span>

<span data-ttu-id="7054b-104">In un mondo in cui i dispositivi mobili e il cloud hanno sempre più importanza, Azure Active Directory (Azure AD) consente ovunque l'accesso Single Sign-On a dispositivi, app e servizi.</span><span class="sxs-lookup"><span data-stu-id="7054b-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on to devices, apps, and services from anywhere.</span></span> <span data-ttu-id="7054b-105">Con il proliferare dei dispositivi, inclusi i dispositivi Bring Your Own Device (BYOD), i professionisti IT hanno due obiettivi opposti:</span><span class="sxs-lookup"><span data-stu-id="7054b-105">With the proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="7054b-106">Fare in modo che gli utenti finali siano produttivi sempre e ovunque</span><span class="sxs-lookup"><span data-stu-id="7054b-106">Empower the end users to be productive wherever and whenever</span></span>
- <span data-ttu-id="7054b-107">Proteggere gli asset aziendali in qualsiasi momento</span><span class="sxs-lookup"><span data-stu-id="7054b-107">Protect the corporate assets at any time</span></span>

<span data-ttu-id="7054b-108">Tramite i dispositivi gli utenti hanno accesso alle risorse aziendali.</span><span class="sxs-lookup"><span data-stu-id="7054b-108">Through devices, your users are getting access to your corporate assets.</span></span> <span data-ttu-id="7054b-109">Per proteggere le risorse aziendali, gli amministratori IT vogliono avere il controllo su questi dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7054b-109">To protect your corporate assets, as an IT administrator, you want to have control over these devices.</span></span> <span data-ttu-id="7054b-110">Ciò consente di verificare che gli utenti accedano alle risorse da dispositivi che soddisfano gli standard per sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="7054b-110">This enables you to make sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="7054b-111">La gestione dei dispositivi rappresenta anche il fondamento per l'[accesso condizionale basato su dispositivo](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7054b-111">Device management is also the foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="7054b-112">Con l'accesso condizionale basato su dispositivo, è possibile assicurarsi che l'accesso alle risorse nell'ambiente sia possibile solo con dispositivi attendibili.</span><span class="sxs-lookup"><span data-stu-id="7054b-112">With device-based conditional access, you can ensure that access to resources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="7054b-113">Questo argomento illustra il funzionamento della gestione dei dispositivi in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7054b-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-the-control-of-azure-ad"></a><span data-ttu-id="7054b-114">Controllo dei dispositivi tramite Azure AD</span><span class="sxs-lookup"><span data-stu-id="7054b-114">Getting devices under the control of Azure AD</span></span>

<span data-ttu-id="7054b-115">Per controllare un dispositivo tramite Azure AD, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="7054b-115">To get a device under the control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="7054b-116">Registrazione</span><span class="sxs-lookup"><span data-stu-id="7054b-116">Registering</span></span> 
- <span data-ttu-id="7054b-117">Aggiunta</span><span class="sxs-lookup"><span data-stu-id="7054b-117">Joining</span></span>

<span data-ttu-id="7054b-118">La **registrazione** di un dispositivo in Azure AD consente di gestire l'identità di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7054b-118">**Registering** a device to Azure AD enables you to manage a device’s identity.</span></span> <span data-ttu-id="7054b-119">Quando un dispositivo viene registrato, Registrazione dispositivo Azure AD fornisce al dispositivo un'identità che viene usata per autenticare il dispositivo quando un utente accede ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7054b-119">When a device is registered, Azure AD device registration provides the device with an identity that is used to authenticate the device when a user signs-in to Azure AD.</span></span> <span data-ttu-id="7054b-120">È possibile usare l'identità per abilitare o disabilitare un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7054b-120">You can use the identity to enable or disable a device.</span></span>

<span data-ttu-id="7054b-121">Con una soluzione di gestione di dispositivi mobili (MDM), ad esempio Microsoft Intune, gli attributi del dispositivo in Azure AD vengono aggiornati con informazioni aggiuntive sul dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7054b-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, the device attributes in Azure AD are updated with additional information about the device.</span></span> <span data-ttu-id="7054b-122">Ciò permette di creare regole di accesso condizionale che subordinano l'accesso dai dispositivi al rispetto dei propri standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="7054b-122">This allows you to create conditional access rules that enforce access from devices to meet your standards for security and compliance.</span></span> <span data-ttu-id="7054b-123">Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere Registrare i dispositivi per la gestione in Intune.</span><span class="sxs-lookup"><span data-stu-id="7054b-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="7054b-124">L'**aggiunta** di un dispositivo è un'estensione della registrazione di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7054b-124">**Joining** a device is an extension to registering a device.</span></span> <span data-ttu-id="7054b-125">Offre infatti tutti i vantaggi della registrazione di un dispositivo, oltre a modificarne lo stato locale.</span><span class="sxs-lookup"><span data-stu-id="7054b-125">This means, it provides you with all the benefits of registering a device and in addition to this, it also changes the local state of a device.</span></span> <span data-ttu-id="7054b-126">Modificando lo stato locale, gli utenti possono accedere a un dispositivo usando un account aziendale o dell'istituto di istruzione invece di un account personale.</span><span class="sxs-lookup"><span data-stu-id="7054b-126">Changing the local state enables your users to sign-in to a device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="7054b-127">Dispositivi registrati in Azure AD</span><span class="sxs-lookup"><span data-stu-id="7054b-127">Azure AD registered devices</span></span>   

<span data-ttu-id="7054b-128">L'obiettivo dei dispositivi registrati in Azure AD è di fornire supporto per lo scenario **Bring Your Own Device (BYOD)**.</span><span class="sxs-lookup"><span data-stu-id="7054b-128">The goal of Azure AD registered devices is to provide you with support for the **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="7054b-129">In questo scenario un utente può accedere alle risorse dell'organizzazione controllate da Azure Active Directory usando un dispositivo personale.</span><span class="sxs-lookup"><span data-stu-id="7054b-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Dispositivi registrati in Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="7054b-131">L'accesso si basa su un account aziendale o dell'istituto di istruzione immesso nel dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7054b-131">The access is based on a work or school account that has been entered on the device.</span></span>  
<span data-ttu-id="7054b-132">Windows 10, ad esempio, consente agli utenti di aggiungere un account aziendale o dell'istituto di istruzione a un computer, un tablet o un telefono personale.</span><span class="sxs-lookup"><span data-stu-id="7054b-132">For example, Windows 10 enables users to add a work or school account to a personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="7054b-133">Dopo l'aggiunta dell'account aziendale o dell'istituto di istruzione il dispositivo viene registrato in Azure AD e, facoltativamente, anche nel sistema di gestione di dispositivi mobili (MDM) configurato dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7054b-133">When a user has added a work or school account, the device is registered with Azure AD and optionally enrolled in the mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="7054b-134">Gli utenti dell'organizzazione possono aggiungere un account aziendale o dell'istituto di istruzione a un dispositivo personale in modo pratico:</span><span class="sxs-lookup"><span data-stu-id="7054b-134">Your organization’s users can add a work or school account to a personal device conveniently:</span></span>

- <span data-ttu-id="7054b-135">Durante il primo accesso a un'applicazione di lavoro</span><span class="sxs-lookup"><span data-stu-id="7054b-135">When accessing a work application for the first time</span></span>
- <span data-ttu-id="7054b-136">Manualmente tramite il menu **Impostazioni** nel caso di Windows 10</span><span class="sxs-lookup"><span data-stu-id="7054b-136">Manually via the **Settings** menu in the case of Windows 10</span></span> 

<span data-ttu-id="7054b-137">È possibile configurare dispositivi registrati in Azure AD per Windows 10, iOS, Android e macOS.</span><span class="sxs-lookup"><span data-stu-id="7054b-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="7054b-138">Dispositivi aggiunti ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="7054b-138">Azure AD joined devices</span></span>

<span data-ttu-id="7054b-139">L'obiettivo dei dispositivi aggiunti ad Azure AD è di semplificare:</span><span class="sxs-lookup"><span data-stu-id="7054b-139">The goal of Azure AD joined devices is to simplify:</span></span>

- <span data-ttu-id="7054b-140">Distribuzioni Windows di dispositivi di proprietà dell'azienda</span><span class="sxs-lookup"><span data-stu-id="7054b-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="7054b-141">Accesso ad app e risorse aziendali da qualsiasi dispositivo Windows</span><span class="sxs-lookup"><span data-stu-id="7054b-141">Access to organizational apps and resources from any Windows device</span></span>

![Dispositivi registrati in Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="7054b-143">Per raggiungere questi obiettivi, è possibile fornire agli utenti un'esperienza self-service per porre i dispositivi di proprietà dell'azienda sotto il controllo di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7054b-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under the control of Azure AD.</span></span>  
<span data-ttu-id="7054b-144">L'**aggiunta ad Azure AD** è destinata alle organizzazioni basate prima di tutto o esclusivamente sul cloud.</span><span class="sxs-lookup"><span data-stu-id="7054b-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="7054b-145">Si tratta in genere piccole e medie imprese che non hanno un'infrastruttura Active Directory di Windows Server locale.</span><span class="sxs-lookup"><span data-stu-id="7054b-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="7054b-146">L'implementazione di dispositivi aggiunti ad Azure AD offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="7054b-146">Implementing Azure AD joined devices provides you with the following benefits:</span></span>

- <span data-ttu-id="7054b-147">**Single Sign-On (SSO)** alle app e ai servizi SaaS gestiti da Azure.</span><span class="sxs-lookup"><span data-stu-id="7054b-147">**Single-Sign-On (SSO)** to your Azure managed SaaS apps and services.</span></span> <span data-ttu-id="7054b-148">Gli utenti non visualizzano richieste di autenticazione aggiuntive quando accedono alle risorse.</span><span class="sxs-lookup"><span data-stu-id="7054b-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="7054b-149">La funzionalità SSO è attiva anche quando non sono connessi alla rete di dominio disponibile.</span><span class="sxs-lookup"><span data-stu-id="7054b-149">The SSO functionality is even when they are not connected to the domain network available.</span></span>

- <span data-ttu-id="7054b-150">**Roaming conforme ai criteri dell'organizzazione** per le impostazioni utente tra dispositivi aggiunti.</span><span class="sxs-lookup"><span data-stu-id="7054b-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="7054b-151">Non è necessario che gli utenti connettano un account Microsoft (ad esempio, Hotmail) per visualizzare le impostazioni tra dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7054b-151">Users don’t need to connect a Microsoft account (for example, Hotmail) to see settings across devices.</span></span>

- <span data-ttu-id="7054b-152">**Accesso a Windows Store per le aziende** tramite l'account AD.</span><span class="sxs-lookup"><span data-stu-id="7054b-152">**Access to Windows Store for Business** using AD account.</span></span> <span data-ttu-id="7054b-153">Gli utenti possono scegliere da un inventario di applicazioni preselezionate dall'organizzazione.</span><span class="sxs-lookup"><span data-stu-id="7054b-153">Your users can choose from an inventory of applications pre-selected by the organization.</span></span>

- <span data-ttu-id="7054b-154">Supporto di **Windows Hello** per un accesso sicuro e agevole alle risorse aziendali.</span><span class="sxs-lookup"><span data-stu-id="7054b-154">**Windows Hello** support for secure and convenient access to work resources.</span></span>

- <span data-ttu-id="7054b-155">**Limitazione dell'accesso** alle app solo dai dispositivi che soddisfano i criteri di conformità.</span><span class="sxs-lookup"><span data-stu-id="7054b-155">**Restriction of access** to apps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="7054b-156">Anche se l'aggiunta ad Azure AD è destinata soprattutto alle organizzazioni prive di un'infrastruttura Active Directory di Windows Server locale, è ovviamente possibile usarla anche in scenari in cui:</span><span class="sxs-lookup"><span data-stu-id="7054b-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="7054b-157">Non è possibile usare un'aggiunta a un dominio locale, ad esempio se è necessario avere il controllo di dispositivi mobili come tablet e telefoni.</span><span class="sxs-lookup"><span data-stu-id="7054b-157">You can’t use an on-premises domain join, for example, if you need to get mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="7054b-158">Gli utenti hanno soprattutto necessità di accedere a Office 365 o ad altre app SaaS integrate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7054b-158">Your users primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="7054b-159">Si vuole gestire un gruppo di utenti in Azure AD invece che in Active Directory,</span><span class="sxs-lookup"><span data-stu-id="7054b-159">You want to manage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="7054b-160">ad esempio lavoratori stagionali, terzisti o studenti.</span><span class="sxs-lookup"><span data-stu-id="7054b-160">This can apply, for example, to seasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="7054b-161">Si vogliono fornire funzionalità di join ai lavoratori in succursali remote con un'infrastruttura locale limitata.</span><span class="sxs-lookup"><span data-stu-id="7054b-161">You want to provide joining capabilities to workers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="7054b-162">È possibile configurare dispositivi aggiunti ad Azure AD per dispositivi Windows 10.</span><span class="sxs-lookup"><span data-stu-id="7054b-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="7054b-163">Dispositivi aggiunti all'identità ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7054b-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="7054b-164">Per oltre un decennio, molte organizzazioni hanno usato l'aggiunta a un dominio ad Active Directory locale per consentire:</span><span class="sxs-lookup"><span data-stu-id="7054b-164">For more than a decade, many organizations have used the domain join to their on-premises Active Directory to enable:</span></span>

- <span data-ttu-id="7054b-165">Ai reparti IT di gestire i dispositivi di proprietà dell'azienda da una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="7054b-165">IT departments to manage work-owned devices from a central location.</span></span>

- <span data-ttu-id="7054b-166">Agli utenti di accedere ai dispositivi con il proprio account aziendale o dell'istituto di istruzione di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7054b-166">Users to sign in to their devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="7054b-167">In genere le aziende con un footprint locale si basano su metodi di creazione dell'immagine per effettuare il provisioning dei dispositivi e, per gestirli, usano **System Center Configuration Manager (SCCM)** o **Criteri di gruppo**.</span><span class="sxs-lookup"><span data-stu-id="7054b-167">Typically, organizations with an on-premises footprint rely on imaging methods to provision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** to manage them.</span></span>

<span data-ttu-id="7054b-168">Se l'ambiente ha un footprint AD locale e si vogliono anche sfruttare le funzionalità offerte da Azure Active Directory, è possibile implementare dispositivi aggiunti all'identità ibrida di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7054b-168">If your environment has an on-premises AD footprint and you also want benefit from the capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="7054b-169">Questi dispositivi vengono aggiunti sia ad Active Directory locale che ad Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7054b-169">These are devices that are both, joined to your on-premises Active Directory and your Azure Active Directory.</span></span>

![Dispositivi registrati in Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="7054b-171">È consigliabile usare dispositivi aggiunti all'identità ibrida di Azure AD se:</span><span class="sxs-lookup"><span data-stu-id="7054b-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="7054b-172">Sono state distribuite app Win32 in questi dispositivi che usano NTLM/Kerberos.</span><span class="sxs-lookup"><span data-stu-id="7054b-172">You have Win32 apps deployed to these devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="7054b-173">Sono necessari Criteri di gruppo o SCCM/DCM per gestire i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="7054b-173">You require GP or SCCM / DCM to manage devices.</span></span>

- <span data-ttu-id="7054b-174">Si vuole continuare a usare soluzioni di creazione dell'immagine per configurare i dispositivi per i dipendenti.</span><span class="sxs-lookup"><span data-stu-id="7054b-174">You want to continue to use imaging solutions to configure devices for your employees.</span></span>

<span data-ttu-id="7054b-175">È possibile configurare dispositivi aggiunti all'identità ibrida di Azure AD per Windows 10 e dispositivi di livello inferiore, ad esempio Windows 8 e Windows 7.</span><span class="sxs-lookup"><span data-stu-id="7054b-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="7054b-176">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7054b-176">Summary</span></span>

<span data-ttu-id="7054b-177">Con la gestione dei dispositivi in Azure AD, è possibile:</span><span class="sxs-lookup"><span data-stu-id="7054b-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="7054b-178">Semplificare il processo per mettere i dispositivi sotto il controllo di Azure AD</span><span class="sxs-lookup"><span data-stu-id="7054b-178">Simplify the process of bringing devices under the control of Azure AD</span></span>

- <span data-ttu-id="7054b-179">Fornire agli utenti un accesso facile da usare alle risorse basate sul cloud dell'organizzazione</span><span class="sxs-lookup"><span data-stu-id="7054b-179">Provide your users with an easy to use access to your organization’s cloud-based resources</span></span>

<span data-ttu-id="7054b-180">Come regola generale, è consigliabile usare:</span><span class="sxs-lookup"><span data-stu-id="7054b-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="7054b-181">Dispositivi registrati in Azure AD per i dispositivi personali</span><span class="sxs-lookup"><span data-stu-id="7054b-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="7054b-182">Dispositivi aggiunti ad Azure AD per i dispositivi non aggiunti ad AD locale</span><span class="sxs-lookup"><span data-stu-id="7054b-182">Azure AD joined devices for devices that are not joined to an on-premises AD</span></span> 

- <span data-ttu-id="7054b-183">Dispositivi aggiunti all'identità ibrida di Azure AD per i dispositivi aggiunti ad AD locale</span><span class="sxs-lookup"><span data-stu-id="7054b-183">Hybrid Azure AD joined devices for devices that are joined to an on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="7054b-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7054b-184">Next steps</span></span>

- <span data-ttu-id="7054b-185">Per una panoramica sulla gestione del dispositivo nel portale di Azure AD, vedere [Gestione dei dispositivi tramite il portale di Azure](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="7054b-185">To get an overview of how to manage device in the Azure portal, see [managing devices using the Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="7054b-186">Per altre informazioni sull'accesso condizionale basato su dispositivo, vedere l'articolo su come [configurare criteri di accesso condizionale basati sul dispositivo in Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="7054b-186">To learn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="7054b-187">Per configurare dispositivi aggiunti all'identità ibrida di Azure AD, vedere [Come configurare dispositivi aggiunti all'identità ibrida di Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="7054b-187">To setup hybrid Azure AD joined devices, see [how to configure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


