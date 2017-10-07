---
title: 'Azure AD Connect: domande frequenti sull''accesso Single Sign-On facile | Microsoft Docs'
description: Le risposte toofrequently domande frequenti su Azure Active Directory trasparente Single Sign-On.
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
ms.date: 08/02/2017
ms.author: billmath
ms.openlocfilehash: e91e7950670633c08c180ece873f7451fa19eef8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-frequently-asked-questions"></a>Accesso Single Sign-On facile di Azure Active Directory: domande frequenti

Questo articolo risponde ad alcune domande frequenti relative all'accesso Single Sign-On facile (SSO facile) di Azure Active Directory. Visitare questa pagina regolarmente per nuovi contenuti.

>[!IMPORTANT]
>caratteristica di SSO trasparente Hello è attualmente in anteprima.

## <a name="what-sign-in-methods-do-seamless-sso-work-with"></a>Con quali metodi di accesso funziona l'accesso SSO facile?

SSO senza problemi può essere combinato con entrambi hello [la sincronizzazione dell'Hash Password](active-directory-aadconnectsync-implement-password-synchronization.md) o [autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md) metodi di accesso. Tuttavia, questa funzionalità non può essere usata con Active Directory Federation Services (AD FS).

## <a name="is-seamless-sso-a-free-feature"></a>La funzionalità Accesso SSO facile è disponibile gratuitamente?

SSO trasparente è una funzionalità disponibile gratuitamente e non è necessario qualsiasi edizione a pagamento di Azure AD toouse è. Rimane disponibile quando la funzionalità hello raggiunge disponibilità generale.

## <a name="what-applications-take-advantage-of-domainhint-or-loginhint-parameter-capability-of-seamless-sso"></a>Quali applicazioni possono sfruttare le capacità dei parametri `domain_hint` o `login_hint` dell'accesso SSO facile?

Siamo nel processo di hello della compilazione di un elenco di hello delle applicazioni che inviano questi parametri e hello quelle che non. Se si hanno applicazioni che sono interessate a, segnalarlo nella sezione commenti hello.

## <a name="does-seamless-sso-support-alternate-id-as-hello-username-instead-of-userprincipalname"></a>Supporta SSO trasparente `Alternate ID` come hello nome utente, anziché `userPrincipalName`?

Sì. Supporta SSO trasparente `Alternate ID` come nome utente quando è configurato in Azure AD Connect, come indicato di hello [qui](active-directory-aadconnect-get-started-custom.md). Non tutte le applicazioni di Office 365 supportano `Alternate ID`. Consultare la documentazione dell'applicazione di toohello specifico per l'istruzione di supporto hello.

## <a name="i-want-tooregister-non-windows-10-devices-with-azure-ad-without-using-ad-fs-can-i-use-seamless-sso-instead"></a>Si desidera tooregister a Windows 10 dispositivi con Azure AD, senza l'utilizzo di ADFS. è possibile usare l'accesso SSO facile?

Sì, questo scenario richiede versione 2.1 o versione successiva di hello [client all'area di lavoro](https://www.microsoft.com/download/details.aspx?id=53554).

## <a name="how-can-i-roll-over-hello-kerberos-decryption-key-of-hello-azureadssoacct-computer-account"></a>Come posso continuata chiave di decrittografia hello Kerberos di hello `AZUREADSSOACCT` account computer?

È importante toofrequently rollover chiave di decrittografia hello Kerberos di hello `AZUREADSSOACCT` account computer (rappresentato da Azure AD) creato in locale foresta di Active Directory.

>[!IMPORTANT]
>Si consiglia di distribuire sulla chiave di decrittografia Kerberos hello almeno ogni 30 giorni.

Seguire questi passaggi nel server locale hello in cui si esegue Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Passaggio 1. Ottenere l'elenco delle foreste di Active Directory in cui è stata abilitata la funzionalità Accesso SSO facile

1. Innanzitutto, scaricare e installare hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Quindi scaricare e installare hello [modulo di Azure Active Directory a 64 bit per Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Passare toohello `%programfiles%\Microsoft Azure Active Directory Connect` cartella.
4. Modulo di PowerShell SSO trasparente hello importazione tramite questo comando: `Import-Module .\AzureADSSO.psd1`.
5. Eseguire PowerShell come amministratore. In PowerShell eseguire la chiamata a `New-AzureADSSOAuthenticationContext`. Questo comando viene fornito un tooenter popup credenziali di amministratore globale del tenant.
6. Eseguire la chiamata a `Get-AzureADSSOStatus`. Questo comando fornisce il che elenco delle foreste di Active Directory (esaminare elenco domini"hello") hello in cui è stata abilitata la funzionalità.

### <a name="step-2-update-hello-kerberos-decryption-key-on-each-ad-forest-that-it-was-set-it-up-on"></a>Passaggio 2. Aggiornare la chiave di decrittografia Kerberos hello in ogni foresta di Active Directory che viene impostata su

1. Eseguire la chiamata a `$creds = Get-Credential`. Quando richiesto, immettere le credenziali di amministratore di dominio hello hello destinato foresta di Active Directory.
2. Eseguire la chiamata a `Update-AzureADSSOForest -OnPremCredentials $creds`. Questo comando aggiornamenti hello Kerberos la chiave di decrittografia per hello `AZUREADSSOACCT` account computer in questa foresta di Active Directory specifica e viene aggiornato in Azure AD.
3. Ripetere hello passaggi per ogni foresta di Active Directory che hai configurato la funzionalità hello in precedenti.

>[!IMPORTANT]
>Verificare che si _non_ eseguire hello `Update-AzureADSSOForest` comando più volte. In caso contrario, la funzione hello smette di funzionare fino al momento hello ticket Kerberos degli utenti scadono e vengono emessi nuovamente da Active Directory locale.

## <a name="how-can-i-disable-seamless-sso"></a>Come è possibile disabilitare l'accesso SSO facile?

La funzionalità Accesso SSO facile può essere disabilitata tramite Azure AD Connect.

Eseguire Azure AD Connect, scegliere la pagina "Cambia l'accesso utente" e fare clic su "Avanti". Deselezionare l'opzione "Abilita single sign-on" hello. Continuare con la procedura guidata hello. Dopo il completamento della procedura guidata hello, SSO senza problemi è disabilitata per il tenant.

Viene tuttavia visualizzato un messaggio con il testo seguente:

"Single sign-on è disabilitata, ma sono disponibili ulteriori passaggi manuali tooperform in ordine toocomplete pulizia. Altre informazioni"

toocomplete hello processo, eseguire la procedura manuale nel server locale hello in cui si esegue Azure AD Connect:

### <a name="step-1-get-list-of-ad-forests-where-seamless-sso-has-been-enabled"></a>Passaggio 1. Ottenere l'elenco delle foreste di Active Directory in cui è stata abilitata la funzionalità Accesso SSO facile

1. Innanzitutto, scaricare e installare hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).
2. Quindi scaricare e installare hello [modulo di Azure Active Directory a 64 bit per Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).
3. Passare toohello `%programfiles%\Microsoft Azure Active Directory Connect` cartella.
4. Modulo di PowerShell SSO trasparente hello importazione tramite questo comando: `Import-Module .\AzureADSSO.psd1`.
5. Eseguire PowerShell come amministratore. In PowerShell eseguire la chiamata a `New-AzureADSSOAuthenticationContext`. Questo comando viene fornito un tooenter popup credenziali di amministratore globale del tenant.
6. Eseguire la chiamata a `Get-AzureADSSOStatus`. Questo comando fornisce il che elenco delle foreste di Active Directory (esaminare elenco domini"hello") hello in cui è stata abilitata la funzionalità.

### <a name="step-2-manually-delete-hello-azureadssoacct-computer-account-from-each-ad-forest-that-you-see-listed"></a>Passaggio 2. Eliminare manualmente hello `AZUREADSSOACCT` account computer da ogni foresta Active Directory è visualizzato.

## <a name="next-steps"></a>Passaggi successivi

- [**Avvio rapido**](active-directory-aadconnect-sso-quick-start.md): avvio ed esecuzione di Accesso SSO facile di Azure AD.
- [**Approfondimento tecnico**](active-directory-aadconnect-sso-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-sso.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
