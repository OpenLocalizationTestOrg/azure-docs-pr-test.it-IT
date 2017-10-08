---
title: aaaSet backup PostgreSQL in una VM Linux | Documenti Microsoft
description: Informazioni su come tooinstall e configurare PostgreSQL in una macchina virtuale di Linux in Azure
services: virtual-machines-linux
documentationcenter: 
author: SuperScottz
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 1a747363-0cc5-4ba3-9be7-084dfeb04651
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: mingzhan
ms.openlocfilehash: 40209647924dffce11500705eb2d9f41c14df6ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a>Installare e configurare PostgreSQL in Azure
PostgreSQL è un database open source avanzate simile tooOracle e DB2. Questo database include funzionalità aziendali quali la conformità ACID completa, l'elaborazione transazionale affidabile e il controllo della concorrenza per più versioni. Supporta anche standard come ANSI SQL e SQL/MED (compresi wrapper di dati esterni per Oracle, MySQL, MongoDB e molti altri). È inoltre altamente estendibile, supportando oltre 12 linguaggi procedurali, gli indici GIN e GIST, i dati spaziali e più funzionalità di tipo NoSQL per le applicazioni basate su chiave-valore o JSON.

In questo articolo si apprenderà come tooinstall e configurare PostgreSQL in una macchina virtuale di Azure che eseguono Linux.

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a>Installare PostgreSQL
> [!NOTE]
> È necessario disporre già una macchina virtuale di Azure che eseguono Linux in ordine toocomplete questa esercitazione. toocreate e impostare una VM Linux prima di procedere, vedere il [esercitazione VM Linux di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
> 
> 

In questo caso, usare la porta 1999 come hello PostgreSQL porta.  

Connettersi toohello VM Linux è stato creato tramite PuTTY. Se si tratta di hello prima volta che si usa una macchina virtuale Linux di Azure, vedere [come tooUse SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn come toouse PuTTY tooconnect tooa VM Linux.

1. Comando che segue di esecuzione hello tooswitch toohello radice (amministratore):
   
        # sudo su -
2. Alcune distribuzioni dispongono di dipendenze che è necessario installare prima di eseguire l'installazione di PostgreSQL. Controllare per la distribuzione nell'elenco ed eseguire i comando appropriato hello:
   
   * Linux basato su Red Hat:
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * Linux basato su Debian:
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * SUSE Linux:
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. Scaricare PostgreSQL nella directory principale di hello e quindi decomprimere il pacchetto di hello:
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    Hello sopra è riportato un esempio. È possibile trovare hello ulteriori download indirizzo hello [indice di /puborigine/](https://ftp.postgresql.org/pub/source/).
4. compilazione di hello toostart, eseguire questi comandi:
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. Se si desidera toobuild tutto ciò che può essere compilato, tra cui documentazione hello (pagine HTML e man) e i moduli aggiuntivi (pensionistici), eseguire comando seguente, invece di hello:
   
        # gmake install-world
   
    Si dovrebbe ricevere hello messaggio di conferma seguente:
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a>Configurare PostgreSQL
1. (Facoltativo) Creare un hello tooshorten collegamento simbolico PostgreSQL riferimento toonot includono il numero di versione di hello:
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. Creare una directory per il database di hello:
   
        # mkdir -p /opt/pgsql_data
3. Creare un utente non ROOT e modificare il relativo profilo. Passare quindi toothis nuovo utente (chiamato *postgres* in questo esempio):
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > Per motivi di sicurezza, PostgreSQL utilizza tooinitialize un utente non root, avviare o arrestare hello database.
   > 
   > 
4. Modifica hello *bash_profile* file immettendo i comandi di hello riportati di seguito. Queste righe verranno aggiunte toohello fine hello *bash_profile* file:
   
        cat >> ~/.bash_profile <<EOF
        export PGPORT=1999
        export PGDATA=/opt/pgsql_data
        export LANG=en_US.utf8
        export PGHOME=/opt/pgsql
        export PATH=\$PATH:\$PGHOME/bin
        export MANPATH=\$MANPATH:\$PGHOME/share/man
        export DATA=`date +"%Y%m%d%H%M"`
        export PGUSER=postgres
        alias rm='rm -i'
        alias ll='ls -lh'
        EOF
5. Eseguire hello *bash_profile* file:
   
        $ source .bash_profile
6. Convalidare l'installazione utilizzando hello comando seguente:
   
        $ which psql
   
    Se l'installazione ha esito positivo, verrà visualizzato hello seguente risposta:
   
        /opt/pgsql/bin/psql
7. È inoltre possibile verificare versione PostgreSQL hello:
   
        $ psql -V
8. Inizializzare hello database:
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    Si dovrebbe ricevere hello seguente output:

![immagine](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a>Impostare PostgreSQL
<!--    [postgres@ test ~]$ exit -->

Eseguire hello seguenti comandi:

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

Modificare le due variabili nel file /etc/init.d/postgresql hello. prefisso di Hello è impostato il percorso di installazione toohello di PostgreSQL: **/OPT/Microsoft pgsql**. PGDATA è impostato toohello percorso di archiviazione di dati di PostgreSQL: **/OPT/Microsoft pgsql_data**.

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![immagine](./media/postgresql-install/no2.png)

Modificare toomake file hello è eseguibile:

    # chmod +x /etc/init.d/postgresql

Avviare PostgreSQL:

    # /etc/init.d/postgresql start

Controllare se endpoint hello di PostgreSQL si trova in:

    # netstat -tunlp|grep 1999

È necessario visualizzare hello seguente output:

![immagine](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a>La connessione a database Postgres toohello
Passare nuovamente toohello postgres utente:

    # su - postgres

Creare un database Postgres:

    $ createdb events

La connessione a database di eventi toohello appena creato:

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a>Come creare ed eliminare una tabella Postgres
Ora che si è connessi toohello database, è possibile creare tabelle in essa contenuti.

Ad esempio, creare una nuova tabella di esempio Postgres utilizzando hello comando seguente:

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

Ora impostati una tabella di quattro colonne con hello seguendo i nomi delle colonne e le restrizioni:

1. Hello colonna "name" è stato limitato dall'hello VARCHAR comando toobe fino a 20 caratteri.
2. colonna "food" Hello indica piatto hello che fornirà ogni persona. VARCHAR limita toobe questo testo in 30 caratteri.
3. Hello "confermata" record di colonna se la persona hello è RSVP'd toohello pranzo. i valori accettabili Hello sono "Y" e "N".
4. Mostra colonna di data"Hello" quando si è effettuata l'iscrizione per l'evento hello. Postgres richiede che le date vengano immesse nel formato aaaa-mm-gg.

Se è stata creata la tabella dovrebbe essere seguito hello:

![immagine](./media/postgresql-install/no4.png)

È inoltre possibile verificare la struttura di tabella hello utilizzando hello comando seguente:

![immagine](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a>Aggiungere dati tooa tabella
Inserire innanzitutto le informazioni in una riga:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

Dovrebbe venire visualizzato questo output:

![immagine](./media/postgresql-install/no6.png)

È possibile aggiungere due ulteriori toohello tabella people anche. Ecco alcuni esempi oppure è possibile inserire i dati desiderati:

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a>Mostrare le tabelle
Utilizzare hello comando tooshow una tabella di seguito:

    select * from potluck;

output di Hello è:

![immagine](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a>Eliminare dati in una tabella
Utilizzare hello comando toodelete dati in una tabella seguenti:

    delete from potluck where name=’John’;

Vengono eliminate tutte le informazioni nella riga "John" hello hello. output di Hello è:

![immagine](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a>Aggiornare dati in una tabella
Utilizzare hello segue comando tooupdate dati in una tabella. In questo caso, Sandy ha confermato che lei partecipazione, in modo verrà modificata la RSVP da "N" troppo "Y":

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a>Per altre informazioni su PostgreSQL
Ora che è stata completata installazione hello di PostgreSQL in una macchina virtuale Linux di Azure, è possibile utilizzare l'uso in Azure. toolearn ulteriori informazioni su PostgreSQL, visitare hello [sito Web PostgreSQL](http://www.postgresql.org/).

