---
title: rilevamento delle intrusioni di rete aaaPerform con Watcher di rete di Azure e strumenti open source | Documenti Microsoft
description: "Questo articolo descrive la modalità di toouse Watcher di rete di Azure e Apri origine strumenti tooperform intrusioni di rete"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 0f043f08-19e1-4125-98b0-3e335ba69681
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: b5a909b827ab32ad6b2fd8e2911a944fd940249e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a>Eseguire il rilevamento di intrusioni di rete con Network Watcher e strumenti open source

Le acquisizioni di pacchetti sono un componente chiave per l'implementazione di sistemi di rilevamento di intrusioni (IDS, Intrusion Detection System) di rete e per l'esecuzione del monitoraggio della sicurezza di rete. Esistono diversi strumenti IDS open source che elaborano le acquisizioni di pacchetti e cercano le firme di possibili intrusioni di rete e di attività dannosa. Utilizzando le acquisizioni di pacchetti hello fornite da Watcher di rete, è possibile analizzare la rete per qualsiasi intrusioni dannose o vulnerabilità.

Una tale strumento open source è Suricata, un motore ID che utilizza il traffico di rete di RuleSet toomonitor e genera avvisi quando si verificano eventi sospetti. Suricata offre un motore a thread multipli e può quindi eseguire l'analisi del traffico di rete con maggiore velocità ed efficienza. Per altri dettagli su Suricata e sulle relative funzionalità, visitare il sito Web all'indirizzo https://suricata-ids.org/.

## <a name="scenario"></a>Scenario

In questo articolo illustra tooset backup tooperform l'ambiente utilizzando Watcher di rete, Suricata, il rilevamento delle intrusioni di rete e hello elastico dello Stack. Watcher di rete offre che i pacchetti hello acquisisce rilevamento delle intrusioni di rete tooperform utilizzato. Acquisizioni di pacchetti di hello Suricata processi e trigger avvisi basati su pacchetti che soddisfano il set di regole specificato delle minacce. Questi avvisi vengono archiviati in un file di log nel computer locale. Utilizza hello Stack elastico, hello e registri di generati da Suricata possono essere indicizzati utilizzato toocreate un dashboard Kibana, offrendo una rappresentazione visiva dei registri hello e un mezzo tooquickly guadagno insights toopotential le vulnerabilità della rete.  

![Scenario di applicazione Web semplice][1]

Entrambi gli strumenti Apri origine da impostare in una macchina virtuale di Azure, consentendo tooperform questa analisi nell'ambiente di rete di Azure.

## <a name="steps"></a>Passi

### <a name="install-suricata"></a>Installare Suricata

Per tutti gli altri metodi di installazione, visitare http://suricata.readthedocs.io/en/latest/install.html

1. Nel terminale della riga di comando di hello della macchina virtuale eseguire hello seguenti comandi:

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. tooverify l'installazione, eseguire il comando hello `suricata -h` elenco completo di hello toosee dei comandi.

### <a name="download-hello-emerging-threats-ruleset"></a>Scaricare hello minacce emergenti ruleset

In questa fase, non sono presenti tutte le regole per Suricata toorun. Se esistono rischi di minacce specifiche tooyour rete toodetect oppure è possibile inoltre utilizzare sviluppato set di regole da un numero di provider, ad esempio minacce emergenti o regole VRT Snort, è possibile creare regole personalizzate. Utilizziamo hello accedere liberamente emergenti minacce ruleset qui:

Scaricare il set di regole hello e copiarli nella directory hello:

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a>Elaborare le acquisizioni di pacchetti con Suricata

acquisizioni di pacchetti tooprocess utilizzando Suricata, eseguire hello comando seguente:

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
toocheck hello risultante avvisi, leggere il file fast.log hello:
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a>Impostare hello Stack elastico

Mentre i registri di hello che produce Suricata contengono importanti informazioni su ciò che avviene nella rete, questi file di log non sono tooread più semplice hello e comprendano. Connettendo Suricata con hello Stack elastico, è possibile creare un dashboard Kibana cosa consente toosearch, grafico, analizzare e derivare informazioni dai nostri registri.

#### <a name="install-elasticsearch"></a>Installare Elasticsearch

1. Hello Stack elastico dalla versione 5.0 e versioni successive richiede Java 8. Eseguire il comando hello `java -version` toocheck la versione in uso. Se non si dispone java installare, vedere toodocumentation su [sito Web Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)
1. Scaricare hello pacchetto binario corretto per il sistema:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    Per altri metodi di installazione, vedere [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installazione di Elasticsearch)

1. Verificare che Elasticsearch sia in esecuzione con il comando hello:

    ```
    curl http://127.0.0.1:9200
    ```

    Verrà visualizzato un toothis simile risposta:

    ```
    {
    "name" : "Angela Del Toro",
    "cluster_name" : "elasticsearch",
    "version" : {
        "number" : "5.2.0",
        "build_hash" : "8ff36d139e16f8720f2947ef62c8167a888992fe",
        "build_timestamp" : "2016-01-27T13:32:39Z",
        "build_snapshot" : false,
        "lucene_version" : "6.1.0"
    },
    "tagline" : "You Know, for Search"
    }
    ```

Per ulteriori istruzioni sull'installazione ricerca elastico, vedere la pagina toohello [installazione](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)

### <a name="install-logstash"></a>Installare Logstash

