---
title: 'Azure AD Connect: guida introduttiva all''accesso Single Sign-On facile | Documentazione Microsoft'
description: "Questo articolo descrive la modalità di avvio tooget con Azure Active Directory trasparente Single Sign-On."
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
ms.openlocfilehash: 97d40ed41b3bfad9ff7e11ddbdb8de594ee85de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-seamless-single-sign-on-quick-start"></a>Accesso Single Sign-On facile di Azure Active Directory: guida introduttiva

## <a name="how-toodeploy-seamless-sso"></a>Come toodeploy SSO trasparente

Azure Active Directory trasparente Single Sign-On (SSO senza problemi per Azure AD) accede automaticamente gli utenti quando si trovano sulla rete aziendale connesso tooyour desktop aziendali. Fornisce agli utenti l'accesso semplice applicazioni basate su cloud tooyour senza la necessità di tutti i componenti locali aggiuntive.

>[!IMPORTANT]
>caratteristica di SSO trasparente Hello è attualmente in anteprima.

toodeploy SSO senza problemi, è necessario toofollow questi passaggi:

## <a name="step-1-check-prerequisites"></a>Passaggio 1: Verificare i prerequisiti

Verificare che hello seguenti prerequisiti siano soddisfatti:

1. Configurare il server di Azure AD Connect: se si usa l'[autenticazione pass-through](active-directory-aadconnect-pass-through-authentication.md) come metodo di accesso, non è necessaria alcuna altra azione. Se come metodo di accesso si usa la [sincronizzazione dell'hash delle password](active-directory-aadconnectsync-implement-password-synchronization.md) e se vi è un firewall tra Azure AD Connect e Azure AD, assicurarsi che:
- Si usi la versione 1.1.484.0 o versioni successive di Azure AD Connect.
- Azure AD Connect possa comunicare con gli URL `*.msappproxy.net` e tramite la porta 443. Questo prerequisito è applicabile solo quando si abilita le funzionalità di hello, non per l'accesso degli utenti effettivi.
- Azure AD Connect è possibile apportare diretto IP connessioni toohello [data center di Azure intervalli IP](https://www.microsoft.com/download/details.aspx?id=41653). Anche questo prerequisito è applicabile solo quando si abilita la funzionalità hello.
2. Sono necessarie le credenziali di amministratore di dominio per ogni foresta di Active Directory di sincronizzare tooAzure Active Directory (tramite Azure AD Connect) e per gli utenti di cui si desidera tooenable SSO senza problemi.

## <a name="step-2-enable-hello-feature"></a>Passaggio 2: Abilitare la funzionalità hello

La funzionalità Accesso SSO facile può essere abilitata tramite [Azure AD Connect](active-directory-aadconnect.md).

Se si sta eseguendo una nuova installazione di Azure AD Connect, scegliere hello [percorso di installazione personalizzato](active-directory-aadconnect-get-started-custom.md). In hello "utente" pagina di accesso, verificare l'opzione "Abilita single sign-on" hello.

![Azure AD Connect - Accesso utente](./media/active-directory-aadconnect-sso/sso8.png)

Se Azure AD Connect è già installato, scegliere la pagina "Cambia l'accesso utente" in Azure AD Connect e fare clic su "Avanti". Verificare quindi l'opzione "Abilita single sign-on" hello.

![Azure AD Connect - Cambiare l'accesso utente](./media/active-directory-aadconnect-user-signin/changeusersignin.png)

Continuare con la procedura guidata hello fino a ottenere pagina "Enable single sign-on" toohello. Fornire le credenziali di amministratore di dominio per ogni foresta di Active Directory di sincronizzare tooAzure Active Directory (tramite Azure AD Connect) e per gli utenti di cui si desidera tooenable SSO senza problemi. 

Dopo il completamento della procedura guidata hello, trasparente SSO è abilitato per il tenant.

>[!NOTE]
> le credenziali di amministratore di dominio Hello non vengono archiviate in Azure AD Connect o in Azure AD, ma sono solo funzionalità di hello tooenable utilizzato.

Seguire questi tooverify istruzioni che è stata attivata correttamente trasparente SSO:

1. Accedi toohello [centro di amministrazione di Azure Active Directory](https://aad.portal.azure.com) con credenziali di amministratore globale di hello per il tenant.
2. Selezionare **Azure Active Directory** nella navigazione a sinistra di hello.
3. Selezionare **Azure AD Connect**.
4. Verificare che hello **Single Sign-On trasparente** funzionalità Mostra come **abilitato**.

![Portale di Azure - Pannello Azure AD Connect](./media/active-directory-aadconnect-sso/sso10.png)

## <a name="step-3-roll-out-hello-feature"></a>Passaggio 3: Distribuire funzionalità hello

tooroll gli utenti di tooyour hello funzionalità, è necessario l'area Intranet degli toousers di tooadd due gli URL (https://autologon.microsoftazuread-sso.com e https://aadg.windows.net.nsatc.net) di Azure Active Directory tramite criteri di gruppo in Active Directory.

>[!NOTE]
> Hello seguendo le istruzioni sono disponibili solo per Internet Explorer e Google Chrome in Windows (se i set di URL sito attendibile condivide con Internet Explorer). Leggere la sezione successiva di hello per le istruzioni tooset Mozilla Firefox e Google Chrome su Mac.

### <a name="why-do-you-need-toomodify-users-intranet-zone-settings"></a>Motivo per cui è necessario area Intranet di toomodify degli utenti?

Per impostazione predefinita, il browser hello calcola automaticamente zona di destra hello (Internet o Intranet) da un URL. Ad esempio, http://contoso/ è mappato toohello area Intranet, mentre http://intranet.contoso.com/ infatti toohello mappato l'area Internet (URL hello contiene un punto). Browser non inviare l'endpoint di cloud tooa i ticket Kerberos, ad esempio hello due Azure AD URL -, a meno che il relativo URL viene aggiunto in modo esplicito l'area Intranet toohello del browser.

### <a name="detailed-steps"></a>Procedura dettagliata

1. Aprire lo strumento di gestione criteri di gruppo hello.
2. Modificare i criteri di gruppo applicati toosome o tutti gli utenti di hello. In questo esempio, si usa hello **criterio dominio predefinito**.
3. Passare troppo**utente Configurazione computer\Modelli amministrativi\Componenti di Windows\Internet Explorer\Pannello controllo Internet\pagina** e selezionare **tooZone elenco di assegnazione sito**.
![Single Sign-On](./media/active-directory-aadconnect-sso/sso6.png)  
4. Abilitare i criteri di hello e immettere hello seguenti valori (Azure AD URL in cui vengono inoltrati i ticket Kerberos) e dati (*1* indica l'area Intranet) nella finestra di dialogo hello.

        Value: https://autologon.microsoftazuread-sso.com
        Data: 1
        Value: https://aadg.windows.net.nsatc.net
        Data: 1
>[!NOTE]
> Se si desidera toodisallow alcuni utenti dall'utilizzo di SSO senza problemi, ad esempio, se questi utenti accedono in condivisi chioschi - impostare hello che precede i valori troppo*4*. Questa azione aggiunge hello Azure AD URL toohello area siti con restrizioni e ha esito negativo tutto il tempo hello SSO senza problemi.

5. Fare clic su **OK**, quindi nuovamente su **OK**.

![Single sign-on](./media/active-directory-aadconnect-sso/sso7.png)

### <a name="browser-considerations"></a>Considerazioni sui browser

#### <a name="mozilla-firefox"></a>Mozilla Firefox

Mozilla Firefox non esegue automaticamente l'autenticazione Kerberos. Ogni utente dispone di toomanually aggiungere le impostazioni Firefox tootheir URL hello Azure AD utilizzando hello alla procedura seguente:
1. Eseguire Firefox e immettere `about:config` nella barra degli indirizzi hello. Eliminare tutte le notifiche visualizzate.
2. Ricerca di hello **network.negotiate-auth.trusted-URI** preferenza. Questa preferenza elenca i siti attendibili di Firefox per l'autenticazione Kerberos.
3. Fare clic con il pulsante destro del mouse e selezionare "Modifica".
4. Immettere "https://autologon.microsoftazuread-sso.com, https://aadg.windows.net.nsatc.net" nel campo hello.
5. Fare clic su "OK" e riaprire il browser hello.

#### <a name="safari-on-mac-os"></a>Safari su Mac OS

Assicurarsi che tale macchina di hello in esecuzione Mac OS tooAD unita in join. Vedere le istruzioni su come toodo che [qui](http://training.apple.com/pdf/Best_Practices_for_Integrating_OS_X_with_Active_Directory.pdf).

#### <a name="google-chrome-on-mac-os"></a>Google Chrome su Mac OS

Per Google Chrome in Mac OS e altre piattaforme non Windows, vedere troppo[questo articolo](https://dev.chromium.org/administrators/policy-list-3#AuthServerWhitelist) per informazioni su come toowhitelist hello gli URL di Azure AD per l'autenticazione integrata.

Utilizzo di criteri di gruppo di terze parti Active Directory tooroll estensioni tooFirefox URL AD Azure hello e Google Chrome sugli utenti Mac esula dall'ambito di questo articolo.

#### <a name="known-limitations"></a>Limitazioni note

L'accesso SSO facile non funziona in modalità di esplorazione privata in Firefox e nel browser Edge. Inoltre non funziona in Internet Explorer se hello browser viene eseguito in modalità di protezione avanzata.

>[!IMPORTANT]
>È recente eseguito il rollback il supporto per Edge tooinvestigate problemi segnalati.

## <a name="step-4-test-hello-feature"></a>Passaggio 4: Testare la funzionalità di hello

funzionalità di hello tootest per un utente specifico, assicurarsi che _tutti_ hello le condizioni seguenti siano soddisfatti:
  - utente Hello accede in un dispositivo aziendale.
  - dispositivo Hello è stata tooyour aggiunti in precedenza a un dominio di Active Directory (AD).
  - dispositivo Hello è tooyour una connessione diretta Domain Controller (DC), in rete cablata o wireless aziendale hello o tramite una connessione di accesso remoto, ad esempio una connessione VPN.
  - Hai [implementato funzionalità hello](##step-3-roll-out-the-feature) toothis utente tramite criteri di gruppo.

scenario di hello tootest dove hello immessi solo hello username, ma non la password di hello:
- Accedere a *https://myapps.microsoft.com/* in una nuova sessione del browser privata.

nello scenario hello tootest utente hello non dispone di password di nome utente o hello hello tooenter: 
- Accedere a *https://myapps.microsoft.com/contoso.onmicrosoft.com* in una nuova sessione del browser privata. Sostituire "*contoso*" con il nome del tenant.
- In alternativa, accedere a *https://myapps.microsoft.com/contoso.com* in una nuova sessione del browser privata. Sostituire "*contoso.com*" con un dominio verificato, non un dominio federato, nel tenant.

## <a name="step-5-roll-over-keys"></a>Passaggio 5: Rinnovare le chiavi

Nel passaggio 2, Azure AD Connect crea gli account computer (che rappresentano Azure AD) in tutte le foreste hello Active Directory in cui è stata attivata SSO senza problemi. [Qui](active-directory-aadconnect-sso-how-it-works.md) sono disponibili informazioni dettagliate a riguardo. Per migliorare la sicurezza, è consigliabile che spesso il rollover delle chiavi di decrittografia Kerberos hello di questi account computer.

>[!IMPORTANT]
>Non è necessario di questo passaggio toodo _immediatamente_ dopo avere abilitato la funzionalità hello. Il rollover delle chiavi di decrittografia Kerberos hello almeno ogni 30 giorni.

## <a name="next-steps"></a>Passaggi successivi

- [**Approfondimento tecnico**](active-directory-aadconnect-sso-how-it-works.md): informazioni sul funzionamento di questa funzionalità.
- [**Domande frequenti su** ](active-directory-aadconnect-sso-faq.md) -risposte toofrequently domande frequenti.
- [**Risoluzione dei problemi** ](active-directory-aadconnect-troubleshoot-sso.md) -informazioni su come le problematiche comuni tooresolve con funzionalità hello.
- [**UserVoice**](https://feedback.azure.com/forums/169401-azure-active-directory/category/160611-directory-synchronization-aad-connect): per l'invio di richieste di nuove funzionalità.
