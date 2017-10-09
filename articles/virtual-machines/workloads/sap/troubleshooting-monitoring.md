---
title: aaaTroubleshooting e monitoraggio di SAP HANA in Azure (istanze di grandi dimensioni) | Documenti Microsoft
description: Risolvere i problemi e monitorare SAP HANA in Azure (istanze di grandi dimensioni).
services: virtual-machines-linux
documentationcenter: 
author: RicksterCDN
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1f1cd35820e227fd99af495431cd4b826aa53600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-and-monitor-sap-hana-large-instances-on-azure"></a>Come tootroubleshoot e monitoraggio SAP HANA (istanze di grandi dimensioni) in Azure


## <a name="monitoring-in-sap-hana-on-azure-large-instances"></a>Monitoraggio in SAP HANA in Azure (istanze di grandi dimensioni)

SAP HANA in Azure (istanze di grandi dimensioni) non è diverso da qualsiasi altra distribuzione IaaS, è necessario toomonitor cosa hello del sistema operativo e un'applicazione hello procedere e come questi utilizzare hello seguenti risorse:

- CPU
- Memoria
- Larghezza di banda della rete
- Spazio su disco

Come con macchine virtuali di Azure è necessario toofigure se le classi di risorse hello sopra sono sufficienti o se queste ottenere esaurite. Ecco ulteriori dettagli su ciascuna delle classi diverse hello:

**Utilizzo delle risorse della CPU:** rapporto hello definite SAP per determinati HANA carico di lavoro è imposto toomake che deve essere sufficiente toowork disponibili risorse di CPU tramite hello i dati archiviati in memoria. Tuttavia, potrebbe essere casi in cui HANA richiede una maggiore quantità di CPU, l'esecuzione di query a causa di problemi simili o toomissing indici. Ciò significa che è necessario monitorare il consumo di risorse della CPU di unità di grandi dimensioni istanza HANA hello, nonché le risorse della CPU utilizzate da servizi HANA specifici hello.

**Utilizzo della memoria:** è importante toomonitor all'interno di HANA, nonché di fuori di HANA unità hello. All'interno di HANA, monitorare come dati hello sta consumando memoria in toostay ordine all'interno di hello richiesto il ridimensionamento delle linee guida di SAP HANA. È anche opportuno toomonitor utilizzo della memoria su hello istanza grande livello toomake che il software aggiuntivo HANA-non installato non usano troppa memoria e pertanto si contendono HANA per la memoria.

**Larghezza di banda di rete:** gateway di rete virtuale di Azure hello è limitata di dati trasferiti in rete virtuale di Azure hello la larghezza di banda, è utile ricevuti da tutti i dati di hello toomonitor hello macchine virtuali di Azure all'interno di un toofigure di rete virtuale come chiudere sono toohello limiti di hello Azure lo SKU selezionato del gateway. Nell'unità di istanza di grandi dimensioni HANA hello, rende senso toomonitor in ingresso e in uscita del traffico di rete nonché e tenere traccia di tookeep dei volumi hello che vengono gestiti nel tempo.

**Spazio su disco**: l'utilizzo dello spazio su disco in genere aumenta nel tempo. Ciò è dovuto a diversi motivi, in particolare l'aumento di volume dei dati, l'esecuzione di backup del log delle transazioni, l'archiviazione dei file di traccia e l'esecuzione di snapshot di archiviazione. Pertanto, è importante toomonitor spazio su disco e gestire lo spazio su disco hello associato hello istanza grande HANA unità.

## <a name="monitoring-and-troubleshooting-from-hana-side"></a>Monitoraggio e risoluzione dei problemi dal lato HANA

In ordine tooeffectively analizzare i problemi correlati tooSAP HANA in Azure (istanze di grandi dimensioni), è utile toonarrow verso il basso della causa radice hello del problema. SAP ha pubblicato una grande quantità di documentazione toohelp è.

Applicabile FAQ tooSAP correlati HANA prestazioni sono reperibile in hello note su SAP seguenti:

