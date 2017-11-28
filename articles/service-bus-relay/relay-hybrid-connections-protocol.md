---
title: le connessioni ibride di inoltro aaaAzure protocollo Guida | Documenti Microsoft
description: Guida al protocollo per le connessioni ibride di inoltro di Azure.
services: service-bus-relay
documentationcenter: na
author: clemensv
manager: timlt
editor: 
ms.assetid: 149f980c-3702-4805-8069-5321275bc3e8
ms.service: service-bus-relay
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: sethm;clemensv
ms.openlocfilehash: 2d145d919d606ae4722b063e1baf39fb845a600a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# Protocollo per le connessioni ibride di inoltro di Azure
Inoltro di Azure è uno dei pilastri funzionalità chiave hello della piattaforma Azure Service Bus hello. nuovo Hello *connessioni ibride* funzionalità di inoltro è un'evoluzione protetta, aprire protocollo basata su HTTP e WebSocket. Sostituisce ex hello, denominato ugualmente *servizi BizTalk* funzionalità che è stata basata su un protocollo proprietario. integrazione di Hello di connessioni ibride in servizi di App di Azure continuerà toofunction come-è.

Connessioni ibride permette di stabilire una comunicazione bidirezionale con flussi binari tra due applicazioni di rete, di cui una o entrambe le parti risiedono dietro NAT o firewall. Questo articolo descrive le interazioni di hello sul lato client con l'inoltro di connessioni ibride hello per la connessione client nel listener e i ruoli di mittente e il listener di accettano nuove connessioni.

## Modello di interazione
inoltro di connessioni ibride Hello si connette due parti, fornendo un punto di rendezvous nel cloud di Azure che sia in grado di individuare e connettersi toofrom prospettiva della propria rete parti hello. Tale punto rendezvous viene chiamato "Connessione ibrida" in questo esempio e altra documentazione, hello API, nonché in hello portale di Azure. Hello connessioni ibride endpoint del servizio è denominato tooas hello "servizio" per il resto di hello di questo articolo. modello di interazione Hello tende è stato a nomenclatura hello stabilita da molte altre API rete seguire.

Sia presente un listener che innanzitutto indica le connessioni in ingresso toohandle di conformità e successivamente li accetta man mano che arrivano. In hello altro lato, è disponibile un connessione client che si connette verso listener hello, previsto toobe tale connessione accettata per stabilire un percorso di comunicazione bidirezionale.
"Connessione", "Ascolto", e "Accetta" sono hello stessa API di socket trova nella maggior parte dei termini.

Qualsiasi modello di comunicazione inoltrata dispone di una delle due parti vengono stabilite le connessioni in uscita verso un endpoint del servizio, che rende listener"hello" anche "client" in uso stilistici e può essere causato anche altri overload di terminologia. è pertanto possibile utilizzare per le connessioni ibride la terminologia precisa Hello è indicato di seguito:

i programmi di Hello su entrambi i lati di una connessione vengono definiti "client", poiché sono servizio toohello client. client che attende e accetta le connessioni "listener" o Hello detto toobe hello "listener ruolo." client Hello che avvia una nuova connessione verso un listener tramite il servizio hello viene chiamato hello "mittente" o "mittente ruolo".

### Interazioni del listener
listener Hello ha quattro interazioni con il servizio di hello. tutti i dettagli di transito sono descritte più avanti in questo articolo nella sezione di riferimento hello.

#### Attesa
servizio di toohello conformità tooindicate che un listener è pronto tooaccept connessioni, crea una connessione WebSocket in uscita. l'handshake della connessione Hello esegue nome hello di una connessione ibrida configurato nell'inoltro di hello dello spazio dei nomi e un token di sicurezza che conferisce hello "Ascolto" destro del mouse su tale nome.
Quando hello WebSocket è accettata dal servizio di hello, registrazione hello e hello stabilita web che WebSocket viene mantenuta attiva come hello "canale di controllo" per l'abilitazione di tutte le interazioni successive. servizio Hello consente backup too25 listener simultanei su una connessione ibrida. In presenza di due o più listener attivi, le connessioni in ingresso vengono bilanciate tra di essi in ordine casuale. Non è garantita una distribuzione equa.

#### Accept
Quando un mittente apre una nuova connessione per il servizio di hello, servizio hello decide e comunica a uno dei listener attivi di hello in hello connessione ibrida. Questa notifica viene inviata toohello listener su canale di controllo aprire hello come un messaggio JSON contenente hello URL dell'endpoint WebSocket hello hello listener deve connettersi toofor accettazione connessione hello.

