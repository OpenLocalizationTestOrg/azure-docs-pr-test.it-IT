---
title: portale aaaUser per Azure MFA Server | Documenti Microsoft
description: "Si tratta hello Azure multi-factor authentication pagina che descrive la modalità di avvio tooget con autenticazione a più fattori di Azure e il portale per gli utenti hello."
services: multi-factor-authentication
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 06b419fa-3507-4980-96a4-d2e3960e1772
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 0e36644c3d780249fb98d5da654e9d267c63561a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="user-portal-for-hello-azure-multi-factor-authentication-server"></a>Portale per gli utenti per hello del Server Azure multi-Factor Authentication

portale per gli utenti Hello è un sito web IIS che consente agli utenti tooenroll in Azure multi-Factor Authentication (MFA) e mantenere i propri account. Un utente può modificare il numero di telefono, modificare il PIN o scegliere toobypass verifica in due passaggi durante il successivo accesso.

Gli utenti accedere toohello portale per gli utenti con il normale nome utente e la password, quindi completano una chiamata di verifica in due passaggi o rispondere toocomplete domande di sicurezza l'autenticazione. Se è consentita la registrazione, gli utenti configura il numero di telefono e hello PIN prima volta, che effettuano l'accesso nel portale per gli utenti toohello.

Portale per gli utenti amministratori può essere impostato e concesse autorizzazioni tooadd nuovi utenti e aggiorna utenti esistenti.

A seconda dell'ambiente, è opportuno portale per gli utenti hello toodeploy su hello nello stesso server come Server Azure multi-Factor Authentication o in un altro server con connessione internet.

![Portale utenti di MFA](./media/multi-factor-authentication-get-started-portal/portal.png)

