---
title: Eseguire il rilevamento di intrusioni di rete con Azure Network Watcher e strumenti open source | Microsoft Docs
description: Questo articolo descrive come usare Azure Network Watcher e strumenti open source per eseguire il rilevamento di intrusioni di rete
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
ms.openlocfilehash: 82d5e525859ebe03b152c63e4debbae469049c12
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="perform-network-intrusion-detection-with-network-watcher-and-open-source-tools"></a><span data-ttu-id="da838-103">Eseguire il rilevamento di intrusioni di rete con Network Watcher e strumenti open source</span><span class="sxs-lookup"><span data-stu-id="da838-103">Perform network intrusion detection with Network Watcher and open source tools</span></span>

<span data-ttu-id="da838-104">Le acquisizioni di pacchetti sono un componente chiave per l'implementazione di sistemi di rilevamento di intrusioni (IDS, Intrusion Detection System) di rete e per l'esecuzione del monitoraggio della sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="da838-104">Packet captures are a key component for implementing network intrusion detection systems (IDS) and performing Network Security Monitoring (NSM).</span></span> <span data-ttu-id="da838-105">Esistono diversi strumenti IDS open source che elaborano le acquisizioni di pacchetti e cercano le firme di possibili intrusioni di rete e di attività dannosa.</span><span class="sxs-lookup"><span data-stu-id="da838-105">There are several open source IDS tools that process packet captures and look for signatures of possible network intrusions and malicious activity.</span></span> <span data-ttu-id="da838-106">Usando le acquisizioni di pacchetti fornite da Network Watcher, è possibile analizzare la rete per trovare eventuali intrusioni dannose o vulnerabilità.</span><span class="sxs-lookup"><span data-stu-id="da838-106">Using the packet captures provided by Network Watcher, you can analyze your network for any harmful intrusions or vulnerabilities.</span></span>

<span data-ttu-id="da838-107">Uno strumento open source di questo tipo è Suricata, un motore IDS che usa set di regole per monitorare il traffico di rete e attiva avvisi quando si verificano eventi sospetti.</span><span class="sxs-lookup"><span data-stu-id="da838-107">One such open source tool is Suricata, an IDS engine that uses rulesets to monitor network traffic and triggers alerts whenever suspicious events occur.</span></span> <span data-ttu-id="da838-108">Suricata offre un motore a thread multipli e può quindi eseguire l'analisi del traffico di rete con maggiore velocità ed efficienza.</span><span class="sxs-lookup"><span data-stu-id="da838-108">Suricata offers a multi-threaded engine, meaning it can perform network traffic analysis with increased speed and efficiency.</span></span> <span data-ttu-id="da838-109">Per altri dettagli su Suricata e sulle relative funzionalità, visitare il sito Web all'indirizzo https://suricata-ids.org/.</span><span class="sxs-lookup"><span data-stu-id="da838-109">For more details about Suricata and its capabilities, visit their website at https://suricata-ids.org/.</span></span>

## <a name="scenario"></a><span data-ttu-id="da838-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="da838-110">Scenario</span></span>

<span data-ttu-id="da838-111">Questo articolo illustra come configurare l'ambiente per eseguire il rilevamento di intrusioni di rete usando Network Watcher, Suricata ed Elastic Stack.</span><span class="sxs-lookup"><span data-stu-id="da838-111">This article explains how to set up your environment to perform network intrusion detection using Network Watcher, Suricata, and the Elastic Stack.</span></span> <span data-ttu-id="da838-112">Network Watcher fornisce le acquisizioni di pacchetti usate per eseguire il rilevamento di intrusioni di rete.</span><span class="sxs-lookup"><span data-stu-id="da838-112">Network Watcher provides you with the packet captures used to perform network intrusion detection.</span></span> <span data-ttu-id="da838-113">Suricata elabora le acquisizioni di pacchetti e attiva avvisi in base ai pacchetti che corrispondono ai set di regole specificati delle minacce.</span><span class="sxs-lookup"><span data-stu-id="da838-113">Suricata processes the packet captures and trigger alerts based on packets that match its given ruleset of threats.</span></span> <span data-ttu-id="da838-114">Questi avvisi vengono archiviati in un file di log nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="da838-114">These alerts are stored in a log file on your local machine.</span></span> <span data-ttu-id="da838-115">Usando Elastic Stack, i log generati da Suricata possono essere indicizzati e usati per creare un dashboard Kibana, che offre una rappresentazione visiva dei log e consente di comprendere rapidamente le potenziali vulnerabilità della rete.</span><span class="sxs-lookup"><span data-stu-id="da838-115">Using the Elastic Stack, the logs generated by Suricata can be indexed and used to create a Kibana dashboard, providing you with a visual representation of the logs and a means to quickly gain insights to potential network vulnerabilities.</span></span>  

