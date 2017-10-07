---
title: gli scenari di analitica avanzati per Azure Machine Learning aaaIdentify | Documenti Microsoft
description: Selezionare scenari appropriato di hello per questo avanzate analitica predittiva con hello processo di analisi scientifica dei dati del Team.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52c6bb10d6df4f640a4f66cf17cf4993cc1067b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a>Scenari per l'analisi avanzata in Azure Machine Learning
Questo articolo vengono illustrati vari hello origini dati di esempio e scenari di destinazione che possono essere gestiti da hello [Team Data Science processo (TDSP)](data-science-process-overview.md). Hello TDSP fornisce un approccio sistematico per i team toocollaborate sulla compilazione di applicazioni intelligenti. scenari di Hello forniti in questa sezione illustrano le opzioni disponibili nel flusso di lavoro di hello l'elaborazione dati che variano in base alle caratteristiche dei dati hello, percorsi di origine e il repository di destinazione in Azure.

Hello **albero delle decisioni** per scenari di esempio hello appropriata per i dati e l'obiettivo di selezione viene presentata nell'ultima sezione hello.

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

Ognuno di hello le sezioni seguenti viene presentato uno scenario di esempio. Per ogni scenario vengono elencati un flusso di dati scientifici o di analisi avanzata possibile e le risorse di Azure di supporto.

