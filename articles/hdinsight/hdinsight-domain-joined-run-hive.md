---
title: criteri di aaaConfigure Hive in HDInsight dominio - Azure | Documenti Microsoft
description: Informazioni su...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a>Configurare criteri Hive in HDInsight aggiunto al dominio (anteprima)
Informazioni su come criteri cane Apache tooconfigure per l'Hive. In questo articolo, creare due cane criteri toorestrict accesso toohello hivesampletable. Hello hivesampletable viene fornito con i cluster HDInsight. Dopo aver configurato i criteri di hello, utilizzare Excel e ODBC driver tooconnect tooHive le tabelle in HDInsight.

## <a name="prerequisites"></a>Prerequisiti
* Un cluster HDInsight aggiunto al dominio. Vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).
* Una workstation con Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone oppure Office 2010 Professional Plus.

## <a name="connect-tooapache-ranger-admin-ui"></a>Connettersi tooApache cane interfaccia utente di amministrazione
**tooconnect tooRanger Admin UI**

1. Da un browser, connettersi tooRanger Admin UI. Hello URL è https://&lt;ClusterName >.azurehdinsight.net/Ranger/.

   > [!NOTE]
   > Ranger usa credenziali diverse da quelle del cluster Hadoop. tooprevent browser utilizzando credenziali memorizzate nella cache di Hadoop, utilizzare toohello tooconnect finestra del browser inprivate nuova interfaccia utente di amministrazione cane.
   >
   >
2. Accedere con la password e nome utente di dominio amministratore cluster hello:

    ![Home page di Ranger con dominio aggiunto a HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    Attualmente, Ranger è compatibile solo con Yarn e Hive.

## <a name="create-domain-users"></a>Creazione di utenti del dominio
In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configurare i cluster HDInsight aggiunti al dominio) sono stati creati hiveruser1 e hiveuser2. Si utilizzerà l'account utente due hello in questa esercitazione.

## <a name="create-ranger-policies"></a>Creazione dei criteri di Ranger
In questa sezione verranno creati due criteri di Ranger per accedere a hivesampletable. Vengono concesse autorizzazioni di selezione su diversi set di colonne. Entrambi gli utenti sono stati creati nella procedura [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad) (Configurare i cluster HDInsight aggiunti al dominio).  Nella sezione successiva hello, verranno testati due criteri di hello in Excel.

**criteri cane toocreate**