![Scenario di applicazione Web semplice][1]

<span data-ttu-id="da838-117">Entrambi gli strumenti open source possono essere configurati in una VM di Azure, consentendo di eseguire questa analisi nell'ambiente di rete di Azure.</span><span class="sxs-lookup"><span data-stu-id="da838-117">Both open source tools can be set up on an Azure VM, allowing you to perform this analysis within your own Azure network environment.</span></span>

## <a name="steps"></a><span data-ttu-id="da838-118">Passi</span><span class="sxs-lookup"><span data-stu-id="da838-118">Steps</span></span>

### <a name="install-suricata"></a><span data-ttu-id="da838-119">Installare Suricata</span><span class="sxs-lookup"><span data-stu-id="da838-119">Install Suricata</span></span>

<span data-ttu-id="da838-120">Per tutti gli altri metodi di installazione, visitare http://suricata.readthedocs.io/en/latest/install.html</span><span class="sxs-lookup"><span data-stu-id="da838-120">For all other methods of installation, visit http://suricata.readthedocs.io/en/latest/install.html</span></span>

1. <span data-ttu-id="da838-121">Nel terminale della riga di comando della VM eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="da838-121">In the command-line terminal of your VM run the following commands:</span></span>

    ```
    sudo add-apt-repository ppa:oisf/suricata-stable
    sudo apt-get update
    sudo sudo apt-get install suricata
    ```

1. <span data-ttu-id="da838-122">Per verificare l'installazione, eseguire il comando `suricata -h` per visualizzare l'elenco completo di comandi.</span><span class="sxs-lookup"><span data-stu-id="da838-122">To verify your installation, run the command `suricata -h` to see the full list of commands.</span></span>

### <a name="download-the-emerging-threats-ruleset"></a><span data-ttu-id="da838-123">Scaricare il set di regole Emerging Threats</span><span class="sxs-lookup"><span data-stu-id="da838-123">Download the Emerging Threats ruleset</span></span>

<span data-ttu-id="da838-124">In questa fase, non sono disponibili regole per l'esecuzione di Suricata.</span><span class="sxs-lookup"><span data-stu-id="da838-124">At this stage, we do not have any rules for Suricata to run.</span></span> <span data-ttu-id="da838-125">È possibile creare le proprie regole se esistono minacce specifiche per la rete, che si vuole rilevare, oppure è possibile usare set di regole sviluppati di diversi provider, ad esempio Emerging Threats o le regole VRT di Snort.</span><span class="sxs-lookup"><span data-stu-id="da838-125">You can create your own rules if there are specific threats to your network you would like to detect, or you can also use developed rule sets from a number of providers, such as Emerging Threats, or VRT rules from Snort.</span></span> <span data-ttu-id="da838-126">Qui viene usato il set di regole Emerging Threats accessibile gratuitamente:</span><span class="sxs-lookup"><span data-stu-id="da838-126">We use the freely accessible Emerging Threats ruleset here:</span></span>

<span data-ttu-id="da838-127">Scaricare il set di regole e copiarle nella directory:</span><span class="sxs-lookup"><span data-stu-id="da838-127">Download the rule set and copy them into the directory:</span></span>

```
wget http://rules.emergingthreats.net/open/suricata/emerging.rules.tar.gz
tar zxf emerging.rules.tar.gz
sudo cp -r rules /etc/suricata/
```

### <a name="process-packet-captures-with-suricata"></a><span data-ttu-id="da838-128">Elaborare le acquisizioni di pacchetti con Suricata</span><span class="sxs-lookup"><span data-stu-id="da838-128">Process packet captures with Suricata</span></span>

<span data-ttu-id="da838-129">Per elaborare le acquisizioni di pacchetti usando Suricata, eseguire questo comando:</span><span class="sxs-lookup"><span data-stu-id="da838-129">To process packet captures using Suricata, run the following command:</span></span>

