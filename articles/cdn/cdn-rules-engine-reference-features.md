---
title: "funzionalità del motore regole di aaaAzure CDN | Documenti Microsoft"
description: "Documentazione di riferimento per le funzionalità e condizioni di corrispondenza del motore regole della rete CDN di Azure."
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: c10b8ef58e3d209b12fbb0ac2173e1ca51ff7538
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-features"></a>Funzionalità del motore regole della rete CDN di Azure
In questo argomento elenca le descrizioni dettagliate delle funzionalità disponibili hello per Azure rete CDN (Content Delivery) [motore regole di business](cdn-rules-engine.md).

Hello terza parte di una regola è funzionalità hello. Una funzionalità definisce il tipo di hello di azione che verrà applicato il tipo di toohello di richiesta identificato da un set di condizioni di corrispondenza.

## <a name="access"></a>Accesso

Queste funzionalità sono progettate toocontrol toocontent di accesso.


Nome | Scopo
-----|--------
Nega l'accesso | Determina se tutte le richieste vengono rifiutate con una risposta 403 Accesso negato.
Autenticazione token | Determina se l'autenticazione basata su Token sarà applicato tooa richiesta.
Codice rifiuto autenticazione token | Determina il tipo di hello di risposta che verrà restituito tooa utente durante una richiesta viene negata a causa dell'autenticazione basata su tooToken.
Maiuscole/minuscole URL autenticazione token | Determina se verrà applicata la distinzione tra maiuscole e minuscole nei confronti di URL eseguiti dall'autenticazione basata su token.
Parametro autenticazione token | Determina se il parametro della stringa query di hello l'autenticazione basata su Token deve essere rinominato.

### <a name="deny-access"></a>Nega l'accesso
**Scopo**: determina se tutte le richieste vengono rifiutate con una risposta 403 - Accesso negato.

Valore | Risultato
------|-------
Enabled| Fa sì che tutte le richieste che soddisfano hello corrispondenti criteri toobe rifiutata con risposta 403 accesso negato.
Disabled| Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è tooallow hello origine server toodetermine hello risposta che verrà restituito.

**Comportamento predefinito**: Disabled

> [!TIP]
   > Un possibile utilizzo di questa funzionalità è tooassociate con un'intestazione di richiesta corrisponde la riferimenti condizione tooblock accesso tooHTTP che utilizzano il contenuto tooyour collegamenti in linea.

### <a name="token-auth"></a>Autenticazione token
**Scopo:** determina se l'autenticazione basata su Token sarà applicato tooa richiesta.

Se è abilitata l'autenticazione basata su Token, verranno rispettate solo le richieste che forniscono un token crittografato e soddisfare i requisiti toohello specificati da tale token.

chiave di crittografia Hello che sarà utilizzati valori tooencrypt e di decrittografia token è la chiave primaria e le opzioni di Backup della chiave nella pagina autenticazione Token. Tenere presente che le chiavi di crittografia sono specifiche della piattaforma.

Valore | Risultato
------|---------
Enabled | Consente di proteggere hello richiesto contenuto con l'autenticazione basata su Token. Verranno soddisfatte solo le richieste provenienti da client che forniscono un token valido e ne soddisfano i requisiti. Dall'autenticazione basata su token sono escluse le transazioni FTP.
Disabled| Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è tooallow il toodetermine configurazione basata su Token di autenticazione se una richiesta da proteggere.

**Comportamento predefinito:** Disabled.

###<a name="token-auth-denial-code"></a>Codice rifiuto autenticazione token
**Scopo:** determina il tipo di hello di risposta che verrà restituito tooa utente durante una richiesta viene negata a causa dell'autenticazione basata su tooToken.

codici di risposta disponibile Hello sono elencati di seguito.

Codice risposta|Nome risposta|Descrizione
----------------|-----------|--------
301|Spostato in modo permanente|Questo codice di stato reindirizza gli utenti non autorizzati toohello URL specificato nell'intestazione Location.
302|Trovato|Questo codice di stato reindirizza gli utenti non autorizzati toohello URL specificato nell'intestazione Location. Questo codice di stato è hello metodo standard dell'esecuzione di un reindirizzamento.
307|Reindirizzamento temporaneo|Questo codice di stato reindirizza gli utenti non autorizzati toohello URL specificato nell'intestazione Location.
401|Non autorizzata|Combinazione di questo codice di stato con l'intestazione della risposta WWW-Authenticate consente tooprompt un utente per l'autenticazione.
403|Accesso negato|Si tratta di hello standard 403 accesso negato messaggio di stato che un utente non autorizzato verrà visualizzato quando si tenta di tooaccess contenuto protetto.
404|File non trovato|Questo codice di stato indica che client HTTP hello è stato in grado di toocommunicate con server hello, ma hello richiesto non è stato trovato il contenuto.

#### <a name="url-redirection"></a>Reindirizzamento URL

Questa funzionalità supporta URL reindirizzamento tooa definito dall'utente URL quando è configurato tooreturn un codice di stato 3xx. È possibile specificare l'URL definito dall'utente eseguendo hello alla procedura seguente:

1. Selezionare un codice di risposta 3xx per funzionalità Token Auth Denial codice hello.
2. Per l'opzione Optional Header Name (Nome intestazione facoltativo) selezionare "Location".
3. Impostare il valore dell'intestazione facoltativa option (URL) toohello desiderato.

Se un URL non è definito per un codice di stato 3xx, hello pagina di risposta standard per un codice di stato 3xx verrà restituito toohello utente.

Il reindirizzamento degli URL può essere usato solo per i codici di risposta 3xx.

L'opzione Optional Header Value (Valore intestazione facoltativo) supporta caratteri alfanumerici, virgolette e spazi.

#### <a name="authentication"></a>Autenticazione

Questa funzionalità supporta l'intestazione WWW-Authenticate tooinclude di hello funzionalità quando si risponde tooan richiesta non autorizzata per il contenuto protetto con l'autenticazione basata su Token. Se è stata impostata l'intestazione WWW-Authenticate troppo "base" in configurazione, verranno richiesto di utenti non autorizzati hello le credenziali dell'account.

Hello di sopra di configurazione può essere ottenuto eseguendo hello alla procedura seguente:

1. Selezionare "401" come codice di risposta hello per funzionalità Token Auth Denial codice hello.
2. Per l'opzione Optional Header Name (Nome intestazione facoltativo) selezionare "WWW-Authenticate".
3. Impostare l'opzione di valore dell'intestazione facoltativa troppo "base".

L'intestazione WWW-Authenticate può essere usata solo per i codici di risposta 401.

### <a name="token-auth-ignore-url-case"></a>Maiuscole/minuscole URL autenticazione token
**Scopo:** determina se durante i confronti di URL eseguiti dall'autenticazione basata su token deve essere applicata la distinzione tra maiuscole e minuscole.

parametri di Hello interessati da questa funzionalità sono:

- ec_url_allow
- ec_ref_allow
- ec_ref_deny

I valori validi sono:

Valore|Risultato
---|----
Enabled|Fa sì che il server perimetrale tooignore caso quando si confrontano gli URL per i parametri di autenticazione basata su Token.
Disabled|Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è per i confronti di URL per l'autenticazione con Token toobe tra maiuscole e minuscole.

**Comportamento predefinito:** Disabled.
 
### <a name="token-auth-parameter"></a>Parametro autenticazione token
**Scopo:** determina se il parametro della stringa query di hello l'autenticazione basata su Token deve essere rinominato.

Informazioni chiave:

- L'opzione valore definisce hello stringa nome del parametro query tramite cui è possibile specificare un token.
- Impossibile impostare l'opzione valore troppo "ec_token".
- Verificare che tale nome hello definita solo l'opzione valore 
- contenga solo caratteri URL validi.

Valore|Risultato
----|----
Enabled|L'opzione valore definisce hello stringa nome del parametro query tramite cui i token devono essere definiti.
Disabled|Un token può essere specificato come parametro di stringa di query non definito nell'URL di richiesta hello.

**Comportamento predefinito:** Disabled. Un token può essere specificato come parametro di stringa di query non definito nell'URL di richiesta hello.

## <a name="caching"></a>Memorizzazione nella cache

Queste funzionalità sono progettate toocustomize quando e come verrà memorizzati nella cache il contenuto.