URL di Hello può e deve essere utilizzato direttamente dal listener hello senza operazioni aggiuntive.
informazioni Hello codificato sono valido solo per un breve periodo di tempo, in pratica per la durata come mittente hello indica toowait disposti per hello connessione stabilita toobe end-to-end, ma i tooa massimo di 30 secondi. URL di Hello utilizzabile solo per il tentativo di una connessione ha esito positivo. Appena hello WebSocket connessione rendezvous hello che URL viene stabilito, tutte le altre attività in questo WebSocket viene inoltrato dal e al mittente toohello, senza alcun intervento da parte dell'interpretazione dal servizio hello.

#### Renew
token di sicurezza Hello che deve essere usato tooregister hello listener e gestire che il canale di controllo può scadere mentre hello listener è attivo. la scadenza del token Hello influisce sulle connessioni in corso, ma comporta hello controllo canale toobe eliminato dal servizio hello in o subito dopo il momento di hello della scadenza. l'operazione "rinnovare" Hello è un messaggio JSON che hello listener può inviare il token di hello tooreplace associato al canale di controllo hello, in modo che hello canale di controllo possa essere mantenuti per lunghi periodi di tempo.

#### Ping
Se il canale di controllo di hello resta inattivo per molto tempo, gli intermediari in modo hello, ad esempio carico bilanciamento del carico o NAT può essere eliminato connessione TCP hello. operazione "ping" Hello evita adatto inviando una piccola quantità di dati su un canale di hello che ricorda di tutti i membri della route di rete hello tale connessione hello toobe alive e funge anche da un test per il listener hello "attivo". Se hello ping non riesce, il canale di controllo di hello deve essere considerato inutilizzabile e listener hello devono riconnettersi.

### Interazione del mittente
mittente Hello è solo una singola interazione con il servizio hello: si connette.

#### Connettere
operazione "connect" Hello apre un protocollo WebSocket nel servizio di hello, che fornisce nome hello della connessione ibrida hello e (facoltativamente, ma obbligatoria per impostazione predefinita) un token di sicurezza che conferisce autorizzazioni "Invia" nella stringa di query hello. servizio Hello interagisce con il listener hello nel modo descritto in precedenza hello e listener hello crea una connessione rendezvous è unita in join con questo WebSocket. Dopo avere accettato hello WebSocket, tutte le altre interazioni in tale WebSocket sono con un listener connesso.

### Riepilogo delle interazioni
il risultato di Hello di questo modello di interazione è che client mittente hello uscirà l'handshake con un WebSocket "pulito", che è connesso tooa listener e che non necessita di alcuna ulteriore preambles o preparazione. Questo modello consente praticamente qualsiasi esistente WebSocket client implementazione tooreadily sfruttare hello servizio connessioni ibride fornendo un URL costruito correttamente in loro livello di client WebSocket.

connessione rendezvous Hello WebSocket che hello listener ottenute tramite l'interazione accetta inoltre sia pulito e può essere passato tooany WebSocket server implementazione esistente con un'astrazione aggiuntiva minima che distingue tra "Accetto" operazioni su listener di rete locale e le connessioni ibride remoto relativo framework "operazioni di accettazione".

## Riferimento al protocollo

In questa sezione vengono descritti dettagliatamente di hello delle interazioni di protocollo hello descritte in precedenza.

Tutte le connessioni WebSocket vengono stabilite sulla porta 443 come aggiornamento da HTTPS 1.1, che è in genere un'astrazione di alcune API o framework del WebSocket. La presente descrizione è neutra dal punto di vista dell'implementazione e non suggerisce un framework specifico.

### Protocollo del listener
protocollo di listener Hello è costituito da tre operazioni di messaggio e due i movimenti di connessione.

