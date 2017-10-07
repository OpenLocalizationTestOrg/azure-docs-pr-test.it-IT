---
title: aaaUse SSH tunneling tooaccess Azure HDInsight | Documenti Microsoft
description: Informazioni su come toouse un toosecurely tunnel SSH individuare le risorse web ospitate sui nodi di HDInsight basati su Linux.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a>Usare SSH Tunneling tooaccess Ambari web dell'interfaccia utente, JobHistory, NameNode, Oozie e altre interfacce utente web

Cluster HDInsight basati su Linux forniscono l'interfaccia utente web tooAmbari accesso tramite Internet hello, ma alcune funzionalità di hello dell'interfaccia utente non sono. Ad esempio, hello web dell'interfaccia utente per altri servizi che vengono rilevate tramite Ambari. Per le funzionalità complete di hello Ambari web dell'interfaccia utente, è necessario utilizzare un'intestazione di cluster toohello tunnel SSH.

## <a name="why-use-an-ssh-tunnel"></a>Perché usare un tunnel SSH

Molti dei menu hello in Ambari funzionano solo tramite un tunnel SSH. Questi menu si basano su servizi e siti Web in esecuzione in altri tipi di nodi, ad esempio i nodi di lavoro. Spesso questi siti web non sono protetti, pertanto non è sicuro toodirectly espongono in hello internet.

Hello segue le interfacce utente Web richiede un tunnel SSH:

* JobHistory
* NameNode
* Thread Stacks
* Interfaccia utente Web di Oozie
* HBase Master e l'interfaccia utente di Log

Se si utilizza toocustomize azioni Script del cluster, tutti i servizi o le utilità che si installa che espongono un'interfaccia utente web richiedono un tunnel SSH. Ad esempio, se si installa tonalità utilizzando un'azione di Script, è necessario utilizzare un SSH tunnel tooaccess hello tonalità interfaccia utente web.

> [!IMPORTANT]
> Se si dispone di accesso diretto tooHDInsight attraverso una rete virtuale, non è necessario toouse SSH tunnel. Per un esempio di accedere direttamente alle HDInsight tramite una rete virtuale, vedere hello [rete locale di connettersi a HDInsight tooyour](connect-on-premises-network.md) documento.

## <a name="what-is-an-ssh-tunnel"></a>Che cos'è un tunnel SSH

[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) instrada il traffico inviato tooa porta nella workstation locale. Hello traffico viene indirizzato attraverso un SSH connessione tooyour HDInsight nodo head del cluster. richiesta di Hello viene risolto come se avesse origine nel nodo head hello. risposta Hello viene indirizzato attraverso la workstation di tooyour tunnel hello.

## <a name="prerequisites"></a>Prerequisiti

* Un client SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Un browser web che può essere configurato un proxy SOCKS5 toouse.

    > [!WARNING]
    > supporto dei proxy SOCKS Hello incorporato in Windows non supporta SOCKS5 e non funziona con i passaggi di hello in questo documento. Hello browser seguenti si basano sulle impostazioni di proxy di Windows e operazioni non attualmente con passaggi hello in questo documento:
    >
    > * Microsoft Edge
    > * Microsoft Internet Explorer
    >
    > Google Chrome utilizza inoltre le impostazioni proxy di Windows hello. In questo caso, tuttavia, è possibile installare estensioni che supportano SOCKS5, tra cui [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp) (opzione consigliata).

## <a name="usessh"></a>Creare un tunnel comando SSH hello

Comando che segue hello utilizzare toocreate un tunnel SSH utilizzando hello `ssh` comando. Sostituire **USERNAME** con un utente SSH per il cluster HDInsight e sostituire **CLUSTERNAME** con nome hello del cluster HDInsight:

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

Questo comando crea una connessione che consenta di instradare i cluster di traffico toolocal porta 9876 toohello su SSH. Hello opzioni sono:

* **D 9876** -hello porta locale che instrada il traffico attraverso il tunnel hello.
* **C** : comprime tutti i dati, in quanto il traffico Web è costituito prevalentemente da testo.
* **2** -force SSH tootry protocol versione 2 solo.
* **q** : modalità non interattiva.
* **T** : disabilita l'allocazione pseudo-tty perché si tratta semplicemente dell'inoltro di una porta.
* **n**: impedisce la lettura di STDIN perché si tratta semplicemente dell'inoltro di una porta.
* **N** : non esegue un comando remoto perché si tratta semplicemente dell'inoltro di una porta.
* **f** -eseguito in background hello.

Al termine del comando hello, il traffico inviato tooport 9876 nel computer locale hello è indirizzato toohello nodo head del cluster.

## <a name="useputty"></a>Creare un tunnel utilizzando PuTTY

[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) è un client SSH grafico per Windows. Utilizzare i seguenti passaggi toocreate un tunnel SSH tramite PuTTY hello:

1. Aprire PuTTY e immettere le informazioni di connessione. Se non si ha familiarità con PuTTY, vedere hello [PuTTY documentazione (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).

2. In hello **categoria** toohello sezione a sinistra della finestra di dialogo hello, espandere **connessione**, espandere **SSH**, quindi selezionare **tunnel**.

3. Fornire le seguenti informazioni su hello hello **opzioni che controllano SSH inoltro alla porta** form:
   
   * **Porta di origine** -hello porta sul client hello che si desidera tooforward. Ad esempio, **9876**.

   * **Destinazione** -hello indirizzo SSH per cluster HDInsight basati su Linux hello. Ad esempio, **mycluster-ssh.azurehdinsight.net**.

   * **Dynamic** : consente il routing tramite proxy SOCKS dinamico.
     
     ![image of tunneling options](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. Fare clic su **Aggiungi** tooadd hello impostazioni e quindi fare clic su **aprire** tooopen una connessione SSH.

5. Quando richiesto, accedere toohello server.

## <a name="use-hello-tunnel-from-your-browser"></a>Utilizzare tunnel hello dal browser

> [!IMPORTANT]
> Hello passaggi hello di utilizzare questa sezione del browser Mozilla FireFox, in quanto forniscono hello stesse impostazioni del proxy in tutte le piattaforme. Altri browser moderni, ad esempio Google Chrome, potrebbe richiedere un'estensione, ad esempio toowork FoxyProxy con tunnel hello.

1. Configurare hello browser toouse **localhost** e porta hello è utilizzato quando la creazione di tunnel hello come un **SOCKS v5** proxy. Ecco le impostazioni di Firefox hello aspetto. Se si utilizza una porta diversa da quella 9876, modificare toohello porta hello che è utilizzato:
   
    ![image of Firefox settings](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > Selezione **DNS remoto** risolve le richieste di sistema DNS (Domain Name) con i cluster HDInsight hello. Questa impostazione consente di risolvere DNS tramite hello del nodo head del cluster di hello.

2. Verificare il funzionamento di tale tunnel hello, visitare un sito, ad esempio [http://www.whatismyip.com/](http://www.whatismyip.com/). IP Hello restituito deve essere utilizzato da Data Center di Microsoft Azure hello.

## <a name="verify-with-ambari-web-ui"></a>Verificare con l’interfaccia utente web di Ambari

Dopo aver stabilito cluster hello, utilizzare hello tooverify passaggi che è possibile accedere servizio web, le interfacce utente da hello Ambari Web seguente:

1. Nel browser passare toohttp://headnodehost:8080. Hello `headnodehost` indirizzo viene inviato su cluster di toohello tunnel hello e risolvere il nodo head toohello Ambari in esecuzione in. Quando richiesto, immettere nome utente amministratore di hello (amministratore) e la password per il cluster. Può essere richiesto un secondo momento da hello Ambari web dell'interfaccia utente. In questo caso, immettere nuovamente le informazioni di hello.

   > [!NOTE]
   > Quando si utilizza hello http://headnodehost:8080 indirizzo tooconnect toohello cluster, ci si connette tramite il tunnel hello. Comunicazione sia protetta con tunnel SSH hello anziché HTTPS. tooconnect oltre hello internet tramite HTTPS, utilizzare https://CLUSTERNAME.azurehdinsight.net, in cui **CLUSTERNAME** hello nome del cluster di hello.

2. Nell'elenco di hello sulla sinistra hello della pagina di hello hello dell'interfaccia utente Web Ambari, selezionare HDFS.

    ![Immagine con HDFS selezionata](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. Selezionare la visualizzazione di informazioni sul servizio HDFS hello **collegamenti rapidi**. Viene visualizzato un elenco di nodi head del cluster hello. Selezionare uno dei nodi head hello e quindi selezionare **NameNode UI**.

    ![Immagine con menu collegamenti rapidi hello espanso](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > Quando si seleziona __Quick Links__ (Collegamenti rapidi), è possibile che venga visualizzato un indicatore di attesa. Questa condizione può verificarsi se la connessione Internet è lenta. Attendere un minuto o due per hello dati toobe ricevuto dal server hello, quindi ripetere l'operazione elenco hello.
   >
   > Alcune voci hello **collegamenti rapidi** menu può essere tagliato da hello destra dello schermo hello. In questo caso, espandere il menu di hello utilizzando il mouse e utilizzare hello freccia destra tooscroll chiave hello schermata toohello toosee destra hello resto del menu hello.

4. Viene visualizzato un toohello simile pagina seguente immagine:

    ![Immagine di hello NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > Si noti hello URL della pagina. dovrebbe essere simile troppo**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**. Questo URI utilizza hello interno completamente nome di dominio completo (FQDN) del nodo hello ed è accessibile solo quando si usa un tunnel SSH.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come toocreate e utilizzare un tunnel SSH, vedere hello documento per altri toouse modi Ambari seguenti:

* [Gestire i cluster HDInsight mediante Ambari](hdinsight-hadoop-manage-ambari.md)

Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

