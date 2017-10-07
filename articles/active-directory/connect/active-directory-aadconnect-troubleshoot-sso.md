---
title: 'Azure AD Connect: risolvere i problemi relativi all''accesso Single Sign-On facile | Microsoft Docs'
description: Questo argomento viene descritto come tootroubleshoot Azure Active Directory trasparente Single Sign-On (SSO senza problemi per Azure AD).
services: active-directory
keywords: "che cos'è Azure AD Connect, installare Active Directory, componenti richiesti per Azure AD, SSO, Single Sign-On"
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
ms.openlocfilehash: f1c1c11522f22d5bc742c126fff483c5b06e1f06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-active-directory-seamless-single-sign-on"></a>Risolvere i problemi relativi all'accesso Single Sign-On facile di Azure Active Directory

Questo articolo consente di trovare informazioni utili per risolvere i problemi comuni relativi all'accesso Single Sign-On facile di Azure AD.

## <a name="known-issues"></a>Problemi noti

- Se si esegue la sincronizzazione di 30 o più foreste di Active Directory, non è possibile abilitare l'accesso SSO facile usando Azure AD Connect. In alternativa, è possibile [abilitare manualmente](#manual-reset-of-azure-ad-seamless-sso) funzionalità hello nel tenant.
- Aggiunta AD Azure service URL (https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net) toohello "area siti attendibili" hello "" Intranet locale invece di **blocca l'accesso degli utenti**.
- L'accesso SSO facile non funziona in modalità di esplorazione privata in Firefox e in Microsoft Edge, ma nemmeno in Internet Explorer quando la modalità di protezione avanzata è attivata.

>[!IMPORTANT]
>È recente eseguito il rollback il supporto per Edge tooinvestigate problemi segnalati.

## <a name="check-status-of-hello-feature"></a>Controllare lo stato della funzionalità hello

Verificare che tale caratteristica di SSO trasparente hello è ancora **abilitato** per il tenant. È possibile controllare lo stato da passare toohello **Azure AD Connect** pannello nel hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com/).

![Interfaccia di amministrazione di Azure Active Directory - Pannello Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="sign-in-failure-reasons-on-hello-azure-active-directory-admin-center"></a>Cause dell'errore di accesso nel centro di amministrazione di hello Azure Active Directory

Toostart un ottimo strumento utente problemi di accesso con SSO senza problemi di risoluzione dei problemi è toolook in hello [report attività di accesso](../active-directory-reporting-activity-sign-ins.md) su hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com/).

![Interfaccia di amministrazione di Azure Active Directory - Report sugli accessi](./media/active-directory-aadconnect-sso/sso9.png)

Passare troppo**Azure Active Directory** -> **accessi** su hello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com/) e fare clic su attività di accesso dell'utente specifico. Cercare hello **il codice di errore di accesso** campo. Eseguire il mapping di valore hello che causa dell'errore tooa di campo e la risoluzione tramite hello nella tabella seguente:

