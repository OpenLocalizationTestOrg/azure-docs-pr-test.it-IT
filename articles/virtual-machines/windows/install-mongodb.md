---
title: aaaInstall MongoDB in una macchina virtuale Windows in Azure | Documenti Microsoft
description: Informazioni su come creare i tooinstall MongoDB in una macchina virtuale di Azure che esegue Windows Server 2012 R2 con modello di distribuzione di gestione risorse di hello.
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Installare e configurare MongoDB in una VM Windows in Azure
[MongoDB](http://www.mongodb.org) è un diffuso database NoSQL open source a prestazioni elevate. In questo articolo viene illustrata la procedura di installazione e configurazione di MongoDB in una macchina virtuale (VM) Windows Server 2012 R2 in Azure. È anche possibile [installare MongoDB in una VM Linux in Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Prerequisiti
Prima di installare e configurare MongoDB, è necessario toocreate una macchina virtuale e, idealmente, aggiungere un tooit disco dati. Vedere i seguenti articoli toocreate una macchina virtuale hello e aggiungere un disco dati:

* Creare una macchina virtuale Windows Server utilizzando [hello Azure portal](quick-create-portal.md) o [Azure PowerShell](quick-create-powershell.md).
* Collegare un dati disco tooa macchina virtuale Windows Server tramite [hello Azure portal](attach-managed-disk-portal.md) o [Azure PowerShell](attach-disk-ps.md).

toobegin installazione e configurazione di MongoDB, [accedere tooyour macchina virtuale Windows Server](connect-logon.md) tramite Desktop remoto.

## <a name="install-mongodb"></a>Installare MongoDB
> [!IMPORTANT]
> Le funzionalità di sicurezza MongoDB, ad esempio l'autenticazione e l'associazione di indirizzi IP, non sono abilitate per impostazione predefinita. Funzionalità di sicurezza devono essere abilitate prima di distribuire l'ambiente di produzione tooa MongoDB. Per altre informazioni, vedere [MongoDB Security and Authentication](http://www.mongodb.org/display/DOCS/Security+and+Authentication) (Sicurezza e autenticazione di MongoDB).


1. Dopo aver collegato tooyour macchina virtuale tramite Desktop remoto, aprire Internet Explorer da hello **avviare** menu hello macchina virtuale.
2. All'apertura di Internet Explorer, selezionare **Usa impostazioni di sicurezza, privacy e compatibilità consigliate** e fare clic su **OK**.
3. La configurazione di protezione avanzata di Internet Explorer è abilitata per impostazione predefinita. Aggiungere hello MongoDB toohello l'elenco dei siti dei siti consentiti:
   
   * Seleziona hello **strumenti** sull'icona nell'angolo superiore destro di hello.
   * In **Opzioni Internet**selezionare hello **sicurezza** scheda e quindi selezionare hello **siti attendibili** icona.
   * Fare clic su hello **siti** pulsante. Aggiungere *https://\*. mongodb.org* toohello elenco siti attendibili e quindi chiudere hello, finestra di dialogo.
     
     ![Configurare le impostazioni di sicurezza di Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Sfoglia toohello [MongoDB - Scarica](http://www.mongodb.org/downloads) pagina (http://www.mongodb.org/downloads).
5. Se necessario, selezionare hello **Server Community** edition e quindi selezionare hello versione più recente corrente stabile per Windows Server 2008 R2 64 bit e versioni successive. toodownload hello programma di installazione, fare clic su **DOWNLOAD (msi)**.
   
    ![Scaricare il programma di installazione di MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Eseguire il programma di installazione hello dopo aver completato il download di hello.
6. Leggere e accettare il contratto di licenza hello. Quando richiesto, selezionare **Completa** per l'installazione.
7. Nella schermata finale hello, fare clic su **installare**.

## <a name="configure-hello-vm-and-mongodb"></a>Configurare hello VM e MongoDB
1. le variabili di percorso Hello non vengono aggiornate dal programma di installazione di hello MongoDB. Senza hello MongoDB `bin` posizione, la variabile path, è necessario percorso completo di hello toospecify ogni volta che si utilizza un file eseguibile di MongoDB. variabile di percorso tooyour posizione hello tooadd:
   
   * Pulsante destro del mouse hello **avviare** dal menu **sistema**.
   * Fare clic sulla scheda **Impostazioni di sistema avanzate**, quindi su **Variabili d'ambiente**.
   * In **Variabili di sistema** selezionare **Percorso**, quindi fare clic su **Modifica**.
     
     ![Configurare le variabili di PERCORSO](./media/install-mongodb/configure-path-variables.png)
     
     Aggiungi percorso di hello tooyour MongoDB `bin` cartella. MongoDB viene in genere installato in *C:\Programmi\MongoDB*. Verificare il percorso di installazione hello nella macchina virtuale. esempio Hello aggiunge hello predefinito MongoDB installazione percorso toohello `PATH` variabile:
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Punto e virgola iniziale di hello tooadd assicurarsi di essere (`;`) che si sta aggiungendo un percorso tooyour tooindicate `PATH` variabile.

2. Creare le directory di log e dati di MongoDB nel disco dati. Da hello **avviare** dal menu **prompt dei comandi**. seguono esempi Hello Crea directory hello nell'unità f:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Avviare un'istanza di MongoDB con hello comando seguente, modificare dati tooyour del percorso hello e directory del Registro di conseguenza:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Può richiedere alcuni minuti per MongoDB tooallocate file journal hello e avvia l'ascolto delle connessioni. Tutti i messaggi di log sono diretto toohello *F:\MongoLogs\mongolog.log* file come `mongod.exe` server verrà avviato e alloca file journal.
   
   > [!NOTE]
   > prompt dei comandi di Hello rimane attivo per l'attività mentre è in esecuzione l'istanza di MongoDB. Lasciare hello prompt dei comandi finestra aperta toocontinue sia in esecuzione MongoDB. In alternativa, installare MongoDB come servizio, come descritto nel passaggio successivo hello.

4. Per un'esperienza più affidabile di MongoDB, installare hello `mongod.exe` come servizio. Creazione di un servizio, significa che è necessario tooleave un prompt dei comandi in esecuzione ogni volta che si desidera toouse MongoDB. Creare il servizio hello come indicato di seguito, regolando hello percorso tooyour log directory di dati e di conseguenza:
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Hello comando precedente crea un servizio denominato MongoDB, con una descrizione di "Mongo DB". è stata specificata anche Hello seguenti parametri:
   
   * Hello `--dbpath` opzione specifica hello percorso della directory di dati hello.
   * Hello `--logpath` opzione deve essere toospecify utilizzato un file di log, perché servizio in esecuzione hello non dispone di un output toodisplay finestra di comando.
   * Hello `--logappend` opzione specifica che un riavvio del servizio hello provoca output tooappend toohello file di log esistente.
   
   servizio di MongoDB di hello di toostart, eseguire il comando seguente hello:
   
    ```
    net start MongoDB
    ```
   
    Per ulteriori informazioni sulla creazione di hello MongoDB servizio, vedere [configurare un servizio Windows per MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Istanza di prova hello MongoDB
Con MongoDB in esecuzione come istanza singola o installato come servizio, è possibile avviare la creazione e l'uso dei database. hello toostart shell amministrativa MongoDB, aprire un'altra finestra del prompt dei comandi da hello **avviare** menu, quindi immettere hello comando seguente:

```
mongo  
```

È possibile elencare i database hello con hello `db` comando. Inserire alcuni dati come mostrato di seguito:

```
db.foo.insert( { a : 1 } )
```

Cercare i dati come mostrato di seguito:

```
db.foo.find()
```

Hello l'output è simile toohello seguente esempio:

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Hello uscita `mongo` console come segue:

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Configurare le regole del firewall e del gruppo di sicurezza di rete
Ora che MongoDB è installato e in esecuzione, aprire una porta in Windows Firewall in modo è possibile connettersi in remoto tooMongoDB. toocreate una nuova regola connessioni in entrata tooallow porta 27017, aprire un prompt dei comandi amministrativi di PowerShell e immettere hello comando seguente:

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

È anche possibile creare regole hello utilizzando hello **Windows Firewall con sicurezza avanzata** strumento di gestione con interfaccia grafica. Creare una nuova regola connessioni in entrata tooallow porta 27017.

Se necessario, creare un gruppo di sicurezza di rete regola tooallow accesso tooMongoDB di fuori di subnet di rete virtuale di Azure esistente hello. È possibile creare regole del gruppo di sicurezza di rete hello utilizzando hello [portale di Azure](nsg-quickstart-portal.md) o [Azure PowerShell](nsg-quickstart-powershell.md). Come con le regole Firewall di Windows hello, consentire l'interfaccia di rete virtuale toohello 27017 porta TCP di VM MongoDB.

> [!NOTE]
> La porta TCP 27017 è utilizzata da MongoDB la porta predefinita hello. È possibile modificare la porta tramite hello `--port` parametro quando si avvia `mongod.exe` manualmente o da un servizio. Se si modifica la porta hello, apportare che tooupdate hello Windows regole Firewall e di gruppo di sicurezza di rete nel hello passaggi precedenti.


## <a name="next-steps"></a>Passaggi successivi
In questa esercitazione, si è appreso come tooinstall e configurare MongoDB nella VM Windows. È ora possibile accedere MongoDB nella VM Windows, di seguito hello avanzata nel hello [documentazione di MongoDB](https://docs.mongodb.com/manual/).

