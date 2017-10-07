---
title: lo sviluppo dell'azione aaaScript con HDInsight basati su Linux - Azure | Documenti Microsoft
description: "Informazioni su come generare script per i cluster HDInsight basati su Linux toocustomize toouse Bash. Hello script azione di HDInsight consente toorun script durante o dopo la creazione del cluster. Gli script è possibile toochange utilizzate le impostazioni di configurazione del cluster o installare software aggiuntivo."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Sviluppo di azioni script con HDInsight

Informazioni su come è il cluster HDInsight tramite Bash toocustomize script. Le azioni script sono toocustomize un modo HDInsight durante o dopo la creazione del cluster.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-are-script-actions"></a>Definizione di azioni script

Le azioni script sono gli script Bash Azure viene eseguito sulle modifiche di configurazione toomake nodi cluster hello o installare software. Un'azione di script viene eseguita come radice e fornisce i nodi del cluster toohello diritti di accesso completo.

Le azioni script possono essere applicate tramite hello dei seguenti metodi:

| Utilizzare questo tooapply metodo uno script... | Durante la creazione di un cluster... | In un cluster in esecuzione... |
| --- |:---:|:---:|
| Portale di Azure |✓  |✓ |
| Azure PowerShell |✓ |✓ |
| Interfaccia della riga di comando di Azure |&nbsp; |✓ |
| HDInsight .NET SDK |✓ |✓ |
| Modello di Azure Resource Manager |✓ |&nbsp; |

Per ulteriori informazioni sull'utilizzo di questi script azione tooapply metodi, vedere [HDInsight personalizzare cluster tramite le azioni script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Procedure consigliate per lo sviluppo di script

Quando si sviluppa uno script personalizzato per un cluster HDInsight, sono disponibili diverse procedure tookeep di procedure consigliate in considerazione:

