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
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="5f387-103">Eseguire il rilevamento di intrusioni di rete con Network Watcher e strumenti open source</span><span class="sxs-lookup"><span data-stu-id="5f387-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="5f387-104">Le acquisizioni di pacchetti sono un componente chiave per l'implementazione di sistemi di rilevamento di intrusioni (IDS, Intrusion Detection System) di rete e per l'esecuzione del monitoraggio della sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5f387-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="5f387-105">Esistono diversi strumenti IDS open source che elaborano le acquisizioni di pacchetti e cercano le firme di possibili intrusioni di rete e di attività dannosa.</span><span class="sxs-lookup"><span data-stu-id="5f387-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="5f387-106">Utilizzando le acquisizioni di pacchetti hello fornite da Watcher di rete, è possibile analizzare la rete per qualsiasi intrusioni dannose o vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="5f387-106">Using hello packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="5f387-107">Una tale strumento open source è Suricata, un motore ID che utilizza il traffico di rete di RuleSet toomonitor e genera avvisi quando si verificano eventi sospetti.</span><span class="sxs-lookup"><span data-stu-id="5f387-107">One such open source tool is Suricata, an IDS engine that uses rulesets toomonitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="5f387-108">Suricata offre un motore a thread multipli e può quindi eseguire l'analisi del traffico di rete con maggiore velocità ed efficienza.</span><span class="sxs-lookup"><span data-stu-id="5f387-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="5f387-109">Per altri dettagli su Suricata e sulle relative funzionalità, visitare il sito Web all'indirizzo https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="5f387-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="5f387-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="5f387-110">Scenario</span></span>

<span data-ttu-id="5f387-111">In questo articolo illustra tooset backup tooperform l'ambiente utilizzando Watcher di rete, Suricata, il rilevamento delle intrusioni di rete e hello elastico dello Stack.</span><span class="sxs-lookup"><span data-stu-id="5f387-111">This article explains how tooset up your environment tooperform network intrusion detection using Network Watcher, Suricata, and hello Elastic Stack.</span></span> <span data-ttu-id="5f387-112">Watcher di rete offre che i pacchetti hello acquisisce rilevamento delle intrusioni di rete tooperform utilizzato.</span><span class="sxs-lookup"><span data-stu-id="5f387-112">Network Watcher provides you with hello packet captures used tooperform network intrusion detection.</span></span> <span data-ttu-id="5f387-113">Acquisizioni di pacchetti di hello Suricata processi e trigger avvisi basati su pacchetti che soddisfano il set di regole specificato delle minacce.</span><span class="sxs-lookup"><span data-stu-id="5f387-113">Suricata processes hello packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="5f387-114">Questi avvisi vengono archiviati in un file di log nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="5f387-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="5f387-115">Utilizza hello Stack elastico, hello e registri di generati da Suricata possono essere indicizzati utilizzato toocreate un dashboard Kibana, offrendo una rappresentazione visiva dei registri hello e un mezzo tooquickly guadagno insights toopotential le vulnerabilità della rete.</span><span class="sxs-lookup"><span data-stu-id="5f387-115">Using hello Elastic Stack, hello logs generated by Suricata can be indexed and used toocreate a Kibana dashboard, providing you with a visual representation of hello logs and a means tooquickly gain insights toopotential network vulnerabilities.</span></span>  

![Scenario di applicazione Web semplice][1]

<span data-ttu-id="5f387-117">Entrambi gli strumenti Apri origine da impostare in una macchina virtuale di Azure, consentendo tooperform questa analisi nell'ambiente di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="5f387-117">Both open source tools can be set up on an Azure VM, allowing you tooperform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="5f387-118">Passi</span><span class="sxs-lookup"><span data-stu-id="5f387-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="5f387-119">Installare Suricata</span><span class="sxs-lookup"><span data-stu-id="5f387-119">Install Suricata</span></span>

<span data-ttu-id="5f387-120">Per tutti gli altri metodi di installazione, visitare http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="5f387-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="5f387-121">Nel terminale della riga di comando di hello della macchina virtuale eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5f387-121">In hello command-line terminal of your VM run hello following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="5f387-122">tooverify l'installazione, eseguire il comando hello `suricata -h` elenco completo di hello toosee dei comandi.</span><span class="sxs-lookup"><span data-stu-id="5f387-122">tooverify your installation, run hello command `suricata -h` toosee hello full list of commands.</span></span>

