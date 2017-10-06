---
title: applicazioni di HDInsight aaaPublish - Azure | Documenti Microsoft
description: Informazioni su come toocreate e pubblicare le applicazioni di HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 14aef891-7a37-4cf1-8f7d-ca923565c783
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 7da0aa53828563e50ef372df901e1ba541fb40be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-hdinsight-applications-into-hello-azure-marketplace"></a>Pubblicare applicazioni HDInsight in hello Azure Marketplace
Un'applicazione HDInsight è un'applicazione che gli utenti possono installare in un cluster HDInsight basato su Linux. Queste applicazioni possono essere sviluppate da Microsoft, da fornitori di software indipendenti (ISV) o dall'utente. In questo articolo viene illustrato come toopublish un'applicazione di HDInsight in hello Azure Marketplace.  Per informazioni generali sulla pubblicazione in hello Azure Marketplace, vedere [pubblicare un toohello offerta Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md).

Le applicazioni di HDInsight utilizzare hello *portare il propria licenza (BYOL)* modello, in cui provider dell'applicazione è responsabile della gestione delle licenze tooend applicazione hello-gli utenti e gli utenti finali addebitato solo da Azure per le risorse di hello sono creare, ad esempio cluster HDInsight hello e relative macchine virtuali o i nodi. Attualmente, la fatturazione per l'applicazione hello stessa non viene eseguita tramite Azure.

Altro articolo correlato all'applicazione HDInsight:

* [Installare le applicazioni di HDInsight](hdinsight-apps-install-applications.md): informazioni su come tooinstall un tooyour applicazione HDInsight cluster.
* [Installare le applicazioni personalizzate HDInsight](hdinsight-apps-install-custom-applications.md): informazioni su come tooinstall e test applicazioni personalizzate di HDInsight.

## <a name="prerequisites"></a>Prerequisiti
toosubmit marketplace toohello applicazione personalizzata, è necessario aver creato e testato l'applicazione personalizzata. Vedere hello seguenti articoli:

* [Installare le applicazioni personalizzate HDInsight](hdinsight-apps-install-custom-applications.md): informazioni su come tooinstall e test applicazioni personalizzate di HDInsight.

È anche necessario registrare l'account per sviluppatore. Vedere [pubblicare un toohello offerta Azure Marketplace](../marketplace-publishing/marketplace-publishing-getting-started.md) e [creare un account di Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).

## <a name="define-application"></a>Definire l'applicazione
Sono disponibili due passaggi per la pubblicazione di applicazioni toohello Azure Marketplace.  Definire innanzitutto un **createUiDef.json** tooindicate file che l'applicazione cluster è compatibile con; e quindi pubblicare il modello di hello da hello portale di Azure. Hello seguente sezione è riportato un esempio di file createUiDef.json.

    {
        "handler": "Microsoft.HDInsight",
        "version": "0.0.1-preview",
        "clusterFilters": {
            "types": ["Hadoop", "HBase", "Storm", "Spark"],
            "tiers": ["Standard", "Premium"],
            "versions": ["3.4"]
        }
    }


| Campo | Descrizione | Valori possibili |
| --- | --- | --- |
| types |tipi di cluster Hello sia compatibile con l'applicazione hello. |Hadoop, HBase, Storm, Spark (o qualsiasi combinazione di questi valori) |
| tiers |Hello livelli applicazione hello è compatibile con cluster. |Standard, Premium (o entrambi) |
| versions |è compatibile con i tipi di cluster di HDInsight Hello hello dell'applicazione. |3.4 |

