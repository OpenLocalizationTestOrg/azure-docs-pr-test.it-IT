---
title: aaaSecurity considerazioni per il Proxy di applicazione Azure AD | Documenti Microsoft
description: Tratta considerazioni relative alla sicurezza quando si usa il proxy applicazione di Azure AD
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/03/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ebd14b9d1fc8f4629c5916e5a910595727d935d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="security-considerations-for-accessing-apps-remotely-with-azure-ad-application-proxy"></a>Considerazioni relative alla sicurezza quando si accede alle app in remoto usando il proxy applicazione di Azure AD

Questo articolo spiega come il proxy di applicazione di Azure Active Directory fornisca un servizio sicuro per la pubblicazione e l'accesso alle applicazioni in remoto.

Hello seguente diagramma illustra come Azure AD consente alle applicazioni locali di tooyour di accesso remoto sicuro.

 ![Diagramma dell'accesso remoto sicuro con il proxy applicazione di Azure AD](./media/application-proxy-security-considerations/secure-remote-access.png)

## <a name="security-benefits"></a>Vantaggi di sicurezza

Proxy dell'applicazione Azure AD offre hello vantaggi di sicurezza seguenti:

### <a name="authenticated-access"></a>Accesso autenticato 

Se si sceglie toouse Azure Active Directory la preautenticazione, solo le connessioni autenticate possono accedere alla rete.

Proxy dell'applicazione Azure Active Directory si basa su hello Azure AD servizio token di sicurezza (STS) per tutte le autenticazioni.  La preautenticazione, per sua stessa natura, impedisce a un numero significativo di attacchi di tipo anonimi, poiché solo identità autenticate possono accedere a un'applicazione hello back-end.

Se si sceglie Pass-through come metodo di preautenticazione, non si otterrà questo vantaggio. 

### <a name="conditional-access"></a>Accesso condizionale

Applicare più controlli dei criteri prima di connessioni vengono stabilite tooyour rete.

Con [accesso condizionale](active-directory-conditional-access-azuread-connected-apps.md), è possibile definire restrizioni per il traffico viene consentito tooaccess le applicazioni back-end. È possibile, ad esempio, creare criteri per definire restrizioni in base alla posizione, al livello di autenticazione e al profilo di rischio.

È anche possibile utilizzare criteri di accesso condizionale tooconfigure multi-Factor Authentication aggiunta di un altro livello di autenticazioni tooyour di sicurezza. 

### <a name="traffic-termination"></a>Terminazione di traffico

Tutto il traffico viene chiusa in cloud hello.

Poiché Azure AD applicazione Proxy è un proxy inverso, tutte le applicazioni di traffico tooback-end viene terminata nel servizio hello. Hello sessione può ottenere ristabilita solo con i server back-end hello, che significa che i server back-end non sono esposti traffico toodirect HTTP. Questa configurazione consente una protezione migliore da attacchi mirati.

### <a name="all-access-is-outbound"></a>Tutti gli accessi sono in uscita 

Rete aziendale toohello di tooopen le connessioni in entrata non è necessario.

Connettori Proxy di applicazione utilizzano solo le connessioni in uscita toohello AD Azure Proxy applicazione del servizio, il che significa che non è necessario tooopen le porte del firewall per le connessioni in ingresso. Proxy tradizionale è necessaria una rete perimetrale (nota anche come *DMZ*, *DMZ*, o *subnet schermata*) e toounauthenticated di accesso è consentito connessioni sul bordo rete hello. Questo scenario richiesto molti investimento aggiuntivo nell'applicazione web firewall traffico tooanalyze prodotti e offerta aggiunta protezioni toohello ambiente. Con il proxy applicazione non è necessario disporre di una rete perimetrale perché tutte le connessioni sono in uscita e su un canale sicuro.

Per altre informazioni sui connettori, vedere [Understand Azure AD Application Proxy connectors](application-proxy-understand-connectors.md) (Informazioni sui connettori proxy di applicazione di Azure AD).

### <a name="cloud-scale-analytics-and-machine-learning"></a>Machine Learning e analisi di livello cloud 

Ottenere una protezione all'avanguardia.

Perché è parte di Azure Active Directory, è possibile sfruttare il Proxy di applicazione [Azure AD Identity Protection](active-directory-identityprotection.md), con Business intelligence basate su learning macchina e dati di Microsoft Security Response Center hello e Digital Crimes Unit. Insieme identifichiamo in modo proattivo gli account compromessi e offriamo una protezione in tempo reale contro gli accessi ad alto rischio. Vengono presi in considerazione diversi fattori, ad esempio l'accesso da dispositivi infetti e tramite reti anonime, da posizioni atipiche e improbabili.

Molti di questi eventi e segnalazioni sono già disponibili tramite un'API per l'integrazione con i sistemi SIEM (Security Information and Event Management, Sistema di gestione delle informazioni e degli eventi di sicurezza).

### <a name="remote-access-as-a-service"></a>Accesso remoto come servizio

Non è necessario tooworry sulla manutenzione e l'applicazione di patch ai server locali.

Il software senza patch è tuttora responsabile di un numero elevato di attacchi. Proxy dell'applicazione AD Azure è un servizio di su scala Internet di proprietà Microsoft, pertanto sarà sempre gli aggiornamenti e patch di sicurezza più recenti di hello.

sicurezza di hello tooimprove di applicazioni pubblicate dal Proxy di applicazione AD Azure, è bloccata robot crawler dall'indicizzazione e l'archiviazione delle applicazioni. Ogni volta che un robot dell'agente di ricerca Web prova a recuperare le impostazioni dei robot per un'app pubblicata, il proxy applicazione risponde con un file robots.txt che include `User-agent: * Disallow: /`.

## <a name="under-hello-hood"></a>Quinte hello

Il proxy applicazione di Azure AD è costituito da due parti:

* Hello servizio basato sul cloud: questo servizio in esecuzione in Azure e in cui vengono eseguite le connessioni client esterne e utenti hello.
* [Hello connettore locale](application-proxy-understand-connectors.md): un componente di on-premise, connettore hello ascolta le richieste dal servizio Proxy di applicazione hello Azure AD e gestisce le applicazioni interne toohello di connessioni. 

Un flusso tra il connettore hello e servizio Proxy applicazione hello viene stabilito quando:

* connettore Hello viene prima configurato.
* connettore Hello reperisce le informazioni di configurazione dal servizio Proxy applicazione hello.
* Un utente accede a un'applicazione pubblicata.

>[!NOTE]
>Si verificano tutte le comunicazioni su SSL e sempre provengono in hello connettore toohello servizio Proxy di applicazione. servizio Hello è solo in uscita.

connettore di Hello utilizza toohello di tooauthenticate un certificato client del servizio Proxy di applicazione per quasi tutte le chiamate. Hello solo eccezione toothis processo è il passaggio di configurazione iniziale di hello, in cui è stato stabilito certificato client hello.

### <a name="installing-hello-connector"></a>Installazione di connector hello

Quando il connettore hello prima di tutto è configurato, hello dopo gli eventi di flusso si verificano:

1. il servizio Hello connettore registrazione toohello avviene come parte dell'installazione di hello del connettore hello. Gli utenti vengono richieste tooenter le proprie credenziali di amministratore di Azure AD. Il token acquisito da questa autenticazione viene quindi presentato servizio Proxy di applicazione AD Azure toohello.
2. servizio Proxy applicazione Hello valuta token hello. Assicura che l'utente hello sia un amministratore della società all'interno di tenant hello che hello token emesso per. Se l'utente hello non è un amministratore, viene terminato il processo di hello.
3. connettore Hello genera una richiesta di certificato client e lo passa, insieme a toohello token, hello servizio Proxy di applicazione. servizio Hello a sua volta verifica token hello e hello richiesta di certificato client.
4. connettore di Hello utilizza certificato client hello per le comunicazioni future con hello servizio Proxy di applicazione.
5. connettore Hello esegue un recupero iniziale dei dati di configurazione di sistema hello dal servizio di hello utilizzando il certificato client ed è ora pronto tootake richieste.

### <a name="updating-hello-configuration-settings"></a>Aggiornamento delle impostazioni di configurazione hello

Ogni volta che il servizio Proxy di applicazione hello Aggiorna le impostazioni di configurazione di hello, vengono eseguite hello eventi di flusso seguente:

1. connettore di Hello connette toohello endpoint di configurazione all'interno di hello servizio Proxy di applicazione utilizzando il certificato client.
2. Dopo la convalida di certificati client hello, hello servizio Proxy applicazione restituisce connettore toohello dati di configurazione (ad esempio, gruppo di connettori hello che hello connettore deve essere parte di).
3. Se il certificato corrente hello è più di 180 giorni, connettore hello genera una nuova richiesta di certificato, che aggiorna in modo efficace i certificati client hello ogni 180 giorni.

### <a name="accessing-published-applications"></a>Accesso alle applicazioni pubblicate

Quando gli utenti accedono a un'applicazione pubblicata, hello gli eventi seguenti avvengono tra il servizio di Proxy applicazione hello e connettore del Proxy di applicazione hello:

1. [servizio Hello autentica l'utente di hello per app hello](#the-service-checks-the-configuration-settings-for-the-app)
2. [servizio Hello inserisce la richiesta nella coda di connettore hello](#The-service-places-a-request-in-the-connector-queue)
3. [Una richiesta di hello connettore processi dalla coda hello](#the-connector-receives-the-request-from-the-queue)
4. [connettore Hello attende una risposta](#the-connector-waits-for-a-response)
5. [utente di Hello servizio flussi dati toohello](#the-service-streams-data-to-the-user)

toolearn ulteriori informazioni su ciò che avviene in ognuno di questi passaggi, continuare a leggere.


#### <a name="1-hello-service-authenticates-hello-user-for-hello-app"></a>1. servizio di hello autentica l'utente di hello per app hello

Se come metodo di preautenticazione è stata configurata hello app toouse pass-through, i passaggi di hello in questa sezione vengono ignorati.

Se è stato configurato hello app toopreauthenticate con Azure AD, gli utenti vengono reindirizzato toohello tooauthenticate servizio token di sicurezza di Azure AD e hello avviene segue:

1. Proxy dell'applicazione controlla eventuali requisiti di criteri di accesso condizionale per un'applicazione hello specifico. Questo passaggio garantisce che l'utente hello è stato assegnato l'applicazione toohello. Se è necessaria la verifica in due passaggi, la sequenza di autenticazione hello richiesto hello un secondo metodo di autenticazione.

2. Dopo che tutti i controlli sono stati superati, hello servizio token di sicurezza di Azure AD rilascia un token firmato di un'applicazione hello e reindirizzamenti hello toohello indietro utente servizio Proxy di applicazione.

3. Proxy dell'applicazione verifica il che applicazione hello toocorrect è stato rilasciato il token di hello. Vengono eseguiti anche altri controlli, ad esempio assicurandosi che hello token è stato firmato da Azure AD e che sia all'interno di finestra valido hello.

4. Proxy dell'applicazione consente di impostare un tooindicate cookie di autenticazione crittografata che si è verificato un applicazione toohello l'autenticazione. Hello cookie include un timestamp di scadenza basato su token hello da Azure AD e altri dati, ad esempio nome utente hello che hello autenticazione si basa su. Hello cookie viene crittografato con una chiave privata, nota solo toohello servizio Proxy di applicazione.

5. Applicazione Proxy reindirizzamenti hello utente indietro toohello richiesto in origine URL.

Se qualsiasi parte dei passaggi di preautenticazione hello non riesce, hello la richiesta dell'utente viene negata e utente hello viene visualizzato un messaggio che indica hello origine del problema hello.


#### <a name="2-hello-service-places-a-request-in-hello-connector-queue"></a>2. servizio hello crea una richiesta nella coda di connettore hello

Connettori di mantenere un toohello aprire Servizio Proxy di applicazione di connessione in uscita. Quando arriva una richiesta, il servizio hello accodato richiesta hello in uno di connessioni aperte hello per hello connettore toopick backup.

richiesta di Hello include gli elementi da un'applicazione hello, ad esempio le intestazioni di richiesta hello, dati del cookie crittografato hello, hello utente che esegue hello richiesta e hello ID richiesta Anche se i dati da cookie crittografato hello viene inviati con richiesta di hello, i cookie di autenticazione hello stesso non è.

#### <a name="3-hello-connector-processes-hello-request-from-hello-queue"></a>3. hello connettore processi hello richiesta dalla coda hello. 

Proxy di applicazione basato su richiesta hello, esegue una delle seguenti azioni hello:

* Se la richiesta hello è un'operazione semplice (ad esempio, non sono presenti dati all'interno del corpo hello come con un RESTful *ottenere* richiesta), il connettore di hello esegue una risorsa di connessione toohello destinazione interno e quindi attende una risposta.

* Se hello richiesta dispone di dati associati nel corpo di hello (ad esempio, un RESTful *POST* operazione), connettore hello effettua una connessione in uscita utilizzando l'istanza del Proxy di applicazione toohello hello client certificato. Effettua dati connessione toorequest hello e aprire una risorsa di connessione toohello interno. Dopo aver ricevuto la richiesta hello dal connettore hello, servizio Proxy applicazione hello inizia ad accettare contenuto utente hello e inoltra connettore toohello di dati. connettore di Hello, inoltra a sua volta, risorse interne di hello dati toohello.

#### <a name="4-hello-connector-waits-for-a-response"></a>4. connettore hello è in attesa di una risposta.

Dopo la richiesta hello e la trasmissione di toohello tutto il contenuto finale è stata completata, connettore hello attende una risposta.

Dopo aver ricevuto una risposta, il connettore hello rende un servizio Proxy di applicazione di connessione in uscita toohello, tooreturn hello dettagli intestazione e avviare il flusso di dati restituito hello.

#### <a name="5-hello-service-streams-data-toohello-user"></a>5. utente di hello servizio flussi dati toohello. 

Alcune operazioni di elaborazione di un'applicazione hello può verificarsi qui. Se è configurato intestazioni tootranslate Proxy dell'applicazione o l'URL dell'applicazione, che l'elaborazione avviene in base alle necessità durante questo passaggio.


## <a name="next-steps"></a>Passaggi successivi

[Considerazioni relative alla topologia di rete quando si usa il proxy applicazione di Azure AD](application-proxy-network-topology-considerations.md)

[Comprendere i connettori del proxy applicazione di Azure AD](application-proxy-understand-connectors.md)