Nome | Scopo
-----|--------
Parametri larghezza di banda | Determina se i parametri di limitazione della larghezza di banda (ad esempio, ec_rate ed ec_prebuf) saranno attivi.
Limitazione larghezza di banda | Limita larghezza di banda di hello per risposta hello fornito dai nostri server edge.
Ignora cache | Determina se la richiesta hello può sfruttare la tecnologia di memorizzazione nella cache.
Gestione intestazione Cache-Control | Controlli hello generazione delle intestazioni Cache-Control da server perimetrale hello quando è attiva la funzionalità esterne Max-Age.
Stringa di query chiave cache | Determina se includere o escludere i parametri di stringa di query associati a una richiesta di chiave di cache di hello.
Riscrittura chiave cache | Riscrive hello-chiave di cache associata a una richiesta.
Completa riempimento cache | Determina ciò che accade quando una richiesta determina un mancato riscontro nella cache parziale in un server perimetrale.
Comprimi tipi di file | Definisce i formati di file hello che verranno compresse nel server di hello.
Max-Age interno predefinito | Determina l'intervallo di validità massima hello predefinito per la riconvalida della cache lato server tooorigin server.
Gestione intestazione Expires | Controlli hello generazione delle intestazioni Expires da un server perimetrale quando è attiva la funzionalità esterne Max-Age hello.
Max-Age esterno | Determina l'intervallo max-age hello di riconvalida della cache del browser tooedge server.
Forza Max-Age interno | Determina l'intervallo max-age "hello" per la riconvalida della cache lato server tooorigin server.
Supporto H.264 (download progressivo HTTP) | Determina i tipi di hello di h. 264 formati di file che possono essere utilizzati toostream contenuto.
Rispetta richiesta No-Cache | Determina se le richieste no-cache del client HTTP deve essere inoltrate toohello server di origine.
Ignora origine No-Cache | Determina se la rete CDN ignorerà alcune direttive servite da un server di origine.
Ignora gli intervalli che non è possibile soddisfare | Determina risposta hello che verrà restituito tooclients quando una richiesta genera un codice di stato 416 richiesto non Impossibile attenersi all'intervallo.
Max-Stale interno | Controlla il tempo trascorso il tempo di scadenza normale hello un asset memorizzati nella cache può essere servito da un server perimetrale quando server perimetrale hello è toorevalidate Impossibile hello asset memorizzati nella cache con il server di origine hello.
Condivisione cache parziale | Determina se una richiesta può generare contenuto parzialmente memorizzato nella cache.
Preconvalida contenuto memorizzato nella cache | Determina se il contenuto memorizzato nella cache sarà idoneo per la riconvalida anticipata prima della scadenza della durata (TTL).
Aggiorna i file della cache con zero byte | Determina come viene gestita dai server perimetrali una richiesta di un client HTTP di un asset della cache con 0 byte.
Imposta codici di stato inseribile nella cache | Definisce il set di hello dei codici di stato che possono comportare contenuto memorizzato nella cache.
Distribuzione di contenuto non aggiornato in caso di errore | Determina se scaduto, verrà recapitato contenuto memorizzato nella cache quando si verifica un errore durante la riconvalida della cache o quando hello durante il recupero delle richieste di contenuto dal server di origine cliente hello.
Client non aggiornato durante la riconvalida | Migliora le prestazioni poiché consente i nostri server edge richiedente toohello di tooserve client non aggiornato durante la riconvalida.
Commento | funzionalità di commento Hello consente un toobe nota aggiunta all'interno di una regola.

###<a name="bandwidth-parameters"></a>Parametri larghezza di banda
**Scopo:** determina se i parametri di limitazione della larghezza di banda (ad esempio ec_rate ed ec_prebuf) saranno attivi.

I parametri di limitazione della larghezza di banda stabilire se hello velocità di trasferimento di dati per una richiesta del client sarà limitato tooa personalizzato frequenza.

Valore|Risultato
--|--
Enabled|Larghezza di banda che i nostri server edge toohonor la limitazione delle richieste.
Disabled|Fa sì che i nostri server edge parametri di limitazione larghezza di banda tooignore. Hello richiesto verrà utilizzato in genere contenuto (ad esempio, senza la limitazione della larghezza di banda).

**Comportamento predefinito:** Enabled.

###<a name="bandwidth-throttling"></a>Limitazione larghezza di banda
**Scopo:** le limitazioni della larghezza di banda per la risposta hello fornito dai nostri server perimetrale di hello.

Entrambe le opzioni seguenti hello deve essere definito tooproperly configurare la limitazione della larghezza di banda.

Opzione|Descrizione
--|--
Kbytes per second (KB al secondo)|Impostare questa opzione toohello larghezza di banda massima (Kb al secondo) che può essere utilizzati toodeliver hello risposta.
Prebuf seconds (Secondi prebuf)|Impostare questa opzione toohello quanti secondi che i nostri server edge attenderà limitazione della larghezza di banda. scopo di Hello di questo periodo di tempo della larghezza di banda senza restrizioni è tooprevent un lettore multimediale da verifica stuttering o problemi dovuti toobandwidth la limitazione delle richieste di memorizzazione nel buffer.

**Comportamento predefinito:** Disabled.

###<a name="bypass-cache"></a>Ignora cache
**Scopo:** determina se la richiesta hello può sfruttare la tecnologia di memorizzazione nella cache.

Valore|Risultato
--|--
Enabled|Fa sì che tutte le richieste toofall attraverso il server di origine toohello, anche se il contenuto di hello è stata precedentemente memorizzati nella cache server edge.
Disabled|Fa sì che i server edge toocache asset in base a criteri di cache toohello definiti nelle intestazioni di risposta.

**Comportamento predefinito:**

- **HTTP Large:** Disabled

<!---
- **ADN:** Enabled
--->

###<a name="cache-control-header-treatment"></a>Cache Control Header Treatment (Gestione intestazioni Cache-Control)
**Scopo:** controlla la generazione di hello delle intestazioni Cache-Control da server perimetrale hello quando è attiva la funzionalità Max-Age esterna.

Hello tooachieve di modo più semplice questo tipo di configurazione è tooplace hello Max-Age esterno e le funzionalità di gestione intestazione Cache-Control hello hello stessa istruzione.

Valore|Risultato
--|--
Overwrite|Garantisce avverrà tale hello seguenti azioni:<br/> -Sovrascrive l'intestazione Cache-Control generato dal server di origine hello. <br/>-Aggiunge un'intestazione Cache-Control prodotta da hello risposta toohello di funzionalità esterni Max-Age.
Pass-through|Assicura che l'intestazione Cache-Control generato dalla funzionalità esterne Max-Age hello non verrà mai inserito toohello risposta. <br/> Se il server di origine hello produce un'intestazione Cache-Control, passerà toohello dati gestito dall'utente. <br/> Se il server di origine hello non produce un'intestazione Cache-Control, quindi questa opzione causa hello risposta intestazione toonot può contenere un'intestazione Cache-Control.
Add if Missing (Aggiungi se mancante)|Se un'intestazione Cache-Control non è stata ricevuta dal server di origine hello, questa opzione aggiunge l'intestazione Cache-Control generato dalla funzionalità esterne Max-Age hello. Assicura quindi che a tutti gli asset venga assegnata un'intestazione Cache-Control.
Rimuovere| Questa opzione assicura che un'intestazione Cache-Control non è inclusa con la risposta di intestazione hello. Se è già stata assegnata un'intestazione Cache-Control, verrà rimossa dalla risposta di intestazione hello.

**Comportamento predefinito:** Overwrite.

###<a name="cache-key-query-string"></a>Stringa di query chiave cache
**Scopo:** determina se la chiave di cache includerà o escluderà i parametri della stringa di query associati a una richiesta.

Informazioni chiave:

- Specificare uno o più nomi di parametri della stringa di query. Ogni nome di parametro deve essere delimitato da uno spazio singolo.
- Questa funzionalità determina se i parametri di stringa di query verranno inclusi o esclusi dalla chiave di cache di hello. Di seguito vengono fornite informazioni aggiuntive per ogni opzione seguente.

Tipo|Descrizione
--|--
 Includi|  Indica che ogni parametro specificato deve essere incluso nella chiave di cache di hello. Verrà generata una chiave di cache univoca per ogni richiesta in cui sia contenuto un valore univoco per un parametro della stringa di query definito in questa funzionalità. 
 Includi tutto  |Indica che una chiave di cache univoca verrà creata per ogni asset tooan richiesta che include una stringa di query univoco. Questo tipo di configurazione non è in genere consigliato perché potrebbe risultare tooa una piccola percentuale di riscontri nella cache. Ciò aumenta il carico di hello sul server di origine hello, dal momento che verrà tooserve più richieste. Questa configurazione duplicati hello comportamento noto come "univoco-cache" nella pagina di memorizzazione nella cache della stringa di Query di memorizzazione nella cache. 
 Escludi | Indica che solo hello specificato parametri verranno esclusi dalla chiave di cache di hello. Nella chiave di cache di hello verranno inclusi tutti gli altri parametri di stringa di query. 
 Escludi tutto  |Indica che tutti i parametri di stringa di query verranno esclusi dalla chiave di cache di hello. Questa configurazione duplicati hello comportamento predefinito della cache, che è noto come "standard-cache" nella pagina di memorizzazione nella cache della stringa di Query. 

potenza Hello del motore regole di HTTP consente modo hello toocustomize in cui viene implementata la memorizzazione nella cache stringa di query. È possibile specificare, ad esempio, che la memorizzazione nella cache della stringa di query può essere eseguita solo su determinate posizioni o tipi di file.

Se si desidera stringa di query hello tooduplicate la memorizzazione nella cache comportamento noto come "no-cache" nella pagina di memorizzazione nella cache della stringa di Query, è necessario toocreate una regola che contiene una condizione di corrispondenza con caratteri jolly Query URL e una funzionalità di ignorare la Cache. condizione di corrispondenza con caratteri jolly Query URL Hello deve essere impostato tooan asterisco (*).

#### <a name="sample-scenarios"></a>Scenari di esempio

Di seguito è riportato un uso di esempio di questa funzionalità Un esempio di richiesta e hello predefinito della chiave di cache vengono fornite di seguito.

- **Richiesta di esempio:** http://wpc.0001.&lt;Domain&gt;/800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01
- **Chiave di cache predefinita:** /800001/Origin/folder/asset.htm