### <a name="download-hello-emerging-threats-ruleset"></a><span data-ttu-id="5f387-123">Scaricare hello minacce emergenti ruleset</span><span class="sxs-lookup"><span data-stu-id="5f387-123">Download hello Emerging Threats ruleset</span></span>

<span data-ttu-id="5f387-124">In questa fase, non sono presenti tutte le regole per Suricata toorun.</span><span class="sxs-lookup"><span data-stu-id="5f387-124">At this stage, we do not have any rules for Suricata toorun.</span></span> <span data-ttu-id="5f387-125">Se esistono rischi di minacce specifiche tooyour rete toodetect oppure è possibile inoltre utilizzare sviluppato set di regole da un numero di provider, ad esempio minacce emergenti o regole VRT Snort, è possibile creare regole personalizzate.</span><span class="sxs-lookup"><span data-stu-id="5f387-125">You can create your own rules if there are specific threats tooyour network you would like toodetect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="5f387-126">Utilizziamo hello accedere liberamente emergenti minacce ruleset qui:</span><span class="sxs-lookup"><span data-stu-id="5f387-126">We use hello freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="5f387-127">Scaricare il set di regole hello e copiarli nella directory hello:</span><span class="sxs-lookup"><span data-stu-id="5f387-127">Download hello rule set and copy them into hello directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="5f387-128">Elaborare le acquisizioni di pacchetti con Suricata</span><span class="sxs-lookup"><span data-stu-id="5f387-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="5f387-129">acquisizioni di pacchetti tooprocess utilizzando Suricata, eseguire hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5f387-129">tooprocess packet captures using Suricata, run hello following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="5f387-130">toocheck hello risultante avvisi, leggere il file fast.log hello:</span><span class="sxs-lookup"><span data-stu-id="5f387-130">toocheck hello resulting alerts, read hello fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-hello-elastic-stack"></a><span data-ttu-id="5f387-131">Impostare hello Stack elastico</span><span class="sxs-lookup"><span data-stu-id="5f387-131">Set up hello Elastic Stack</span></span>

<span data-ttu-id="5f387-132">Mentre i registri di hello che produce Suricata contengono importanti informazioni su ciò che avviene nella rete, questi file di log non sono tooread più semplice hello e comprendano.</span><span class="sxs-lookup"><span data-stu-id="5f387-132">While hello logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t hello easiest tooread and understand.</span></span> <span data-ttu-id="5f387-133">Connettendo Suricata con hello Stack elastico, è possibile creare un dashboard Kibana cosa consente toosearch, grafico, analizzare e derivare informazioni dai nostri registri.</span><span class="sxs-lookup"><span data-stu-id="5f387-133">By connecting Suricata with hello Elastic Stack, we can create a Kibana dashboard what allows us toosearch, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="5f387-134">Installare Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="5f387-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="5f387-135">Hello Stack elastico dalla versione 5.0 e versioni successive richiede Java 8.</span><span class="sxs-lookup"><span data-stu-id="5f387-135">hello Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="5f387-136">Eseguire il comando hello `java -version` toocheck la versione in uso.</span><span class="sxs-lookup"><span data-stu-id="5f387-136">Run hello command `java -version` toocheck your version.</span></span> <span data-ttu-id="5f387-137">Se non si dispone java installare, vedere toodocumentation su [sito Web Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="5f387-137">If you do not have java install, refer toodocumentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="5f387-138">Scaricare hello pacchetto binario corretto per il sistema:</span><span class="sxs-lookup"><span data-stu-id="5f387-138">Download hello correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="5f387-139">Per altri metodi di installazione, vedere [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installazione di Elasticsearch)</span><span class="sxs-lookup"><span data-stu-id="5f387-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="5f387-140">Verificare che Elasticsearch sia in esecuzione con il comando hello:</span><span class="sxs-lookup"><span data-stu-id="5f387-140">Verify that Elasticsearch is running with hello command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="5f387-141">Verrà visualizzato un toothis simile risposta:</span><span class="sxs-lookup"><span data-stu-id="5f387-141">You should see a response similar toothis:</span></span>

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

<span data-ttu-id="5f387-142">Per ulteriori istruzioni sull'installazione ricerca elastico, vedere la pagina toohello [installazione](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span><span class="sxs-lookup"><span data-stu-id="5f387-142">For further instructions on installing Elastic search, refer toohello page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="5f387-143">Installare Logstash</span><span class="sxs-lookup"><span data-stu-id="5f387-143">Install Logstash</span></span>

