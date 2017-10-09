---
title: 'Avvio rapido: Creare un database di Azure per il server MySQL - Portale di Azure | Microsoft Docs'
description: Passaggi in questo articolo si tramite hello tooquickly portale Azure creare un Database di Azure di esempio per il server MySQL in circa cinque minuti.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Creare un database di Azure per il server MySQL tramite il portale di Azure
Il Database di Azure per MySQL è un servizio gestito che consente di toorun, gestire e scalare il database MySQL a disponibilità elevata nel cloud hello. Questa Guida introduttiva viene illustrato come toocreate un Azure di Database per server di MySQL mediante hello portale di Azure in circa cinque minuti. 

Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.

## <a name="log-in-tooazure"></a>Accedi tooAzure
Aprire il web browser e passare toohello [portale Microsoft Azure](https://portal.azure.com/). Immettere le credenziali toosign nel portale toohello. visualizzazione predefinita Hello è il dashboard del servizio.

## <a name="create-azure-database-for-mysql-server"></a>Creare un database di Azure per il server MySQL
Verrà creato un database di Azure per MySQL con un set definito di [risorse di calcolo e di archiviazione](./concepts-compute-unit-and-storage.md). Hello server viene creato all'interno di un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md).

Seguire questi toocreate passaggi un Database di Azure per il server MySQL:

1. Fare clic su hello **New** pulsante (+) in hello angolo superiore sinistro del portale di Azure hello.

2. Selezionare **database** da hello **New** pagina e selezionare **Database di Azure per MySQL** da hello **database** pagina. È anche possibile digitare **MySQL** nel nuovo servizio di hello toofind pagina ricerca casella hello.
![Portale di Azure - Nuovo - Database - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Compilare hello nuovi server Dettagli modulo con hello le seguenti informazioni, come mostrato nella precedente immagine hello:

    **Impostazione** | **Valore consigliato** | **Descrizione campo** 
    ---|---|---
    Nome server | myserver4demo | Scegliere un nome univoco per identificare il database di Azure per il server MySQL. nome di dominio Hello *mysql.database.azure.com* è il nome di server aggiunti toohello Fornisci per tooconnect di applicazioni per. nome del server Hello può contenere solo lettere minuscole, numeri e caratteri di trattino (-) hello e deve contenere da 3 a 63 caratteri.
    Sottoscrizione | Sottoscrizione in uso | Hello sottoscrizione di Azure che si desidera toouse per il server. Se si dispone di più sottoscrizioni, scegliere in cui la risorsa hello viene fatturata per la sottoscrizione appropriata hello.
    Gruppo di risorse | myresourcegroup | È possibile creare un nuovo nome di gruppo di risorse o usarne uno esistente nella sottoscrizione.
    Accesso amministratore server | myadmin | Verificare la propria toouse di account di accesso durante la connessione server toohello. nome di account di accesso amministratore Hello non può essere 'azure_superuser', 'admin', 'administrator', 'root', 'guest' o 'public'.
    Password | *A scelta dell'utente* | Creare una nuova password per l'account amministratore di server hello. Deve contenere da 8 too128 caratteri. La password deve contenere caratteri di tre delle seguenti categorie di hello: inglese lettere maiuscole, lettere minuscole, numeri (0-9) e caratteri non alfanumerici (!, $, #, %, ecc.).
    Conferma password | *A scelta dell'utente*| Conferma password dell'account admin hello.
    Percorso | *utenti tooyour di Hello area più vicini*| Scegliere percorso hello è più vicino agli utenti di tooyour o altre applicazioni Azure.
    Versione | *Scegliere la versione più recente di hello*| Scegliere la versione più recente di hello, a meno che non si dispone di requisiti specifici.
    Piano tariffario | **Basic**, **50 unità di calcolo** **50 GB** | Fare clic su **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo database. Scegliere **livello Basic** nella scheda hello nella parte superiore di hello. Fare clic su hello estremità sinistra hello **unità di calcolo** dispositivo di scorrimento tooadjust hello valore toohello importo minimo disponibile per questa Guida rapida. Fare clic su **Ok** hello toosave dei prezzi di selezione. Vedere la seguente schermata hello.
    PIN toodashboard | Controllo | Controllare hello **toodashboard Pin** opzione tooallow facile rilevamento del server nella pagina dashboard anteriore hello del portale di Azure.

    > [!IMPORTANT]
    > account di accesso amministratore server Hello e una password che è possibile specificare sono necessari toolog toohello server e i relativi database più avanti in questa Guida rapida. Prendere nota di queste informazioni per usarle in seguito.
    > 

    ![Portale di Azure - creare MySQL fornendo l'input del form hello richiesto](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Fare clic su **crea** server hello tooprovision. Provisioning richiede alcuni minuti, i minuti too20 massimo.
   
5.  Sulla barra degli strumenti hello, fare clic su **notifiche** processo di distribuzione hello toomonitor (icona campana).

## <a name="configure-a-server-level-firewall-rule"></a>Configurare una regola del firewall a livello di server

Hello Azure Database per il servizio MySQL consente di creare un firewall a livello di server hello. Questo firewall impedisce applicazioni esterne e gli strumenti di connessione toohello server e tutti i database nel server di hello, solo una regola del firewall creata firewall hello tooopen per indirizzi IP specifici. 

1.  Individuare il server al termine della distribuzione hello. Se necessario, è possibile eseguire una ricerca. Ad esempio, fare clic su **tutte le risorse** dal menu a sinistra hello e digitare il nome di server hello (ad esempio esempio hello *myserver4demo*) toosearch per il server appena creato. Fare clic sul nome del server elencato nei risultati di ricerca hello. Hello **Panoramica** pagina per il server viene aperto e offre opzioni per un'ulteriore configurazione.

2. Nella pagina server hello selezionare **sicurezza della connessione**.

3.  In hello **regole del Firewall** fare clic su nella casella di testo vuoto hello hello **nome regola** toobegin colonna creazione hello regola del firewall. 

    Per questa Guida rapida, di seguito consentono di tutti gli indirizzi IP in server hello immettendo nella casella di testo hello in ogni colonna con hello seguenti valori:

    Nome regola | Indirizzo IP iniziale | Indirizzo IP finale 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Sulla barra degli strumenti superiore hello di hello **sicurezza della connessione** pagina, fare clic su **salvare**. Attendere qualche istante e notifica hello informativa che mostra che l'aggiornamento di sicurezza della connessione è stato completato prima di continuare.

    > [!NOTE]
    > Connessioni tooAzure Database per MySQL comunicare 3306 la porta. Se si sta tentando di tooconnect da una rete aziendale, il traffico in uscita sulla porta 3306 può non essere consentito dal firewall della rete. In questo caso, non sarà in grado di tooconnect tooyour server, a meno che il reparto IT apre la porta 3306.
    > 

## <a name="get-hello-connection-information"></a>Ottenere informazioni sulla connessione hello
server di database tooyour tooconnect, è necessario tooremember hello server completo dall'amministratore e nome credenziali di accesso. Tali valori in precedenza nell'articolo della Guida rapida di hello potrebbe avere indicate. Nel caso in cui non è stato eseguito, il server di hello è possibile trovare facilmente informazioni di accesso tramite nome e dal server hello **Panoramica** pagina o hello **proprietà** pagina hello portale di Azure.

1. Aprire la pagina **Panoramica** del server. Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**. 
    Posiziona il cursore sulla ogni campo e icona Copia hello toohello destra del testo hello. Fare clic sull'icona di copia hello come valori hello toocopy necessari.

    In questo esempio, è il nome di server hello *myserver4demo.mysql.database.azure.com*, e l'account di accesso amministratore server hello è  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Connettersi usando lo strumento da riga di comando di mysql tooMySQL
Esistono un numero di applicazioni è possibile utilizzare tooconnect tooyour Database di Azure per il server MySQL. Consente di usare innanzitutto hello [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) della riga di comando dello strumento tooillustrate come tooconnect toohello server.  È possibile utilizzare un web browser e della Shell di Cloud di Azure come descritto di seguito senza hello hello necessario tooinstall software aggiuntivo. Se si dispone di utilità di mysql hello installato localmente nel computer, è possibile connettersi anche da quest '.

1. Avviare hello Shell di Cloud di Azure tramite l'icona terminal hello (> _) su hello parte superiore destra della pagina web del portale Azure hello.

2. Hello Azure Cloud Shell apre nel browser, consentendo tootype i comandi della shell bash.

    ![Prompt dei comandi - Esempio di riga di comando mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. Al prompt della Shell Cloud hello connettersi tooyour Database di Azure per il server MySQL digitando una riga di comando di mysql hello al prompt dei comandi hello verde.

    Hello seguente formato viene usato tooconnect tooan Database di Azure per il server MySQL con l'utilità di mysql hello:
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Ad esempio, hello comando seguente si connette a server di esempio tooour:
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    Parametro di mysql |Valore consigliato|Descrizione
    ---|---|---
    --host | *nome del server* | Specificare hello server valore del nome è stato utilizzato durante la creazione hello Database di Azure per MySQL in precedenza. Il server di esempio visualizzato è myserver4demo.mysql.database.azure.com. Utilizza il nome di dominio completo hello (\*. mysql.database.azure.com) come illustrato nell'esempio hello. Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda il nome del server. 
    --user | *nome di accesso amministratore server* |Digitare nome utente account di accesso amministratore server hello specificato durante la creazione del Database di Azure hello per MySQL in precedenza. Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda hello username.  formato hello è  *username@servername* .
    --password | *attendere finché non viene richiesta* | Verrà richiesto troppo "Immettere la password" dopo aver immettere il comando hello. Quando richiesto, digitare hello stessa password fornita durante la creazione di server hello.  Hello nota tipizzati caratteri non vengono visualizzati in bash hello prompt dei comandi quando si digitano le password. Premere INVIO dopo aver digitato tutti hello caratteri tooauthenticate e connettersi.

   Una volta connessi, utilità mysql hello viene visualizzato un `mysql>` prompt dei comandi per l'utente tootype comandi. 

    Output di mysql di esempio:
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Se hello firewall non è configurato l'indirizzo IP tooallow hello del hello Shell di Cloud di Azure, hello seguente errore:
    >
    > Errore 2003 (28000): Il Client con indirizzo IP 123.456.789.0 server hello tooaccess non è consentito.
    >
    > Errore di hello tooresolve, verificare che hello server configuration corrispondenze hello passaggi hello *configurare una regola firewall di livello server* sezione dell'articolo hello.

4. Vista server stato tooensure hello connessione è funzionale. Tipo `status` a mysql hello > richiesto quando è connesso.
    ```sql
    status
    ```

   > [!TIP]
   > Per altri comandi, vedere il capitolo 4.5.1 di [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) (Manuale di riferimento di MySQL 5.7).

5.  Creare un database vuoto a mysql hello > prompt dei comandi digitando hello comando seguente:
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    comando Hello potrebbe richiedere alcuni istanti toocomplete. 

    In un database di Azure per il server MySQL è possibile creare uno o più database. È possibile rifiutare un singolo database per ogni server tooutilize toocreate tutte le risorse di hello o creare più database tooshare risorse hello. Non esiste alcun toohello limita il numero di database che possono essere creati, ma più database condividono hello stesse risorse di server. 

6. Elenco di database mysql hello hello > prompt dei comandi digitando hello comando seguente:

    ```sql
    SHOW DATABASES;
    ```

7.  Tipo `\q` e quindi premere strumento mysql hello tooquit di invio. Dopo avere completato, è possibile chiudere hello Shell di Cloud di Azure.

Si dispone ora connessi toohello Database di Azure per MySQL e creato un database utente vuoto. Continuare toohello successiva sezione toorepeat un simile toohello tooconnect esercizio stesso server con un altro strumento comune, MySQL Workbench.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Connessione server toohello strumento GUI Workbench MySQL hello
utilizzo dello strumento GUI hello Workbench di MySQL server tooconnect tooAzure MySQL:

1.  Avviare hello applicazione Workbench di MySQL nel computer client. È possibile scaricare e installare MySQL Workbench da [qui](https://dev.mysql.com/downloads/workbench/).

2.  In **il programma di installazione nuova connessione** finestra di dialogo immettere le seguenti informazioni hello **parametri** scheda:

    ![Setup New Connection (Configura nuova connessione)](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Impostazione** | **Valore consigliato** | **Descrizione campo** |
    |---|---|---|
    |   Connection Name (Nome connessione) | Demo Connection | Specificare un'etichetta per la connessione. |
    | Connection Method (Metodo di connessione) | Standard (TCP/IP) | Standard (TCP/IP) è sufficiente. |
    | Nome host | *nome del server* | Specificare hello server valore del nome è stato utilizzato durante la creazione hello Database di Azure per MySQL in precedenza. Il server di esempio visualizzato è myserver4demo.mysql.database.azure.com. Utilizza il nome di dominio completo hello (\*. mysql.database.azure.com) come illustrato nell'esempio hello. Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda il nome del server.  |
    | Porta | 3306 | Utilizzare sempre porta 3306 durante la connessione di Database tooAzure per MySQL. |
    | Username |  *nome di accesso amministratore server* | Digitare nome utente account di accesso amministratore server hello specificato durante la creazione del Database di Azure hello per MySQL in precedenza. Il nome utente dell'esempio è myadmin@myserver4demo. Seguire i passaggi di hello in hello precedente sezione tooget hello le informazioni di connessione se non si ricorda hello username. formato hello è  *username@servername* .
    | Password | Immettere la password. | Fare clic su archiviare nell'insieme di credenziali... la password di hello toosave pulsante. |

    Fare clic su **Test connessione** tootest se tutti i parametri siano configurati correttamente. Fare clic su OK toosave hello connessione. 

    > [!NOTE]
    > SSL viene applicato per impostazione predefinita sul server e richiede configurazioni aggiuntive in ordine tooconnect correttamente. Vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](./howto-configure-ssl.md).  Se si desidera toodisable SSL per questa Guida rapida, visitare il portale di Azure hello e fare clic su hello connessione sicurezza pagina toodisable hello applicare SSL connessione interruttore.

## <a name="clean-up-resources"></a>Pulire le risorse
Pulire le risorse di hello creato nella Guida introduttiva hello uno eliminando hello [gruppo di risorse](../azure-resource-manager/resource-group-overview.md), che include tutte le risorse di hello nel gruppo di risorse hello o eliminando la risorsa di un server hello se si desidera tookeep hello altre risorse intatti.

> [!TIP]
> Altre guide introduttive della raccolta si basano su questa. Se si intende toocontinue toowork con successive Guide rapide, eseguire la pulizia hello le risorse create in questa Guida rapida. Se non si prevede toocontinue, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa Guida rapida nel portale di Azure hello.
>

toodelete hello intero gruppo di risorse tra cui server hello appena creato:
1.  Individuare il gruppo di risorse nel portale di Azure hello. Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello del gruppo di risorse, ad esempio esempio **myresourcegroup**.
2.  Nella pagina del gruppo di risorse fare clic su **Elimina**. Quindi hello del tipo del gruppo di risorse, ad esempio esempio **myresourcegroup**in hello di eliminazione tooconfirm casella di testo e quindi fare clic su **eliminare**.

O invece hello toodelete appena creata server:
1.  Se non si dispone, aprire, individuare il server nel portale di Azure hello. Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse**e quindi cercare server hello è stato creato.
2.  In hello **Panoramica** pagina, fare clic su hello **eliminare** pulsante nel riquadro superiore hello.
![Database di Azure per MySQL: eliminare il server](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Confermare il nome server hello desiderato toodelete e visualizzare i database di hello in essa contenute sono interessate. Digitare il nome del server nella casella di testo hello, ad esempio esempio **myserver4demo**, quindi fare clic su **eliminare**.

## <a name="next-steps"></a>Passaggi successivi

> [!div class="nextstepaction"]
> [Progettare il primo database di Azure per il database MySQL](./tutorial-design-database-using-portal.md)