##### <a name="include"></a>Includi

Configurazione di esempio:

- **Tipo:** Includi
- **Parametri:** language

Questo tipo di configurazione generano hello seguente parametro stringa di query cache-chiave:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="include-all"></a>Includi tutto

Configurazione di esempio:

- **Tipo:** Includi tutto

Questo tipo di configurazione generano hello seguente parametro stringa di query cache-chiave:

    /800001/Origin/folder/asset.htm?sessionid=1234&language=EN&userid=01

##### <a name="exclude"></a>Escludi

Configurazione di esempio:

- **Tipo:** Escludi
- **Parametri:** sessionid userid

Questo tipo di configurazione generano hello seguente parametro stringa di query cache-chiave:

    /800001/Origin/folder/asset.htm?language=EN

##### <a name="exclude-all"></a>Escludi tutto

Configurazione di esempio:

- **Tipo:** Escludi tutto

Questo tipo di configurazione generano hello seguente parametro stringa di query cache-chiave:

    /800001/Origin/folder/asset.htm

###<a name="cache-key-rewrite"></a>Riscrittura chiave cache
**Scopo:** riscritture hello chiave di cache associata a una richiesta.

Una chiave di cache è relativo hello che identifica un asset per scopi di hello della memorizzazione nella cache. In altre parole, i nostri server controllerà per una versione memorizzata nella cache di un asset in base percorso tooits come definito in base alla chiave di cache.

Questa funzionalità può essere configurata mediante la definizione di entrambi hello le opzioni seguenti:

Opzione|Descrizione
--|--
Percorso originale| Definire tipi di toohello hello percorso relativo di richieste la cui chiave di cache verrà riscritto. Un percorso relativo può essere definito selezionando un percorso di origine di base e quindi definendo un modello di espressione regolare.
Nuovo percorso|Definire il percorso relativo di hello hello nuova cache-chiave. Un percorso relativo può essere definito selezionando un percorso di origine di base e quindi definendo un modello di espressione regolare. Questo percorso può essere costruito in modo dinamico tramite l'utilizzo di hello delle variabili di HTTP
**Comportamento predefinito:** chiave della richiesta è una di cache è determinata dall'URI della richiesta hello.

###<a name="complete-cache-fill"></a>Completa riempimento cache
**Scopo:** determina ciò che accade quando una richiesta genera un mancato riscontro nella cache parziale in un server perimetrale.

Accesso alla cache parziale descrive lo stato della cache di hello per un asset che non era server perimetrale tooan completamente scaricato. Se un asset è solo parzialmente memorizzata nella cache in un server perimetrale, quindi hello successiva richiesta dell'asset verrà inoltrato nuovamente toohello server di origine.
<!---
This feature is not available for hello ADN platform. hello typical traffic on this platform consists of relatively small assets. hello size of hello assets served through these platforms helps mitigate hello effects of partial cache misses, since hello next request will typically result in hello asset being cached on that POP.
--->
In genere, un mancato riscontro nella cache parziale si verifica dopo che un utente interrompe un download o in caso di asset che vengono richiesti esclusivamente tramite richieste di intervallo HTTP. Questa funzionalità è particolarmente utile per gli asset di grandi dimensioni in cui gli utenti non in genere li scaricheranno dall'inizio toofinish (ad esempio, video). Di conseguenza, questa funzionalità è abilitata per impostazione predefinita nella piattaforma di grandi dimensioni HTTP hello. ed è disabilitata in tutte le altre piattaforme.

Configurazione predefinita di hello tooleave per piattaforma di grandi dimensioni HTTP hello, è consigliabile in quanto ridurre il carico di hello del server di origine cliente e aumentare la velocità di hello in corrispondenza del quale i clienti scaricare il contenuto.

Scadenza toohello modo nella cui cache vengono rilevate le impostazioni, questa funzionalità non può essere associata seguendo le condizioni di corrispondenza hello: bordo Cname, valore letterale intestazione richiesta, con caratteri jolly dell'intestazione di richiesta, valore letterale di Query di URL e jolly Query URL.

Valore|Risultato
--|--
Enabled|Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è tooforce hello edge server tooinitiate un recupero in background dell'asset hello dal server di origine hello. Dopodiché sarà asset hello nella cache locale del server perimetrale hello.
Disabled|Impedisce a un server perimetrale di eseguire un recupero in background per asset hello. Ciò significa che la richiesta successiva hello per l'asset di tale regione causerà un toorequest server edge dal server di origine cliente hello.

**Comportamento predefinito:** Enabled.

###<a name="compress-file-types"></a>Comprimi tipi di file
**Scopo:** definisce i formati di file hello che verranno compresse nel server di hello.

Un formato di file può essere specificato usando il rispettivo tipo di elemento multimediale Internet (ad esempio, Content-Type). Tipo di supporto Internet è indipendente dalla piattaforma metadati che consente il formato di file server hello tooidentify di una particolare attività. Di seguito è riportato un elenco dei tipi di elementi multimediali Internet.

Tipo di elemento multimediale Internet|Descrizione
--|--
text/plain|File di testo normale
text/html| File HTML
text/css|Fogli di stile CSS
application/x-javascript|JavaScript
application/javascript|JavaScript
Informazioni chiave:

- È possibile specificare più tipi di elementi multimediali Internet delimitandoli ciascuno con uno spazio singolo. 
- Questa funzionalità comprimerà solo asset con dimensioni inferiori a 1 MB. Gli asset con dimensioni superiori non verranno compressi dai server.
- Alcuni tipi di contenuti, come le immagini e i contenuti multimediali audio e video (ad esempio JPG, MP3, MP4 e così via), sono già compressi. Un ulteriore compressione di questi tipi di asset, pertanto, non ne diminuirebbe in modo significativo le dimensioni. È consigliabile quindi non abilitare la compressione su questi tipi di asset.
- Non sono supportati i caratteri jolly come gli asterischi.
- Prima di aggiungere questa regola tooa funzionalità, assicurarsi che tooset l'opzione di compressione disabilitato nella pagina di compressione per hello piattaforma toowhich che verrà applicata questa regola.

###<a name="default-internal-max-age"></a>Max-Age interno predefinito
**Scopo:** intervallo max-age di determina hello predefinito per la riconvalida della cache lato server tooorigin server. In altre parole, hello periodo di tempo che passa prima di un server perimetrale controllerà se asset hello archiviati sul server di origine hello corrisponde a un asset memorizzati nella cache.

Informazioni chiave:

- Questa azione viene eseguita solo per le risposte generate da un server di origine che non ha assegnato un'indicazione di validità massima nell'intestazione Cache-Control o Expires.
- Questa azione non viene eseguita per gli asset che non sono considerati memorizzabili nella cache.
- Questa operazione non influenza riconvalide cache server tooedge di browser. Questi tipi di riconvalide dipendono dalle Cache-Control o Expires intestazioni inviate toohello browser, che può essere personalizzato con la funzione Max-Age esterno.
- risultati Hello di questa azione non dispone di un effetto osservabile alle intestazioni di risposta hello e contenuto hello restituito dal server di bordo per il contenuto, ma può avere un effetto sulla quantità di hello di riconvalida il traffico inviato dal server di origine tooyour server perimetrale.
- Per configurare questa funzionalità:
    - Se si seleziona il codice di stato hello per i quali può essere applicate max-age predefinita interno.
    - Specificando un valore integer e quindi selezionando hello unità di tempo desiderato (ad esempio secondi, minuti, ore e così via). Questo valore definisce l'intervallo hello predefinito interno max-age.

- Unità di tempo hello impostazione troppo "Off" verrà assegnato un intervallo di validità massima interno predefinito di 7 giorni per le richieste che non è state assegnate un'indicazione max-age Cache-Control o Expires intestazione.
- Scadenza toohello modo nella cui cache vengono rilevate le impostazioni, questa funzionalità non può essere associata seguendo le condizioni di corrispondenza hello: 
    - Edge 
    - CNAME
    - Valore letterale intestazione richiesta
    - Carattere jolly intestazione richiesta
    - Metodo richiesta
    - Valore letterale query URL
    - Carattere jolly query URL

**Valore predefinito:** 7 giorni

###<a name="expires-header-treatment"></a>Gestione intestazione Expires
**Scopo:** controlla la generazione di hello delle intestazioni Expires da un server perimetrale quando è attiva la funzionalità esterne Max-Age.

Hello tooachieve di modo più semplice questo tipo di configurazione è hello tooplace Max-Age esterne e le funzionalità di scadenza trattamento intestazione hello hello stessa istruzione.

Valore|Risultato
--|--
Overwrite|Garantisce avverrà tale hello seguenti azioni:<br/>-Sovrascrive l'intestazione Expires generato dal server di origine hello.<br/>-Aggiunge un'intestazione Expires prodotto dalla risposta toohello funzionalità di hello Max-Age esterno.
Pass-through|Assicura che l'intestazione Expires generato dalla funzionalità esterne Max-Age hello non verrà mai inserito toohello risposta. <br/> Se il server di origine hello produce un'intestazione Expires, passerà toohello dati gestito dall'utente. <br/>Se il server di origine hello non produce un'intestazione Expires, quindi questa opzione causa hello risposta intestazione toonot può contenere un'intestazione Expires.
Add if Missing (Aggiungi se mancante)| Se un'intestazione Expires non è stata ricevuta dal server di origine hello, questa opzione aggiunge l'intestazione Expires generato dalla funzionalità esterne Max-Age hello. Assicura quindi che a tutti gli asset venga assegnata un'intestazione Expires.
Rimuovere| Assicura che un'intestazione Expires non viene fornita con la risposta di intestazione hello. Se è già stata assegnata un'intestazione Expires, verrà rimossa dalla risposta di intestazione hello.

