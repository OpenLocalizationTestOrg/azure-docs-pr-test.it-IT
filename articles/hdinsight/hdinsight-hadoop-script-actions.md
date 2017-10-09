---
title: lo sviluppo dell'azione con HDInsight - Azure aaaScript | Documenti Microsoft
description: "Informazioni su come toocustomize Hadoop cluster con azione di Script. Genera script azione può essere utilizzato tooinstall software aggiuntivo in esecuzione in una configurazione di hello cluster o toochange Hadoop delle applicazioni installate in un cluster."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 836d68a8-8b21-4d69-8b61-281a7fe67f21
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4fc3a389df8a003f7129ab00b4cd9bc7ad81a419
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-script-action-scripts-for-hdinsight-windows-based-clusters"></a>Sviluppare script di Azione script per HDInsight nei cluster basati su Windows
Informazioni su come toowrite genera Script azione gli script per HDInsight. Per informazioni sull'uso di script di Azione script, vedere [Personalizzare cluster HDInsight mediante Azione script](hdinsight-hadoop-customize-cluster.md). Per hello stesso articolo scritto per i cluster HDInsight basati su Linux, vedere [script sviluppare genera Script azione per HDInsight](hdinsight-hadoop-script-actions-linux.md).



> [!IMPORTANT]
> Hello passaggi sono disponibili solo in questo documento per i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per informazioni sull'uso di azioni script con cluster basati su Linux, vedere [Sviluppo di azioni script con HDInsight (Linux)](hdinsight-hadoop-script-actions-linux.md).
>
>



Genera script azione può essere utilizzato tooinstall software aggiuntivo in esecuzione in una configurazione di hello cluster o toochange Hadoop delle applicazioni installate in un cluster. Le azioni script sono gli script da eseguire sui nodi del cluster di hello quando si distribuiscono cluster HDInsight e vengono eseguiti una volta che i nodi cluster hello completare la configurazione di HDInsight. Un'azione di script viene eseguita con privilegi di account amministratore di sistema e fornisce i diritti di accesso completi toohello i nodi del cluster. Ogni cluster può essere fornito con un elenco di toobe azioni script eseguiti in ordine di hello in cui sono state specificate.

