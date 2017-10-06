---
title: Considerazioni sulla aaaPerformance per gestione traffico di Azure | Documenti Microsoft
description: Informazioni sulle prestazioni per gestione traffico e come tootest delle prestazioni del sito Web quando si Usa gestione traffico
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 3ba5dfa1-2922-43f1-9a23-d06969c4a516
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: fd4e6cb221a2ceee63ec57237ee90fd714e91db8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="performance-considerations-for-traffic-manager"></a>Considerazioni sulle prestazioni per Gestione traffico

Questa pagina illustrati alcune considerazioni sulle prestazioni di Gestione traffico. Prendere in considerazione hello seguente scenario:

Si dispone di istanze del sito Web in hello WestUS e aree asiatico. Una delle istanze di hello non è possibile eseguire il controllo di integrità hello per il probe di gestione traffico hello. Il traffico delle applicazioni è area integro toohello diretto. È previsto il failover, ma le prestazioni possono essere un problema in base a latenza hello di hello traffico ora tooa distante area.

## <a name="performance-considerations-for-traffic-manager"></a>Considerazioni sulle prestazioni per Gestione traffico

impatto sulle prestazioni di solo Hello che dispongono di gestione traffico nel sito Web è ricerca DNS iniziale hello. Una richiesta DNS per il nome di hello del profilo di Traffic Manager viene gestita dal server principale di hello Microsoft DNS che ospita la zona trafficmanager.net hello. Gestione traffico compila e aggiorna regolarmente hello DNS radice server Microsoft in base a criteri di Traffic Manager hello e risultati probe hello. Pertanto, anche durante la ricerca DNS iniziale di hello, nessuna query DNS viene inviata tooTraffic Manager.

Gestione traffico è costituito da diversi componenti: il nome DNS server, un servizio API, il livello di archiviazione hello e un endpoint di servizio di monitoraggio. Se un componente del servizio Gestione traffico non riesce, non vi è alcun effetto sul nome DNS hello associato al profilo di Traffic Manager. record Hello in server Microsoft DNS hello rimangono invariati. Il monitoraggio degli endpoint e l'aggiornamento DNS, tuttavia, non vengono eseguiti. Pertanto, Traffic Manager non è in grado di tooupdate DNS toopoint tooyour failover sito quando si arresta il sito primario.

La risoluzione dei nomi DNS è rapida e i risultati vengono memorizzati nella cache. Hello velocità di ricerca DNS iniziale hello varia a seconda hello client hello di server DNS viene utilizzato per la risoluzione dei nomi. In genere, un client è in grado di eseguire una ricerca DNS in circa 50 ms. risultati di Hello di ricerca hello vengono memorizzati nella cache per la durata di hello di hello DNS Time-to-live (TTL). valore TTL per gestione traffico predefinito di Hello è 300 secondi.

Il traffico NON attraversa Gestione traffico. Al termine di ricerca DNS hello, hello client dispone di un indirizzo IP per un'istanza del sito web. Hello client si connette direttamente toothat indirizzo e il non passa attraverso Traffic Manager. criterio di Traffic Manager si sceglie di Hello non ha effetto sulle prestazioni di DNS hello. Tuttavia, un metodo di routing di prestazioni può influire negativamente sulle prestazioni dell'applicazione hello. Ad esempio, se i criteri reindirizza il traffico dal Nord America tooan istanza ospitata in Asia, latenza di rete hello per le sessioni può essere un problema di prestazioni.

## <a name="measuring-traffic-manager-performance"></a>Misurazione delle prestazioni di Gestione traffico

Esistono diversi siti Web, è possibile utilizzare toounderstand hello prestazioni e sul comportamento di un profilo di Traffic Manager. Molti di questi siti sono gratuiti, ma possono presentare alcune limitazioni. Alcuni siti offrono servizi avanzati di monitoraggio e report a pagamento.

strumenti Hello in questi siti misurano le latenze DNS e visualizzazione hello risolto gli indirizzi IP per tutto il mondo hello posizioni del client. La maggior parte di questi strumenti non memorizzare nella cache i risultati di DNS hello. Di conseguenza, gli strumenti di hello dimostrano ricerca DNS completa hello ogni volta che viene eseguito un test. Quando si testa da un client specifico, si verificano solo hello completo DNS le prestazioni di ricerca di una volta durante la durata TTL hello.

## <a name="sample-tools-toomeasure-dns-performance"></a>Prestazioni DNS toomeasure strumenti di esempio

* [SolveDNS](http://www.solvedns.com/dns-comparison/)

    SolveDNS offre diversi strumenti per la misurazione delle prestazioni. strumento di confronto del DNS Hello consente di visualizzare il tempo impiegato tooresolve il nome DNS e il modo in cui che confronta i provider di servizi DNS tooother.

* [WebSitePulse](http://www.websitepulse.com/help/tools.php)

    Uno degli strumenti più semplici di hello è WebSitePulse. Immettere i tempi di risoluzione DNS toosee hello URL, il primo Byte, l'ultimo Byte e altre statistiche sulle prestazioni. È possibile scegliere tra tre posizioni di test. In questo esempio, si noterà che prima esecuzione hello è indicato che la ricerca DNS accetta 0.204 sec.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse.png)

    Poiché i risultati vengono memorizzati nella cache, hello hello secondo test hello ricerca DNS hello endpoint di gestione traffico stesso accetta 0.002 sec.

    ![pulse2](./media/traffic-manager-performance-considerations/traffic-manager-web-site-pulse2.png)

* [CA App Synthetic Monitor](https://asm.ca.com/en/checkit.php)

    In precedenza come strumento di hello Watchmouse sito Web di controllo, questo sito mostrano hello risoluzione DNS ora contemporaneamente da più aree geografiche. Immettere i tempi di risoluzione DNS toosee hello URL, il tempo di connessione e velocità da diverse posizioni geografiche. Utilizzare questo toosee test viene restituito il servizio ospitato per percorsi diversi in tutto il mondo hello.

    ![pulse1](./media/traffic-manager-performance-considerations/traffic-manager-web-site-watchmouse.png)

* [Pingdom](http://tools.pingdom.com/)

    Questo strumento offre statistiche sulle prestazioni per ogni elemento di una pagina Web. scheda analisi pagina Hello Mostra percentuale di hello di tempo impiegato per la ricerca DNS.

* [What's My DNS?](http://www.whatsmydns.net/)

    Il sito esegue una ricerca DNS da diverse 20 posizioni e Visualizza risultati hello su una mappa.

* [Dig Web Interface](http://www.digwebinterface.com)

    Mostra informazioni più dettagliate sul DNS, inclusi i record A e CNAME. Verificare che si selezioni 'Colorizza output di hello' e 'Stats' opzioni e selezionare "All" Nameservers.

## <a name="next-steps"></a>Passaggi successivi

[Informazioni sui metodi di routing di Gestione traffico](traffic-manager-routing-methods.md)

[Verifica delle impostazioni di Gestione traffico](traffic-manager-testing-settings.md)

[Operazioni per Gestione traffico (informazioni di riferimento API REST)](http://go.microsoft.com/fwlink/?LinkId=313584)

[Cmdlet di Gestione traffico di Azure](http://go.microsoft.com/fwlink/p/?LinkId=400769)

