---
title: aaaConnect tooSQL Database usano C e C++ | Documenti Microsoft
description: Esempio hello utilizzare il codice in questa Guida introduttiva toobuild un'applicazione moderna in C++ e supportato da un database relazionale potente nel cloud hello con Database SQL di Azure.
services: sql-database
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: 
ms.assetid: 07d9e0b1-3234-4f17-a252-a7559160a9db
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: cpp
ms.topic: article
ms.date: 03/06/2017
ms.author: edmacauley
ms.openlocfilehash: 9b581424c91bfdd93deb6914212629519a011d8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-toosql-database-using-c-and-c"></a>Connettersi tooSQL Database usano C e C++
Questo post è rivolta agli sviluppatori C e C++ tentativo tooconnect tooAzure database di SQL Server. Si è suddivisa in sezioni, è possibile passare sezione toohello che meglio acquisisce l'interesse dimostrato. 

## <a name="prerequisites-for-hello-cc-tutorial"></a>Prerequisiti per l'esercitazione C/C++ hello
Assicurarsi di avere hello seguenti elementi:

* Un account Azure attivo. Se non si ha un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita di Azure](https://azure.microsoft.com/pricing/free-trial/).
* [Visual Studio](https://www.visualstudio.com/downloads/) È necessario installare toobuild di componenti del linguaggio C++ hello ed eseguire questo esempio.
* [Sviluppo di Linux per Visual Studio](https://visualstudiogallery.msdn.microsoft.com/725025cf-7067-45c2-8d01-1e0fd359ae6e). Se si sviluppa in Linux, è necessario installare anche l'estensione di Visual Studio Linux hello. 

## <a id="AzureSQL"></a>Database SQL di Azure ed SQL Server nelle macchine virtuali
SQL Azure si basa su Microsoft SQL Server ed è progettato tooprovide a disponibilità elevata, ad alte prestazioni e servizio scalabile. Esistono molti vantaggi toousing SQL Azure tramite il database proprietario in esecuzione in locale. Con SQL Azure non hanno tooinstall, configurare, gestire o gestire il database, ma solo hello contenuto e struttura hello del database. Alcuni elementi tipici dei database che destano preoccupazione, ad esempio la ridondanza e la tolleranza di errore, sono incorporati. 

Azure attualmente offre due opzioni per l'hosting dei carichi di lavoro su SQL Server: database SQL di Azure, database come servizio ed SQL Server in Macchine virtuali (VM). Non, è possibile ottenere informazioni dettagliate sulle differenze di hello tra questi due ad eccezione del fatto che il database SQL di Azure è il modo migliore per nuove applicazioni basate su cloud tootake sfruttare hello risparmio sui costi e ottimizzazione delle prestazioni che i servizi cloud forniscono. Se si prevede di eseguire la migrazione o l'estensione locale cloud toohello applicazioni, SQL server nella macchina virtuale di Azure potrebbe funzionare la più appropriata per l'utente. tookeep le cose semplici per questo articolo, creare un database SQL di Azure. 

## <a id="ODBC"></a>Tecnologie di accesso ai dati: ODBC e OLE DB
TooAzure connessione database di SQL Server non è diversa e attualmente sono disponibili due modi tooconnect toodatabases: ODBC (Open Database connectivity) e OLE DB (Object Linking and Embedding database). Negli ultimi anni Microsoft si è allineata a [ODBC per l'accesso ai dati relazionali nativi](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/). ODBC è relativamente semplice e molto più veloce rispetto a OLE DB. Hello qui unico problema è che ODBC utilizza un'API di tipo C precedenti. 

## <a id="Create"></a>Passaggio 1: Creazione di un database SQL di Azure
Vedere hello [pagina Guida introduttiva](sql-database-get-started-portal.md) toolearn come toocreate un database di esempio.  In alternativa, è possibile seguire questo [breve video di due minuti](https://azure.microsoft.com/documentation/videos/azure-sql-database-create-dbs-in-seconds/) toocreate un database SQL di Azure utilizzando hello portale di Azure.

## <a id="ConnectionString"></a>Passaggio 2: Ottenere la stringa di connessione
Dopo che è stato eseguito il provisioning del database SQL di Azure, è necessario toocarry le seguenti informazioni di connessione toodetermine passaggi hello e aggiungere l'indirizzo IP del client per l'accesso del firewall. 

In [portale di Azure](https://portal.azure.com/), passare una stringa di connessione ODBC database SQL di Azure tooyour utilizzando hello **Mostra le stringhe di connessione di database** elencati come parte della sezione Panoramica hello per il database: 

![ODBCConnectionString](./media/sql-database-develop-cplusplus-simple/azureportal.png)

![ODBCConnectionStringProps](./media/sql-database-develop-cplusplus-simple/dbconnection.png)

Copiare il contenuto di hello di hello **ODBC (include Node. js) [autenticazione di SQL Server]** stringa. Utilizziamo questa stringa tooconnect successive dall'interprete riga di comando C++ ODBC. Questa stringa fornisce informazioni dettagliate, ad esempio driver di hello, server e altri parametri di connessione di database. 

## <a id="Firewall"></a>Passaggio 3: Aggiungere il firewall toohello IP
Passare toohello sezione di firewall per il server di Database e aggiungere il [firewall toohello IP del client utilizzando i seguenti passaggi](sql-database-configure-firewall-settings.md) toomake che è possibile stabilire una connessione ha esito positivo: 

![AddyourIPWindow](./media/sql-database-develop-cplusplus-simple/ip.png)

A questo punto, è stato configurato il database SQL di Azure e sono pronti tooconnect dal codice C++. 

## <a id="Windows"></a>Passaggio 4: Connessione da un'applicazione C/C++ per Windows
È possibile connettere facilmente tooyour [database SQL di Azure tramite ODBC in Windows tramite l'esempio](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29) che consente di compilare con Visual Studio. esempio Hello implementa un interprete della riga di comando ODBC che può essere utilizzati tooconnect tooour database SQL di Azure. In questo esempio accetta un file di Database origine nome file (DSN) come argomento della riga di comando o stringa di connessione dettagliata hello che è stati copiati in precedenza hello portale di Azure. Aprire la pagina delle proprietà per questo progetto hello e incollare la stringa di connessione hello come argomento di comando, come illustrato di seguito: 

![Propsfile DNS](./media/sql-database-develop-cplusplus-simple/props.png)

Assicurarsi di specificare i dettagli di autenticazione appropriato hello per il database come parte di tale stringa di connessione di database. 

Avviare toobuild applicazione hello è. Dovrebbe essere hello successiva finestra ha stabilito una connessione di convalida. È anche possibile eseguire alcuni comandi SQL di base come **Crea tabella** toovalidate la connettività di database:

![Comandi SQL](./media/sql-database-develop-cplusplus-simple/sqlcommands.png)

In alternativa, è possibile creare un file DSN hello guidata che viene avviata quando è specificato alcun argomento di comando. Si consiglia di provare anche questa opzione. È possibile usare questo file DSN per l'automazione e per proteggere le impostazioni di autenticazione: 

![Creare un file DSN](./media/sql-database-develop-cplusplus-simple/datasource.png)

Congratulazioni. A questo punto si è connessi tooAzure SQL scritte in C++ e ODBC in Windows. È possibile continuare la lettura toodo hello stesso per la piattaforma Linux nonché. 

## <a id="Linux"></a>Passaggio 5: Connessione da un'applicazione C/C++ per Linux
Nel caso in cui non si è venuti a notizie hello ancora Visual Studio consente ora toodevelop anche applicazioni Linux C++. Informazioni su questo nuovo scenario di hello [Visual C++ per lo sviluppo di Linux](https://blogs.msdn.microsoft.com/vcblog/2016/03/30/visual-c-for-linux-development/) blog. toobuild per Linux, è necessario un computer remoto in cui è in esecuzione la distribuzione di Linux. Se non si ha disponibile un computer remoto con Linux, è possibile configurarlo rapidamente seguendo i passaggi presenti nell'articolo [Linux Azure Virtual machines](../virtual-machines/linux/quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Macchine virtuali di Linux in Azure). 

Per questa esercitazione, si supponga di avere configurata una distribuzione di Linux Ubuntu 16.04. Questa procedura Hello, applicare anche tooUbuntu 15.10, Red Hat 6 e 7 di Red Hat. 

Hello segue installare librerie hello necessari per ODBC e SQL per la distribuzione:

    sudo su
    sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/mssql-ubuntu-test/ xenial main" > /etc/apt/sources.list.d/mssqlpreview.list'
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    apt-get update
    apt-get install msodbcsql
    apt-get install unixodbc-dev-utf16 #this step is optional but recommended*

Avviare Visual Studio. In Strumenti -> Opzioni -> multipiattaforma -> Gestione connessione, aggiungere una casella di Linux tooyour connessione: 

![Opzioni degli strumenti](./media/sql-database-develop-cplusplus-simple/tools.png)

Dopo aver stabilito la connessione tramite SSH, creare un modello di progetto vuoto (Linux): 

![Nuovo modello di progetto](./media/sql-database-develop-cplusplus-simple/template.png)

È quindi possibile aggiungere un [nuovo file di origine C e sostituirlo con questo contenuto](https://github.com/Microsoft/VCSamples/blob/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29/odbcconnector/odbcconnector.c). Utilizzando hello SQLAllocHandle API ODBC e SQLSetConnectAttr SQLDriverConnect, si deve essere in grado di tooinitialize e impostare un database tooyour di connessione. Come esempio ODBC Windows hello, è necessario tooreplace hello SQLDriverConnect chiamata con dettagli hello da parametri di stringa di connessione del database copiato dal portale di Azure hello in precedenza. 

     retcode = SQLDriverConnect(
        hdbc, NULL, "Driver=ODBC Driver 13 for SQL"
                    "Server;Server=<yourserver>;Uid=<yourusername>;Pwd=<"
                    "yourpassword>;database=<yourdatabase>",
        SQL_NTS, outstr, sizeof(outstr), &outstrlen, SQL_DRIVER_NOPROMPT);

Hello ultima operazione toodo prima che la compilazione venga tooadd **odbc** come dipendenze della libreria: 

![Aggiunta di ODBC come libreria di input](./media/sql-database-develop-cplusplus-simple/lib.png)

toolaunch l'applicazione, aprire la Linux Console hello da hello **Debug** menu: 

![Console Linux](./media/sql-database-develop-cplusplus-simple/linuxconsole.png)

Se la connessione ha esito positivo, dovrebbe essere hello nome del database corrente stampato nella Linux Console hello: 

![Output della finestra della console Linux](./media/sql-database-develop-cplusplus-simple/linuxconsolewindow.png)

Congratulazioni. È stata completata l'esercitazione hello e può stabilire una connessione tooyour database SQL di Azure da C++ nelle piattaforme Windows e Linux.

## <a id="GetSolution"></a>Ottenere una soluzione dell'esercitazione C/C++ completa hello
È possibile trovare una soluzione di GetStarted hello che contiene tutti gli esempi di hello in questo articolo in github:

* [Esempio di Windows in C++ ODBC](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28windows%29), scaricare tooAzure tooconnect di esempio ODBC C++ di Windows hello SQL
* [Esempio di ODBC C++ Linux](https://github.com/Microsoft/VCSamples/tree/master/VC2015Samples/ODBC%20database%20sample%20%28linux%29), scaricare hello esempio ODBC in Linux C++ tooconnect tooAzure SQL

## <a name="next-steps"></a>Passaggi successivi
* Hello revisione [Cenni preliminari sullo sviluppo di Database SQL](sql-database-develop-overview.md)
* Ulteriori informazioni su hello [riferimento all'API ODBC](https://docs.microsoft.com/sql/odbc/reference/syntax/odbc-api-reference/)

## <a name="additional-resources"></a>Risorse aggiuntive
* [Schemi progettuali per applicazioni SaaS multi-tenant con il database SQL di Azure](sql-database-design-patterns-multi-tenancy-saas-applications.md)
* Esplorare tutti hello [funzionalità del Database SQL](https://azure.microsoft.com/services/sql-database/)