```
sudo suricata -c /etc/suricata/suricata.yaml -r <location_of_pcapfile>
```
<span data-ttu-id="da838-130">Per controllare gli avvisi risultanti, leggere il file fast.log:</span><span class="sxs-lookup"><span data-stu-id="da838-130">To check the resulting alerts, read the fast.log file:</span></span>
```
tail -f /var/log/suricata/fast.log
```

### <a name="set-up-the-elastic-stack"></a><span data-ttu-id="da838-131">Configurare Elastic Stack</span><span class="sxs-lookup"><span data-stu-id="da838-131">Set up the Elastic Stack</span></span>

<span data-ttu-id="da838-132">Anche se i log generati da Suricata contengono informazioni importanti su quanto avviene nella rete, la lettura e la comprensione di questi file di log non sono molto semplici.</span><span class="sxs-lookup"><span data-stu-id="da838-132">While the logs that Suricata produces contain valuable information about what’s happening on our network, these log files aren’t the easiest to read and understand.</span></span> <span data-ttu-id="da838-133">Connettendo Suricata con Elastic Stack, è possibile creare un dashboard Kibana che consente di cercare, creare grafici, analizzare e derivare informazioni dettagliate dai log.</span><span class="sxs-lookup"><span data-stu-id="da838-133">By connecting Suricata with the Elastic Stack, we can create a Kibana dashboard what allows us to search, graph, analyze, and derive insights from our logs.</span></span>

#### <a name="install-elasticsearch"></a><span data-ttu-id="da838-134">Installare Elasticsearch</span><span class="sxs-lookup"><span data-stu-id="da838-134">Install Elasticsearch</span></span>

