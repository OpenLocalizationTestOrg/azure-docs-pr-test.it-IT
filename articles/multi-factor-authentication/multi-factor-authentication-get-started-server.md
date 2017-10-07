---
title: aaaGetting avviato il Server Azure multi-Factor Authentication | Documenti Microsoft
description: "Si tratta hello Azure multi-factor authentication pagina che descrive la modalità di avvio tooget con Azure MFA Server."
services: multi-factor-authentication
keywords: server di autenticazione, pagina di attivazione dell'app azure multi factor authentication, download server di autenticazione
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: e94120e4-ed77-44b8-84e4-1c5f7e186a6b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 92a6a586eb96375e92a9455ad64e67221001db81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-azure-multi-factor-authentication-server"></a>Introduzione a hello del Server Azure multi-Factor Authentication

<center>![MFA locale](./media/multi-factor-authentication-get-started-server/server2.png)</center>

Ora che è stato rilevato toouse multi-Factor Authentication Server locale, si continuare a lavorare. Questa pagina illustra una nuova installazione di server hello e impostarlo con Active Directory locale. Se già dispone di server di autenticazione a più fattori hello installato e si vogliono tooupgrade, vedere [toohello l'aggiornamento più recente Server Azure multi-Factor Authentication](multi-factor-authentication-server-upgrade.md). Se si sta cercando informazioni sull'installazione appena hello del servizio web, vedere [distribuzione hello Azure multi-Factor Authentication Server servizio Web App Mobile](multi-factor-authentication-get-started-server-webservice.md).

## <a name="plan-your-deployment"></a>Pianificare la distribuzione

Prima di scaricare hello del Server Azure multi-Factor Authentication, considerare quali sono i requisiti di disponibilità elevata e di carico. Utilizzare questa toodecide informazioni come e dove toodeploy.

Buona per quantità hello di memoria necessaria è il numero di hello di utenti previsti tooauthenticate a intervalli regolari.

| Utenti | RAM |
| ----- | --- |
| 1-10.000 | 4 GB |
| 10.001-50.000 | 8 GB |
| 50.001-100.000 | 12 GB |
| 100.000-200.001 | 16 GB |
| Oltre 200.001 | 32 GB |

È necessario tooset di più server per la disponibilità elevata o il bilanciamento del carico? Esistono numerosi modi tooset la configurazione con Server di autenticazione a più fattori di Azure. Quando si installa il primo Server di autenticazione a più fattori di Azure, diventa master hello. Qualsiasi server aggiuntivi diventano subordinati e sincronizzare automaticamente gli utenti e la configurazione con master hello. Quindi, è possibile configurare un server primario e il resto di hello agire come backup oppure è possibile configurare il bilanciamento del carico tra tutti i server hello.

Quando un master Azure MFA Server passa alla modalità offline, i server subordinati hello comunque possono elaborare le richieste di verifica in due passaggi. Tuttavia, non è possibile aggiungere nuovi utenti e gli utenti esistenti non è possibile aggiornare le relative impostazioni fino a quando non master hello è tornata in linea o una forma subordinata viene alzato di livello.

### <a name="prepare-your-environment"></a>Preparare l'ambiente

Verificare che server hello che si sta utilizzando per Azure multi-Factor Authentication soddisfi hello seguenti requisiti:

| Requisiti del server Azure Multi-Factor Authentication | Descrizione |
|:--- |:--- |
| Hardware |<li>200 MB di spazio su disco rigido</li><li>processore idoneo per x32 o x64</li><li>1 GB o più di RAM</li> |
| Software |<li>Windows Server 2008 o versione successiva se host hello è un server del sistema operativo</li><li>Windows 7 o versione successiva se host hello è un sistema operativo client</li><li>Microsoft .NET 4.0 Framework</li><li>IIS 7.0 o versione successiva se l'installazione di hello utente portale o il servizio web SDK</li> |

### <a name="azure-mfa-server-components"></a>Componenti del server Azure MFA

Il server Azure MFA è costituito da tre componenti Web:

* Servizio SDK - abilita la comunicazione con altri componenti di hello e viene installato nel server di applicazioni Azure MFA hello Web
* Portale per gli utenti - un sito web IIS che consente agli utenti tooenroll in Azure multi-Factor Authentication (MFA) e mantenere i propri account.
* Servizio App Web mobile - consente di usare un'app per dispositivi mobili quali app Microsoft Authenticator hello per la verifica in due passaggi.

Tutti e tre i componenti possono essere installati hello stesso server se hello server con connessione internet. Se i componenti di hello di rilievo, hello Web Service SDK viene installato nel server di applicazioni Azure MFA hello e hello portale per gli utenti e servizio Web App Mobile vengono installati in un server con connessione internet.

### <a name="azure-multi-factor-authentication-server-firewall-requirements"></a>Requisiti del firewall del server Azure Multi-Factor Authentication

Ogni server di autenticazione a più fattori devono essere in grado di toocommunicate su toohello di porta 443 in uscita seguenti indirizzi:

* https://pfd.phonefactor.net
* https://pfd2.phonefactor.net
* https://css.phonefactor.net

Se il firewall in uscita si limitazione alla porta 443, aprire hello seguenti intervalli di indirizzi IP:

| Subnet IP | Netmask | Intervallo IP |
|:---: |:---: |:---: |
| 134.170.116.0/25 |255.255.255.128 |134.170.116.1 – 134.170.116.126 |
| 134.170.165.0/25 |255.255.255.128 |134.170.165.1 – 134.170.165.126 |
| 70.37.154.128/25 |255.255.255.128 |70.37.154.129 – 70.37.154.254 |

Se non si utilizzano funzionalità di conferma evento hello e gli utenti non usano l'App per dispositivi mobili tooverify dai dispositivi nella rete aziendale hello, è necessario solo hello intervalli seguenti:

| Subnet IP | Netmask | Intervallo IP |
|:---: |:---: |:---: |
| 134.170.116.72/29 |255.255.255.248 |134.170.116.72 – 134.170.116.79 |
| 134.170.165.72/29 |255.255.255.248 |134.170.165.72 – 134.170.165.79 |
| 70.37.154.200/29 |255.255.255.248 |70.37.154.201 – 70.37.154.206 |

## <a name="download-hello-azure-multi-factor-authentication-server"></a>Scaricare hello del Server Azure multi-Factor Authentication

1. Accedi toohello [portale di Azure](https://portal.azure.com) come amministratore.
2. A sinistra di hello, selezionare **Active Directory**
3. Fare clic su **Utenti e gruppi**.
4. Fare clic su **Tutti gli utenti**.
5. Fare clic su **Multi-Factor Authentication**.
6. Nella sezione **Multi-Factor Authentication** selezionare **Impostazioni servizio**.

   ![Pagina Impostazioni servizio](./media/multi-factor-authentication-get-started-server/servicesettings.png)

6. Nella pagina Impostazioni servizi hello in basso hello hello fare clic su **Go toohello portale**. Viene aperta una nuova pagina.
7. Fare clic su **Download**.
8. Fare clic su hello **scaricare** collegamento e il salvataggio di programma di installazione hello.

   ![Download del server MFA](./media/multi-factor-authentication-get-started-server/download4.png)

9. Tenere aperta questa pagina come si farà riferimento tooit dopo l'installazione di hello in esecuzione.

## <a name="install-and-configure-hello-azure-multi-factor-authentication-server"></a>Installare e configurare hello del Server Azure multi-Factor Authentication

Ora che sono stati scaricati server hello è possibile installare e configurare. Assicurarsi che tale server hello in che si installa soddisfi i requisiti elencati nella sezione hello.

1. Fare doppio clic sul file eseguibile hello.
2. Nella schermata di selezione cartella di installazione di hello, assicurarsi che tale cartella hello sia corretto e fare clic su **Avanti**.
3. Al termine dell'installazione di hello, fare clic su **fine**.  verrà avviata Hello configurazione guidata.
4. Nella schermata iniziale di hello configurazione guidata: controllo **Skip utilizzando hello configurazione guidata autenticazione** e fare clic su **Avanti**.  procedura guidata Hello e hello server viene avviato.

   ![Cloud](./media/multi-factor-authentication-get-started-server/skip2.png)

5. Tornare nella pagina di hello che sono state scaricate dal server di hello, fare clic su hello **generare le credenziali di attivazione** pulsante. Copiare queste informazioni in hello Azure MFA Server nelle caselle hello fornite e fare clic su **attiva**.

## <a name="send-users-an-email"></a>Inviare agli utenti un messaggio di posta elettronica

implementazione di tooease, consentire toocommunicate Server MFA con gli utenti. Server di autenticazione a più fattori può inviare un messaggio di posta elettronica tooinform loro che sono stati registrati per la verifica in due passaggi.

si invia posta elettronica di Hello deve essere determinata dai come configurare gli utenti per la verifica in due passaggi. Ad esempio, se si è in grado di tooimport i numeri di telefono dalla directory aziendale hello, posta elettronica hello deve includere i numeri di telefono predefinito hello in modo che gli utenti sappiano quali tooexpect. Se non si importa i numeri di telefono o gli utenti verranno toouse hello app per dispositivi mobili, inviare un messaggio di posta elettronica per invitarli toocomplete registrazione del loro account. Includere toohello un collegamento ipertestuale portale utenti Azure multi-Factor Authentication nel messaggio di posta elettronica hello.

contenuto di Hello del messaggio di posta elettronica hello varia anche in base al metodo hello di verifica che è stata impostata per l'utente hello (telefonata, SMS o app per dispositivi mobili).  Ad esempio, se utente hello toouse richiesto un PIN quando eseguono l'autenticazione, posta elettronica hello indica ciò che il PIN iniziale è stato impostato su.  Gli utenti è necessari toochange il proprio PIN durante la verifica prima.

### <a name="configure-email-and-email-templates"></a>Configurare l'indirizzo di posta elettronica e i modelli di messaggio di posta elettronica

Fare clic sul messaggio di posta elettronica di hello sulla hello tooset sinistro impostazioni hello per l'invio di questi messaggi di posta elettronica. Questa pagina è in cui è possibile immettere informazioni hello SMTP di posta elettronica di server e inviare la posta elettronica controllando hello **invia messaggi di posta elettronica toousers** casella di controllo.

![Configurazione della posta elettronica per il server MFA](./media/multi-factor-authentication-get-started-server/email1.png)

Nella scheda contenuto messaggio hello, è possibile visualizzare i modelli di messaggio di posta elettronica hello toochoose disponibile da. A seconda di come sono stati configurati la verifica in due passaggi tooperform di utenti, scegliere modello hello adatta alle proprie esigenze.

![Modelli di posta elettronica per il server MFA](./media/multi-factor-authentication-get-started-server/email2.png)

## <a name="import-users-from-active-directory"></a>Importare gli utenti da Active Directory

Ora è installato il server di hello è tooadd utenti. È possibile scegliere toocreate manualmente, importare utenti da Active Directory, o configurare la sincronizzazione automatica con Active Directory.

### <a name="manual-import-from-active-directory"></a>Importazione manuale da Active Directory

1. In hello Azure MFA Server, a sinistra di hello, selezionare **utenti**.
2. Nella parte inferiore di hello, selezionare **Importa da Active Directory**.
3. Ora è possibile eseguire una ricerca per singoli utenti o hello ricerca directory di Active Directory per unità organizzative con utenti in essi contenuti.  In questo caso, si specifica unità Organizzativa utenti hello.
4. Evidenziare tutti gli utenti hello hello destra e fare clic su **importazione**.  Verrà visualizzata una finestra popup che informa che tutte le operazioni sono state eseguite correttamente.  Finestra di importazione hello Chiudi.

   ![Importazione di utenti nel server MFA](./media/multi-factor-authentication-get-started-server/import2.png)

### <a name="automated-synchronization-with-active-directory"></a>Sincronizzazione automatica con Active Directory

1. In hello Azure MFA Server, a sinistra di hello, selezionare **integrazione Directory**.
2. Passare toohello **sincronizzazione** scheda.
3. Nella parte inferiore di hello, scegliere **Aggiungi**
4. In hello **Aggiungi elemento di sincronizzazione** visualizzata scegliere hello dominio, OU **o** gruppo di sicurezza, le impostazioni, impostazioni predefinite metodo e linguaggio predefinito per la sincronizzazione di attività e fare clic su **Aggiungere**.
5. Casella di controllo hello denominata **Abilita sincronizzazione con Active Directory** e scegliere un **l'intervallo di sincronizzazione** tra un minuto e 24 ore.

## <a name="how-hello-azure-multi-factor-authentication-server-handles-user-data"></a>La modalità di gestione di dati utente hello del Server Azure multi-Factor Authentication

Quando si utilizzano il Server multi-Factor Authentication (MFA) hello in locale, i dati di un utente vengono archiviati in server locali hello. Nessun dato utente persistente viene archiviato nel cloud hello. Quando l'utente hello esegue una verifica in due passaggi, hello Server MFA invia dati toohello verifica del hello tooperform servizio cloud Azure MFA. Quando queste richieste di autenticazione vengono inviate servizio cloud toohello, hello campi seguenti vengono inviati nella richiesta di hello e registri in modo che siano disponibili nei report di autenticazione/utilizzo del cliente hello. Alcuni dei campi hello sono facoltativi, pertanto possono essere abilitati o disabilitati nel Server multi-Factor Authentication hello. comunicazione Hello dal servizio cloud MFA toohello di MFA Server hello utilizza SSL/TLS sulla porta 443 in uscita. Questi campi sono:

* ID univoco: nome utente o ID interno del MFA
* Nome e cognome (facoltativo)
* Indirizzo di posta elettronica (facoltativo)
* Numero di telefono: quando si esegue una chiamata vocale o l'autenticazione tramite SMS
* Token del dispositivo: quando si esegue l'autenticazione con l'app per dispositivi mobili
* Modalità di autenticazione
* Risultato dell'autenticazione
* Nome del server MFA
* IP del server MFA
* IP client: se disponibile

Inoltre, toohello campi sopra indicati, il risultato di verifica hello (esito positivo/rifiuto) e il motivo di eventuali rifiuti è anche archiviati con i dati di autenticazione hello e sono disponibili tramite i report di autenticazione/utilizzo hello.

## <a name="back-up-and-restore-azure-mfa-server"></a>Eseguire il backup e il ripristino del server Azure MFA

Assicurarsi di disporre di un backup valido è un passaggio importante di tootake con qualsiasi sistema.

tooback di Server di autenticazione a più fattori di Azure, verificare di disporre di una copia di hello **c:\Programmi\Microsoft multi-Factor Authentication Server\Data** cartella inclusi hello **PhoneFactor.pfdata** file. 

In caso di un ripristino è necessario hello completo come segue:

1. Reinstallare il server Azure MFA in un nuovo server.
2. Attivare hello nuovo Server di autenticazione a più fattori di Azure.
3. Arresto hello **MultiFactorAuth** servizio.
4. Sovrascrivere hello **PhoneFactor.pfdata** con hello copia il backup.
5. Avviare hello **MultiFactorAuth** servizio.

nuovo server Hello è ora installato e in esecuzione con hello originali backup configurazione e i dati utente.

## <a name="next-steps"></a>Passaggi successivi

- Installare e configurare hello [portale per gli utenti](multi-factor-authentication-get-started-portal.md) per l'utente self-service.
- Installare e configurare Azure MFA Server con hello [Active Directory Federation Services](multi-factor-authentication-get-started-adfs.md), [l'autenticazione RADIUS](multi-factor-authentication-get-started-server-radius.md), o [autenticazione LDAP](multi-factor-authentication-get-started-server-ldap.md).
- Installare e configurare [Gateway Desktop remoto e server Azure Multi-Factor Authentication utilizzando RADIUS](multi-factor-authentication-get-started-server-rdg.md).
- [Distribuire hello Azure multi-Factor Authentication Server servizio Web App Mobile](multi-factor-authentication-get-started-server-webservice.md).
- [Scenari avanzati con Azure Multi-Factor Authentication e soluzioni VPN di terze parti](multi-factor-authentication-advanced-vpn-configurations.md).