## <a name="application-install-script"></a>Script di installazione dell'applicazione
Ogni volta che un'applicazione è installata in un cluster (uno esistente o uno nuovo), viene creato un nodo del bordo e script di installazione dell'applicazione hello viene eseguito su di esso.
  > [!IMPORTANT]
  > nome Hello di nomi di script di installazione dell'applicazione hello deve essere univoco per un determinato cluster con hello seguente formato.
  > 
  > name": "[concat('hue-install-v0','-' ,uniquestring(‘applicationName’)]"
  > 
  > Sono presenti tre nome di script toohello parti:
  > 
  > 1. Un prefisso del nome dello script, che comprende il nome di applicazione di hello o un'applicazione toohello rilevanti nome.
  > 2. Un "-" per migliorare la leggibilità.
  > 3. Funzioni stringa univoca con nome dell'applicazione hello come parametro hello.
  > 
  > Un esempio è hello precedente finisce diventando: tonalità-installazione-v0-4wkahss55hlas in hello persistente l'elenco di azioni di script. Per un payload JSON di esempio, vedere [https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json](https://raw.githubusercontent.com/hdinsight/Iaas-Applications/master/Hue/azuredeploy.json).
  > 
script di installazione Hello deve avere hello seguenti caratteristiche:
1. Assicurarsi che script hello è idempotente. Più chiamate toohello script dovrebbe produrre hello stesso risultato.
2. script Hello deve essere con controllo delle versioni in modo corretto. Utilizzare un percorso diverso per lo script hello quando esegue l'aggiornamento o testare le modifiche in modo che i clienti che si sta tentando di un'applicazione hello tooinstall non vengono modificati. 
3. Aggiungere gli script di registrazione adeguate toohello in ogni punto. In genere hello log di script sono hello solo modo toodebug problemi di installazione dell'applicazione.
4. Verificare che chiama tooexternal servizi o le risorse siano adeguate tentativi in modo che l'installazione di hello non è interessata da problemi di rete temporanei.
5. Se lo script di avvio servizi su nodi hello, assicurarsi che i servizi di hello vengono monitorati e configurato toostart automaticamente in caso di riavvio del nodo.

## <a name="package-application"></a>Inserire l'applicazione in un pacchetto
Creare un file ZIP contenente tutti i file necessari per installare le applicazioni HDInsight. È necessario hello file zip in [pubblica applicazione](#publish-application).

* [createUiDefinition.json](#define-application).
* mainTemplate.json. Vedere un esempio in [Installare applicazioni HDInsight personalizzate](hdinsight-apps-install-custom-applications.md).
* Tutti gli script necessari.

> [!NOTE]
> Hello file dell'applicazione (inclusi i file di applicazione web eventuale) può trovarsi in qualsiasi endpoint accessibile pubblicamente.
> 

## <a name="publish-application"></a>Pubblicare l'applicazione
Seguire i seguenti passaggi toopublish un'applicazione di HDInsight hello:

1. Accesso toohello [portale Azure pubblicazione](https://publish.windowsazure.com/).
2. Fare clic su **modelli di soluzioni** da toocreate sinistro hello un nuovo modello di soluzione.
3. Immettere un titolo, quindi fare clic su **Create a new solution template** (Crea un nuovo modello di soluzione).
4. Fare clic su **account crea Dev Center e join hello Azure programma** tooregister azienda se è ancora fatto.  Vedere [Creare un account di Microsoft Developer](../marketplace-publishing/marketplace-publishing-accounts-creation-registration.md).
5. Fare clic su **definire alcuni tooget topologie avviato**. Un modello di soluzione è un tooall "padre" relativo topologie. È possibile definire più topologie in un singolo modello di soluzione/offerta. Quando un'offerta viene inserita toostaging, esso viene inserito con tutte le relative topologie. 
6. Immettere un nome di topologia e quindi fare clic su hello sul segno più.
7. Immettere una nuova versione e quindi fare clic sul segno più hello.
8. Caricamento file zip di hello preparato nel [pacchetto applicazione](#package-application).  
9. Fare clic su **Request Certification**(Richiedi certificazione). team di certificazione Microsoft Hello verrà esaminare i file di hello e certificare topologia hello.

## <a name="next-steps"></a>Passaggi successivi
* [Installare le applicazioni di HDInsight](hdinsight-apps-install-applications.md): informazioni su come tooinstall un tooyour applicazione HDInsight cluster.
* [Installare le applicazioni personalizzate HDInsight](hdinsight-apps-install-custom-applications.md): informazioni su come toodeploy un tooHDInsight di applicazione non pubblicata di HDInsight.
* [Personalizzazione dei cluster HDInsight basati su Linux con azione Script](hdinsight-hadoop-customize-cluster-linux.md): informazioni su come applicazioni aggiuntive di toouse genera Script azione tooinstall.
* [Creare i cluster basati su Linux, Hadoop in HDInsight mediante modelli di gestione risorse di Azure](hdinsight-hadoop-create-linux-clusters-arm-templates.md): informazioni su come toocreate modelli tramite Gestione risorse toocall HDInsight cluster.
* [Usare i nodi del bordo vuoto in HDInsight](hdinsight-apps-use-edge-node.md): informazioni su come toouse vuota bordo nodo per l'accesso a cluster HDInsight, testing delle applicazioni di HDInsight e hosting di applicazioni di HDInsight.