#### Connessione del canale di controllo del listener
il canale di controllo di Hello viene aperto con la creazione di una connessione WebSocket a:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...[&sb-hc-id=...]&sb-hc-token=...
```

Hello `namespace-address` è il nome di dominio completo hello dello spazio dei nomi di Azure inoltro hello che gli host hello connessione ibrida, in genere del modulo di hello `{myname}.servicebus.windows.net`.

opzioni del parametro stringa query Hello sono i seguenti.

| . | Obbligatorio | Descrizione |
| --- | --- | --- |
| `sb-hc-action` |Sì |Per hello ruolo di listener hello parametro deve essere **sb-hc-action = ascolto** |
| `{path}` |Sì |percorso dello spazio dei nomi con codifica URL Hello di hello preconfigurato connessione ibrida tooregister questo listener in. Questa espressione viene accodato toohello fissata `$hc/` parte del percorso. |
| `sb-hc-token` |Sì\* |Hello listener deve fornire un valido, la codifica URL del servizio Bus condiviso Token di accesso per spazio dei nomi hello o la connessione ibrida che conferisce hello **ascolto** destra. |
| `sb-hc-id` |No |Questo ID facoltativo fornito dal client consente la traccia diagnostica end-to-end. |

Se hello connessione WebSocket non riesce a causa di percorso di connessione ibrida toohello non è registrato o un token non valido o manca o di altri errori, viene fornito un feedback errore hello modello hello regolare HTTP 1.1 stato commenti e suggerimenti. La descrizione dello stato contiene un ID di traccia dell'errore che può essere comunicato al personale del supporto di Azure:

| Codice | Errore | Description |
| --- | --- | --- |
| 404 |Non trovato |percorso di Hello connessione ibrida non è valido o hello URL di base non è corretto. |
| 401 |Non autorizzata |token di sicurezza Hello è mancante o non valido o non valido. |
| 403 |Accesso negato |token di sicurezza Hello non è valido per questo percorso per questa azione. |
| 500 |Errore interno |Si è verificato un errore nel servizio hello. |

Se hello connessione WebSocket è intenzionalmente arrestato dal servizio hello dopo che è stato inizialmente configurato, motivo hello per eseguire questa operazione viene comunicato utilizzando un codice di errore di protocollo WebSocket appropriato con un messaggio di errore descrittivo che include un rilevamento ID. servizio Hello non interromperà il canale di controllo senza che si verifichi una condizione di errore. Le chiusure normali sono controllate dal client.

| Stato Web Socket | Description |
| --- | --- |
| 1001 |percorso della connessione ibrida Hello è stato eliminato o disabilitato. |
| 1008 |token di sicurezza Hello è scaduta, pertanto viene violato i criteri di autorizzazione hello. |
| 1011 |Si è verificato un errore nel servizio hello. |

### Handshake accept
Hello "accetta" notifica viene inviata dal listener di hello servizio toohello attraverso il canale di controllo definito in precedenza come un messaggio JSON in un intervallo di testo di WebSocket. Non vi è alcun messaggio di risposta toothis.

messaggio contiene un oggetto JSON denominato "accetta", che definisce le proprietà seguenti in questo momento hello:

* **indirizzo** : hello toobe stringa URL utilizzato per stabilire hello WebSocket toothe servizio tooaccept una connessione in ingresso.
* **ID** : hello identificatore univoco per questa connessione. Se ID hello è stato fornito dal client mittente hello è il valore di mittente fornito hello, in caso contrario è un valore generato dal sistema.
* **connectHeaders** : tutte le intestazioni HTTP che sono stati forniti endpoint di inoltro toohello dal mittente hello, che include anche hello protocollo WebSocket al secondo e le intestazioni le estensioni di WebSocket al secondo.

#### Messaggio accept

```json
{                                                           
    "accept" : {
        "address" : "wss://168.61.148.205:443/$hc/{path}?..."    
        "id" : "4cb542c3-047a-4d40-a19f-bdc66441e736",  
        "connectHeaders" : {                                         
            "Host" : "...",                                                
            "Sec-WebSocket-Protocol" : "...",                              
            "Sec-WebSocket-Extensions" : "..."                             
        }                                                            
     }                                                         
}
```

Hello indirizzo URL fornito in hello messaggio JSON viene usato dal listener hello per stabilire hello WebSocket per l'accettazione o rifiuto di socket mittente hello.

#### Accettazione socket hello
tooaccept, listener hello stabilisce un indirizzo di toohello fornito connessione WebSocket.

Se hello "accetta" messaggio trasporta un `Sec-WebSocket-Protocol` intestazione, è previsto listener hello accetta hello WebSocket solo se supporta tale protocollo. Inoltre, imposta l'intestazione di hello come hello che WebSocket viene stabilita.

Hello vale toohello `Sec-WebSocket-Extensions` intestazione. Se il framework di hello supporta un'estensione, è necessario impostare risposta sul lato server di hello intestazione toohello di hello necessario `Sec-WebSocket-Extensions` handshake per estensione hello.

URL Hello devono essere usati come-per stabilire hello accetta socket, ma contiene i parametri seguenti:

| . | Obbligatorio | Descrizione |
| --- | --- | --- |
| `sb-hc-action` |Sì |Per accettare un socket, è necessario il parametro hello`sb-hc-action=accept` |
| `{path}` |Sì |(vedere il seguente paragrafo hello) |
| `sb-hc-id` |No |Vedere la descrizione precedente di **id**. |

`{path}`è il percorso dello spazio dei nomi con codifica URL hello di hello preconfigurato connessione ibrida in cui tooregister questo listener. Questa espressione viene accodato toothe fissata `$hc/` parte del percorso. 

Hello `path` espressione può essere esteso con un suffisso e un'espressione di stringa di query seguente, nome registrato hello dopo una barra rovesciata separazione. In questo modo hello mittente toopass invio argomenti toohello accettazione listener del client quando non è possibile tooinclude HTTP intestazioni. Hello previsione listener hello framework analizza parte di percorso predefinito di hello e hello nome registrato dal percorso e resto hello, probabilmente senza argomenti di stringa di query preceduti da `sb-`, applicazione toohello disponibile per determinazione se tooaccept hello connessione.

Per ulteriori informazioni, vedere hello successiva sezione "Mittente protocollo".

Se si verifica un errore, il servizio hello può rispondere nel modo seguente:

| Codice | Errore | Description |
| --- | --- | --- |
| 403 |Accesso negato |Hello URL non è valido. |
| 500 |Errore interno |Si è verificato un errore nel servizio hello |

Dopo aver stabilita la connessione hello, hello server viene arrestato hello WebSocket quando il mittente di hello WebSocket arresta, oppure con hello seguente stato:

| Stato Web Socket | Description |
| --- | --- |
| 1001 |client mittente Hello viene chiuso la connessione hello. |
| 1001 |percorso della connessione ibrida Hello è stato eliminato o disabilitato. |
| 1008 |token di sicurezza Hello è scaduta, pertanto viene violato i criteri di autorizzazione hello. |
| 1011 |Si è verificato un errore nel servizio hello. |

#### Rifiuto di socket hello
Rifiuto di socket hello dopo "esame hello accetta" messaggio richiede un handshake simile in modo che hello codice di stato e la descrizione di stato comunicare che il motivo del rifiuto hello possano essere scambiate all'indietro toohello mittente.

Hello protocollo progettazione scelta è toouse un handshake di WebSocket, ovvero tooend progettato in uno stato di errore definito, in modo che le implementazioni di client listener possono continuare toorely in un client WebSocket e non è necessario utilizzare un'ulteriore, bare client HTTP.

socket client hello hello tooreject accetta hello indirizzo URI dal messaggio "accetta" hello e accoda due query tooit di parametri stringa, come indicato di seguito:

| Param | Obbligatorio | Descrizione |
| --- | --- | --- |
| statusCode |Sì |Codice di stato HTTP numerico. |
| statusDescription |Sì |Motivo leggibile umano hello rifiuto. |

Hello che URI risultante viene quindi utilizzato tooestablish una connessione WebSocket.

Se completato correttamente, questo handshake non riuscirà di proposito con il codice di errore HTTP 410, perché non è stato stabilito alcun WebSocket. Se si verificano problemi, hello seguenti codici di descrivere l'errore hello:

| Codice | Errore | Description |
| --- | --- | --- |
| 403 |Accesso negato |Hello URL non è valido. |
| 500 |Errore interno |Si è verificato un errore nel servizio hello. |

### Rinnovo del token del listener
Quando il token di listener hello su tooexpire, è possibile sostituirlo mediante l'invio di un frame toohello servizio SMS tramite il canale di controllo di hello stabilita. Il messaggio contiene un oggetto JSON chiamato `renewToken`, che definisce hello seguente proprietà in questo momento:

* **token** : un token di accesso condiviso Bus di servizio valido, la codifica URL per dello spazio dei nomi o di una connessione ibrida che conferisce hello **ascolto** destra.

#### Messaggio renewToken

```json
{                                                                                                                                                                        
    "renewToken" : {                                                                                                                                                      
        "token" : "SharedAccessSignature sr=http%3a%2f%2fcontoso.servicebus.windows.net%2fhyco%2f&amp;sig=XXXXXXXXXX%3d&amp;se=1471633754&amp;skn=SasKeyName"  
    }                                                                                                                                                                     
}
```

Se si verifica un errore di convalida del token hello, viene negato l'accesso e servizio cloud hello chiude il canale di controllo hello WebSocket con un errore. In caso contrario non vi è alcuna risposta.

| Stato Web Socket | Description |
| --- | --- |
| 1008 |token di sicurezza Hello è scaduta, pertanto viene violato i criteri di autorizzazione hello. |

## Protocollo per il mittente
protocollo di mittente Hello è in pratica è identico toohello modo che viene stabilito un listener.
obiettivo di Hello è massima trasparenza per hello end-to-end WebSocket. indirizzo di Hello per la connessione hello toois che identico a quello del listener hello, ma l'azione"hello" è diverso e il token richiede un'autorizzazione diversa:

```
wss://{namespace-address}/$hc/{path}?sb-hc-action=...&sb-hc-id=...&sbc-hc-token=...
```

Hello *dello spazio dei nomi indirizzo* è il nome di dominio completo hello dello spazio dei nomi di Azure inoltro hello che gli host hello connessione ibrida, in genere del modulo di hello `{myname}.servicebus.windows.net`.

richiesta di Hello può contenere arbitrarie intestazioni HTTP aggiuntive, inclusi quelli definiti dall'applicazione. Tutti fornito toohello listener del flusso di intestazioni e possono trovarsi in hello `connectHeader` oggetto di hello **accettare** messaggio di controllo.

opzioni del parametro stringa query Hello sono i seguenti:

| Param | Obbligatorio? | Descrizione |
| --- | --- | --- |
| `sb-hc-action` |Sì |Per il ruolo di mittente hello, hello parametro deve essere `action=connect`. |
| `{path}` |Sì |(vedere il seguente paragrafo hello) |
| `sb-hc-token` |Sì\* |Hello listener deve fornire un valido, la codifica URL del servizio Bus condiviso Token di accesso per spazio dei nomi hello o la connessione ibrida che conferisce hello **inviare** destra. |
| `sb-hc-id` |No |Un ID facoltativo che consente la traccia diagnostica end-to-end e viene reso disponibile toohello listener durante hello accettare handshake. |

Hello `{path}` è il percorso dello spazio dei nomi con codifica URL hello di hello preconfigurato connessione ibrida in cui tooregister questo listener. Hello `path` espressione può essere esteso con un suffisso e un toocommunicate a un'espressione stringa di query ulteriormente. Se la connessione ibrida hello è registrato in un percorso di hello `hyco`, hello `path` espressione può essere `hyco/suffix?param=value&...` seguito dai parametri di stringa di query hello definiti qui. Un'espressione completa potrebbe quindi essere:

```
wss://{namespace-address}/$hc/hyco/suffix?param=value&sb-hc-action=...[&sb-hc-id=...&]sbc-hc-token=...
```

Hello `path` espressione viene passata tramite il listener toohello indirizzo hello URI contenuto nel messaggio di controllo "accept" hello.

Se hello connessione WebSocket non riesce a causa di percorso della connessione ibrida toohello non è registrato, un token non valido o manca o di altri errori, viene fornito un feedback errore hello modello hello regolare HTTP 1.1 stato commenti e suggerimenti. La descrizione dello stato contiene un ID di traccia dell'errore che può essere comunicato al personale del supporto di Azure:

| Codice | Errore | Description |
| --- | --- | --- |
| 404 |Non trovato |percorso di Hello connessione ibrida non è valido o hello URL di base non è corretto. |
| 401 |Non autorizzata |token di sicurezza Hello è mancante o non valido o non valido. |
| 403 |Accesso negato |token di sicurezza Hello non è valido per questo percorso e per questa azione. |
| 500 |Errore interno |Si è verificato un errore nel servizio hello. |

Se intenzionalmente hello connessione WebSocket viene chiuso dal servizio hello dopo che è stato inizialmente configurato, motivo hello ad esempio, quando pertanto viene comunicato utilizzando un codice di errore di protocollo WebSocket appropriato con un messaggio di errore descrittivo che include anche un ID rilevamento.

| Stato Web Socket | Description |
| --- | --- |
| 1000 |listener Hello arrestato dal socket hello. |
| 1001 |percorso della connessione ibrida Hello è stato eliminato o disabilitato. |
| 1008 |token di sicurezza Hello è scaduta, pertanto viene violato i criteri di autorizzazione hello. |
| 1011 |Si è verificato un errore nel servizio hello. |

## Passaggi successivi
* [Domande frequenti sull'inoltro](relay-faq.md)
* [Creare uno spazio dei nomi](relay-create-namespace-portal.md)
* [Introduzione a .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introduzione a Node](relay-hybrid-connections-node-get-started.md)

