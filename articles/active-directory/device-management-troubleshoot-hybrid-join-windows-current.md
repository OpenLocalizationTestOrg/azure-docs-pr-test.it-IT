---
title: "Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: 51962c14a3c32bbfa9a613fa203cc48cfea50c0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="431d8-103">Risoluzione dei problemi relativi a dispositivi Windows 10 e Windows Server 2016 aggiunti all'identità ibrida di Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="431d8-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="431d8-104">Questo argomento è applicabile ai seguenti client:</span><span class="sxs-lookup"><span data-stu-id="431d8-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="431d8-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="431d8-105">Windows 10</span></span>
-   <span data-ttu-id="431d8-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="431d8-106">Windows Server 2016</span></span>

<span data-ttu-id="431d8-107">Per altri client Windows, vedere [Risoluzione dei problemi relativi a dispositivi di livello inferiore aggiunti all'identità ibrida di Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="431d8-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="431d8-108">Questo argomento presuppone che siano stati [configurati dispositivi aggiunti all'identità ibrida di Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) per supportare gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="431d8-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="431d8-109">Accesso condizionale basato su dispositivo</span><span class="sxs-lookup"><span data-stu-id="431d8-109">Device-based conditional access</span></span>

- [<span data-ttu-id="431d8-110">Roaming aziendale delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="431d8-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- <span data-ttu-id="431d8-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)</span><span class="sxs-lookup"><span data-stu-id="431d8-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)</span></span>


<span data-ttu-id="431d8-112">Questo documento fornisce indicazioni sulla risoluzione di potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="431d8-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 


<span data-ttu-id="431d8-113">Per Windows 10 e Windows Server 2016, l'aggiunta all'identità ibrida di Azure Active Directory supporta l'aggiornamento di Windows del 10 novembre 2015 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="431d8-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="431d8-114">È consigliabile usare l'aggiornamento dell'anniversario.</span><span class="sxs-lookup"><span data-stu-id="431d8-114">We recommend using the Anniversary update.</span></span>

## <a name="step-1-retrieve-the-join-status"></a><span data-ttu-id="431d8-115">Passaggio 1: Recuperare lo stato delle aggiunte</span><span class="sxs-lookup"><span data-stu-id="431d8-115">Step 1: Retrieve the join status</span></span> 

<span data-ttu-id="431d8-116">**Per recuperare lo stato delle aggiunte:**</span><span class="sxs-lookup"><span data-stu-id="431d8-116">**To retrieve the join status:**</span></span>

1. <span data-ttu-id="431d8-117">Aprire il prompt dei comandi come amministratore</span><span class="sxs-lookup"><span data-stu-id="431d8-117">Open the command prompt as an administrator</span></span>

2. <span data-ttu-id="431d8-118">Digitare **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="431d8-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="431d8-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="431d8-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="431d8-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="431d8-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="431d8-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="431d8-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="431d8-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="431d8-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="431d8-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="431d8-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-the-join-status"></a><span data-ttu-id="431d8-124">Passaggio 2: Valutare lo stato delle aggiunte</span><span class="sxs-lookup"><span data-stu-id="431d8-124">Step 2: Evaluate the join status</span></span> 

<span data-ttu-id="431d8-125">Esaminare i campi seguenti e assicurarsi che siano presenti i valori previsti:</span><span class="sxs-lookup"><span data-stu-id="431d8-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="431d8-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="431d8-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="431d8-127">Questo campo mostra se il dispositivo è aggiunto ad Azure AD.</span><span class="sxs-lookup"><span data-stu-id="431d8-127">This field indicates whether the device is joined with Azure AD.</span></span> <span data-ttu-id="431d8-128">Se il valore è **NO**, l'aggiunta ad Azure AD non è ancora completata.</span><span class="sxs-lookup"><span data-stu-id="431d8-128">If the value is **NO**, the join to Azure AD has not completed yet.</span></span> 

<span data-ttu-id="431d8-129">**Possibili cause:**</span><span class="sxs-lookup"><span data-stu-id="431d8-129">**Possible causes:**</span></span>

