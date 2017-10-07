---
title: sicurezza aaaHadoop - dominio cluster HDInsight - Azure | Documenti Microsoft
description: Informazioni su...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7dc6847d-10d4-4b5c-9c83-cc513cf91965
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/31/2016
ms.author: saurinsh
ms.openlocfilehash: 5a9469402a61bcba4017e1ff4bd06dfba23ac963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="an-introduction-toohadoop-security-with-domain-joined-hdinsight-clusters-preview"></a>Sicurezza di tooHadoop un'introduzione con i cluster di HDInsight dominio (anteprima)

Fino a questo momento, Azure HDInsight ha supportato solo un unico amministratore locale degli utenti. Questo funzionava bene per i team di applicazioni o i reparti di dimensioni ridotte. Come i carichi di lavoro in base acquisite ulteriori popolarità nel settore aziendale hello, hello necessario per enterprise Hadoop funzionalità di livello come basata su active directory l'autenticazione, il supporto di più utenti e controllo di accesso basato sui ruoli sono diventate sempre più importante. Utilizzo dei cluster HDInsight appartenenti a un dominio, è possibile creare un dominio di Active Directory tooan aggiunti a un cluster HDInsight, configurare un elenco di dipendenti da enterprise hello che possono eseguire l'autenticazione tramite Azure Active Directory toolog tooHDInsight cluster. Utenti esterni all'organizzazione di hello non è possibile accedere o accedere ai cluster HDInsight hello. Hello amministratore dell'organizzazione può configurare il controllo di accesso basato sui ruoli per l'utilizzo di sicurezza Hive [cane Apache](http://hortonworks.com/apache/ranger/), quindi limitare l'accesso toodata tooonly come necessario. Infine, salve possibile controllare l'accesso ai dati hello dai dipendenti, e tooaccess eventuali modifiche apportate controllare i criteri, quindi ottenere un livello elevato di governance delle risorse aziendali.

> [!NOTE]
> nuove funzionalità di Hello descritte in questa versione di anteprima sono disponibili solo nei cluster HDInsight basati su Linux per l'Hive del carico di lavoro. salve altri carichi di lavoro, ad esempio HBase, Spark, Storm e Kafka, verranno attivate nelle future versioni.

> [!IMPORTANT]
> Oozie non è abilitato su HDInsight appartenente al dominio.

## <a name="benefits"></a>Vantaggi
La protezione aziendale si basa su quattro importanti pilastri: protezione perimetrale, autenticazione, autorizzazione e crittografia.

![I pilastri dei vantaggi dei cluster HDInsight aggiunti al dominio](./media/hdinsight-domain-joined-introduction/hdinsight-domain-joined-four-pillars.png).

### <a name="perimeter-security"></a>Protezione perimetrale
La protezione perimetrale in HDInsight si raggiunge con l'uso di reti virtuali e servizio gateway. Oggi, un amministratore dell'organizzazione può creare un cluster HDInsight all'interno di una rete virtuale e usare la rete virtuale toohello accesso toorestrict gruppi di sicurezza (regole di firewall in entrata o in uscita). Solo hello gli indirizzi IP definiti in hello in ingresso regole del firewall sarà in grado di toocommunicate con cluster HDInsight hello, in modo da fornire protezione perimetrale. Un altro livello di protezione perimetrale viene garantito grazie al servizio gateway. Hello Gateway è servizio hello che agisce come prima linea di difesa per qualsiasi cluster di HDInsight toohello richiesta in ingresso. Accetta una richiesta hello, convalida e consente solo a questo punto hello richiesta toopass toohello altri nodi nel cluster, in modo da fornire protezione perimetrale tooother i nodi di nome e i dati in cluster hello.

### <a name="authentication"></a>Autenticazione
Con questa anteprima pubblica, un amministratore può effettuare il provisioning di un cluster HDInsight aggiunto al dominio in una [rete virtuale](https://azure.microsoft.com/services/virtual-network/). i nodi del cluster HDInsight hello Hello sarà toohello aggiunti a un dominio gestito da hello enterprise. Questo è possibile grazie all'uso dei [servizi di dominio di Azure Active Directory](../active-directory-domain-services/active-directory-ds-overview.md). Tutti i nodi nel cluster hello hello sono tooa aggiunti a un dominio che gestisce enterprise hello. Con questa configurazione, i dipendenti dell'organizzazione hello possono accedere toohello i nodi del cluster utilizzando le credenziali di dominio. Può anche usare i relativi tooauthenticate le credenziali di dominio con altri endpoint come toointeract tonalità, Ambari viste, ODBC, JDBC, PowerShell e API REST con cluster hello approvati. salve abbia il pieno controllo sulla limitazione hello numero di utenti di interagire con i cluster hello tramite questi endpoint.

### <a name="authorization"></a>Authorization
Aggiungendo la maggior parte delle aziende consigliata è che non tutti i dipendenti ha tooall accedere alle risorse aziendali. Con questa versione, in modo analogo, salve possibile definire criteri di controllo di accesso basato sui ruoli per le risorse cluster hello. Ad esempio, è possibile configurare salve [cane Apache](http://hortonworks.com/apache/ranger/) tooset i criteri di controllo di accesso per l'Hive. Questa funzionalità garantisce che i dipendenti saranno in grado di tooaccess solo tutti i dati devono toobe correttamente i processi. Cluster toohello di accesso SSH è anche amministratore toohello solo con restrizioni.

### <a name="auditing"></a>Controllo
Insieme hello HDInsight le risorse del cluster da utenti non autorizzati e la protezione dei dati di hello, il controllo di tutti accedere alle risorse di cluster toohello e hello di protezione dati sono necessario tootrack accesso non autorizzato o non intenzionale di risorse hello. Con questa versione di anteprima, salve può visualizzare e segnalare tutti i dati e accedere alle risorse del cluster di HDInsight toohello. salve inoltre è possibile visualizzare e report tutte le modifiche a criteri di controllo di accesso toohello eseguiti in Apache cane supportati gli endpoint. Un cluster HDInsight dominio utilizza hello familiare dell'interfaccia utente cane Apache toosearch i registri di controllo. Nel back-end hello, utilizza cane [Solr Apache](http://hortonworks.com/apache/solr/) per l'archiviazione e la ricerca di log hello.

### <a name="encryption"></a>Crittografia
Protezione dei dati è importante per la protezione dell'organizzazione di riunione e i requisiti di conformità e insieme a limitare l'accesso toodata da dipendenti non autorizzati, deve essere protetti mediante crittografia. Entrambi hello archivi dati per i cluster HDInsight, Blob di archiviazione di Azure, e l'archiviazione di Azure Data Lake supportano trasparente sul lato server [crittografia dei dati](../storage/common/storage-service-encryption.md) inattivi. La protezione dei cluster HDInsight sarà perfettamente compatibile con questa crittografia lato server della funzionalità dei dati inattivi.

## <a name="next-steps"></a>Passaggi successivi
* Per configurare un cluster HDInsight aggiunto al dominio, vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).
* Per gestire cluster HDInsight aggiunti al dominio, vedere [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire i cluster HDInsight aggiunti al dominio).
* Per configurare i criteri ed eseguire query Hive, vedere [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configurare criteri Hive per cluster HDInsight aggiunti al dominio).
* Per eseguire query Hive usando SSH nei cluster HDInsight aggiunti al dominio, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
