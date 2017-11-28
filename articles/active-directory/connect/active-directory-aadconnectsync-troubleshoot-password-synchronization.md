---
title: sincronizzazione delle password aaaTroubleshoot con sincronizzazione di Azure AD Connect | Documenti Microsoft
description: In questo articolo fornisce informazioni su come i problemi di sincronizzazione password tootroubleshoot.
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="da3be-103">Risolvere i problemi di sincronizzazione della password con il servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="da3be-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="da3be-104">Questo argomento illustra i passaggi per la modalità tootroubleshoot problemi con la sincronizzazione delle password.</span><span class="sxs-lookup"><span data-stu-id="da3be-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="da3be-105">Se le password non vengono sincronizzate come previsto, il problema può riguardare un subset di utenti o tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="da3be-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="da3be-106">Per Azure Active Directory (Azure AD) connettere distribuzione con la versione 1.1.524.0 o versioni successive, è ora disponibile un cmdlet di diagnostica che è possibile utilizzare tootroubleshoot problemi di sincronizzazione password:</span><span class="sxs-lookup"><span data-stu-id="da3be-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="da3be-107">Se si dispone di un problema in cui non vengono sincronizzati alcuna password, consultare toohello [non le password vengono sincronizzate: risolvere i problemi utilizzando i cmdlet di diagnostica hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) sezione.</span><span class="sxs-lookup"><span data-stu-id="da3be-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="da3be-108">Se si dispone di un problema con i singoli oggetti, consultare toohello [un oggetto è non in sincronizzazione password: risolvere i problemi utilizzando i cmdlet di diagnostica hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) sezione.</span><span class="sxs-lookup"><span data-stu-id="da3be-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="da3be-109">Per le versioni precedenti della distribuzione di Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="da3be-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="da3be-110">Se si dispone di un problema in cui non vengono sincronizzati alcuna password, consultare toohello [non le password vengono sincronizzate: risoluzione manuale](#no-passwords-are-synchronized-manual-troubleshooting-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="da3be-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="da3be-111">Se si dispone di un problema con i singoli oggetti, consultare toohello [un oggetto è non in sincronizzazione password: risoluzione manuale](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="da3be-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="da3be-112">Nessun password vengono sincronizzate: risolvere i problemi utilizzando i cmdlet di diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="da3be-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="da3be-113">È possibile utilizzare hello `Invoke-ADSyncDiagnostics` toofigure cmdlet out perché nessuna password è sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="da3be-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="da3be-114">Hello `Invoke-ADSyncDiagnostics` cmdlet è disponibile solo per la versione di Azure AD Connect 1.1.524.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="da3be-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="da3be-115">Eseguire i cmdlet di diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="da3be-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="da3be-116">problemi di tootroubleshoot in cui non vengono sincronizzati alcuna password:</span><span class="sxs-lookup"><span data-stu-id="da3be-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="da3be-117">Aprire una nuova sessione di Windows PowerShell nel server di Azure AD Connect con hello **Esegui come amministratore** opzione.</span><span class="sxs-lookup"><span data-stu-id="da3be-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="da3be-118">Eseguire `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="da3be-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="da3be-119">Eseguire `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="da3be-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="da3be-120">Eseguire `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="da3be-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="da3be-121">Comprendere i risultati di hello del cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="da3be-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="da3be-122">cmdlet di diagnostica Hello esegue hello seguenti controlli:</span><span class="sxs-lookup"><span data-stu-id="da3be-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="da3be-123">Convalida che hello funzionalità di sincronizzazione password è abilitata per il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da3be-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="da3be-124">Convalida che hello Azure AD Connect, server non è in modalità di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="da3be-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="da3be-125">Per ogni esistente locali di Active Directory connector (che corrisponde a foresta Active Directory esistente tooan):</span><span class="sxs-lookup"><span data-stu-id="da3be-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="da3be-126">Convalida che hello è abilitata la funzionalità di sincronizzazione password.</span><span class="sxs-lookup"><span data-stu-id="da3be-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="da3be-127">Cerca gli eventi di heartbeat di sincronizzazione password in hello registri eventi applicazioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="da3be-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="da3be-128">Per ogni dominio di Active Directory in connettore di Active Directory locale hello:</span><span class="sxs-lookup"><span data-stu-id="da3be-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="da3be-129">Convalida che hello dominio sia raggiungibile dal server di hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="da3be-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="da3be-130">Verifica che gli account di servizi di dominio Active Directory (AD DS) hello usati dal connettore di Active Directory locale hello è hello correttezza del nome utente, password e delle autorizzazioni necessarie per la sincronizzazione delle password.</span><span class="sxs-lookup"><span data-stu-id="da3be-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="da3be-131">Hello seguente diagramma illustra i risultati di hello del cmdlet hello per una topologia di Active Directory locale a dominio singolo:</span><span class="sxs-lookup"><span data-stu-id="da3be-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Output di diagnostica per la sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="da3be-133">Hello in questa sezione descrive i risultati specifici che vengono restituiti dal cmdlet hello e problemi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="da3be-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="da3be-134">La funzionalità di sincronizzazione delle password non è abilitata</span><span class="sxs-lookup"><span data-stu-id="da3be-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="da3be-135">Se è stata abilitata la sincronizzazione delle password utilizzando la procedura guidata di hello Azure AD Connect, viene restituito il seguente errore hello:</span><span class="sxs-lookup"><span data-stu-id="da3be-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![La sincronizzazione delle password non è abilitata](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="da3be-137">Il server di Azure AD Connect è in modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="da3be-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="da3be-138">Se il server di Azure AD Connect hello è in modalità di gestione temporanea, la sincronizzazione delle password è temporaneamente disabilitata e hello seguente errore:</span><span class="sxs-lookup"><span data-stu-id="da3be-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Il server di Azure AD Connect è in modalità di gestione temporanea](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="da3be-140">Eventi heartbeat di mancata sincronizzazione delle password</span><span class="sxs-lookup"><span data-stu-id="da3be-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="da3be-141">Ogni istanza locale di Active Directory Connector ha uno specifico canale di sincronizzazione delle password.</span><span class="sxs-lookup"><span data-stu-id="da3be-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="da3be-142">Quando viene stabilito canale di sincronizzazione password hello e non vi sono eventuali toobe modifiche password sincronizzate, un evento di heartbeat (EventId 654) viene generato una volta ogni 30 minuti nel registro eventi applicazioni di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="da3be-143">Per ogni connettore di Active Directory locale, hello cmdlet Cerca eventi heartbeat corrispondenti in hello ultime tre ore.</span><span class="sxs-lookup"><span data-stu-id="da3be-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="da3be-144">Se non viene trovato alcun evento di heartbeat, hello seguente errore:</span><span class="sxs-lookup"><span data-stu-id="da3be-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Evento heartbeat di mancata sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="da3be-146">L'account di Active Directory Domain Services non ha le autorizzazioni corrette</span><span class="sxs-lookup"><span data-stu-id="da3be-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="da3be-147">Se l'account di hello di dominio Active Directory che viene usato da hello locale hash delle password di Active Directory connector toosynchronize non dispone delle autorizzazioni appropriate di hello, hello seguente errore:</span><span class="sxs-lookup"><span data-stu-id="da3be-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Credenziali non corrette](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="da3be-149">La password o il nome utente dell'account di Active Directory Domain Services non è corretto</span><span class="sxs-lookup"><span data-stu-id="da3be-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="da3be-150">Se hello account di dominio Active Directory utilizzata da hello gli hash delle password locali Active Directory connector toosynchronize ha un nome utente non corretto o la password, hello seguente errore:</span><span class="sxs-lookup"><span data-stu-id="da3be-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Credenziali non corrette](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="da3be-152">Un oggetto è non in sincronizzazione password: risolvere i problemi utilizzando i cmdlet di diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="da3be-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="da3be-153">È possibile utilizzare hello `Invoke-ADSyncDiagnostics` toodetermine cmdlet perché un oggetto è non in sincronizzazione delle password.</span><span class="sxs-lookup"><span data-stu-id="da3be-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="da3be-154">Hello `Invoke-ADSyncDiagnostics` cmdlet è disponibile solo per la versione di Azure AD Connect 1.1.524.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="da3be-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="da3be-155">Eseguire i cmdlet di diagnostica hello</span><span class="sxs-lookup"><span data-stu-id="da3be-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="da3be-156">problemi di tootroubleshoot in cui non vengono sincronizzati alcuna password:</span><span class="sxs-lookup"><span data-stu-id="da3be-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="da3be-157">Aprire una nuova sessione di Windows PowerShell nel server di Azure AD Connect con hello **Esegui come amministratore** opzione.</span><span class="sxs-lookup"><span data-stu-id="da3be-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="da3be-158">Eseguire `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="da3be-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="da3be-159">Eseguire `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="da3be-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="da3be-160">Eseguire hello seguente cmdlet:</span><span class="sxs-lookup"><span data-stu-id="da3be-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="da3be-161">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="da3be-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="da3be-162">Comprendere i risultati di hello del cmdlet hello</span><span class="sxs-lookup"><span data-stu-id="da3be-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="da3be-163">cmdlet di diagnostica Hello esegue hello seguenti controlli:</span><span class="sxs-lookup"><span data-stu-id="da3be-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="da3be-164">Esamina lo stato di hello dell'oggetto di Active Directory hello spazio connettore di Active Directory hello Metaverse e Azure spazio connettore di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da3be-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="da3be-165">Convalida che non esistono regole di sincronizzazione con la sincronizzazione delle password è abilitata e applicata toohello oggetto di Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da3be-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="da3be-166">Prova tooretrieve e visualizzare risultati hello di hello ultimo tentativo toosynchronize hello password per l'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="da3be-167">Hello seguente diagramma illustra i risultati di hello del cmdlet hello quando la risoluzione dei problemi di sincronizzazione delle password per un singolo oggetto:</span><span class="sxs-lookup"><span data-stu-id="da3be-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Output di diagnostica per la sincronizzazione delle password: singolo oggetto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="da3be-169">Hello in questa sezione descrive i risultati specifici restituiti dal cmdlet hello e problemi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="da3be-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="da3be-170">oggetto di Active Directory Hello non esportati tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="da3be-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="da3be-171">La sincronizzazione delle password per l'account di Active Directory locale non riesce perché è presente alcun oggetto corrispondente nel tenant di Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="da3be-172">viene restituito l'errore seguente Hello:</span><span class="sxs-lookup"><span data-stu-id="da3be-172">hello following error is returned:</span></span>

![Oggetto Azure AD mancante](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="da3be-174">L'utente ha una password temporanea</span><span class="sxs-lookup"><span data-stu-id="da3be-174">User has a temporary password</span></span>
<span data-ttu-id="da3be-175">Azure AD Connect non supporta attualmente la sincronizzazione delle password temporanee con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da3be-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="da3be-176">Una password viene considerata toobe temporaneo se hello **Cambia password all'accesso successivo** opzione è impostata su utente di Active Directory locale hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="da3be-177">viene restituito l'errore seguente Hello:</span><span class="sxs-lookup"><span data-stu-id="da3be-177">hello following error is returned:</span></span>

![Password temporanea non esportata](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="da3be-179">Risultati dell'ultimo tentativo toosynchronize password non sono disponibili</span><span class="sxs-lookup"><span data-stu-id="da3be-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="da3be-180">Per impostazione predefinita, Azure AD Connect archivia i risultati di hello dei tentativi di sincronizzazione password per sette giorni.</span><span class="sxs-lookup"><span data-stu-id="da3be-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="da3be-181">Se non sono disponibili per l'oggetto di Active Directory hello selezionato alcun risultato, viene restituito hello seguente avviso:</span><span class="sxs-lookup"><span data-stu-id="da3be-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Output di diagnostica per un singolo oggetto: cronologia di mancata sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="da3be-183">Nessuna password viene sincronizzata: passaggi per la risoluzione manuale dei problemi</span><span class="sxs-lookup"><span data-stu-id="da3be-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="da3be-184">Seguire questi passaggi toodetermine perché nessuna password venga sincronizzata:</span><span class="sxs-lookup"><span data-stu-id="da3be-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="da3be-185">È il server di connessione hello in [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="da3be-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="da3be-186">Un server in modalità di gestione temporanea non sincronizza le password.</span><span class="sxs-lookup"><span data-stu-id="da3be-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="da3be-187">Eseguire script hello in hello [ottenere lo stato di hello di impostazioni di sincronizzazione password](#get-the-status-of-password-sync-settings) sezione.</span><span class="sxs-lookup"><span data-stu-id="da3be-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="da3be-188">Fornisce una panoramica della configurazione di sincronizzazione password hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Output dello script di PowerShell dalle impostazioni di sincronizzazione password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="da3be-190">Se la funzione hello non è abilitata in Azure AD o hello sincronizzazione canale stato non è abilitato, eseguire hello Connetti installazione guidata.</span><span class="sxs-lookup"><span data-stu-id="da3be-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="da3be-191">Selezionare **Personalizzazione delle opzioni di sincronizzazione** e deselezionare l'opzione di sincronizzazione delle password. Questa modifica Disabilita temporaneamente funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="da3be-192">Quindi eseguire nuovamente la procedura guidata hello e riattivare la sincronizzazione delle password. Eseguire script hello nuovamente tooverify che hello configurazione sia corretto.</span><span class="sxs-lookup"><span data-stu-id="da3be-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="da3be-193">Cercare nel registro eventi di hello per gli errori.</span><span class="sxs-lookup"><span data-stu-id="da3be-193">Look in hello event log for errors.</span></span> <span data-ttu-id="da3be-194">Cercare hello eventi, che potrebbe indicare un problema di seguito:</span><span class="sxs-lookup"><span data-stu-id="da3be-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="da3be-195">Origine: ID "Sincronizzazione della directory": 0, 611, 652, 655 Se vengono visualizzati eventi di questo tipo, c'è un problema di connettività.</span><span class="sxs-lookup"><span data-stu-id="da3be-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="da3be-196">messaggio registro eventi contiene informazioni relative alla foresta in cui si verifica un problema.</span><span class="sxs-lookup"><span data-stu-id="da3be-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="da3be-197">Per altre informazioni, vedere [Problemi di connettività](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="da3be-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="da3be-198">Se non viene visualizzato alcun heartbeat o non si sono trovate altre soluzioni al problema, eseguire lo script riportato in [Attivare una sincronizzazione completa di tutte le password](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="da3be-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="da3be-199">Eseguire script hello una sola volta.</span><span class="sxs-lookup"><span data-stu-id="da3be-199">Run hello script only once.</span></span>

6. <span data-ttu-id="da3be-200">Vedere hello [risolvere i problemi relativi a un oggetto che è non in sincronizzazione password](#one-object-is-not-synchronizing-passwords) sezione.</span><span class="sxs-lookup"><span data-stu-id="da3be-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="da3be-201">Problemi di connettività</span><span class="sxs-lookup"><span data-stu-id="da3be-201">Connectivity problems</span></span>

<span data-ttu-id="da3be-202">La connettività con Azure AD è presente?</span><span class="sxs-lookup"><span data-stu-id="da3be-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="da3be-203">Account hello sono richieste autorizzazioni tooread hello gli hash delle password in tutti i domini?</span><span class="sxs-lookup"><span data-stu-id="da3be-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="da3be-204">Se è stato installato utilizzando le impostazioni rapide Connect, le autorizzazioni di hello dovrebbero già essere corrette.</span><span class="sxs-lookup"><span data-stu-id="da3be-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="da3be-205">Se si utilizza l'installazione personalizzata, impostare manualmente le autorizzazioni di hello eseguendo hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="da3be-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="da3be-206">account di hello toofind utilizzato dal connettore di Active Directory hello, inizio **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="da3be-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="da3be-207">Andare troppo**connettori**e quindi cercare nella foresta di Active Directory locale hello risoluzione.</span><span class="sxs-lookup"><span data-stu-id="da3be-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="da3be-208">Selezionare il connettore hello e quindi fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="da3be-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="da3be-209">Andare troppo**connettersi foresta Directory tooActive**.</span><span class="sxs-lookup"><span data-stu-id="da3be-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Account usato da Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="da3be-211">Si noti username hello e dominio hello account hello in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="da3be-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="da3be-212">Avviare **Active Directory Users and Computers**, quindi verificare che account hello individuati in precedenza disponga delle autorizzazioni di seguire hello impostata nella radice di hello di tutti i domini della foresta:</span><span class="sxs-lookup"><span data-stu-id="da3be-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="da3be-213">Replica modifiche directory</span><span class="sxs-lookup"><span data-stu-id="da3be-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="da3be-214">Replica modifiche directory - Tutto</span><span class="sxs-lookup"><span data-stu-id="da3be-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="da3be-215">È hello controller di dominio raggiungibile da Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="da3be-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="da3be-216">Se il server di connessione hello è possibile connettersi tooall i controller di dominio, configurare **utilizzare solo i controller di dominio preferito**.</span><span class="sxs-lookup"><span data-stu-id="da3be-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Controller di dominio usato da Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="da3be-218">Tornare indietro troppo**Synchronization Service Manager** e **configurare partizione di Directory**.</span><span class="sxs-lookup"><span data-stu-id="da3be-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="da3be-219">Selezionare il dominio in **seleziona partizioni di directory**selezionare hello **utilizzare solo i controller di dominio preferito** casella di controllo e quindi fare clic su **configura**.</span><span class="sxs-lookup"><span data-stu-id="da3be-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="da3be-220">Nell'elenco di hello, immettere i controller di dominio hello Connetti devono utilizzare per la sincronizzazione delle password. Hello stesso elenco viene utilizzato per importare ed esportare anche.</span><span class="sxs-lookup"><span data-stu-id="da3be-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="da3be-221">Eseguire questi passaggi per tutti i domini.</span><span class="sxs-lookup"><span data-stu-id="da3be-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="da3be-222">Se uno script hello mostra che non è stato rilevato alcun heartbeat, è possibile eseguire script di hello in [attivare una sincronizzazione completa di tutte le password](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="da3be-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="da3be-223">Un oggetto non sincronizza le password: passaggi per la risoluzione manuale dei problemi</span><span class="sxs-lookup"><span data-stu-id="da3be-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="da3be-224">Esaminando hello lo stato di un oggetto, è possibile risolvere facilmente i problemi di sincronizzazione password.</span><span class="sxs-lookup"><span data-stu-id="da3be-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="da3be-225">In **Active Directory Users and Computers**, cercare hello utente e quindi verificare che hello **cambiamento obbligatorio password all'accesso successivo** casella di controllo è deselezionata.</span><span class="sxs-lookup"><span data-stu-id="da3be-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Password per la produttività di Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="da3be-227">Se è selezionata la casella di controllo hello, porre toosign utente hello in e modificare la password di hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="da3be-228">Le password temporanee non vengono sincronizzate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da3be-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="da3be-229">Se la password di hello corretto in Active Directory, seguire utente hello nel motore di sincronizzazione hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="da3be-230">Utente seguente hello tooAzure di Active Directory locale AD, consente di visualizzare se si verifica un errore descrittivo sull'oggetto hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="da3be-231">a.</span><span class="sxs-lookup"><span data-stu-id="da3be-231">a.</span></span> <span data-ttu-id="da3be-232">Avviare hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="da3be-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="da3be-233">b.</span><span class="sxs-lookup"><span data-stu-id="da3be-233">b.</span></span> <span data-ttu-id="da3be-234">Fare clic su **Connectors**(Connettori).</span><span class="sxs-lookup"><span data-stu-id="da3be-234">Click **Connectors**.</span></span>

    <span data-ttu-id="da3be-235">c.</span><span class="sxs-lookup"><span data-stu-id="da3be-235">c.</span></span> <span data-ttu-id="da3be-236">Seleziona hello **Active Directory Connector** utente hello in cui si trova.</span><span class="sxs-lookup"><span data-stu-id="da3be-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="da3be-237">d.</span><span class="sxs-lookup"><span data-stu-id="da3be-237">d.</span></span> <span data-ttu-id="da3be-238">Selezionare **Search Connector Space**(Cerca spazio connettore).</span><span class="sxs-lookup"><span data-stu-id="da3be-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="da3be-239">e.</span><span class="sxs-lookup"><span data-stu-id="da3be-239">e.</span></span> <span data-ttu-id="da3be-240">In hello **ambito** , quindi selezionare **DN o ancoraggio**, quindi immettere hello DN completo dell'utente hello risoluzione.</span><span class="sxs-lookup"><span data-stu-id="da3be-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Cercare l'utente nello spazio connettore con nome distinto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="da3be-242">f.</span><span class="sxs-lookup"><span data-stu-id="da3be-242">f.</span></span> <span data-ttu-id="da3be-243">Individuare hello utente che si sta cercando, quindi fare clic su **proprietà** toosee tutti gli attributi di hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="da3be-244">Se è presente nei risultati di ricerca hello utente hello, verificare il [le regole di filtro](active-directory-aadconnectsync-configure-filtering.md) e accertarsi di eseguire [applica e verificare le modifiche](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) per tooappear utente hello nella connessione.</span><span class="sxs-lookup"><span data-stu-id="da3be-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="da3be-245">g.</span><span class="sxs-lookup"><span data-stu-id="da3be-245">g.</span></span> <span data-ttu-id="da3be-246">Fare clic su dettagli di sincronizzazione password hello toosee dell'oggetto hello per hello settimana precedente, **Log**.</span><span class="sxs-lookup"><span data-stu-id="da3be-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Dettagli del log dell'oggetto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="da3be-248">Se il log di oggetto hello è vuoto, Azure AD Connect è stato Impossibile tooread hash della password hello da Active Directory.</span><span class="sxs-lookup"><span data-stu-id="da3be-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="da3be-249">Continuare la risoluzione dei problemi con [Errori di connettività](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="da3be-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="da3be-250">Se viene visualizzato un valore diverso da **successo**, fare riferimento a tabella toohello [log di sincronizzazione Password](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="da3be-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="da3be-251">h.</span><span class="sxs-lookup"><span data-stu-id="da3be-251">h.</span></span> <span data-ttu-id="da3be-252">Seleziona hello **derivazione** scheda e verificare che tale regola di almeno sincronizzazione hello **PasswordSync** colonna **True**.</span><span class="sxs-lookup"><span data-stu-id="da3be-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="da3be-253">Nella configurazione predefinita di hello, hello regola di sincronizzazione hello è denominato **In ingresso da AD – User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="da3be-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informazioni sulla derivazione relative a un utente](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="da3be-255">i.</span><span class="sxs-lookup"><span data-stu-id="da3be-255">i.</span></span> <span data-ttu-id="da3be-256">Fare clic su **proprietà oggetto Metaverse** toodisplay un elenco di attributi utente.</span><span class="sxs-lookup"><span data-stu-id="da3be-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Informazioni del metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="da3be-258">Verificare che non sia presente alcun attributo **cloudFiltered**.</span><span class="sxs-lookup"><span data-stu-id="da3be-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="da3be-259">Assicurarsi che gli attributi di dominio di hello (domainFQDN e domainNetBios) hanno valori previsti hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="da3be-260">j.</span><span class="sxs-lookup"><span data-stu-id="da3be-260">j.</span></span> <span data-ttu-id="da3be-261">Fare clic su hello **connettori** scheda. Verificare che sia visualizzato tooboth connettori Active Directory locale e Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da3be-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Informazioni del metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="da3be-263">k.</span><span class="sxs-lookup"><span data-stu-id="da3be-263">k.</span></span> <span data-ttu-id="da3be-264">Riga selezionare hello che rappresenta AD Azure, fare clic su **proprietà**, quindi fare clic su hello **derivazione** oggetto spazio connettore hello di scheda deve disporre di una regola in uscita in hello **PasswordSync** set di colonne troppo**True**.</span><span class="sxs-lookup"><span data-stu-id="da3be-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="da3be-265">Nella configurazione predefinita di hello, hello regola di sincronizzazione hello è denominato **Out tooAAD - aggiunta utente**.</span><span class="sxs-lookup"><span data-stu-id="da3be-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Finestra di dialogo Proprietà dell'oggetto spazio connettore](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="da3be-267">Log di sincronizzazione delle password</span><span class="sxs-lookup"><span data-stu-id="da3be-267">Password sync log</span></span>
<span data-ttu-id="da3be-268">Nella colonna Stato Hello può avere hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="da3be-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="da3be-269">Stato</span><span class="sxs-lookup"><span data-stu-id="da3be-269">Status</span></span> | <span data-ttu-id="da3be-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="da3be-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="da3be-271">Success</span><span class="sxs-lookup"><span data-stu-id="da3be-271">Success</span></span> |<span data-ttu-id="da3be-272">La password è stata sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="da3be-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="da3be-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="da3be-273">FilteredByTarget</span></span> |<span data-ttu-id="da3be-274">La password è troppo**cambiamento obbligatorio password all'accesso successivo**.</span><span class="sxs-lookup"><span data-stu-id="da3be-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="da3be-275">La password non è stata sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="da3be-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="da3be-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="da3be-276">NoTargetConnection</span></span> |<span data-ttu-id="da3be-277">Nessun oggetto nel metaverse hello o nello spazio connettore hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="da3be-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="da3be-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="da3be-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="da3be-279">Nessun oggetto trovato nello spazio connettore Active Directory locale di hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="da3be-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="da3be-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="da3be-281">oggetto Hello in hello spazio connettore Azure AD non è ancora stato esportato.</span><span class="sxs-lookup"><span data-stu-id="da3be-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="da3be-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="da3be-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="da3be-283">La voce di log è stata creata prima della compilazione 1.0.9125.0 e viene visualizzata nello stato precedente.</span><span class="sxs-lookup"><span data-stu-id="da3be-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="da3be-284">Errore</span><span class="sxs-lookup"><span data-stu-id="da3be-284">Error</span></span> |<span data-ttu-id="da3be-285">Il servizio ha restituito un errore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="da3be-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="da3be-286">Sconosciuto</span><span class="sxs-lookup"><span data-stu-id="da3be-286">Unknown</span></span> |<span data-ttu-id="da3be-287">Si è verificato un errore durante il tentativo di tooprocess un batch degli hash delle password.</span><span class="sxs-lookup"><span data-stu-id="da3be-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="da3be-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="da3be-288">MissingAttribute</span></span> |<span data-ttu-id="da3be-289">Gli attributi specifici (ad esempio hash Kerberos) richiesti da Azure AD Domain Services non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="da3be-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="da3be-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="da3be-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="da3be-291">Gli attributi specifici (ad esempio hash Kerberos) richiesti da Azure AD Domain Services non erano disponibili in precedenza.</span><span class="sxs-lookup"><span data-stu-id="da3be-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="da3be-292">Hash della password dell'utente un tentativo tooresynchronize hello viene eseguita.</span><span class="sxs-lookup"><span data-stu-id="da3be-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="da3be-293">Risoluzione dei problemi degli script toohelp</span><span class="sxs-lookup"><span data-stu-id="da3be-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="da3be-294">Ottenere lo stato di hello di impostazioni di sincronizzazione password</span><span class="sxs-lookup"><span data-stu-id="da3be-294">Get hello status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="da3be-295">Attivare una sincronizzazione completa di tutte le password</span><span class="sxs-lookup"><span data-stu-id="da3be-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="da3be-296">Eseguire questo script una sola volta.</span><span class="sxs-lookup"><span data-stu-id="da3be-296">Run this script only once.</span></span> <span data-ttu-id="da3be-297">Se è necessario toorun più di una volta, un altro elemento è il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="da3be-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="da3be-298">problema di hello tootroubleshoot, contattare il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da3be-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="da3be-299">È possibile attivare una sincronizzazione completa di tutte le password utilizzando hello lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="da3be-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="da3be-300">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da3be-300">Next steps</span></span>
* [<span data-ttu-id="da3be-301">Implementazione della sincronizzazione password con il servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="da3be-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="da3be-302">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="da3be-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="da3be-303">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="da3be-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