**Comportamento predefinito:** Overwrite

###<a name="external-max-age"></a>Max-Age esterno
**Scopo:** intervallo max-age "hello" determina di riconvalida della cache del browser tooedge server. In altre parole, hello periodo di tempo che passa prima di un browser può essere cercati una nuova versione di un asset da un server perimetrale.

Abilitazione di questa funzionalità genera Cache-controllo: max-age e scade intestazioni dai nostri server edge e inviarli toohello HTTP client. Per impostazione predefinita, queste intestazioni sovrascriverà quelli creati dal server di origine hello. Tuttavia, la modalità di gestione di intestazione Cache-Control e le funzionalità di scadenza trattamento intestazione possono essere utilizzato tooalter questo comportamento.

Informazioni chiave:

- Questa azione non influenza la riconvalide cache lato server tooorigin server. Questi tipi di riconvalide sono determinati dalle intestazioni Cache-controllo/Expires ricevute dal server di origine hello e possono essere personalizzati con il predefinito interno Max-Age e le funzionalità interne Force Max-Age.
- Questa funzionalità può essere configurata specificando un valore integer e selezionando l'unità di tempo desiderato hello (ad esempio secondi, minuti, ore e così via).
- Se questa funzionalità tooa negativo, i nostri toosend server edge una Cache-Control: no-cache e un'ora di scadenza impostata nel hello passato con ogni browser toohello di risposta. Anche se un client HTTP non verrà memorizzati nella cache la risposta hello, questa impostazione non influirà possibilità toocache hello risposta il server perimetrale hello origine server.
- Unità di tempo hello impostazione troppo "Off" verrà disabilitare questa funzionalità. Le intestazioni Cache-controllo/Expires memorizzata nella cache con risposta hello del server di origine hello passerà toohello browser.

**Comportamento predefinito:** Off

###<a name="force-internal-max-age"></a>Forza Max-Age interno
**Scopo:** intervallo max-age "hello" determina per la riconvalida della cache lato server tooorigin server. In altre parole, quantità di hello di tempo che devono trascorrere prima che un server perimetrale può controllare se un asset memorizzati nella cache corrisponde a asset hello archiviati sul server di origine hello.

Informazioni chiave:

- Questa funzionalità sostituisce intervallo max-age hello definito nella Cache-Control o Expires intestazioni generate da un server di origine.
- Questa funzionalità non influisce sul riconvalide cache server tooedge di browser. Questi tipi di riconvalide dipendono dalle Cache-Control o Expires intestazioni inviate toohello browser.
- Questa funzionalità non ha un effetto osservabile sulla risposta hello recapitato a un richiedente di toohello lato server. Tuttavia, è un effetto sulla quantità di hello di riconvalida il traffico inviato dal server di origine lato server toohello.
- Per configurare questa funzionalità:
    - Se si seleziona il codice di stato hello per il quale verrà applicato un interno max-age.
    - Specifica un valore integer e selezione di hello unità di tempo desiderato (ad esempio secondi, minuti, ore e così via). Questo valore definisce l'intervallo di durata massima della richiesta di hello.

- Unità di tempo hello impostazione troppo "Off" Disabilita questa funzionalità. Non verrà assegnato un intervallo max-age interno toorequested asset. Se l'intestazione originale hello non contiene istruzioni di memorizzazione nella cache, asset hello verranno memorizzate in base toohello impostazione attiva la caratteristica predefinita Max-Age interno.
- Scadenza toohello modo nella cui cache vengono rilevate le impostazioni, questa funzionalità non può essere associata seguendo le condizioni di corrispondenza hello: 
    - Edge 
    - CNAME
    - Valore letterale intestazione richiesta
    - Carattere jolly intestazione richiesta
    - Metodo richiesta
    - Valore letterale query URL
    - Carattere jolly query URL

**Comportamento predefinito:** Off

###<a name="h264-support-http-progressive-download"></a>Supporto H.264 (download progressivo HTTP)
**Scopo:** determina i tipi di hello di h. 264 formati di file che possono essere utilizzati toostream contenuto.

Informazioni chiave:

- Nell'opzione Estensioni file definire un set delimitato da spazi di estensioni di file H.264 consentite. L'opzione di estensioni di File sostituirà il comportamento predefinito di hello. Garantire il supporto di file MP4 e F4V includendo queste estensioni durante la configurazione dell'opzione. 
- Verificare che tooinclude un punto quando si specifica ogni estensione del nome file (ad esempio,. mp4 F4V).

**Comportamento predefinito:** il download progressivo HTTP supporta file multimediali MP4 e F4V per impostazione predefinita.

###<a name="honor-no-cache-request"></a>Rispetta richiesta no-cache
**Scopo:** determina se le richieste no-cache del client HTTP deve essere inoltrate toohello server di origine.

Una richiesta di no-cache si verifica quando il client di hello HTTP invia una Cache-Control: no-cache e/o pragma: No-intestazione della cache nella richiesta HTTP hello.

Valore|Risultato
--|--
Enabled|Consente di no-cache del client HTTP richiede toobe toohello inoltrato server di origine e il server di origine hello restituirà le intestazioni di risposta hello e corpo hello tramite server perimetrale hello toohello indietro HTTP client.
Disabled|Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è richieste no-cache tooprevent dal server di origine toohello inoltrati.

Per tutto il traffico di produzione, è altamente consigliabile tooleave questa funzionalità nello stato disabilitato predefinito. In caso contrario, i server di origine verranno non protetti dagli utenti finali che potrebbero inavvertitamente generare molte richieste no-cache durante l'aggiornamento di pagine web o da hello lettore multimediale comuni che vengono codificati toosend un'intestazione no-cache con ogni richiesta video. Tuttavia, questa funzionalità può essere di gestione temporanea non di produzione di toocertain tooapply utile o directory, il test in toobe contenuto aggiornato di ordine tooallow pull su richiesta dal server di origine hello.

stato della cache di Hello che verrà segnalato per una richiesta che è un server di origine tooan toobe inoltrato a causa di funzionalità toothis è TCP_Client_Refresh_Miss. Il report, gli stati di Cache che è disponibile nel modulo dei report Core hello, fornisce informazioni statistiche in base allo stato della cache. In questo modo si tootrack hello numero e percentuale di richieste che vengono inoltrati tooan server di origine a causa di funzionalità toothis.

**Comportamento predefinito:** Disabled.

###<a name="ignore-origin-no-cache"></a>Ignore Origin no-cache (Ignora origine No-Cache)
**Scopo:** determina se la rete CDN ignorerà hello seguenti direttive servite da un server di origine:

- Cache-Control: private
- Cache-Control: no-store
- Cache-Control: no-cache
- Pragma: no-cache

Informazioni chiave:

- Questa funzionalità può essere configurata mediante la definizione di un elenco delimitato da virgole dei codici di stato per il quale hello sopra direttive verrà ignorato.
- Hello set di codici di stato valido per questa funzionalità è: 200, 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 e 505.
- Disabilitare questa funzionalità impostando il valore vuoto tooa.
- Scadenza toohello modo nella cui cache vengono rilevate le impostazioni, questa funzionalità non può essere associata seguendo le condizioni di corrispondenza hello: 
    - Edge 
    - CNAME
    - Valore letterale intestazione richiesta
    - Carattere jolly intestazione richiesta
    - Metodo richiesta
    - Valore letterale query URL
    - Carattere jolly query URL

**Comportamento predefinito:** il comportamento predefinito prevede hello toohonor sopra direttive.

###<a name="ignore-unsatisfiable-ranges"></a>Ignora gli intervalli che non è possibile soddisfare 
**Scopo:** determina risposta hello che verrà restituito tooclients quando una richiesta genera un codice di stato 416 richiesto non Impossibile attenersi all'intervallo.

Per impostazione predefinita, questo codice di stato viene restituito quando hello specificato non è possibile soddisfare la richiesta di intervallo di byte da un server perimetrale e non è stato specificato un campo di intestazione di richiesta If-Range.

Valore|Risultato
-|-
Enabled|Impedisce che i nostri server edge dalla richiesta di intervallo di byte non validi tooan risponde con un codice di stato 416 richiesto non Impossibile attenersi all'intervallo. I nostri server verranno invece trasmettere l'asset richiesto hello e restituire un messaggio 200 OK hello client.
Disabled|Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è toohonor il codice di stato 416 richiesto non Impossibile attenersi all'intervallo.

**Comportamento predefinito:** Disabled.

###<a name="internal-max-stale"></a>Max-Stale interno
**Scopo:** controlla la durata di memorizzazione asset con il server di origine hello ultimi hello normale scadenza un asset memorizzati nella cache può essere servito da un server perimetrale quando server perimetrale hello è Impossibile toorevalidate hello.

