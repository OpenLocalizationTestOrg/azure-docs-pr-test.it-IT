---
title: flusso di controllo di rete di Azure aaaVisualize registra utilizzando strumenti open source | Documenti Microsoft
description: "Questa pagina vengono descritti come modalità di apertura di log del flusso di origine strumenti toovisualize NSG toouse."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e9b2dcad-4da4-4d6b-aee2-6d0afade0cb8
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 47cb529d4a1e00e8c4c0fa6885cbf72aed3e74c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-azure-network-watcher-nsg-flow-logs-using-open-source-tools"></a>Visualizzare i log dei flussi dei gruppi di sicurezza di rete di Azure Network Watcher con strumenti open source

I log dei flussi dei gruppi di sicurezza di rete contengono informazioni utili per comprendere il traffico IP in ingresso e in uscita nei gruppi di sicurezza di rete. Questi log flusso mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applica, 5 tuple informazioni flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol), e se il traffico hello consentito o negato.

Questi registri di flusso possono essere difficile toomanually analisi e ottenere informazioni approfondite. Esistono tuttavia diversi strumenti open source che possono semplificare la visualizzazione di questi dati. In questo articolo verrà fornite toovisualize una soluzione di questi log tramite hello elastico Stack, che consentono di indice tooquickly e visualizzare i log di flusso in un dashboard Kibana.

## <a name="scenario"></a>Scenario

In questo articolo, si imposterà una soluzione che consentirà di registri di flusso di gruppo di sicurezza di rete toovisualize mediante hello Stack elastico.  Un plug-in di input Logstash otterrà registri flusso hello direttamente dal blob di archiviazione hello configurato per contenente i registri del flusso di hello. Quindi, utilizza hello Stack elastico, hello flusso registri verranno indicizzati e utilizzato toocreate una Kibana toovisualize hello le informazioni relative.

![scenario][scenario]

## <a name="steps"></a>Passi

### <a name="enable-network-security-group-flow-logging"></a>Abilitare la registrazione dei flussi dei gruppi di sicurezza di rete
Per questo scenario, è necessario abilitare la registrazione dei flussi dei gruppi di sicurezza di rete in almeno un gruppo di sicurezza di rete nel proprio account. Per istruzioni su come abilitare i registri di flusso di sicurezza di rete, consultare toohello articolo seguente [registrazione tooflow introduzione per gruppi di sicurezza di rete](network-watcher-nsg-flow-logging-overview.md).


### <a name="set-up-hello-elastic-stack"></a>Impostare hello Stack elastico
Connettendosi NSG flusso registri con hello Stack elastico, è possibile creare un dashboard Kibana cosa consente toosearch, grafico, analizzare e derivare informazioni dai nostri registri.

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
1. Successivamente è necessario tooconfigure Logstash tooaccess e analizzare i log di flusso hello. Creare un file logstash.conf usando:

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. Aggiungere i seguenti file di contenuto toohello hello:

  ```
    input {
      azureblob
        {
            storage_account_name => "mystorageaccount"
            storage_access_key => "storageaccesskey"
            container => "nsgflowlogContainerName"
            codec => "json"
        }
      }

      filter {
        split { field => "[records]" }
        split { field => "[records][properties][flows]"}
        split { field => "[records][properties][flows][flows]"}
        split { field => "[records][properties][flows][flows][flowTuples]"}

     mutate{
      split => { "[records][resourceId]" => "/"}
      add_field => {"Subscription" => "%{[records][resourceId][2]}"
                    "ResourceGroup" => "%{[records][resourceId][4]}"
                    "NetworkSecurityGroup" => "%{[records][resourceId][8]}"}
      convert => {"Subscription" => "string"}
      convert => {"ResourceGroup" => "string"}
      convert => {"NetworkSecurityGroup" => "string"}
      split => { "[records][properties][flows][flows][flowTuples]" => ","}
      add_field => {
                  "unixtimestamp" => "%{[records][properties][flows][flows][flowTuples][0]}"
                  "srcIp" => "%{[records][properties][flows][flows][flowTuples][1]}"
                  "destIp" => "%{[records][properties][flows][flows][flowTuples][2]}"
                  "srcPort" => "%{[records][properties][flows][flows][flowTuples][3]}"
                  "destPort" => "%{[records][properties][flows][flows][flowTuples][4]}"
                  "protocol" => "%{[records][properties][flows][flows][flowTuples][5]}"
                  "trafficflow" => "%{[records][properties][flows][flows][flowTuples][6]}"
                  "traffic" => "%{[records][properties][flows][flows][flowTuples][7]}"
                   }
      convert => {"unixtimestamp" => "integer"}
      convert => {"srcPort" => "integer"}
      convert => {"destPort" => "integer"}        
     }

     date{
       match => ["unixtimestamp" , "UNIX"]
     }
    }

    output {
      stdout { codec => rubydebug }
      elasticsearch {
        hosts => "localhost"
        index => "nsg-flow-logs"
      }
    }  

  ```

Per ulteriori istruzioni sull'installazione Logstash, consultare toohello [documentazione ufficiale](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)

### <a name="install-hello-logstash-input-plugin-for-azure-blob-storage"></a>Installare hello Logstash input del plug-in per l'archiviazione blob di Azure

Questo plug-in Logstash consentirà toodirectly accesso hello flusso registri il proprio account di archiviazione designate. tooinstall questo plug-in, dalla directory di installazione di Logstash hello predefinita (in questo caso /usr/share/logstash/bin) comando hello:

```
logstash-plugin install logstash-input-azureblob
```

eseguire il comando hello Logstash toostart:

```
sudo /etc/init.d/logstash start
```

Per ulteriori informazioni su questo plug-in, vedere toodocumentation [qui](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-input-azureblob)

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
1. Per questo scenario, il modello di indice hello usato per i log di flusso hello è "nsg-flusso di log". È possibile modificare il modello di indice hello nella sezione "output" hello del file logstash.conf.

1. Se si desidera dashboard Kibana di tooview hello in modalità remota, creare una regola di gruppo in ingresso che consente l'accesso troppo**porta 5601**.

### <a name="create-a-kibana-dashboard"></a>Creare un dashboard Kibana

In questo articolo, Microsoft ha fornito un dashboard di esempio per consentire le tendenze tooview e i dettagli degli avvisi.

![Figura 1][1]

1. Scaricare il file dashboard hello [qui](https://aka.ms/networkwatchernsgflowlogdashboard), file di visualizzazione hello [qui](https://aka.ms/networkwatchernsgflowlogvisualizations)e i file di ricerca salvata hello [qui](https://aka.ms/networkwatchernsgflowlogsearch).

1. In hello **Management** scheda di Kibana, passare troppo**gli oggetti salvati** e importare tutti i tre file. Quindi dal hello **Dashboard** scheda è possibile aprire e carico hello dashboard di esempio.

È anche possibile creare visualizzazioni e dashboard personalizzati per le metriche a cui si è interessati. Per altre informazioni sulla creazione di visualizzazioni Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/kibana/current/visualize.html) di Kibana.

### <a name="visualize-nsg-flow-logs"></a>Visualizzare i log dei flussi dei gruppi di sicurezza di rete

dashboard di esempio Hello fornisce diverse visualizzazioni dei registri di flusso hello:

1. I flussi dalla decisione/direzione nel tempo, i grafici di serie temporali che mostra il numero di hello di flussi su hello periodo di tempo. È possibile modificare l'unità di hello di tempo e l'intervallo di entrambe queste visualizzazioni. Flussi di base delle decisioni Mostra hello proporzione di consentono o negare le decisioni prese, mentre i flussi da parte di hello Mostra direzione del traffico in ingresso e in uscita. Questi oggetti visivi consentono di esaminare le tendenze del traffico nel tempo e individuare eventuali picchi o modelli insoliti.

  ![Figura 2][2]

1. I flussi dalla porta di origine/destinazione: grafici a torta che mostra la suddivisione hello di flussi di tootheir rispettive porte. Questa visualizzazione consente di verificare le porte più usate. Se si fa clic su una porta specifica all'interno del grafico a torta hello, rest hello del dashboard hello filtrerà verso il basso tooflows di tale porta.

  ![Figura 3][3]

1. Numero di flussi e ora Log meno recente: metriche mostrando hello numero di flussi registrato e data hello del log meno recente hello acquisiti.

  ![Figura 4][4]

1. Flussi di gruppo e regola, un grafico a barre che mostra distribuzione hello dei flussi all'interno di ogni gruppo, nonché distribuzione hello di regole all'interno di ogni gruppo. Da qui è possibile visualizzare il gruppo e le regole generati hello maggior parte del traffico.

  ![Figura 5][5]

1. Primi 10 origine/destinazione IP: grafici a barre che mostra origine primi 10 hello e gli indirizzi IP di destinazione. È possibile modificare questi tooshow grafici gli indirizzi IP superiore più o meno. Da qui è possibile vedere hello più di frequente che si verificano gli indirizzi IP, nonché hello decisione di traffico (Consenti o Nega) apportate a ogni IP.

  ![Figura 6][6]

1. Tuple di flusso: in questa tabella mostra le informazioni contenute all'interno di ogni tupla del flusso, nonché il relativo NGS corrispondente e regola hello.

  ![Figura 7][7]

Usa barra query hello nella parte superiore di hello del dashboard hello, è possibile filtrare verso il basso dashboard hello in base a qualsiasi parametro di hello flussi, ad esempio l'ID sottoscrizione, i gruppi di risorse, regola o qualsiasi altra variabile di interesse. Per ulteriori informazioni sulla query e i filtri del Kibana, consultare toohello [documentazione ufficiale](https://www.elastic.co/guide/en/beats/packetbeat/current/kibana-queries-filters.html)

## <a name="conclusion"></a>Conclusioni

Combinando i registri del flusso di hello il gruppo di sicurezza di rete con hello Stack elastico è stata ideare toovisualize sistema efficiente e personalizzabile il traffico di rete. Questi dashboard consentono un miglioramento tooquickly e condividono informazioni dettagliate sul traffico di rete, nonché filtro verso il basso e analizzare in qualsiasi potenziali anomalie. Utilizza Kibana, è possibile personalizzare questi dashboard e creare visualizzazioni specifiche toomeet eventuali esigenze di sicurezza, conformità e controllo.

## <a name="next-steps"></a>Passaggi successivi

Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)


<!--Image references-->

[scenario]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/scenario.png
[1]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure1.png
[2]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure2.png
[3]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure3.png
[4]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure4.png
[5]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure5.png
[6]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure6.png
[7]: ./media/network-watcher-visualize-nsg-flow-logs-open-source-tools/figure7.png