> [!NOTE]
> **Per tutti i seguenti scenari hello, è necessario:**
> <br/>
> 
> * [Creare un account di archiviazione](../storage/common/storage-create-storage-account.md)
>   <br/>
> * [Creare un'area di lavoro di Machine Learning di Azure](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a>Scenario \#1: toomedium piccoli set di dati tabulari in un file locale
![File locali toomedium Small][1]

#### <a name="additional-azure-resources-none"></a>Risorse di Azure aggiuntive: nessuna
1. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
2. Caricare un set di dati.
3. Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.

## <a name="smalllocalprocess"></a>Scenario \#2: toomedium piccoli set di dati di file locali che richiedono l'elaborazione
![File locali toomedium di piccole dimensioni con l'elaborazione][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Risorse di Azure aggiuntive: macchina virtuale di Azure (server IPython Notebook)
1. Creare una macchina virtuale di Azure Virtual Machine che esegue IPython Notebook.
2. Caricare dati tooan contenitore di archiviazione Azure.
3. Pre-elaborare e pulire i dati in IPython Notebook, accedere ai dati dal contenitore di archiviazione di Azure.
4. Trasformare dati toocleaned, sotto forma di tabella.
5. Salvare i dati trasformati in BLOB di Azure.
6. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
7. Leggere i dati di hello dal BLOB di Azure utilizzando hello [l'importazione dei dati] [ import-data] modulo.
8. Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.

## <a name="largelocal"></a>Scenario \#3: Set di dati di grandi dimensioni in file locali, con destinazione BLOB di Azure
![File locali di grandi dimensioni][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a>Risorse di Azure aggiuntive: macchina virtuale di Azure (server IPython Notebook)
1. Creare una macchina virtuale di Azure Virtual Machine che esegue IPython Notebook.
2. Caricare dati tooan contenitore di archiviazione Azure.
3. Pre-elaborare e pulire i dati in IPython Notebook, accedere ai dati dai BLOB di Azure.
4. Trasformare dati toocleaned, tabulare, se necessario.
5. Esaminare i dati e creare le funzionalità necessarie.
6. Estrarre un campione di dati medio-piccolo.
7. Salvare i dati campionato hello in BLOB di Azure.
8. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Leggere i dati di hello dal BLOB di Azure utilizzando hello [l'importazione dei dati] [ import-data] modulo.
10. Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.

## <a name="smalllocaltodb"></a>Scenario \#4: toomedium piccoli set di dati di file locali, come destinazione di SQL Server in una macchina virtuale di Azure
![Toomedium piccoli file locali tooSQL DB in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)
1. Creare una macchina virtuale di Azure Virtual Machine che esegue SQL Server e IPython Notebook.
2. Caricare dati tooan contenitore di archiviazione Azure.
3. Pre-elaborare e pulire i dati nel contenitore di archiviazione di Azure usando IPython Notebook.
4. Trasformare dati toocleaned, tabulare, se necessario.
5. Salvare i file di dati locale tooVM (IPython Notebook è in esecuzione nella macchina virtuale, le unità locali fare riferimento a unità tooVM).
6. Caricare il database del Server tooSQL dati in esecuzione in una macchina virtuale di Azure.
   
   Opzione \#1: Uso di SQL Server Management Studio.
   
   * Account di accesso tooSQL macchina virtuale Server
   * Eseguire SQL Server Management Studio
   * Creare tabelle di database e di destinazione
   * Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi dai file di macchina virtuale locale.
   
   Opzione \#2: L'uso di IPython Notebook non è consigliabile per i set di dati di medie o grandi dimensioni
   
   <!-- -->    
   * Utilizzare tooaccess di stringa di connessione ODBC SQL Server nella macchina virtuale.
   * Creare tabelle di database e di destinazione
   * Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi dai file di macchina virtuale locale.
7. Esaminare i dati e creare le funzionalità necessarie. Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello. Nota solo hello query necessaria toocreate li.
8. Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.
9. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
10. Dati di lettura hello direttamente da hello SQL Server tramite hello [l'importazione dei dati] [ import-data] modulo. Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.
11. Compilare un flusso di esperimento di Azure Machine Learning iniziando con il set di dati inserito.

## <a name="largelocaltodb"></a>Scenario \#5: Set di dati di grandi dimensioni in file locali, con destinazione SQL Server in una macchina virtuale di Azure
![File locale di grandi dimensioni tooSQL DB in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)
1. Creare una macchina virtuale di Azure che esegue SQL Server e il server IPython Notebook.
2. Caricare dati tooan contenitore di archiviazione Azure.
3. (Facoltativo) Pre-elaborare e pulire i dati.
   
   a.  Pre-elaborare e pulire i dati in IPython Notebook, accedendo ai dati da Azure
   
       blobs.
   
   b.  Trasformare dati toocleaned, tabulare, se necessario.
   
   c.  Salvare i file di dati locale tooVM (IPython Notebook è in esecuzione nella macchina virtuale, le unità locali fare riferimento a unità tooVM).
4. Caricare il database del Server tooSQL dati in esecuzione in una macchina virtuale di Azure.
   
   a.  Account di accesso tooSQL macchina virtuale di Server.
   
   b.  Se i dati non sono ancora stati salvati, scaricare i file di dati da Azure
   
       storage container toolocal-VM folder.
   
   c.  Eseguire SQL Server Management Studio
   
   d.  Creare tabelle di database e di destinazione
   
   e.  Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi.
   
   f.  Se sono necessari i join di tabelle, creare indici tooexpedite join.
   
   > [!NOTE]
   > Per un caricamento più rapido delle dimensioni di dati di grandi dimensioni, è consigliabile creare tabelle partizionate e importazione bulk hello in parallelo. Per ulteriori informazioni, vedere [tooSQL importazione parallela dei dati le tabelle partizionate](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Esaminare i dati e creare le funzionalità necessarie. Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello. Nota solo hello query necessaria toocreate li.
6. Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.
7. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Dati di lettura hello direttamente da hello SQL Server tramite hello [l'importazione dei dati] [ import-data] modulo. Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.
9. Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato

## <a name="largedbtodb"></a>Scenario \#6: Set di dati di grandi dimensioni in un database SQL Server locale, con destinazione SQL Server nella macchina virtuale di Azure
![Database di SQL Server locale tooSQL DB grandi dimensioni in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)
1. Creare una macchina virtuale di Azure che esegue SQL Server e il server IPython Notebook.
2. Utilizzare uno dei dati hello esportare i dati di hello tooexport metodi dai file toodump di SQL Server.
   
   > [!NOTE]
   > Se si decide di toomove tutti i dati dal database locale di hello, un'alternativa (più veloce) metodo toomove hello completo del database toothe istanza SQL Server in Azure. Ignorare i dati di hello passaggi tooexport, creare database e database di destinazione / importazione a caricamento dati toohello e seguire il metodo alternativo di hello.
   > 
   > 
3. Caricare contenitore di archiviazione tooAzure file dump.
4. Caricare i dati di hello tooa database di SQL Server in esecuzione in una macchina virtuale di Azure.
   
   a.  Account di accesso toohello macchina virtuale SQL Server.
   
   b.  Scaricare i file di dati da una cartella di archiviazione di Azure contenitore toohello-VM locale.
   
   c.  Eseguire SQL Server Management Studio
   
   d.  Creare tabelle di database e di destinazione
   
   e.  Utilizzare uno dei bulk hello Importa i dati di hello tooload metodi.
   
   f.  Se sono necessari i join di tabelle, creare indici tooexpedite join.
   
   > [!NOTE]
   > Per un caricamento più rapido delle dimensioni di dati di grandi dimensioni, creare le tabelle partizionate e l'importazione dei dati hello toobulk in parallelo. Per ulteriori informazioni, vedere [tooSQL importazione parallela dei dati le tabelle partizionate](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).
   > 
   > 
5. Esaminare i dati e creare le funzionalità necessarie. Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello. Nota solo hello query necessaria toocreate li.
6. Scegliere le dimensioni del campione di dati, se necessario e/o lo si desidera.
7. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
8. Dati di lettura hello direttamente da hello SQL Server tramite hello [l'importazione dei dati] [ import-data] modulo. Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.
9. Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.

### <a name="alternate-method-toocopy-a-full-database-from-an-on-premises--sql-server-tooazure-sql-database"></a>Metodo alternativo toocopy completo di un database da un tooAzure di SQL Server on-premise SQL Database
![Collegamento e scollegamento di local DB tooSQL DB in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a>Risorse di Azure aggiuntive: macchina virtuale di Azure (SQL Server/server IPython Notebook)
tooreplicate hello intero database di SQL Server nella macchina virtuale SQL Server, è necessario copiare un database da un server dei percorsi/tooanother, presupponendo che il database hello è possibile portare temporaneamente offline. A tale scopo, in Esplora oggetti di SQL Server Management Studio hello o utilizzando i comandi Transact-SQL equivalenti hello.

1. Scollegare il database di hello nel percorso di origine hello. Per altre informazioni, vedere [Scollegamento di un database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).
2. Nella finestra di Esplora risorse o prompt dei comandi di Windows hello copia scollegata i file di database o file e file di log o percorso di destinazione dei file toohello su hello macchina virtuale di SQL Server in Azure.
3. Collegare l'istanza di SQL Server di destinazione di hello copiato i file toohello. Per altre informazioni, vedere [Collegare un database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).

[Spostamento di un database tramite la funzionalità di scollegamento e collegamento (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)

## <a name="largedbtohive"></a>Scenario \#7: Big Data nei file locali, con destinazione il database Hive nei cluster Hadoop di Azure HDInsight
![Big Data nell'Hive di destinazione locale][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a>Risorse di Azure aggiuntive: cluster Hadoop di Azure HDInsight e macchina virtuale di Azure (server IPython Notebook)
1. Creare una macchina virtuale di Azure che esegue il server IPython Notebook.
2. Creare un cluster Hadoop di Azure HDInsight
3. (Facoltativo) Pre-elaborare e pulire i dati.
   
   a.  Pre-elaborare e pulire i dati in IPython Notebook, accedendo ai dati da Azure
   
       blobs.
   
   b.  Trasformare dati toocleaned, tabulare, se necessario.
   
   c.  Salvare i file di dati locale tooVM (IPython Notebook è in esecuzione nella macchina virtuale, le unità locali fare riferimento a unità tooVM).
4. Caricare contenitore predefinito toohello di dati di un cluster Hadoop hello selezionato nel passaggio hello 2.
5. Caricamento dati tooHive database cluster Azure HDInsight Hadoop.
   
   a.  Accedi toohello nodo head del cluster Hadoop hello
   
   b.  Aprire hello Hadoop della riga di comando.
   
   c.  Immettere una directory radice di Hive hello dal comando `cd %hive_home%\bin` nella riga di comando di Hadoop.
   
   d.  Eseguire hello Hive query toocreate database e le tabelle e caricare i dati da tabelle tooHive di archiviazione blob.
   
   > [!NOTE]
   > Se i dati di hello sono grandi, gli utenti possono creare tabella Hive hello con partizioni. Quindi, gli utenti possono usare un `for` ciclo in hello riga di comando di Hadoop su dati di tooload hello nodo head in tabella Hive hello partizionata dalla partizione.
   > 
   > 
6. Esaminare i dati e creare le funzionalità necessarie nella riga di comando di Hadoop. Si noti che le funzionalità di hello non è necessitino toobe materializzato in tabelle di database hello. Nota solo hello query necessaria toocreate li.
   
   a.  Accedi toohello nodo head del cluster Hadoop hello
   
   b.  Aprire hello Hadoop della riga di comando.
   
   c.  Immettere una directory radice di Hive hello dal comando `cd %hive_home%\bin` nella riga di comando di Hadoop.
   
   d.  Eseguire le query Hive hello nella riga di comando di Hadoop nel nodo head di hello di dati di hello tooexplore cluster Hadoop hello e creare le funzionalità in base alle esigenze.
7. Se necessario e/o lo si desidera, esempio hello toofit di dati in Azure Machine Learning Studio.
8. Accedi toohello [Azure Machine Learning Studio](https://studio.azureml.net/).
9. Leggere dati hello direttamente da hello `Hive Queries` utilizzando hello [l'importazione dei dati] [ import-data] modulo. Incolla hello query necessarie che estrae i campi, crea le funzionalità e campionamento dei dati, se necessario direttamente nella hello [l'importazione dei dati] [ import-data] query.
10. Semplificare il flusso di esperimento di Azure Machine Learning iniziando con il set di dati caricato.

## <a name="decisiontree"></a>Albero delle decisioni per la scelta degli scenari
- - -
Hello diagramma seguente sono riepilogati gli scenari di hello descritti in precedenza e hello avanzate processo Analitica e la tecnologia le scelte effettuate che consentono di accedere tooeach degli scenari indicati in modo dettagliato hello. Si noti che potrebbe richiedere l'elaborazione dati, l'esplorazione, progettazione di funzionalità e campionamento inserire in uno o più metodo/ambiente - origine hello, intermedio, e/o ambienti di destinazione e possono essere eseguite in modo iterativo, in base alle esigenze. diagramma di Hello solo funge da un'illustrazione di alcune delle possibili flussi e non fornisce un'enumerazione completa.

![Scenari della procedura dettagliata del processo di analisi scientifica][8]

### <a name="advanced-analytics-in-action-examples"></a>Analisi avanzata in esempi di azioni
Per procedure dettagliate di Azure Machine Learning end-to-end che impiegano hello avanzate processo Analitica e la tecnologia utilizzano set di dati pubblici, vedere:

* [Processo di analisi scientifica dei dati per i team in azione: uso di SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).
* [Processo di analisi scientifica dei dati per i team in azione: uso dei cluster Hadoop di HDInsight](machine-learning-data-science-process-hive-walkthrough.md).

[1]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