In genere, quando una risorsa max-age dell'orario, server perimetrale hello invierà un server di origine toohello richiesta la riconvalida. Hello server di origine verranno quindi rispondere con un 304 non modificato per fornire server perimetrale hello un nuovo lease asset memorizzati nella cache di hello, oppure con 200 OK per fornire il server perimetrale hello con una versione aggiornata dell'asset memorizzati nella cache di hello.

Se server perimetrale hello è Impossibile tooestablish una connessione con il server di origine hello durante il tentativo di questo tipo una riconvalida, questa funzionalità aggiornata Max interno controlla se e per quanto tempo, hello server perimetrale potrebbe continuare asset di tooserve hello ora aggiornata.

Si noti che questo intervallo di tempo inizia quando scade la durata massima dell'asset hello, non quando hello riconvalida si verifica. Pertanto, il periodo massimo di hello durante il quale un asset può essere soddisfatta senza riconvalida è intervallo hello di tempo specificato da una combinazione di hello max-age più aggiornata di max. Ad esempio, se un asset è stato memorizzato nella cache alle 9:00 con una durata massima di 30 minuti e aggiornata un numero massimo di 15 minuti, quindi tentare una riconvalida non riuscita a 9:44 comporta un utente finale ricevente hello non aggiornati memorizzati nella cache asset, durante un tentativo non riuscito riconvalida 9:46 darà origine a ricezione di un Timeout del Gateway 504 all'utente finale Hello.

Qualsiasi valore configurato per questa funzionalità è stata sostituita dalla Cache-controllo: deve-riconvalidare oppure memorizzare nella Cache-controllo: proxy-revalidate intestazioni ricevute dal server di origine hello. Se uno di tali intestazioni viene ricevuto dal server di origine hello quando viene inizialmente memorizzato nella cache un asset, server perimetrale hello non soddisferà un asset memorizzati nella cache non aggiornato. In tal caso, se hello bordo è un server non è possibile toorevalidate con origine hello intervallo max-age dell'asset hello è scaduto, quindi server perimetrale hello restituirà un 504 Timeout del Gateway.

Informazioni chiave:

- Per configurare questa funzionalità:
    - Se si seleziona il codice di stato hello per il quale verrà applicato un max aggiornata.
    - Specificando un valore integer e quindi selezionando hello unità di tempo desiderato (ad esempio secondi, minuti, ore e così via). Questo valore definisce hello interno max aggiornata che verrà applicata.

- Unità di tempo hello impostazione troppo "Off" verrà disabilitare questa funzionalità. Un asset memorizzato nella cache non verrà servito dopo la normale scadenza.
- Scadenza toohello modo nella cui cache vengono rilevate le impostazioni, questa funzionalità non può essere associata seguendo le condizioni di corrispondenza hello: 
    - Edge 
    - CNAME
    - Valore letterale intestazione richiesta
    - Carattere jolly intestazione richiesta
    - Metodo richiesta
    - Valore letterale query URL
    - Carattere jolly query URL

**Comportamento predefinito:** 2 minuti

###<a name="partial-cache-sharing"></a>Condivisione cache parziale
**Scopo:** determina se una richiesta può generare contenuti parzialmente memorizzati nella cache.

Successivamente, la cache parziale potrebbe essere utilizzati toofulfill nuove richieste per il contenuto finché non viene richiesto di hello contenuto completamente memorizzato nella cache.

Valore|Risultato
-|-
Enabled|Le richieste possono generare contenuti parzialmente memorizzati nella cache.
Disabled|Le richieste è possibile generare solo un oggetto completamente nella cache il contenuto di richiesta la versione di hello.

**Comportamento predefinito:** Disabled.

###<a name="prevalidate-cached-content"></a>Preconvalida contenuto memorizzato nella cache
**Scopo:** determina se i contenuti memorizzati nella cache saranno idonei per la riconvalida anticipata prima della scadenza della durata (TTL).

Definire la quantità hello tempo di scadenza precedenti toohello di hello richiesto durata (TTL) del contenuto durante i quali sarà idoneo per la riconvalida anticipata.

Informazioni chiave:

- Selezione di "Off" come unità di tempo hello richiede sul posto tootake riconvalida dopo la durata (TTL) del contenuto memorizzato nella cache di hello è scaduto. Non è necessario specificare alcun valore di tempo, poiché verrebbe ignorato.

**Comportamento predefinito:** Off. La riconvalida può essere eseguita solo dopo hello durata (TTL) del contenuto memorizzato nella cache è scaduto.

###<a name="refresh-zero-byte-cache-files"></a>Aggiorna i file della cache con zero byte
**Scopo:** determina come viene gestita dai server perimetrali una richiesta da parte di un client HTTP di un asset della cache con 0 byte.

I valori validi sono:

Valore|Risultato
--|--
Enabled|Determina l'asset di hello edge server toore-fetch dal server di origine hello.
Disabled|Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è tooserve le risorse di cache valido su richiesta.
Questa funzionalità non è necessaria per eseguire correttamente operazioni di memorizzazione nella cache o distribuzione di contenuti, ma può essere utile come soluzione alternativa. Ad esempio, i generatori di contenuto dinamici nei server di origine possono causare inavvertitamente le risposte di 0 byte inviate server edge toohello. Questi tipi di risposte, in genere, vengono memorizzati nella cache dai server periferici. Presupponendo che una risposta con 0 byte non sia mai una risposta valida 

Per questo tipo di contenuto, quindi questa funzionalità può impedire questi tipi di risorse servito tooyour client.

**Comportamento predefinito:** Disabled.

###<a name="set-cacheable-status-codes"></a>Imposta codici di stato inseribile nella cache
**Scopo:** definisce il set di hello dei codici di stato che possono comportare contenuto memorizzato nella cache.

Per impostazione predefinita, la memorizzazione nella cache è abilitata solo per le risposte 200 - OK.

Definire un set delimitato da spazi hello desiderato dei codici di stato.

Informazioni chiave:

- Abilitare anche la funzionalità Ignore Origin No-Cache (Ignora origine No-Cache). In caso contrario, è possibile che le risposte diverse da 200 - OK non vengano memorizzate nella cache.
- Hello set di codici di stato valido per questa funzionalità è: 203, 300, 301, 302, 305, 307, 400, 401, 402, 403, 404, 405, 406, 407, 408, 409, 410, 411, 412, 413, 414, 415, 416, 417, 500, 501, 502, 503, 504 e 505.
- Questa funzionalità non può essere utilizzato toodisable la memorizzazione nella cache per le risposte che generano un codice di stato OK 200.

**Comportamento predefinito:** la memorizzazione nella cache è abilitata solo per le risposte che generano un codice di stato 200 - OK.
###<a name="stale-content-delivery-on-error"></a>Distribuzione di contenuto non aggiornato in caso di errore
**Scopo:** 

Determina se scaduto, verrà recapitato contenuto memorizzato nella cache quando si verifica un errore durante la riconvalida della cache o quando hello durante il recupero delle richieste di contenuto dal server di origine cliente hello.

Valore|Risultato
-|-
Enabled|Contenuto aggiornato verrà utilizzato toohello richiedente quando si verifica un errore durante un server di origine tooan di connessione.
Disabled|Errore del server di origine Hello verrà inoltrati toohello richiedente.

**Comportamento predefinito:** Disabled

###<a name="stale-while-revalidate"></a>Client non aggiornato durante la riconvalida
**Scopo:** migliora le prestazioni, consentendo il nostro server edge tooserve toohello contenuto aggiornato richiedente durante la riconvalida.

Informazioni chiave:

- comportamento di Hello di questa funzionalità varia secondo unità di tempo selezionato toohello.
    - **Unità di tempo:** specificare un periodo di tempo e selezionare un tempo unità (ad esempio secondi, minuti, ore, e così via) tooallow obsoleti contenuti. Questo tipo di programma di installazione consente hello CDN tooextend hello durata di tempo può distribuire il contenuto prima di richiedere la convalida in base toohello formula seguente:**TTL** + **mentre riconvalidare ritardo** 
    - **OFF:** selezionare "Off" riconvalida toorequire prima di una richiesta per il contenuto non aggiornato può essere servito.
        - Non specificare un intervallo di tempo poiché non è applicabile e verrebbe ignorato.

**Comportamento predefinito:** Off. La riconvalida deve essere effettuata prima hello richiesto contenuto possa essere utilizzato.

###<a name="comment"></a>Commento
**Scopo:** consente un toobe nota aggiunta all'interno di una regola.

È possibile utilizzare questa funzionalità è tooprovide ulteriori informazioni sull'utilizzo generico di hello di una regola o perché corrispondono a una particolare condizione o una funzionalità è stata aggiunta la regola toohello.

Informazioni chiave:

- Non possono essere specificati più di 150 caratteri.
- Verificare che tooonly utilizzare caratteri alfanumerici.
- Questa funzionalità non influisce sul comportamento hello della regola di hello. Si tratta semplicemente tooprovide un'area in cui è possibile fornire informazioni per riferimento futuro o che possono essere utili durante la risoluzione dei problemi regola hello.
 
## <a name="headers"></a>Headers

Queste funzionalità sono progettate tooadd, modificare o eliminare le intestazioni da hello richiesta o risposta.