> [!NOTE]
> Se si verifica hello seguente messaggio di errore:
>
> System.Management.Automation.CommandNotFoundException; ExceptionMessage: hello termine 'Salva HDIFile' non è riconosciuto come nome hello di un cmdlet, funzione, file di script o programma eseguibile. Il controllo ortografico hello del nome di hello, o se è stato incluso un percorso, verificare che il percorso hello sia corretto e riprovare.
> È perché non inclusi metodi helper hello.  Vedere [Metodi helper per gli script personalizzati](hdinsight-hadoop-script-actions.md#helper-methods-for-custom-scripts).
>
>

## <a name="sample-scripts"></a>Script di esempio
Per la creazione di cluster HDInsight nel sistema operativo Windows, hello azione Script è uno script di PowerShell di Azure. Hello script riportato di seguito è riportato un esempio per la configurazione del file di configurazione del sito hello:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    param (
        [parameter(Mandatory)][string] $ConfigFileName,
        [parameter(Mandatory)][string] $Name,
        [parameter(Mandatory)][string] $Value,
        [parameter()][string] $Description
    )

    if (!$Description) {
        $Description = ""
    }

    $hdiConfigFiles = @{
        "hive-site.xml" = "$env:HIVE_HOME\conf\hive-site.xml";
        "core-site.xml" = "$env:HADOOP_HOME\etc\hadoop\core-site.xml";
        "hdfs-site.xml" = "$env:HADOOP_HOME\etc\hadoop\hdfs-site.xml";
        "mapred-site.xml" = "$env:HADOOP_HOME\etc\hadoop\mapred-site.xml";
        "yarn-site.xml" = "$env:HADOOP_HOME\etc\hadoop\yarn-site.xml"
    }

    if (!($hdiConfigFiles[$ConfigFileName])) {
        Write-HDILog "Unable tooconfigure $ConfigFileName because it is not part of hello HDI configuration files."
        return
    }

    [xml]$configFile = Get-Content $hdiConfigFiles[$ConfigFileName]

    $existingproperty = $configFile.configuration.property | where {$_.Name -eq $Name}

    if ($existingproperty) {
        $existingproperty.Value = $Value
        $existingproperty.Description = $Description
    } else {
        $newproperty = @($configFile.configuration.property)[0].Clone()
        $newproperty.Name = $Name
        $newproperty.Value = $Value
        $newproperty.Description = $Description
        $configFile.configuration.AppendChild($newproperty)
    }

    $configFile.Save($hdiConfigFiles[$ConfigFileName])

    Write-HDILog "$configFileName has been configured."

script di Hello accetta quattro parametri, un nome di file di configurazione di hello, hello la proprietà toomodify, il valore di hello desiderato tooset e una descrizione. ad esempio:

    hive-site.xml hive.metastore.client.socket.timeout 90

Questi parametri imposta hello hive.metastore.client.socket.timeout valore too90 nel file hive-Site.XML hello.  valore predefinito di Hello è 60 secondi.

Lo script di esempio è disponibile anche all'indirizzo [https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1](https://hditutorialdata.blob.core.windows.net/customizecluster/editSiteConfig.ps1).

HDInsight disponibili alcuni script di componenti aggiuntivi tooinstall nei cluster HDInsight:

| Nome | Script |
| --- | --- |
| **Installare Spark** |https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1. Vedere [Installare e usare Spark in cluster Hadoop di HDInsight][hdinsight-install-spark]. |
| **Installare R** |https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1. Vedere [Installare e usare R nei cluster HDInsight][hdinsight-r-scripts]. |
| **Installare Solr** |https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1. Vedere [Installare e usare Solr nei cluster Hadoop di HDInsight](hdinsight-hadoop-solr-install.md). |
| - **Installare Giraph** |https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1. Vedere [Installare Giraph nei cluster HDInsight Hadoop](hdinsight-hadoop-giraph-install.md). |

Genera script azione può essere distribuite da hello portale di Azure, Azure PowerShell o utilizzando hello HDInsight .NET SDK.  Per altre informazioni, vedere [Personalizzare cluster HDInsight mediante l'azione script][hdinsight-cluster-customize].

> [!NOTE]
> script di esempio Hello funziona solo con una versione del cluster HDInsight 3.1 o successiva. Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).
>
>

## <a name="helper-methods-for-custom-scripts"></a>Metodi helper per gli script personalizzati
I metodi di supporto di Azione script sono utilità che è possibile usare durante la scrittura di script personalizzati. Questi metodi sono definiti in [https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1](https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1)e possono essere inclusi negli script utilizzando hello seguente esempio:

    # Download config action module from a well-known directory.
    $CONFIGACTIONURI = "https://hdiconfigactions.blob.core.windows.net/configactionmodulev05/HDInsightUtilities-v05.psm1";
    $CONFIGACTIONMODULE = "C:\apps\dist\HDInsightUtilities.psm1";
    $webclient = New-Object System.Net.WebClient;
    $webclient.DownloadFile($CONFIGACTIONURI, $CONFIGACTIONMODULE);

    # (TIP) Import config action helper method module toomake writing config action easy.
    if (Test-Path ($CONFIGACTIONMODULE))
    {
        Import-Module $CONFIGACTIONMODULE;
    }
    else
    {
        Write-Output "Failed tooload HDInsightUtilities module, exiting ...";
        exit;
    }

Di seguito sono metodi di supporto hello forniti da questo script:

| Metodo helper | Descrizione |
| --- | --- |
| **Save-HDIFile** |Scaricare un file da hello specificato percorso tooa identificatore URI (Uniform Resource) sul disco locale hello associato al cluster di hello Azure VM nodi toohello assegnato. |
| **Expand-HDIZippedFile** |Decomprimere un file compresso. |
| **Invoke-HDICmdScript** |Eseguire uno script da cmd.exe. |
| **Write-HDILog** |Scrivere l'output dello script di hello personalizzato utilizzato per un'azione di script. |
| **Get-Services** |Ottenere un elenco dei servizi in esecuzione nel computer di hello in cui viene eseguito uno script hello. |
| **Get-Service** |Nome del servizio specifico hello come input, di ottenere informazioni dettagliate per un servizio specifico (nome del servizio, ID processo, lo stato e così via) nel computer di hello in cui viene eseguito uno script hello. |
| **Get-HDIServices** |Ottenere un elenco dei servizi HDInsight in esecuzione nel computer di hello in cui viene eseguito uno script hello. |
| **Get-HDIService** |Hello HDInsight servizio nome specifico come input, di ottenere informazioni dettagliate per un servizio specifico (nome del servizio, ID processo, lo stato e così via) nel computer di hello in cui viene eseguito uno script hello. |
| **Get-ServicesRunning** |Ottenere un elenco di servizi in esecuzione nel computer di hello in cui viene eseguito uno script hello. |
| **Get-ServiceRunning** |Controllare se un servizio specifico (per nome) è in esecuzione nel computer di hello in cui viene eseguito uno script hello. |
| **Get-HDIServicesRunning** |Ottenere un elenco dei servizi HDInsight in esecuzione nel computer di hello in cui viene eseguito uno script hello. |
| **Get-HDIServiceRunning** |Controllare se un servizio HDInsight specifico (per nome) è in esecuzione nel computer di hello in cui viene eseguito uno script hello. |
| **Get-HDIHadoopVersion** |Ottenere la versione di hello Hadoop installato nel computer di hello in cui viene eseguito uno script hello. |
| **Test-IsHDIHeadNode** |Verificare se il computer di hello in cui viene eseguito uno script hello è un nodo head. |
| **Test-IsActiveHDIHeadNode** |Verificare se il computer di hello in cui viene eseguito uno script hello è un nodo head attivo. |
| **Test-IsHDIDataNode** |Verificare se il computer di hello in cui viene eseguito uno script hello è un nodo di dati. |
| **Edit-HDIConfigFile** |Modificare hello config file hive-Site.XML, Core-Site.XML, hdfs-Site.XML, mapred-Site.XML o yarn-Site.Xml. |

## <a name="best-practices-for-script-development"></a>Procedure consigliate per lo sviluppo di script
Quando si sviluppa uno script personalizzato per un cluster HDInsight, sono disponibili diverse procedure tookeep di procedure consigliate in considerazione:

* Controllo per la versione di Hadoop hello

    Solo HDInsight versione 3.1 (Hadoop 2.4) e versioni successive supportano utilizzando i componenti personalizzati di tooinstall genera Script azione in un cluster. Nello script personalizzato, è necessario utilizzare hello **Get HDIHadoopVersion** helper metodo toocheck hello versione di Hadoop prima di procedere con l'esecuzione di altre attività nello script hello.
* Fornire stabile collega tooscript risorse

    Gli utenti devono assicurarsi che tutti gli script hello e altri artefatti usati in hello personalizzazione di un cluster rimangono disponibili per tutta la durata di hello del cluster hello e che le versioni di hello di questi file non cambiano per durata hello. Queste risorse sono necessarie se hello ricreando le immagini dei nodi nel cluster hello è obbligatorio. procedura consigliata Hello è toodownload e archiviare tutti gli elementi di un account di archiviazione che hello controlli utente. Può trattarsi di account di archiviazione predefinito hello o qualsiasi hello aggiuntive di account di archiviazione specificato in fase di hello di distribuzione per un cluster personalizzato.
    In hello Spark e R personalizzati esempi cluster fornite nella documentazione di hello, ad esempio, è stata introdotta una copia locale di risorse hello questo account di archiviazione: https://hdiconfigactions.blob.core.windows.net/.
* Verificare che uno script di personalizzazione cluster hello è idempotente

    È necessario prevedere che i nodi di un cluster HDInsight hello viene ricreata l'immagine nel corso della durata del cluster di hello. script di personalizzazione di Hello cluster viene eseguito ogni volta che viene ricreata l'immagine di un cluster. Questo script deve essere idempotente toobe progettato in senso hello che al momento di ricreazione dell'immagine, script hello deve assicurare che tale cluster hello è restituiti stesso personalizzato dello stato in cui era subito dopo hello script è stato eseguito per hello prima ora cluster hello inizialmente toohello creato. Ad esempio, se uno script personalizzato installata un'applicazione in D:\AppLocation la prima esecuzione, quindi ogni successiva esecuzione, al momento di ricreazione dell'immagine, script hello deve verificare l'esistenza di un'applicazione hello in hello D:\AppLocation percorso prima di procedere con altre passaggi in uno script hello.
* Installare i componenti personalizzati in posizione ottimale hello

    Quando vengano ricreata l'immagine di nodi del cluster, unità di risorsa C:\ hello e unità di sistema D:\ può essere riformattati, pertanto hello perdita di dati e applicazioni installate in tali unità. Questo problema può verificarsi anche se un nodo di macchina virtuale di Azure (VM) che fa parte del cluster hello diventa inattivo e viene sostituito da un nuovo nodo. È possibile installare i componenti hello unità D:\ o nel percorso C:\apps hello cluster hello. Tutti gli altri percorsi in hello unità C:\ sono riservati. Specificare hello percorso in cui le applicazioni o librerie toobe installato in uno script di personalizzazione di hello del cluster.
* Verificare la disponibilità elevata dell'architettura di cluster hello

    HDInsight è un'architettura attivo-passivo per la disponibilità elevata, in cui un nodo head è in modalità attiva (in cui sono in esecuzione servizi HDInsight hello) e altri hello nodo head è in modalità standby (nella quale HDInsight servizi non vengono eseguiti). nodi Hello cambiare la modalità di attive e passive se HDInsight vengono interrotti. Se un'azione di script è servizi tooinstall usato in entrambi i nodi head per la disponibilità elevata, si noti che il meccanismo di failover di HDInsight hello non fail tooautomatically in grado di questi servizi installato dall'utente. Servizi pertanto installato dall'utente nei nodi head HDInsight che sono previsti toobe a disponibilità elevata devono essere dispongono di un proprio meccanismo di failover se è in modalità attiva-passiva o in modalità attivo-attivo.

    Viene eseguito un comando di HDInsight genera Script azione in entrambi i nodi head quando il ruolo del nodo head hello è specificato come valore di hello *ClusterRoleCollection* parametro. Pertanto, quando si progetta uno script personalizzato, assicurarsi che lo script tenga conto di questa impostazione. È consigliabile non eseguire problemi in cui hello stessi servizi sono installati e avviati su entrambi i nodi head hello e finiscono con competizione tra loro. Inoltre, tenere presente che i dati vengano persi durante la ricreazione dell'immagine, in modo software installato tramite l'azione di Script ha toobe toosuch resilienti eventi. Applicazioni devono essere progettate toowork con disponibilità elevata dei dati sono distribuita in molti nodi. Si noti che può essere ricreata l'immagine di un massimo di 1/5 di nodi hello in un cluster in hello contemporaneamente.
* Configurare l'archiviazione Blob di Azure toouse componenti personalizzati di hello

    i componenti personalizzati Hello installata nei nodi del cluster hello potrebbero essere un toouse di configurazione predefinito archiviazione Hadoop Distributed File System (HDFS). In alternativa, è necessario modificare hello configurazione toouse archiviazione Blob di Azure. In una nuova immagine del cluster, hello HDFS file system Ottiene formattato e si perderanno tutti i dati sono archiviati. Se invece si usa l'archivio BLOB di Azure, i dati vengono mantenuti.

## <a name="common-usage-patterns"></a>Modelli di utilizzo comuni
Questa sezione vengono fornite informazioni aggiuntive sull'implementazione di alcuni dei modelli di utilizzo comuni hello che potrebbero essere generati durante la scrittura di script personalizzato.

### <a name="configure-environment-variables"></a>Configurare le variabili di ambiente
Spesso nello sviluppo di azione di script, si ritiene hello necessario tooset le variabili di ambiente. Ad esempio, uno scenario più probabile è quando si scarica un file binario da un sito esterno, installarlo nel cluster hello e aggiunta hello posizione in cui è installato tooyour variabile di ambiente 'PATH'. Hello frammento di codice seguente viene illustrato come le variabili di ambiente tooset in hello script personalizzato.

    Write-HDILog "Starting environment variable setting at: $(Get-Date)";
    [Environment]::SetEnvironmentVariable('MDS_RUNNER_CUSTOM_CLUSTER', 'true', 'Machine');

Questa istruzione consente di impostare la variabile di ambiente hello **MDS_RUNNER_CUSTOM_CLUSTER** toohello valore 'true', nonché set hello ambito di questa variabile toobe a livello di computer. In alcuni casi è importante che le variabili di ambiente sono impostate in ambito appropriato hello-computer o dell'utente. Vedere [qui][1] per altre informazioni sull'impostazione delle variabili di ambiente.

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Accesso toolocations in cui sono archiviati gli script personalizzati hello
Script utilizzati toocustomize tooeither di esigenze di un cluster trovarsi nell'account di archiviazione predefinito hello per cluster hello o in un contenitore di sola lettura pubblico in qualsiasi altro account di archiviazione. Se lo script accede a risorse che si trovano in un' posizione, questi devono toobe in accessibile pubblicamente (pubblici almeno sola lettura). Ad esempio si tooaccess un file e salvarlo con il comando hello SaveFile HDI.

    Save-HDIFile -SrcUri 'https://somestorageaccount.blob.core.windows.net/somecontainer/some-file.jar' -DestFile 'C:\apps\dist\hadoop-2.4.0.2.1.9.0-2196\share\hadoop\mapreduce\some-file.jar'

In questo esempio, è necessario assicurarsi che il contenitore hello 'somecontainer' in 'somestorageaccount' account di archiviazione è accessibile pubblicamente. In caso contrario, script hello genera un'eccezione "Non trovato" e non riuscire.

### <a name="pass-parameters-toohello-add-azurermhdinsightscriptaction-cmdlet"></a>Passare parametri toohello Aggiungi AzureRmHDInsightScriptAction cmdlet
toopass più parametri toohello Aggiungi AzureRmHDInsightScriptAction cmdlet, è necessario tooformat hello stringa valore toocontain tutti i parametri per lo script hello. ad esempio:

    "-CertifcateUri wasb:///abc.pfx -CertificatePassword 123456 -InstallFolderName MyFolder"

oppure

    $parameters = '-Parameters "{0};{1};{2}"' -f $CertificateName,$certUriWithSasToken,$CertificatePassword


### <a name="throw-exception-for-failed-cluster-deployment"></a>Generare un'eccezione per la distribuzione cluster non riuscita
Se si desidera tooget una notifica in modo accurato dei fatti hello di personalizzazione di cluster non è stata eseguita come previsto, è importante toothrow un'eccezione e la creazione di cluster hello di esito negativo. Ad esempio, si potrebbe essere necessario tooprocess un file se esiste e gestire il caso di errore hello file hello in cui non esiste. In tal modo che script hello viene chiuso normalmente e stato hello del cluster di hello correttamente è noto. Hello frammento di codice seguente viene fornito un esempio di come tooachieve questo:

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    exit
    }

