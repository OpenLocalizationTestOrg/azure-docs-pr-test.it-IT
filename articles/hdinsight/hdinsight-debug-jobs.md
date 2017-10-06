---
title: 'Eseguire il debug di Hadoop in HDInsight: visualizzare i log e interpretare i messaggi di errore - Azure | Microsoft Docs'
description: Informazioni sui messaggi di errore hello che potrebbe essere visualizzato per l'amministrazione tramite PowerShell e i passaggi da eseguire toorecover HDInsight.
services: hdinsight
tags: azure-portal
editor: cgronlun
manager: jhubbard
author: mumian
documentationcenter: 
ms.assetid: 7e6ceb0e-8be8-4911-bc80-20714030a3ad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 2f12a40e9dcac32ce2e11d66d60d8b3b212ecb53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-hdinsight-logs"></a>Analizzare i log di HDInsight
Ogni cluster Hadoop in HDInsight di Azure dispone di un account di archiviazione di Azure usato come file system predefinito hello. account di archiviazione Hello è definito come account di archiviazione predefinito hello. Cluster utilizza l'archiviazione tabelle di Azure hello e hello nell'archiviazione Blob in hello predefinito Storage account toostore dei log.  toofind all'account di archiviazione hello predefinito per il cluster, vedere [cluster di gestire Hadoop in HDInsight](hdinsight-administer-use-management-portal.md#find-the-default-storage-account). i registri di Hello mantengono in hello account di archiviazione, anche dopo l'eliminazione di cluster hello.

## <a name="logs-written-tooazure-tables"></a>Scrittura tooAzure tabelle dei log
Hello log scritto tooAzure tabelle forniscono un livello di informazioni su cosa avviene con un cluster HDInsight.

Quando si crea un cluster HDInsight, le 6 tabelle vengono create automaticamente per i cluster basati su Linux nell'archiviazione tabelle di hello predefinito:

* hdinsightagentlog
* syslog
* daemonlog
* hadoopservicelog
* ambariserverlog
* ambariagentlog

Per i cluster basati su Windows vengono create 3 tabelle:

* setuplog: log di eventi/eccezioni rilevati durante il provisioning o la configurazione dei cluster HDInsight.
* hadoopinstalllog: Log di eventi le eccezioni durante l'installazione di Hadoop in cluster hello. Questa tabella può essere utile per il debug dei problemi correlati tooclusters creato con parametri personalizzati.
* hadoopservicelog: log di eventi/eccezioni registrati da tutti i servizi Hadoop. Questa tabella può essere utile eseguire il debug di problemi correlati toojob errori nei cluster HDInsight.

nomi file Hello sono **u<ClusterName>DDMonYYYYatHHMMSSsss<TableName>**.

Queste tabelle contiene hello seguenti campi:

* ClusterDnsName
* ComponentName
* EventTimestamp
* Host
* MALoggingHash
* Message
* N
* PreciseTimeStamp
* Ruolo
* RowIndex
* Tenant
* TIMESTAMP
* TraceLevel

### <a name="tools-for-accessing-hello-logs"></a>Strumenti per l'accesso ai registri hello
Sono disponibili diversi strumenti per accedere ai dati in queste tabelle:

* Visual Studio
* Azure Storage Explorer
* Power Query per Excel

