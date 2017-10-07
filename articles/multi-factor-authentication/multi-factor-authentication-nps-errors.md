---
title: codici di errore aaaTroubleshoot per hello estensione dei criteri di rete di Azure MFA | Documenti Microsoft
description: Informazioni su come risolvere i problemi con l'estensione dei criteri di rete hello Azure multi-Factor Authentication con risoluzioni per messaggi di errore comuni
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
ms.date: 07/14/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8b602954364c6e9f801d86edca6432bd8446c58b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-error-messages-from-hello-nps-extension-for-azure-multi-factor-authentication"></a>Risolvere i messaggi di errore di hello estensione dei criteri di rete per Azure multi-Factor Authentication

Se si verificano errori con hello estensione dei criteri di rete per Azure multi-Factor Authentication, utilizzare questo tooreach articolo una risoluzione più veloce. 

## <a name="troubleshooting-steps-for-common-errors"></a>Procedura per la risoluzione di errori comuni

| Codice di errore | Passaggi per la risoluzione dei problemi |
| ---------- | --------------------- |
| **CONTACT_SUPPORT** | [Contattare il supporto tecnico](#contact-microsoft-support)e indicare l'elenco di hello dei passaggi per la raccolta di log. Fornire le informazioni come su cosa è successo prima dell'errore hello, inclusi id tenant e il nome dell'entità utente (UPN). |
| **CLIENT_CERT_INSTALL_ERROR** | Potrebbe esserci un problema con il certificato client hello è stato installato o associata al tenant. Seguire le istruzioni hello [Troubleshooting hello estensione NPS MFA](multi-factor-authentication-nps-extension.md#troubleshooting) tooinvestigate problemi di certificato client. |
| **ESTS_TOKEN_ERROR** | Seguire le istruzioni hello [Troubleshooting hello estensione NPS MFA](multi-factor-authentication-nps-extension.md#troubleshooting) certificato client tooinvestigate e ADAL token problemi. |
| **HTTPS_COMMUNICATION_ERROR** | server dei criteri di rete Hello è Impossibile tooreceive risposte da Azure MFA. Verificare che i firewall siano aperte bidirezionale per il traffico tooand da https://adnotifications.windowsazure.com |
| **HTTP_CONNECT_ERROR** | Nel server di hello che esegue l'estensione dei criteri di rete hello, verificare che si possa raggiungere https://adnotifications.windowsazure.com e https://login.microsoftonline.com/. Se tali siti non vengono caricati, risolvere i problemi di connettività sul server. |
| **REGISTRY_CONFIG_ERROR** | Manca una chiave del Registro di sistema hello applicazione hello, che può essere poiché hello [script di PowerShell](multi-factor-authentication-nps-extension.md#install-the-nps-extension) non è stata eseguita dopo l'installazione. messaggio di errore Hello deve includere una chiave mancante hello. Assicurarsi di avere chiave hello in HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\AzureMfa. |
| **REQUEST_FORMAT_ERROR** <br> Nella richiesta RADIUS manca l'attributo RADIUS userName\Identifier attributo obbligatorio. Verificare che NPS riceva le richieste RADIUS | Questo errore indica in genere un problema di installazione. Hello estensione dei criteri di rete deve essere installato nel server dei criteri di rete che può ricevere le richieste RADIUS. I server NPS installati come dipendenze dei servizi come RDG e RRAS non ricevono le richieste RADIUS. Estensione dei criteri di rete non funziona installato su tali installazioni ed errori non è possibile leggere i dettagli di hello dalla richiesta di autenticazione hello. |
| **REQUEST_MISSING_CODE** | Assicurarsi che protocollo di crittografia password hello tra hello dei criteri di rete e server NAS supporti metodo di autenticazione secondario hello in uso. **PAP** supporta tutti i metodi di autenticazione di hello di Azure MFA nel cloud hello: telefonata, SMS unidirezionali, notifica dell'app mobile e il codice di verifica app per dispositivi mobili. **CHAPV2** e **EAP** supportano la chiamata telefonica e la notifica dell'app per dispositivi mobili. |
| **USERNAME_CANONICALIZATION_ERROR** | Verificare che l'utente hello è presente nell'istanza di Active Directory locale, e tale server NPS hello dispone di una directory di hello tooaccess autorizzazioni. Se si usano i trust tra foreste, [contattare il supporto tecnico](#contact-microsoft-support) per maggiore assistenza. |


   

### <a name="alternate-login-id-errors"></a>Errori relativi all'ID di accesso alternativo

| Codice di errore | Messaggio di errore | Passaggi per la risoluzione dei problemi |
| ---------- | ------------- | --------------------- |
| **ALTERNATE_LOGIN_ID_ERROR** | Errore: la ricerca di userObjectSid non è riuscita | Verificare che l'utente hello esista nell'istanza di Active Directory locale. Se si usano i trust tra foreste, [contattare il supporto tecnico](#contact-microsoft-support) per maggiore assistenza. |
| **ALTERNATE_LOGIN_ID_ERROR** | Errore: la ricerca dell'ID di accesso alternativo non è riuscita | Verificare che LDAP_ALTERNATE_LOGINID_ATTRIBUTE sia impostato tooa [attributi di active directory valido](https://msdn.microsoft.com/library/ms675090(v=vs.85).aspx). <br><br> Se LDAP_FORCE_GLOBAL_CATALOG è impostato tooTrue o LDAP_LOOKUP_FORESTS è configurato con un valore non vuoto, verificare che è stato configurato un catalogo globale e che tale attributo AlternateLoginId hello viene aggiunto tooit. <br><br> Se LDAP_LOOKUP_FORESTS è configurato con un valore non vuoto, verificare che il valore di hello sia corretto. Se è presente più di un nome di foresta, i nomi di hello devono essere separati da punti e virgola, non gli spazi. <br><br> Se questi passaggi non risolve il problema di hello, [contattare il supporto tecnico](#contact-microsoft-support) per ulteriore assistenza. |
| **ALTERNATE_LOGIN_ID_ERROR** | Errore: il valore dell'ID di accesso alternativo è vuoto | Verificare che tale attributo AlternateLoginId hello è configurato per l'utente hello. |


## <a name="errors-your-users-may-encounter"></a>Errori che possono verificarsi per gli utenti

| Codice di errore | Messaggio di errore | Passaggi per la risoluzione dei problemi |
| ---------- | ------------- | --------------------- |
| **AccessDenied** | Tenant chiamante non dispone di autenticazione toodo le autorizzazioni di accesso per utente hello | Controllare se hello dominio hello del nome dell'entità hello utente (UPN) e dominio del tenant sono hello stesso. Ad esempio, assicurarsi che user@contoso.com sta tentando di tooauthenticate toohello Contoso tenant. Hello UPN rappresenta un utente valido per il tenant di hello in Azure. |
| **AuthenticationMethodNotConfigured** | Hello specificato metodo di autenticazione non è stato configurato per l'utente hello | Dispone di utente hello aggiungere o verificare i relativi metodi di verifica in base a istruzioni toohello [gestire le impostazioni per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **AuthenticationMethodNotSupported** | Specified authentication method is not supported. (Il metodo di autenticazione specificato non è supportato.) | Raccogliere tutti i log che includono questo errore e [contattare il supporto tecnico](#contact-microsoft-support). Quando si contatta il supporto tecnico, fornire nome utente di hello e metodo di verifica secondaria hello che ha generato errore hello. |
| **BecAccessDenied** | Chiamata di MSODS Bec restituito accesso negato, probabilmente hello username non è definito nel tenant di hello | utente Hello è presente in Active Directory locale, ma non è sincronizzato in Azure Active Directory da Active Directory Connect. In alternativa, è mancante per il tenant hello utente hello. Aggiungere hello utente tooAzure AD e farsi aggiungere i propri metodi di verifica in base a istruzioni toohello [gestire le impostazioni per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-manage-settings.md). |
| **InvalidFormat** o **StrongAuthenticationServiceInvalidParameter** | numero di telefono Hello è in formato non riconoscibile | Chiedere a hello utente di correggere i numeri di telefono di verifica. |
| **InvalidSession** | Hello specificato sessione non è valida o potrebbe essere scaduto | sessione Hello è diventata più di tre minuti toocomplete. Verificare che l'utente hello è immettendo il codice di verifica hello o risponde toohello notifica dell'app, all'interno di tre minuti di avviare la richiesta di autenticazione hello. Se il problema persiste problema hello, non verificare che le latenze di rete tra endpoint di Azure MFA hello, Server NAS, Server dei criteri di rete e client.  |
| **NoDefaultAuthenticationMethodIsConfigured** | È stato configurato alcun metodo di autenticazione predefinito per l'utente hello | Dispone di utente hello aggiungere o verificare i relativi metodi di verifica in base a istruzioni toohello [gestire le impostazioni per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-manage-settings.md). Verificare che l'utente hello ha scelto un metodo di autenticazione predefinito e configurato tale metodo per il proprio account. |
| **OathCodePinIncorrect** | Wrong code and pin entered. (Codice e pin inseriti non corretti.) | Questo errore non previsto in hello estensione dei criteri di rete. Se l'utente rileva questo errore, [contattare il supporto tecnico](#contact-microsoft-support) per la risoluzione del problema. |
| **ProofDataNotFound** | Dati di prova non è stati configurati per hello specificato metodo di autenticazione. | Avere utente hello provare un altro metodo di verifica o aggiungere un nuovi metodi di verifica in base a istruzioni toohello [gestire le impostazioni per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-manage-settings.md). Se l'utente di hello continua toosee questo errore dopo aver confermato che il metodo di verifica è configurato correttamente, [contattare il supporto tecnico](#contact-microsoft-support). |
| **SMSAuthFailedWrongCodePinEntered** | Wrong code and pin entered. (Codice e pin inseriti non corretti.) (OneWaySMS) | Questo errore non previsto in hello estensione dei criteri di rete. Se l'utente rileva questo errore, [contattare il supporto tecnico](#contact-microsoft-support) per la risoluzione del problema. |
| **TenantIsBlocked** | Tenant is blocked (Il tenant è bloccato) | [Contattare il supporto tecnico](#contact-microsoft-support) con ID di Directory dalla pagina delle proprietà hello Azure AD in hello portale di Azure. |
| **UserNotFound** | non è stato possibile trovare l'utente specificato di Hello | tenant di Hello non è più visibile in Azure AD come attivo. Verificare che la sottoscrizione è attiva e si dispone di hello necessaria prima app di terze parti. Assicurarsi anche tenant hello nel soggetto del certificato hello è quello previsto e il certificato di hello è ancora valido e registrato in un'entità servizio hello. |

## <a name="messages-your-users-may-encounter-that-arent-errors"></a>Messaggi che l'utente potrebbe visualizzare ma che non sono errori

In alcuni casi, gli utenti possono ricevere messaggi da Multi-Factor Authentication in quanto la richiesta di autenticazione ha esito negativo. Non si tratta di errori nel prodotto hello della configurazione, ma sono avvisi intenzionali che spiega perché è stata negata una richiesta di autenticazione.

| Codice di errore | Messaggio di errore | Procedure consigliate | 
| ---------- | ------------- | ----------------- |
| **OathCodeIncorrect** | Wrong code entered\OATH Code Incorrect (Codice inserito non corretto\Codice OATH errato) | Non è un errore, l'utente ha immesso un codice errato. | Hello utente ha immesso il codice non corretto di hello. Fare in modo che l'utente ripeta l'operazione richiedendo un nuovo codice o effettuando di nuovo l'accesso. | 
| **SMSAuthFailedMaxAllowedCodeRetryReached** | Maximum allowed code retry reached (Numero massimo di tentativi di inserimento del codice raggiunto) | utente Hello hello richiesta di verifica non riuscita troppe volte. A seconda delle impostazioni, si potrebbe essere necessario toobe sbloccato da un amministratore ora.  |
| **SMSAuthFailedWrongCodeEntered** | Wrong code entered/Text Message OTP Incorrect (Codice inserito errato/OTP del messaggio di testo errato) | Hello utente ha immesso il codice non corretto di hello. Fare in modo che l'utente ripeta l'operazione richiedendo un nuovo codice o effettuando di nuovo l'accesso. |

## <a name="errors-that-require-support"></a>Errori per cui è necessario il supporto tecnico

Se si verifica uno di questi errori, è consigliabile [contattare il supporto tecnico](#contact-microsoft-support) per assistenza diagnostica. Non esistono procedure standard che consentono di risolvere questi errori. Quando si contatta il supporto, che tooinclude come più informazioni possibili sui passaggi hello led di errore tooan e le informazioni del tenant.

| Codice di errore | Messaggio di errore |
| ---------- | ------------- |
| **InvalidParameter** | Request must not be null (La richiesta non deve essere null) |
| **InvalidParameter** | ObjectId must not be null or empty for ReplicationScope:{0} (ObjectId non deve essere null o vuoto per ReplicationScope: {0}) |
| **InvalidParameter** | lunghezza di CompanyName Hello \{0} \ è più lungo di \\{1 \\} la lunghezza massima consentita di hello |
| **InvalidParameter** | UserPrincipalName must not be null or empty (UserPrincipalName non deve essere null o vuoto) |
| **InvalidParameter** | Hello fornito il che ID tenant non è nel formato corretto. |
| **InvalidParameter** | SessionId must not be null or empty (SessionId non deve essere null o vuoto) |
| **InvalidParameter** | Could not resolve any ProofData from request or Msods. (Impossibile risolvere ProofData dalla richiesta o Msods.) Hello ProofData è sconosciuto |
| **InternalError** |  |
| **OathCodePinIncorrect** |  |
| **VersionNotSupported** |  |
| **MFAPinNotSetup** |  |

## <a name="next-steps"></a>Passaggi successivi

### <a name="troubleshoot-user-accounts"></a>Risolvere i problemi relativi agli account utente

Se gli utenti hanno [Problemi con la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-troubleshoot.md) è necessario aiutarli a diagnosticare autonomamente i problemi. 

### <a name="contact-microsoft-support"></a>Contattare il supporto Microsoft

Se è necessario avere un maggiore supporto, contattare un tecnico del supporto tramite il [supporto del server Multi-Factor Authentication di Azure](https://support.microsoft.com/oas/default.aspx?prid=14947). Quando si contatta Microsoft, è utile includere il maggior numero possibile di informazioni relative al problema. È possibile fornire le informazioni includono pagina hello in cui si è visto errore hello, hello ID hello codice, ID di sessione specifico hello, di errore specifico dell'utente hello che visto errore hello e registri di debug.

toocollect i registri di debug per la diagnostica di supporto, usare hello alla procedura seguente: 

1. Aprire un prompt dei comandi di amministratore ed eseguire questi comandi:

   ```
   Mkdir c:\NPS
   Cd NPS
   netsh trace start Scenario=NetConnection capture=yes tracefile=c:\NPS\nettrace.etl
   logman create trace "NPSExtension" -ow -o c:\NPS\NPSExtension.etl -p {7237ED00-E119-430B-AB0F-C63360C8EE81} 0xffffffffffffffff 0xff -nb 16 16 -bs 1024 -mode Circular -f bincirc -max 4096 -ets
   logman update trace "NPSExtension" -p {EC2E6D3A-C958-4C76-8EA4-0262520886FF} 0xffffffffffffffff 0xff -ets
   ```

2. Riprodurre il problema di hello

3. Arrestare la traccia hello con questi comandi:

   ```
   logman stop "NPSExtension" -ets
   netsh trace stop
   wevtutil epl AuthNOptCh C:\NPS\%computername%_AuthNOptCh.evtx
   wevtutil epl AuthZOptCh C:\NPS\%computername%_AuthZOptCh.evtx
   wevtutil epl AuthZAdminCh C:\NPS\%computername%_AuthZAdminCh.evtx
   Start .
   ```

4. Comprimere il contenuto di hello della cartella C:\NPS hello e collegare i case di supporto toohello file hello compresso.


