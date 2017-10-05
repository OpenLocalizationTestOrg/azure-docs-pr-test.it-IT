---
title: Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio Azure AD per client di livello inferiore di Windows 10 e Windows Server 2016 | Microsoft Docs
description: Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio Azure AD per client di livello inferiore di Windows 10 e Windows Server 2016.
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="bf24f-103">Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio di Azure AD - Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bf24f-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="bf24f-104">Questo argomento è applicabile ai seguenti client:</span><span class="sxs-lookup"><span data-stu-id="bf24f-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="bf24f-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="bf24f-105">Windows 10</span></span>
-   <span data-ttu-id="bf24f-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bf24f-106">Windows Server 2016</span></span>

<span data-ttu-id="bf24f-107">Per altri client Windows, vedere [Risoluzione dei problemi di registrazione automatica di computer aggiunti al dominio Azure AD per client di livello inferiore di Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="bf24f-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="bf24f-108">Questo argomento presuppone che la registrazione automatica dei dispositivi aggiunti a un dominio sia stata configurata come descritto in [Come configurare la registrazione automatica dei dispositivi aggiunti al dominio di Windows con Azure Active Directory](active-directory-device-registration-get-started.md) per il supporto degli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="bf24f-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="bf24f-109">Accesso condizionale basato su dispositivo</span><span class="sxs-lookup"><span data-stu-id="bf24f-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="bf24f-110">Roaming aziendale delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="bf24f-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- <span data-ttu-id="bf24f-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)</span><span class="sxs-lookup"><span data-stu-id="bf24f-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)</span></span>


<span data-ttu-id="bf24f-112">Questo documento fornisce indicazioni sulla risoluzione di potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="bf24f-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="bf24f-113">La registrazione è supportata in nell'aggiornamento di Windows 10 di novembre 2015 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="bf24f-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="bf24f-114">È consigliabile usare l'aggiornamento dell'anniversario per abilitare gli scenari descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="bf24f-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="bf24f-115">Passaggio 1: Recuperare lo stato della registrazione</span><span class="sxs-lookup"><span data-stu-id="bf24f-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="bf24f-116">**Per recuperare lo stato della registrazione:**</span><span class="sxs-lookup"><span data-stu-id="bf24f-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="bf24f-117">Aprire il prompt dei comandi come amministratore.</span><span class="sxs-lookup"><span data-stu-id="bf24f-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="bf24f-118">Digitare **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="bf24f-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="bf24f-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="bf24f-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="bf24f-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="bf24f-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="bf24f-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="bf24f-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="bf24f-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="bf24f-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="bf24f-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="bf24f-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="bf24f-124">Passaggio 2: Valutare lo stato della registrazione</span><span class="sxs-lookup"><span data-stu-id="bf24f-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="bf24f-125">Esaminare i campi seguenti e assicurarsi che siano presenti i valori previsti:</span><span class="sxs-lookup"><span data-stu-id="bf24f-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="bf24f-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="bf24f-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="bf24f-127">Questo campo indica se il dispositivo è registrato con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf24f-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="bf24f-128">Se il valore visualizzato è "NO", la registrazione non è stata completata.</span><span class="sxs-lookup"><span data-stu-id="bf24f-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="bf24f-129">**Possibili cause:**</span><span class="sxs-lookup"><span data-stu-id="bf24f-129">**Possible causes:**</span></span>

- <span data-ttu-id="bf24f-130">Autenticazione del computer non riuscita per la registrazione.</span><span class="sxs-lookup"><span data-stu-id="bf24f-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="bf24f-131">È presente un proxy HTTP nell'organizzazione che non può essere individuato dal computer</span><span class="sxs-lookup"><span data-stu-id="bf24f-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="bf24f-132">Il computer non riesce a raggiungere Azure AD per l'autenticazione o il servizio Registrazione dispositivo Azure per la registrazione</span><span class="sxs-lookup"><span data-stu-id="bf24f-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="bf24f-133">Il computer non è presente nella rete interna dell'organizzazione o nella VPN con connessione diretta a un controller di dominio locale AD.</span><span class="sxs-lookup"><span data-stu-id="bf24f-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="bf24f-134">Se il computer dispone di TPM, potrebbe essere in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="bf24f-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="bf24f-135">Verificare nuovamente le configurazioni precedentemente indicate per assicurarsi che non ci siano errori.</span><span class="sxs-lookup"><span data-stu-id="bf24f-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="bf24f-136">Esempi comuni:</span><span class="sxs-lookup"><span data-stu-id="bf24f-136">Common examples are:</span></span>

    - <span data-ttu-id="bf24f-137">Il server federativo non dispone di endpoint WS-Trust abilitati</span><span class="sxs-lookup"><span data-stu-id="bf24f-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="bf24f-138">Il server federativo potrebbe non consentire l'autenticazione in ingresso dai computer nella rete con l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="bf24f-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="bf24f-139">Non è presente alcun oggetto Punto di connessione del servizio che punti al nome di dominio verificato in Azure AD nella foresta AD a cui appartiene il computer</span><span class="sxs-lookup"><span data-stu-id="bf24f-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="bf24f-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="bf24f-140">DomainJoined : YES</span></span>  

<span data-ttu-id="bf24f-141">Questo campo indica se il dispositivo è aggiunto a un dominio Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="bf24f-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="bf24f-142">Se il valore visualizzato è **NO**, il dispositivo non può eseguire la registrazione automatica con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf24f-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="bf24f-143">Verificare innanzitutto che il dispositivo sia aggiunto al dominio Active Directory locale prima della registrazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bf24f-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="bf24f-144">Se si sta cercando di aggiungere il computer direttamente in Azure AD, passare a Ulteriori informazioni sulle funzionalità di Aggiunta ad Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="bf24f-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="bf24f-145">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="bf24f-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="bf24f-146">Questo campo indica se il dispositivo è registrato con Azure AD ma come dispositivo personale, contrassegnato come aggiunto correttamente all'area di lavoro.</span><span class="sxs-lookup"><span data-stu-id="bf24f-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="bf24f-147">Il valore visualizzato deve essere "NO" per un computer aggiunto a un dominio e registrato con Azure AD. Se è "YES", significa che è stato aggiunto un account aziendale o dell'istituto di istruzione prima del completamento della registrazione.</span><span class="sxs-lookup"><span data-stu-id="bf24f-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="bf24f-148">In questo caso l'account verrà ignorato se si usa l'aggiornamento dell'anniversario di Windows 10 (1607 quando si usa il comando WinVer nella finestra "Esegui" o in un prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="bf24f-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="bf24f-149">WamDefaultSet: YES e AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="bf24f-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="bf24f-150">Questi campi mostrano che l'utente è autenticato correttamente in Azure AD durante l'accesso al dispositivo.</span><span class="sxs-lookup"><span data-stu-id="bf24f-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="bf24f-151">Se il valore visualizzato è "NO", di seguito vengono elencate alcune possibili cause:</span><span class="sxs-lookup"><span data-stu-id="bf24f-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="bf24f-152">Chiave di archiviazione STK non valida in TPM e associata al dispositivo al momento della registrazione. Verificare KeySignTest durante l'esecuzione con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="bf24f-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="bf24f-153">ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="bf24f-153">Alternate Login ID</span></span>

- <span data-ttu-id="bf24f-154">Proxy HTTP non trovato</span><span class="sxs-lookup"><span data-stu-id="bf24f-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="bf24f-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bf24f-155">Next steps</span></span>

<span data-ttu-id="bf24f-156">Per ulteriori informazioni, vedere [Domande frequenti sulla registrazione automatica dei dispositivi](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="bf24f-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 