1. Aprire l'interfaccia utente di amministrazione di Ranger. Vedere [connettersi tooApache dell'interfaccia utente amministrazione cane](#connect-to-apache-ranager-admin-ui).
2. Fare clic su **&lt;ClusterName>_hive** in **Hive**. Verranno visualizzati due criteri preconfigurati.
3. Fare clic su **Aggiungi nuovo criterio**, quindi immettere hello seguenti valori:

   * Nome criterio: read-hivesampletable-all
   * Database Hive: predefinito
   * Tabella: hivesampletable
   * Colonna Hive: *
   * Seleziona utente: hiveuser1
   * Autorizzazioni: selezionare

     ![Configurazione dei criteri di Hive Ranger con dominio aggiunto a HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png).

     > [!NOTE]
     > Se un utente di dominio non viene popolato in Seleziona utente, attendere alcuni istanti per cane toosync con AAD.
     >
     >
4. Fare clic su **Aggiungi** criteri hello toosave.
5. Ripetere l'operazione hello ultimi due passaggi toocreate un altro criterio con hello le proprietà seguenti:

   * Nome criterio: read-hivesampletable-devicemake
   * Database Hive: predefinito
   * Tabella: hivesampletable
   * Colonna Hive: clientid, devicemake
   * Seleziona utente: hiveuser2
   * Autorizzazioni: selezionare

## <a name="create-hive-odbc-data-source"></a>Creare un'origine dati Hive ODBC
istruzioni di Hello sono reperibile [origine dati ODBC di Hive creare](hdinsight-connect-excel-hive-odbc-driver.md).  

    Proprietà|Descrizione
    ---|---
    Data Source Name|Fornire un'origine dati di nome tooyour
    Host|Immettere &lt;HDInsightClusterName>.azurehdinsight.net. Ad esempio, myHDICluster.azurehdinsight.net
    Porta|Utilizzare <strong>443</strong>. (Questa porta è stata modificata da too443 563).
    Database|Usare l'<strong>impostazione predefinita</strong>.
    Hive Server Type|Selezionare <strong>Hive Server 2</strong>
    Mechanism|Selezionare <strong>Azure HDInsight Service</strong>
    HTTP Path|Lasciare vuoto.
    User Name|Immettere hiveuser1@contoso158.onmicrosoft.com. Aggiornare il nome di dominio hello se è diverso.
    Password|Immettere la password di hello per hiveuser1.
    </table>

Verificare che tooclick **Test** prima di salvare l'origine dati hello.

## <a name="import-data-into-excel-from-hdinsight"></a>Importazione di dati in Excel da HDInsight
Nell'ultima sezione hello, è stato configurato due criteri.  hiveuser1 hello selezionare autorizzazione su tutte le colonne di hello, che hiveuser2 ha hello selezionare l'autorizzazione per due colonne. In questa sezione è rappresentare hello due utenti tooimport dati in Excel.

1. Aprire una cartella di lavoro nuova o esistente in Excel.
2. Da hello **dati** scheda, fare clic su **da altre origini dati**, quindi fare clic su **da connessione guidata dati** toolaunch hello **connessione guidata dati**.

    ![Aprire Connessione guidata dati][img-hdi-simbahiveodbc.excel.dataconnection]
3. Selezionare **DSN ODBC** come origine dati hello e quindi fare clic su **Avanti**.
4. Origini dati ODBC, creato nel passaggio precedente hello il nome dell'origine dati selezionare hello e quindi fare clic su **Avanti**.
5. Immettere nuovamente la password hello per cluster hello nella procedura guidata hello e quindi fare clic su **OK**. Attendere hello **seleziona Database e tabella** tooopen finestra di dialogo. Questa operazione potrebbe richiedere alcuni secondi.
6. Selezionare **hivesampletable**, quindi fare clic su **Avanti**.
7. Fare clic su **Finish**.
8. In hello **l'importazione dei dati** finestra di dialogo, è possibile modificare o specificare query hello. Questa operazione, scegliere toodo **proprietà**. Questa operazione potrebbe richiedere alcuni secondi.
9. Fare clic su hello **definizione** scheda hello testo del comando è:

       SELECT * FROM "HIVE"."default"."hivesampletable"

   Criteri di cane hello che è definito, hiveuser1 dispone dell'autorizzazione select per tutte le colonne di hello.  Pertanto, questa query funziona con le credenziali di hiveuser1, ma non con quelle di hiveuser2.

   ![Proprietà di connessione][img-hdi-simbahiveodbc-excel-connectionproperties]
10. Fare clic su **OK** tooclose finestra di dialogo Proprietà connessione hello.
11. Fare clic su **OK** tooclose hello **l'importazione dei dati** finestra di dialogo.  
12. Digitare nuovamente la password di hello per hiveuser1 e quindi fare clic su **OK**. Alcuni secondi prima del recupero dei dati importati tooExcel necessario. Al termine, verranno visualizzate 11 colonne di dati.

tootest hello secondo criteri (read-hivesampletable-devicemake) creati nell'ultima sezione hello

1. Aggiungere un nuovo foglio in Excel.
2. Seguire i dati hello tooimport hello ultima procedura.  modifica solo del Hello che si apporterà è credenziali del hiveuser2 toouse invece del hiveuser1. L'operazione non riuscirà perché hiveuser2 ha solo due colonne di autorizzazione toosee. Si deve ottenere hello errore seguente:

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. Seguire hello stesso dati tooimport stored procedure. Questa volta, utilizzare le credenziali del hiveuser2 e inoltre modificare hello from dell'istruzione select:

        SELECT * FROM "HIVE"."default"."hivesampletable"

    in:

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    Al termine, verranno visualizzate due colonne di dati importati.

## <a name="next-steps"></a>Passaggi successivi
* Per configurare un cluster HDInsight aggiunto al dominio, vedere [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md) (Configurare i cluster HDInsight aggiunti al dominio).
* Per gestire cluster HDInsight aggiunti al dominio, vedere [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md) (Gestire i cluster HDInsight aggiunti al dominio).
* Per eseguire query Hive usando SSH nei cluster HDInsight aggiunti al dominio, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).
* Per la connessione Hive tramite Hive JDBC, vedere [connettersi tooHive in Azure HDInsight utilizza hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)
* Per l'utilizzo di ODBC Hive connessione tooHadoop di Excel, vedere [tooHadoop Excel connettersi con unità di Microsoft ODBC Hive hello](hdinsight-connect-excel-hive-odbc-driver.md)
* Per la connessione tooHadoop di Excel tramite Power Query, vedere [tooHadoop Excel connettersi tramite Power Query](hdinsight-connect-excel-power-query.md)