1. <span data-ttu-id="da838-135">Elastic Stack versione 5.0 e successive richiede Java 8.</span><span class="sxs-lookup"><span data-stu-id="da838-135">The Elastic Stack from version 5.0 and above requires Java 8.</span></span> <span data-ttu-id="da838-136">Eseguire il comando `java -version` per controllare la versione in uso.</span><span class="sxs-lookup"><span data-stu-id="da838-136">Run the command `java -version` to check your version.</span></span> <span data-ttu-id="da838-137">Se Java non è installato, vedere la documentazione sul [sito Web Oracle](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span><span class="sxs-lookup"><span data-stu-id="da838-137">If you do not have java install, refer to documentation on [Oracle's website](http://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html)</span></span>
1. <span data-ttu-id="da838-138">Scaricare il pacchetto binario corretto per il proprio sistema:</span><span class="sxs-lookup"><span data-stu-id="da838-138">Download the correct binary package for your system:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.2.0.deb
    sudo dpkg -i elasticsearch-5.2.0.deb
    sudo /etc/init.d/elasticsearch start
    ```

    <span data-ttu-id="da838-139">Per altri metodi di installazione, vedere [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html) (Installazione di Elasticsearch)</span><span class="sxs-lookup"><span data-stu-id="da838-139">Other installation methods can be found at [Elasticsearch Installation](https://www.elastic.co/guide/en/beats/libbeat/5.2/elasticsearch-installation.html)</span></span>

1. <span data-ttu-id="da838-140">Verificare che Elasticsearch sia in esecuzione con questo comando:</span><span class="sxs-lookup"><span data-stu-id="da838-140">Verify that Elasticsearch is running with the command:</span></span>

    ```
    curl http://127.0.0.1:9200
    ```

    <span data-ttu-id="da838-141">La risposta visualizzata sarà simile a questa:</span><span class="sxs-lookup"><span data-stu-id="da838-141">You should see a response similar to this:</span></span>

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

<span data-ttu-id="da838-142">Per altre istruzioni sull'installazione di Elasticsearch, vedere la pagina [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html) (Installazione)</span><span class="sxs-lookup"><span data-stu-id="da838-142">For further instructions on installing Elastic search, refer to the page [Installation](https://www.elastic.co/guide/en/elasticsearch/reference/5.2/_installation.html)</span></span>

### <a name="install-logstash"></a><span data-ttu-id="da838-143">Installare Logstash</span><span class="sxs-lookup"><span data-stu-id="da838-143">Install Logstash</span></span>

1. <span data-ttu-id="da838-144">Per installare Logstash, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="da838-144">To install Logstash run the following commands:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/logstash/logstash-5.2.0.deb
    sudo dpkg -i logstash-5.2.0.deb
    ```
1. <span data-ttu-id="da838-145">Successivamente è necessario configurare Logstash per la lettura dall'output del file eve.json.</span><span class="sxs-lookup"><span data-stu-id="da838-145">Next we need to configure Logstash to read from the output of eve.json file.</span></span> <span data-ttu-id="da838-146">Creare un file logstash.conf usando:</span><span class="sxs-lookup"><span data-stu-id="da838-146">Create a logstash.conf file using:</span></span>

    ```
    sudo touch /etc/logstash/conf.d/logstash.conf
    ```

1. <span data-ttu-id="da838-147">Aggiungere il contenuto seguente al file (verificare che il percorso al file eve.json sia corretto):</span><span class="sxs-lookup"><span data-stu-id="da838-147">Add the following content to the file (make sure that the path to the eve.json file is correct):</span></span>

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

1. <span data-ttu-id="da838-148">Verificare di assegnare le autorizzazioni corrette al file eve.json in modo che Logstash possa inserire il file.</span><span class="sxs-lookup"><span data-stu-id="da838-148">Make sure to give the correct permissions to the eve.json file so that Logstash can ingest the file.</span></span>
    
    ```
    sudo chmod 775 /var/log/suricata/eve.json
    ```

1. <span data-ttu-id="da838-149">Per avviare Logstash, eseguire il comando:</span><span class="sxs-lookup"><span data-stu-id="da838-149">To start Logstash run the command:</span></span>

    ```
    sudo /etc/init.d/logstash start
    ```

<span data-ttu-id="da838-150">Per altre istruzioni sull'installazione di Logstash, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span><span class="sxs-lookup"><span data-stu-id="da838-150">For further instructions on installing Logstash, refer to the [official documentation](https://www.elastic.co/guide/en/beats/libbeat/5.2/logstash-installation.html)</span></span>

### <a name="install-kibana"></a><span data-ttu-id="da838-151">Installare Kibana</span><span class="sxs-lookup"><span data-stu-id="da838-151">Install Kibana</span></span>

1. <span data-ttu-id="da838-152">Eseguire questi comandi per installare Kibana:</span><span class="sxs-lookup"><span data-stu-id="da838-152">Run the following commands to install Kibana:</span></span>

    ```
    curl -L -O https://artifacts.elastic.co/downloads/kibana/kibana-5.2.0-linux-x86_64.tar.gz
    tar xzvf kibana-5.2.0-linux-x86_64.tar.gz

    ```
1. <span data-ttu-id="da838-153">Per eseguire Kibana, usare questi comandi:</span><span class="sxs-lookup"><span data-stu-id="da838-153">To run Kibana use the commands:</span></span>

    ```
    cd kibana-5.2.0-linux-x86_64/
    ./bin/kibana
    ```

1. <span data-ttu-id="da838-154">Per visualizzare l'interfaccia Web di Kibana, passare a `http://localhost:5601`</span><span class="sxs-lookup"><span data-stu-id="da838-154">To view your Kibana web interface, navigate to `http://localhost:5601`</span></span>
1. <span data-ttu-id="da838-155">Per questo scenario, il modello di indice usato per i log di Suricata è "logstash-*"</span><span class="sxs-lookup"><span data-stu-id="da838-155">For this scenario, the index pattern used for the Suricata logs is "logstash-*"</span></span>

1. <span data-ttu-id="da838-156">Per visualizzare il dashboard Kibana in remoto, creare una regola dei gruppi di sicurezza di rete in ingresso che consenta l'accesso alla **porta 5601**.</span><span class="sxs-lookup"><span data-stu-id="da838-156">If you want to view the Kibana dashboard remotely, create an inbound NSG rule allowing access to **port 5601**.</span></span>

### <a name="create-a-kibana-dashboard"></a><span data-ttu-id="da838-157">Creare un dashboard Kibana</span><span class="sxs-lookup"><span data-stu-id="da838-157">Create a Kibana dashboard</span></span>

<span data-ttu-id="da838-158">Per questo articolo, è stato fornito un dashboard di esempio per visualizzare tendenze e dettagli degli avvisi.</span><span class="sxs-lookup"><span data-stu-id="da838-158">For this article, we have provided a sample dashboard for you to view trends and details in your alerts.</span></span>

1. <span data-ttu-id="da838-159">Scaricare il file del dashboard [qui](https://aka.ms/networkwatchersuricatadashboard), il file di visualizzazione [qui](https://aka.ms/networkwatchersuricatavisualization) e il file della ricerca salvato [qui](https://aka.ms/networkwatchersuricatasavedsearch).</span><span class="sxs-lookup"><span data-stu-id="da838-159">Download the dashboard file [here](https://aka.ms/networkwatchersuricatadashboard), the visualization file [here](https://aka.ms/networkwatchersuricatavisualization), and the saved search file [here](https://aka.ms/networkwatchersuricatasavedsearch).</span></span>

1. <span data-ttu-id="da838-160">Nella scheda **Management** (Gestione) di Kibana passare a **Saved Objects** (Oggetti salvati) e importare tutti e tre i file.</span><span class="sxs-lookup"><span data-stu-id="da838-160">Under the **Management** tab of Kibana, navigate to **Saved Objects** and import all three files.</span></span> <span data-ttu-id="da838-161">Dalla scheda **Dashboard** è quindi possibile aprire e caricare il dashboard di esempio.</span><span class="sxs-lookup"><span data-stu-id="da838-161">Then from the **Dashboard** tab you can open and load the sample dashboard.</span></span>

<span data-ttu-id="da838-162">È anche possibile creare visualizzazioni e dashboard personalizzati per le metriche a cui si è interessati.</span><span class="sxs-lookup"><span data-stu-id="da838-162">You can also create your own visualizations and dashboards tailored towards metrics of your own interest.</span></span> <span data-ttu-id="da838-163">Per altre informazioni sulla creazione di visualizzazioni Kibana, vedere la [documentazione ufficiale](https://www.elastic.co/guide/en/kibana/current/visualize.html) di Kibana.</span><span class="sxs-lookup"><span data-stu-id="da838-163">Read more about creating Kibana visualizations from Kibana's [official documentation](https://www.elastic.co/guide/en/kibana/current/visualize.html).</span></span>

![Dashboard Kibana][2]

### <a name="visualize-ids-alert-logs"></a><span data-ttu-id="da838-165">Visualizzare i log di avvisi IDS</span><span class="sxs-lookup"><span data-stu-id="da838-165">Visualize IDS alert logs</span></span>

<span data-ttu-id="da838-166">Il dashboard di esempio offre diverse visualizzazioni dei log di avvisi di Suricata:</span><span class="sxs-lookup"><span data-stu-id="da838-166">The sample dashboard provides several visualizations of the Suricata alert logs:</span></span>

1. <span data-ttu-id="da838-167">Alerts by GeoIP (Avvisi per IP geografico): mappa che illustra la distribuzione degli avvisi per paese di origine in base alla località geografica (determinata dall'IP)</span><span class="sxs-lookup"><span data-stu-id="da838-167">Alerts by GeoIP – a map showing the distribution of alerts by their country of origin based on geographic location (determined by IP)</span></span>

    ![IP geografico][3]

1. <span data-ttu-id="da838-169">Top 10 Alerts (Primi 10 avvisi): riepilogo dei 10 avvisi attivati più di frequente e relativa descrizione.</span><span class="sxs-lookup"><span data-stu-id="da838-169">Top 10 Alerts – a summary of the 10 most frequent triggered alerts and their description.</span></span> <span data-ttu-id="da838-170">Facendo clic su un singolo avviso, si accede alle informazioni del dashboard relative a quell'avviso specifico.</span><span class="sxs-lookup"><span data-stu-id="da838-170">Clicking an individual alert filters down the dashboard to the information pertaining to that specific alert.</span></span>

    ![Immagine 4][4]

1. <span data-ttu-id="da838-172">Number of Alerts (Numero di avvisi): conteggio totale degli avvisi attivati dal set di regole</span><span class="sxs-lookup"><span data-stu-id="da838-172">Number of Alerts – the total count of alerts triggered by the ruleset</span></span>

    ![Immagine 5][5]

1. <span data-ttu-id="da838-174">Top 20 Source/Destination IPs/Ports (Primi 20 IP/porte di origine/destinazione): grafici a torta che illustrano i primi 20 IP e porte in cui sono stati attivati avvisi.</span><span class="sxs-lookup"><span data-stu-id="da838-174">Top 20 Source/Destination IPs/Ports - pie charts showing the top 20 IPs and ports that alerts were triggered on.</span></span> <span data-ttu-id="da838-175">È possibile filtrare specifici IP/porte per visualizzare quanti avvisi e di quale tipo sono stati attivati.</span><span class="sxs-lookup"><span data-stu-id="da838-175">You can filter down on specific IPs/ports to see how many and what kind of alerts are being triggered.</span></span>

    ![Immagine 6][6]

1. <span data-ttu-id="da838-177">Alert Summary (Riepilogo avvisi): tabella che riepiloga specifici dettagli di ogni singolo avviso.</span><span class="sxs-lookup"><span data-stu-id="da838-177">Alert Summary – a table summarizing specific details of each individual alert.</span></span> <span data-ttu-id="da838-178">È possibile personalizzare questa tabella per visualizzare altri parametri di interesse per ogni avviso.</span><span class="sxs-lookup"><span data-stu-id="da838-178">You can customize this table to show other parameters of interest for each alert.</span></span>

    ![Immagine 7][7]

<span data-ttu-id="da838-180">Per altri documenti sulla creazione di visualizzazioni e dashboard personalizzati, vedere la [documentazione ufficiale di Kibana](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span><span class="sxs-lookup"><span data-stu-id="da838-180">For more documentation on creating custom visualizations and dashboards, see [Kibana’s official documentation](https://www.elastic.co/guide/en/kibana/current/introduction.html).</span></span>

## <a name="conclusion"></a><span data-ttu-id="da838-181">Conclusione</span><span class="sxs-lookup"><span data-stu-id="da838-181">Conclusion</span></span>

<span data-ttu-id="da838-182">Combinando le acquisizioni di pacchetti fornite da Network Watcher e da strumenti IDS open source come Suricata, è possibile eseguire il rilevamento di intrusioni di rete per svariate minacce.</span><span class="sxs-lookup"><span data-stu-id="da838-182">By combining packet captures provided by Network Watcher and open source IDS tools such as Suricata, you can perform network intrusion detection for a wide range of threats.</span></span> <span data-ttu-id="da838-183">Questi dashboard consentono di trovare rapidamente tendenze e anomalie nella rete, oltre che esaminare i dati per trovare le cause radice degli avvisi, ad esempio agenti utenti malintenzionati o porte vulnerabili.</span><span class="sxs-lookup"><span data-stu-id="da838-183">These dashboards allow you to quickly spot trends and anomalies within your network, as well dig into the data to discover root causes of alerts such as malicious user agents or vulnerable ports.</span></span> <span data-ttu-id="da838-184">Con i dati estratti, è possibile prendere decisioni informate su come reagire e proteggere la rete da qualsiasi tentativo di intrusione dannoso e creare regole per impedire intrusioni future nella rete.</span><span class="sxs-lookup"><span data-stu-id="da838-184">With this extracted data, you can make informed decisions on how to react to and protect your network from any harmful intrusion attempts, and create rules to prevent future intrusions to your network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da838-185">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="da838-185">Next steps</span></span>

<span data-ttu-id="da838-186">Per informazioni su come attivare le acquisizioni di pacchetti in base agli avvisi, vedere [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md) (Usare l'acquisizione di pacchetti per eseguire il monitoraggio proattivo della rete con Funzioni di Azure)</span><span class="sxs-lookup"><span data-stu-id="da838-186">Learn how to trigger packet captures based on alerts by visiting [Use packet capture to do proactive network monitoring with Azure Functions](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="da838-187">Per informazioni su come visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI, vedere [Visualizzare i log dei flussi dei gruppi di sicurezza di rete con Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span><span class="sxs-lookup"><span data-stu-id="da838-187">Learn how to visualize your NSG flow logs with Power BI by visiting [Visualize NSG flows logs with Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md)</span></span>



<!-- images -->
[1]: ./media/network-watcher-intrusion-detection-open-source-tools/figure1.png
[2]: ./media/network-watcher-intrusion-detection-open-source-tools/figure2.png
[3]: ./media/network-watcher-intrusion-detection-open-source-tools/figure3.png
[4]: ./media/network-watcher-intrusion-detection-open-source-tools/figure4.png
[5]: ./media/network-watcher-intrusion-detection-open-source-tools/figure5.png
[6]: ./media/network-watcher-intrusion-detection-open-source-tools/figure6.png
[7]: ./media/network-watcher-intrusion-detection-open-source-tools/figure7.png
