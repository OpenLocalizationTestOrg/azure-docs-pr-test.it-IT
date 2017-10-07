---
title: cluster HDInsight dominio aaaManage - Azure | Documenti Microsoft
description: Informazioni su come toomanage HDInsight dominio cluster
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 233ddf0953e981f9a24b77d9dde194d590e5e6d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a>Gestione dei cluster HDInsight aggiunti al dominio (anteprima)
Informazioni su hello utenti e ruoli di hello in HDInsight appartenenti a un dominio, e come toomanage HDInsight dominio cluster.

## <a name="users-of-domain-joined-hdinsight-clusters"></a>Utenti dei cluster HDInsight aggiunti al dominio
Un cluster di HDInsight non aggiunti al dominio è disponibili due account utente creati durante la creazione di cluster hello:

* **Amministratore Ambari**: questo account è denominato anche *Utente Hadoop* o *Utente HTTP*. Questo account può essere utilizzato toolog su tooAmbari in https://&lt;clustername >. cluster>.azurehdinsight.NET. Può anche essere utilizzati toorun query sulle viste Ambari, eseguire i processi tramite strumenti esterni (ad esempio PowerShell, Templeton, Visual Studio) e l'autenticazione con il driver ODBC Hive hello e strumenti di Business Intelligence (ad esempio Excel, Power BI o Tableau).
* **Utente SSH**: questo account può essere usato con SSH e per eseguire comandi sudo. Dispone di privilegi di radice toohello le macchine virtuali Linux.

Un cluster di HDInsight dominio dispone di tre nuovi utenti dell'utente di amministrazione e SSH tooAmbari aggiunta.

* **Amministrazione cane**: questo account è hello locale Apache cane amministratore account. Non si tratta di un utente del dominio di Active Directory. Questo account può essere toosetup utilizzato criteri e verificare altri utenti amministratori o gli amministratori delegati (in modo che gli utenti possono gestire i criteri). Per impostazione predefinita, il nome utente hello è *admin* e la password di hello è hello stesso hello Ambari password di amministratore. password Hello può essere aggiornata dalla pagina Impostazioni hello cane.
* **Utente di dominio amministratore cluster**: questo account è un utente di dominio active directory designato come amministratore di cluster Hadoop inclusi Ambari e cane hello. Durante la creazione del cluster, è necessario fornire le credenziali dell'utente. A questo utente è hello seguenti privilegi:

  * Aggiunta a dominio toohello macchine e inserirli in hello unità Organizzativa specificata durante la creazione del cluster.
  * Creare entità di servizio all'interno di hello unità Organizzativa specificata durante la creazione del cluster.
  * Creazione delle voci DNS inverse.

    Hello nota altri utenti di Active Directory dispongano anche di questi privilegi.

    Esistono alcuni punti di fine all'interno di cluster hello (ad esempio, Templeton) che non sono gestiti da cane e pertanto non sono protetti. Questi punti vengono bloccati per tutti gli utenti tranne l'utente di dominio amministratore cluster hello.
* **Normale**: durante la creazione del cluster, è possibile specificare più gruppi di Active Directory. gli utenti di Hello di questi gruppi verranno sincronizzati tooRanger e Ambari. Questi utenti sono utenti di dominio e avranno accesso tooonly gestiti cane endpoint (ad esempio, Hiveserver2). Tutti i criteri RBAC di hello e il controllo sarà utenti toothese applicabile.

## <a name="roles-of-domain-joined-hdinsight-clusters"></a>Ruoli dei cluster HDInsight aggiunti al dominio
HDInsight dominio hanno hello seguenti ruoli:

* Amministratore del cluster
* Operatore del cluster
* Amministratore del servizio
* Operatore del servizio
* Utente del cluster

**autorizzazioni di hello toosee di questi ruoli**

1. Aprire l'interfaccia utente Gestione Ambari hello.  Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).
2. Scegliere dal menu a sinistra hello **ruoli**.
3. Fare clic su hello blu punto interrogativo toosee hello autorizzazioni:

    ![Autorizzazioni dei ruoli dei cluster HDInsight aggiunti al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-hello-ambari-management-ui"></a>Aprire l'interfaccia utente Gestione Ambari hello
1. Accesso toohello [portale di Azure](https://portal.azure.com).
2. Aprire il cluster HDInsight in un pannello. Vedere [Elencare e visualizzare i cluster](hdinsight-administer-use-management-portal.md#list-and-show-clusters).
3. Fare clic su **Dashboard** dal menu principale di hello tooopen Ambari.
4. Accedere utilizzando la password e nome utente di dominio amministratore cluster hello tooAmbari.
5. Fare clic su hello **Admin** menu a discesa da hello angolo superiore destro e quindi fare clic su **gestire Ambari**.

    ![Gestire Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    Hello dell'interfaccia utente simile a:

    ![Interfaccia utente della gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-hello-domain-users-synchronized-from-your-active-directory"></a>Elenco utenti del dominio hello sincronizzati da Active Directory
1. Aprire l'interfaccia utente Gestione Ambari hello.  Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).
2. Scegliere dal menu a sinistra hello **utenti**. Vedrai tutti gli utenti di hello sincronizzati da cluster HDInsight toohello Active Directory.

    ![Elenco degli utenti dell'interfaccia per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-hello-domain-groups-synchronized-from-your-active-directory"></a>Elenco di gruppi di dominio hello sincronizzati da Active Directory
1. Aprire l'interfaccia utente Gestione Ambari hello.  Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).
2. Scegliere dal menu a sinistra hello **gruppi**. Vedrai tutti i gruppi di hello sincronizzati da cluster HDInsight toohello Active Directory.

    ![Elenco dei gruppi dell'interfaccia utente per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a>Configurare le autorizzazioni delle viste Hive
1. Aprire l'interfaccia utente Gestione Ambari hello.  Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).
2. Scegliere dal menu a sinistra hello **viste**.
3. Fare clic su **HIVE** dettagli hello tooshow.

    ![Viste Hive dell'interfaccia utente per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. Fare clic su hello **visualizzazione Hive** collegamento tooconfigure Hive viste.
5. Scorrere verso il basso toohello **autorizzazioni** sezione.

    ![Configurare le autorizzazioni delle viste Hive nell'interfaccia utente per la gestione di Ambari nel cluster HDInsight aggiunto al dominio](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. Fare clic su **Aggiungi utente** o **Aggiungi gruppo**, quindi specificare hello utenti o gruppi che è possono utilizzare viste Hive.

## <a name="configure-users-for-hello-roles"></a>Configurare gli utenti per i ruoli di hello
 vedere un elenco di ruoli e le relative autorizzazioni, toosee [cluster HDInsight ruoli di dominio](#roles-of-domain---joined-hdinsight-clusters).

1. Aprire l'interfaccia utente Gestione Ambari hello.  Vedere [aprire hello dell'interfaccia utente Gestione Ambari](#open-the-ambari-management-ui).
2. Scegliere dal menu a sinistra hello **ruoli**.
3. Fare clic su **Aggiungi utente** o **Aggiungi gruppo** tooassign utenti e gruppi toodifferent i ruoli.

## <a name="next-steps"></a>Passaggi successivi
* Per configurare un cluster HDInsight aggiunto al dominio, vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).
* Per configurare i criteri ed eseguire query Hive, vedere [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md) (Configurare criteri Hive per cluster HDInsight aggiunti al dominio).
* Per eseguire query Hive usando SSH nei cluster HDInsight aggiunti al dominio, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
