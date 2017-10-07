---
title: architettura di Azure HDInsight unita aaaDomain | Documenti Microsoft
description: Informazioni su come tooplan dominio HDInsight.
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
ms.date: 02/03/2017
ms.author: saurinsh
ms.openlocfilehash: 1c3ecedf3739b4f8fa54160225be9c1d6e2ca6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="plan-azure-domain-joined-hadoop-clusters-in-hdinsight"></a>Pianificare cluster Hadoop aggiunti a un dominio di Azure in HDInsight

Hello Hadoop tradizionale è un cluster singolo utente. adatto alla maggior parte delle aziende con team di piccole dimensioni che compilano carichi di lavoro di dati di grandi dimensioni. Man mano che aumenta la diffusione di Hadoop, molte aziende stanno passando a un modello in cui i cluster sono gestiti da team IT e condivisi tra più team di sviluppo. Di conseguenza, le funzionalità che coinvolgono cluster multiutente sono tra hello più funzionalità richieste in Azure HDInsight.

Invece di compilare il proprio multiutente autenticazione e autorizzazione, HDInsight si basa su hello più provider di identità, Active Directory (AD). Hello potenti funzionalità per la sicurezza Active Directory può essere utilizzato toomanage autorizzazione multiutente in HDInsight. Grazie all'integrazione di HDInsight con Active Directory, è possibile comunicare con i cluster hello utilizzando le credenziali di Active Directory. HDInsight esegue il mapping di un annuncio utente tooa Hadoop utente locale, in modo da tutti i servizi in esecuzione su HDInsight di hello (Ambari, Hive Spark thrift di server, cane, server e altri) funzionare senza problemi per l'utente autenticato hello.

## <a name="integrate-hdinsight-with-ad-and-ad-on-iaas-vm"></a>Integrazione di HDInsight con AD e AD nella macchina virtuale IaaS

Grazie all'integrazione di HDInsight con Azure Active Directory o Active Directory in VM Iaas, i nodi del cluster HDInsight hello sono aggiunti a un dominio tooa dominio. HDInsight crea le entità servizio per hello servizi Hadoop in esecuzione nel cluster hello e li inserisce in un'unità organizzativa specificata (OU) in Azure Active Directory o Active Directory in VM IaaS. HDInsight crea anche i mapping DNS inversi nel dominio hello hello indirizzi IP dei nodi di hello toohello aggiunti a un dominio.

È possibile eseguire questa configurazione usando più architetture. È possibile scegliere tra hello seguendo le architetture.

**HDInsight integrato con Active Directory in esecuzione in Azure IaaS**

Si tratta di architettura più semplice di hello per l'integrazione di HDInsight con Active Directory. Hello controller di dominio Active Directory viene eseguito su uno (o più) macchine virtuali (VM) in Azure. che in genere si trovano in una rete virtuale. Impostare un'altra rete virtuale per il cluster HDInsight hello. Per HDInsight toohave tooActive una visibilità di Directory, è necessario toopeer queste reti virtuali tramite [peering per rete virtuale a](../virtual-network/virtual-network-create-peering.md). Se si crea hello Active Directory in ARM, è possibile creare hello Active Directory e hello di HDInsight nella stessa rete virtuale e non è necessario toodo peering. 

![Topologia del cluster HDInsight aggiunto a un dominio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_1.png)

> [!NOTE]
> In questa architettura, è possibile utilizzare l'archivio Azure Data Lake con i cluster di HDInsight hello.


Prerequisiti per Active Directory:

