---
title: "funzionalità del sistema aaaOperating nel servizio App di Azure"
description: "Informazioni sulle App tooweb disponibili funzionalità di hello del sistema operativo, back-end delle app per dispositivi mobili e App per le API nel servizio App di Azure"
services: app-service
documentationcenter: 
author: cephalin
manager: erikre
editor: mollybos
ms.assetid: 39d5514f-0139-453a-b52e-4a1c06d8d914
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/01/2016
ms.author: cephalin
ms.openlocfilehash: 695188c48102b10ece326fba8d50a5f55b03b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="operating-system-functionality-on-azure-app-service"></a>Funzionalità del sistema operativo in Servizio app di Azure
Questo articolo descrive hello linea di base del sistema operativo funzionalità comuni che è disponibile tooall App in esecuzione su [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Queste funzionalità includono l'accesso a file, rete e registro, nonché log ed eventi di diagnostica. 

<a id="tiers"></a>

## <a name="app-service-plan-tiers"></a>Livelli del piano del servizio app di Azure
Il servizio app esegue app di clienti in un ambiente host multi-tenant. Le app distribuite in hello **libero** e **Shared** livelli eseguono in processi di lavoro macchine virtuali condivise, mentre le app distribuite in hello **Standard** e  **Premium** livelli di eseguire in macchine virtuali dedicata per l'App hello associata a un singolo cliente.

Poiché il servizio App supporta un'esperienza di scalabilità tra livelli diversi, configurazione della sicurezza hello applicata per hello rimane impostato su applicazioni di servizio App stessa. In questo modo si garantisce che le app non improvvisamente si comportano in modo diverso, non riusciti in modo imprevisto, quando il piano di servizio App passa da un livello tooanother.

<a id="developmentframeworks"></a>

## <a name="development-frameworks"></a>Framework di sviluppo
Servizio App prezzi quantità di hello controllo livelli delle risorse di calcolo (CPU, spazio su disco, memoria e in uscita di rete) tooapps disponibili. Tuttavia, varietà hello del framework funzionalità disponibile tooapps rimane hello che uguali indipendentemente dal valore hello livelli di scalabilità.

Il servizio app supporta diversi framework di sviluppo, tra cui ASP.NET, ASP classico, Node.js, PHP e Python, tutti eseguibili come estensioni in IIS. In ordine toosimplify e normalizzare configurazione della sicurezza, le applicazioni di servizio App in genere eseguono hello diversi framework di sviluppo con le impostazioni predefinite. Un approccio tooconfiguring App potrebbe essere avvenuta toocustomize della superficie di attacco di hello API e le funzionalità per ogni struttura di sviluppo singoli. Il servizio app invece usa un approccio più generico, abilitando una linea di base comune delle funzionalità del sistema operativo indipendentemente dal framework di sviluppo di un'app.

Hello nelle sezioni seguenti riepilogano tipi generali di hello di applicazioni di servizio disponibili tooApp funzionalità del sistema operativo.

<a id="FileAccess"></a>

## <a name="file-access"></a>Accesso ai file
Nel servizio app sono presenti varie unità, tra cui unità locali e unità di rete.

<a id="LocalDrives"></a>

### <a name="local-drives"></a>Unità locali
In sostanza, servizio App è un servizio in esecuzione nell'infrastruttura di hello Azure PaaS (piattaforma distribuita come servizio). Come un risultato, hello le unità locali sono "collegate" macchina virtuale tooa hello stesso ruolo di lavoro disponibili tooany di tipi unità eseguono in Azure. Ad esempio un'unità del sistema operativo (Buongiorno unità D:\), un'unità di applicazione che contiene file cspkg pacchetto Azure utilizzati esclusivamente dal servizio App (e toocustomers inaccessibile) e un'unità "user" (Buongiorno unità C:\), la cui dimensione varia a seconda delle dimensioni di hello di hello macchina virtuale.

<a id="NetworkDrives"></a>

### <a name="network-drives-aka-unc-shares"></a>Unità di rete (note anche come condivisioni UNC)
Uno degli aspetti di univoco hello del servizio App che semplifica la manutenzione e la distribuzione di app è che tutto il contenuto utente viene archiviato in un set di condivisioni UNC. Questo modello viene eseguito il mapping molto ben toohello modello comune di archiviazione del contenuto utilizzati per gli ambienti che dispongono di più server con bilanciamento del carico di hosting web locale. 

Nel servizio app sono presenti numerose condivisioni UNC create in ogni data center. Percentuale del contenuto utente hello per tutti i clienti in ogni data center viene allocata tooeach condivisione UNC. Inoltre, tutti hello contenuto del file per una singola sottoscrizione del cliente viene sempre inserita nella condivisione UNC stesso hello. 

Si noti che, a causa di servizi cloud toohow di lavoro, hello macchina virtuale specifica responsabile per l'hosting di una condivisione UNC cambia nel tempo. Viene garantito che condivisioni UNC verranno montate da diverse macchine virtuali come si trovino su e giù durante hello normali operazioni cloud. Per questo motivo, le applicazioni non devono mai supposizioni hardcoded che le informazioni sul computer hello in un percorso file UNC rimane stabile nel tempo. Al contrario, dovrebbero usare hello pratico *simulato* percorso assoluto **D:\home\site** che fornisce il servizio App. Il percorso assoluto simulato fornisce un metodo di portatile e indipendente di app e utente per app di tooone di fare riferimento. Utilizzando **D:\home\site**, una possibile trasferire i file condivisi da tooapp app senza la necessità di un nuovo percorso assoluto tooconfigure di ciascun trasferimento.

<a id="TypesOfFileAccess"></a>

### <a name="types-of-file-access-granted-tooan-app"></a>Tipi di accesso ai file concesso tooan app
La sottoscrizione di ciascun cliente presenta una struttura di directory riservata su una condivisione UNC specifica all'interno di un data center. Un cliente può disporre di più applicazioni create all'interno di un data center specifico, pertanto tutte le directory hello appartengono sottoscrizione singolo cliente tooa vengono create in hello stessa condivisione UNC. condivisione Hello può includere una directory, ad esempio quelli relativi al contenuto, errore e i log di diagnostica e le versioni precedenti di app hello creata dal controllo del codice sorgente. Directory dell'app del cliente come previsto, sono disponibili per l'accesso in lettura e scrittura in fase di esecuzione dal codice dell'applicazione hello dell'app.

In hello unità locali sulla macchina virtuale toohello che esegue un'app, servizio App si riserva un blocco di spazio su unità C:\ per l'archiviazione locale temporanea specifico dell'applicazione hello. Sebbene un'applicazione ha accesso in lettura/scrittura tooits proprietari temporaneo archiviazione locale, che l'archiviazione non è realmente toobe previsto utilizzato direttamente dal codice dell'applicazione hello. Piuttosto, finalità hello è tooprovide archiviazione temporanea dei file per i framework dell'applicazione web e IIS. Servizio App limita inoltre quantità hello di archiviazione locale temporanea tooeach disponibili app tooprevent singole App utilizzino una quantità eccessiva di spazio di archiviazione di file locale.

Due esempi di utilizzo di archiviazione locale temporanea del servizio App sono directory hello per file ASP.NET temporanei e file compressi directory hello per IIS. sistema di compilazione ASP.NET Hello utilizza directory "Temporary ASP.NET Files" hello come un percorso della cache di compilazione temporanei. IIS Usa l'output di risposta toostore compressi directory hello "IIS compressi temporanei". Entrambi questi tipi di file sull'utilizzo (come altre) vengono mappate nuovamente nell'archiviazione locale di servizio App tooper app temporaneo. Il remapping garantisce una funzionalità conforme alle aspettative.

Ogni applicazione nel servizio App viene eseguito come un'identità di processo di lavoro di privilegi di basso livello univoco casuale denominato hello "identità pool di applicazioni", descritto più avanti in questo caso: [http://www.iis.net/learn/manage/configuring-security/application-pool-identities ](http://www.iis.net/learn/manage/configuring-security/application-pool-identities). Il codice dell'applicazione usa questa identità per unità del sistema operativo di base accesso in sola lettura toohello (Buongiorno unità D:\). Questo significa che il codice dell'applicazione può elencare strutture di directory comuni e file comuni in lettura nell'unità del sistema operativo. Anche se ciò potrebbe essere visualizzato toobe un livello leggermente generale di accesso, hello stesse directory e i file sono accessibili quando si esegue il provisioning di un ruolo di lavoro in un Azure servizio ospitato e leggere i contenuti dell'unità hello. 

<a name="multipleinstances"></a>

### <a name="file-access-across-multiple-instances"></a>Accesso ai file tra più istanze
home directory di Hello contiene il contenuto di un'app e il codice dell'applicazione è possibile scrivere tooit. Se un'applicazione eseguita su più istanze, home directory di hello è condiviso tra tutte le istanze in modo che tutte le istanze vedere hello stessa directory. In tal caso, ad esempio, se un'app Salva home directory di file caricati toohello, tali file sono immediatamente disponibili tooall istanze. 

<a id="NetworkAccess"></a>

## <a name="network-access"></a>Accesso alla rete
Il codice dell'applicazione può utilizzare TCP/IP e UDP basato su protocolli toomake in uscita rete connessioni tooInternet accessibile endpoint che espongono servizi esterni. Le app possono usare queste tooservices tooconnect protocolli stesso all'interno di Azure & #151, ad esempio stabilendo tooSQL connessioni HTTPS Database.

È inoltre disponibile una funzionalità limitate per la connessione delle App tooestablish un loopback locale, e dispone di un'app in attesa su tale socket di loopback locale. Questa funzionalità esiste tooenable principalmente le applicazioni in ascolto su socket di loopback locale come parte delle funzionalità. Si noti che ogni app rileva una connessione loopback "private". app "A" non può essere in ascolto socket di loopback locale tooa stabilita da app "B".

Sono supportate anche le named pipe come meccanismo di comunicazione interprocesso (IPC) tra processi diversi che eseguono collettivamente un'app. Ad esempio, il modulo di IIS FastCGI hello si basa su named pipe toocoordinate hello singoli processi che eseguono le pagine PHP.

<a id="Code"></a>

## <a name="code-execution-processes-and-memory"></a>Esecuzione del codice, processi e memoria
Come indicato in precedenza, le app vengono eseguite all'interno di processi di lavoro con privilegi limitati che usano un'identità del pool di applicazioni casuale. Il codice dell'applicazione dispone di spazio di memoria toohello di accesso associato al processo di lavoro hello, nonché tutti i processi figlio che possono essere generati da processi CGI o altre applicazioni. Tuttavia, un'applicazione non può accedere memoria hello o dati di anche se si trova in un'altra app hello stessa macchina virtuale.

Le app possono eseguire script o pagine scritte con framework di sviluppo Web supportati. Servizio App non di configurare le modalità di toomore limitato impostazioni framework web. Ad esempio, le applicazioni ASP.NET in esecuzione nel servizio App eseguire "attendibilità" come modalità di attendibilità anziché tooa più limitato. Framework Web, comprese le ASP classico e ASP.NET, è possibile chiamare componenti COM in-process, ma non è un timeout di componenti COM di processo, ad esempio ADO (ActiveX Data Objects), che sono registrati per impostazione predefinita nel sistema operativo di Windows hello.

Le app possono generare ed eseguire codice arbitrario. È consentita per un operazioni toodo app come generare una shell dei comandi o eseguire uno script di PowerShell. Tuttavia, anche se i processi e codice non autorizzato possono essere generati da un'app, i programmi eseguibili e gli script sono comunque limitate toohello privilegi concessi toohello padre del pool di applicazioni. Ad esempio, un'applicazione può generare un file eseguibile che effettua una chiamata HTTP in uscita, ma tale stesso file eseguibile non è possibile tentare l'indirizzo IP di hello toounbind di una macchina virtuale dalla relativa interfaccia di rete. Effettuare una chiamata di rete in uscita è consentito codice con privilegi toolow, ma il tentativo di tooreconfigure le impostazioni di rete in una macchina virtuale richiede privilegi amministrativi.

<a id="Diagnostics"></a>

## <a name="diagnostics-logs-and-events"></a>Log ed eventi di diagnostica
Informazioni del log sono un altro set di dati che alcune applicazioni tentano tooaccess. tipi di Hello di toocode disponibili informazioni di log in esecuzione nel servizio App include diagnostica e registrare le informazioni generate da un'app che è anche app toohello facilmente accessibili. 

Ad esempio log HTTP W3C generati da un'app active sono disponibili in una directory di log nella rete hello percorso di condivisione creato per l'applicazione hello o disponibili nell'archiviazione blob, se un cliente ha configurato la registrazione W3C toostorage. quest'ultima opzione Hello consente grandi quantità di log toobe raccolte senza il rischio di hello di superamento dei limiti di archiviazione di file hello associati a una condivisione di rete.

Infine proposta, diagnostica in tempo reale informazioni da applicazioni .NET possono essere registrate anche utilizzando l'infrastruttura di diagnostica e traccia di .NET hello, con opzioni toowrite hello condivisione di rete dell'applicazione di traccia informazioni tooeither hello o, in alternativa, nell'archiviazione blob tooa percorso.

Le aree di diagnostica registrazione e analisi che non è disponibili tooapps sono eventi ETW di Windows e i registri eventi di Windows comuni (ad esempio, sistema, sicurezza registri eventi applicazioni e). Poiché le informazioni di traccia ETW potrebbero essere visibili gli eventi di tooETW accesso in lettura e scrittura a livello di computer (con diritto di hello ACL), vengono bloccati. Gli sviluppatori potrebbero notare API chiama tooread e scrittura eventi ETW e i registri eventi di Windows comuni vengono visualizzati toowork, ma ciò accade perché il servizio App è "falsificare" hello chiamate in modo che sembrino toosucceed. In realtà, il codice dell'applicazione hello non dispone di accesso toothis evento dati.

<a id="RegistryAccess"></a>

## <a name="registry-access"></a>Accesso al Registro di sistema
Le app hanno accesso in sola lettura toomuch (anche se non tutti) del Registro di sistema di hello della macchina virtuale hello vengono eseguiti in. In pratica, ciò significa chiavi del Registro di sistema che consentono il gruppo Users locale di accesso in sola lettura toohello sono accessibili da parte delle app. Un'area del Registro di sistema hello che non è attualmente supportato per la lettura o accesso in scrittura è hello HKEY\_corrente\_hive dell'utente.

Registro di sistema di accesso in scrittura toohello viene bloccato, incluse le chiavi del Registro di sistema per utente di accesso tooany. Dal punto di vista dell'applicazione hello, Registro di sistema di accesso in scrittura toohello non debba mai essere ritenuto hello ambiente Azure poiché le App (possano) vengono migrate tra diverse macchine virtuali. Hello solo scrivibile nell'archivio permanente che può essere dipende da un'app è una struttura di directory del contenuto per app hello archiviato in condivisioni UNC di servizio App hello. 

## <a name="more-information"></a>Altre informazioni

[Sandbox di App Web Azure](https://github.com/projectkudu/kudu/wiki/Azure-Web-App-sandbox) -hello la maggior parte delle informazioni aggiornate sull'ambiente di esecuzione hello di servizio App. Questa pagina viene mantenuta direttamente dal team di sviluppo del servizio App hello.

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 