In questo frammento di codice, se il file hello non esiste, potrebbe causare tooa stato in cui hello script effettivamente viene chiuso normalmente dopo la stampa il messaggio di errore hello e cluster hello raggiunge uno stato di esecuzione presupponendo che "" completato il processo di personalizzazione di cluster. Se si desidera toobe una notifica in modo accurato dei fatti hello personalizzazione cluster essenzialmente non è stata eseguita come previsto a causa di un file mancante, è più appropriato toothrow un'eccezione e imposti hello cluster personalizzazione passaggio non riuscito. tooachieve scopo, è necessario usare hello seguente frammento di codice di esempio invece.

    If(Test-Path($SomePath)) {
        #Process file in some way
    } else {
        # File does not exist; handle error case
        # Print error message
    throw
    }


## <a name="checklist-for-deploying-a-script-action"></a>Elenco di controllo per la distribuzione di un'azione script
Ecco i passaggi di hello effettuati durante la preparazione di questi script toodeploy:

1. Inserire i file hello che contengono gli script personalizzati hello in una posizione accessibile dai nodi di cluster hello durante la distribuzione. Può trattarsi di qualsiasi valore predefinito di hello o altri account di archiviazione specificato in fase di distribuzione di cluster, o qualsiasi altro contenitore di archiviazione accessibile pubblicamente di hello.
2. Aggiungere i controlli in script toomake si è certi che vengono eseguiti in modo idempotente, in modo che script hello può essere eseguito più volte su hello stesso nodo.
3. Hello utilizzare **Write-Output** tooSTDOUT tooprint cmdlet di Azure PowerShell, nonché STDERR. Non usare **Write-Host**.
4. Utilizzare una cartella di file temporaneo, ad esempio $env: TEMP, tookeep hello file scaricato utilizzato dagli script hello e quindi li elimina dopo aver eseguito gli script.
5. Installare il software personalizzato solo in D:\ o C:\apps. Altre posizioni nell'unità c: hello non devono essere utilizzati poiché sono riservate. Si noti che l'installazione di file nell'unità c: hello esterni alla cartella C:\apps hello potrebbe causare errori durante l'installazione durante reimages del nodo hello.
6. In caso di hello che siano stati modificati le impostazioni a livello del sistema operativo o i file di configurazione del servizio di Hadoop, è consigliabile toorestart HDInsight servizi in modo che sia possibile acquisiscono le impostazioni a livello del sistema operativo, ad esempio le variabili di ambiente hello set negli script hello.