Nome | Scopo
-----|--------
Intestazione di risposta Age | Determina se un'intestazione di risposta Age verrà incluso nella risposta di hello inviata toohello richiedente.
Intestazioni di risposta di debug per la cache | Determina se una risposta può includere l'intestazione della risposta X-EC-Debug hello che fornisce informazioni su criteri di cache di hello per hello richiesto asset.
Modifica intestazione richiesta client | Sovrascrive, aggiunge o elimina un'intestazione da una richiesta.
Modificare intestazione risposta client | Sovrascrive, aggiunge o elimina un'intestazione da una risposta.
Imposta intestazione personalizzata IP client | Consente l'indirizzo IP hello del client richiedente hello toobe toohello aggiunto richiesta come un'intestazione personalizzata.

###<a name="age-response-header"></a>Intestazione di risposta Age
**Scopo**: determina se debba essere inclusa un'intestazione di risposta Age in hello risposta inviata toohello richiedente.
Valore|Risultato
--|--
Enabled | intestazione della risposta Age Hello verrà inclusi nella risposta di hello inviata toohello richiedente.
Disabled | intestazione della risposta Age Hello verrà esclusi dalla risposta hello inviato toohello richiedente.

**Comportamento predefinito:**: Disabled.

###<a name="debug-cache-response-headers"></a>Intestazioni di risposta di debug per la cache
**Scopo:** determina se una risposta può includere l'intestazione della risposta X-EC-Debug che fornisce informazioni su criteri di cache di hello per hello richiesto asset.

Eseguire il debug di risposta della cache intestazioni verranno inclusi nella risposta hello quando entrambe operazioni hello seguenti sono vere:

- eseguire il Debug di funzionalità di intestazioni di risposta della Cache di Hello è stata abilitata nella richiesta di hello desiderato.
- Hello sopra richiesta definisce il set di hello di intestazioni di risposta della cache di debug che verranno inclusi nella risposta hello.

Eseguire il debug di risposta della cache, le intestazioni possono essere richiesti includendo la seguente intestazione hello e hello direttive desiderate nella richiesta di hello:

X-EC-Debug: _Direttiva1_,_Direttiva2_,_DirettivaN_

**Esempio:**

X-EC-Debug: x-ec-cache,x-ec-check-cacheable,x-ec-cache-key,x-ec-cache-state

Valore|Risultato
-|-
Enabled|Le richieste di intestazioni di risposta di debug per la cache restituiranno una risposta che include l'intestazione X-EC-Debug.
Disabled|L'intestazione della risposta X-EC-Debug verrà esclusi dalla risposta hello.

**Comportamento predefinito:** Disabled.

###<a name="modify-client-response-header"></a>Modificare intestazione risposta client
**Scopo:** ogni richiesta contiene un set di [intestazioni di richiesta]() che la descrivono. Questa funzionalità può:

- Aggiungere o sovrascrivere il valore di hello assegnato tooa intestazione della richiesta. Se l'intestazione della richiesta specificato hello non esiste, quindi questa funzionalità verrà aggiunte toohello richiesta.
- Eliminare un'intestazione di richiesta dalla richiesta hello.

Le richieste vengono inoltrate a server di origine tooan rifletteranno hello apportate da questa funzionalità.

Una delle seguenti azioni hello può essere eseguita su un'intestazione della richiesta:

Opzione|Descrizione|Esempio
-|-|-
Append|Hello specificato verrà aggiunto valore toend del valore dell'intestazione di richiesta esistente hello.|**Valore intestazione richiesta (Client):**Value1 <br/> **Valore intestazione richiesta (Motore regole HTTP):** Value2 <br/>**Valore nuova intestazione di richiesta:** Value1Value2
Overwrite|valore dell'intestazione sarà set toohello richiesta di Hello valore specificato.|**Valore intestazione richiesta (Client):**Value1 <br/>**Valore intestazione richiesta (Motore regole HTTP):** Value2 <br/>**Valore nuova intestazione richiesta:** Value2 <br/>
Elimina|Elimina l'intestazione della richiesta specificato hello.|**Valore intestazione richiesta (Client):**Value1 <br/> **Modificare la configurazione di intestazione della richiesta Client:** intestazione richiesta Delete hello in questione. <br/>**Risultato:** hello specificato l'intestazione della richiesta non verrà inoltrato al server di origine toohello.

Informazioni chiave:

- Assicurarsi che il valore di hello specificato nell'opzione Name è una corrispondenza esatta per l'intestazione della richiesta desiderato hello.
- Caso non viene preso in considerazione per scopo hello di identificazione di un'intestazione. Ad esempio, uno dei seguenti varianti del nome di intestazione Cache-Control hello può essere utilizzato tooidentify è:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- Verificare che tooonly utilizzare caratteri alfanumerici, trattini o caratteri di sottolineatura quando si specifica un nome di intestazione.
- L'eliminazione di un'intestazione ne impedirà inoltrati server di origine tooan nostri server edge.
- Hello intestazioni seguenti sono riservate e non possono essere modificate da questa funzionalità:
    - forwarded
    - host
    - via
    - Avviso
    - x-forwarded-for
    - Tutti i nomi di intestazione che iniziano con "x-ec" sono riservati.

###<a name="modify-client-response-header"></a>Modificare intestazione risposta client
Ogni risposta contiene un set di [intestazioni di risposta]() che la descrivono. Questa funzionalità può:

- Aggiungere o sovrascrivere il valore di hello assegnato tooa intestazione della risposta. Se l'intestazione della richiesta specificato hello non esiste, quindi questa funzionalità verrà aggiunte toohello risposta.
- Eliminare un'intestazione di risposta dalla risposta hello.

Per impostazione predefinita, i valori delle intestazioni di risposta vengono definiti da un server di origine e dai server periferici.

Una delle seguenti azioni hello può essere eseguita su un'intestazione di risposta:

Opzione|Descrizione|Esempio
-|-|-
Append|Hello specificato verrà aggiunto valore toend del valore dell'intestazione di richiesta esistente hello.|**Valore intestazione risposta (Client):**Value1 <br/> **Valore intestazione risposta (Motore regole HTTP):** Value2 <br/>**Valore nuova intestazione risposta:** Value1Value2
Overwrite|valore dell'intestazione sarà set toohello richiesta di Hello valore specificato.|**Valore intestazione risposta (Client):**Value1 <br/>**Valore intestazione risposta (Motore regole HTTP):** Value2 <br/>**Valore nuova intestazione risposta:** Value2 <br/>
Elimina|Elimina l'intestazione della richiesta specificato hello.|**Valore intestazione richiesta (Client):**Value1 <br/> **Modificare la configurazione di intestazione della richiesta Client:** intestazione della risposta hello Delete in questione. <br/>**Risultato:** hello specificato l'intestazione della risposta non verrà inoltrata toohello richiedente.

Informazioni chiave:

- Assicurarsi che il valore di hello specificato nell'opzione Name è una corrispondenza esatta per l'intestazione della risposta desiderato hello. 
- Caso non viene preso in considerazione per scopo hello di identificazione di un'intestazione. Ad esempio, uno dei seguenti varianti del nome di intestazione Cache-Control hello può essere utilizzato tooidentify è:
    - cache-control
    - CACHE-CONTROL
    - cachE-Control
- L'eliminazione di un'intestazione ne impedirà inoltrati toohello richiedente.
- Hello intestazioni seguenti sono riservate e non possono essere modificate da questa funzionalità:
    - accept-encoding
    - age
    - connection
    - content-encoding
    - content-length
    - content-range
    - date
    - server
    - trailer
    - transfer-encoding
    - Aggiornamento
    - vary
    - via
    - Avviso
    - Tutti i nomi di intestazione che iniziano con "x-ec" sono riservati.

###<a name="set-client-ip-custom-header"></a>Imposta intestazione personalizzata IP client
**Scopo:** aggiunge un'intestazione personalizzata che identifica i client richiedente hello tramite una richiesta di toohello indirizzo IP.

L'opzione Nome intestazione definisce il nome di hello dell'intestazione della richiesta personalizzata hello in cui verrà archiviato hello indirizzo IP del client.

Questa funzionalità consente a un cliente toofind server di origine gli indirizzi IP client tramite un'intestazione personalizzata. Se la richiesta hello viene servita dalla cache, il server di origine hello non venire informato di indirizzo IP hello del client. È consigliabile quindi usare questa funzionalità con reti ADN e asset che non verranno memorizzati nella cache.

Verificare che il nome dell'intestazione specificato hello non corrisponde a hello seguenti:

- Nomi di intestazioni di richiesta standard. L'elenco dei nomi di intestazioni standard è disponibile in [RFC 2616](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html).
- Nomi di intestazioni riservate:
    - forwarded-for
    - host
    - vary
    - via
    - Avviso
    - x-forwarded-for
    - Tutti i nomi di intestazione che iniziano con "x-ec" sono riservati.
 
## <a name="logs"></a>Log

Queste funzionalità sono dati hello toocustomize progettato archiviati nei file di registro non elaborati.

Nome | Scopo
-----|--------
Campo 1 log personalizzato | Determina il formato di hello e il contenuto di hello che verrà assegnato toohello campo di log personalizzato in un file di registro non elaborati.
Stringa di query log | Determina se una stringa di query verrà memorizzata con URL hello nei registri di accesso.

###<a name="custom-log-field-1"></a>Campo 1 log personalizzato
**Scopo:** determina il formato di hello e il contenuto di hello che verrà assegnato toohello campo di log personalizzato in un file di registro non elaborati.

