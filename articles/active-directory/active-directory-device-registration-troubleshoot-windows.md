---
title: appartenenti aaaTroubleshooting hello-registrazione automatica del dominio di Azure AD per Windows 10 e Windows Server 2016 | Documenti Microsoft
description: Risoluzione dei problemi di registrazione automatica hello del dominio di Azure AD aggiunto a un computer Windows 10 e Windows Server 2016.
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="c0d45-103">Risoluzione dei problemi di registrazione automatica del dominio aggiunti a un computer tooAzure AD – Windows 10 e Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c0d45-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="c0d45-104">In questo argomento è applicabile toohello client seguenti:</span><span class="sxs-lookup"><span data-stu-id="c0d45-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="c0d45-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="c0d45-105">Windows 10</span></span>
-   <span data-ttu-id="c0d45-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="c0d45-106">Windows Server 2016</span></span>

<span data-ttu-id="c0d45-107">Per altri client di Windows, vedere [risoluzione dei problemi di registrazione automatica del dominio aggiunto tooAzure computer Active Directory per i client legacy di Windows](active-directory-device-registration-troubleshoot-windows-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="c0d45-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="c0d45-108">Questo argomento si presuppone di aver configurato la registrazione automatica dei dispositivi appartenenti a un dominio come descritto in descritto in [come tooconfigure la registrazione automatica di Windows appartenenti a un dominio dispositivi con Azure Active Directory](active-directory-device-registration-get-started.md) hello toosupport seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="c0d45-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="c0d45-109">Accesso condizionale basato su dispositivo</span><span class="sxs-lookup"><span data-stu-id="c0d45-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="c0d45-110">Roaming aziendale delle impostazioni</span><span class="sxs-lookup"><span data-stu-id="c0d45-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- <span data-ttu-id="c0d45-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md) (Configurare Windows Hello for Business)</span><span class="sxs-lookup"><span data-stu-id="c0d45-111">[Windows Hello for Business](active-directory-azureadjoin-passport-deployment.md)</span></span>


<span data-ttu-id="c0d45-112">Questo documento fornisce istruzioni sulla risoluzione dei problemi in modo tooresolve potenziali problemi.</span><span class="sxs-lookup"><span data-stu-id="c0d45-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="c0d45-113">Hello registrazione è supportata in Windows hello aggiornamento 10 novembre 2015 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c0d45-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="c0d45-114">È consigliabile utilizzare hello dall'aggiornamento Aniversary per l'abilitazione di scenari di hello precedenti.</span><span class="sxs-lookup"><span data-stu-id="c0d45-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="c0d45-115">Passaggio 1: Recuperare lo stato della registrazione hello</span><span class="sxs-lookup"><span data-stu-id="c0d45-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="c0d45-116">**stato della registrazione tooretrieve hello:**</span><span class="sxs-lookup"><span data-stu-id="c0d45-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="c0d45-117">Aprire il prompt dei comandi di hello come amministratore.</span><span class="sxs-lookup"><span data-stu-id="c0d45-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="c0d45-118">Digitare **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="c0d45-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="c0d45-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="c0d45-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="c0d45-120">EnterpriseJoined: Nessun DeviceId: identificazione personale 5820fbe9-60c8-43b0-bb11-44aee233e4e7: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: TpmProtected del Provider di crittografia della piattaforma Microsoft: Sì KeySignTest:: deve eseguire con privilegi elevati tootest.</span><span class="sxs-lookup"><span data-stu-id="c0d45-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="c0d45-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="c0d45-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="c0d45-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="c0d45-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="c0d45-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="c0d45-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="c0d45-124">Passaggio 2: Valutare lo stato della registrazione hello</span><span class="sxs-lookup"><span data-stu-id="c0d45-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="c0d45-125">Esaminare i seguenti campi hello e assicurarsi che dispongano di valori previsti hello:</span><span class="sxs-lookup"><span data-stu-id="c0d45-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="c0d45-126">AzureAdJoined: YES</span><span class="sxs-lookup"><span data-stu-id="c0d45-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="c0d45-127">Questo campo viene visualizzato se il dispositivo di hello è registrato con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0d45-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="c0d45-128">Se il valore di hello Mostra come 'NO', non è stata completata la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c0d45-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="c0d45-129">**Possibili cause:**</span><span class="sxs-lookup"><span data-stu-id="c0d45-129">**Possible causes:**</span></span>

- <span data-ttu-id="c0d45-130">Autenticazione del computer hello per la registrazione non riuscita.</span><span class="sxs-lookup"><span data-stu-id="c0d45-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="c0d45-131">È un proxy HTTP nell'organizzazione hello che non può essere individuati dal computer hello</span><span class="sxs-lookup"><span data-stu-id="c0d45-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="c0d45-132">non riesce a raggiungere il computer Hello Azure Active Directory per l'autenticazione o Azure DRS per la registrazione</span><span class="sxs-lookup"><span data-stu-id="c0d45-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="c0d45-133">Hello computer potrebbero non essere nella rete interna dell'organizzazione hello o VPN con tooan diretto visibilità diretta del controller di dominio Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="c0d45-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="c0d45-134">Se il computer di hello dispone di un TPM, potrebbe essere in uno stato non valido.</span><span class="sxs-lookup"><span data-stu-id="c0d45-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="c0d45-135">Potrebbe esserci un errore di configurazione in servizi di evidenziato nel documento hello che sarà necessario tooverify nuovamente.</span><span class="sxs-lookup"><span data-stu-id="c0d45-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="c0d45-136">Esempi comuni:</span><span class="sxs-lookup"><span data-stu-id="c0d45-136">Common examples are:</span></span>

    - <span data-ttu-id="c0d45-137">Il server federativo non dispone di endpoint WS-Trust abilitati</span><span class="sxs-lookup"><span data-stu-id="c0d45-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="c0d45-138">Il server federativo potrebbe non consentire l'autenticazione in ingresso dai computer nella rete con l'autenticazione integrata di Windows.</span><span class="sxs-lookup"><span data-stu-id="c0d45-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="c0d45-139">È presente alcun oggetto punto di connessione del servizio che fa riferimento il nome di dominio verificato tooyour in Azure Active Directory nella foresta Active Directory hello cui appartiene il computer di hello</span><span class="sxs-lookup"><span data-stu-id="c0d45-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="c0d45-140">DomainJoined: YES</span><span class="sxs-lookup"><span data-stu-id="c0d45-140">DomainJoined : YES</span></span>  

<span data-ttu-id="c0d45-141">Questo campo Mostra se dispositivo hello è unita in join tooan Active Directory locale o meno.</span><span class="sxs-lookup"><span data-stu-id="c0d45-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="c0d45-142">Se il valore di hello Mostra come **n**, dispositivo hello non vengono registrati automaticamente con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0d45-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="c0d45-143">Verificare innanzitutto che toohello di join hello dispositivo in Active Directory locale prima che la registrazione con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0d45-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="c0d45-144">Se si sta cercando di unione hello computer tooAzure AD direttamente, visitare tooLearn sulle funzionalità di Azure Active Directory Join.</span><span class="sxs-lookup"><span data-stu-id="c0d45-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="c0d45-145">WorkplaceJoined: NO</span><span class="sxs-lookup"><span data-stu-id="c0d45-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="c0d45-146">Questo campo viene visualizzato se il dispositivo di hello è registrato con Azure AD, ma come un dispositivo personale (contrassegnati come 'All'area di lavoro').</span><span class="sxs-lookup"><span data-stu-id="c0d45-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="c0d45-147">Se questo valore deve essere 'NO' per un computer aggiunto a un dominio registrato con Azure AD, tuttavia se viene visualizzato Sì significa che un account aziendale o dell'istituto di istruzione è stata aggiunta toohello precedente computer con la registrazione.</span><span class="sxs-lookup"><span data-stu-id="c0d45-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="c0d45-148">In questo caso account hello verrà ignorato se si utilizza una versione di hello dall'aggiornamento Aniversary di Windows 10 (1607 quando in esecuzione comando WinVer hello in hello finestra 'Esegui' o una finestra del prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="c0d45-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="c0d45-149">WamDefaultSet: YES e AzureADPrt: YES</span><span class="sxs-lookup"><span data-stu-id="c0d45-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="c0d45-150">Questi campi mostrano che l'utente hello ha autenticato tooAzure Active Directory all'accesso toohello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c0d45-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="c0d45-151">Se vengono visualizzate 'NO' hello Ecco le possibili cause:</span><span class="sxs-lookup"><span data-stu-id="c0d45-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="c0d45-152">Chiave di archiviazione non valida (STK) nel TPM associato hello dispositivo durante la registrazione (controllo hello KeySignTest durante l'esecuzione con privilegi elevati).</span><span class="sxs-lookup"><span data-stu-id="c0d45-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="c0d45-153">ID di accesso alternativo</span><span class="sxs-lookup"><span data-stu-id="c0d45-153">Alternate Login ID</span></span>

- <span data-ttu-id="c0d45-154">Proxy HTTP non trovato</span><span class="sxs-lookup"><span data-stu-id="c0d45-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="c0d45-155">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c0d45-155">Next steps</span></span>

<span data-ttu-id="c0d45-156">Per ulteriori informazioni, vedere hello [domande frequenti sulla registrazione automatica dei dispositivi](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c0d45-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