1. tooinstall Logstash eseguire hello seguenti comandi:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. Quindi, sarà necessario tooconfigure Logstash tooread dall'output di hello del file eve.json. Creare un file logstash.conf usando:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Aggiungere i seguenti file di contenuto toohello hello (assicurarsi che il file di eve.json hello toohello percorso sia corretto):

    ```ruby
    input {
    file {
        path => ["/var/log/suricata/eve.json"]
        codec =>  "json"
        type => "SuricataIDPS"
    }

    }

    filter {
    if [type] == "SuricataIDPS" {
        date {
        match => [ "timestamp", "ISO8601" ]
        }
        ruby {
        code => "
            if event.get('[event_type]') == 'fileinfo'
            event.set('[fileinfo][type]', event.get('[fileinfo][magic]').to_s.split(',')[0])
            end
        "
        }

        ruby{
        code => "
            if event.get('[event_type]') == 'alert'
            sp = event.get('[alert][signature]').to_s.split(' group ')
            if (sp.length == 2) and /\A\d+\z/.match(sp[1])
                event.set('[alert][signature]', sp[0])
            end
            end
            "
        }
    }

    if [src_ip]  {
        geoip {
        source => "src_ip"
        target => "geoip"
        #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
        add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
        add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
        }
        mutate {
        convert => [ "[geoip][coordinates]", "float" ]
        }
        if ![geoip.ip] {
        if [dest_ip]  {
            geoip {
            source => "dest_ip"
            target => "geoip"
            #database => "/opt/logstash/vendor/geoip/GeoLiteCity.dat"
            add_field => [ "[geoip][coordinates]", "%{[geoip][longitude]}" ]
            add_field => [ "[geoip][coordinates]", "%{[geoip][latitude]}"  ]
            }
            mutate {
            convert => [ "[geoip][coordinates]", "float" ]
            }
        }
        }
    }
    }

    output {
    elasticsearch {
        hosts => "localhost"
    }
    }
    ```

1. Verificare che toogive hello toohello il delle autorizzazioni corrette eve.json file in modo che Logstash in grado di acquisire file hello.
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. eseguire il comando hello Logstash toostart:

    ```
    sudo /etc/init.d/logstash start
    ```

Per ulteriori istruzioni sull'installazione Logstash, consultare toohello [documentazione ufficiale](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-kibana"></a>Installare Kibana

1. Eseguire i seguenti comandi tooinstall Kibana hello:

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. toorun Kibana utilizzare i comandi di hello:

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. tooview web Kibana interfaccia, passare troppo`http://localhost:5601`
1. Per questo scenario, il criterio di indice hello utilizzato per hello Suricata registra è "logstash-*"

1. Se si desidera dashboard Kibana di tooview hello in modalità remota, creare una regola di gruppo in ingresso che consente l'accesso troppo**porta 5601**.

### <a name="create-a-kibana-dashboard"></a>Creare un dashboard Kibana

In questo articolo, Microsoft ha fornito un dashboard di esempio per consentire le tendenze tooview e i dettagli degli avvisi.

1. Scaricare il file dashboard hello [qui](https://aka.ms/networkwatchersuricatadashboard), file di visualizzazione hello [qui](https://aka.ms/networkwatchersuricatavisualization)e i file di ricerca salvata hello [qui](https://aka.ms/networkwatchersuricatasavedsearch).

1. In hello **Management** scheda di Kibana, passare troppo**gli oggetti salvati** e importare tutti i tre file. Quindi dal hello **Dashboard** scheda è possibile aprire e carico hello dashboard di esempio.

È anche possibile creare visualizzazioni e dashboard personalizzati per le metriche a cui si è interessati. Per altre informazioni sulla creazione di visualizzazioni Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/kibana/current/visualize.html) di Kibana.

![Dashboard Kibana][2]

### <a name="visualize-ids-alert-logs"></a>Visualizzare i log di avvisi IDS

dashboard di esempio Hello fornisce diverse visualizzazioni dei log di avviso Suricata hello:

1. Avvisi da GeoIP: una mappa con la distribuzione di hello di avvisi in base al paese di origine in base alla posizione geografica (determinata dal IP)

    ![IP geografico][3]

1. Primi 10 avvisi: un riepilogo degli avvisi di hello 10 più frequenti attivata e la relativa descrizione. Fare clic su un singolo avviso Filtra verso il basso hello dashboard toohello informazioni toothat specifico avviso.

    ![Immagine 4][4]

1. Numero di avvisi: hello conteggio totale di avvisi generati dal set di regole hello

    ![Immagine 5][5]

1. Primi 20 origine/destinazione IP/porte, i grafici a torta che mostra hello superiore e 20 indirizzi IP e porte di avviso in cui sono state attivate in. È possibile filtrare verso il basso toosee specifico di indirizzi IP/porte quanti e quali tipi di avvisi vengono attivati.

    ![Immagine 6][6]

1. Alert Summary (Riepilogo avvisi): tabella che riepiloga specifici dettagli di ogni singolo avviso. È possibile personalizzare questo tooshow tabella altri parametri di interesse per ogni avviso.

    ![Immagine 7][7]

Per altri documenti sulla creazione di visualizzazioni e dashboard personalizzati, vedere la [documentazione ufficiale di Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).

## <a name="conclusion"></a>Conclusione

Combinando le acquisizioni di pacchetti fornite da Network Watcher e da strumenti IDS open source come Suricata, è possibile eseguire il rilevamento di intrusioni di rete per svariate minacce. Questi dashboard consentono si tooquickly individuare tendenze e anomalie all'interno della rete, nonché di esaminare in hello dati toodiscover cause degli avvisi, ad esempio gli agenti utente malintenzionato o porte vulnerabili. Con questi dati estratti, è possibile prendere decisioni informate in modalità tooreact tooand proteggere la rete da qualsiasi tentativo di intrusione dannoso e creare regole tooprevent intrusioni future tooyour rete.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come pacchetto tootrigger acquisisce gli avvisi in base a visitando [utilizzare pacchetti acquisizione toodo attiva il monitoraggio della rete con le funzioni di Azure](network-watcher-alert-triggered-packet-capture.md)

Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