1. <span data-ttu-id="5f387-144">tooinstall Logstash eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="5f387-144">tooinstall Logstash run hello following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="5f387-145">Quindi, sarà necessario tooconfigure Logstash tooread dall'output di hello del file eve.json.</span><span class="sxs-lookup"><span data-stu-id="5f387-145">Next we need tooconfigure Logstash tooread from hello output of eve.json file.</span></span> <span data-ttu-id="5f387-146">Creare un file logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="5f387-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="5f387-147">Aggiungere i seguenti file di contenuto toohello hello (assicurarsi che il file di eve.json hello toohello percorso sia corretto):</span><span class="sxs-lookup"><span data-stu-id="5f387-147">Add hello following content toohello file (make sure that hello path toohello eve.json file is correct):</span></span>

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

1. <span data-ttu-id="5f387-148">Verificare che toogive hello toohello il delle autorizzazioni corrette eve.json file in modo che Logstash in grado di acquisire file hello.</span><span class="sxs-lookup"><span data-stu-id="5f387-148">Make sure toogive hello correct permissions toohello eve.json file so that Logstash can ingest hello file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="5f387-149">eseguire il comando hello Logstash toostart:</span><span class="sxs-lookup"><span data-stu-id="5f387-149">toostart Logstash run hello command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="5f387-150">Per ulteriori istruzioni sull'installazione Logstash, consultare toohello [documentazione ufficiale](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="5f387-150">For further instructions on installing Logstash, refer toohello [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="5f387-151">Installare Kibana</span><span class="sxs-lookup"><span data-stu-id="5f387-151">Install Kibana</span></span>

1. <span data-ttu-id="5f387-152">Eseguire i seguenti comandi tooinstall Kibana hello:</span><span class="sxs-lookup"><span data-stu-id="5f387-152">Run hello following commands tooinstall Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="5f387-153">toorun Kibana utilizzare i comandi di hello:</span><span class="sxs-lookup"><span data-stu-id="5f387-153">toorun Kibana use hello commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="5f387-154">tooview web Kibana interfaccia, passare troppo`http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="5f387-154">tooview your Kibana web interface, navigate too`http://localhost:5601`</span></span>
1. <span data-ttu-id="5f387-155">Per questo scenario, il criterio di indice hello utilizzato per hello Suricata registra è "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="5f387-155">For this scenario, hello index pattern used for hello Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="5f387-156">Se si desidera dashboard Kibana di tooview hello in modalità remota, creare una regola di gruppo in ingresso che consente l'accesso troppo**porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="5f387-156">If you want tooview hello Kibana dashboard remotely, create an inbound NSG rule allowing access too**port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="5f387-157">Creare un dashboard Kibana</span><span class="sxs-lookup"><span data-stu-id="5f387-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="5f387-158">In questo articolo, Microsoft ha fornito un dashboard di esempio per consentire le tendenze tooview e i dettagli degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="5f387-158">For this article, we have provided a sample dashboard for you tooview trends and details in your alerts.</span></span>

