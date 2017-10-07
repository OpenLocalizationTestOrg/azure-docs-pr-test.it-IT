---
title: "funzionalità di aaaUse esistenti dei criteri di rete server tooprovide Azure MFA | Documenti Microsoft"
description: "Hello estensione Server dei criteri di rete per Azure multi-Factor Authentication è una semplice soluzione tooadd basato su cloud in due passaggi vericiation funzionalità tooyour autenticazione infrastruttura esistente."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: e9fc495b06873d45f06233f1aa618db9d94f8bd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-your-existing-nps-infrastructure-with-azure-multi-factor-authentication"></a>Integrare l'infrastruttura NPS esistente con Azure Multi-Factor Authentication

estensione dei criteri di rete Server () per Azure MFA Hello aggiunge basato su cloud MFA funzionalità tooyour infrastruttura di autenticazione con i server esistenti. Con hello estensione dei criteri di rete, è possibile aggiungere una telefonata, SMS o telefono app verifica tooyour esistente flusso di autenticazione senza tooinstall, configurare e gestire nuovi server. 

Questa estensione è stata creata per le organizzazioni che vogliono le connessioni VPN tooprotect senza hello Azure MFA Server di distribuzione. Hello estensione dei criteri di rete opera come un adapter tra RADIUS e basato su cloud Azure MFA tooprovide secondo fattore di autenticazione per gli utenti federati o sincronizzati.

Quando si utilizza l'estensione dei criteri di rete hello per Azure MFA, il flusso di autenticazione hello include hello seguenti componenti: 

1. **Server NAS/VPN** riceve le richieste dei client VPN e li converte in server tooNPS di richieste RADIUS. 
2. **Server dei criteri di rete** si connette tooActive Directory tooperform hello l'autenticazione principale per hello RADIUS richiede e, al completamento dell'operazione, passa le estensioni di hello richiesta tooany installato.  
3. **Estensione dei criteri di rete** attiva un tooAzure richiesta autenticazione a più fattori per l'autenticazione secondaria hello. Una volta estensione hello riceve risposta hello e se la richiesta di autenticazione a più fattori hello ha esito positivo, viene completata la richiesta di autenticazione hello fornendo server NPS hello con i token di sicurezza che includono un'attestazione di autenticazione a più fattori, emesso dal servizio token di Azure.  
4. **Azure MFA** comunica con i dettagli dell'utente di Azure Active Directory tooretrieve hello ed esegue l'autenticazione secondaria hello in qualità di utente toohello verifica metodo configurato.

Hello seguente diagramma viene illustrato questo flusso di richiesta di autenticazione di alto livello: 

![Diagramma del flusso di autenticazione](./media/multi-factor-authentication-nps-extension/auth-flow.png)

## <a name="plan-your-deployment"></a>Pianificare la distribuzione

Hello estensione dei criteri di rete gestisce automaticamente la ridondanza, pertanto non è necessario una configurazione speciale.

È possibile creare un qualsiasi numero di Server dei criteri di rete abilitati per Azure MFA. Se si installano più server, è consigliabile usare un certificato client di differenza per ciascuno. La creazione di un certificato per ogni server significa che è possibile aggiornare singolarmente ogni certificato senza doversi preoccupare dei tempi di inattività in tutti i server.

Server VPN di instradare le richieste di autenticazione, pertanto è necessario conoscere i server dei criteri di rete abilitati per Azure MFA nuovo hello toobe.

## <a name="prerequisites"></a>Prerequisiti

Hello estensione dei criteri di rete deve essere toowork con l'infrastruttura esistente. Assicurarsi di avere hello seguenti prerequisiti prima di iniziare.

### <a name="licenses"></a>Licenze

Hello estensione dei criteri di rete per l'autenticazione a più fattori di Azure è disponibile toocustomers con [licenze per Azure multi-Factor Authentication](multi-factor-authentication.md) (incluso in una sottoscrizione di autenticazione a più fattori, Azure AD Premium o EMS).

### <a name="software"></a>Software

Windows Server 2008 R2 SP1 o versione successiva.