- [Nota SAP #2222200 – FAQ: rete e SAP HANA](https://launchpad.support.sap.com/#/notes/2222200)
- [Nota SAP #2100040 – FAQ: CPU e SAP HANA](https://launchpad.support.sap.com/#/notes/0002100040)
- [Nota SAP #199997 – FAQ: memoria e SAP HANA](https://launchpad.support.sap.com/#/notes/2177064)
- [Nota SAP #200000 – FAQ: ottimizzazione delle prestazioni di SAP HANA](https://launchpad.support.sap.com/#/notes/2000000)
- [Nota SAP #199930 – FAQ: analisi dell'I/O di SAP HANA](https://launchpad.support.sap.com/#/notes/1999930)
- [Nota SAP #2177064 – FAQ: riavvio del servizio e interruzioni inaspettate di SAP HANA](https://launchpad.support.sap.com/#/notes/2177064)

**Avvisi SAP HANA**

Come primo passaggio, verificare hello corrente SAP HANA avviso log. In SAP HANA Studio andare troppo**Console di amministrazione: gli avvisi: Mostra: tutti gli avvisi**. Questa scheda visualizzerà tutti gli avvisi di SAP HANA per valori specifici (memoria fisica disponibile, l'utilizzo della CPU e così via) che rientrano nella hello impostare minimo e massimo delle soglie. Per impostazione predefinita i controlli vengono aggiornati automaticamente ogni 15 minuti.

![In SAP HANA Studio andare tooAdministration Console: gli avvisi: Mostra: tutti gli avvisi](./media/troubleshooting-monitoring/image1-show-alerts.png)

**CPU**

Per un avviso generato a causa di impostazione della soglia tooimproper, valore predefinito di tooreset toohello o un valore di soglia più ragionevole è una soluzione.

![Valore predefinito di reimpostazione toohello o un valore di soglia accettabile](./media/troubleshooting-monitoring/image2-cpu-utilization.png)

Hello seguendo gli avvisi può indicare problemi di risorse della CPU:

- Utilizzo della CPU dell'host (avviso 5)
- Funzionamento del punto di salvataggio più recente (avviso 28)
- Durata del punto di salvataggio (avviso 54)

È possibile notare elevato della CPU sul database SAP HANA da uno dei seguenti hello:

- L'avviso 5 (utilizzo della CPU dell'host) viene generato per l'utilizzo della CPU corrente o precedente
- Hello visualizzato l'utilizzo della CPU nella schermata introduttiva hello

![Visualizzato l'utilizzo della CPU nella schermata introduttiva hello](./media/troubleshooting-monitoring/image3-cpu-usage.png)

grafico del carico Hello potrebbe mostrare elevato della CPU, o consumo elevato nelle ultime hello:

![grafico del carico Hello potrebbe mostrare elevato della CPU, o consumo elevato nelle ultime hello](./media/troubleshooting-monitoring/image4-load-graph.png)

Un avviso generato a causa di utilizzo della CPU toohigh potrebbe essere causato da diversi motivi, ad esempio, a titolo esemplificativo: esecuzione di determinate transazioni, il caricamento dei dati, blocco di processi a esecuzione prolungata istruzioni SQL e le prestazioni delle query non valida (ad esempio, con BW su HANA cubi).

Fare riferimento toohello [risoluzione dei problemi di SAP HANA: provoca correlati della CPU e le soluzioni](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4f/bc915462db406aa2fe92b708b95189/content.htm?frameset=/en/db/6ca50424714af8b370960c04ce667b/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=46&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.

**Sistema operativo**

Uno dei più importante hello verifica la presenza di SAP HANA in Linux è toomake assicurarsi che le pagine di grandi dimensioni trasparente sono disabilitate, vedere [SAP nota #2131662 – trasparente enorme pagine (THP) nei server di SAP HANA](https://launchpad.support.sap.com/#/notes/2131662).

- È possibile controllare se le pagine di grandi dimensioni trasparente sono abilitate tramite hello Linux comando seguente: **cat /sys/kernel/mm/transparent\_hugepage abilitato**
- Se _sempre_ è racchiuso tra parentesi quadre, come indicato di seguito, significa che sono abilitate le pagine di grandi dimensioni trasparente hello: [sempre] madvise mai; se _mai_ è racchiuso tra parentesi quadre, come indicato di seguito, significa che hello trasparente Pagine di grandi dimensioni sono disabilitate: sempre madvise [mai]

comando Linux seguente Hello deve restituire nothing: **rpm - qa | grep ulimit.** Nel caso sembrasse che _ulimit_ è installato, disinstallarlo immediatamente.

**Memoria**

È possibile osservare tale quantità hello della memoria allocata dall'hello SAP HANA database è supera al previsto. Hello seguendo gli avvisi indica problemi con utilizzo elevato della memoria:

- Utilizzo di memoria fisica dell'host (avviso 1)
- Utilizzo di memoria del server dei nomi (avviso 12)
- Utilizzo di memoria totale delle tabelle columnstore (avviso 40)
- Utilizzo di memoria dei servizi (avviso 43)
- Utilizzo di memoria totale della risorsa di archiviazione principale delle tabelle columnstore (avviso 45)
- File di dump di runtime (avviso 46)

Fare riferimento toohello [risoluzione dei problemi di SAP HANA: problemi di memoria](http://help.sap.com/saphelp_hanaplatform/helpdata/en/db/6ca50424714af8b370960c04ce667b/content.htm?frameset=/en/59/5eaa513dde43758b51378ab3315ebb/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=26&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.

**Rete**

Fare riferimento troppo[SAP nota #2081065: risoluzione dei problemi di rete di SAP HANA](https://launchpad.support.sap.com/#/notes/2081065) ed eseguire i passaggi descritti in questa nota SAP risoluzione dei problemi di rete di hello.

1. Analisi del tempo di round trip tra client e server.
  R. Esecuzione dello script SQL hello [ _HANA\_rete\_client_](https://launchpad.support.sap.com/#/notes/1969700)_._
  
2. Analizzare le comunicazioni internodo.
  R. Eseguire lo script SQL [_HANA\_Network\_Services_](https://launchpad.support.sap.com/#/notes/1969700)_._

3. Eseguire il comando Linux **ifconfig** (output di hello Mostra se si verificano perdite di pacchetti).
4. Eseguire il comando di Linux **tcpdump**.

Inoltre, utilizzare open source di hello [IPERF](https://iperf.fr/) strumento (o simile) toomeasure prestazioni di rete reali dell'applicazione.

Fare riferimento toohello [risoluzione dei problemi di SAP HANA: prestazioni di rete e problemi di connettività](http://help.sap.com/saphelp_hanaplatform/helpdata/en/a3/ccdff1aedc4720acb24ed8826938b6/content.htm?frameset=/en/dc/6ff98fa36541e997e4c719a632cbd8/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=142&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.

**Archiviazione**

Dal punto di vista dell'utente finale, un'applicazione (o l'intero sistema hello) esegue risultano ridotte, non risponde o può anche sembrare toohang se esistono problemi di prestazioni dei / o. In hello **volumi** scheda in SAP HANA Studio, è possibile visualizzare hello collegato volumi e i volumi sono utilizzati da ogni servizio.

![Nella scheda di volumi hello in SAP HANA Studio, è possibile visualizzare hello collegato volumi e i volumi sono utilizzati da ogni servizio](./media/troubleshooting-monitoring/image5-volumes-tab-a.png)

I volumi collegati nella parte inferiore di hello della schermata di hello di che è possibile visualizzare i dettagli hello volumi, ad esempio file e le statistiche dei / o.

![I volumi collegati nella parte inferiore di hello della schermata di hello di che è possibile visualizzare i dettagli hello volumi, ad esempio file e le statistiche dei / o](./media/troubleshooting-monitoring/image6-volumes-tab-b.png)

Fare riferimento toohello [risoluzione dei problemi di SAP HANA: i/o relative cause e soluzioni](http://help.sap.com/saphelp_hanaplatform/helpdata/en/dc/6ff98fa36541e997e4c719a632cbd8/content.htm?frameset=/en/47/4cb08a715c42fe9f7cc5efdc599959/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=55&amp;show_children=false) e [risoluzione dei problemi di SAP HANA: disco relative cause e soluzioni](http://help.sap.com/saphelp_hanaplatform/helpdata/en/47/4cb08a715c42fe9f7cc5efdc599959/content.htm?frameset=/en/44/3e1db4f73d42da859008df4f69e37a/frameset.htm&amp;current_toc=/en/85/d132c3f05e40a2b20c25aa5fd6331b/plain.htm&amp;node_id=53&amp;show_children=false) sito per i passaggi di risoluzione dei problemi dettagliata.

**Strumenti di diagnostica**

Eseguire un controllo di integrità di SAP HANA tramite HANA\_Configuration\_Minichecks. Questo strumento restituisce problemi tecnici critici che dovrebbero essere già stati notificati mediante avvisi in SAP HANA Studio.

Fare riferimento troppo[SAP nota #1969700 – insieme di istruzioni SQL per SAP HANA](https://launchpad.support.sap.com/#/notes/1969700) e scaricare nota di hello SQL Statements.zip file toothat associata. Archiviare il file con estensione zip sul disco rigido locale hello.

In SAP HANA Studio scegliere hello **informazioni di sistema** scheda, fare doppio clic nella hello **nome** colonna e selezionare **le istruzioni SQL Import**.

![In SAP HANA Studio, nella scheda informazioni di sistema hello, fare clic nella colonna nome hello e selezionare le istruzioni Import in SQL](./media/troubleshooting-monitoring/image7-import-statements-a.png)

Selezionare hello SQL Statements.zip file archiviato in locale e una cartella con istruzioni SQL corrispondenti hello verrà importata. A questo punto, hello che molti diversi controlli di diagnostica possono essere eseguiti con queste istruzioni SQL.

Ad esempio, requisiti di larghezza di banda replica DFS di SAP HANA tootest, fare doppio clic su hello **della larghezza di banda** istruzione in **replica: la larghezza di banda** e selezionare **aprire** Nella Console SQL.

istruzione SQL completa Hello apre toobe consentendo di parametri di input (sezione di modifica) modificato e quindi eseguita.

![istruzione SQL completa Hello apre toobe consentendo di parametri di input (sezione di modifica) modificato e quindi eseguita](./media/troubleshooting-monitoring/image8-import-statements-b.png)

Un altro esempio è il pulsante destro su istruzioni hello in **replica: Panoramica**. Selezionare **Execute** dal menu di scelta rapida hello:

![Un altro esempio è il pulsante destro su istruzioni hello in replica: Panoramica. Selezionare Esegui dal menu di scelta rapida hello](./media/troubleshooting-monitoring/image9-import-statements-c.png)

Vengono visualizzate informazioni utili per la risoluzione dei problemi:

![Vengono visualizzate informazioni utili per la risoluzione dei problemi](./media/troubleshooting-monitoring/image10-import-statements-d.png)

Hello stesso per HANA\_configurazione\_Minichecks e cercare eventuali _X_ segni di hello _C_ colonna (Critical).

Output di esempio:

**HANA\_Configuration\_MiniChecks\_Rev102.01+1** per controlli SAP HANA generali.

![HANA\_Configuration\_MiniChecks\_Rev102.01+1 per controlli SAP HANA generali](./media/troubleshooting-monitoring/image11-configuration-minichecks.png)

**HANA\_Services\_Overview** per una panoramica di quanto stanno eseguendo attualmente i servizi SAP HANA.

![HANA\_Services\_Overview per una panoramica di quanto stanno eseguendo attualmente i servizi SAP HANA](./media/troubleshooting-monitoring/image12-services-overview.png)

**HANA\_Services\_Statistics** per informazioni sul servizio SAP HANA (CPU, memoria, ecc.).

![HANA\_Services\_Statistics per informazioni sul servizio SAP HANA ](./media/troubleshooting-monitoring/image13-services-statistics.png)

**HANA\_configurazione\_Panoramica\_Rev110 +** per informazioni generali sull'istanza di SAP HANA hello.

![HANA\_configurazione\_Panoramica\_Rev110 + per informazioni generali sull'istanza di SAP HANA hello](./media/troubleshooting-monitoring/image14-configuration-overview.png)

**HANA\_configurazione\_parametri\_Rev70 +** toocheck i parametri di SAP HANA.

![HANA\_configurazione\_parametri\_i parametri di SAP HANA toocheck Rev70 +](./media/troubleshooting-monitoring/image15-configuration-parameters.png)