#### <a name="use-power-query-for-excel"></a>Usare Power Query per Excel
Power Query può essere installato da [www.microsoft.com/it-it/download/details.aspx?id=39379](http://www.microsoft.com/en-us/download/details.aspx?id=39379). Vedere hello pagina di download per i requisiti di sistema hello

**toouse Power Query tooopen e analizzare i log di servizio hello**

1. Aprire **Microsoft Excel**.
2. Da hello **Power Query** menu, fare clic su **da Azure**, quindi fare clic su **archiviazione tabelle di Azure da Microsoft**.
   
    ![Hadoop in HDInsight - PowerQuery per Excel - Aprire l'archivio tabelle di Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-open.png)
3. Immettere nome account di archiviazione hello. Può trattarsi di nome breve hello o hello FQDN.
4. Immettere una chiave dell'account di archiviazione hello. Verrà visualizzato un elenco di tabelle:
   
    ![Hadoop in HDInsight - Log archiviati nell'archivio tabelle di Azure](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-table-names.png)
5. Pulsante destro del mouse hello hadoopservicelog tabella hello **Navigator** riquadro e selezionare **modifica**. Verranno visualizzate 4 colonne. Facoltativamente, eliminare hello **chiave di partizione**, **chiave di riga**, e **Timestamp** colonne selezionandoli e scegliendo **Rimuovi colonne** una delle opzioni di hello nella barra multifunzione hello.
6. Fare clic su hello espandere l'icona di hello colonna toochoose hello colonne che si desidera tooimport nel foglio di calcolo Excel hello del contenuto. Per questa dimostrazione, sono state scelte TraceLevel e ComponentName che contengono alcune informazioni di base sui componenti con problemi.
   
    ![Log di Hadoop in HDInsight - Scegliere le colonne](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-using-excel-power-query-filter.png)
7. Fare clic su **OK** dati hello tooimport.
8. Seleziona hello **TraceLevel**, ruolo e **ComponentName** colonne e quindi fare clic su **Group By** controllo nella barra multifunzione hello.
9. Fare clic su **OK** in hello Group By finestra di dialogo
10. Fare clic su **Applica e chiudi**.

È ora possibile usare Excel toofilter e ordinamento in base alle esigenze. Ovviamente, è opportuno tooinclude altre colonne (ad esempio messaggio), in ordine toodrill verso il basso in problemi quando si verificano, ma selezionare e raggruppare le colonne di hello descritte sopra offre un quadro ragionevole delle operazioni eseguite con i servizi Hadoop. Hello stesso concetto può essere applicato toohello setuplog e hadoopinstalllog tabelle.

#### <a name="use-visual-studio"></a>Usare Visual Studio
**toouse Visual Studio**

1. Aprire Visual Studio.
2. Da hello **vista** menu, fare clic su **Cloud Explorer**. oppure fare semplicemente clic su **CTRL+\,** CTRL+X.
3. In **Cloud Explorer** selezionare **Tipi di risorse**.  Hello altra opzione disponibile è **gruppi di risorse**.
4. Espandere **gli account di archiviazione**, hello account di archiviazione predefinito per il cluster, quindi **tabelle**.
5. Fare doppio clic su **hadoopservicelog**.
6. Aggiungere un filtro. Ad esempio:
   
        TraceLevel eq 'ERROR'
   
    ![Log di Hadoop in HDInsight - Scegliere le colonne](./media/hdinsight-debug-jobs/hdinsight-hadoop-analyze-logs-visual-studio-filter.png)
   
    Per ulteriori informazioni sulla creazione di filtri, vedere [costruire stringhe di filtro per Progettazione tabelle hello](../vs-azure-tools-table-designer-construct-filter-strings.md).

## <a name="logs-written-tooazure-blob-storage"></a>Registra tooAzure scritti nell'archiviazione Blob
[Hello log scritto tooAzure tabelle](#log-written-to-azure-tables) forniscono un livello di informazioni su cosa avviene con un cluster HDInsight. Queste tabelle non offrono tuttavia log a livello di attività, che possono essere utili per approfondire i problemi quando si verificano. tooprovide questo livello di dettaglio, sono i cluster HDInsight successivo configurato toowrite attività registri tooyour account di archiviazione Blob di qualsiasi processo che viene inviata tramite Templeton. In pratica, ciò significa che i processi inviati tramite i cmdlet di Microsoft Azure PowerShell hello o hello invio le API .NET processo, non i processi inviati tramite RDP/della riga di comando toohello cluster di accesso. 

vedere i log hello tooview, [log applicazioni di accesso YARN in HDInsight basati su Linux](hdinsight-hadoop-access-yarn-app-logs-linux.md).

Per altre informazioni sui registri applicazioni, vedere la pagina che illustra come [semplificare la gestione e l'accesso ai log utenti in YARN](http://hortonworks.com/blog/simplifying-user-logs-management-and-access-in-yarn/).

## <a name="view-cluster-health-and-job-logs"></a>Visualizzare i log di integrità e dei processi del cluster
### <a name="access-hadoop-ui"></a>Accedere all'interfaccia utente di Hadoop
Dal portale di Azure hello, fare clic su un pannello del cluster di HDInsight cluster nome tooopen hello. Dal Pannello di hello cluster, fare clic su **Dashboard**.

![Avviare il dashboard del cluster](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard.png)

Quando richiesto, immettere le credenziali di amministratore cluster hello. Nella Console di Query che consente di aprire hello, fare clic su **Hadoop UI**.

![Avviare l'interfaccia utente di Hadoop](./media/hdinsight-debug-jobs/hdi-debug-launch-dashboard-hadoop-ui.png)

### <a name="access-hello-yarn-ui"></a>Accedere hello Yarn UI
Dal portale di Azure hello, fare clic su un pannello del cluster di HDInsight cluster nome tooopen hello. Dal Pannello di hello cluster, fare clic su **Dashboard**. Quando richiesto, immettere le credenziali di amministratore cluster hello. Nella Console di Query che consente di aprire hello, fare clic su **dell'interfaccia utente YARN**.

È possibile utilizzare hello dell'interfaccia utente YARN toodo hello seguente:

* **Ottenere lo stato del cluster**. Nel riquadro sinistro hello espandere **Cluster**, fare clic su **su**. Il presente cluster dettagli stato come totale di memoria, core utilizzati, lo stato di gestione delle risorse cluster hello, versione e così via del cluster.
  
    ![Avviare il dashboard del cluster](./media/hdinsight-debug-jobs/hdi-debug-yarn-cluster-state.png)
* **Ottenere lo stato del nodo**. Nel riquadro sinistro hello espandere **Cluster**, fare clic su **nodi**. Elenca tutti i nodi hello cluster hello, l'indirizzo HTTP di ogni nodo, il nodo tooeach allocate risorse e così via.
* **Monitorare lo stato dei processi**. Nel riquadro sinistro hello espandere **Cluster**e quindi fare clic su **applicazioni** toolist tutti hello processi nel cluster hello. Se si desidera toolook a processi in un determinato stato (ad esempio, nuovo, inviata, in esecuzione e così via), fare clic su collegamento appropriato di hello in **applicazioni**. È possibile scegliere un'ulteriore hello processo nome toofind ulteriori informazioni sui processi hello tali incluso l'output di hello, log e così via.

### <a name="access-hello-hbase-ui"></a>Accedere hello UI HBase
Dal portale di Azure hello, fare clic su un pannello del cluster di HDInsight HBase cluster nome tooopen hello. Dal Pannello di hello cluster, fare clic su **Dashboard**. Quando richiesto, immettere le credenziali di amministratore cluster hello. Nella Console di Query che consente di aprire hello, fare clic su **HBase UI**.

## <a name="hdinsight-error-codes"></a>Codici di errore di HDInsight
Hello messaggi di errore dettagliati in questa sezione vengono forniti gli utenti di hello toohelp di Hadoop in HDInsight di Azure comprendere eventuali condizioni di errore riscontrati quando si amministra servizio hello Azure PowerShell e tooadvise usarle in passaggi hello che può essere effettuato toorecover errore hello.

Alcuni di questi messaggi di errore potrebbe anche nel portale di Azure hello quando è cluster HDInsight toomanage utilizzato. Ma possono verificarsi altri messaggi di errore sono disponibili meno granulari a causa di vincoli toohello sulle azioni correttive hello possibili in questo contesto. Altri messaggi di errore sono incluse nei contesti di hello in attenuazione hello è ovvio. 

### <a id="AtleastOneSqlMetastoreMustBeProvided"></a>AtleastOneSqlMetastoreMustBeProvided
* **Descrizione**: specificare i dettagli del database SQL di Azure per almeno un componente in ordine toouse impostazioni personalizzate per i Metastore Hive e Oozie.
* **Attenuazione**: utente hello deve toosupply una SQL Azure metastore e ripetere hello richiesta valida.  

### <a id="AzureRegionNotSupported"></a>AzureRegionNotSupported
* **Descrizione**: non è possibile creare il cluster nell'area *NomeAreaGeografica*. Utilizzare un'area HDInsight valida e ripetere le richiesta.
* **Attenuazione**: cliente deve creare l'area del cluster hello che li supporta attualmente: Stati Uniti occidentali, Stati Uniti orientali, Europa settentrionale, Europa occidentale o Asia sudorientale.  

### <a id="ClusterContainerRecordNotFound"></a>ClusterContainerRecordNotFound
* **Descrizione**: Impossibile trovare server hello hello richiesto record cluster.  
* **Attenuazione**: hello riprovare.

### <a id="ClusterDnsNameInvalidReservedWord"></a>ClusterDnsNameInvalidReservedWord
* **Descrizione**: il nome DNS del cluster *NomeDNS* non è valido. Il nome deve iniziare e finire con un carattere alfanumerico e può contenere solo il carattere speciale '-'.  
* **Attenuazione**: assicurarsi che sia stato utilizzato un nome DNS valido per il cluster che inizia e termina con caratteri alfanumerici e non speciale contiene caratteri diversi da dash hello '-', quindi ripetere l'operazione di hello.

### <a id="ClusterNameUnavailable"></a>ClusterNameUnavailable
* **Descrizione**: il nome del cluster *NomeCluster* non è disponibile. Scegliere un altro nome.  
* **Attenuazione**: hello utente deve specificare un nome cluster che è univoco e non esiste e riprovare. Se l'utente hello utilizza hello portale, hello dell'interfaccia utente verrà notifica se un nome di cluster è già in uso durante hello creare passaggi.

### <a id="ClusterPasswordInvalid"></a>ClusterPasswordInvalid
* **Descrizione**: la password del cluster non è valida. La password deve essere pari ad almeno 10 caratteri e deve contenere almeno un numero, una lettera maiuscola, una lettera minuscola e un carattere speciale senza spazi e non deve contenere il nome utente hello come parte di esso.  
* **Attenuazione**: fornire una password di cluster valido e ripetere l'operazione di hello.

### <a id="ClusterUserNameInvalid"></a>ClusterUserNameInvalid
* **Descrizione**: il nome utente del cluster non è valido. Assicurarsi che il nome utente non contenga caratteri speciali o spazi.  
* **Attenuazione**: specificare un nome utente valido del cluster e ripetere l'operazione di hello.

### <a id="ClusterUserNameInvalidReservedWord"></a>ClusterUserNameInvalidReservedWord
* **Descrizione**: il nome DNS del cluster *NomeClusterDns* non è valido. Il nome deve iniziare e finire con un carattere alfanumerico e può contenere solo il carattere speciale '-'.  
* **Attenuazione**: specificare un nome utente valido del cluster DNS e ripetere l'operazione di hello.

### <a id="ContainerNameMisMatchWithDnsName"></a>ContainerNameMisMatchWithDnsName
* **Descrizione**: nome del contenitore nell'URI *yourcontainerURI* e il nome DNS *yourDnsName* nella richiesta deve hello corpo stesso.  
* **Attenuazione**: verificare che il nome del contenitore e il nome DNS sono hello stesso e ripetere l'operazione di hello.

### <a id="DataNodeDefinitionNotFound"></a>DataNodeDefinitionNotFound
* **Descrizione**: configurazione del cluster non valida. Non è possibile toofind le definizioni del nodo di dati nella dimensione del nodo.  
* **Attenuazione**: hello riprovare.

### <a id="DeploymentDeletionFailure"></a>DeploymentDeletionFailure
* **Descrizione**: l'eliminazione della distribuzione non riuscita per hello Cluster  
* **Attenuazione**: ripetere l'operazione di eliminazione hello.

### <a id="DnsMappingNotFound"></a>DnsMappingNotFound
* **Descrizione**: errore di configurazione del servizio. Informazioni di mapping DNS richieste non trovate.  
* **Soluzione**: eliminare il cluster e crearne uno nuovo.

### <a id="DuplicateClusterContainerRequest"></a>DuplicateClusterContainerRequest
* **Descrizione**: tentativo di creazione di contenitore cluster duplicato. Esiste un record per *NomeContenitore* ma gli Etag non corrispondono.
* **Attenuazione**: specificare un nome univoco per il contenitore di hello e riprova hello operazione di creazione.

### <a id="DuplicateClusterInHostedService"></a>DuplicateClusterInHostedService
* **Descrizione**: il servizio ospitato *NomeServizioOspitato* contiene già un cluster. Un servizio ospitato non può contenere più cluster.  
* **Attenuazione**: cluster hello Host in un altro servizio ospitato.

### <a id="FailureToUpdateDeploymentStatus"></a>FailureToUpdateDeploymentStatus
* **Descrizione**: hello Impossibile aggiornare lo stato di hello hello dell'implementazione del cluster.  
* **Attenuazione**: hello riprovare. Se il problema persiste, contattare il servizio di assistenza clienti.

### <a id="HdiRestoreClusterAltered"></a>HdiRestoreClusterAltered
* **Descrizione**: il cluster *NomeCluster* è stato eliminato durante la manutenzione. Ricreare il cluster hello.
* **Attenuazione**: cluster hello ricreare.

### <a id="HeadNodeConfigNotFound"></a>HeadNodeConfigNotFound
* **Descrizione**: configurazione del cluster non valida. Impossibile trovare la configurazione del nodo head richiesta nelle dimensioni dei nodi.
* **Attenuazione**: hello riprovare.

### <a id="HostedServiceCreationFailure"></a>HostedServiceCreationFailure
* **Descrizione**: servizio ospitato non è possibile toocreate *nameOfYourHostedService*. Ripetere la richiesta.  
* **Attenuazione**: ripetere la richiesta hello.

### <a id="HostedServiceHasProductionDeployment"></a>HostedServiceHasProductionDeployment
* **Descrizione**: il servizio ospitato *NomeServizioOspitato* include già una distribuzione di produzione. Un servizio ospitato non può contenere più distribuzioni di produzione. Ripetere la richiesta di hello con un nome di cluster diverso.
* **Attenuazione**: utilizzare un nome di cluster diverso e ripetere la richiesta hello.

### <a id="HostedServiceNotFound"></a>HostedServiceNotFound
* **Descrizione**: servizio ospitato *nameOfYourHostedService* per cluster hello non è stato trovato.  
* **Attenuazione**: se hello cluster è in stato di errore, eliminare e quindi riprovare.

### <a id="HostedServiceWithNoDeployment"></a>HostedServiceWithNoDeployment
* **Descrizione**: al servizio ospitato *NomeServizioOspitato* non è associata alcuna distribuzione.  
* **Attenuazione**: se hello cluster è in stato di errore, eliminare e quindi riprovare.

### <a id="InsufficientResourcesCores"></a>InsufficientResourcesCores
* **Descrizione**: hello SubscriptionId *yourSubscriptionId* privo di cluster toocreate sinistro core *yourClusterName*. Richiesti: *RisorseRichieste*, Disponibili: *RisorseDisponibili*.  
* **Attenuazione**: liberare risorse nella sottoscrizione o aumentare la sottoscrizione di hello risorse toohello disponibile e riprovare a eseguire cluster hello toocreate.

### <a id="InsufficientResourcesHostedServices"></a>InsufficientResourcesHostedServices
* **Descrizione**: ID sottoscrizione *yourSubscriptionId* non dispone di quota per un nuovo cluster toocreate HostedService *yourClusterName*.  
* **Attenuazione**: liberare risorse nella sottoscrizione o aumentare la sottoscrizione di hello risorse toohello disponibile e riprovare a eseguire cluster hello toocreate.

### <a id="InternalErrorRetryRequest"></a>InternalErrorRetryRequest
* **Descrizione**: hello rilevato un errore interno. Ripetere la richiesta.  
* **Attenuazione**: ripetere la richiesta hello.

### <a id="InvalidAzureStorageLocation"></a>InvalidAzureStorageLocation
* **Descrizione**: la posizione di archiviazione di Azure *NomeAreaDati* non è una posizione valida. Verificare che l'area hello sia corretto e ripetere richiesta.
* **Attenuazione**: selezionare un percorso di archiviazione che supporta HDInsight, verificare che il cluster sia con risorse condivise e ripetere l'operazione di hello.

### <a id="InvalidNodeSizeForDataNode"></a>InvalidNodeSizeForDataNode
* **Descrizione**: dimensioni della macchina virtuale non valide per i nodi dati. Per tutti i nodi dati è supportata solo la dimensione grande della macchina virtuale.  
* **Attenuazione**: specificare le dimensioni di nodo hello è supportato per il nodo di dati hello e ripetere l'operazione di hello.

### <a id="InvalidNodeSizeForHeadNode"></a>InvalidNodeSizeForHeadNode
* **Descrizione**: dimensioni della macchina virtuale non valide per il nodo head. Per il nodo head sono supportate solo le dimensioni Molto grande della macchina virtuale.  
* **Attenuazione**: specificare dimensioni di nodo hello è supportato per il nodo head hello e ripetere l'operazione di hello

### <a id="InvalidRightsForDeploymentDeletion"></a>InvalidRightsForDeploymentDeletion
* **Descrizione**: ID sottoscrizione *yourSubscriptionId* in uso non dispone di operazione di eliminazione tooexecute di autorizzazioni sufficienti per cluster *yourClusterName*.  
* **Attenuazione**: se hello cluster è in stato di errore, eliminarlo e quindi riprovare.  

### <a id="InvalidStorageAccountBlobContainerName"></a>InvalidStorageAccountBlobContainerName
* **Descrizione**: il nome del contenitore BLOB dell'account di archiviazione esterno *NomeContenitore* non è valido. Verificare che il nome inizi con una lettera e contenga solo lettere minuscole, numeri e trattini.  
* **Attenuazione**: specificare un nome di contenitore blob di account di archiviazione valido e ripetere l'operazione di hello.

### <a id="InvalidStorageAccountConfigurationSecretKey"></a>InvalidStorageAccountConfigurationSecretKey
* **Descrizione**: configurazione per l'account di archiviazione esterna *yourStorageAccountName* è obbligatorio toohave dettagli chiave segreti toobe set.  
* **Attenuazione**: specificare una chiave segreta valida per l'account di archiviazione hello e ripetere l'operazione di hello.

### <a id="InvalidVersionHeaderFormat"></a>InvalidVersionHeaderFormat
* **Descrizione**: l'intestazione della versione *IntestazioneVersione* non è nel formato valido aaaa-mm-gg.  
* **Attenuazione**: specificare un formato valido per l'intestazione di versione di hello e ripetere la richiesta hello.

### <a id="MoreThanOneHeadNode"></a>MoreThanOneHeadNode
* **Descrizione**: configurazione del cluster non valida. Sono state rilevate più configurazioni di nodi head.  
* **Attenuazione**: configurazione di hello modifica in modo che solo un nodo head sia specificato.

### <a id="OperationTimedOutRetryRequest"></a>OperationTimedOutRetryRequest
* **Descrizione**: non è stato possibile completare l'operazione di hello all'interno di hello consentito ora o numero massimo di hello tentativi possibili. Ripetere la richiesta.  
* **Attenuazione**: ripetere la richiesta hello.

### <a id="ParameterNullOrEmpty"></a>ParameterNullOrEmpty
* **Descrizione**: il parametro *NomeParametro* non può essere Null o vuoto.  
* **Attenuazione**: specificare un valore valido per il parametro hello.

### <a id="PreClusterCreationValidationFailure"></a>PreClusterCreationValidationFailure
* **Descrizione**: uno o più input di hello cluster creazione richiesta non è valido. Assicurarsi che i valori di input hello siano corretti e ripetere richiesta.  
* **Attenuazione**: assicurarsi che i valori di input hello siano corretti e ripetere richiesta.

### <a id="RegionCapabilityNotAvailable"></a>RegionCapabilityNotAvailable
* **Descrizione**: la funzionalità relativa all'area geografica non è disponibile per l'area *NomeAreaGeografica* e l'ID sottoscrizione *IDSottoscrizione*.  
* **Soluzione**: specificare un'area geografica che supporta i cluster HDInsight. le aree Hello pubblicamente supportato sono: Stati Uniti occidentali, Stati Uniti orientali, Europa settentrionale, Europa occidentale o Asia sudorientale.

### <a id="StorageAccountNotColocated"></a>StorageAccountNotColocated
* **Descrizione**: l'account di archiviazione *NomeAccountArchiviazione* si trova nell'area *NomeAreaGeograficaCorrente*. Deve essere uguale a area cluster hello *yourClusterRegionName*.  
* **Attenuazione**: specificare un account di archiviazione in hello stessa regione che il cluster è in o se i dati sono già nell'account di archiviazione hello, creare un nuovo cluster in hello stessa area account di archiviazione esistente hello. Se si utilizza hello portale hello dell'interfaccia utente verrà informarli di questo problema in anticipo.

### <a id="SubscriptionIdNotActive"></a>SubscriptionIdNotActive
* **Descrizione**: l'ID sottoscrizione specificato *IDSottoscrizione* non è attivo.  
* **Soluzione**: riattivare la sottoscrizione oppure ottenere una nuova sottoscrizione valida.

### <a id="SubscriptionIdNotFound"></a>SubscriptionIdNotFound
* **Descrizione**:impossibile trovare l'ID sottoscrizione specificato *IDSottoscrizione* .  
* **Attenuazione**: verificare che l'ID sottoscrizione sia valido e ripetere l'operazione di hello.

### <a id="UnableToResolveDNS"></a>UnableToResolveDNS
* **Descrizione**: Impossibile tooresolve DNS *yourDnsUrl*. Verificare che URL hello completo per endpoint blob hello è fornito.  
* **Soluzione**: specificare un URL BLOB valido. Hello URL deve essere completamente validi, inclusi a partire da *http://* e di fine *. com*.

### <a id="UnableToVerifyLocationOfResource"></a>UnableToVerifyLocationOfResource
* **Descrizione**: Impossibile tooverify percorso della risorsa *yourDnsUrl*. Verificare che URL hello completo per endpoint blob hello è fornito.  
* **Soluzione**: specificare un URL BLOB valido. Hello URL deve essere completamente validi, inclusi a partire da *http://* e di fine *. com*.

### <a id="VersionCapabilityNotAvailable"></a>VersionCapabilityNotAvailable
* **Descrizione**: la funzionalità relativa alla versione non è disponibile per la versione *VersioneSpecificata* e l'ID sottoscrizione *IDSottoscrizione*.  
* **Attenuazione**: scegliere una versione che è disponibile e riprovare hello.

### <a id="VersionNotSupported"></a>VersionNotSupported
* **Descrizione**: la versione *VersioneSpecificata* non è supportata.
* **Attenuazione**: scegliere una versione supportata e ripetere l'operazione di hello.

### <a id="VersionNotSupportedInRegion"></a>VersionNotSupportedInRegion
* **Descrizione**: la versione *VersioneSpecificata* non è disponibile nell'area di Azure *AreaSpecificata*.  
* **Attenuazione**: scegliere una versione supportata nell'area di hello specificato e ripetere l'operazione di hello.

### <a id="WasbAccountConfigNotFound"></a>WasbAccountConfigNotFound
* **Descrizione**: configurazione del cluster non valida. Impossibile trovare la configurazione dell'account WASB negli account esterni.  
* **Attenuazione**: verificare che account hello esista e sia correttamente specificato nell'operazione di hello configurazione e riprovare.

## <a name="next-steps"></a>Passaggi successivi
* [Utilizzare viste Ambari toodebug Tez processi in HDInsight](hdinsight-debug-ambari-tez-view.md)
* [Abilitare i dump dell'heap per i servizi Hadoop in HDInsight basato su Linux](hdinsight-hadoop-collect-debug-heap-dump-linux.md)
* [Gestire cluster HDInsight con Ambari Web UI hello](hdinsight-hadoop-manage-ambari.md)