1. <span data-ttu-id="5f387-159">Scaricare il file dashboard hello [qui](https://aka.ms/networkwatchersuricatadashboard), file di visualizzazione hello [qui](https://aka.ms/networkwatchersuricatavisualization)e i file di ricerca salvata hello [qui](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="5f387-159">Download hello dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), hello visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and hello saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="5f387-160">In hello **Management** scheda di Kibana, passare troppo**gli oggetti salvati** e importare tutti i tre file.</span><span class="sxs-lookup"><span data-stu-id="5f387-160">Under hello **Management** tab of Kibana, navigate too**Saved Objects** and import all three files.</span></span> <span data-ttu-id="5f387-161">Quindi dal hello **Dashboard** scheda è possibile aprire e carico hello dashboard di esempio.</span><span class="sxs-lookup"><span data-stu-id="5f387-161">Then from hello **Dashboard** tab you can open and load hello sample dashboard.</span></span>

<span data-ttu-id="5f387-162">È anche possibile creare visualizzazioni e dashboard personalizzati per le metriche a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="5f387-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="5f387-163">Per altre informazioni sulla creazione di visualizzazioni Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/kibana/current/visualize.html) di Kibana.</span><span class="sxs-lookup"><span data-stu-id="5f387-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![Dashboard Kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="5f387-165">Visualizzare i log di avvisi IDS</span><span class="sxs-lookup"><span data-stu-id="5f387-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="5f387-166">dashboard di esempio Hello fornisce diverse visualizzazioni dei log di avviso Suricata hello:</span><span class="sxs-lookup"><span data-stu-id="5f387-166">hello sample dashboard provides several visualizations of hello Suricata alert logs:</span></span>

1. <span data-ttu-id="5f387-167">Avvisi da GeoIP: una mappa con la distribuzione di hello di avvisi in base al paese di origine in base alla posizione geografica (determinata dal IP)</span><span class="sxs-lookup"><span data-stu-id="5f387-167">Alerts by GeoIP – a map showing hello distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![IP geografico][3]

1. <span data-ttu-id="5f387-169">Primi 10 avvisi: un riepilogo degli avvisi di hello 10 più frequenti attivata e la relativa descrizione.</span><span class="sxs-lookup"><span data-stu-id="5f387-169">Top 10 Alerts – a summary of hello 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="5f387-170">Fare clic su un singolo avviso Filtra verso il basso hello dashboard toohello informazioni toothat specifico avviso.</span><span class="sxs-lookup"><span data-stu-id="5f387-170">Clicking an individual alert filters down hello dashboard toohello information pertaining toothat specific alert.</span></span>

    ![Immagine 4][4]

1. <span data-ttu-id="5f387-172">Numero di avvisi: hello conteggio totale di avvisi generati dal set di regole hello</span><span class="sxs-lookup"><span data-stu-id="5f387-172">Number of Alerts – hello total count of alerts triggered by hello ruleset</span></span>

    ![Immagine 5][5]

1. <span data-ttu-id="5f387-174">Primi 20 origine/destinazione IP/porte, i grafici a torta che mostra hello superiore e 20 indirizzi IP e porte di avviso in cui sono state attivate in.</span><span class="sxs-lookup"><span data-stu-id="5f387-174">Top 20 Source/Destination IPs/Ports - pie charts showing hello top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="5f387-175">È possibile filtrare verso il basso toosee specifico di indirizzi IP/porte quanti e quali tipi di avvisi vengono attivati.</span><span class="sxs-lookup"><span data-stu-id="5f387-175">You can filter down on specific IPs/ports toosee how many and what kind of alerts are being triggered.</span></span>

    ![Immagine 6][6]

1. <span data-ttu-id="5f387-177">Alert Summary (Riepilogo avvisi): tabella che riepiloga specifici dettagli di ogni singolo avviso.</span><span class="sxs-lookup"><span data-stu-id="5f387-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="5f387-178">È possibile personalizzare questo tooshow tabella altri parametri di interesse per ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="5f387-178">You can customize this table tooshow other parameters of interest for each alert.</span></span>

    ![Immagine 7][7]

<span data-ttu-id="5f387-180">Per altri documenti sulla creazione di visualizzazioni e dashboard personalizzati, vedere la [documentazione ufficiale di Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="5f387-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="5f387-181">Conclusione</span><span class="sxs-lookup"><span data-stu-id="5f387-181">Conclusion</span></span>

<span data-ttu-id="5f387-182">Combinando le acquisizioni di pacchetti fornite da Network Watcher e da strumenti IDS open source come Suricata, è possibile eseguire il rilevamento di intrusioni di rete per svariate minacce.</span><span class="sxs-lookup"><span data-stu-id="5f387-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="5f387-183">Questi dashboard consentono si tooquickly individuare tendenze e anomalie all'interno della rete, nonché di esaminare in hello dati toodiscover cause degli avvisi, ad esempio gli agenti utente malintenzionato o porte vulnerabili.</span><span class="sxs-lookup"><span data-stu-id="5f387-183">These dashboards allow you tooquickly spot trends and anomalies within your network, as well dig into hello data toodiscover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="5f387-184">Con questi dati estratti, è possibile prendere decisioni informate in modalità tooreact tooand proteggere la rete da qualsiasi tentativo di intrusione dannoso e creare regole tooprevent intrusioni future tooyour rete.</span><span class="sxs-lookup"><span data-stu-id="5f387-184">With this extracted data, you can make informed decisions on how tooreact tooand protect your network from any harmful intrusion attempts, and create rules tooprevent future intrusions tooyour network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f387-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5f387-185">Next steps</span></span>

<span data-ttu-id="5f387-186">Informazioni su come pacchetto tootrigger acquisisce gli avvisi in base a visitando [utilizzare pacchetti acquisizione toodo attiva il monitoraggio della rete con le funzioni di Azure](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="5f387-186">Learn how tootrigger packet captures based on alerts by visiting [Use packet capture toodo proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="5f387-187">Informazioni su come toovisualize il flusso di gruppo Registra con Power BI visitando [NSG visualizzare flussi di log con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="5f387-187">Learn how toovisualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