- <span data-ttu-id="431d8-130">L'autenticazione del computer per un'aggiunta non è riuscita.</span><span class="sxs-lookup"><span data-stu-id="431d8-130">Authentication of the computer for a join failed.</span></span>

- <span data-ttu-id="431d8-131">È presente un proxy HTTP nell'organizzazione che non può essere individuato dal computer</span><span class="sxs-lookup"><span data-stu-id="431d8-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="431d8-132">Il computer non riesce a raggiungere Azure AD per l'autenticazione o il servizio Registrazione dispositivo Azure per la registrazione</span><span class="sxs-lookup"><span data-stu-id="431d8-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="431d8-133">Il computer non è presente nella rete interna dell'organizzazione o nella VPN con connessione diretta a un controller di dominio locale AD.</span><span class="sxs-lookup"><span data-stu-id="431d8-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="431d8-134">Se il computer dispone di TPM, potrebbe essere in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="431d8-134">If the computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="431d8-135">Verificare nuovamente le configurazioni precedentemente indicate per assicurarsi che non ci siano errori.</span><span class="sxs-lookup"><span data-stu-id="431d8-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="431d8-136">Esempi comuni:</span><span class="sxs-lookup"><span data-stu-id="431d8-136">Common examples are:</span></span>

    - <span data-ttu-id="431d8-137">Il server federativo non dispone di endpoint WS-Trust abilitati</span><span class="sxs-lookup"><span data-stu-id="431d8-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="431d8-138">Il server federativo non consente l'autenticazione in ingresso dai computer nella rete con l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="431d8-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="431d8-139">Non è presente alcun oggetto Punto di connessione del servizio che punti al nome di dominio verificato in Azure AD nella foresta AD a cui appartiene il computer</span><span class="sxs-lookup"><span data-stu-id="431d8-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="431d8-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="431d8-140">DomainJoined : YES</span></span>  

<span data-ttu-id="431d8-141">Questo campo mostra se il dispositivo è aggiunto a un dominio Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="431d8-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="431d8-142">Se il valore è **NO**, il dispositivo non riesce a eseguire un'aggiunta all'identità ibrida di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="431d8-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="431d8-143">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="431d8-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="431d8-144">Questo campo mostra se il dispositivo è registrato con Azure AD come dispositivo personale, contrassegnato come *aggiunto correttamente* all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="431d8-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="431d8-145">Questo valore deve essere **NO** per un computer aggiunto al dominio che è anche aggiunto all'identità ibrida di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="431d8-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="431d8-146">Se il valore è **YES**, è stato aggiunto un account aziendale o dell'istituto di istruzione prima del completamento dell'aggiunta all'identità ibrida di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="431d8-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span></span> <span data-ttu-id="431d8-147">In questo caso l'account viene ignorato quando si usa la versione anniversario dell'aggiornamento di Windows 10 (1607).</span><span class="sxs-lookup"><span data-stu-id="431d8-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="431d8-148">WamDefaultSet: YES e AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="431d8-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="431d8-149">Questi campi indicano se l'utente è autenticato correttamente in Azure AD durante l'accesso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="431d8-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span></span> <span data-ttu-id="431d8-150">Se i valori sono **NO**, il motivo potrebbe essere:</span><span class="sxs-lookup"><span data-stu-id="431d8-150">If the values are **NO**, it could be due:</span></span>

- <span data-ttu-id="431d8-151">Chiave di archiviazione STK non valida in TPM e associata al dispositivo al momento della registrazione. Verificare KeySignTest durante l'esecuzione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="431d8-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="431d8-152">ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="431d8-152">Alternate Login ID</span></span>

- <span data-ttu-id="431d8-153">Proxy HTTP non trovato</span><span class="sxs-lookup"><span data-stu-id="431d8-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="431d8-154">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="431d8-154">Next steps</span></span>

<span data-ttu-id="431d8-155">Per altre informazioni, vedere le [domande frequenti sulla gestione dei dispositivi](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="431d8-155">For questions, see the [device management FAQ](device-management-faq.md)</span></span> 