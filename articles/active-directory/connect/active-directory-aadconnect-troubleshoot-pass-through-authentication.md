---
title: 'Azure AD Connect: Risolvere i problemi di autenticazione pass-through | Microsoft Docs'
description: Questo articolo viene descritto come tootroubleshoot l'autenticazione pass-through di Azure Active Directory (Azure AD).
services: active-directory
keywords: Risolvere i problemi di autenticazione pass-through di Azure AD Connect, installare Active Directory, componenti necessari per Azure AD, SSO, Single Sign-On
documentationcenter: 
author: swkrish
manager: femila
ms.assetid: 9f994aca-6088-40f5-b2cc-c753a4f41da7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: billmath
ms.openlocfilehash: 87130952f660762f91b0a34b05287603b565639f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-pass-through-authentication"></a>Risolvere i problemi di autenticazione pass-through di Azure Active Directory

Questo articolo consente di trovare informazioni utili per risolvere i problemi comuni relativi all'autenticazione pass-through di Azure AD.

>[!IMPORTANT]
>Se si devono affrontare utente problemi di accesso con autenticazione pass-through, non disabilitare la funzionalità hello o disinstallare gli agenti di autenticazione pass-through senza un toofall account amministratore globale solo cloud in. Informazioni su come [aggiungere un account amministratore globale di tipo solo cloud](../active-directory-users-create-azure-portal.md). L'esecuzione di questo passaggio è fondamentale ed evita di rimanere bloccati fuori dal tenant.

## <a name="general-issues"></a>Problemi generali

### <a name="check-status-of-hello-feature-and-authentication-agents"></a>Controllare lo stato delle funzionalità di hello e gli agenti di autenticazione

Assicurarsi che funzionalità di autenticazione pass-through hello è ancora **abilitato** sullo stato del tenant e hello degli agenti di autenticazione Mostra **Active**e non **inattivo**. È possibile controllare lo stato da passare toohello **Azure AD Connect** pannello nel hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com/).

![Interfaccia di amministrazione di Azure Active Directory - Pannello Azure AD Connect](./media/active-directory-aadconnect-pass-through-authentication/pta7.png)

![Interfaccia di amministrazione di Azure Active Directory - Pannello Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta11.png)

### <a name="user-facing-sign-in-error-messages"></a>Messaggi di errore visualizzati in fase di accesso

Se l'utente di hello è Impossibile toosign in utilizzando l'autenticazione pass-through, essi venga visualizzato uno dei hello gli errori rivolta all'utente di seguenti nella schermata di accesso hello Azure AD: 

|Errore|Description|Risoluzione
| --- | --- | ---
|AADSTS80001|Non è possibile tooconnect tooActive Directory|Verificare che l'agente server sono membri della foresta hello stesso Active Directory come utenti hello le cui password è necessario convalidare toobe e sono in grado di tooconnect tooActive Directory.  
|AADSTS8002|Si è verificato un timeout connessione tooActive Directory|Controllare che Active Directory sia disponibile e risponde toorequests dagli agenti hello di tooensure.
|AADSTS80004|nome utente di Hello passato toohello agente non è valido|Verificare l'utente hello tenta toosign con nome utente corretto hello.
|AADSTS80005|La convalida ha rilevato un errore WebException imprevedibile|Errore temporaneo. Ripetere la richiesta hello. Se continua a toofail, contattare il supporto tecnico Microsoft.
|AADSTS80007|Errore durante la comunicazione con Active Directory|Controllare i registri dell'agente di hello per ulteriori informazioni e verificare che Active Directory funzioni come previsto.

### <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Cause dell'errore di accesso nel centro di amministrazione di hello Azure Active Directory

Iniziare la risoluzione di problemi di accesso utente esaminando hello [report attività di accesso](../active-directory-reporting-activity-sign-ins.md) su hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com/).

![Interfaccia di amministrazione di Azure Active Directory - Report sugli accessi](./media/active-directory-aadconnect-pass-through-authentication/pta4.png)

Passare troppo**Azure Active Directory** -> **accessi** su hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com/) e fare clic su attività di accesso dell'utente specifico. Cercare hello **il codice di errore di accesso** campo. Eseguire il mapping di valore hello che causa dell'errore tooa di campo e la risoluzione tramite hello nella tabella seguente:

|Codice dell'errore di accesso|Motivo dell'errore di accesso|Risoluzione
| --- | --- | ---
| 50144 | La password di Active Directory dell'utente è scaduta. | Reimpostare la password dell'utente hello in Active Directory locale.
| 80001 | Non sono disponibili agenti di autenticazione. | Installare e registrare un agente di autenticazione.
| 80002 | Timeout della richiesta di convalida della password dell'agente di autenticazione. | Controllare se il servizio Active Directory sia raggiungibile da hello agente di autenticazione.
| 80003 | Risposta non valida ricevuta dall'agente di autenticazione. | Se il problema di hello è riproducibile in modo coerente tra più utenti, è possibile controllare la configurazione di Active Directory.
| 80004 | È stato usato un nome dell'entità utente (UPN) non corretto nella richiesta di accesso. | Chiedere hello utente toosign con nome utente corretto hello.
| 80005 | Agente di autenticazione: si è verificato un errore. | Errore temporaneo. Riprovare.
| 80007 | L'autenticazione dell'agente non è possibile tooconnect tooActive Directory. | Controllare se il servizio Active Directory sia raggiungibile da hello agente di autenticazione.
| 80010 | Password per l'autenticazione dell'agente non è possibile toodecrypt. | Se il problema di hello è riproducibile in modo coerente, installare e registrare un nuovo agente di autenticazione. E disinstallare hello corrente. 
| 80011 | Chiave di decrittografia non è possibile tooretrieve agente autenticazione. | Se il problema di hello è riproducibile in modo coerente, installare e registrare un nuovo agente di autenticazione. E disinstallare hello corrente.

## <a name="authentication-agent-installation-issues"></a>Problemi di installazione dell'agente di autenticazione

### <a name="an-unexpected-error-occurred"></a>Si è verificato un errore imprevisto

