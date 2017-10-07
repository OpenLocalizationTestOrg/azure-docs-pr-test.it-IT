---
title: procedure consigliate aaaBest e Guida alla risoluzione dei problemi per le applicazioni di nodo per le app Web di Azure
description: Altre procedure consigliate hello e procedure di risoluzione dei problemi per le applicazioni di nodo per le app Web di Azure.
services: app-service\web
documentationcenter: nodejs
author: ranjithr
manager: wadeh
editor: 
ms.assetid: 387ea217-7910-4468-8987-9a1022a99bef
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 06/06/2016
ms.author: ranjithr
ms.openlocfilehash: 975898142a224f14df1091a46d16e9074d9e2831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-and-troubleshooting-guide-for-node-applications-on-azure-web-apps"></a>Procedure consigliate e guida alla risoluzione dei problemi per le applicazioni Node in App Web di Azure
[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

In questo articolo verranno illustrate le procedure consigliate di hello e procedure di risoluzione dei problemi per [applicazioni nodo](app-service-web-get-started-nodejs.md) in esecuzione in Azure WebApp (con [iisnode](https://github.com/azure/iisnode)).

> [!WARNING]
> Prestare attenzione durante l'uso delle procedure di risoluzione dei problemi nel sito di produzione. Si consiglia di tootroubleshoot l'app in una non di produzione del programma di installazione, ad esempio slot di gestione temporanea e quando non è stato risolto il problema di hello, scambio di slot di gestione temporanea con slot di produzione.
> 
> 

## <a name="iisnode-configuration"></a>Configurazione IISNODE
Questo [file di schema](https://github.com/Azure/iisnode/blob/master/src/config/iisnode_schema_x64.xml) Mostra tutte le impostazioni di hello che possono essere configurate per iisnode. Alcune impostazioni che si riveleranno utili per l'applicazione hello sono:

* nodeProcessCountPerApplication
  
    Questa impostazione controlla il numero di hello di processi di nodo che vengono avviate per ogni applicazione IIS. Il valore predefinito è 1. È possibile avviare tante node.exe come il numero di core VM impostando questo too0. Valore consigliato è 0 per la maggior parte delle applicazioni in modo è possibile utilizzare tutti i core hello nel computer. Node.exe è singolo thread in modo uno node.exe utilizzerà un massimo di 1 core e tooget le massime prestazioni dall'applicazione nodo si tooutilize tutti i core.
* nodeProcessCommandLine
  
    Questa impostazione Controlla hello percorso toohello node.exe. È possibile impostare questa versione di node.exe tooyour toopoint valore.
* maxConcurrentRequestsPerProcess
  
    Questa impostazione Controlla numero massimo di hello di richieste simultanee inviato da iisnode tooeach node.exe. In azure WebApp, valore predefinito hello è infinito. Non è tooworry su questa impostazione. All'esterno di azure WebApp, valore predefinito di hello è 1024. È possibile tooconfigure a seconda di quanti richiede l'applicazione ottiene e la velocità con cui l'applicazione elabora ogni richiesta.
* maxNamedPipeConnectionRetry
  
    Questa impostazione Controlla hello numero massimo iisnode ritenterà la connessione su hello denominato richiesta hello di pipe toosend su toonode.exe. Questa impostazione in combinazione con namedPipeConnectionRetryDelay determina hello timeout totale di ogni richiesta all'interno di iisnode. Il valore predefinito è 200 in App Web di Azure. Timeout totale in secondi = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
* namedPipeConnectionRetryDelay
  
    Questa quantità di hello impostazione controlli di tempo (in ms) iisnode dovrà attendere tra ogni tentativo toosend richiesta toonode.exe su hello denominato pipe. Il valore predefinito è 250 ms.
    Timeout totale in secondi = (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000
  
    Per impostazione predefinita il timeout totale di hello in iisnode in azure WebApp è 200 \* 250ms = 50 secondi.
* logDirectory
  
    Questa impostazione Controlla directory hello in iisnode registrerà stdout/stderr. Il valore predefinito è iisnode ovvero directory script principale relativo toohello (directory in cui è presente server.js principale)
* debuggerExtensionDll
  
    Questa impostazione controlla la versione di node-inspector verrà usata da iisnode durante il debug dell'applicazione Node. Attualmente iisnode-controllo-0.7.3.dll e iisnode inspector.dll hello solo 2 valori sono validi per questa impostazione. Il valore predefinito è iisnode-inspector-0.7.3.dll. versione di iisnode-controllo-0.7.3.dll Usa nodo-controllo-0.7.3 e WebSocket, pertanto sarà necessario tooenable WebSocket in toouse l'App Web di azure questa versione. Vedere <http://www.ranjithr.com/?p=98> per ulteriori informazioni su come tooconfigure iisnode toouse hello nuovo nodo-controllo.
* flushResponse
  
    comportamento predefinito di Hello di IIS è che memorizza nel buffer dei dati di risposta di too4MB prima di scaricare o fino al termine di hello di risposta hello, verifica per primo. iisnode offre un'impostazione di questo comportamento toooverride di configurazione: tooflush un frammento del corpo entità della risposta hello appena iisnode riceve da node.exe, è necessario tooset hello iisnode/@flushResponse attributo nel file Web. config too'true':
  
    ```
    <configuration>    
        <system.webServer>    
            <!-- ... -->    
            <iisnode flushResponse="true" />    
        </system.webServer>    
    </configuration>
    ```
  
    L'abilitazione lo scaricamento di ogni frammento del corpo entità della risposta hello aggiunge overhead delle prestazioni che consente di ridurre la velocità effettiva hello del sistema hello del 5% (a partire da v0.1.13), pertanto è ottimale tooscope questo tooendpoints unica impostazione che richiedono il flusso di risposta (ad esempio utilizzando hello <location> elemento hello di Web. config)
  
    In aggiunta toothis, per lo streaming di applicazioni, sarà necessario tooalso set responseBufferLimit del too0 gestore iisnode.
  
    ```
    <handlers>    
        <add name="iisnode" path="app.js" verb="\*" modules="iisnode" responseBufferLimit="0"/>    
    </handlers>
    ```
* watchedFiles
  
    Si tratta di un elenco di file separato da punti e virgola che sarà controllato per rilevare le modifiche. Un file tooa modifica comporta toorecycle applicazione hello. Ogni voce è costituito da un nome di directory facoltativo più di un nome file richiesto che sono directory toohello relativo punto di ingresso principale dell'applicazione hello in cui si trova. I caratteri jolly sono consentiti nelle solo parte del nome file hello. Il valore predefinito è "\*.js;web.config"
* recycleSignalEnabled
  
    Il valore predefinito è False. Se abilitata, l'applicazione del nodo può connettersi tooa denominato pipe (variabile di ambiente IISNODE\_controllo\_PIPE) e inviare un messaggio "riciclo". In questo modo hello w3wp toorecycle normalmente.
* idlePageOutTimePeriod
  
    Il valore predefinito è 0, ovvero questa funzionalità è disabilitata. Quando set toosome valore maggiore di 0, iisnode effettua il paging tutti i relativi elementi figlio elabora ogni millisecondi 'idlePageOutTimePeriod'. cosa significa che, paging toounderstand consultare toothis [documentazione](https://msdn.microsoft.com/library/windows/desktop/ms682606.aspx). Questa impostazione sarà utile per le applicazioni che utilizzano una grande quantità di memoria e si desidera toopageout memoria toodisk occasionalmente toofree backup parte della RAM.

> [!WARNING]
> Prestare attenzione quando si abilita hello seguire le impostazioni di configurazione di applicazioni di produzione. Toonot si consiglia di attivare l'applicazioni di produzione in tempo reale.
> 
> 

* debugHeaderEnabled
  
    valore predefinito di Hello è false. Se impostato, tootrue iisnode aggiungerà una risposta HTTP risposta intestazione iisnode debug tooevery HTTP invia il valore dell'intestazione di debug iisnode hello è un URL. Esaminando il frammento di URL hello possono potranno singole parti di informazioni diagnostiche, ma viene ottenuta una migliore visualizzazione aprendo hello URL nel browser hello.
* loggingEnabled
  
    Questa impostazione controlla la registrazione di hello di stdout e stderr da iisnode. Iisnode verrà acquisire stdout/stderr dai processi di nodo che viene avviato e scrittura directory toohello specificato nell'impostazione di 'logDirectory' hello. Dopo aver attivato attiva, l'applicazione verrà scritta registri toohello file system e a seconda della quantità di hello di registrazione eseguita dall'applicazione hello, potrebbe essere implicazioni sulle prestazioni.
* devErrorsEnabled
  
    Il valore predefinito è False. Se impostato, tootrue iisnode verrà visualizzato il codice di stato HTTP hello e codice di errore Win32 nel browser. codice win32 Hello possono risultare utile per determinati tipi di problemi di debug.
* debuggingEnabled (non abilitare questa impostazione nel sito di produzione live)
  
    Questa impostazione controlla la funzionalità di debug. Iisnode è integrato con node-inspector. Abilitando questa impostazione, si abilita il debug dell'applicazione Node. Dopo aver abilitata questa impostazione, iisnode verrà layout hello necessarie nodo-controllo file nella directory 'debuggerVirtualDir' nel primo debug richiesta tooyour nodo un'applicazione hello. È possibile caricare hello nodo-controllo inviando una richiesta toohttp://yoursite/server.js/debug. Segmento di URL hello debug è possibile controllare con l'impostazione 'debuggerPathSegment'. Per impostazione predefinita, debuggerPathSegment='debug'. È possibile impostare questo GUID tooa ad esempio, in modo che sia più difficile toobe individuati da altri utenti.
  
    Per altre informazioni sul debug, vedere questo [collegamento](https://tomasz.janczuk.org/2011/11/debug-nodejs-applications-on-windows.html) .

## <a name="scenarios-and-recommendationstroubleshooting"></a>Scenari e indicazioni/risoluzione dei problemi
### <a name="my-node-application-is-making-too-many-outbound-calls"></a>L'applicazione Node effettua un numero eccessivo di chiamate in uscita.
Molte applicazioni opportuno che le connessioni in uscita toomake come parte del relativo funzionamento regolare. Ad esempio, quando arriva una richiesta, l'app nodo sarebbe desidera toocontact altrove un'API REST e ottenere una richiesta di informazioni tooprocess hello. Quando si effettuano chiamate http o https, è opportuno toouse un agente di keep alive. Ad esempio, è possibile utilizzare il modulo di agentkeepalive hello come l'agente di keep-alive quando si eseguono queste chiamate in uscita. Ciò assicura che i socket hello vengono riutilizzati sul webapp azure VM e riduzione di overhead hello di creazione di nuovi socket per ogni richiesta in uscita. Inoltre, in tal modo che si sta utilizzando un minor numero di socket toomake che molte richieste in uscita e pertanto non superare maxSockets hello allocati per ogni macchina virtuale. Indicazione su Azure WebApp sarebbe tooset hello agentKeepAlive maxSockets valore totale tooa di 160 socket per ogni macchina virtuale. Ciò significa che se si dispone di 4 node.exe in esecuzione su hello VM, desiderata tooset hello agentKeepAlive maxSockets too40 per node.exe ovvero 160 totale per ogni macchina virtuale.

Configurazione di esempio per [agentKeepALive](https://www.npmjs.com/package/agentkeepalive):

```
var keepaliveAgent = new Agent({    
    maxSockets: 40,    
    maxFreeSockets: 10,    
    timeout: 60000,    
    keepAliveTimeout: 300000    
});
```

Questo esempio presuppone che siano presenti quattro file node.exe in esecuzione nella VM. Se si dispone di un numero diverso di node.exe in esecuzione su hello VM, sarà necessario toomodify hello maxSockets impostare di conseguenza.

### <a name="my-node-application-is-consuming-too-much-cpu"></a>L'applicazione Node utilizza una quantità eccessiva di CPU.
È probabile che si riceva una raccomandazione relativa all'utilizzo elevato di CPU da App Web di Azure nel portale. È anche possibile toowatch monitoraggi il programma di installazione per determinati [metriche](web-sites-monitor.md). Durante il controllo dell'utilizzo della CPU hello nel hello [Dashboard portale Azure](../application-insights/app-insights-web-monitor-performance.md), verificare i valori massimo hello per CPU, per perdere neanche i valori di picco hello.
Nei casi in cui si ritiene che l'applicazione utilizza una quantità eccessiva della CPU e si non può spiegare il motivo, è necessario tooprofile l'applicazione del nodo.

### 
#### <a name="profiling-your-node-application-on-azure-webapps-with-v8-profiler"></a>Profilatura dell'applicazione Node in App Web di Azure con V8-Profiler
Ad esempio, consente ad esempio si dispone di un'app di hello world che si desidera tooprofile come illustrato di seguito:

```
var http = require('http');    
function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    WriteConsoleLog();    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Passare tooyour scm sito https://yoursite.scm.azurewebsites.net/DebugConsole

Verrà visualizzato un prompt dei comandi, come illustrato di seguito. Passare al sito/directory wwwroot.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_install_v8.png)

Eseguire il comando hello "npm install v8 profiler"

Nella directory node\_modules dovrebbe essere eseguita l'installazione di v8-profiler e di tutte le rispettive dipendenze.
A questo punto, modificare il tooprofile server.js l'applicazione.

```
var http = require('http');    
var profiler = require('v8-profiler');    
var fs = require('fs');

function WriteConsoleLog() {    
    for(var i=0;i<99999;++i) {    
        console.log('hello world');    
    }    
}

function HandleRequest() {    
    profiler.startProfiling('HandleRequest');    
    WriteConsoleLog();    
    fs.writeFileSync('profile.cpuprofile', JSON.stringify(profiler.stopProfiling('HandleRequest')));    
}

http.createServer(function (req, res) {    
    res.writeHead(200, {'Content-Type': 'text/html'});    
    HandleRequest();    
    res.end('Hello world!');    
}).listen(process.env.PORT);
```

Hello sopra le modifiche verrà funzione WriteConsoleLog hello del profilo e quindi scrivere hello profilo output too'profile.cpuprofile' file in wwwroot del sito. Invio di un'applicazione tooyour richiesta. Verrà visualizzato un file 'profile.cpuprofile' creato in wwwroot del sito.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/scm_profile.cpuprofile.png)

Scaricare questo file e sarà necessario tooopen questo file con strumenti F12 Chrome. Premere F12 in chrome, quindi fare clic su hello "Nella scheda Profili". Fare clic sul pulsante "Load" (Carica). Selezionare il file profile.cpuprofile appena scaricato. Fare clic sul profilo hello che appena caricato.

![](./media/app-service-web-nodejs-best-practices-and-troubleshoot-guide/chrome_tools_view.png)

Si noterà che 95% di tempo hello utilizzato dalla funzione WriteConsoleLog come illustrato di seguito. Ciò illustra anche i numeri di riga esatta hello e i file di origine che causano il problema di hello.

### <a name="my-node-application-is-consuming-too-much-memory"></a>L'applicazione Node utilizza una quantità eccessiva di memoria.
È probabile che si riceva da App Web di Azure nel portale una raccomandazione relativa all'utilizzo elevato di memoria. È anche possibile toowatch monitoraggi il programma di installazione per determinati [metriche](web-sites-monitor.md). Durante il controllo dell'utilizzo della memoria hello in hello [Dashboard portale Azure](../application-insights/app-insights-web-monitor-performance.md), verificare i valori massimo hello per la memoria per perdere neanche i valori di picco hello.

#### <a name="leak-detection-and-heap-diffing-for-nodejs"></a>Rilevamento della perdita di risorse e delle differenze tra heap per node.js
È possibile utilizzare [nodo memwatch](https://github.com/lloyd/node-memwatch) perdite toohelp identificare la memoria.
È possibile installare memwatch come v8 profiler e modificare che il codice toocapture e diff heap tooidentify hello le perdite di memoria nell'applicazione.

### <a name="my-nodeexes-are-getting-killed-randomly"></a>I file node.exe vengono terminati in modo casuale
Questo problema può avere alcune cause:

1. L'applicazione sta generando eccezioni non rilevate – d: controllo Please\\home\\LogFiles\\applicazione\\file di registrazione-Errors. txt per i dettagli di hello eccezione hello generata. Questo file contiene l'analisi dello stack hello per risolverli in base a questa applicazione.
2. L'applicazione utilizza una quantità troppo elevata di memoria e ciò impedisce l'avvio di altri processi. Se memoria della macchina virtuale hello totale è % too100 Chiudi, potrebbe essere terminato il node.exe hello processo manager toolet altri processi di ottengono un toodo possibilità alcune operazioni. toofix, assicurarsi che l'applicazione non dispone di memoria o se l'applicazione deve toouse una grande quantità di memoria, per applicare la scalabilità verticale tooa VM più grande con una grande quantità di RAM.

### <a name="my-node-application-does-not-start"></a>Non è possibile avviare l'applicazione Node
Se l'applicazione restituisce errori di tipo 500 all'avvio, è possibile che si siano verificati i problemi seguenti:

1. Node.exe non è presente nella posizione corretta hello. Verificare l'impostazione nodeProcessCommandLine.
2. File di script principale non è presente nella posizione corretta hello. Verificare i file Web. config e verificare nome hello hello principale del file di script nella sezione gestori hello corrisponde al file script principale di hello.
3. Configurazione Web. config non è corretta – controllare le impostazioni di hello nomi/valori.
4. Avvio a freddo: l'applicazione richiede toostartup troppo lungo. Se l'avvio dell'applicazione richiede più di (maxNamedPipeConnectionRetry \* namedPipeConnectionRetryDelay) / 1000 secondi, iisnode restituirà un errore di tipo 500. Aumentare i valori hello di toomatch queste impostazioni applicazione avviare ora tooprevent iisnode da scadere e restituire l'errore hello 500.

### <a name="my-node-application-crashed"></a>Si è verificato l'arresto anomalo dell'applicazione Node
L'applicazione sta generando eccezioni non rilevate – d: controllo Please\\home\\LogFiles\\applicazione\\file di registrazione-Errors. txt per i dettagli di hello eccezione hello generata. Questo file contiene l'analisi dello stack hello per risolverli in base a questa applicazione.

### <a name="my-node-application-takes-too-much-time-toostartup-cold-start"></a>Applicazione nodo accetta toostartup troppo tempo (avvio freddo)
Motivo più comune è che un'applicazione hello dispone di molti file nel nodo hello\_moduli e tooload tentativi di applicazione hello la maggior parte di questi file durante l'avvio. Per impostazione predefinita, poiché si trovano i file nella condivisione di rete hello in WebApp di Azure, il caricamento di molti file può richiedere del tempo.
Alcune soluzioni toomake più velocemente in questo sono:

1. Accertarsi di avere una struttura flat dipendenza e senza dipendenze duplicate utilizzando npm3 tooinstall dei moduli.
2. Provare a carico toolazy il nodo\_moduli e caricare tutti i moduli di hello all'avvio. Ciò significa che toorequire('module') chiamata hello deve essere eseguita quando è effettivamente necessario all'interno di funzione hello si tenta di modulo hello toouse.
3. App Web di Azure offre una funzionalità definita cache locale. Questa funzione Copia il contenuto da hello rete condivisione toohello disco locale nel hello macchina virtuale. Poiché i file hello sono locali, hello tempo di caricamento della nodo\_moduli è molto più veloce. -Questo [documentazione](../app-service/app-service-local-cache.md) spiega come toouse Cache locale in ulteriori dettagli.

## <a name="iisnode-http-status-and-substatus"></a>Stato e stato secondario HTTP di IISNODE
Questo [file di origine](https://github.com/Azure/iisnode/blob/master/src/iisnode/cnodeconstants.h) elenchi tutti iisnode di combinazione di stato possibili dello stato secondario hello può restituire in caso di errore.

Abilita FREB per il codice di errore applicazione toosee hello win32 (. Assicurarsi di abilitare FREB solo nei siti non di produzione per motivi di prestazioni).

| Stato HTTP | Stato secondario HTTP | Possibile motivo |
| --- | --- | --- |
| 500 |1000 |Si è verificato un problema di invio hello richiesta tooIISNODE: controllare se node.exe è stato avviato. È possibile che si sia verificato l'arresto anomalo di Node.exe all'avvio. Cercare eventuali errori nella configurazione del file web.config. |
| 500 |1001 |-0x2 - App Win32Error toohello URL non risponde. Le regole o se l'applicazione express ha definita la route corretto hello riscrittura dell'URL di controllo. -Win32Error 0x6d – named pipe è occupato: Node.exe non accetta richieste pipe hello è occupata. Controllare se l'utilizzo della CPU è elevato. - Altri errori: controllare se si è verificato l'arresto anomalo di node.exe. |
| 500 |1002 |Si è verificato l'arresto anomalo di Node.exe: verificare se nel file d:\\home\\LogFiles\\logging-errors.txt è disponibile l'analisi dello stack. |
| 500 |1003 |Problema di configurazione di pipe non dovrebbe mai visibile, ma in caso contrario, hello denominato configurazione pipe non è corretto. |
| 500 |1004-1018 |Si è verificato un errore durante l'invio di risposta di hello di richiesta o elaborazione hello in/da node.exe. Controllare se si è verificato l'arresto anomalo di node.exe. Verificare se nel file d:\\home\\LogFiles\\logging-errors.txt è disponibile l'analisi dello stack. |
| 503 |1000 |Non è sufficiente memoria tooallocate più connessioni named pipe. Verificare i motivi per cui l'app utilizza una quantità così elevata di memoria. Controllare il valore dell'impostazione maxConcurrentRequestsPerProcess. Se non infinito e si dispone di un numero elevato di richieste, aumentare questo valore tooprevent questo errore. |
| 503 |1001 |Richiesta non è stato inviato toonode.exe perché il riciclo dell'applicazione hello. Dopo l'applicazione hello è stato riciclato, le richieste di effettiva necessità di servire normalmente. |
| 503 |1002 |Codice di errore win32 di controllo per il motivo effettivo: richiesta non è stato inviato tooa node.exe. |
| 503 |1003 |La named pipe è troppo occupata. Controllare se il nodo utilizza una quantità elevata di CPU. |

NODE.exe include un'impostazione definita NODE\_PENDING\_PIPE\_INSTANCES. Per impostazione predefinita, all'esterno di App Web di Azure questo valore è 4. Ciò significa che node.exe può accettare solo 4 richieste contemporaneamente nella hello denominato pipe. In Azure WebApp, questo valore è impostato too5000 e questo valore deve essere adeguato per la maggior parte delle applicazioni in esecuzione in azure WebApp nodo. Non dovrebbe essere visualizzato 503.1003 in azure WebApp poiché è un valore elevato per hello nodo\_PENDING\_PIPE\_istanze.  |

## <a name="more-resources"></a>Altre risorse
Seguire questi toolearn collegamenti ulteriori informazioni sulle applicazioni node.js in Azure App Service.

* [Introduzione alle app Web Node.js nel servizio app di Azure](app-service-web-get-started-nodejs.md)
* [Come toodebug un Node.js web app in Azure App Service](web-sites-nodejs-debug.md)
* [Utilizzo di moduli Node.js con le applicazioni Azure](../nodejs-use-node-modules-azure-apps.md)
* [Blog sulle app Web del servizio app di Azure: Node.js](https://blogs.msdn.microsoft.com/silverlining/2012/06/14/windows-azure-websites-node-js/)
* [Centro per sviluppatori di Node. js](../nodejs-use-node-modules-azure-apps.md)
* [Esplorazione hello Super segreto Kudu Debug Console](https://azure.microsoft.com/documentation/videos/super-secret-kudu-debug-console-for-azure-web-sites/)