|Codice dell'errore di accesso|Motivo dell'errore di accesso|Risoluzione
| --- | --- | ---
| 81001 | Il ticket Kerberos dell'utente è troppo grande. | Ridurre l'appartenenza a gruppi dell'utente e riprovare.
| 81002 | Ticket Kerberos non è possibile toovalidate dell'utente. | Vedere l'[elenco di controllo per la risoluzione dei problemi](#troubleshooting-checklist).
| 81003 | Ticket Kerberos non è possibile toovalidate dell'utente. | Vedere l'[elenco di controllo per la risoluzione dei problemi](#troubleshooting-checklist).
| 81004 | Tentativo di autenticazione Kerberos non riuscito. | Vedere l'[elenco di controllo per la risoluzione dei problemi](#troubleshooting-checklist).
| 81008 | Ticket Kerberos non è possibile toovalidate dell'utente. | Vedere l'[elenco di controllo per la risoluzione dei problemi](#troubleshooting-checklist).
| 81009 | "Impossibile toovalidate Kerberos ticket utente. | Vedere l'[elenco di controllo per la risoluzione dei problemi](#troubleshooting-checklist).
| 81010 | SSO trasparente non riuscita perché il ticket Kerberos dell'utente hello è scaduto o non è valido. | L'utente deve toosign in da un dispositivo aggiunto al dominio all'interno della rete aziendale.
| 81011 | Oggetto utente non è possibile toofind in base alle informazioni nel ticket Kerberos dell'utente hello. | Utilizzare le informazioni sull'utente in Azure AD Azure AD Connect toosynchronize.
| 81012 | utente Hello tentativo toosign in tooAzure Active Directory è diverso dall'utente hello effettuato l'accesso al dispositivo hello. | Accedere da un altro dispositivo.
| 81013 | Oggetto utente non è possibile toofind in base alle informazioni nel ticket Kerberos dell'utente hello. |Utilizzare le informazioni sull'utente in Azure AD Azure AD Connect toosynchronize. 

## <a name="troubleshooting-checklist"></a>Elenco di controllo per la risoluzione dei problemi

Utilizzare hello seguente elenco di controllo tootroubleshoot SSO senza problemi:

- Verificare se funzionalità SSO trasparente hello è abilitata in Azure AD Connect. Se non è possibile abilitare la funzionalità hello (ad esempio, a causa di porta tooa bloccato), assicurarsi di disporre tutti hello [prerequisiti](active-directory-aadconnect-sso-quick-start.md#step-1-check-prerequisites) sul posto.
- Controllare se entrambi questi Azure AD URL (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) sono parte dell'area Intranet di hello utente.
- Assicurarsi di dispositivi aziendali hello sono unita in join toohello AD dominio.
- Verificare hello utente è connesso al dispositivo toohello utilizzando un account di dominio Active Directory.
- Verificare che hello dell'account utente da una foresta di Active Directory in cui è stato SSO senza problemi di.
- Verificare hello dispositivo è connesso in rete aziendale hello.
- Verificare che ora del dispositivo hello è sincronizzato con il tempo hello Active Directory e controller di dominio hello ed entro cinque minuti.
- Elenco esistente dei ticket Kerberos nel dispositivo hello utilizzando hello **klist** comando da un prompt dei comandi. Controllare se il ticket emesso per hello `AZUREADSSOACCT` sono presenti account del computer. I ticket Kerberos degli utenti sono in genere validi per 12 ore. È possibile che siano in uso impostazioni diverse in Active Directory.
- Eliminare i ticket Kerberos dal dispositivo hello utilizzando hello **klist purge** comando, quindi riprovare.
- toodetermine se sono presenti problemi di JavaScript, esaminare i registri della console hello del browser hello (in "Developer Tools").
- Hello revisione [Controller di dominio registra](#domain-controller-logs) anche.

### <a name="domain-controller-logs"></a>Log del controller di dominio

Se il controllo di esito positivo è abilitato sul Controller di dominio, quindi ogni volta che un utente accede utilizzando SSO trasparente sicurezza viene registrata una voce nel registro eventi di hello. È possibile trovare questi eventi di sicurezza con hello seguente query (cercare l'evento **4769** associata con l'account computer hello **AzureADSSOAcc$**):

```
    <QueryList>
      <Query Id="0" Path="Security">
    <Select Path="Security">*[EventData[Data[@Name='ServiceName'] and (Data='AZUREADSSOACC$')]]</Select>
      </Query>
    </QueryList>
```

## <a name="manual-reset-of-hello-feature"></a>Reimpostazione manuale della funzionalità hello

Se la risoluzione dei problemi non sono utili, è possibile reimpostare manualmente la funzionalità hello nel tenant di. Seguire questi passaggi nel server locale hello in cui si esegue Azure AD Connect:

### <a name="step-1-import-hello-seamless-sso-powershell-module"></a>Passaggio 1: Importare il modulo di PowerShell SSO trasparente hello

1. Innanzitutto, scaricare e installare hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Quindi scaricare e installare hello [modulo di Azure Active Directory a 64 bit per Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Passare toohello `%programfiles%\Microsoft Azure Active Directory Connect` cartella.
4. Modulo di PowerShell SSO trasparente hello importazione tramite questo comando: `Import-Module .\AzureADSSO.psd1`.

### <a name="step-2-get-hello-list-of-ad-forests-on-which-seamless-sso-has-been-enabled"></a>Passaggio 2: Ottenere l'elenco di hello delle foreste di Active Directory in cui è stato abilitato SSO trasparente

1. Eseguire PowerShell come amministratore. In PowerShell eseguire la chiamata a `New-AzureADSSOAuthenticationContext`. Quando richiesto, immettere le credenziali di amministratore globale del tenant.
2. Eseguire la chiamata a `Get-AzureADSSOStatus`. Questo comando fornisce il che elenco delle foreste di Active Directory (esaminare elenco domini"hello") hello in cui è stata abilitata la funzionalità.

### <a name="step-3-disable-seamless-sso-for-each-ad-forest-that-it-was-set-it-up-on"></a>Passaggio 3: disabilitare l'accesso SSO facile per ogni foresta di Active Directory in cui era impostato

1. Eseguire la chiamata a `$creds = Get-Credential`. Quando richiesto, immettere le credenziali di amministratore di dominio hello hello destinato foresta di Active Directory.
2. Eseguire la chiamata a `Disable-AzureADSSOForest -OnPremCredentials $creds`. Questo comando rimuove hello `AZUREADSSOACCT` account computer da hello locale Controller di dominio per questa foresta di Active Directory specifica.
3. Ripetere hello passaggi per ogni foresta di Active Directory che hai configurato la funzionalità hello in precedenti.

### <a name="step-4-enable-seamless-sso-for-each-ad-forest"></a>Passaggio 4: abilitare l'accesso SSO facile per ogni foresta di Active Directory

1. Eseguire la chiamata a `Enable-AzureADSSOForest`. Quando richiesto, immettere le credenziali di amministratore di dominio hello hello destinato foresta di Active Directory.
2. Ripetere i passaggi per ogni foresta di Active Directory che si vuole tooset funzionalità hello nei precedenti hello.

### <a name="step-5-enable-hello-feature-on-your-tenant"></a>Passaggio 5. Abilitare la funzionalità di hello nel tenant di

Chiamare `Enable-AzureADSSO` e digitare "true" in hello `Enable: ` prompt tooturn funzionalità hello nel tenant.