[Raccogliere i registri dell'agente](#collecting-pass-through-authentication-agent-logs) dal server di hello e contattare il supporto Microsoft per risolvere il problema.

## <a name="authentication-agent-registration-issues"></a>Problemi di registrazione dell'agente di autenticazione

### <a name="registration-of-hello-authentication-agent-failed-due-tooblocked-ports"></a>Registrazione di hello agente di autenticazione non riuscita a causa di porte tooblocked

Verificare in quali hello è stato installato l'agente di autenticazione server hello possa comunicare con il servizio di porte e gli URL elencate [qui](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="registration-of-hello-authentication-agent-failed-due-tootoken-or-account-authorization-errors"></a>Registrazione dell'agente di autenticazione hello non riuscita a causa di errori di autorizzazione tootoken o account

Assicurarsi di usare un account amministratore globale solo cloud per tutte le operazioni di installazione e registrazione dell'agente di autenticazione autonomo o di Azure AD Connect. Si verifica un problema noto con gli account di amministratore globale basate sull'autenticazione a più fattori, disattivare l'autenticazione a più fattori temporaneamente (solo operazioni hello toocomplete) come soluzione alternativa.

### <a name="an-unexpected-error-occurred"></a>Si è verificato un errore imprevisto

[Raccogliere i registri dell'agente](#collecting-pass-through-authentication-agent-logs) dal server di hello e contattare il supporto Microsoft per risolvere il problema.

## <a name="authentication-agent-uninstallation-issues"></a>Problemi di disinstallazione dell'agente di autenticazione

### <a name="warning-message-when-uninstalling-azure-ad-connect"></a>Messaggio di avviso quando si disinstalla Azure AD Connect

Se l'autenticazione pass-through abilitato per il tenant e si tenta di toouninstall Azure AD Connect, verrà visualizzato hello il seguente messaggio di avviso: "gli utenti non saranno tooAzure in grado di toosign-in Active Directory a meno che non si dispone di altri agenti di autenticazione pass-through installati su altri server."

Verificare che il programma di installazione sia [elevata disponibili](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-5-ensure-high-availability) prima di disinstallare Azure AD Connect tooavoid rilievo account utente.

## <a name="issues-with-enabling-hello-feature"></a>Problemi con l'abilitazione di funzionalità hello

### <a name="enabling-hello-feature-failed-because-there-were-no-authentication-agents-available"></a>Abilitare la funzionalità di hello non riuscita perché nessun agente di autenticazione sono disponibili

È necessario toohave tooenable agente autenticazione active almeno autenticazione pass-through per il tenant. È possibile installare sia un agente di autenticazione di Azure AD Connect sia un agente di autenticazione autonomo.

### <a name="enabling-hello-feature-failed-due-tooblocked-ports"></a>Abilitare la funzionalità di hello tooblocked porte non riuscita

Verificare che server hello in cui è installato Azure AD Connect possa comunicare con il servizio di porte e gli URL elencate [qui](active-directory-aadconnect-pass-through-authentication-quick-start.md#step-1-check-prerequisites).

### <a name="enabling-hello-feature-failed-due-tootoken-or-account-authorization-errors"></a>Abilitare la funzionalità di hello non è riuscita a causa di errori di autorizzazione tootoken o account

Assicurarsi di usare un account di amministratore globale cloud solo quando si abilita la funzionalità di hello. Si verifica un problema noto con l'autenticazione a più fattori (MFA)-abilitato l'account amministratore globale. disattivare l'autenticazione a più fattori temporaneamente (solo operazione hello toocomplete) come soluzione alternativa.

## <a name="exchange-activesync-configuration-issues"></a>Problemi di configurazione di Exchange ActiveSync

Si tratta di problemi comuni di hello quando si configura il supporto di Exchange ActiveSync per l'autenticazione pass-through.

### <a name="exchange-powershell-issue"></a>Problema relativo a PowerShell per Exchange

Se viene visualizzato hello "**Impossibile trovare un parametro che corrisponde a nome del parametro 'PerTenantSwitchToESTSEnabled'\.**" Errore durante l'esecuzione di hello `Set-OrganizationConfig` Exchange PowerShell command, contattare il supporto Microsoft.

### <a name="exchange-activesync-not-working"></a>Exchange ActiveSync non funziona

configurazione di Hello accetta alcuni effetto tootake tempo - hello periodo di tempo dipende dall'ambiente. Se la situazione hello persiste per molto tempo, contattare il supporto Microsoft.

## <a name="collecting-pass-through-authentication-agent-logs"></a>Raccolta dei registri dell'agente di autenticazione pass-through

In base al tipo di hello del problema, che è possibile, è necessario toolook in posizioni diverse per i registri dell'agente autenticazione pass-through.

### <a name="authentication-agent-event-logs"></a>Registri eventi dell'agente di autenticazione

Per errori correlati toohello agente di autenticazione, aprire l'applicazione Visualizzatore eventi nel server di hello hello e controllare le impostazioni di **applicazione e servizio Logs\Microsoft\AzureAdConnect\AuthenticationAgent\Admin**.

Per dettagliate analitica, abilitare il log di "Sessione" hello. Non vengono eseguiti con questo log abilitato durante le normali operazioni; hello agente di autenticazione usare solo per la risoluzione dei problemi. contenuto del log Hello è visibili solo dopo aver disabilitato il log di hello nuovamente.

### <a name="detailed-trace-logs"></a>Log di traccia dettagliati

tootroubleshoot utente errori di accesso, cercare i log di traccia a **%programdata%\Microsoft\Azure AD connettersi autenticazione Agent\Trace\\**. Questi log includono motivi perché un utente specifico Accedi non riuscito usando la funzionalità di autenticazione pass-through hello. Questi errori sono anche cause dell'errore di accesso mappato toohello mostrati nella precedente hello [tabella](#sign-in-failure-reasons-on-the-Azure-portal). Di seguito è riportato un esempio di voce di registro:

```
    AzureADConnectAuthenticationAgentService.exe Error: 0 : Passthrough Authentication request failed. RequestId: 'df63f4a4-68b9-44ae-8d81-6ad2d844d84e'. Reason: '1328'.
        ThreadId=5
        DateTime=xxxx-xx-xxTxx:xx:xx.xxxxxxZ
```

È possibile ottenere una descrizione dettagliata dell'errore hello ('1328' nel precedente esempio hello) aprendo il prompt hello e hello in esecuzione comando seguente (Nota: sostituire '1328' con numero di errore effettivo hello visualizzati nel log di):

`Net helpmsg 1328`

![Autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta3.png)

### <a name="domain-controller-logs"></a>Log del controller di dominio

Se è abilitata la registrazione di controllo, informazioni aggiuntive disponibili nei registri di protezione hello dei controller di dominio. Un modo semplice tooquery Accedi inviate dagli agenti di autenticazione pass-through è il seguente:

```
    <QueryList>
    <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ProcessName'] and (Data='C:\Program Files\Microsoft Azure AD Connect Authentication Agent\AzureADConnectAuthenticationAgentService.exe')]]</Select>
    </Query>
    </QueryList>
```

### <a name="performance-monitor-counters"></a>Contatori di Performance Monitor

Un altro modo toomonitor gli agenti di autenticazione è tootrack specifici Monitor contatori delle prestazioni in ogni server in cui è installato l'agente di autenticazione hello. Hello utilizzare seguenti contatori globali (**autenticazioni # PTA**, **#PTA Impossibile autenticazioni** e **autenticazioni #PTA**) e i contatori degli errori (**Errori di autenticazione # PTA**):

![Contatori di Performance Monitor per l'autenticazione pass-through](./media/active-directory-aadconnect-pass-through-authentication/pta12.png)

>[!IMPORTANT]
>L'autenticazione pass-through fornisce disponibilità elevata tramite più agenti di autenticazione, _senza_ il bilanciamento del carico. A seconda della configurazione, _non_ tutti gli agenti di autenticazione ricevono all'incirca un numero _uguale_ di richieste. È possibile che un agente di autenticazione specifico non riceva traffico del tutto.
