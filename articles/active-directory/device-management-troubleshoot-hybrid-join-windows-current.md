---
title: dispositivi Windows 10 e Windows Server 2016 unita in join ibrido aaaTroubleshooting Azure Active Directory | Documenti Microsoft
description: "Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="7f1a3-103">Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f1a3-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="7f1a3-104">In questo argomento è applicabile toohello client seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f1a3-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="7f1a3-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="7f1a3-105">Windows 10</span></span>
-   <span data-ttu-id="7f1a3-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="7f1a3-106">Windows Server 2016</span></span>

<span data-ttu-id="7f1a3-107">Per altri client Windows, vedere [Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="7f1a3-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="7f1a3-108">In questo argomento si presuppone che sia [Configurazione ibrida di Azure Active Directory i dispositivi appartenenti](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="7f1a3-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="7f1a3-109">Accesso condizionale basato su dispositivo</span><span class="sxs-lookup"><span data-stu-id="7f1a3-109">Device-based conditional access</span></span>

- [<span data-ttu-id="7f1a3-110">Roaming aziendale delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="7f1a3-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- <span data-ttu-id="7f1a3-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)</span><span class="sxs-lookup"><span data-stu-id="7f1a3-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)</span></span>


<span data-ttu-id="7f1a3-112">Questo documento fornisce istruzioni sulla risoluzione dei problemi in modo tooresolve potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="7f1a3-113">Per Windows 10 e Windows Server 2016, ibrida di Azure Active Directory join supporta hello Windows 10 aggiornamento di novembre 2015 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="7f1a3-114">È consigliabile utilizzare dall'aggiornamento Aniversary hello.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="7f1a3-115">Passaggio 1: Recuperare lo stato di join hello</span><span class="sxs-lookup"><span data-stu-id="7f1a3-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="7f1a3-116">**stato di join tooretrieve hello:**</span><span class="sxs-lookup"><span data-stu-id="7f1a3-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="7f1a3-117">Hello Apri prompt dei comandi come amministratore</span><span class="sxs-lookup"><span data-stu-id="7f1a3-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="7f1a3-118">Digitare **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="7f1a3-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="7f1a3-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="7f1a3-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="7f1a3-120">EnterpriseJoined: Nessun DeviceId: identificazione personale 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected del Provider di crittografia della piattaforma Microsoft: Sì KeySignTest:: deve eseguire con privilegi elevati tootest.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="7f1a3-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="7f1a3-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="7f1a3-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="7f1a3-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="7f1a3-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="7f1a3-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="7f1a3-124">Passaggio 2: Valutare lo stato di join hello</span><span class="sxs-lookup"><span data-stu-id="7f1a3-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="7f1a3-125">Esaminare i seguenti campi hello e assicurarsi che dispongano di valori previsti hello:</span><span class="sxs-lookup"><span data-stu-id="7f1a3-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="7f1a3-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="7f1a3-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="7f1a3-127">Questo campo indica se il dispositivo hello viene unito con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="7f1a3-128">Se il valore di hello è **n**, hello tooAzure join Active Directory non è ancora completato.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="7f1a3-129">**Possibili cause:**</span><span class="sxs-lookup"><span data-stu-id="7f1a3-129">**Possible causes:**</span></span>

- <span data-ttu-id="7f1a3-130">Autenticazione del computer hello per un join non riuscita.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="7f1a3-131">È un proxy HTTP nell'organizzazione hello che non può essere individuati dal computer hello</span><span class="sxs-lookup"><span data-stu-id="7f1a3-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="7f1a3-132">computer Hello non riesce a raggiungere tooauthenticate AD Azure o Azure DRS per la registrazione</span><span class="sxs-lookup"><span data-stu-id="7f1a3-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="7f1a3-133">Hello computer potrebbero non essere nella rete interna dell'organizzazione hello o VPN con tooan diretto visibilità diretta del controller di dominio Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="7f1a3-134">Se il computer di hello dispone di un TPM, può essere in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="7f1a3-135">Potrebbe esserci un errore di configurazione in servizi di hello evidenziato nel documento hello che sarà necessario tooverify nuovamente.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="7f1a3-136">Esempi comuni:</span><span class="sxs-lookup"><span data-stu-id="7f1a3-136">Common examples are:</span></span>

    - <span data-ttu-id="7f1a3-137">Il server federativo non dispone di endpoint WS-Trust abilitati</span><span class="sxs-lookup"><span data-stu-id="7f1a3-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="7f1a3-138">Il server federativo non consente l'autenticazione in ingresso dai computer nella rete con l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="7f1a3-139">È presente alcun oggetto punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello</span><span class="sxs-lookup"><span data-stu-id="7f1a3-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="7f1a3-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="7f1a3-140">DomainJoined : YES</span></span>  

<span data-ttu-id="7f1a3-141">Questo campo indica se si aggiunge il dispositivo hello tooan Active Directory locale o non.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="7f1a3-142">Se il valore di hello è **n**, dispositivo hello non è possibile eseguire un join di Azure AD ibrido.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="7f1a3-143">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="7f1a3-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="7f1a3-144">Questo campo indica se il dispositivo di hello è registrato con Azure AD come un dispositivo personale (contrassegnata come *all'area di lavoro*).</span><span class="sxs-lookup"><span data-stu-id="7f1a3-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="7f1a3-145">Questo valore deve essere **NO** per un computer aggiunto al dominio che è anche aggiunto all'identità ibrida di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="7f1a3-146">Se il valore di hello è **Sì**, completamento toohello precedente di join di Azure AD ibrido hello è stato aggiunto un account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="7f1a3-147">In questo caso, l'account di hello viene ignorato quando si utilizza una versione di hello dall'aggiornamento Aniversary di Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="7f1a3-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="7f1a3-148">WamDefaultSet: YES e AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="7f1a3-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="7f1a3-149">Questi campi indicano se utente hello è autenticata correttamente tooAzure AD durante l'accesso toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="7f1a3-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="7f1a3-150">Se i valori hello sono **n**, potrebbe essere dovuto:</span><span class="sxs-lookup"><span data-stu-id="7f1a3-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="7f1a3-151">Chiave di archiviazione non valida (STK) nel TPM associato hello dispositivo durante la registrazione (controllo hello KeySignTest durante l'esecuzione con privilegi elevati).</span><span class="sxs-lookup"><span data-stu-id="7f1a3-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="7f1a3-152">ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="7f1a3-152">Alternate Login ID</span></span>

- <span data-ttu-id="7f1a3-153">Proxy HTTP non trovato</span><span class="sxs-lookup"><span data-stu-id="7f1a3-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f1a3-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f1a3-154">Next steps</span></span>

<span data-ttu-id="7f1a3-155">Per domande, vedere hello [domande frequenti sulla gestione dei dispositivi](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="7f1a3-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
