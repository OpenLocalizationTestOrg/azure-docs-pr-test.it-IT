---
title: aaaRestrict l'accesso con firme di accesso condiviso - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse firme di accesso condiviso toorestrict HDInsight accedere toodata archiviato nel BLOB di archiviazione di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: a34a2f8e52e47a15b09f09bc1fc67fc6159ec75f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-shared-access-signatures-toorestrict-access-toodata-in-hdinsight"></a>Utilizzo di firme di accesso condiviso archiviazione Azure toorestrict accesso toodata in HDInsight

HDInsight dispone di accesso completo toodata negli account di archiviazione di Azure hello associato hello cluster. È possibile utilizzare le firme di accesso condiviso ai dati del blob contenitore toorestrict accesso toohello hello. Ad esempio, tooprovide accesso in sola lettura toohello dati. Le firme di accesso condiviso (SAS) sono una funzionalità di account di archiviazione di Azure che consente di toolimit toodata di accesso. Ad esempio, fornendo toodata accesso in sola lettura.

> [!IMPORTANT]
> Per una soluzione che usi Apache Ranger, considerare la possibilità di usare HDInsight aggiunto al dominio. Per ulteriori informazioni, vedere hello [configurare dominio HDInsight](hdinsight-domain-joined-configure.md) documento.

> [!WARNING]
> HDInsight è necessario spazio di archiviazione di accesso completo toohello predefinito per il cluster hello.

## <a name="requirements"></a>Requisiti

* Una sottoscrizione di Azure.
* C# o Python. Il codice di esempio in C# viene fornito come soluzione di Visual Studio.

  * Visual Studio versione 2013, 2015 o 2017
  * Python versione 2.7 o successiva.

* Un cluster HDInsight basati su Linux o [Azure PowerShell] [ powershell] -se si dispone di un cluster esistente basata su Linux, è possibile utilizzare Ambari tooadd un cluster di toohello di firma di accesso condiviso. In caso contrario, è possibile usare Azure PowerShell toocreate un cluster e aggiungere una firma di accesso condiviso durante la creazione del cluster.

    > [!IMPORTANT]
    > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* i file di esempio da Hello [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature). Il repository contiene hello seguenti elementi:

  * Un progetto di Visual Studio che può creare un contenitore di archiviazione, i criteri archiviati e la firma di accesso condiviso da usare con HDInsight.
  * Uno script di Python che può creare un contenitore di archiviazione, i criteri archiviati e la firma di accesso condiviso da usare con HDInsight.
  * Uno script di PowerShell che è possibile creare un HDInsight cluster e configurarlo hello toouse SAS.

## <a name="shared-access-signatures"></a>Firme di accesso condiviso

Esistono due tipi di firme di accesso condiviso:

* Ad hoc: hello ora di inizio, ora di scadenza e le autorizzazioni per hello SAS vengono specificate in hello URI SAS.

* Criteri di accesso archiviati: i criteri di accesso archiviati vengono definiti per un contenitore di risorse, ovvero un contenitore BLOB. I criteri possono essere utilizzati toomanage vincoli per uno o più firme di accesso condiviso. Quando si associa una firma di accesso condiviso con criteri di accesso archiviati, hello SAS eredita i vincoli di hello: hello ora di inizio, ora di scadenza e le autorizzazioni - definite per i criteri di accesso archiviato hello.

Hello differenza tra hello due forme è importante per uno scenario di chiave: revoche di certificati. Una firma di accesso condiviso è un URL, chiunque Ottiene hello SAS poterla utilizzare, indipendentemente dal fatto che ne ha richiesto toobegin con. Se una firma di accesso condiviso viene pubblicato, può essere utilizzato da chiunque in HelloWorld. Una forma di accesso condiviso rimane valida finché non si verifica una delle quattro condizioni seguenti:

1. ora di scadenza Hello specificato su hello che SAS viene raggiunto.

2. ora di scadenza Hello specificato nel criterio di accesso archiviato hello hello che viene raggiunto firma di accesso condiviso a cui fa riferimento. negli scenari seguenti Hello causano l'ora di scadenza hello toobe raggiunto:

    * è trascorso l'intervallo di tempo Hello.
    * i criteri di accesso archiviato Hello sono toohave modificata un'ora di scadenza in hello precedente. Modificando l'ora di scadenza hello è un modo toorevoke hello SAS.