> [!NOTE]
> portale per gli utenti Hello è disponibile solo con Server multi-Factor Authentication. Se si usa multi-Factor Authentication nel cloud hello, consultare il toohello utenti [l'account per la verifica in due passaggi di configurazione](./end-user/multi-factor-authentication-end-user-first-time.md) o [gestire le impostazioni per la verifica in due passaggi](./end-user/multi-factor-authentication-end-user-manage-settings.md).

## <a name="install-hello-web-service-sdk"></a>Installare il SDK servizi web di hello

In entrambi gli scenari, se hello Azure multi-Factor Authentication Web Service SDK è **non** già installati nel Server Azure multi-Factor Authentication (MFA) hello, hello completato i passaggi che seguono.

1. Aprire la console di Server multi-Factor Authentication hello.
2. Passare toohello **Web Service SDK** e selezionare **installare Web Service SDK**.
3. Installazione completa di hello utilizzando le impostazioni predefinite di hello a meno che non è necessario toochange per qualche motivo.
4. Associare un sito di toohello certificato SSL in IIS.

Se hai domande sulla configurazione di un certificato SSL in un server IIS, vedere l'articolo hello [come configurare SSL in IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

Hello Web Service SDK deve essere protetto con un certificato SSL. Un certificato autofirmato è accettabile per questo scopo. Importare il certificato di hello nell'archivio "Autorità di certificazione" hello dell'account Computer locale hello server web del portale per gli utenti hello in modo da considerare attendibile tale certificato quando si avvia una connessione SSL hello.

![Configurazione del server MFA, SDK servizio Web](./media/multi-factor-authentication-get-started-portal/sdk.png)

## <a name="deploy-hello-user-portal-on-hello-same-server-as-hello-azure-multi-factor-authentication-server"></a>Distribuire il portale utenti hello in hello nello stesso server hello del Server Azure multi-Factor Authentication

i prerequisiti seguenti Hello sono portale per gli utenti hello tooinstall necessari su hello **nello stesso server** come hello del Server Azure multi-Factor Authentication:

* IIS con ASP.NET e la compatibilità della metabase di IIS 6 (per IIS 7 o versione successiva).
* Un account con diritti di amministratore per il computer di hello e il dominio, se applicabile. account di Hello richiede gruppi di sicurezza di Active Directory toocreate autorizzazioni.
* Hello sicura portale per gli utenti con un certificato SSL.
* Proteggere hello Azure multi-Factor Authentication Web Service SDK con un certificato SSL.

toodeploy hello seguire portale utente questi passaggi:

1. Aprire la console di hello del Server Azure multi-Factor Authentication, fare clic su hello **portale per gli utenti** icona in hello dal menu a sinistra, quindi fare clic su **installa portale utenti**.
2. Installazione completa di hello utilizzando le impostazioni predefinite di hello a meno che non è necessario toochange per qualche motivo.
3. Associare un sito toohello certificato SSL in IIS

   > [!NOTE]
   > Il certificato SSL è in genere un certificato SSL firmato pubblicamente.

4. Aprire un web browser da qualsiasi computer, quindi spostarsi toohello URL in cui è stato installato il portale per gli utenti hello (esempio: https://mfa.contoso.com/MultiFactorAuth). Assicurarsi che non vengano visualizzati errori o avvisi relativi al certificato.

![Installazione del portale utenti del server MFA](./media/multi-factor-authentication-get-started-portal/install.png)

Se hai domande sulla configurazione di un certificato SSL in un server IIS, vedere l'articolo hello [come configurare SSL in IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="deploy-hello-user-portal-on-a-separate-server"></a>Distribuire il portale utenti hello in un server separato

Se server hello in cui è in esecuzione il Server Azure multi-Factor Authentication non è rivolto a internet, è necessario installare il portale utenti hello in un **server separato, con connessione internet**.

Se l'organizzazione Usa hello app Authenticator Microsoft come uno dei metodi di verifica hello e toodeploy hello utente portale nel proprio server, completare hello seguenti requisiti:

* Utilizzare versione 6.0 o versione successiva di hello del Server Azure multi-Factor Authentication.
* Installare portale per gli utenti hello in un server web con connessione internet che esegue Microsoft internet Information Services (IIS) 6. x o versione successiva.
* Quando si utilizza IIS 6. x, verificare che ASP.NET v 2.0.50727 è installato, registrato e impostato troppo**consentito**.
* Quando si usa IIS 7.x o versione successiva, IIS, che include l'autenticazione di base, ASP.NET e la compatibilità della metabase di IIS 6.
* Hello sicura portale per gli utenti con un certificato SSL.
* Proteggere hello Azure multi-Factor Authentication Web Service SDK con un certificato SSL.
* Verificare che il portale utente hello può connettersi toohello Azure multi-Factor Authentication Web Service SDK tramite SSL.
* Verificare che il portale utente hello in grado di autenticare toohello Azure multi-Factor Authentication Web Service SDK usando le credenziali di hello di un account di servizio nel gruppo di sicurezza "PhoneFactor Admins" hello. Questo account del servizio e il gruppo devono essere presenti in Active Directory se hello del Server Azure multi-Factor Authentication è in esecuzione in un server di dominio. Questo account del servizio e il gruppo esistono in locale sul Server Azure multi-Factor Authentication hello in caso contrario tooa aggiunti a un dominio.

Portale utenti di hello l'installazione in un server diverso dal Server Azure multi-Factor Authentication hello richiede hello alla procedura seguente:

1. **Nel Server di autenticazione a più fattori hello**, individuare il percorso di installazione toohello (esempio: c:\Programmi\Microsoft multi-Factor Authentication Server) e copiare file hello **MultiFactorAuthenticationUserPortalSetup64** tooa percorso server di accesso a internet toohello accessibile in cui verrà installato.
2. **Server web con connessione internet hello**, eseguire il file di installazione MultiFactorAuthenticationUserPortalSetup64 hello come amministratore, se si desidera modificare hello del sito e modificare nome breve tooa directory virtuale hello se si desidera.
3. Associare un sito di toohello certificato SSL in IIS.

   > [!NOTE]
   > Il certificato SSL è in genere un certificato SSL firmato pubblicamente.

4. Sfoglia troppo**C:\inetpub\wwwroot\MultiFactorAuth**
5. Modificare il file Web. config hello nel blocco note

    * Trovare la chiave di hello **"USE_WEB_SERVICE_SDK"** e modificare **valore = "false"** troppo**valore = "true"**
    * Trovare la chiave di hello **"WEB_SERVICE_SDK_AUTHENTICATION_USERNAME"** e modificare **valore = ""** troppo**valore = "Dominio\nomeutente"** dove dominio\utente è un Account del servizio che fa parte di Gruppo "Amministratori di PhoneFactor".
    * Trovare la chiave di hello **"WEB_SERVICE_SDK_AUTHENTICATION_PASSWORD"** e modificare **valore = ""** troppo**valore = "Password"** in cui Password è hello per hello servizio Account specificato nella riga precedente hello.
    * Trovare il valore di hello **https://www.contoso.com/MultiFactorAuthWebServiceSdk/PfWsSdk.asmx** e modificare questo toohello URL segnaposto URL del servizio Web SDK è installati nel passaggio 2.
    * Salvare i file Web. config hello e chiudere il blocco note.

6. Aprire un web browser da qualsiasi computer, quindi spostarsi toohello URL in cui è stato installato il portale per gli utenti hello (esempio: https://mfa.contoso.com/MultiFactorAuth). Assicurarsi che non vengano visualizzati errori o avvisi relativi al certificato.

Se hai domande sulla configurazione di un certificato SSL in un server IIS, vedere l'articolo hello [come configurare SSL in IIS tooSet](https://docs.microsoft.com/en-us/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## <a name="configure-user-portal-settings-in-hello-azure-multi-factor-authentication-server"></a>Configurare impostazioni del portale utenti in hello del Server Azure multi-Factor Authentication

Ora è installato il portale utente hello, è necessario tooconfigure hello del Server Azure multi-Factor Authentication toowork con il portale di hello.

1. Nella console di hello del Server Azure multi-Factor Authentication, fare clic su hello **portale per gli utenti** icona. Nella scheda Impostazioni hello immettere portale per gli utenti toohello URL hello in hello **URL portale utenti** casella di testo. Se è stata abilitata la funzionalità di posta elettronica, questo URL è incluso nei messaggi hello inviati toousers quando vengono importati in hello del Server Azure multi-Factor Authentication.
2. Scegliere le impostazioni di hello che si desidera toouse in hello portale per gli utenti. Ad esempio, se gli utenti sono autorizzati toochoose i propri metodi di autenticazione, assicurarsi che **consentire agli utenti il metodo tooselect** è selezionata, insieme ai metodi hello che possono scegliere.
3. Definire che devono essere gli amministratori in hello **amministratori** scheda. È possibile creare autorizzazioni amministrative granulari utilizzando le caselle di controllo di hello ed elenchi a discesa nelle caselle Aggiungi/modifica hello.

Configurazione facoltativa:
- **Domande di sicurezza** -definire approvato domande di sicurezza per la lingua di ambiente e hello appaiono in.
- **Sessioni passate**: configurare l'integrazione del portale utenti con un sito Web basato su form tramite MFA.
- **Indirizzi IP attendibili** -Consenti agli utenti tooskip autenticazione a più fattori quando l'autenticazione da un elenco di attendibili gli indirizzi IP o intervalli.

![Configurazione del portale utenti del server MFA](./media/multi-factor-authentication-get-started-portal/config.png)

Azure multi-Factor Authentication server fornisce diverse opzioni per il portale utenti hello. Hello nella tabella seguente fornisce un elenco di queste opzioni e una spiegazione di vengono utilizzati per.

| Impostazioni del portale utenti | Descrizione |
|:--- |:--- |
| URL portale utenti | Immettere l'URL di hello di in cui è ospitato il portale di hello. |
| Autenticazione primaria | Specificare il tipo di hello di toouse di autenticazione per la firma nel portale toohello. Autenticazione di Windows, Radius o LDAP. |
| Consenti toolog gli utenti in | Consente agli utenti tooenter un nome utente e password nel hello-pagina di accesso per il portale utenti hello. Se questa opzione non è selezionata, le caselle di hello sono disattivate. |
| Consenti registrazione utente | Consente un tooenroll utente multi-Factor Authentication eseguendo tooa schermata che richiede l'immissione di informazioni aggiuntive, ad esempio il numero di telefono. Richiedi telefono di backup consente agli utenti toospecify un numero di telefono secondario. Prompt dei comandi per terze parti token OATH consente a utenti toospecify un token OATH di terze parti. |
| Consentire agli utenti tooinitiate Bypass monouso | Consentire agli utenti tooinitiate un bypass monouso. Se l'utente imposta questa opzione, sarà necessario hello effetto tempo successivo accesso dell'utente hello. Richiedi bypass secondi fornisce hello utente una casella in modo che potranno modificare predefinito hello è 300 secondi. In caso contrario, bypass monouso hello è valido solo per 300 secondi. |
| Consentire agli utenti tooselect (metodo) | Consentire agli utenti toospecify il metodo di contatto primario. Il metodo può essere una telefonata, un SMS, un'app per dispositivi mobili o un token OATH. |
| Consentire agli utenti di lingua tooselect | Consentire agli utenti di lingua hello toochange utilizzata per hello telefonata, SMS, app mobile o token OATH. |
| Consentire agli utenti tooactivate app per dispositivi mobili | Consentire a utenti toogenerate un attivazione codice toocomplete hello app per dispositivi mobili Attivazione processo che viene utilizzato con server hello.  È inoltre possibile impostare il numero di hello di dispositivi che possono attivare app hello in, compreso tra 1 e 10. |
| Usa domande di sicurezza per il fallback | Consente le domande di sicurezza in caso di esito negativo della verifica in due passaggi. È possibile specificare il numero di hello di domande di sicurezza che è necessario rispondere correttamente. |
| Consenti token OATH di terze parti tooassociate utenti | Consentire agli utenti toospecify un token OATH di terze parti. |
| Usa token OATH per fallback | Consentire hello uso di un token OATH nel caso in cui la verifica non è riuscita. È anche possibile specificare hello timeout della sessione in minuti. |
| Abilitazione della registrazione | Abilitare la registrazione nel portale per gli utenti hello. Hello i file di log si trovano in: c:\Programmi\Microsoft multi-Factor Authentication Server\Logs.. |

Queste impostazioni diventano visibili toohello utente nel portale di hello dopo che sono abilitate e che si sarà connesso toohello portale per gli utenti.

![Impostazioni del portale utenti](./media/multi-factor-authentication-get-started-portal/portalsettings.png)

### <a name="self-service-user-enrollment"></a>Registrazione utente in modalità self-service

Se si desidera che il toosign gli utenti e si registra, è necessario selezionare hello **consentire toolog gli utenti in** e **Consenti registrazione utente** opzioni nella scheda Impostazioni hello. Tenere presente che le impostazioni di hello selezionate interessano esperienza di accesso utente hello.

Ad esempio, quando un utente accede toohello portale per gli utenti per hello prima volta, viene visualizzata toohello pagina di configurazione di utenti di Azure multi-Factor Authentication. A seconda di come sono stati configurati Azure multi-Factor Authentication, hello utente può essere in grado di tooselect il metodo di autenticazione.

Se si seleziona metodo di verifica hello telefonata o sono stati configurati in precedenza toouse tale metodo, la pagina di hello richiede hello utente tooenter il numero di telefono principale e l'interno, se applicabile. Possono inoltre essere un numero di telefono di backup consentito tooenter.

![Registrare i numeri di telefono principale e di backup](./media/multi-factor-authentication-get-started-portal/backupphone.png)

Se l'utente hello è toouse richiesto un PIN quando eseguono l'autenticazione, pagina hello richiede l'immissione toocreate un PIN. Dopo aver immesso i numeri di telefono e il PIN (se applicabile), hello scelto hello **chiamare Me ora tooAuthenticate** pulsante. Azure multi-Factor Authentication esegue il numero di telefono principale dell'utente di toohello verifica telefonata. Hello è necessario rispondere hello telefonata e immettere il PIN (se applicabile) e premere # toomove toohello il passaggio successivo del processo di autoregistrazione hello.

Se l'utente di hello Seleziona metodo di verifica SMS hello o è stato preconfigurato toouse tale metodo, pagina hello richiesto hello il numero di telefono cellulare. Se l'utente hello è toouse richiesto un PIN quando eseguono l'autenticazione, pagina hello inoltre richiede l'immissione tooenter un PIN.  Dopo aver immesso il numero di telefono e il PIN (se applicabile), hello scelto hello **testo Me ora tooAuthenticate** pulsante. Azure multi-Factor Authentication esegue cellulare dell'utente un SMS verifica toohello. utente Hello riceve il messaggio di testo hello con un unico-tempo-passcode (OTP), quindi il messaggio toohello risposte con l'OTP più il PIN (se applicabile).

![SMS del portale utenti](./media/multi-factor-authentication-get-started-portal/text.png)

Se l'utente di hello Seleziona metodo di verifica App Mobile hello, pagina hello richiede hello utente tooinstall hello Microsoft Authenticator app sul dispositivo e generare un codice di attivazione. Dopo aver installato l'applicazione hello, hello pulsante hello genera codice di attivazione.

> [!NOTE]
> app di Microsoft Authenticator hello toouse, è necessario abilitare le notifiche push per il dispositivo utente hello.

Nella pagina Hello verrà visualizzato un codice di attivazione e un URL con un codice a barre. Se l'utente hello è toouse richiesto un PIN quando eseguono l'autenticazione, pagina hello inoltre richiede l'immissione tooenter un PIN. utente Hello immette il codice di attivazione hello e l'URL nell'app Authenticator Microsoft hello o utilizza hello scanner tooscan hello codice a barre a barre e fa clic sul pulsante Attiva hello.

Al termine dell'attivazione di hello, utente hello sceglie hello **autenticare questo punto** pulsante. Azure multi-Factor Authentication esegue l'app mobile dell'utente toohello di verifica. Hello è necessario immettere il PIN (se applicabile) e premere toohello il passaggio successivo del processo di autoregistrazione hello pulsante Esegui autenticazione hello in toomove le app per dispositivi mobili.

Se gli amministratori di hello hanno domande e risposte hello del Server Azure multi-Factor Authentication toocollect sicurezza, hello viene visualizzata pagina domande di sicurezza toohello. Hello è necessario selezionare quattro domande di sicurezza e fornire risposte alle domande tootheir selezionato.

![Domande di sicurezza del portale utenti](./media/multi-factor-authentication-get-started-portal/secq.png)

registrazione automatica Hello è stata completata e hello utente è connesso nel portale per gli utenti toohello. Gli utenti accedere di nuovo portale per gli utenti toohello in qualsiasi momento nel futuro toochange di hello i relativi numeri di telefono, pin, metodi di autenticazione e domande di sicurezza se i relativi metodi di modifica è consentita dagli amministratori.

## <a name="next-steps"></a>Passaggi successivi

- [Distribuire hello Azure multi-Factor Authentication Server servizio Web App Mobile](multi-factor-authentication-get-started-server-webservice.md)