* [Versione di destinazione hello Hadoop](#bPS1)
* [Hello versione del sistema operativo di destinazione](#bps10)
* [Fornire stabile collega tooscript risorse](#bPS2)
* [Usare risorse precompilate](#bPS4)
* [Verificare che uno script di personalizzazione cluster hello è idempotente](#bPS3)
* [Verificare la disponibilità elevata dell'architettura di cluster hello](#bPS5)
* [Configurare l'archiviazione Blob di Azure toouse componenti personalizzati di hello](#bPS6)
* [Scrivere informazioni tooSTDOUT e STDERR](#bPS7)
* [Salvare i file in formato ASCII con terminazioni di riga LF](#bps8)
* [Utilizzare toorecover logica di tentativi di errori temporanei](#bps9)

> [!IMPORTANT]
> Le azioni script devono essere completate entro 60 minuti o hello processo avrà esito negativo. Durante il provisioning del nodo, script di hello viene eseguito contemporaneamente ad altri processi di installazione e configurazione. Contesa per le risorse, ad esempio larghezza di banda della CPU ora o di rete potrebbe essere hello script tootake più toofinish rispetto a quello usato nell'ambiente di sviluppo.

### <a name="bPS1"></a>Versione di destinazione hello Hadoop

Nelle diverse versioni di HDInsight sono installate versioni diverse di servizi e componenti di Hadoop. Se lo script prevede una versione specifica di un servizio o componente, è necessario utilizzare solo script di hello con la versione di hello di HDInsight che include i componenti necessario di hello. È possibile trovare informazioni sulle versioni dei componenti inclusi in HDInsight usando hello [il controllo delle versioni di HDInsight componente](hdinsight-component-versioning.md) documento.

### <a name="bps10"></a>Versione di hello del sistema operativo di destinazione

HDInsight basati su Linux si basa su hello distribuzione Ubuntu Linux. Versioni diverse di HDInsight si basano su versioni differenti di Ubuntu e questo può influire sul comportamento dello script. HDInsight 3.4 e versioni precedenti si basano ad esempio su versioni di Ubuntu che usano Upstart. La versione 3.5 si basa su Ubuntu 16.04 che usa Systemd. Systemd e Upstart si basano sui diversi comandi, in modo che lo script deve essere scritto toowork con entrambi.

Un'altra differenza importante tra 3.4 HDInsight e 3.5 è che `JAVA_HOME` punti ora tooJava 8.

È possibile controllare la versione del sistema operativo hello utilizzando `lsb_release`. Hello codice seguente viene illustrato come toodetermine se hello script è in esecuzione in Ubuntu 14 o 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

È possibile trovare uno script completo di hello contenente questi frammenti di codice in https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

La versione di hello di Ubuntu utilizzato da HDInsight, vedere hello [la versione del componente HDInsight](hdinsight-component-versioning.md) documento.

differenze di hello toounderstand tra Systemd e Upstart, vedere [Systemd per gli utenti Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Fornire stabile collega tooscript risorse

Hello script e le risorse associate devono rimanere disponibile per tutta la durata di hello del cluster di hello. Queste risorse sono necessarie se vengono aggiunti nuovi nodi cluster toohello durante le operazioni di ridimensionamento.

procedura consigliata Hello è toodownload e archiviare tutti gli elementi di un account di archiviazione di Azure nella sottoscrizione.

> [!IMPORTANT]
> account di archiviazione Hello usato deve essere l'account di archiviazione predefinito hello per cluster hello o un contenitore di sola lettura pubblico su qualsiasi altro account di archiviazione.

Ad esempio, gli esempi di hello forniti da Microsoft vengono archiviati in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) account di archiviazione. Si tratta di un contenitore di sola lettura pubblico gestito dal team di HDInsight hello.

### <a name="bPS4"></a>Usare risorse precompilate

hello tooreduce tempo accetta toorun hello script, evitare operazioni di compilazione risorse dal codice sorgente. Ad esempio, la precompilazione risorse e archiviarli in un blob dell'account di archiviazione di Azure in hello stesso data center in HDInsight.

### <a name="bPS3"></a>Verificare che uno script di personalizzazione cluster hello è idempotente

Gli script devono essere idempotenti. Se viene eseguito più volte di script di hello, dovrebbe restituire hello toohello cluster stesso stato di ogni volta.

Uno script che modifica i file di configurazione, ad esempio, non deve aggiungere voci duplicate se viene eseguito più volte.

### <a name="bPS5"></a>Verificare la disponibilità elevata dell'architettura di cluster hello

Cluster HDInsight basati su Linux forniscono due nodi head attivi all'interno di cluster hello e le azioni di script vengono eseguite in entrambi i nodi. Se si installa i componenti di hello prevedono un solo nodo head, non installare i componenti di hello in entrambi i nodi head.

> [!IMPORTANT]
> Fornito come parte di HDInsight sono servizi toofail progettato tra due nodi head di hello in base alle esigenze. Questa funzionalità non viene estesa toocustom componenti installati tramite le azioni script. Se i componenti personalizzati richiedono una disponibilità elevata, è necessario implementare un meccanismo di failover personalizzato.

### <a name="bPS6"></a>Configurare l'archiviazione Blob di Azure toouse componenti personalizzati di hello

I componenti da installare nel cluster hello potrebbero essere una configurazione predefinita che utilizza l'archiviazione di Hadoop Distributed File System (HDFS). HDInsight Usa archiviazione di Azure o archivio Data Lake come spazio di archiviazione predefinito hello. Forniscono entrambi un sistema compatibile file HDFS che mantiene i dati anche se hello cluster verrà eliminato. Potrebbe essere necessario tooconfigure componenti installati toouse WASB o ADL anziché HDFS.

Per la maggior parte delle operazioni, non è necessario del sistema di file hello toospecify. Ad esempio, seguente hello copia file giraph examples.jar hello dalla hello archivio locale del sistema toocluster dei file:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

In questo esempio hello `hdfs` comando utilizza in modo trasparente l'archiviazione del cluster predefinito hello. Per alcune operazioni, potrebbe essere necessario toospecify hello URI. ad esempio `adl:///example/jars` per Data Lake Store o `wasb:///example/jars` per l'archiviazione di Azure.

### <a name="bPS7"></a>Scrivere informazioni tooSTDOUT e STDERR

HDInsight registra l'output dello script che viene scritto tooSTDOUT e STDERR. È possibile visualizzare queste informazioni tramite interfaccia utente di hello Ambari web.

> [!NOTE]
> Ambari è disponibile solo se il cluster hello è stato creato. Se si utilizza un'azione di script durante la creazione del cluster e non viene completata la creazione, vedere Risoluzione dei problemi di sezione hello [HDInsight personalizzare cluster utilizzando l'azione script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) per altre modalità di accesso alle informazioni registrate.

La maggior parte delle utilità e pacchetti di installazione già scrivono informazioni tooSTDOUT e STDERR, tuttavia è opportuno tooadd ulteriori opzioni di registrazione. toosend testo tooSTDOUT, utilizzare `echo`. ad esempio:

```bash
echo "Getting ready tooinstall Foo"
```

Per impostazione predefinita, `echo` invia hello tooSTDOUT stringa. toodirect è tooSTDERR, aggiungere `>&2` prima `echo`. ad esempio:

```bash
>&2 echo "An error occurred installing Foo"
```

Consente di reindirizzare le informazioni scritte invece tooSTDOUT tooSTDERR (2). Per altre informazioni sul reindirizzamento I/O, vedere [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Per altre informazioni sulla visualizzazione delle informazioni registrate tramite azioni script, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a> Salvare i file in formato ASCII con terminazioni di riga LF

Gli script Bash devono essere archiviati nel formato ASCII con righe terminate da LF. I file vengono archiviati come UTF-8 o utilizzano CRLF come terminazione di riga hello potrebbero non riuscire con hello errore seguente:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Utilizzare toorecover logica di tentativi di errori temporanei

Quando si scaricano file, l'installazione dei pacchetti tramite apt get o altre azioni che trasmettono dati su internet hello, azione hello potrebbe non riuscire a causa di errori di rete tootransient. Ad esempio, si sta comunicando con la risorsa remota hello sia nel processo di hello del failover sul nodo backup tooa.

toomake gli errori di tootransient resilienti script, è possibile implementare la logica di ripetizione. Hello che segue viene illustrato come la logica di riesecuzione tooimplement. Eseguire un nuovo tentativo operazione hello tre volte prima che si verifichi.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Hello esempi seguenti illustrano come toouse questa funzione.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Metodi helper per gli script personalizzati

I metodi helper dell'azione script sono utilità che è possibile usare durante la scrittura di script personalizzati. Questi metodi sono contenuti nello script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh). Utilizzare hello seguente toodownload e utilizzarle come parte dello script:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Hello helper disponibili per l'utilizzo nello script seguente:

| Utilizzo dell'helper | Descrizione |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Scarica un file dal percorso del file specificato toohello hello origine URI. Per impostazione predefinita, non sovrascrive un file esistente. |
| `untar_file TARFILE DESTDIR` |Estrae un file con estensione tar (utilizzando `-xf`) toohello directory di destinazione. |
| `test_is_headnode` |Se viene eseguito su un nodo head del cluster restituisce 1; in caso contrario, 0. |
| `test_is_datanode` |Se il nodo corrente hello è un nodo di dati (lavoratore), restituisce 1; in caso contrario, 0. |
| `test_is_first_datanode` |Se il nodo corrente di hello è hello innanzitutto i dati (lavoratore) nodo (denominata workernode0) restituisce 1; in caso contrario, 0. |
| `get_headnodes` |Restituisce il nome di dominio completo hello di hello headnodes cluster hello. I nomi sono delimitati da virgole. In caso di errore, viene restituita una stringa vuota. |
| `get_primary_headnode` |Ottiene il nome di dominio completo hello del nodo head primario hello. In caso di errore, viene restituita una stringa vuota. |
| `get_secondary_headnode` |Ottiene il nome di dominio completo hello del nodo head secondario hello. In caso di errore, viene restituita una stringa vuota. |
| `get_primary_headnode_number` |Ottiene hello suffisso numerico del nodo head primario hello. In caso di errore, viene restituita una stringa vuota. |
| `get_secondary_headnode_number` |Ottiene hello suffisso numerico del nodo head secondario hello. In caso di errore, viene restituita una stringa vuota. |

## <a name="commonusage"></a>Modelli di utilizzo comuni

Questa sezione vengono fornite informazioni aggiuntive sull'implementazione di alcuni dei modelli di utilizzo comuni hello che potrebbero essere generati durante la scrittura di script personalizzato.

### <a name="passing-parameters-tooa-script"></a>Passaggio di parametri script tooa

In alcuni casi, lo script potrebbe richiedere l'uso di parametri. Ad esempio, potrebbe essere la password di amministratore di hello per cluster hello quando si utilizza l'API REST Ambari hello.

I parametri passati toohello script sono note come *parametri posizionali*e sono assegnati troppo`$1` per primo parametro hello, `$2` per hello secondo e pertanto-on. `$0`contiene il nome di hello dello script hello stesso.

Valori passati toohello script come parametri devono essere racchiusi tra virgolette singole ('). In modo da garantire che hello passato valore viene considerato come un valore letterale.

### <a name="setting-environment-variables"></a>Impostazioni delle variabili di ambiente

L'impostazione di una variabile di ambiente viene eseguita dall'istruzione hello:

    VARIABLENAME=value

Dove nomevariabile è il nome di hello della variabile hello. uso delle variabili, hello tooaccess `$VARIABLENAME`. Ad esempio, tooassign un valore fornito da un parametro posizionale come una variabile di ambiente denominata PASSWORD, si utilizzerebbe hello seguente istruzione:

    PASSWORD=$1

Quindi è possibile utilizzare le informazioni di accesso successivo toohello `$PASSWORD`.

Variabili di ambiente impostate all'interno dello script hello esistono solo nell'ambito di hello dello script hello. In alcuni casi, potrebbe essere variabili di ambiente a livello di sistema tooadd che rimarrà termine script hello. variabili di ambiente a livello di sistema tooadd, aggiungere la variabile hello troppo`/etc/environment`. Ad esempio, hello istruzione aggiunge `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Accesso toolocations in cui sono archiviati gli script personalizzati hello

Script utilizzati toocustomize un cluster deve toobe archiviati in una delle posizioni seguenti hello:

* Un __account di archiviazione Azure__ associato al cluster hello.

* Un __account di archiviazione aggiuntivo__ associato hello cluster.

* __URI leggibile pubblicamente__, Ad esempio, un URL toodata archiviato in OneDrive, Dropbox o altri file di servizio di hosting.

* Un __account archivio Azure Data Lake__ associato al cluster HDInsight hello. Per altre informazioni sull'uso di Azure Data Lake Store con HDInsight, vedere [Creare un cluster HDInsight con Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Hello servizio principale HDInsight utilizza tooaccess archivio Data Lake deve avere accesso in lettura toohello script.

Le risorse utilizzate dallo script hello devono essere disponibile pubblicamente.

Archiviazione dei file hello in un account di archiviazione di Azure o l'archivio Azure Data Lake fornisce accesso veloce, sia all'interno di hello rete di Azure.

> [!NOTE]
> Hello URI formato utilizzato tooreference hello script varia a seconda del servizio hello in uso. Per gli account di archiviazione associati al cluster HDInsight hello, utilizzare `wasb://` o `wasbs://`. Per gli URI leggibili pubblicamente, usare `http://` o `https://`. Per Data Lake Store, usare `adl://`.

### <a name="checking-hello-operating-system-version"></a>Controllo della versione del sistema operativo hello

Le diverse versioni di HDInsight si basano su versioni specifiche di Ubuntu. Ci possono essere differenze tra le versioni del sistema operativo che è necessario verificare nello script. Ad esempio, potrebbe essere necessario un file binario che è toohello legati versione Ubuntu tooinstall.

versione del sistema operativo hello toocheck, utilizzare `lsb_release`. Ad esempio, hello lo script seguente viene illustrato come tooreference un specifico tar file a seconda della versione del sistema operativo hello:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Elenco di controllo per la distribuzione di un'azione script

Ecco i passaggi di hello effettuati durante la preparazione di questi script toodeploy:

* Inserire i file hello che contengono gli script personalizzati hello in una posizione accessibile dai nodi di cluster hello durante la distribuzione. Ad esempio, hello archivio predefinito per il cluster hello. I file possono essere archiviati anche in servizi di hosting leggibili pubblicamente.
* Verificare che sia impotent script hello. In questo modo possono hello script toobe eseguita più volte su hello stesso nodo.
* Utilizzare hello di tookeep un file temporaneo directory /tmp scaricato i file utilizzati dagli script hello e quindi li elimina dopo aver eseguito gli script.
* Se vengono modificati le impostazioni a livello del sistema operativo o i file di configurazione del servizio di Hadoop, è consigliabile toorestart HDInsight servizi.

## <a name="runScriptAction"></a>Come toorun un'azione di script

È possibile utilizzare script azioni toocustomize dei cluster HDInsight con hello dei seguenti metodi:

* Portale di Azure
* Azure PowerShell
* Modelli di Gestione risorse di Azure
* Hello HDInsight .NET SDK.

Per ulteriori informazioni sull'utilizzo di ogni metodo, vedere [come toouse script azione](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Esempi di script personalizzati

Microsoft fornisce gli script di esempio tooinstall componenti in un cluster HDInsight. Vedere i seguenti collegamenti per ulteriori azioni di script di esempio hello.

* [Installare e usare Hue nei cluster HDInsight.](hdinsight-hadoop-hue-linux.md)
* [Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Installare o aggiornare Mono nei cluster HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Risoluzione dei problemi

di seguito Hello sono errori che possono verificarsi quando si usano script che è stato sviluppato.

**Errore**: `$'\r': command not found`. A volte seguito da `syntax error: unexpected end of file`.

*Causa*: questo errore si verifica quando le righe di hello in uno script di terminano con CR/LF. Sistemi UNIX prevedono solo LF come terminazione di riga hello.

Questo problema più si verifica spesso quando è stato creato in un ambiente Windows script hello CRLF è una linea comune che termina per molti editor di testo in Windows.

*Risoluzione*: se è un'opzione nell'editor di testo, selezionare il formato Unix o LF per terminazioni di riga hello. È inoltre possibile utilizzare i seguenti comandi in un tooan CRLF Unix system toochange hello LF hello:

> [!NOTE]
> Hello comandi riportati di seguito sono quasi equivalenti che deve essere cambiata tooLF terminazioni riga CRLF di hello. Selezionare una basata sull'utilità hello disponibili nel sistema.

| Comando | Note |
| --- | --- |
| `unix2dos -b INFILE` |il file originale di Hello viene eseguito il backup con una. Estensione BAK |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE contiene una versione solo con le terminazioni LF |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Modifica direttamente il file hello |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE contiene una versione solo con le terminazioni LF. |

**Errore**: `line 1: #!/usr/bin/env: No such file or directory`.

*Causa*: questo errore si verifica quando hello script è stato salvato come UTF-8 con un provider di servizi Internet (BOM, Byte Order Mark).

*Risoluzione*: Save hello file come ASCII, oppure come UTF-8 senza una distinta base. È inoltre possibile utilizzare hello comando seguente in un toocreate sistema un file senza hello DBA Linux o Unix:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Sostituire `INFILE` con file hello contenente hello DBA. `OUTFILE`deve essere un nuovo nome di file, che contiene lo script hello senza hello DBA.

## <a name="seeAlso"></a>Passaggi successivi

* Informazioni su come troppo[personalizzare HDInsight cluster mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md)
* Hello utilizzare [riferimento HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx) toolearn ulteriori informazioni sulla creazione di applicazioni .NET che gestire HDInsight
* Hello utilizzare [API REST di HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn come cluster di azioni di gestione di toouse REST tooperform in HDInsight.
