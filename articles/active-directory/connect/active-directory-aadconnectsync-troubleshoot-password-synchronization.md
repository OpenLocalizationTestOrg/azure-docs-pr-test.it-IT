---
title: Risolvere i problemi di sincronizzazione della password con il servizio di sincronizzazione Azure AD Connect | Microsoft Docs
description: Questo articolo contiene informazioni sulla risoluzione dei problemi di sincronizzazione delle password.
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
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="4c636-103">Risolvere i problemi di sincronizzazione della password con il servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4c636-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="4c636-104">In questo argomento viene descritta la procedura per risolvere i problemi di sincronizzazione della password.</span><span class="sxs-lookup"><span data-stu-id="4c636-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="4c636-105">Se le password non vengono sincronizzate come previsto, il problema può riguardare un subset di utenti o tutti gli utenti.</span><span class="sxs-lookup"><span data-stu-id="4c636-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="4c636-106">Per la distribuzione di Azure Active Directory (Azure AD) Connect versione 1.1.524.0 o successiva è ora disponibile un cmdlet di diagnostica che è possibile usare per risolvere i problemi di sincronizzazione delle password:</span><span class="sxs-lookup"><span data-stu-id="4c636-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="4c636-107">Se si verifica un problema per cui nessuna password viene sincronizzata, vedere la sezione [Nessuna password viene sincronizzata: risolvere i problemi tramite il cmdlet di diagnostica](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="4c636-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="4c636-108">Se si verifica un problema relativo a singoli oggetti, vedere la sezione [Un oggetto non sincronizza le password: risolvere i problemi tramite il cmdlet di diagnostica](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="4c636-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="4c636-109">Per le versioni precedenti della distribuzione di Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="4c636-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="4c636-110">Se si verifica un problema per cui nessuna password viene sincronizzata, vedere la sezione [Nessuna password viene sincronizzata: passaggi per la risoluzione manuale dei problemi](#no-passwords-are-synchronized-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="4c636-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="4c636-111">Se si verifica un problema relativo a singoli oggetti, vedere la sezione [Un oggetto non sincronizza le password: passaggi per la risoluzione manuale dei problemi](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="4c636-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="4c636-112">Nessuna password viene sincronizzata: risolvere i problemi tramite il cmdlet di diagnostica</span><span class="sxs-lookup"><span data-stu-id="4c636-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="4c636-113">Per stabilire il motivo per cui nessuna password viene sincronizzata, è possibile usare il cmdlet `Invoke-ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4c636-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="4c636-114">Il cmdlet `Invoke-ADSyncDiagnostics` è disponibile solo per Azure AD Connect versione 1.1.524.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4c636-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="4c636-115">Eseguire il cmdlet di diagnostica</span><span class="sxs-lookup"><span data-stu-id="4c636-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="4c636-116">Per risolvere i problemi per cui nessuna password viene sincronizzata:</span><span class="sxs-lookup"><span data-stu-id="4c636-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="4c636-117">Aprire una nuova sessione di Windows PowerShell nel server di Azure AD Connect con l'opzione **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="4c636-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="4c636-118">Eseguire `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="4c636-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="4c636-119">Eseguire `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4c636-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="4c636-120">Eseguire `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="4c636-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="4c636-121">Comprendere i risultati del cmdlet</span><span class="sxs-lookup"><span data-stu-id="4c636-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="4c636-122">Il cmdlet di diagnostica esegue i controlli seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c636-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="4c636-123">Verifica che la funzionalità di sincronizzazione delle password sia abilitata per il tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c636-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="4c636-124">Verifica che il server di Azure AD Connect non sia in modalità di gestione temporanea.</span><span class="sxs-lookup"><span data-stu-id="4c636-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="4c636-125">Per ogni istanza locale esistente di Active Directory Connector, corrispondente a una foresta di Active Directory esistente:</span><span class="sxs-lookup"><span data-stu-id="4c636-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="4c636-126">Verifica che la funzionalità di sincronizzazione delle password sia abilitata.</span><span class="sxs-lookup"><span data-stu-id="4c636-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="4c636-127">Cerca gli eventi heartbeat di sincronizzazione delle password nei log eventi delle applicazioni di Windows.</span><span class="sxs-lookup"><span data-stu-id="4c636-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="4c636-128">Per ogni dominio di Active Directory nell'istanza locale di Active Directory Connector:</span><span class="sxs-lookup"><span data-stu-id="4c636-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="4c636-129">Verifica che il dominio sia raggiungibile dal server di Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="4c636-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="4c636-130">Verifica che gli account di Active Directory Domain Services usati dall'istanza locale di Active Directory Connector abbiano il nome utente e la password corretti e le autorizzazioni necessarie per la sincronizzazione delle password.</span><span class="sxs-lookup"><span data-stu-id="4c636-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="4c636-131">Il diagramma seguente illustra i risultati del cmdlet per una topologia di Active Directory locale a dominio singolo:</span><span class="sxs-lookup"><span data-stu-id="4c636-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Output di diagnostica per la sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="4c636-133">La parte restante di questa sezione descrive i risultati specifici restituiti dal cmdlet e i problemi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="4c636-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="4c636-134">La funzionalità di sincronizzazione delle password non è abilitata</span><span class="sxs-lookup"><span data-stu-id="4c636-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="4c636-135">Se la sincronizzazione delle password non è stata abilitata tramite la procedura guidata di Azure AD Connect, viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![La sincronizzazione delle password non è abilitata](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="4c636-137">Il server di Azure AD Connect è in modalità di gestione temporanea</span><span class="sxs-lookup"><span data-stu-id="4c636-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="4c636-138">Se il server di Azure AD Connect è in modalità di gestione temporanea, la sincronizzazione delle password è temporaneamente disabilitata e viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![Il server di Azure AD Connect è in modalità di gestione temporanea](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="4c636-140">Eventi heartbeat di mancata sincronizzazione delle password</span><span class="sxs-lookup"><span data-stu-id="4c636-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="4c636-141">Ogni istanza locale di Active Directory Connector ha uno specifico canale di sincronizzazione delle password.</span><span class="sxs-lookup"><span data-stu-id="4c636-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="4c636-142">Quando il canale di sincronizzazione delle password è attivo e non vi sono modifiche di password da sincronizzare, nel log eventi delle applicazioni di Windows viene generato un evento heartbeat (EventId 654) ogni 30 minuti.</span><span class="sxs-lookup"><span data-stu-id="4c636-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="4c636-143">Per ogni istanza locale di Active Directory Connector, il cmdlet cerca gli eventi heartbeat corrispondenti che si sono verificati nelle ultime tre ore.</span><span class="sxs-lookup"><span data-stu-id="4c636-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="4c636-144">Se la ricerca ha esito negativo, viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-144">If no heartbeat event is found, the following error is returned:</span></span>

![Evento heartbeat di mancata sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="4c636-146">L'account di Active Directory Domain Services non ha le autorizzazioni corrette</span><span class="sxs-lookup"><span data-stu-id="4c636-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="4c636-147">Se l'account di Active Directory Domain Services usato dall'istanza locale di Active Directory Connector per sincronizzare gli hash delle password non ha le autorizzazioni appropriate, viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Credenziali non corrette](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="4c636-149">La password o il nome utente dell'account di Active Directory Domain Services non è corretto</span><span class="sxs-lookup"><span data-stu-id="4c636-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="4c636-150">Se l'account di Active Directory Domain Services usato dall'istanza locale di Active Directory Connector per sincronizzare gli hash delle password ha una password o un nome utente non corretto, viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Credenziali non corrette](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="4c636-152">Un oggetto non sincronizza le password: risolvere i problemi tramite il cmdlet di diagnostica</span><span class="sxs-lookup"><span data-stu-id="4c636-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="4c636-153">Per stabilire il motivo per cui un oggetto non sincronizza le password è possibile usare il cmdlet `Invoke-ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4c636-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="4c636-154">Il cmdlet `Invoke-ADSyncDiagnostics` è disponibile solo per Azure AD Connect versione 1.1.524.0 o successiva.</span><span class="sxs-lookup"><span data-stu-id="4c636-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="4c636-155">Eseguire il cmdlet di diagnostica</span><span class="sxs-lookup"><span data-stu-id="4c636-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="4c636-156">Per risolvere i problemi per cui nessuna password viene sincronizzata:</span><span class="sxs-lookup"><span data-stu-id="4c636-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="4c636-157">Aprire una nuova sessione di Windows PowerShell nel server di Azure AD Connect con l'opzione **Esegui come amministratore**.</span><span class="sxs-lookup"><span data-stu-id="4c636-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="4c636-158">Eseguire `Set-ExecutionPolicy RemoteSigned` o `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="4c636-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="4c636-159">Eseguire `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="4c636-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="4c636-160">Eseguire il cmdlet seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="4c636-161">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="4c636-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="4c636-162">Comprendere i risultati del cmdlet</span><span class="sxs-lookup"><span data-stu-id="4c636-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="4c636-163">Il cmdlet di diagnostica esegue i controlli seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c636-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="4c636-164">Esamina lo stato dell'oggetto Active Directory nello spazio di Active Directory Connector, nel metaverse e nello spazio di Azure AD Connector.</span><span class="sxs-lookup"><span data-stu-id="4c636-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="4c636-165">Verifica che siano definite regole di sincronizzazione con la sincronizzazione delle password abilitata e applicata all'oggetto Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c636-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="4c636-166">Prova a recuperare e visualizzare i risultati dell'ultimo tentativo di sincronizzazione della password per l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="4c636-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="4c636-167">Il diagramma seguente illustra i risultati del cmdlet durante la risoluzione dei problemi di sincronizzazione delle password per un singolo oggetto:</span><span class="sxs-lookup"><span data-stu-id="4c636-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Output di diagnostica per la sincronizzazione delle password: singolo oggetto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="4c636-169">La parte restante di questa sezione descrive i risultati specifici restituiti dal cmdlet e i problemi corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="4c636-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="4c636-170">L'oggetto Active Directory non viene esportato in Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c636-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="4c636-171">La sincronizzazione delle password per questo account di Active Directory locale non riesce perché non è presente alcun oggetto corrispondente nel tenant di Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c636-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="4c636-172">Viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-172">The following error is returned:</span></span>

![Oggetto Azure AD mancante](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="4c636-174">L'utente ha una password temporanea</span><span class="sxs-lookup"><span data-stu-id="4c636-174">User has a temporary password</span></span>
<span data-ttu-id="4c636-175">Azure AD Connect non supporta attualmente la sincronizzazione delle password temporanee con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c636-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="4c636-176">Una password viene considerata temporanea se l'opzione **Cambiamento obbligatorio password all'accesso successivo** è impostata per l'utente di Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="4c636-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="4c636-177">Viene restituito l'errore seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-177">The following error is returned:</span></span>

![Password temporanea non esportata](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="4c636-179">I risultati dell'ultimo tentativo di sincronizzare la password non sono disponibili</span><span class="sxs-lookup"><span data-stu-id="4c636-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="4c636-180">Per impostazione predefinita, Azure AD Connect archivia i risultati dei tentativi di sincronizzazione delle password per sette giorni.</span><span class="sxs-lookup"><span data-stu-id="4c636-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="4c636-181">Se per l'oggetto Active Directory selezionato non sono disponibili risultati, viene restituito l'avviso seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Output di diagnostica per un singolo oggetto: cronologia di mancata sincronizzazione delle password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="4c636-183">Nessuna password viene sincronizzata: passaggi per la risoluzione manuale dei problemi</span><span class="sxs-lookup"><span data-stu-id="4c636-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="4c636-184">Per stabilire il motivo per cui nessuna password viene sincronizzata, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="4c636-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="4c636-185">Il server di connessione è in [modalità di gestione temporanea](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="4c636-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="4c636-186">Un server in modalità di gestione temporanea non sincronizza le password.</span><span class="sxs-lookup"><span data-stu-id="4c636-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="4c636-187">Eseguire lo script nella sezione [Ottenere lo stato delle impostazioni di sincronizzazione password](#get-the-status-of-password-sync-settings).</span><span class="sxs-lookup"><span data-stu-id="4c636-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="4c636-188">Fornisce una panoramica della configurazione della sincronizzazione password.</span><span class="sxs-lookup"><span data-stu-id="4c636-188">It gives you an overview of the password sync configuration.</span></span>  

    ![Output dello script di PowerShell dalle impostazioni di sincronizzazione password](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="4c636-190">Se la funzionalità non è abilitata in Azure AD o se lo stato del canale di sincronizzazione non è abilitato, eseguire l'Installazione guidata di Connect.</span><span class="sxs-lookup"><span data-stu-id="4c636-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="4c636-191">Selezionare **Personalizzazione delle opzioni di sincronizzazione** e deselezionare l'opzione di sincronizzazione delle password. Questa modifica disabilita temporaneamente la funzionalità.</span><span class="sxs-lookup"><span data-stu-id="4c636-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="4c636-192">Eseguire quindi di nuovo la procedura guidata e riabilitare la sincronizzazione password. Eseguire di nuovo lo script per verificare che la configurazione sia corretta.</span><span class="sxs-lookup"><span data-stu-id="4c636-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="4c636-193">Esaminare il log eventi per cercare eventuali errori.</span><span class="sxs-lookup"><span data-stu-id="4c636-193">Look in the event log for errors.</span></span> <span data-ttu-id="4c636-194">Cercare gli eventi seguenti che potrebbero indicare un problema:</span><span class="sxs-lookup"><span data-stu-id="4c636-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="4c636-195">Origine: ID "Sincronizzazione della directory": 0, 611, 652, 655 Se vengono visualizzati eventi di questo tipo, c'è un problema di connettività.</span><span class="sxs-lookup"><span data-stu-id="4c636-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="4c636-196">Il messaggio del log eventi contiene informazioni relative alla foresta in cui è presente un problema.</span><span class="sxs-lookup"><span data-stu-id="4c636-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="4c636-197">Per altre informazioni, vedere [Problemi di connettività](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="4c636-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="4c636-198">Se non viene visualizzato alcun heartbeat o non si sono trovate altre soluzioni al problema, eseguire lo script riportato in [Attivare una sincronizzazione completa di tutte le password](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="4c636-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="4c636-199">Eseguire lo script una sola volta.</span><span class="sxs-lookup"><span data-stu-id="4c636-199">Run the script only once.</span></span>

6. <span data-ttu-id="4c636-200">Vedere la sezione [Risolvere i problemi relativi a un oggetto che non sincronizza le password](#one-object-is-not-synchronizing-passwords).</span><span class="sxs-lookup"><span data-stu-id="4c636-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="4c636-201">Problemi di connettività</span><span class="sxs-lookup"><span data-stu-id="4c636-201">Connectivity problems</span></span>

<span data-ttu-id="4c636-202">La connettività con Azure AD è presente?</span><span class="sxs-lookup"><span data-stu-id="4c636-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="4c636-203">L'account dispone delle autorizzazioni necessarie per leggere gli hash delle password in tutti i domini?</span><span class="sxs-lookup"><span data-stu-id="4c636-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="4c636-204">Se si è installato Connect usando le impostazioni rapide, le autorizzazioni dovrebbero già essere corrette.</span><span class="sxs-lookup"><span data-stu-id="4c636-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="4c636-205">Se invece si è usata l'installazione personalizzata, impostare manualmente le autorizzazioni eseguendo queste le operazioni:</span><span class="sxs-lookup"><span data-stu-id="4c636-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="4c636-206">Per trovare l'account usato dall'istanza di Active Directory Connector, avviare **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="4c636-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="4c636-207">Passare a **Connettori** e cercare la foresta di Active Directory locale per cui risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="4c636-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="4c636-208">Selezionare il connettore e quindi fare clic su **Proprietà**.</span><span class="sxs-lookup"><span data-stu-id="4c636-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="4c636-209">Passare a **Connetti a Foresta Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="4c636-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Account usato da Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="4c636-211">Prendere nota del nome utente e del dominio in cui si trova l'account.</span><span class="sxs-lookup"><span data-stu-id="4c636-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="4c636-212">Avviare **Utenti e computer di Active Directory** e verificare che l'account trovato in precedenza disponga delle autorizzazioni seguenti impostate nella radice di tutti i domini della foresta:</span><span class="sxs-lookup"><span data-stu-id="4c636-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="4c636-213">Replica modifiche directory</span><span class="sxs-lookup"><span data-stu-id="4c636-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="4c636-214">Replica modifiche directory - Tutto</span><span class="sxs-lookup"><span data-stu-id="4c636-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="4c636-215">I controller di dominio sono raggiungibili da Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="4c636-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="4c636-216">Se il server Connect non riesce a connettersi a tutti i controller di dominio, configurare **Only use preferred domain controller** (Usare solo controller di dominio preferito).</span><span class="sxs-lookup"><span data-stu-id="4c636-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Controller di dominio usato da Active Directory Connector](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="4c636-218">Tornare a **Synchronization Service Manager** e **Configure Directory Partition** (Configurare la partizione della directory).</span><span class="sxs-lookup"><span data-stu-id="4c636-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="4c636-219">Selezionare il dominio in **Select directory partitions** (Selezionare le partizioni della directory), selezionare la casella di controllo **Only use preferred domain controller** (Usare solo controller di dominio preferito) e quindi fare clic su **Configura**.</span><span class="sxs-lookup"><span data-stu-id="4c636-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="4c636-220">Nell'elenco immettere i controller di dominio che Connect deve usare per la sincronizzazione delle password. Lo stesso elenco viene usato anche per importare ed esportare.</span><span class="sxs-lookup"><span data-stu-id="4c636-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="4c636-221">Eseguire questi passaggi per tutti i domini.</span><span class="sxs-lookup"><span data-stu-id="4c636-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="4c636-222">Se lo script mostra che non sono stati generati heartbeat, eseguire lo script riportato in [Attivare una sincronizzazione completa di tutte le password](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="4c636-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="4c636-223">Un oggetto non sincronizza le password: passaggi per la risoluzione manuale dei problemi</span><span class="sxs-lookup"><span data-stu-id="4c636-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="4c636-224">È possibile risolvere facilmente i problemi di sincronizzazione password esaminando lo stato di un oggetto.</span><span class="sxs-lookup"><span data-stu-id="4c636-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="4c636-225">In **Utenti e computer di Active Directory** cercare l'utente e verificare che la casella di controllo **Cambiamento obbligatorio password all'accesso successivo** sia deselezionata.</span><span class="sxs-lookup"><span data-stu-id="4c636-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Password per la produttività di Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="4c636-227">Se la casella di controllo è selezionata, chiedere all'utente di accedere e modificare la password.</span><span class="sxs-lookup"><span data-stu-id="4c636-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="4c636-228">Le password temporanee non vengono sincronizzate con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4c636-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="4c636-229">Se in Active Directory la password sembra corretta, seguire l'utente nel motore di sincronizzazione.</span><span class="sxs-lookup"><span data-stu-id="4c636-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="4c636-230">Seguendo l'utente da Active Directory locale ad Azure AD, è possibile verificare se viene generato un errore descrittivo per l'oggetto.</span><span class="sxs-lookup"><span data-stu-id="4c636-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="4c636-231">a.</span><span class="sxs-lookup"><span data-stu-id="4c636-231">a.</span></span> <span data-ttu-id="4c636-232">Avviare [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="4c636-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="4c636-233">b.</span><span class="sxs-lookup"><span data-stu-id="4c636-233">b.</span></span> <span data-ttu-id="4c636-234">Fare clic su **Connectors**(Connettori).</span><span class="sxs-lookup"><span data-stu-id="4c636-234">Click **Connectors**.</span></span>

    <span data-ttu-id="4c636-235">c.</span><span class="sxs-lookup"><span data-stu-id="4c636-235">c.</span></span> <span data-ttu-id="4c636-236">Selezionare l'istanza di **Active Directory Connector** in cui si trova l'utente.</span><span class="sxs-lookup"><span data-stu-id="4c636-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="4c636-237">d.</span><span class="sxs-lookup"><span data-stu-id="4c636-237">d.</span></span> <span data-ttu-id="4c636-238">Selezionare **Search Connector Space**(Cerca spazio connettore).</span><span class="sxs-lookup"><span data-stu-id="4c636-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="4c636-239">e.</span><span class="sxs-lookup"><span data-stu-id="4c636-239">e.</span></span> <span data-ttu-id="4c636-240">Nella casella **Ambito** selezionare **DN or Anchor** (DN o ancoraggio) e quindi immettere il nome distinto completo dell'utente per il quale si devono risolvere i problemi.</span><span class="sxs-lookup"><span data-stu-id="4c636-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Cercare l'utente nello spazio connettore con nome distinto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="4c636-242">f.</span><span class="sxs-lookup"><span data-stu-id="4c636-242">f.</span></span> <span data-ttu-id="4c636-243">Trovare l'utente e fare clic su **Proprietà** per visualizzare tutti gli attributi.</span><span class="sxs-lookup"><span data-stu-id="4c636-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="4c636-244">Se l'utente non è incluso nei risultati della ricerca, verificare le [regole di filtro](active-directory-aadconnectsync-configure-filtering.md) e accertarsi di seguire le istruzioni in [Applicare e verificare le modifiche](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) per visualizzare l'utente in Connect.</span><span class="sxs-lookup"><span data-stu-id="4c636-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="4c636-245">g.</span><span class="sxs-lookup"><span data-stu-id="4c636-245">g.</span></span> <span data-ttu-id="4c636-246">Per visualizzare i dettagli della sincronizzazione della password dell'oggetto per la settimana precedente, fare clic su **Log**.</span><span class="sxs-lookup"><span data-stu-id="4c636-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Dettagli del log dell'oggetto](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="4c636-248">Se il log dell'oggetto è vuoto, Azure AD Connect non è stato in grado di leggere l'hash della password da Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4c636-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="4c636-249">Continuare la risoluzione dei problemi con [Errori di connettività](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="4c636-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="4c636-250">Se viene visualizzato un valore diverso da **success**, fare riferimento alla tabella [Log di sincronizzazione delle password](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="4c636-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="4c636-251">h.</span><span class="sxs-lookup"><span data-stu-id="4c636-251">h.</span></span> <span data-ttu-id="4c636-252">Selezionare la scheda **Lineage** (Derivazione) e verificare che almeno una regola di sincronizzazione nella colonna **PasswordSync** (Sincronizzazione password) sia impostata su **True**.</span><span class="sxs-lookup"><span data-stu-id="4c636-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="4c636-253">Nella configurazione predefinita il nome della regola di sincronizzazione è **In from AD - User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="4c636-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Informazioni sulla derivazione relative a un utente](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="4c636-255">i.</span><span class="sxs-lookup"><span data-stu-id="4c636-255">i.</span></span> <span data-ttu-id="4c636-256">Fare clic su **Metaverse Object Properties** (Proprietà dell'oggetto Metaverse) per visualizzare un elenco di attributi utente.</span><span class="sxs-lookup"><span data-stu-id="4c636-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Informazioni del metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="4c636-258">Verificare che non sia presente alcun attributo **cloudFiltered**.</span><span class="sxs-lookup"><span data-stu-id="4c636-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="4c636-259">Assicurarsi che gli attributi di dominio (domainFQDN e domainNetBios) abbiano i valori previsti.</span><span class="sxs-lookup"><span data-stu-id="4c636-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="4c636-260">j.</span><span class="sxs-lookup"><span data-stu-id="4c636-260">j.</span></span> <span data-ttu-id="4c636-261">Fare clic sulla scheda **Connettori**. Assicurarsi che i connettori per Active Directory locale e Azure AD siano visualizzati.</span><span class="sxs-lookup"><span data-stu-id="4c636-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Informazioni del metaverse](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="4c636-263">k.</span><span class="sxs-lookup"><span data-stu-id="4c636-263">k.</span></span> <span data-ttu-id="4c636-264">Selezionare la riga che rappresenta Azure AD, fare clic su **Proprietà** e quindi sulla scheda **Lineage** (Derivazione). L'oggetto spazio connettore deve avere una regola in uscita con la colonna **PasswordSync** (Sincronizzazione password) impostata su **True**.</span><span class="sxs-lookup"><span data-stu-id="4c636-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="4c636-265">Nella configurazione predefinita il nome della regola di sincronizzazione è **Out to AAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="4c636-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Finestra di dialogo Proprietà dell'oggetto spazio connettore](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="4c636-267">Log di sincronizzazione delle password</span><span class="sxs-lookup"><span data-stu-id="4c636-267">Password sync log</span></span>
<span data-ttu-id="4c636-268">I valori possibili per la colonna dello stato sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4c636-268">The status column can have the following values:</span></span>

| <span data-ttu-id="4c636-269">Stato</span><span class="sxs-lookup"><span data-stu-id="4c636-269">Status</span></span> | <span data-ttu-id="4c636-270">Descrizione</span><span class="sxs-lookup"><span data-stu-id="4c636-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4c636-271">Success</span><span class="sxs-lookup"><span data-stu-id="4c636-271">Success</span></span> |<span data-ttu-id="4c636-272">La password è stata sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="4c636-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="4c636-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="4c636-273">FilteredByTarget</span></span> |<span data-ttu-id="4c636-274">La password è impostata su **Richiedi modifica della password all'accesso successivo**.</span><span class="sxs-lookup"><span data-stu-id="4c636-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="4c636-275">La password non è stata sincronizzata.</span><span class="sxs-lookup"><span data-stu-id="4c636-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="4c636-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="4c636-276">NoTargetConnection</span></span> |<span data-ttu-id="4c636-277">Nessun oggetto in metaverse o nello spazio connettore di Azure AD</span><span class="sxs-lookup"><span data-stu-id="4c636-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="4c636-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="4c636-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="4c636-279">Nessun oggetto trovato nello spazio connettore di Active Directory locale.</span><span class="sxs-lookup"><span data-stu-id="4c636-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="4c636-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="4c636-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="4c636-281">L'oggetto nello spazio connettore di Azure AD non è stato ancora esportato.</span><span class="sxs-lookup"><span data-stu-id="4c636-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="4c636-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="4c636-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="4c636-283">La voce di log è stata creata prima della compilazione 1.0.9125.0 e viene visualizzata nello stato precedente.</span><span class="sxs-lookup"><span data-stu-id="4c636-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="4c636-284">Errore</span><span class="sxs-lookup"><span data-stu-id="4c636-284">Error</span></span> |<span data-ttu-id="4c636-285">Il servizio ha restituito un errore sconosciuto.</span><span class="sxs-lookup"><span data-stu-id="4c636-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="4c636-286">Sconosciuto</span><span class="sxs-lookup"><span data-stu-id="4c636-286">Unknown</span></span> |<span data-ttu-id="4c636-287">Si è verificato un errore durante il tentativo di elaborare un batch di hash delle password.</span><span class="sxs-lookup"><span data-stu-id="4c636-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="4c636-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="4c636-288">MissingAttribute</span></span> |<span data-ttu-id="4c636-289">Gli attributi specifici (ad esempio hash Kerberos) richiesti da Azure AD Domain Services non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="4c636-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="4c636-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="4c636-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="4c636-291">Gli attributi specifici (ad esempio hash Kerberos) richiesti da Azure AD Domain Services non erano disponibili in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4c636-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="4c636-292">Viene effettuato un tentativo di risincronizzare l'hash della password dell'utente.</span><span class="sxs-lookup"><span data-stu-id="4c636-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="4c636-293">Script per facilitare la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="4c636-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="4c636-294">Ottenere lo stato delle impostazioni di sincronizzazione password</span><span class="sxs-lookup"><span data-stu-id="4c636-294">Get the status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="4c636-295">Attivare una sincronizzazione completa di tutte le password</span><span class="sxs-lookup"><span data-stu-id="4c636-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="4c636-296">Eseguire questo script una sola volta.</span><span class="sxs-lookup"><span data-stu-id="4c636-296">Run this script only once.</span></span> <span data-ttu-id="4c636-297">Se è necessario eseguirlo più volte, il problema è dovuto a un'altra causa.</span><span class="sxs-lookup"><span data-stu-id="4c636-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="4c636-298">Per risolverlo, contattare il supporto tecnico Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4c636-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="4c636-299">È possibile attivare una sincronizzazione completa di tutte le password usando lo script seguente:</span><span class="sxs-lookup"><span data-stu-id="4c636-299">You can trigger a full sync of all passwords by using the following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4c636-300">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4c636-300">Next steps</span></span>
* [<span data-ttu-id="4c636-301">Implementazione della sincronizzazione password con il servizio di sincronizzazione Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="4c636-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="4c636-302">Servizio di sincronizzazione Azure AD Connect: Comprendere e personalizzare la sincronizzazione</span><span class="sxs-lookup"><span data-stu-id="4c636-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4c636-303">Integrazione delle identità locali con Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4c636-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
