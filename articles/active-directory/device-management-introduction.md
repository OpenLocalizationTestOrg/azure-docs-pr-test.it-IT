---
title: gestione toodevice aaaIntroduction in Azure Active Directory | Documenti Microsoft
description: Informazioni su come la gestione dei dispositivi consente un controllo tooget dei dispositivi hello che accedono alle risorse nell'ambiente in uso.
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
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="fd988-103">Gestione toodevice introduzione in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd988-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="fd988-104">In un ambiente mobile-first, prima di cloud, Azure Active Directory (Azure AD) consente di single sign-on toodevices, applicazioni e servizi da qualsiasi posizione.</span><span class="sxs-lookup"><span data-stu-id="fd988-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="fd988-105">Con la proliferazione di hello di dispositivi, tra cui BYOD Bring Your Own Device (), i professionisti IT devono affrontare due obiettivi opposti:</span><span class="sxs-lookup"><span data-stu-id="fd988-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="fd988-106">Consentire toobe gli utenti finali di hello produttivi ovunque e</span><span class="sxs-lookup"><span data-stu-id="fd988-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="fd988-107">Proteggere le risorse aziendali hello in qualsiasi momento</span><span class="sxs-lookup"><span data-stu-id="fd988-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="fd988-108">Tramite i dispositivi, gli utenti ottengono accesso risorse aziendali tooyour.</span><span class="sxs-lookup"><span data-stu-id="fd988-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="fd988-109">tooprotect risorse aziendali, come un amministratore IT, si desidera controllare toohave questi dispositivi.</span><span class="sxs-lookup"><span data-stu-id="fd988-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="fd988-110">In questo modo toomake assicurarsi che gli utenti accede alle risorse dai dispositivi che soddisfano gli standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="fd988-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="fd988-111">Gestione dei dispositivi è inoltre foundation hello per [accesso condizionale basato su dispositivo](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="fd988-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="fd988-112">Con accesso condizionale basato su dispositivi, è possibile garantire che tooresources nell'ambiente in uso è possibile solo con accesso dispositivo attendibile.</span><span class="sxs-lookup"><span data-stu-id="fd988-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="fd988-113">Questo argomento illustra il funzionamento della gestione dei dispositivi in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd988-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="fd988-114">Dispositivi sotto controllo hello di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd988-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="fd988-115">tooget un dispositivo sotto controllo hello di Azure AD, sono disponibili due opzioni:</span><span class="sxs-lookup"><span data-stu-id="fd988-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="fd988-116">Registrazione</span><span class="sxs-lookup"><span data-stu-id="fd988-116">Registering</span></span> 
- <span data-ttu-id="fd988-117">Aggiunta</span><span class="sxs-lookup"><span data-stu-id="fd988-117">Joining</span></span>

<span data-ttu-id="fd988-118">**Registrazione** tooAzure un dispositivo AD consente si toomanage identità di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fd988-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="fd988-119">Quando un dispositivo viene registrato, registrazione dispositivo di Azure AD fornisce dispositivo hello con un'identità che è un dispositivo di hello tooauthenticate utilizzato quando un utente accede tooAzure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd988-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="fd988-120">È possibile utilizzare hello identità tooenable o disattivare un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fd988-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="fd988-121">Se combinato con una soluzione di management(MDM) di dispositivi mobili, ad esempio Microsoft Intune, sugli attributi del dispositivo hello in Azure AD vengono aggiornati con informazioni aggiuntive sul dispositivo di hello.</span><span class="sxs-lookup"><span data-stu-id="fd988-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="fd988-122">Ciò consente di regole di accesso condizionale toocreate che impongono l'accesso da dispositivi toomeet agli standard di sicurezza e conformità.</span><span class="sxs-lookup"><span data-stu-id="fd988-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="fd988-123">Per altre informazioni sulla registrazione dei dispositivi in Microsoft Intune, vedere Registrare i dispositivi per la gestione in Intune.</span><span class="sxs-lookup"><span data-stu-id="fd988-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="fd988-124">**Unione di** un dispositivo è un tooregistering estensione un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fd988-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="fd988-125">Ciò significa, esso consente di tutti i vantaggi di hello della registrazione di un dispositivo in toothis aggiunta, modifica inoltre lo stato locale di hello di un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="fd988-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="fd988-126">Modifica dello stato locale hello consente il dispositivo tooa toosign-in utenti utilizzando un organizzazione account aziendale o dell'istituto di istruzione anziché un account personale.</span><span class="sxs-lookup"><span data-stu-id="fd988-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="fd988-127">Dispositivi registrati in Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd988-127">Azure AD registered devices</span></span>   