## <a name="debug-custom-scripts"></a>Eseguire il debug degli script personalizzati
vengono archiviati i log degli errori di script Hello, insieme a altro output, nell'account di archiviazione hello predefinito specificato per il cluster hello al momento della relativa creazione. Hello i log vengono archiviati in una tabella con nome hello *u < \cluster-name-fragment >< \time-stamp > setuplog*. Questi sono registri aggregati che presentano record da tutti i nodi hello (nodo head e i nodi di lavoro) in cui hello script viene eseguito nel cluster hello.
Un modo semplice i registri di hello toocheck è toouse di strumenti di HDInsight per Visual Studio. Per installare gli strumenti di hello, vedere [iniziare a usare gli strumenti di Visual Studio Hadoop per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md#install-data-lake-tools-for-visual-studio)

**log di hello toocheck utilizzando Visual Studio**

1. Aprire Visual Studio.
2. Fare clic su **Visualizza** e quindi su **Esplora server**.
3. Fare doppio clic su "Azure", fare clic su Connetti troppo**sottoscrizioni di Microsoft Azure**e quindi immettere le credenziali.
4. Espandere **archiviazione**, espandere account di archiviazione di Azure hello utilizzato come file system predefinito hello **tabelle**e quindi fare doppio clic sul nome della tabella hello.

È possibile anche remoto in toosee di nodi cluster hello sia STDOUT e STDERR per gli script personalizzati. Hello i log in ogni nodo sono nodo toothat solo specifico e vengono registrati in **C:\HDInsightLogs\DeploymentAgent.log**. Questi file di log registrano tutti gli output di uno script personalizzato hello. Un frammento di log di esempio per un'azione script Spark è simile a quanto riportato di seguito:

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand; Details : BEGIN: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Starting Spark installation at: 09/04/2014 21:46:02 Done with Spark installation at: 09/04/2014 21:46:38;

    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;
    ...

    Microsoft.Hadoop.Deployment.Engine.CustomPowershellScriptCommand;
    Details : END: Invoking powershell script https://configactions.blob.core.windows.net/sparkconfigactions/spark-installer.ps1.;
    Version : 2.1.0.0;
    ActivityId : 739e61f5-aa22-4254-aafc-9faf56fc2692;
    AzureVMName : HEADNODE0;
    IsException : False;
    ExceptionType : ;
    ExceptionMessage : ;
    InnerExceptionType : ;
    InnerExceptionMessage : ;
    Exception : ;


In questo log, è evidente che l'azione di script Spark hello è stato eseguito nella macchina virtuale denominata HEADNODE0 hello e che non sono state generate eccezioni durante l'esecuzione di hello.

In caso di hello che si verifica un errore di esecuzione, che descrive il output di hello è contenuta anche in questo file di log. informazioni di Hello fornite in questi registri devono essere utile eseguire il debug di problemi di script che possono verificarsi.

## <a name="see-also"></a>Vedere anche
* [Personalizzare cluster HDInsight mediante l'azione script][hdinsight-cluster-customize]
* [Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]
* [Installare e usare R nei cluster HDInsight][hdinsight-r-scripts]
* [Installare e usare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md).
* [Installare e usare Giraph nei cluster HDInsight](hdinsight-hadoop-giraph-install.md).

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-r-scripts]: hdinsight-hadoop-r-scripts.md
[powershell-install-configure]: install-configure-powershell.md

<!--Reference links in article-->
[1]: https://msdn.microsoft.com/library/96xafkes(v=vs.110).aspx
