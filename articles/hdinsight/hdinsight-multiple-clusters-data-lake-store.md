---
title: "HDInsight più cluster con un account archivio Azure Data Lake - Azure aaaUse | Documenti Microsoft"
description: "Informazioni su come toouse più di un HDInsight cluster con un singolo account archivio Data Lake"
keywords: archiviazione hdinsight, hdfs, dati strutturati, dati non strutturati, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/02/2017
ms.author: nitinme
ms.openlocfilehash: 3a125b91fcc1e436270a1bd349f7a2d8f27e06fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-multiple-hdinsight-clusters-with-an-azure-data-lake-store-account"></a>Usare più cluster HDInsight con un account Azure Data Lake Store

A partire dalla versione 3.5 di HDInsight, è possibile creare cluster HDInsight con account archivio Azure Data Lake come file System predefinito hello.
Supportando l'archiviazione illimitata, Data Lake Store è ideale non solo per l'hosting di grandi quantità di dati, ma anche per l'hosting di più cluster HDInsight che condividono un unico account Data Lake Store. Per instructionson come toocreate un HDInsight cluster con archivio Data Lake come archiviazione hello, vedere [HDInsight creare cluster con archivio Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Questo articolo fornisce amministratore dell'archivio Data Lake toohello indicazioni per la configurazione di un singolo e condivise Account Data Lake archiviare che può essere utilizzato in più **active** cluster HDInsight. Questi consigli si applicano toohosting Hadoop protetto nonché non sicure più cluster in un account archivio Data Lake condiviso.


## <a name="data-lake-store-file-and-folder-level-acls"></a>ACL a livello di file e cartella di Data Lake Store

Hello parte restante di questo articolo si presuppone che esista una buona conoscenza dei file e cartelle livello ACL nell'archivio Azure Data Lake, come descritto in dettaglio [controllo degli accessi in archivio Azure Data Lake](../data-lake-store/data-lake-store-access-control.md).

## <a name="data-lake-store-setup-for-multiple-hdinsight-clusters"></a>Configurazione di Data Lake Store per più cluster HDInsight
Richiedere una gerarchia di cartelle a due livelli prendano indicazioni hello tooexplain per l'utilizzo di cluster HDInsight vengono con un account archivio Data Lake. È consigliabile avere un account archivio Data Lake con struttura di cartelle hello **/cluster/finance**. Con questa struttura, tutti i cluster di hello necessari hello Finance organizzazione possono usare /clusters/finance come percorso di archiviazione hello. In futuro, se un'altra organizzazione, ad esempio Marketing, desidera che il cluster HDInsight toocreate con hello stesso account archivio Data Lake, è stato possibile creare /clusters/marketing hello. Per il momento si userà solo **/clusters/finance**.

tooenable toobe di struttura questa cartella può essere utilizzato in modo efficace dai cluster HDInsight, amministratore di archivio Data Lake hello deve assegnare le autorizzazioni appropriate, come descritto nella tabella hello. autorizzazioni Hello illustrate nella tabella hello corrispondono tooAccess ACL e non gli ACL predefinito. 


|Cartella  |Autorizzazioni  |utente proprietario  |gruppo proprietario  | Utente non anonimo | Autorizzazioni utente non anonimo | Gruppo non anonimo | Autorizzazioni gruppo non anonimo |
|---------|---------|---------|---------|---------|---------|---------|---------|
|/ | rwxr-x--x  |admin |admin  |Entità servizio |--x  |FINGRP   |r-x         |
|/clusters | rwxr-x--x |admin |admin |Entità servizio |--x  |FINGRP |r-x         |
|/clusters/finance | rwxr-x--t |admin |FINGRP  |Entità servizio |rwx  |-  |-     |

Nella tabella di hello,

- **amministrazione** è autore hello e amministratore di hello account archivio Data Lake.
- **Entità servizio** è hello Azure Active Directory (AAD) entità servizio associata a hello account.
- **FINGRP** è un gruppo di utenti creato in AAD che contenga gli utenti da hello organizzazione Finance.

