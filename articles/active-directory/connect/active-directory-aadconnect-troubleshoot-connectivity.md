---
title: "Azure AD Connect: risolvere i problemi di connettività | Documentazione Microsoft"
description: "Viene illustrato come sono problemi di connettività tootroubleshoot con Azure AD Connect."
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 3aa41bb5-6fcb-49da-9747-e7a3bd780e64
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 60d6b7c4ad8a3ab907c20e598ec9443f115df287
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connectivity-issues-with-azure-ad-connect"></a>Risolvere i problemi di connettività con Azure AD Connect
In questo articolo viene illustrato come funziona la connettività tra Azure AD Connect e Azure AD e come problemi di connettività di tootroubleshoot. Questi problemi sono probabilmente toobe visualizzato in un ambiente con un server proxy.

## <a name="troubleshoot-connectivity-issues-in-hello-installation-wizard"></a>Risoluzione dei problemi di connettività in Installazione guidata di hello
Azure AD Connect utilizza l'autenticazione moderna (mediante la libreria ADAL hello) per l'autenticazione. installazione guidata di Hello e motore di sincronizzazione hello corretto richiedono toobe Machine. config configurato correttamente poiché questi due sono le applicazioni .NET.

In questo articolo viene illustrata la modalità di connessione tooAzure AD tramite il proxy di Fabrikam. server proxy Hello è denominato fabrikamproxy e utilizza la porta 8080.

È prima necessario toomake che [ **Machine. config** ](active-directory-aadconnect-prerequisites.md#connectivity) sia configurato correttamente.  
![machineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/machineconfig.png)

> [!NOTE]
> In alcuni blog non Microsoft, è documentata che devono essere apportate modifiche toomiiserver.exe.config invece. Tuttavia, questo file viene sovrascritto ogni pertanto anche se risulta appropriato durante l'installazione iniziale, il sistema hello smette di funzionare in seguito all'aggiornamento prima l'aggiornamento. Per questo motivo, indicazione hello è invece tooupdate file Machine. config.
>
>

server proxy Hello inoltre necessario aprire gli URL di hello necessario. elenco ufficiale Hello è documentato [gli intervalli di indirizzi IP e gli URL di Office 365](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2).

Gli URL, hello nella tabella seguente è hello assoluto toobe minimo bare tooconnect in grado di tooAzure Active Directory. L'elenco non include le funzionalità facoltative, ad esempio il writeback delle password o Azure AD Connect Health. È documentato qui toohelp nella risoluzione dei problemi per la configurazione iniziale di hello.

| URL | Port | Descrizione |
| --- | --- | --- |
| mscrl.microsoft.com |HTTP/80 |Elenca toodownload utilizzati CRL. |
| \*.verisign.com |HTTP/80 |Elenca toodownload utilizzati CRL. |
| \*.entrust.com |HTTP/80 |Toodownload usato CRL Elenca per l'autenticazione a più fattori. |
| \*.windows.net |HTTPS/443 |Toosign utilizzati in tooAzure Active Directory. |
| secure.aadcdn.microsoftonline-p.com |HTTPS/443 |Usato per MFA. |
| \*.microsoftonline.com |HTTPS/443 |Utilizzato tooconfigure i dati di directory e l'importazione/esportazione di Azure AD. |

## <a name="errors-in-hello-wizard"></a>Errori nella creazione guidata hello
installazione guidata di Hello usa due diversi contesti di sicurezza. Nella pagina hello **connettersi tooAzure AD**, utilizza hello attualmente effettuato l'accesso utente. Nella pagina hello **configura**, in fase di modifica toohello [account che esegue il servizio di hello per il motore di sincronizzazione hello](active-directory-aadconnect-accounts-permissions.md#azure-ad-connect-sync-service-account). Se si verifica un problema, viene visualizzato probabilmente già esistenti in hello **connettersi tooAzure AD** pagina nella procedura guidata hello poiché la configurazione del proxy hello è globale.

Hello seguenti problemi è gli errori più comuni di hello riscontrati nell'installazione guidata di hello.

### <a name="hello-installation-wizard-has-not-been-correctly-configured"></a>installazione guidata di Hello non è stato configurato correttamente
Questo errore viene visualizzato quando non riesce a raggiungere proxy hello guidata hello stesso.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomachineconfig.png)