3. Hello archiviati i criteri di accesso a cui fa riferimento hello che SAS viene eliminato, ovvero hello toorevoke di un altro modo SAS. Se si ricrea il criterio di accesso archiviato hello con stesso nome, tutti i token di firma di accesso condiviso per hello criteri precedenti hello valide (se l'ora di scadenza hello in hello SAS non ha superato). Se si prevede di hello toorevoke SAS, essere toouse che un altro nome se si ricrea il criterio di accesso hello con un'ora di scadenza in hello future.

4. chiave dell'account che è stato utilizzato toocreate hello SAS Hello viene rigenerato. Rigenerazione della chiave di hello fa sì che tutte le applicazioni che utilizzano l'autenticazione chiave toofail hello precedente. Aggiornare la chiave di nuovo di tutti i componenti toohello.

> [!IMPORTANT]
> Un URI di firma di accesso condiviso è associato con firma di hello toocreate utilizzati chiave account hello e hello associati criteri di accesso archiviati (se presente). Se si specifica alcun criterio di accesso archiviati, hello solo modo toorevoke una firma di accesso condiviso è toochange hello account chiave.

È consigliabile usare sempre i criteri di accesso archiviati. Quando si utilizzano i criteri archiviati, è possibile revocare le firme o estendere la data di scadenza hello in base alle esigenze. passaggi di Hello in questo documento usano i criteri di accesso archiviati toogenerate SAS.

Per ulteriori informazioni sulle firme di accesso condiviso, vedere [modello di firma di accesso condiviso hello comprensione](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

### <a name="create-a-stored-policy-and-sas-using-c"></a>Creare un criterio archiviato e una firma di accesso condiviso con C\#

1. Aprire la soluzione hello in Visual Studio.

2. In Esplora soluzioni, fare clic su hello **SASToken** del progetto e selezionare **proprietà**.

3. Selezionare **impostazioni** e aggiungere i valori per hello seguenti voci:

   * StorageConnectionString: hello stringa di connessione per l'account di archiviazione hello che si desidera toocreate un criterio archiviato e SAS per. deve essere formato Hello `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` in `myaccount` hello nome dell'account di archiviazione e `mykey` è hello chiave hello account di archiviazione.

   * ContainerName: contenitore hello nell'account di archiviazione hello che si desidera accedere toorestrict a.

   * SASPolicyName: hello Nome toouse per hello archiviati toocreate criteri.

   * FileToUpload: hello percorso tooa file contenitore toohello caricato.

4. Eseguire il progetto hello. Toohello simile di informazioni dopo il testo viene visualizzato dopo che è stato generato hello SAS:

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Salvare i token del criterio SAS hello, nome account di archiviazione e nome del contenitore. Questi valori vengono utilizzati quando si associa l'account di archiviazione hello con il cluster HDInsight.

### <a name="create-a-stored-policy-and-sas-using-python"></a>Creare un criterio archiviato e una firma di accesso condiviso con Python

1. Aprire il file SASToken.py hello e modificare hello seguenti valori:

   * criteri\_nome: hello Nome toouse per hello archiviati toocreate criteri.

   * archiviazione\_account\_name: nome hello dell'account di archiviazione.

   * archiviazione\_account\_chiave: hello chiave hello account di archiviazione.

   * archiviazione\_contenitore\_nome: il contenitore di hello nell'account di archiviazione hello che si desidera accedere toorestrict a.

   * esempio\_file\_percorso: hello percorso tooa file contenitore toohello caricato.

2. Eseguire script hello. Visualizza hello SAS token simile toohello seguente testo al termine dello script hello:

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    Salvare i token del criterio SAS hello, nome account di archiviazione e nome del contenitore. Questi valori vengono utilizzati quando si associa l'account di archiviazione hello con il cluster HDInsight.

## <a name="use-hello-sas-with-hdinsight"></a>Utilizzare hello SAS con HDInsight

Quando si crea un cluster HDInsight è necessario specificare un account di archiviazione primario e, facoltativamente, è possibile specificare account di archiviazione aggiuntivi. Entrambi i metodi di aggiunta di memoria richiedono account di archiviazione toohello accesso completo e contenitori che vengono utilizzati.

toouse contenitore tooa accesso toolimit firma di accesso condiviso, aggiungere una voce personalizzata di toohello **core sito** configurazione per il cluster hello.

* Per **basati su Windows** o **basati su Linux** cluster HDInsight, è possibile aggiungere la voce hello durante la creazione del cluster tramite PowerShell.
* Per **basati su Linux** cluster HDInsight, modificare la configurazione di hello dopo la creazione di cluster con Ambari.

### <a name="create-a-cluster-that-uses-hello-sas"></a>Creare un cluster che usa hello SAS

Un esempio di creazione di un cluster HDInsight che hello utilizza firma di accesso condiviso è incluso in hello `CreateCluster` directory del repository hello. toouse, utilizzare hello seguendo i passaggi:

1. Aprire hello `CreateCluster\HDInsightSAS.ps1` file in un editor di testo e modificare i seguenti valori all'inizio di hello del documento hello hello.

    ```powershell
    # Replace 'mycluster' with hello name of hello cluster toobe created
    $clusterName = 'mycluster'
    # Valid values are 'Linux' and 'Windows'
    $osType = 'Linux'
    # Replace 'myresourcegroup' with hello name of hello group toobe created
    $resourceGroupName = 'myresourcegroup'
    # Replace with hello Azure data center you want toohello cluster toolive in
    $location = 'North Europe'
    # Replace with hello name of hello default storage account toobe created
    $defaultStorageAccountName = 'mystorageaccount'
    # Replace with hello name of hello SAS container created earlier
    $SASContainerName = 'sascontainer'
    # Replace with hello name of hello SAS storage account created earlier
    $SASStorageAccountName = 'sasaccount'
    # Replace with hello SAS token generated earlier
    $SASToken = 'sastoken'
    # Set hello number of worker nodes in hello cluster
    $clusterSizeInNodes = 3
    ```

    Ad esempio, modificare `'mycluster'` toohello nome del cluster hello desiderato toocreate. i valori di firma di accesso condiviso Hello devono corrispondere i valori hello nei passaggi precedenti hello durante la creazione di un account di archiviazione e il token di firma di accesso condiviso.

    Dopo avere modificato i valori hello, salvare file hello.

2. Aprire un nuovo prompt dei comandi di Azure PowerShell. Se non si ha familiarità con Azure PowerShell o non è stato installato, vedere [Install and configure Azure PowerShell][powershell] (Installare e configurare Azure PowerShell).

1. Dal prompt dei comandi hello, utilizzare hello successivo comando tooauthenticate tooyour sottoscrizione di Azure:

    ```powershell
    Login-AzureRmAccount
    ```

    Quando richiesto, accedere con l'account hello per la sottoscrizione di Azure.

    Se l'account è associato a più sottoscrizioni di Azure, potrebbe essere necessario toouse `Select-AzureRmSubscription` sottoscrizione hello tooselect desiderato toouse.

4. Dal prompt dei comandi hello, modificare le directory toohello `CreateCluster` directory che contiene file HDInsightSAS.ps1 hello. Quindi utilizzare lo script di comando toorun hello seguente hello

    ```powershell
    .\HDInsightSAS.ps1
    ```

    Durante l'esecuzione di script hello, Registra prompt di PowerShell toohello output durante la creazione risorsa hello gli account di archiviazione e di gruppo. Si è utente di hello HTTP richiesta tooenter per hello cluster HDInsight. Questo account è di tipo cluster toohello di accesso HTTP/s toosecure utilizzato.

    Se si sta creando un cluster basato su Linux, viene chiesto di specificare anche un nome e una password per l'account utente SSH. Questo account è usato tooremotely log toohello cluster.

   > [!IMPORTANT]
   > Quando viene richiesto di hello HTTP/s o nome utente SSH e password, è necessario fornire una password che soddisfi i seguenti criteri hello:
   >
   > * La lunghezza non può essere inferiore a 10 caratteri
   > * Deve contenere almeno una cifra
   > * Deve contenere almeno un carattere non alfanumerico
   > * Deve contenere almeno una lettera maiuscola o minuscola

Occorre un po' di tempo per toocomplete questo script, in genere circa 15 minuti. Al termine dello script hello senza errori, è stato creato il cluster hello.

### <a name="use-hello-sas-with-an-existing-cluster"></a>Utilizzare hello SAS con un cluster esistente

Se si dispone di un cluster esistente basata su Linux, è possibile aggiungere hello SAS toohello **core sito** configurazione utilizzando hello alla procedura seguente:

1. Aprire hello Ambari web dell'interfaccia utente per il cluster. indirizzo Hello questa pagina è https://YOURCLUSTERNAME.azurehdinsight.net. Quando richiesto, eseguire l'autenticazione toohello cluster utilizzando il nome amministratore hello (amministratore) e la password utilizzati durante la creazione di cluster hello.

2. Hello il lato sinistro di hello Ambari web dell'interfaccia utente, selezionare **HDFS** e quindi selezionare hello **configurazioni** scheda centro hello della pagina hello.

3. Seleziona hello **avanzate** scheda e quindi scorrere fino a individuare hello **dei siti principali personalizzato** sezione.

4. Espandere hello **Custom. core-sito** sezione, quindi Fine toohello scorrere e seleziona hello **aggiungere proprietà...**  collegamento. I valori seguenti di hello di utilizzo per hello **chiave** e **valore** campi:

   * **Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net
   * **Valore**: hello SAS restituito da hello applicazione c# o Python è stato eseguito in precedenza

     Sostituire **CONTAINERNAME** con il nome di contenitore hello è usata con un'applicazione hello in c# o SAS. Sostituire **STORAGEACCOUNTNAME** con nome di account di archiviazione hello è stato utilizzato.

5. Fare clic su hello **Aggiungi** toosave questa chiave e valore, quindi fare clic su hello **salvare** pulsante toosave modifiche alla configurazione di hello. Quando richiesto, aggiungere una descrizione della modifica di hello ("aggiunta di accesso all'archiviazione SAS", ad esempio) e quindi fare clic su **salvare**.

    Fare clic su **OK** quando le modifiche di hello sono state completate.

   > [!IMPORTANT]
   > Prima di hello modifica abbia effetto, è necessario riavviare diversi servizi.

6. Nell'interfaccia utente web di Ambari hello, selezionare **HDFS** elenco hello hello a sinistra e quindi selezionare **riavviare tutti** da hello **azioni servizio** hello destra elenco a discesa. Quando richiesto, selezionare **Turn on maintenance mode** e quindi selezionare __Conform Restart All".

    Ripetere il processo per MapReduce2 e YARN.

7. Dopo aver riavviato servizi hello, selezionare ciascuno di essi e disabilitare la modalità di manutenzione da hello **azioni servizio** elenco a discesa.

## <a name="test-restricted-access"></a>Testare l'accesso limitato

tooverify che con accesso limitato, hello di utilizzo dei seguenti metodi:

* Per **basati su Windows** cluster HDInsight, utilizzare cluster toohello tooconnect di Desktop remoto. Per ulteriori informazioni, vedere [connettersi tramite RDP tooHDInsight](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

    Una volta connessi, utilizzare hello **Hadoop della riga di comando** icona su hello desktop tooopen un prompt dei comandi.

* Per **basati su Linux** cluster HDInsight, usare SSH tooconnect toohello cluster. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Una volta connessi toohello cluster, utilizzare hello tooverify passaggi che è possibile solo lettura e l'elenco di elementi presenti in account di archiviazione SAS hello seguenti:

1. comando seguente dal prompt dei comandi hello hello del contenuto di hello toolist del contenitore di hello, utilizzare: 

    ```bash
    hdfs dfs -ls wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/
    ```

    Sostituire **SASCONTAINER** con nome hello del contenitore di hello creato per l'account di archiviazione SAS hello. Sostituire **SASACCOUNTNAME** con nome hello hello dell'account di archiviazione utilizzato per hello SAS.

    elenco di Hello include file hello caricate quando sono state create contenitore hello e SAS.

2. Utilizzare hello seguente tooverify comando che è possibile leggere il contenuto di hello del file hello. Sostituire hello **SASCONTAINER** e **SASACCOUNTNAME** come passaggio precedente hello. Sostituire **FILENAME** con nome hello del file hello visualizzato nel comando precedente hello:

    ```bash
    hdfs dfs -text wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME
    ```

    Questo comando Elenca il contenuto di hello del file hello.

3. Utilizzare hello successivo comando toodownload hello file toohello file system locale:

    ```bash
    hdfs dfs -get wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt
    ```

    Questo comando Scarica hello tooa locale da un file denominato **testfile.txt**.

4. Comando che segue di hello utilizzare tooupload hello file locale tooa nuovo file denominato **testupload.txt** su hello archiviazione SAS:

    ```bash
    hdfs dfs -put testfile.txt wasb://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt
    ```

    Viene visualizzato un toohello simile messaggio seguente testo:

        put: java.io.IOException

    Questo errore si verifica perché il percorso di archiviazione hello lettura + solo nell'elenco. Comando che segue di hello utilizzare dati di hello tooput in hello nell'archivio predefinito per i cluster di hello, che è accessibile in scrittura:

    ```bash
    hdfs dfs -put testfile.txt wasb:///testupload.txt
    ```

    Questa volta, hello operazione deve essere completata correttamente.

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="a-task-was-canceled"></a>Un'attività è stata annullata

**Sintomi**: durante la creazione di un cluster utilizzando uno script di PowerShell hello, potrebbe essere visualizzato hello seguente messaggio di errore:

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

**Causa**: questo errore può verificarsi se si utilizza una password per l'utente di amministrazione/HTTP hello per cluster hello o (per i cluster basati su Linux) utente SSH hello.

**Risoluzione**: utilizzare una password che soddisfi i seguenti criteri hello:

* La lunghezza non può essere inferiore a 10 caratteri
* Deve contenere almeno una cifra
* Deve contenere almeno un carattere non alfanumerico
* Deve contenere almeno una lettera maiuscola o minuscola

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come tooadd archiviazione ad accesso limitato tooyour cluster HDInsight, informazioni su altri toowork modi con i dati sul cluster:

* [Usare Hive con HDInsight](hdinsight-use-hive.md)
* [Usare Pig con HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con HDInsight](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