<span data-ttu-id="fd988-128">obiettivo di dispositivi AD Azure registrata Hello è tooprovide è con il supporto per hello **BYOD Bring Your Own Device ()** scenario.</span><span class="sxs-lookup"><span data-stu-id="fd988-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="fd988-129">In questo scenario un utente può accedere alle risorse dell'organizzazione controllate da Azure Active Directory usando un dispositivo personale.</span><span class="sxs-lookup"><span data-stu-id="fd988-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Dispositivi registrati in Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="fd988-131">accesso Hello è basata su un account aziendale o dell'istituto di istruzione che è stata immessa nel dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="fd988-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="fd988-132">Ad esempio, Windows 10 consente tooadd agli utenti un lavoro o scuola account tooa per PC, tablet o telefono.</span><span class="sxs-lookup"><span data-stu-id="fd988-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="fd988-133">Quando un utente ha aggiunto un account aziendale o dell'istituto di istruzione, il dispositivo hello è registrato con Azure AD e facoltativamente registrato nel sistema di gestione (MDM) di dispositivi mobili hello che l'organizzazione ha configurato.</span><span class="sxs-lookup"><span data-stu-id="fd988-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="fd988-134">Aggiungere un lavoro agli utenti dell'organizzazione o dell'istituto di istruzione convenientemente dispositivo personale tooa di account:</span><span class="sxs-lookup"><span data-stu-id="fd988-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="fd988-135">Quando si accede a un'applicazione di lavoro per hello prima volta</span><span class="sxs-lookup"><span data-stu-id="fd988-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="fd988-136">Manualmente tramite hello **impostazioni** menu nel caso di hello di Windows 10</span><span class="sxs-lookup"><span data-stu-id="fd988-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="fd988-137">È possibile configurare dispositivi registrati in Azure AD per Windows 10, iOS, Android e macOS.</span><span class="sxs-lookup"><span data-stu-id="fd988-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="fd988-138">Dispositivi aggiunti ad Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd988-138">Azure AD joined devices</span></span>

<span data-ttu-id="fd988-139">obiettivo di Hello dei dispositivi di Azure AD aggiunti è toosimplify:</span><span class="sxs-lookup"><span data-stu-id="fd988-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="fd988-140">Distribuzioni Windows di dispositivi di proprietà dell'azienda</span><span class="sxs-lookup"><span data-stu-id="fd988-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="fd988-141">Accesso alle App tooorganizational e risorse da qualsiasi dispositivo Windows</span><span class="sxs-lookup"><span data-stu-id="fd988-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Dispositivi registrati in Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="fd988-143">Questi obiettivi, vengono eseguiti da fornire agli utenti un'esperienza self-service per ottenere i dispositivi di proprietà lavoro sotto controllo hello di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd988-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="fd988-144">L'**aggiunta ad Azure AD** è destinata alle organizzazioni basate prima di tutto o esclusivamente sul cloud.</span><span class="sxs-lookup"><span data-stu-id="fd988-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="fd988-145">Si tratta in genere piccole e medie imprese che non hanno un'infrastruttura Active Directory di Windows Server locale.</span><span class="sxs-lookup"><span data-stu-id="fd988-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="fd988-146">Implementazione di dispositivi AD Azure unita in join vengono hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="fd988-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="fd988-147">**Single Sign-On (SSO)** tooyour Azure gestito App SaaS e servizi.</span><span class="sxs-lookup"><span data-stu-id="fd988-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="fd988-148">Gli utenti non visualizzano richieste di autenticazione aggiuntive quando accedono alle risorse.</span><span class="sxs-lookup"><span data-stu-id="fd988-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="fd988-149">Hello funzionalità SSO è anche quando non sono connessi toohello rete di dominio disponibili.</span><span class="sxs-lookup"><span data-stu-id="fd988-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="fd988-150">**Roaming conforme ai criteri dell'organizzazione** per le impostazioni utente tra dispositivi aggiunti.</span><span class="sxs-lookup"><span data-stu-id="fd988-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="fd988-151">Gli utenti non devono tooconnect le impostazioni di toosee un Microsoft account (ad esempio Hotmail) tra i dispositivi.</span><span class="sxs-lookup"><span data-stu-id="fd988-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="fd988-152">**Accesso tooWindows Store per le aziende** utilizzando l'account di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd988-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="fd988-153">Gli utenti possono scegliere da un inventario delle applicazioni pre-selezionata dall'organizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="fd988-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="fd988-154">**Windows Hello** supporto per le risorse toowork accesso sicuro e pratico.</span><span class="sxs-lookup"><span data-stu-id="fd988-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="fd988-155">**Limitazione dell'accesso** tooapps da solo i dispositivi che soddisfano i criteri di conformità.</span><span class="sxs-lookup"><span data-stu-id="fd988-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="fd988-156">Anche se l'aggiunta ad Azure AD è destinata soprattutto alle organizzazioni prive di un'infrastruttura Active Directory di Windows Server locale, è ovviamente possibile usarla anche in scenari in cui:</span><span class="sxs-lookup"><span data-stu-id="fd988-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="fd988-157">È possibile utilizzare un'aggiunta al dominio locale, ad esempio, se è necessario tooget di dispositivi mobili come Tablet e telefoni nel controllo.</span><span class="sxs-lookup"><span data-stu-id="fd988-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="fd988-158">Gli utenti devono principalmente tooaccess Office 365 o altre applicazioni SaaS integrate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd988-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="fd988-159">Si desidera toomanage un gruppo di utenti in Azure Active Directory anziché in Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd988-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="fd988-160">Questo è applicabile, ad esempio, lavoratori tooseasonal, collaboratori o studenti.</span><span class="sxs-lookup"><span data-stu-id="fd988-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="fd988-161">Si desidera tooprovide tooworkers funzionalità di unione nelle succursali remote con l'infrastruttura locale limitato.</span><span class="sxs-lookup"><span data-stu-id="fd988-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="fd988-162">È possibile configurare dispositivi aggiunti ad Azure AD per dispositivi Windows 10.</span><span class="sxs-lookup"><span data-stu-id="fd988-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="fd988-163">Dispositivi aggiunti all'identità ibrida di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd988-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="fd988-164">Per più di dieci anni, molte organizzazioni hanno utilizzato hello dominio join tootheir locale Active Directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="fd988-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="fd988-165">IT reparti toomanage lavoro dispositivi di proprietà da una posizione centrale.</span><span class="sxs-lookup"><span data-stu-id="fd988-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="fd988-166">Gli utenti toosign nei dispositivi tootheir con Active Directory di lavoro o scuola account.</span><span class="sxs-lookup"><span data-stu-id="fd988-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="fd988-167">In genere, le organizzazioni con un footprint locale si basano su metodi tooprovision periferiche e utilizzano spesso **System Center Configuration Manager (SCCM)** o **(GP) di criteri di gruppo** toomanage essi.</span><span class="sxs-lookup"><span data-stu-id="fd988-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="fd988-168">Se l'ambiente comprende una locale footprint di Active Directory e si desiderano anche vantaggi offerti dalla funzionalità hello fornite da Azure Active Directory, è possibile implementare i dispositivi di Azure AD unita in join ibrido.</span><span class="sxs-lookup"><span data-stu-id="fd988-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="fd988-169">Si tratta di dispositivi che sono entrambi, unita in join tooyour Active Directory locale e Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd988-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Dispositivi registrati in Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="fd988-171">È consigliabile usare dispositivi aggiunti all'identità ibrida di Azure AD se:</span><span class="sxs-lookup"><span data-stu-id="fd988-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="fd988-172">Si dispone Win32 App distribuito toothese dispositivi che utilizzano l'autenticazione NTLM o Kerberos.</span><span class="sxs-lookup"><span data-stu-id="fd988-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="fd988-173">È necessario criteri di gruppo o SCCM / dispositivi toomanage DCM.</span><span class="sxs-lookup"><span data-stu-id="fd988-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="fd988-174">Si desidera toocontinue toouse imaging soluzioni tooconfigure dispositivi per i dipendenti.</span><span class="sxs-lookup"><span data-stu-id="fd988-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="fd988-175">È possibile configurare dispositivi aggiunti all'identità ibrida di Azure AD per Windows 10 e dispositivi di livello inferiore, ad esempio Windows 8 e Windows 7.</span><span class="sxs-lookup"><span data-stu-id="fd988-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="fd988-176">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="fd988-176">Summary</span></span>