* Se viene visualizzato questo errore, verificare hello [Machine. config](active-directory-aadconnect-prerequisites.md#connectivity) sia stato configurato correttamente.
* Se sembra corretto, seguire hello [verificare la connettività proxy](#verify-proxy-connectivity) toosee se è presente all'esterno di hello guidata nonché problema hello.

### <a name="a-microsoft-account-is-used"></a>Viene usato un account Microsoft
Se si usa un **account Microsoft** anziché un account **dell'istituto di istruzione o dell'organizzazione**, viene visualizzato un errore generico.  
![Viene usato un account Microsoft](./media/active-directory-aadconnect-troubleshoot-connectivity/unknownerror.png)

### <a name="hello-mfa-endpoint-cannot-be-reached"></a>Impossibile raggiungere l'endpoint di autenticazione a più fattori Hello
Questo errore viene visualizzato se hello endpoint **https://secure.aadcdn.microsoftonline-p.com** non può essere raggiunto e l'amministratore globale è abilitato con autenticazione a più fattori.  
![nomachineconfig](./media/active-directory-aadconnect-troubleshoot-connectivity/nomicrosoftonlinep.png)

* Se viene visualizzato questo errore, verificare che l'endpoint hello **secure.aadcdn.microsoftonline p.com** è stato aggiunto toohello proxy.

### <a name="hello-password-cannot-be-verified"></a>Impossibile verificare la password Hello
Impossibile verificare se l'installazione guidata di hello è riuscito a connettersi AD tooAzure ma stessa password hello che viene visualizzato questo errore:  
![badpassword](./media/active-directory-aadconnect-troubleshoot-connectivity/badpassword.png)

* Password hello una password temporanea e deve essere modificato? Si effettivamente hello password corretta? Provare a toosign in toohttps://login.microsoftonline.com (in un altro computer server di Azure AD Connect di hello) e verificare l'account di hello è utilizzabile.

### <a name="verify-proxy-connectivity"></a>Verificare la connettività del proxy
tooverify se hello Azure AD Connect server dispone di connettività effettiva con hello Proxy e Internet, utilizzare alcuni toosee PowerShell se proxy hello consente le richieste web o non. Al prompt di PowerShell eseguire `Invoke-WebRequest -Uri https://adminwebservice.microsoftonline.com/ProvisioningService.svc`. (Tecnicamente hello prima chiamata è toohttps://login.microsoftonline.com e questo URI può essere utilizzata anche, ma altri URI hello è più veloce toorespond).

PowerShell utilizza configurazione hello proxy hello toocontact di Machine. config. impostazioni Hello/netsh winhttp dovrebbero influire questi cmdlet.

Se il proxy di hello è configurato correttamente, è necessario ottenere uno stato di esito positivo: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest200.png)

Se si riceve **tooconnect Impossibile toohello remote server**, PowerShell sta tentando una chiamata diretta toomake senza l'utilizzo di proxy hello o DNS non è configurato correttamente. Verificare che hello **Machine. config** file sia configurato correttamente.
![unabletoconnect](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequestunable.png)

Se il proxy di hello non è configurato correttamente, viene visualizzato un errore: ![proxy200](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest403.png)
![proxy407](./media/active-directory-aadconnect-troubleshoot-connectivity/invokewebrequest407.png)

| Errore | Testo dell'errore | Commento |
| --- | --- | --- |
| 403 |Accesso negato |proxy Hello non è stato aperto per hello richiesti URL. Rivedere la configurazione del proxy hello e assicurarsi che hello [URL](https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2) sono stati aperti. |
| 407 |Autenticazione proxy obbligatoria |server proxy Hello è richiesto un Accedi e non è stato specificato alcun valore. Se il server proxy richiede l'autenticazione, assicurarsi che toohave questa impostazione configurata in Machine. config hello. Accertarsi che si utilizzano account di dominio per l'utente hello guidata hello e per l'account del servizio hello. |

## <a name="hello-communication-pattern-between-azure-ad-connect-and-azure-ad"></a>modello di comunicazione Hello tra Azure AD Connect e Azure AD
Se sono stati eseguiti tutti i passaggi precedenti e ancora non è possibile connettersi, si può iniziare a esaminare i log di rete. Questa sezione documenta un normale modello di connettività riuscita. Inoltre è listato herrings rosso comuni che possono essere ignorati durante la lettura log rete hello.

* Sono presenti chiamate toohttps://dc.services.visualstudio.com. Non è necessario toohave che questo URL aperto in proxy hello per toosucceed installazione hello e queste chiamate può essere ignorato.
* Vedrai che la risoluzione dns Elenca hello host effettivo toobe nsatc.net spazio nome DNS di hello e altri spazi dei nomi non in microsoftonline.com. Tuttavia, non vi sono richieste di servizio web sui nomi di server effettivo hello e non si dispone tooadd questi proxy toohello URL.
* provisioningapi e hello endpoint adminwebservice sono endpoint di individuazione e utilizzati toofind hello endpoint effettivo toouse. Questi endpoint variano in base al paese.

### <a name="reference-proxy-logs"></a>Log del proxy di riferimento
Ecco un dump di una proxy effettivo log hello installazione pagina procedura guidata e da dove si è stato eseguito (toohello voci duplicate stesso endpoint sono stati rimossi). Questa sezione può essere usata come riferimento per i log di rete e proxy in uso. gli endpoint effettivo Hello potrebbero essere diversi nel proprio ambiente (in particolare degli URL in *corsivo*).

**Connettersi AD tooAzure**

| Tempo | URL |
| --- | --- |
| 1/11/2016 8:31 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:31 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:32 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:33 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Configura**

| Time | URL |
| --- | --- |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:43 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://*bba800-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:44 |connect://login.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://provisioningapi.microsoftonline.com:443 |
| 1/11/2016 8:46 |connect://*bwsc02-relay*.microsoftonline.com:443 |

**Sincronizzazione iniziale**

| Time | URL |
| --- | --- |
| 1/11/2016 8:48 |connect://login.windows.net:443 |
| 1/11/2016 8:49 |connect://adminwebservice.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba900-anchor*.microsoftonline.com:443 |
| 1/11/2016 8:49 |connect://*bba800-anchor*.microsoftonline.com:443 |

## <a name="authentication-errors"></a>Errori di autenticazione
Questa sezione vengono trattati gli errori che possono essere restituiti da ADAL (libreria di autenticazione hello utilizzata da Azure AD Connect) e PowerShell. Errore Hello illustrati in deve comprendere i passaggi successivi.

### <a name="invalid-grant"></a>Concessione non valida
Nome utente o password non validi. Per ulteriori informazioni, vedere [hello password non può essere verificata](#the-password-cannot-be-verified).

### <a name="unknown-user-type"></a>Tipo di utente sconosciuto
Non è possibile trovare o risolvere la directory di Azure AD. Forse si tenta di toologin con un nome utente in un dominio non verificato?

### <a name="user-realm-discovery-failed"></a>Individuazione dell'area di autenticazione utente non riuscita
Problemi di configurazione di rete o del proxy. Impossibile raggiungere la rete Hello. Vedere [risoluzione dei problemi di connettività in Installazione guidata di hello](#troubleshoot-connectivity-issues-in-the-installation-wizard).

### <a name="user-password-expired"></a>Password utente scaduta
Le credenziali sono scadute. Modificare la password.

### <a name="authorizationfailure"></a>Errore di autorizzazione
Problema sconosciuto.

### <a name="authentication-cancelled"></a>Autenticazione annullata
richiesta di Hello multi-factor authentication (MFA) è stata annullata.

### <a name="connecttomsonline"></a>Connessione a MS Online
L'autenticazione ha avuto esito positivo, ma Azure AD PowerShell ha un problema di autenticazione.

### <a name="azurerolemissing"></a>Ruolo di Azure mancante
L'autenticazione ha avuto esito positivo. L'utente non è un amministratore globale.

### <a name="privilegedidentitymanagement"></a>Privileged Identity Management
L'autenticazione ha avuto esito positivo. Privileged Identity Management è abilitata e l'utente attualmente non è un amministratore globale. Per altre informazioni, vedere [Privileged Identity Management](../active-directory-privileged-identity-management-getting-started.md).

### <a name="companyinfounavailable"></a>Informazioni aziendali non disponibili
L'autenticazione ha avuto esito positivo. Impossibile recuperare le informazioni aziendali da Azure AD.

### <a name="retrievedomains"></a>Recupero domini
L'autenticazione ha avuto esito positivo. Impossibile recuperare le informazioni sul dominio da Azure AD.

### <a name="unexpected-exception"></a>Eccezione imprevista
Visualizzato come un errore imprevisto nell'installazione guidata di hello. Può verificarsi se si tenta di toouse un **Account Microsoft** anziché **account aziendale o dell'istituto di istruzione organizzazione**.

## <a name="troubleshooting-steps-for-previous-releases"></a>Procedure di risoluzione dei problemi per le versioni precedenti.
Con le versioni a partire dal numero di build 1.1.105.0 (rilasciata febbraio 2016), l'Assistente per l'accesso hello è stata ritirata. Questa sezione e hello di configurazione non deve più essere obbligatoria, ma viene mantenuta come riferimento.

Per hello single sign-in assistant toowork, è necessario configurare winhttp. Questa configurazione può essere eseguita con [ **netsh**](active-directory-aadconnect-prerequisites.md#connectivity).  
![netsh](./media/active-directory-aadconnect-troubleshoot-connectivity/netsh.png)

### <a name="hello-sign-in-assistant-has-not-been-correctly-configured"></a>Assistente per l'accesso Hello non è stato configurato correttamente
Questo errore viene visualizzato quando hello-Assistente per l'accesso non riesce a raggiungere il proxy di hello o hello proxy non consenta richiesta hello.
![nonetsh](./media/active-directory-aadconnect-troubleshoot-connectivity/nonetsh.png)

* Se viene visualizzato questo errore, consultare configurazione proxy hello in [netsh](active-directory-aadconnect-prerequisites.md#connectivity) e verificare sia corretto.
  ![netshshow](./media/active-directory-aadconnect-troubleshoot-connectivity/netshshow.png)
* Se sembra corretto, seguire hello [verificare la connettività proxy](#verify-proxy-connectivity) toosee se è presente all'esterno di hello guidata nonché problema hello.

## <a name="next-steps"></a>Passaggi successivi
Altre informazioni su [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md).