scopo principale di Hello dietro il campo personalizzato è tooallow toodetermine verranno archiviati i valori di intestazione di richiesta e risposta nei file di registro.

Per impostazione predefinita, il campo di log personalizzato hello viene chiamato "x-ec_custom-1". Tuttavia, il nome di hello di questo campo può essere personalizzato il [pagina Impostazioni di registro non elaborati]().

la formattazione che è necessario utilizzare le intestazioni di richiesta e risposta toospecify Hello è definito di seguito.

Tipo di intestazione|Format|Esempi
-|-|-
Intestazione di richiesta|%{[RequestHeader]()}[i]() | %{Accept-Encoding}i <br/> {Referer}i <br/> %{Authorization}i
Intestazione di risposta|%{[ResponseHeader]()}[o]()| %{Age}o <br/> %{Content-Type}o <br/> %{Cookie}o

Informazioni chiave:

- Un campo di log personalizzato può contenere qualsiasi combinazione di campi di intestazione e testo normale.
- I caratteri validi per questo campo includono seguente hello: alfanumerici (ad esempio, 0-9, a-z e A-Z), trattini, i due punti, punti e virgola, apostrofi, virgole, punti, caratteri di sottolineatura, segni di uguale, tra parentesi, parentesi quadre e spazi. Hello simbolo di percentuale e parentesi graffe sono consentite solo quando utilizzato toospecify un campo di intestazione.
- ortografia Hello per ogni campo di intestazione specificato deve corrispondere a nome di intestazione di richiesta/risposta desiderato hello.
- Se si desidera toospecify più intestazioni, quindi, è consigliabile usare un separatore tooindicate ogni intestazione. Per ogni intestazione, ad esempio, è possibile usare un'abbreviazione. Di seguito è riportata una sintassi di esempio.
    - AE: %{Accept-Encoding}i A: %{Authorization}i CT: %{Content-Type}o 

**Valore predefinito:** -

###<a name="log-query-string"></a>Stringa di query log
**Scopo:** determina se una stringa di query verrà memorizzata con URL hello nei registri di accesso.

Valore|Risultato
-|-
Enabled|Consente l'archiviazione di hello di stringhe di query durante la registrazione URL in un log di accesso. Se un URL non contiene una stringa di query, questa opzione non produrrà alcun effetto.
Disabled|Ripristina impostazioni predefinite hello. comportamento predefinito di Hello è tooignore le stringhe di query durante la registrazione URL in un log di accesso.

**Comportamento predefinito:** Disabled.

<!---
## Optimize

These features determine whether a request will undergo hello optimizations provided by Edge Optimizer.

Name | Purpose
-----|--------
Edge Optimizer | Determines whether Edge Optimizer can be applied tooa request.
Edge Optimizer – Instantiate Configuration | Instantiates or activates hello Edge Optimizer configuration associated with a site.

###Edge Optimizer
**Purpose:** Determines whether Edge Optimizer can be applied tooa request.

If this feature has been enabled, then hello following criteria must also be met before hello request will be processed by Edge Optimizer:

- hello requested content must use an edge CNAME URL.
- hello edge CNAME referenced in hello URL must correspond tooa site whose configuration has been activated in a rule.

This feature requires the ADN platform and hello Edge Optimizer feature.

Value|Result
-|-
Enabled|Indicates that hello request is eligible for Edge Optimizer processing.
Disabled|Restores hello default behavior. hello default behavior is toodeliver content over the ADN platform without any additional processing.

**Default Behavior:** Disabled
 

###Edge Optimizer - Instantiate Configuration
**Purpose:** Instantiates or activates hello Edge Optimizer configuration associated with a site.

This feature requires the ADN platform and hello Edge Optimizer feature.

Key information:

- Instantiation of a site configuration is required before requests toohello corresponding edge CNAME can be processed by Edge Optimizer.
- This instantiation only needs toobe performed a single time per site configuration. A site configuration that has been instantiated will remain in that state until hello Edge Optimizer – Instantiate Configuration feature that references it is removed from hello rule.
- hello instantiation of a site configuration does not mean that all requests toohello corresponding edge CNAME will automatically be processed by Edge Optimizer. The Edge Optimizer feature determines whether an individual request will be processed.

If hello desired site does not appear in hello list, then you should edit its configuration and verify that the Active option has been marked.

**Default Behavior:** Site configurations are inactive by default.
--->

## <a name="origin"></a>Origine

Queste funzionalità sono progettate toocontrol come hello CDN comunica con un server di origine.

Nome | Scopo
-----|--------
Numero massimo di richieste Keep-Alive | Definisce il numero massimo di hello di richieste per una connessione Keep-Alive prima che venga chiuso.
Intestazioni speciali proxy | Definisce il set di hello specifiche della rete CDN di intestazioni di richiesta che verrà inoltrato da un server di origine tooan server perimetrale.


###<a name="maximum-keep-alive-requests"></a>Numero massimo di richieste Keep-Alive
**Scopo:** consente di definire hello il numero massimo di richieste per una connessione Keep-Alive prima che venga chiuso.

L'impostazione di hello massimo valore del numero di richieste tooa bassa è fortemente sconsigliata e può comportare un calo delle prestazioni.

Informazioni chiave:

- Specificare questo valore come un numero intero.
- Non includere virgole o punti in hello specificato valore.

**Valore predefinito:** 10.000 richieste

###<a name="proxy-special-headers"></a>Intestazioni speciali proxy
**Scopo:** definisce il set di hello di [intestazioni di richiesta specifici della rete CDN]() che verranno inoltrati da un server di origine tooan server perimetrale.

Informazioni chiave:

- Ogni intestazione di richiesta specifici della rete CDN definito in questa funzionalità verrà inoltrato tooan server di origine.
- Evitare un'intestazione di richiesta specifici della rete CDN viene inoltrato al server di origine tooan rimuovendolo dall'elenco.

**Comportamento predefinito:** tutti [intestazioni di richiesta specifici della rete CDN]() verranno inoltrati toohello server di origine.

## <a name="specialty"></a>Funzionalità specializzate

Queste funzionalità offrono caratteristiche avanzate che devono essere usate solo dagli utenti esperti.

Nome | Scopo
-----|--------
Metodi HTTP inseribile nella cache | Determina il set di hello di metodi HTTP aggiuntivi che possono essere memorizzati nella cache nella rete.
Dimensioni corpo richiesta inseribile nella cache | Definisce una soglia di hello per determinare se una risposta POST può essere memorizzati nella cache.

###<a name="cacheable-http-methods"></a>Metodi HTTP inseribile nella cache
**Scopo:** determina hello set di metodi HTTP aggiuntivi che possono essere memorizzati nella cache nella rete.

Informazioni chiave:

- Questa funzionalità presuppone che le risposte GET vengano sempre memorizzate nella cache. Di conseguenza, il metodo HTTP GET hello non deve essere inclusa durante l'impostazione di questa funzionalità.
- Questa funzionalità supporta solo il metodo HTTP POST hello. Per abilitare la memorizzazione nella cache della risposta POST, impostare questa funzionalità su POST. 
- Per impostazione predefinita, vengono memorizzate nella cache solo le richieste con un corpo di dimensioni inferiori a 14 Kb. Utilizzare la funzionalità di dimensioni di corpo della richiesta memorizzabile nella cache per impostare hello dimensione massima del corpo della richiesta.

**Comportamento predefinito:** vengono memorizzate nella cache solo le risposte GET.

###<a name="cacheable-request-body-size"></a>Dimensioni corpo richiesta inseribile nella cache

**Scopo:** soglia hello definisce per determinare se una risposta POST può essere memorizzati nella cache.

Questa soglia viene determinata specificando la dimensione massima del corpo della richiesta. Non verranno memorizzate nella cache le richieste il cui corpo supera le dimensioni specificate.

Informazioni chiave:

- Questa funzionalità è applicabile solo se le risposte POST sono idonee per la memorizzazione nella cache. Utilizzare funzionalità di metodi HTTP memorizzabile nella cache di hello per abilitare la memorizzazione nella cache di richiesta POST.
- corpo della richiesta Hello viene preso in considerazione per:
    - Valori x-www-form-urlencoded
    - Garantire una chiave di cache univoca
- La definizione di un valore molto alto per le dimensioni massime del corpo della richiesta può rallentare le prestazioni in fase di distribuzione dei contenuti.
    - **Valore consigliato:** 14 Kb
    - **Valore minimo:** 1 Kb

**Comportamento predefinito:** 14 Kb
 
## <a name="url"></a>URL

Queste funzionalità consentono un toobe richiesta reindirizzato o riscrivere tooa altro URL.

Nome | Scopo
-----|--------
Segui reindirizzamenti | Determina se le richieste possono essere reindirizzato toohello hostname definito nell'intestazione Location hello restituito da un server di origine del cliente.
Reindirizzamento URL | Reindirizza le richieste tramite intestazione Location hello.
Riscrittura URL  | Riscrive l'URL della richiesta hello.

###<a name="follow-redirects"></a>Segui reindirizzamenti
**Scopo:** determina se le richieste possono essere reindirizzato toohello hostname definito nell'intestazione della posizione restituita da un server di origine del cliente.

Informazioni chiave:

- Le richieste possono essere solo CNAME tooedge reindirizzato corrispondenti toohello stessa piattaforma.

Valore|Risultato
-|-
Enabled|Le richieste possono essere reindirizzate.
Disabled|Le richieste non verranno reindirizzate.

