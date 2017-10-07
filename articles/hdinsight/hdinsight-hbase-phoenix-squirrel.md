---
title: aaaUse Phoenix Apache ed esce con basati su Windows Azure HDInsight | Documenti Microsoft
description: Informazioni su come toouse Phoenix Apache in HDInsight e come tooinstall e configurare esce sul cluster workstation tooconnect tooan HBase in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Usare Apache Phoenix e SQuirreL con i cluster HBase basati su Windows in HDInsight
Informazioni su come toouse [Phoenix Apache](http://phoenix.apache.org/) in HDInsight e come tooinstall e configurare esce sul cluster workstation tooconnect tooan HBase in HDInsight. Per altre informazioni su Phoenix, vedere la [breve panoramica su Phoenix](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Per hello grammatica Phoenix, vedere [grammatica Phoenix](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Per informazioni sulla versione Phoenix in HDInsight hello, vedere [novità introdotta nelle versioni di cluster Hadoop hello fornite da HDInsight?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> Hello passaggi sono disponibili solo in questo documento per i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per informazioni sull'uso di Phoenix su HDInsight basato su Linux, vedere [Usare Apache Phoenix con cluster HBase basati su Linux in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>Usare SQLLine
[SQLLine](http://sqlline.sourceforge.net/) è un tooexecute di utilità della riga di comando SQL.

### <a name="prerequisites"></a>Prerequisiti
Prima di poter utilizzare SQLLine, è necessario disporre delle seguenti hello:

* **Un cluster HBase in HDInsight**. Per informazioni sul provisioning di un cluster HBase, vedere l'[introduzione all'uso di Apache HBase in HDInsight][hdinsight-hbase-get-started].
* **Connettere il cluster HBase toohello tramite protocollo desktop remoto hello**. Per istruzioni, vedere [cluster di gestire Hadoop in HDInsight mediante hello portale di Azure classico][hdinsight-manage-portal].

**toofind il nome host hello**

1. Aprire **della riga di comando Hadoop** da desktop hello.
2. Eseguire hello suffisso DNS hello tooget di comando seguente:

        ipconfig

    Annotare il **suffisso DNS specifico della connessione**. Ad esempio, *myhbasecluster.f5.internal.cloudapp.net*. Quando ci si connette cluster HBase tooan, sarà necessario tooone tooconnect di Zookeepers hello tramite FQDN. Ogni cluster HDInsight ha tre Zookeeper: *zookeeper0*, *zookeeper1* e *zookeeper2*. Hello FQDN sarà simile al seguente *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLLine**

1. Aprire **della riga di comando Hadoop** da desktop hello.
2. Eseguire i seguenti comandi tooopen SQLLine hello:

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight HBase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    comandi Hello utilizzati nell'esempio hello:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Per altre informazioni, vedere il [manuale di SQLLine](http://sqlline.sourceforge.net/#manual) e la [grammatica Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>Usare SQuirreL
[Esce SQL Client](http://squirrel-sql.sourceforge.net/) è un programma Java con interfaccia grafico che consentono di struttura hello tooview di un database conforme a JDBC, esplorare i dati di hello in tabelle, eseguire comandi SQL e così via. Può essere utilizzato tooconnect tooApache Phoenix in HDInsight.

In questa sezione illustra come tooinstall e configurare esce il cluster workstation tooconnect tooan HBase in HDInsight tramite una VPN.

### <a name="prerequisites"></a>Prerequisiti
Prima di seguire le procedure di hello, è necessario disporre delle seguenti hello:

* Un cluster HBase distribuito tooan rete virtuale di Azure con una macchina virtuale DNS.  Per istruzioni, vedere [Creare cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet].

* Ottiene il suffisso DNS specifico della connessione del cluster di hello HBase cluster. tooget RDP in cluster hello, esso, quindi eseguire IPConfig.  suffisso DNS Hello è simile a:

        myhbase.b7.internal.cloudapp.net
* Scaricare e installare [Microsoft Visual Studio Express per Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) sulla workstation. Sarà necessario makecert da hello pacchetto toocreate il certificato.  
* Scaricare e installare [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) sulla workstation.  SQuirreL SQL Client versione 3.0 e versioni successive richiede la versione JRE 1.6 o versioni successive.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Configurare un toohello di connessione VPN Point-to-Site rete virtuale di Azure
La configurazione di una connessione VPN Point-To-Site prevede tre passaggi:

1. [Configurare una rete virtuale e un gateway di routing dinamico](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Creare i certificati](#Create-your-certificates)
3. [Configurare il client VPN](#Configure-your-VPN-client)

Vedere [configurare tooan di connessione rete virtuale di Azure un VPN Point-to-Site](../vpn-gateway/vpn-gateway-point-to-site-create.md) per ulteriori informazioni.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Configurare una rete virtuale e un gateway di routing dinamico
Garantire è stato effettuato il provisioning di un cluster HBase in una rete virtuale di Azure (vedere hello prerequisiti per questa sezione). passaggio successivo Hello è tooconfigure una connessione point-to-site.

**connettività point-to-site di hello tooconfigure**

1. Accedi toohello [portale di Azure classico][azure-portal].
2. A sinistra di hello, fare clic su **reti**.
3. Fare clic su rete virtuale di hello creato (vedere [provisioning HBase cluster nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]).
4. Fare clic su **configura** dall'alto hello.
5. In hello **connettività point-to-site** selezionare **configurare la connettività point-to-site**.
6. Configurare **IP iniziale** e **CIDR** toospecify hello indirizzo IP da cui i client VPN riceveranno un indirizzo IP di indirizzi quando si è connessi. intervallo di Hello non può sovrapporsi con uno qualsiasi dei hello intervalli presenti in locale di rete e hello connettono alla rete virtuale di Azure. Ad esempio, Se si seleziona 10.0.0.0/20 per la rete virtuale hello, è possibile selezionare 10.1.0.0/24 hello client dello spazio degli indirizzi. Vedere hello [connettivitàPoint-To-Site] [ vnet-point-to-site-connectivity] pagina per altre informazioni.
7. Nella sezione di spazi indirizzi di rete virtuale hello, fare clic su **Aggiungi subnet gateway**.
8. Fare clic su **salvare** nella parte inferiore di hello della pagina hello.
9. Fare clic su **Sì** modifica hello tooconfirm. Attendere che il sistema hello ha apportato hello modificare prima di continuare la procedura successiva toohello.

**toocreate un gateway con routing dinamico**

1. Dal portale di Azure classico hello, fare clic su **DASHBOARD** dall'alto hello della pagina hello.
2. Fare clic su **crea GATEWAY** dal basso hello della pagina hello.
3. Fare clic su **Sì** tooconfirm. Attendere fino a quando non è stato creato il gateway hello.
4. Fare clic su **DASHBOARD** dall'alto hello.  Verrà visualizzato un grafico visuale della rete virtuale hello:

    ![Diagramma virtuale Point-to-Site della rete virtuale di Azure][img-vnet-diagram]

    diagramma di Hello Mostra le connessioni client 0. Dopo aver apportato una rete virtuale toohello di connessione, il numero di hello sarà tooone aggiornato.

#### <a name="create-your-certificates"></a>Creare i certificati
Un modo toocreate è un certificato x. 509 utilizzando hello strumento di creazione certificati (makecert.exe) fornita con [Microsoft Visual Studio Express per Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**un certificato radice autofirmato toocreate**

1. Dalla workstation, aprire una finestra del prompt dei comandi.
2. Esplorazione delle cartelle di strumenti di Visual Studio toohello.
3. comando nel seguente esempio hello seguente Hello creare e installare un certificato radice nell'archivio certificati personali hello nella workstation e anche creare un file con estensione cer corrispondente che verrà caricato in un secondo momento toohello portale classico di Azure.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Cambiare directory toohello che si desidera hello toobe file con estensione cer trova, dove HBaseVnetVPNRootCertificate è il nome di hello che si desidera toouse certificato hello.

    Non chiudere hello il prompt dei comandi.  Sarà necessario hello procedura descritta di seguito.

   > [!NOTE]
   > Poiché è stato creato un certificato radice da cui verranno generati certificati client, è possibile desidera tooexport insieme alla relativa chiave privata e salvarlo tooa posizione sicura dove può essere recuperato.
   >
   >

**toocreate un certificato client**

* Da hello stesso prompt dei comandi (e presenta toobe hello computer in cui è stato creato certificato radice hello. certificato client Hello deve essere generato dal certificato radice hello), esecuzione hello il seguente comando:

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate è nome del certificato radice hello.  Include un nome del certificato radice toomatch hello.  

    Certificato radice hello sia certificato client hello vengono archiviati nell'archivio certificati personali nel computer in uso. Utilizzare tooverify Certmgr. msc.

    ![Certificato VPN Point-to-Site della rete virtuale di Azure][img-certificate]

    Un certificato client deve essere installato in ogni computer che si desidera rete virtuale di tooconnect toohello. È consigliabile creare client univoci certificati per ogni computer che si desidera rete virtuale di tooconnect toohello. i certificati client hello tooexport, utilizzare Certmgr. msc.

**tooupload hello radice certificato toohello portale classico di Azure**

1. Dal portale di Azure classico hello, fare clic su **rete** a sinistra di hello.
2. Fare clic in cui viene distribuito il cluster HBase per la rete virtuale hello.
3. Fare clic su **certificati** dall'alto hello.
4. Fare clic su **caricare** da hello basso e specificare i file del certificato radice hello creato nella procedura di hello prima dell'ultima. Attendere che il certificato di hello ottenuto importato.
5. Fare clic su **DASHBOARD** nella parte superiore di hello.  diagramma virtuale Hello Mostra stato hello.

#### <a name="configure-your-vpn-client"></a>Configurare il client VPN
**toodownload e installare il pacchetto VPN hello client**

1. Dalla pagina DASHBOARD hello della rete virtuale hello, nella sezione riepilogo rapido hello, fare clic su **Download hello pacchetto VPN Client a 64 bit** o **Download hello pacchetto VPN Client a 32 bit** in base il versione del sistema operativo della workstation.
2. Fare clic su **eseguire** pacchetto hello tooinstall.
3. Al prompt dei comandi sicurezza hello, fare clic su **informazioni**, quindi fare clic su **eseguire comunque**.
4. Fare clic due volte su **Sì** .

**tooconnect tooVPN**

1. Sul desktop di hello della workstation, fare clic sull'icona di reti hello sulla barra delle applicazioni hello. Verrà visualizzata una connessione VPN con il nome della propria rete virtuale.
2. Fare clic su nome della connessione VPN hello.
3. Fare clic su **Connetti**.

**hello tootest risoluzione di nome di dominio e di connessione VPN**

* Dalla workstation hello, aprire un prompt dei comandi e ping uno dei seguenti nomi di suffisso DNS del cluster HBase hello hello è myhbase.b7.internal.cloudapp.net:

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Installare e configurare SQuirreL sulla workstation
**tooinstall esce**

1. Scaricare file jar del client SQL esce hello da [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. File jar hello apertura ed esecuzione. Richiede hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Fare clic su **Next** due volte.
4. Specificare un percorso in cui occorre hello l'autorizzazione di scrittura e quindi fare clic su **Avanti**.

  > [!NOTE]
  > cartella di installazione predefinita di Hello è nella cartella c:\Programmi\Microsoft Files\squirrel-sql-3.6 hello.  Nel percorso toothis toowrite ordine installer hello deve disporre dei privilegi di amministratore hello. È possibile aprire un prompt dei comandi come amministratore, spostarsi nella cartella bin del tooJava ed eseguire quindi:
  >
  >     Java.exe-jar [percorso hello del file jar di hello esce]
5. Fare clic su **OK** tooconfirm creazione hello directory di destinazione.
6. impostazione predefinita Hello è hello tooinstall Base pacchetti e Standard.  Fare clic su **Avanti**.
7. Fare clic su **Next** (Avanti) due volte e quindi su **Done** (Fine).

**driver di Phoenix hello tooinstall**

file jar di Hello phoenix driver si trova nel cluster HBase hello. percorso di Hello è simile toohello seguenti, in base alle versioni hello:

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
È necessario toocopy è tooyour workstation in hello [cartella di installazione esce] / percorso lib.  il modo più semplice Hello è tooRDP in cluster hello e quindi utilizzare file copia e Incolla (CTRL + C e CTRL + V) toocopy è tooyour workstation.

**tooadd un tooSQuirreL driver Phoenix**

1. Aprire SQuirreL SQL Client dalla workstation.
2. Fare clic su hello **Driver** scheda hello sinistra.
3. Da hello **driver** menu, fare clic su **nuovo Driver**.
4. Immettere hello le seguenti informazioni:

   * **Name**: Phoenix
   * **Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Class Name**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Utente tutte le lettere minuscole nell'URL di esempio hello. È possibile usare il quorum zookeeper completo nel caso in cui uno di essi sia inattivo.  i nomi host Hello sono zookeeper0, zookeeper1 e zookeeper2.
     >
     >

     ![Driver di HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. Fare clic su **OK**.

**un cluster HBase di alias toohello toocreate**

1. Esce, fare clic su hello **alias** scheda hello sinistra.
2. Da hello **alias** menu, fare clic su **nuovo Alias**.
3. Immettere hello le seguenti informazioni:

   * **Nome**: nome hello del cluster HBase hello o qualsiasi nome desiderato.
   * **Driver**: Phoenix.  Nome del driver hello creato nella procedura precedente hello deve corrispondere.
   * **URL**: hello URL viene copiato dalla configurazione del driver. Verificare che toouser lettere minuscole.
   * **Nome utente**: può essere qualsiasi testo.  Poiché si utilizza la connettività VPN in questo caso, il nome di utente hello non viene usato affatto.
   * **Password**: può essere qualsiasi testo.

     ![Driver di HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. Fare clic su **Test**.
5. Fare clic su **Connetti**. Quando la connessione di hello, esce aspetto:

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun un test**

1. Fare clic su hello **SQL** scheda toohello destra Avanti **oggetti** scheda.
2. Copiare e incollare hello seguente codice:

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Fare clic su pulsante di esecuzione hello.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Passa indietro toohello **oggetti** scheda.
5. Espandere il nome di alias hello e quindi **tabella**.  Verrà visualizzata sotto la tabella nuova hello.

## <a name="next-steps"></a>Passaggi successivi
In questo articolo, si è appreso come toouse Phoenix Apache in HDInsight.  toolearn informazioni, vedere

* [Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.
* [Eseguire il provisioning di cluster HBase in rete virtuale di Azure][hdinsight-hbase-provision-vnet]: con l'integrazione di rete virtuale cluster HBase può essere distribuito toohello stessa virtuale rete delle applicazioni in modo che le applicazioni possono comunicare con HBase direttamente.
* [Configurare la replica di HBase in HDInsight](hdinsight-hbase-replication.md): informazioni su come la replica di HBase tooconfigure tra due Data Center di Azure.
* [Analizzare Twitter sentiment con HBase in HDInsight][hbase-twitter-sentiment]: informazioni su come toodo in tempo reale [analisi del sentiment](http://en.wikipedia.org/wiki/Sentiment_analysis) dei big data dall'utilizzo di HBase in un cluster Hadoop in HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