<span data-ttu-id="fd988-177">Con la gestione dei dispositivi in Azure AD, è possibile:</span><span class="sxs-lookup"><span data-stu-id="fd988-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="fd988-178">Semplificare il processo di hello di riportare i dispositivi sotto controllo hello di Azure AD</span><span class="sxs-lookup"><span data-stu-id="fd988-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="fd988-179">Fornire agli utenti con le risorse basate su cloud toouse facile accesso tooyour di un'organizzazione</span><span class="sxs-lookup"><span data-stu-id="fd988-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="fd988-180">Come regola generale, è consigliabile usare:</span><span class="sxs-lookup"><span data-stu-id="fd988-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="fd988-181">Dispositivi registrati in Azure AD per i dispositivi personali</span><span class="sxs-lookup"><span data-stu-id="fd988-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="fd988-182">Azure AD unita in join i dispositivi per i dispositivi non aggiunti a un tooan AD locale</span><span class="sxs-lookup"><span data-stu-id="fd988-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="fd988-183">Azure AD ibrido unita in join i dispositivi per i dispositivi che vengono aggiunti a un tooan AD locale</span><span class="sxs-lookup"><span data-stu-id="fd988-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="fd988-184">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fd988-184">Next steps</span></span>

- <span data-ttu-id="fd988-185">una panoramica delle modalità dispositivo toomanage in hello Azure portale, vedere tooget [gestendo i dispositivi con hello portale di Azure](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="fd988-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="fd988-186">toolearn ulteriori informazioni sull'accesso condizionale basato su dispositivi, vedere [configurare i criteri di accesso condizionale basato su dispositivo di Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="fd988-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="fd988-187">dispositivi di Azure AD aggiunti toosetup ibride, vedere [modalità ibrida tooconfigure Azure Active Directory unite in join i dispositivi](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="fd988-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