Per istruzioni su come toocreate un'applicazione AAD (che crea un'entità servizio), vedere [creare un'applicazione AAD](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application). Per istruzioni su come toocreate un gruppo di utenti in AAD, vedere [la gestione dei gruppi in Azure Active Directory](../active-directory/active-directory-accessmanagement-manage-groups.md).

Tooconsider alcuni punti chiave.

- struttura di cartelle di livello due Hello (**/cluster/finance/**) deve essere creato e il provisioning con le autorizzazioni appropriate dall'amministratore di archivio Data Lake hello **prima** utilizzando l'account di archiviazione hello per i cluster. Questa struttura non viene creata automaticamente durante la creazione dei cluster.
- esempio Hello precedente si consiglia di impostare hello appartenenza gruppo di **/cluster/finance** come **FINGRP** permessi e **r-x** accedere tooFINGRP toohello intera gerarchia di cartelle a partire dalla radice hello. In questo modo si garantisce che i membri di hello del FINGRP possono esplorare la struttura di cartella hello a partire dalla radice.
- In caso di hello quando le entità di servizio diversi AAD è possibile creare cluster in **/cluster/finance**, hello sticky bit (quando impostato su hello **finance** cartella) garantisce che le cartelle creati da un servizio Impossibile eliminare l'entità da altre hello.
- Quando la struttura di cartelle hello e le autorizzazioni siano soddisfatti, processo di creazione del cluster HDInsight crea un loaction di archiviazione specifici per i cluster in **/cluster/finance/**. Ad esempio, è possibile archiviazione hello per un cluster con hello Nome fincluster01 **/clusters/finance/fincluster01**. Hello proprietà e le autorizzazioni per le cartelle di hello create dal cluster HDInsight è illustrato nella tabella hello qui.

    |Cartella  |Autorizzazioni  |utente proprietario  |gruppo proprietario  | Utente non anonimo | Autorizzazioni utente non anonimo | Gruppo non anonimo | Autorizzazioni gruppo non anonimo |
    |---------|---------|---------|---------|---------|---------|---------|---------|
    |/clusters/finanace/ fincluster01 | rwxr-x---  |Entità servizio |FINGRP  |- |-  |-   |-  | 
   


## <a name="recommendations-for-job-input-and-output-data"></a>Suggerimenti per i dati di input e di output del processo

È consigliabile processo tooa dei dati di input e output da un processo di hello essere archiviati in una cartella di fuori **/cluster**. In questo modo si garantisce che anche se hello specifici per i cluster cartella tooreclaim eliminati alcuni spazio di archiviazione, hello processo input e output sono ancora disponibili per un utilizzo futuro. In tal caso, verificare che la gerarchia di cartelle hello per l'archiviazione hello processo input e output consenta appropriato livello di accesso per hello dell'entità servizio.

## <a name="limit-on-clusters-sharing-a-single-storage-account"></a>Limite di cluster che condividono un unico account di archiviazione

limite Hello hello numero di cluster che è possibile condividere un singolo account archivio Data Lake dipende dal carico di lavoro hello in esecuzione su tali cluster. Presenza di troppi cluster o i carichi di lavoro genera un notevole carico nei cluster hello che condividono un account di archiviazione potrebbe hello storage account ingresso/uscita tooget limitate.

## <a name="support-for-default-acls"></a>Supporto per gli ACL predefiniti

Quando si crea un'entità servizio con accesso utente specifico (come illustrato nella tabella hello precedente), è consigliabile **non** aggiunta hello denominato utente con un valore predefinito-ACL. Utilizzo dei risultati di ACL predefiniti nell'assegnazione hello di 770 autorizzazioni per l'utente proprietario, gruppo di appartenenza e altri l'accesso utente denominato provisioning. Sebbene non sottragga autorizzazioni all'utente proprietario (7) o al gruppo proprietario (7), il valore predefinito di 770 sottrae tutte le autorizzazioni agli altri membri (0). Di conseguenza, un problema noto con una particolari casi di utilizzo illustrato in dettaglio in hello [problemi noti e soluzioni alternative](#known-issues-and-workarounds) sezione.

## <a name="known-issues-and-workarounds"></a>Problemi noti e soluzioni alternative

Questa sezione elenca hello conosciuti per l'uso di HDInsight con archivio Data Lake e le relative soluzioni.

### <a name="publicly-visible-localized-yarn-resources"></a>Risorse YARN localizzate visibili pubblicamente

Quando viene creato un nuovo account archivio Azure Data Lake, viene eseguito automaticamente il provisioning directory radice hello con accesso ACL autorizzazione bits set too770. cartella Hello radice proprietario l'utente è set toohello che hello account (amministratore archivio Data Lake hello) creato e hello appartenenza gruppo toohello gruppo primario dell'utente hello che ha creato l'account di hello. Per gli altri membri non è previsto alcun tipo di acceso.

Queste impostazioni sono note tooaffect uno specifico HDInsight casi di utilizzo acquisiti in [YARN 247](https://hwxmonarch.atlassian.net/browse/YARN-247). Invio processo potrebbe non riuscire con un messaggio di errore simile toothis:

    Resource XXXX is not publicly accessible and as such cannot be part of hello public cache.

Come indicato nella hello che YARN JIRA collegato in precedenza, durante la localizzazione di risorse pubbliche, hello localizzatore convalida hello tutte le risorse richieste sono effettivamente pubbliche selezionando le relative autorizzazioni sul sistema di file remoto hello. Eventuali LocalResource che non soddisfano questa condizione vengono rifiutate per la localizzazione. salve controllo delle autorizzazioni, include file toohello e accesso in lettura per "altri". Questo scenario non funziona della casella quando si ospita il cluster HDInsight su Azure Data Lake, poiché Azure Data Lake Nega l'accesso troppo "altri" a livello di cartella radice.

#### <a name="workaround"></a>Soluzione alternativa
Lettura-esecuzione set di autorizzazioni per **altri** tramite la gerarchia di hello, ad esempio, in  **/** , **/cluster** e   **/cluster/finance**  come illustrato nella tabella hello precedente.

## <a name="see-also"></a>Vedere anche

* [Creare un cluster HDInsight con Archivio Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)