### <a name="libraries"></a>Librerie

Queste librerie vengono installate automaticamente con l'estensione hello.
-   [Visual C++ Redistributable Packages per Visual Studio 2013 (X64)](https://www.microsoft.com/download/details.aspx?id=40784)
-   [Modulo di Microsoft Azure Active Directory per Windows PowerShell versione 1.1.166.0](https://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)

### <a name="azure-active-directory"></a>Azure Active Directory

Gli utenti che utilizzano l'estensione dei criteri di rete hello devono essere sincronizzati tooAzure Active Directory con Azure AD Connect e deve essere registrato per l'autenticazione a più fattori.

Quando si installa l'estensione di hello, credenziali admin e ID di directory hello è necessario per il tenant di Azure AD. È possibile trovare l'ID di directory in hello [portale di Azure](https://portal.azure.com). Accedere come amministratore, seleziona hello **Azure Active Directory** icona a sinistra di hello, quindi selezionare **proprietà**. Ciao copia GUID hello **ID Directory** casella e salvarlo. Utilizzare questo GUID come ID tenant hello quando si installa hello estensione dei criteri di rete.

![L'ID directory si trova nelle proprietà di Azure Active Directory](./media/multi-factor-authentication-nps-extension/find-directory-id.png)

## <a name="prepare-your-environment"></a>Preparare l'ambiente

Prima di installare l'estensione dei criteri di rete hello, si desidera tooprepare si ambiente toohandle hello il traffico di autenticazione.

### <a name="enable-hello-nps-role-on-a-domain-joined-server"></a>Abilitare il ruolo dei criteri di rete hello in un server di dominio

server dei criteri di rete Hello si connette tooAzure Active Directory e consente di autenticare le richieste di autenticazione a più fattori hello. Scegliere un server per questo ruolo. Si consiglia di scegliere un server che non gestiva le richieste provenienti da altri servizi, poiché hello estensione dei criteri di rete genera errori per tutte le richieste che non sono RADIUS.

1. Nel server, aprire hello **Aggiunta guidata ruoli e funzionalità** dal menu di Server Manager Quickstart hello.
2. Come tipo di installazione scegliere **Installazione basata su ruoli o basata su funzionalità**.
3. Seleziona hello **servizi di accesso e criteri di rete** ruolo del server. Una finestra può popup tooinform di funzionalità necessarie toorun questo ruolo.
4. Continuare con la procedura guidata hello fino a quando la pagina di conferma hello. Selezionare **Installa**.

Ora che si dispone di un server designato per criteri di rete, è inoltre necessario configurare questo toohandle server richieste RADIUS da hello soluzione VPN.

### <a name="configure-your-vpn-solution-toocommunicate-with-hello-nps-server"></a>Configurare il toocommunicate soluzione VPN con server dei criteri di rete hello

A seconda di quale soluzione VPN utilizzata, hello tooconfigure passaggi variare i criteri di autenticazione RADIUS. Configurare il server di criteri toopoint tooyour RADIUS dei criteri di rete.

### <a name="sync-domain-users-toohello-cloud"></a>Sincronizzazione dominio utenti toohello cloud

Questo passaggio potrebbe essere già completo per il tenant, ma è buona controllo toodouble che Azure AD Connect sia sincronizzato i database di recente.

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. Selezionare **Azure Active Directory** > **Azure AD Connect**
3. Verificare che lo stato della sincronizzazione sia **Abilitata** e che l'ultima sincronizzazione sia stata eseguita da meno di un'ora.

Se è necessario tookick disattivare un nuovo ciclo di sincronizzazione, ci hello istruzioni [sincronizzazione di Azure AD Connect: utilità di pianificazione](../active-directory/connect/active-directory-aadconnectsync-feature-scheduler.md#start-the-scheduler).

### <a name="determine-which-authentication-methods-your-users-can-use"></a>Determinare i metodi di autenticazione che è possibile usare

Sono due i fattori che determinano i metodi di autenticazione disponibili con una distribuzione dell'estensione di Server dei criteri di rete:

1. algoritmo di crittografia password Hello utilizzato tra client RADIUS hello (VPN, server Netscaler, o altri) e server NPS hello.
   - **PAP** supporta tutti i metodi di autenticazione di hello di Azure MFA nel cloud hello: telefonata, SMS unidirezionali, notifica dell'app mobile e il codice di verifica app per dispositivi mobili.
   - **CHAPV2** e **EAP** supportano la chiamata telefonica e la notifica dell'app per dispositivi mobili.
2. Hello input metodi hello applicazione client (VPN, server Netscaler, o altri) in grado di gestire. Ad esempio, il client VPN hello dispone in modo tooallow hello utente tootype in un codice di verifica da un testo o app per dispositivi mobili?

Quando si distribuisce l'estensione dei criteri di rete hello, utilizzare tooevaluate questi fattori quali metodi sono disponibili per gli utenti. Se il client RADIUS supporta PAP, ma il client di hello UX privo di campi di input per un codice di verifica, quindi telefonata e notifica dell'app mobile sono disponibili due opzioni supportate hello.

È possibile [disabilitare i metodi di autenticazione non supportati](multi-factor-authentication-whats-next.md#selectable-verification-methods) in Azure.

### <a name="enable-users-for-mfa"></a>Abilitare gli utenti per l'MFA

Prima di distribuire l'estensione dei criteri di rete completo hello, è necessario tooenable autenticazione a più fattori per hello gli utenti che si verifica in due passaggi tooperform. Più immediatamente, estensione hello tootest durante la distribuzione, è necessario almeno un test account che è completamente registrato per l'autenticazione a più fattori.

Utilizzare questi passaggi tooget avvio di un account di prova:
1. Accedi troppo[https://aka.ms/mfasetup](https://aka.ms/mfasetup) con un account di prova. 
2. Seguire hello tooset di richieste di un metodo di verifica.
3. Creare un criterio di accesso condizionale o [modificare lo stato utente hello](multi-factor-authentication-get-started-user-states.md) toorequire di verifica in due passaggi per l'account di prova hello. 

Gli utenti devono inoltre toofollow tooenroll questi passaggi prima che questi possono autenticarsi con l'estensione dei criteri di rete hello.

## <a name="install-hello-nps-extension"></a>Installare l'estensione dei criteri di rete hello

> [!IMPORTANT]
> Installare l'estensione dei criteri di rete hello in un server diverso rispetto al punto di accesso VPN hello.

### <a name="download-and-install-hello-nps-extension-for-azure-mfa"></a>Scaricare e installare l'estensione dei criteri di rete hello per Azure MFA

1.  [Scaricare l'estensione dei criteri di rete hello](https://aka.ms/npsmfa) da hello Microsoft Download Center.
2.  Copiare toohello binario hello desiderato tooconfigure Server dei criteri di rete.
3.  Eseguire *setup.exe* e seguire le istruzioni di installazione di hello. Se si verificano errori, verificare che hello due librerie dalla sezione dei prerequisiti hello sono state installate correttamente.

### <a name="run-hello-powershell-script"></a>Eseguire script PowerShell hello

programma di installazione di Hello crea uno script di PowerShell in questa posizione: `C:\Program Files\Microsoft\AzureMfa\Config` (dove C:\ rappresenta l'unità di installazione). Questo script di PowerShell esegue hello seguenti azioni:

-   Creare un certificato autofirmato.
-   Associare una chiave pubblica di hello di hello certificato toohello entità servizio in Azure AD.
-   Archivio hello certificato nell'archivio certificati computer locale di hello.
-   Privato chiave tooNetwork concedere accesso toohello certificato utente.
-   Riavviare hello dei criteri di rete.

Se non si desidera toouse propri certificati (anziché hello certificati autofirmati che hello genera script di PowerShell), installazione hello Script di PowerShell toocomplete hello. Se si installa l'estensione hello in più server, ciascuna di esse deve avere il proprio certificato.

1. Eseguire Windows PowerShell come amministratore.
2. Cambiare le directory.

   `cd "C:\Program Files\Microsoft\AzureMfa\Config"`

3. Eseguire uno script di PowerShell hello creato dal programma di installazione hello.

   `.\AzureMfaNpsExtnConfigSetup.ps1`

4. Prompt di PowerShell per l'ID tenant. Utilizzare Directory ID GUID copiata dal portale di Azure nella sezione Prerequisiti hello hello hello.
5. Accedi tooAzure AD un amministratore.
6. PowerShell Visualizza un messaggio di conferma al termine dello script hello.  

Ripetere questi passaggi in altri server dei criteri di rete che si desidera tooset per il bilanciamento del carico.

>[!NOTE]
>Se si utilizzano certificati personalizzati invece di generare i certificati con hello script di PowerShell, assicurarsi che queste si allinea toohello convenzione di denominazione dei criteri di rete. deve essere il nome di soggetto Hello **CN =\<TenantID\>, OU = estensione dei criteri di rete Microsoft**. 

## <a name="configure-your-nps-extension"></a>Configurare l'estensione di Server dei criteri di rete

In questa sezione sono disponibili considerazioni e suggerimenti sulla progettazione per una corretta distribuzione dell'estensione di Server dei criteri di rete.

### <a name="configuration-limitations"></a>Limitazioni di configurazione

- estensione dei criteri di rete per Azure MFA Hello non include strumenti toomigrate utenti e le impostazioni dal cloud toohello Server MFA. Per questo motivo, è consigliabile utilizzare estensione hello per nuove distribuzioni, anziché di distribuzione esistente. Se si utilizza l'estensione hello in una distribuzione esistente, gli utenti dispongono di backup tooperform prova nuovamente toopopulate dettagli loro MFA nel cloud hello.  
- Hello estensione dei criteri di rete utilizza hello UPN da hello locale utente Active directory tooidentify hello su Azure MFA per l'esecuzione di estensione di hello hello autenticazione secondaria può essere configurato toouse un identificatore diverso come account di accesso alternativo ID o personalizzato di Active Directory campo diverso da UPN. Vedere [configurazione opzioni avanzate per hello estensione dei criteri di rete multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) per ulteriori informazioni.
- Non tutti i protocolli di crittografia supportano tutti i metodi di verifica.
   - **PAP** supporta la chiamata telefonica, gli SMS unidirezionali, la notifica dell'app per dispositivi mobili e il codice di verifica app per dispositivi mobili
   - **CHAPV2** e **EAP** supportano la chiamata telefonica e la notifica dell'app per dispositivi mobili

### <a name="control-radius-clients-that-require-mfa"></a>Client RADIUS di controllo che richiedono MFA

Dopo aver abilitato l'autenticazione a più fattori per un client RADIUS utilizzando hello estensione dei criteri di rete, tutte le autenticazioni riuscite per questo client sono necessari tooperform autenticazione a più fattori. Se si desidera tooenable autenticazione a più fattori per alcuni client RADIUS, ma non altri, è possibile configurare due server dei criteri di rete e installare l'estensione hello in uno solo di essi. Configurare i client RADIUS che si desidera toorequire toosend richieste toohello dei criteri di rete server MFA configurato con estensione hello e altro server RADIUS client toohello dei criteri di rete non è configurato con estensione hello.

### <a name="prepare-for-users-that-arent-enrolled-for-mfa"></a>Impostazioni per gli utenti che non sono registrati per MFA

Se sono presenti utenti che non sono registrati per l'autenticazione a più fattori, è possibile determinare che cosa avviene quando si tenta di tooauthenticate. Utilizzare l'impostazione del Registro di sistema hello *REQUIRE_USER_MATCH* nel percorso del Registro di sistema hello *HKLM\Software\Microsoft\AzureMFA* toocontrol comportamento della caratteristica hello. Questa impostazione non ha un'unica opzione di configurazione:

| Chiave | Valore | Default |
| --- | ----- | ------- |
| REQUIRE_USER_MATCH | VERO/FALSO | Non è impostato (tooTRUE equivalente) |

Salve a scopo di questa impostazione è toodetermine quali toodo quando un utente non è registrato per l'autenticazione a più fattori. Quando non esiste, non è impostata o è impostata, tooTRUE chiave hello hello utente non è registrato, quindi estensione hello si verifica un errore di richiesta di autenticazione a più fattori hello. Quando la chiave hello viene impostata tooFALSE e hello utente non è registrato, l'autenticazione procede senza eseguire l'autenticazione a più fattori.

È possibile scegliere toocreate questa chiave e impostare tooFALSE mentre gli utenti sono caricamento potrebbe non essere registrati per Azure MFA ancora. Tuttavia, poiché l'impostazione chiave hello consente agli utenti che non sono registrati per l'autenticazione a più fattori toosign in, è consigliabile rimuovere questa chiave prima di passare tooproduction.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="how-do-i-verify-that-hello-client-cert-is-installed-as-expected"></a>Come verificare che il certificato client hello viene installato come previsto?

Cercare hello autofirmato creato dal programma di installazione di hello nell'archivio certificati hello e verificare che la chiave privata di hello dispone delle autorizzazioni concesse toouser **servizio di rete**. è un nome soggetto di Hello **CN \<tenantid\>, OU = estensione dei criteri di rete Microsoft**

-------------------------------------------------------------

### <a name="how-can-i-verify-that-my-client-cert-is-associated-toomy-tenant-in-azure-active-directory"></a>Come è possibile verificare che il certificato client è associato toomy tenant in Azure Active Directory?

Aprire un prompt dei comandi di PowerShell e hello eseguire i comandi seguenti:

```
import-module MSOnline
Connect-MsolService
Get-MsolServicePrincipalCredential -AppPrincipalId "981f26a1-7f43-403b-a875-f8b09b8cd720" -ReturnKeyValues 1 
```

Questi comandi stampano tutti i certificati di hello associazione tenant con l'istanza di hello estensione dei criteri di rete nella sessione di PowerShell. Cercare il certificato da esportare il certificato client come file con "X.509(.cer) con codifica Base-64" senza chiave privata hello e confrontarlo con l'elenco di hello da PowerShell.

Valido-da e valido-fino a quando i timestamp, che sono in formato leggibile, possono essere utilizzato toofilter out misfits evidente se hello restituito più di un certificato.

-------------------------------------------------------------

### <a name="why-are-my-requests-failing-with-adal-token-error"></a>Perché le richieste hanno esito negativo con errore di token ADAL?

Questo errore potrebbe essere stato causato tooone diversi motivi. Utilizzare la procedura di risoluzione dei problemi toohelp:

1. Riavviare il server di Server dei criteri di rete.
2. Verificare che il certificato client sia installato come previsto.
3. Verificare che il certificato hello è associato a tenant di Windows Azure.
4. Verificare che https://login.microsoftonline.com/ sia accessibile dal server di hello che esegue estensione hello.

-------------------------------------------------------------

### <a name="why-does-authentication-fail-with-an-error-in-http-logs-stating-that-hello-user-is-not-found"></a>Motivo per cui l'autenticazione esito negativo con un errore nel log HTTP che informa che l'utente hello non è stato trovato?

Verificare che Active Directory Connect è in esecuzione e che l'utente hello è presente in Active Directory di Windows e Azure Active Directory.

------------------------------------------------------------

### <a name="why-do-i-see-http-connect-errors-in-logs-with-all-my-authentications-failing"></a>Perché vengono visualizzati errori di connessione HTTP nei log che contengono le autenticazioni non riuscite?

Verificare che https://adnotifications.windowsazure.com sia raggiungibile dal server hello esegue hello estensione di criteri di rete.


## <a name="next-steps"></a>Passaggi successivi

- Configurare gli ID alternativi per l'account di accesso o impostare un elenco di eccezioni per gli indirizzi IP che non devono eseguire la verifica in due fasi in [configurazione opzioni avanzate per hello estensione dei criteri di rete multi-Factor Authentication](nps-extension-advanced-configuration.md)

- [Risolvere i messaggi di errore di hello estensione dei criteri di rete per Azure multi-Factor Authentication](multi-factor-authentication-nps-errors.md)