**Comportamento predefinito:** Disabled.
###<a name="url-redirect"></a>Reindirizzamento URL
**Scopo:** reindirizza le richieste tramite l'intestazione Location.

configurazione di Hello di questa funzionalità richiede l'impostazione hello le opzioni seguenti:

Opzione|Descrizione
-|-
Codice|Selezionare il codice di risposta hello che verrà restituito toohello richiedente.
Source & Pattern (Origine e modello)| Queste impostazioni definiscono un modello di URI di richiesta che identifica il tipo di hello di richieste che può essere reindirizzato. Verranno reindirizzate solo le richieste con URL soddisfa entrambe hello seguenti criteri: <br/> <br/> **Origine** (o un punto di accesso dei contenuti): selezionare un percorso relativo che identifica un server di origine. Si tratta di sezione "/XXXX/" hello e il nome dell'endpoint. <br/> **Origine (modello):** deve essere definito un modello che identifica le richieste in base al percorso relativo. Questo modello di espressione regolare è necessario definire un percorso che inizia direttamente dopo hello selezionati in precedenza, il punto di accesso al contenuto (vedere sopra). <br/> -Verificare che Criteri di URI di richiesta di hello (ad esempio, origine e modello) definiti in precedenza non sia in conflitto con le condizioni di corrispondenza definite per questa funzionalità. <br/> -Verificare che toospecify un modello. Utilizzo di un valore vuoto come modello hello corrisponderà solo a cartella radice di toohello le richieste del server di origine selezionato hello (ad esempio, http://cdn.mydomain.com/).
Destination| Definire l'URL di hello hello toowhich sopra le richieste verrà reindirizzata. <br/> Costruire l'URL in modo dinamico usando: <br/> - Un modello di espressione regolare <br/>- Variabili HTTP <br/> Sostituire i valori hello acquisiti nel modello di origine hello nello schema di destinazione hello usando $ _n_  in  _n_  identifica un valore dall'ordine hello in cui è stato acquisito. Ad esempio, $1 rappresenta primo valore hello acquisiti nel modello di origine hello, mentre $2 rappresenta hello secondo valore. <br/> 
È altamente consigliabile toouse un URL assoluto. utilizzo di Hello di un URL relativo può reindirizzare percorso di rete CDN URL tooan non valido.

**Scenario di esempio**

In questo esempio verrà illustrato come un bordo URL CNAME che risolve toothis tooredirect CDN URL di base: http://marketing.azureedge.net/brochures

Qualificazione richiede sarà reindirizzato toothis edge base URL CNAME: http://cdn.mydomain.com/resources

Il reindirizzamento URL può essere ottenuto tramite hello seguente configurazione:![](./media/cdn-rules-engine-reference/cdn-rules-engine-redirect.png)

**Punti principali:**

- funzionalità di reindirizzamento URL Hello definisce hello URL a cui verrà reindirizzato richiesta. Non sono quindi necessarie condizioni di corrispondenza aggiuntive. Anche se la condizione di corrispondenza hello è stata definita come "Sempre", solo le richieste che toohello punto "brochure" cartella di origine cliente "marketing" hello verrà reindirizzata. 
- Tutte le richieste corrispondente sarà reindirizzato toohello bordo che CNAME URL definito nell'opzione di destinazione. 
    - Scenario di esempio #1: 
        - Richiesta di esempio (URL CDN): http://marketing.azureedge.net/brochures/widgets.pdf 
        - URL richiesta (dopo il reindirizzamento): http://cdn.mydomain.com/resources/widgets.pdf  
    - Scenario di esempio #2: 
        - Richiesta di esempio (URL CDN periferico): http://marketing.mydomain.com/brochures/widgets.pdf 
        - URL richiesta (dopo il reindirizzamento): http://cdn.mydomain.com/resources/widgets.pdf  Sample scenario
    - Scenario di esempio #3: 
        - Richiesta di esempio (URL CNAME periferico): http://brochures.mydomain.com/campaignA/final/productC.ppt 
        - URL richiesta (dopo il reindirizzamento): http://cdn.mydomain.com/resources/campaignA/final/productC.ppt  
- variabile di Hello schema richiesta (% {schema}) è stato sfruttato nell'opzione di destinazione. In questo modo che lo schema della richiesta che hello rimane invariato dopo il reindirizzamento.
- i segmenti di URL Hello che sono stati acquisiti dalla richiesta di hello vengono accodati toohello nuovo URL tramite "$1".
 
###<a name="url-rewrite"></a>Riscrittura URL
**Scopo:** riscrive l'URL della richiesta hello.

Informazioni chiave:

- configurazione di Hello di questa funzionalità richiede l'impostazione hello le opzioni seguenti:

Opzione|Descrizione
-|-
 Source & Pattern (Origine e modello) | Queste impostazioni definiscono un modello di URI di richiesta che identifica il tipo di hello di richieste che può essere riscritto. Verranno riscritto solo le richieste con URL soddisfa entrambe hello seguenti criteri: <br/>     - **Origine (o un punto di accesso dei contenuti):** selezionare un percorso relativo che identifica un server di origine. Si tratta di sezione "/XXXX/" hello e il nome dell'endpoint. <br/> - **Origine (modello):** deve essere definito un modello che identifica le richieste in base al percorso relativo. Questo modello di espressione regolare è necessario definire un percorso che inizia direttamente dopo hello selezionati in precedenza, il punto di accesso al contenuto (vedere sopra). <br/> Assicurarsi che non siano in conflitto con una delle condizioni di corrispondenza hello è definite per questa funzionalità hello richiesta URI criteri (ad esempio, origine e modello) definiti in precedenza. Verificare che toospecify un modello. Utilizzo di un valore vuoto come modello hello corrisponderà solo a cartella radice di toohello le richieste del server di origine selezionato hello (ad esempio, http://cdn.mydomain.com/). 
 Destination  |Definire un URL relativo hello hello toowhich sopra richieste verrà riscritto da: <br/>    1. Selezionando un punto di accesso dei contenuti che identifichi un server di origine. <br/>    2. Definendo di un percorso tramite: <br/>        - Un modello di espressione regolare <br/>        - Variabili HTTP <br/> <br/> Sostituire i valori hello acquisiti nel modello di origine hello nello schema di destinazione hello usando $ _n_  in  _n_  identifica un valore dall'ordine hello in cui è stato acquisito. Ad esempio, $1 rappresenta primo valore hello acquisiti nel modello di origine hello, mentre $2 rappresenta hello secondo valore. 
 Questa funzionalità consente che i nostri server edge toorewrite hello URL senza eseguire un reindirizzamento tradizionale. Ciò significa che richiedente hello riceverà hello risposta entro lo stesso codice come se venisse richiesta URL hello riscritto.

**Scenario di esempio 1**

In questo esempio verrà illustrato come un bordo URL CNAME che risolve toothis tooredirect CDN URL di base: http://marketing.azureedge.net/brochures/

Qualificazione richiede sarà reindirizzato toothis edge base URL CNAME: http://MyOrigin.azureedge.net/resources/

Il reindirizzamento URL può essere ottenuto tramite hello seguente configurazione:![](./media/cdn-rules-engine-reference/cdn-rules-engine-rewrite.png)

**Scenario di esempio 2**

In questo esempio verrà illustrato come tooredirect un URL CNAME bordo da MAIUSCOLI toolowercase tramite espressioni regolari.

Il reindirizzamento URL può essere ottenuto tramite hello seguente configurazione:![](./media/cdn-rules-engine-reference/cdn-rules-engine-to-lowercase.png)


**Punti principali:**

- funzionalità di riscrittura URL Hello definisce hello URL che verrà riscritto richiesta. Non sono quindi necessarie condizioni di corrispondenza aggiuntive. Anche se la condizione di corrispondenza hello è stata definita come "Sempre", solo le richieste che toohello punto "brochure" cartella di origine cliente "marketing" hello verrà riscritto.

- i segmenti di URL Hello che sono stati acquisiti dalla richiesta di hello vengono accodati toohello nuovo URL tramite "$1".



###<a name="compatibility"></a>Compatibilità

Questa funzionalità include corrispondenti ai criteri che devono essere soddisfatte prima di poter essere applicati tooa richiesta. In ordine tooprevent impostazione in conflitto i criteri di corrispondenza, questa funzionalità è incompatibile con hello seguendo le condizioni di corrispondenza:

- Numero AS
- Origine CDN
- Indirizzo IP client
- Origine cliente
- Schema richiesta
- Directory percorso URL
- Estensione percorso URL
- Nome file percorso URL
- Valore letterale percorso URL
- Espressione regolare percorso URL
- Carattere jolly percorso URL
- Valore letterale query URL
- Parametro query URL
- Espressione regolare query URL
- Carattere jolly query URL


## <a name="next-steps"></a>Passaggi successivi
* [Informazioni di riferimento sul motore regole](cdn-rules-engine-reference.md)
* [Espressioni condizionali del motore regole](cdn-rules-engine-reference-conditional-expressions.md)
* [Condizioni di corrispondenza del motore regole](cdn-rules-engine-reference-match-conditions.md)
* [Override del comportamento HTTP predefinito utilizzando il motore regole di hello](cdn-rules-engine.md)
* [Panoramica della rete CDN di Azure](cdn-overview.md)
