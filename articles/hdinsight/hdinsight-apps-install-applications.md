---
title: applicazioni di Hadoop aaaInstall terze parti in Azure HDInsight | Documenti Microsoft
description: Informazioni su come applicazioni di Hadoop tooinstall terze parti in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: eaf5904d-41e2-4a5f-8bec-9dde069039c2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/16/2017
ms.author: jgao
ms.openlocfilehash: 00071517c81a17c01dccedf9e8dd5d0cabb38567
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-third-party-hadoop-applications-on-azure-hdinsight"></a>Installare applicazioni Hadoop di terze parti in Azure HDInsight

In questo articolo viene illustrato come tooinstall un'applicazione di Hadoop di terze parti già pubblicata in Azure HDInsight. Per istruzioni sull'installazione di un'applicazione personalizzata, vedere l'articolo su come [installare applicazioni HDInsight personalizzate](hdinsight-apps-install-custom-applications.md).

Un'applicazione HDInsight è un'applicazione che gli utenti possono installare in un cluster HDInsight basato su Linux. Queste applicazioni possono essere sviluppate da Microsoft, da fornitori di software indipendenti (ISV) o dall'utente.  

Attualmente sono disponibili quattro applicazioni pubblicate:

* **DDS DATAIKU in HDInsight**: Dataiku DSS (Studio analisi scientifica dei dati) è un software che consente di dati tooprototype professionisti (esperti di dati, gli analisti aziendali, gli sviluppatori...), compilare e distribuire servizi altamente specifici che trasformano i dati non elaborati in stime ripercussioni sulle business.
* **Datameer**: [Datameer](http://www.datameer.com/documentation/display/DAS50/Home?ls=Partners&lsd=Microsoft&c=Partners&cd=Microsoft) offre gli analisti toodiscover una modalità interattiva, analizzare e visualizzare i risultati di hello sui Big Data. Pull facilmente in altre origini dati nuove relazioni toodiscover e ottenere risposte hello che è svolta in tempi rapidi.
* **Agente di raccolta dati Streamsets per HDnsight** offre un ambiente completo di sviluppo integrato (IDE) che consente di progettare, testare, distribuire e gestire qualsiasi per qualsiasi inserimento le pipeline che mesh batch e flusso di dati e includono una varietà di trasformazioni nel flusso, tutto senza dover toowrite di codice personalizzato. 
* **Contenitori CDAP per HDInsight** fornisce hello unificata prima la piattaforma di integrazione per i big data che riduce tooproduction ora hello per le applicazioni di dati e laghi dati dell'80%. Questa applicazione supporta solo i cluster Standard HBase 3.4.
* **Intelligenza artificiale H2O per HDInsight (Beta)** H2O spumanti acqua supporta hello seguenti algoritmi: GLM, Naïve Bayes, foresta casuale distribuito, macchina Boosting sfumatura, Deep Neural Networks, Deep learning, K-medie, PCA, Modelli di classificazione bassi generalizzati, il rilevamento di anomalie e Autoencoders.
* **Kyligence Analytics Platform**: Kyligence Analytics Platform (KAP) è un data warehouse di livello aziendale con tecnologia Apache Kylin e Apache Hadoop che supporta una latenza di query inferiore al secondo su set di dati di enormi dimensioni e semplifica l'analisi dei dati per gli utenti business e gli analisti. 
* **SnapLogic Hadooplex** hello SnapLogic Hadooplex in esecuzione in HDInsight consente insights di toobusiness tooget clienti più veloce, fornendo l'inserimento di dati in modalità self-service e di preparazione da qualsiasi toohello origine cloud di Microsoft Azure piattaforma.
* **Server dei processi Spark per KNIME Spark esecutore** Spark Server dei processi per l'esecutore di Spark KNIME è usato tooconnect hello KNIME Analitica piattaforma tooHDInsight cluster.

Hello istruzioni fornite in questo articolo si usa il portale di Azure. È anche possibile esportare il modello di Azure Resource Manager hello dal portale hello o ottenere una copia del modello di gestione risorse di hello fornitori e usare Azure PowerShell e un modello di hello toodeploy CLI di Azure.  Vedere [Creare cluster Hadoop basati su Linux in HDInsight tramite modelli ARM](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

## <a name="prerequisites"></a>Prerequisiti
Se si desidera tooinstall HDInsight applicazioni su un cluster HDInsight esistente, è necessario disporre di un cluster HDInsight. toocreate uno, vedere [creare cluster](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). È anche possibile installare applicazioni HDInsight quando si crea un cluster HDInsight.

## <a name="install-applications-tooexisting-clusters"></a>Installare i cluster tooexisting applicazioni
Hello procedura riportata di seguito illustra come tooinstall HDInsight applicazioni tooan cluster HDInsight esistente.

**tooinstall un'applicazione di HDInsight**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** nel menu a sinistra di hello.  Se non è visualizzato, fare clic su **Altri servizi** e quindi su **Cluster HDInsight**.
3. Fare clic su un cluster HDInsight.  Se non ci sono cluster disponibili, è necessario crearne uno.  Vedere [Creare cluster](hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).
4. Fare clic su **applicazioni** in hello **configurazioni** categoria. Verrà visualizzato un elenco delle applicazioni installate. Se non è possibile trovare le applicazioni, significa che non vi è alcuna applicazione per questa versione del cluster HDInsight hello.
   
    ![Menu del portale Applicazioni di HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-portal-menu.png)
5. Fare clic su **Aggiungi** dal menu Pannello hello. 
   
    ![App installate in Applicazioni di HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps.png)
   
    Verrà visualizzato un elenco delle applicazioni HDInsight esistenti.
   
    ![Applicazioni disponibili in Applicazioni di HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-list.png)
6. Fare clic su una delle applicazioni di hello, accettare i termini legali specifici hello e quindi fare clic su **selezionare**.

È possibile visualizzare lo stato di installazione hello dalle notifiche portale hello (fare clic sull'icona di campanello hello nella parte superiore di hello del portale hello). Dopo aver hello l'applicazione è installata, un'applicazione hello verrà visualizzati nel pannello App installate hello.

## <a name="install-applications-during-cluster-creation"></a>Installare applicazioni durante la creazione del cluster
Si dispone di hello opzione tooinstall HDInsight applicazioni quando si crea un cluster. Durante il processo di hello, HDInsight applicazioni installate dopo cluster hello viene creato ed è in stato di esecuzione hello. Hello procedura riportata di seguito viene illustrato come le applicazioni di HDInsight tooinstall quando si crea un cluster.

**tooinstall un'applicazione di HDInsight**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **Nuovo**, su **Analisi dei dati** e quindi su **HDInsight**.
3. Inserire il **Nome cluster**: il nome deve essere univoco a livello globale.
4. Fare clic su **sottoscrizione** tooselect hello sottoscrizione di Azure che viene utilizzato per il cluster hello.
5. Fare clic su **Selezionare il tipo di cluster**, quindi selezionare:
   
   * **Tipo di cluster**: se non si conosce quali toochoose, selezionare **Hadoop**. È il tipo di cluster più diffuso hello.
   * **Sistema operativo**: selezionare **Linux**.
   * **Versione**: utilizzare versione di hello predefinita se non si conosce quali toochoose. Per altre informazioni, vedere [Versioni del cluster HDInsight](hdinsight-component-versioning.md).
   * **Livello del cluster**: HDInsight di Azure fornisce offerte di cloud hello dati in due categorie: livello Standard e Premium. Per ulteriori informazioni, vedere [Livelli di cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers).
6. Fare clic su **applicazioni**, fare clic su uno dei hello pubblicazione delle applicazioni, quindi **selezionare**.
7. Fare clic su **credenziali** e quindi immettere una password per l'utente amministratore hello. È inoltre necessario tooenter un **nome utente SSH** e un **PASSWORD** o **chiave pubblica**, ovvero utente SSH di hello tooauthenticate utilizzato. Utilizzo di una chiave pubblica è hello approccio consigliato. Fare clic su **selezionare** durante la configurazione di credenziali di hello inferiore toosave hello.
8. Fare clic su **origine dati**, selezionare una delle hello gli account di archiviazione esistente o creare un nuovo toobe di account di archiviazione utilizzato come account di archiviazione predefinito hello per cluster hello.
9. Fare clic su **gruppo di risorse** tooselect una risorsa esistente di gruppo, oppure fare clic su **New** toocreate un nuovo gruppo di risorse
10. In hello **nuovo HDInsight Cluster** pannello, assicurarsi che **Pin tooStartboard** sia selezionata e quindi fare clic su **crea**. 

## <a name="list-installed-hdinsight-apps-and-properties"></a>Elencare le app HDInsight installate e le proprietà
portale Hello mostra che un elenco di hello installate le applicazioni di HDInsight per un cluster e le proprietà di hello di ogni applicazione installata.

**proprietà dell'applicazione e visualizzazione di HDInsight toolist**

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Fare clic su **cluster HDInsight** nel menu a sinistra di hello.  Se non è visualizzato, fare clic su **Esplora** e quindi su **Cluster HDInsight**.
3. Fare clic su un cluster HDInsight.
4. Da hello **impostazioni** pannello, fare clic su **applicazioni** in hello **generale** categoria. Pannello App installate Hello Elenca tutte le applicazioni hello installato. 
   
    ![App installate in Applicazioni di HDInsight](./media/hdinsight-apps-install-applications/hdinsight-apps-installed-apps-with-apps.png)
5. Fare clic su una delle proprietà di hello tooshow applicazioni hello installato. Pannello proprietà Hello Elenca:
   
   * Nome dell'app: nome all'applicazione.
   * Stato: stato dell'applicazione. 
   * Pagina Web: hello URL dell'applicazione web hello di aver distribuito il nodo di edge toohello. credenziali Hello sono identico a quello delle credenziali utente hello HTTP che si sono configurati per il cluster hello hello.
   * Endpoint HTTP: credenziali hello sono identico a quello delle credenziali utente hello HTTP che si sono configurati per il cluster hello hello. 
   * Endpoint SSH: È possibile usare SSH tooconnect toohello bordo nodo. le credenziali di Hello SSH sono uguali a quelli delle credenziali utente SSH hello che si sono configurati per cluster hello hello. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
6. Fare doppio clic su un'applicazione hello toodelete un'applicazione e quindi fare clic su **eliminare** dal menu di scelta rapida hello.

## <a name="connect-toohello-edge-node"></a>Connettere toohello bordo nodo
È possibile connettere il nodo di edge toohello tramite HTTP e SSH. sono disponibili informazioni sull'endpoint Hello hello [portale](#list-installed-hdinsight-apps-and-properties). Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

le credenziali dell'endpoint HTTP Hello sono hello HTTP le credenziali dell'utente è stato configurato per il cluster HDInsight hello; le credenziali dell'endpoint SSH Hello sono le credenziali di SSH hello che è stato configurato per il cluster HDInsight hello.

## <a name="troubleshoot"></a>Risoluzione dei problemi
Vedere [problemi relativi all'installazione di hello](hdinsight-apps-install-custom-applications.md#troubleshoot-the-installation).

## <a name="next-steps"></a>Passaggi successivi
* [Installare le applicazioni personalizzate HDInsight](hdinsight-apps-install-custom-applications.md): informazioni su come toodeploy un tooHDInsight di applicazione non pubblicata di HDInsight.
* [Pubblicare applicazioni HDInsight](hdinsight-apps-publish-applications.md): informazioni su come toopublish il tooAzure di applicazioni personalizzate HDInsight Marketplace.
* [MSDN: Installare un'applicazione di HDInsight](https://msdn.microsoft.com/library/mt706515.aspx): informazioni su come toodefine HDInsight applicazioni.
* [Personalizzazione dei cluster HDInsight basati su Linux con azione Script](hdinsight-hadoop-customize-cluster-linux.md): informazioni su come applicazioni aggiuntive di toouse genera Script azione tooinstall.
* [Creare i cluster basati su Linux, Hadoop in HDInsight mediante modelli di gestione risorse](hdinsight-hadoop-create-linux-clusters-arm-templates.md): informazioni su come toocreate modelli tramite Gestione risorse toocall HDInsight cluster.
* [Usare i nodi del bordo vuoto in HDInsight](hdinsight-apps-use-edge-node.md): informazioni su come toouse vuota bordo nodo per l'accesso a cluster HDInsight, testing delle applicazioni di HDInsight e hosting di applicazioni di HDInsight.