* Un [unità organizzativa](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) devono essere creati, in cui posizionare hello macchine virtuali del cluster HDInsight e le entità di servizio utilizzate dal cluster hello hello.
* È necessario configurare [Lightweight Directory Access Protocol](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) (LDAP) per comunicare con AD. Hello certificato utilizzato tooset backup LDAPS deve essere un certificato reale (non un certificato autofirmato).
* Le zone DNS inverse devono essere create nel dominio hello per intervallo di indirizzi IP hello della subnet di HDInsight hello (ad esempio, 10.2.0.0/24 nell'immagine precedente hello).
* È necessario un account del servizio o un account utente. Utilizzare questo cluster di HDInsight hello toocreate account. Questo account deve disporre di hello queste autorizzazioni:

    - Oggetti entità servizio toocreate di autorizzazioni e gli oggetti computer all'interno di un'unità organizzativa hello
    - Autorizzazioni toocreate inversa DNS le regole del proxy
    - Dominio di Active Directory toohello macchine toojoin autorizzazioni

**HDInsight integrato con Azure AD solo cloud**

Per Azure AD solo cloud, configurare un controller di dominio in modo che HDInsight possa essere integrato con Azure AD. A tale scopo è possibile usare [Azure Active Directory Domain Services](../active-directory-domain-services/active-directory-ds-overview.md). Azure Active Directory crea macchine del controller di dominio nel cloud hello e fornisce gli indirizzi IP per loro. Per garantire disponibilità elevata, crea due controller di dominio.

Attualmente, Azure Active Directory Domain Services esiste solo in reti virtuali classiche È accessibile solo tramite hello portale di Azure classico. HDInsight è presente una rete virtuale nel portale di Azure, che deve toobe hello Hello peering con la rete virtuale classica hello utilizzando peering per rete virtuale a.

> [!NOTE]
> Peering tra una rete virtuale classica e rete virtuale è necessario che entrambe le reti virtuali siano un gestore delle risorse Azure hello stessa regione e hello nella stessa sottoscrizione di Azure.

![Topologia del cluster HDInsight aggiunto a un dominio](./media/hdinsight-domain-joined-architecture/hdinsight-domain-joined-architecture_2.png)

Prerequisiti per Azure AD:

* Un [unità organizzativa](../active-directory-domain-services/active-directory-ds-admin-guide-create-ou.md) deve essere creato in cui posizionare hello macchine virtuali del cluster HDInsight e le entità di servizio utilizzate dal cluster hello hello.
* I protocolli [LDAP](../active-directory-domain-services/active-directory-ds-admin-guide-configure-secure-ldap.md) devono essere impostati durante la configurazione di Azure Active Directory Domain Services. Hello certificato utilizzato tooset backup LDAPS deve essere un certificato reale (non un certificato autofirmato).
* Le zone DNS inverse devono essere create nel dominio hello per intervallo di indirizzi IP hello della subnet di HDInsight hello (ad esempio, 10.2.0.0/24 nell'immagine precedente hello).
* [Gli hash delle password](../active-directory-domain-services/active-directory-ds-getting-started-password-sync.md) devono essere sincronizzati da tooAzure AD Azure Active Directory.
* È necessario un account del servizio o un account utente. Utilizzare questo cluster di HDInsight hello toocreate account. Questo account deve disporre di hello queste autorizzazioni:

    - Oggetti entità servizio toocreate di autorizzazioni e gli oggetti computer all'interno di un'unità organizzativa hello
    - Autorizzazioni toocreate inversa DNS le regole del proxy
    - Dominio di Azure AD toohello macchine toojoin autorizzazioni

## <a name="next-steps"></a>Passaggi successivi
* tooconfigure un cluster di HDInsight appartenenti a un dominio, vedere [configurare cluster di HDInsight dominio](hdinsight-domain-joined-configure.md).
* i cluster HDInsight dominio toomanage, vedere [la gestione dei cluster HDInsight dominio](hdinsight-domain-joined-manage.md).
* tooconfigure Hive criteri e l'esecuzione delle query Hive, vedere [Hive configurare criteri per i cluster HDInsight dominio](hdinsight-domain-joined-run-hive.md).
* le query Hive toorun utilizzando SSH nel dominio cluster HDInsight, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).
