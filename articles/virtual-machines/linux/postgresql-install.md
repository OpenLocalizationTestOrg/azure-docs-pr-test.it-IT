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
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="6c741-103">Installare e configurare PostgreSQL in Azure</span><span class="sxs-lookup"><span data-stu-id="6c741-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="6c741-104">PostgreSQL è un database open source avanzate simile tooOracle e DB2.</span><span class="sxs-lookup"><span data-stu-id="6c741-104">PostgreSQL is an advanced open-source database similar tooOracle and DB2.</span></span> <span data-ttu-id="6c741-105">Questo database include funzionalità aziendali quali la conformità ACID completa, l'elaborazione transazionale affidabile e il controllo della concorrenza per più versioni.</span><span class="sxs-lookup"><span data-stu-id="6c741-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="6c741-106">Supporta anche standard come ANSI SQL e SQL/MED (compresi wrapper di dati esterni per Oracle, MySQL, MongoDB e molti altri).</span><span class="sxs-lookup"><span data-stu-id="6c741-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="6c741-107">È inoltre altamente estendibile, supportando oltre 12 linguaggi procedurali, gli indici GIN e GIST, i dati spaziali e più funzionalità di tipo NoSQL per le applicazioni basate su chiave-valore o JSON.</span><span class="sxs-lookup"><span data-stu-id="6c741-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="6c741-108">In questo articolo si apprenderà come tooinstall e configurare PostgreSQL in una macchina virtuale di Azure che eseguono Linux.</span><span class="sxs-lookup"><span data-stu-id="6c741-108">In this article, you will learn how tooinstall and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="6c741-109">Installare PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6c741-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="6c741-110">È necessario disporre già una macchina virtuale di Azure che eseguono Linux in ordine toocomplete questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6c741-110">You must already have an Azure virtual machine running Linux in order toocomplete this tutorial.</span></span> <span data-ttu-id="6c741-111">toocreate e impostare una VM Linux prima di procedere, vedere il [esercitazione VM Linux di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="6c741-111">toocreate and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="6c741-112">In questo caso, usare la porta 1999 come hello PostgreSQL porta.</span><span class="sxs-lookup"><span data-stu-id="6c741-112">In this case, use port 1999 as hello PostgreSQL port.</span></span>  

<span data-ttu-id="6c741-113">Connettersi toohello VM Linux è stato creato tramite PuTTY.</span><span class="sxs-lookup"><span data-stu-id="6c741-113">Connect toohello Linux VM you created via PuTTY.</span></span> <span data-ttu-id="6c741-114">Se si tratta di hello prima volta che si usa una macchina virtuale Linux di Azure, vedere [come tooUse SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn come toouse PuTTY tooconnect tooa VM Linux.</span><span class="sxs-lookup"><span data-stu-id="6c741-114">If this is hello first time you're using an Azure Linux VM, see [How tooUse SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) toolearn how toouse PuTTY tooconnect tooa Linux VM.</span></span>

1. <span data-ttu-id="6c741-115">Comando che segue di esecuzione hello tooswitch toohello radice (amministratore):</span><span class="sxs-lookup"><span data-stu-id="6c741-115">Run hello following command tooswitch toohello root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="6c741-116">Alcune distribuzioni dispongono di dipendenze che è necessario installare prima di eseguire l'installazione di PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="6c741-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="6c741-117">Controllare per la distribuzione nell'elenco ed eseguire i comando appropriato hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-117">Check for your distro in this list and run hello appropriate command:</span></span>
   
   * <span data-ttu-id="6c741-118">Linux basato su Red Hat:</span><span class="sxs-lookup"><span data-stu-id="6c741-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="6c741-119">Linux basato su Debian:</span><span class="sxs-lookup"><span data-stu-id="6c741-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="6c741-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="6c741-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="6c741-121">Scaricare PostgreSQL nella directory principale di hello e quindi decomprimere il pacchetto di hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-121">Download PostgreSQL into hello root directory, and then unzip hello package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="6c741-122">Hello sopra è riportato un esempio.</span><span class="sxs-lookup"><span data-stu-id="6c741-122">hello above is an example.</span></span> <span data-ttu-id="6c741-123">È possibile trovare hello ulteriori download indirizzo hello [indice di /puborigine/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="6c741-123">You can find hello more detailed download address in hello [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="6c741-124">compilazione di hello toostart, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="6c741-124">toostart hello build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="6c741-125">Se si desidera toobuild tutto ciò che può essere compilato, tra cui documentazione hello (pagine HTML e man) e i moduli aggiuntivi (pensionistici), eseguire comando seguente, invece di hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-125">If  you want toobuild everything that can be built, including hello documentation (HTML and man pages) and additional modules (contrib), run hello following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="6c741-126">Si dovrebbe ricevere hello messaggio di conferma seguente:</span><span class="sxs-lookup"><span data-stu-id="6c741-126">You should receive hello following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready tooinstall.

## <a name="configure-postgresql"></a><span data-ttu-id="6c741-127">Configurare PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6c741-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="6c741-128">(Facoltativo) Creare un hello tooshorten collegamento simbolico PostgreSQL riferimento toonot includono il numero di versione di hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-128">(Optional) Create a symbolic link tooshorten hello PostgreSQL reference toonot include hello version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="6c741-129">Creare una directory per il database di hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-129">Create a directory for hello database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="6c741-130">Creare un utente non ROOT e modificare il relativo profilo.</span><span class="sxs-lookup"><span data-stu-id="6c741-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="6c741-131">Passare quindi toothis nuovo utente (chiamato *postgres* in questo esempio):</span><span class="sxs-lookup"><span data-stu-id="6c741-131">Then, switch toothis new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="6c741-132">Per motivi di sicurezza, PostgreSQL utilizza tooinitialize un utente non root, avviare o arrestare hello database.</span><span class="sxs-lookup"><span data-stu-id="6c741-132">For security reasons, PostgreSQL uses a non-root user tooinitialize, start, or shut down hello database.</span></span>
   > 
   > 
4. <span data-ttu-id="6c741-133">Modifica hello *bash_profile* file immettendo i comandi di hello riportati di seguito.</span><span class="sxs-lookup"><span data-stu-id="6c741-133">Edit hello *bash_profile* file by entering hello commands below.</span></span> <span data-ttu-id="6c741-134">Queste righe verranno aggiunte toohello fine hello *bash_profile* file:</span><span class="sxs-lookup"><span data-stu-id="6c741-134">These lines will be added toohello end of hello *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="6c741-135">Eseguire hello *bash_profile* file:</span><span class="sxs-lookup"><span data-stu-id="6c741-135">Execute hello *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="6c741-136">Convalidare l'installazione utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c741-136">Validate your installation by using hello following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="6c741-137">Se l'installazione ha esito positivo, verrà visualizzato hello seguente risposta:</span><span class="sxs-lookup"><span data-stu-id="6c741-137">If your installation is successful, you will see hello following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="6c741-138">È inoltre possibile verificare versione PostgreSQL hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-138">You can also check hello PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="6c741-139">Inizializzare hello database:</span><span class="sxs-lookup"><span data-stu-id="6c741-139">Initialize hello database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="6c741-140">Si dovrebbe ricevere hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="6c741-140">You should receive hello following output:</span></span>

![immagine](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="6c741-142">Impostare PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6c741-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="6c741-143">Eseguire hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="6c741-143">Run hello following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="6c741-144">Modificare le due variabili nel file /etc/init.d/postgresql hello.</span><span class="sxs-lookup"><span data-stu-id="6c741-144">Modify two variables in hello /etc/init.d/postgresql file.</span></span> <span data-ttu-id="6c741-145">prefisso di Hello è impostato il percorso di installazione toohello di PostgreSQL: **/OPT/Microsoft pgsql**.</span><span class="sxs-lookup"><span data-stu-id="6c741-145">hello prefix is set toohello installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="6c741-146">PGDATA è impostato toohello percorso di archiviazione di dati di PostgreSQL: **/OPT/Microsoft pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="6c741-146">PGDATA is set toohello data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![immagine](./media/postgresql-install/no2.png)

<span data-ttu-id="6c741-148">Modificare toomake file hello è eseguibile:</span><span class="sxs-lookup"><span data-stu-id="6c741-148">Change hello file toomake it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="6c741-149">Avviare PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="6c741-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="6c741-150">Controllare se endpoint hello di PostgreSQL si trova in:</span><span class="sxs-lookup"><span data-stu-id="6c741-150">Check if hello endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="6c741-151">È necessario visualizzare hello seguente output:</span><span class="sxs-lookup"><span data-stu-id="6c741-151">You should see hello following output:</span></span>

![immagine](./media/postgresql-install/no3.png)

## <a name="connect-toohello-postgres-database"></a><span data-ttu-id="6c741-153">La connessione a database Postgres toohello</span><span class="sxs-lookup"><span data-stu-id="6c741-153">Connect toohello Postgres database</span></span>
<span data-ttu-id="6c741-154">Passare nuovamente toohello postgres utente:</span><span class="sxs-lookup"><span data-stu-id="6c741-154">Switch toohello postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="6c741-155">Creare un database Postgres:</span><span class="sxs-lookup"><span data-stu-id="6c741-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="6c741-156">La connessione a database di eventi toohello appena creato:</span><span class="sxs-lookup"><span data-stu-id="6c741-156">Connect toohello events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="6c741-157">Come creare ed eliminare una tabella Postgres</span><span class="sxs-lookup"><span data-stu-id="6c741-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="6c741-158">Ora che si è connessi toohello database, è possibile creare tabelle in essa contenuti.</span><span class="sxs-lookup"><span data-stu-id="6c741-158">Now that you have connected toohello database, you can create tables in it.</span></span>

<span data-ttu-id="6c741-159">Ad esempio, creare una nuova tabella di esempio Postgres utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c741-159">For example, create a new example Postgres table by using hello following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="6c741-160">Ora impostati una tabella di quattro colonne con hello seguendo i nomi delle colonne e le restrizioni:</span><span class="sxs-lookup"><span data-stu-id="6c741-160">You have now set up a four-column table with hello following column names and restrictions:</span></span>

1. <span data-ttu-id="6c741-161">Hello colonna "name" è stato limitato dall'hello VARCHAR comando toobe fino a 20 caratteri.</span><span class="sxs-lookup"><span data-stu-id="6c741-161">hello “name” column has been limited by hello VARCHAR command toobe under 20 characters long.</span></span>
2. <span data-ttu-id="6c741-162">colonna "food" Hello indica piatto hello che fornirà ogni persona.</span><span class="sxs-lookup"><span data-stu-id="6c741-162">hello “food” column indicates hello food item that each person will bring.</span></span> <span data-ttu-id="6c741-163">VARCHAR limita toobe questo testo in 30 caratteri.</span><span class="sxs-lookup"><span data-stu-id="6c741-163">VARCHAR limits this text toobe under 30 characters.</span></span>
3. <span data-ttu-id="6c741-164">Hello "confermata" record di colonna se la persona hello è RSVP'd toohello pranzo.</span><span class="sxs-lookup"><span data-stu-id="6c741-164">hello “confirmed” column records whether hello person has RSVP’d toohello potluck.</span></span> <span data-ttu-id="6c741-165">i valori accettabili Hello sono "Y" e "N".</span><span class="sxs-lookup"><span data-stu-id="6c741-165">hello acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="6c741-166">Mostra colonna di data"Hello" quando si è effettuata l'iscrizione per l'evento hello.</span><span class="sxs-lookup"><span data-stu-id="6c741-166">hello “date” column shows when they signed up for hello event.</span></span> <span data-ttu-id="6c741-167">Postgres richiede che le date vengano immesse nel formato aaaa-mm-gg.</span><span class="sxs-lookup"><span data-stu-id="6c741-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="6c741-168">Se è stata creata la tabella dovrebbe essere seguito hello:</span><span class="sxs-lookup"><span data-stu-id="6c741-168">You should see hello following if your table has been successfully created:</span></span>

![immagine](./media/postgresql-install/no4.png)

<span data-ttu-id="6c741-170">È inoltre possibile verificare la struttura di tabella hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6c741-170">You can also check hello table structure by using hello following command:</span></span>

![immagine](./media/postgresql-install/no5.png)

### <a name="add-data-tooa-table"></a><span data-ttu-id="6c741-172">Aggiungere dati tooa tabella</span><span class="sxs-lookup"><span data-stu-id="6c741-172">Add data tooa table</span></span>
<span data-ttu-id="6c741-173">Inserire innanzitutto le informazioni in una riga:</span><span class="sxs-lookup"><span data-stu-id="6c741-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="6c741-174">Dovrebbe venire visualizzato questo output:</span><span class="sxs-lookup"><span data-stu-id="6c741-174">You should see this output:</span></span>

![immagine](./media/postgresql-install/no6.png)

<span data-ttu-id="6c741-176">È possibile aggiungere due ulteriori toohello tabella people anche.</span><span class="sxs-lookup"><span data-stu-id="6c741-176">You can add a couple more people toohello table as well.</span></span> <span data-ttu-id="6c741-177">Ecco alcuni esempi oppure è possibile inserire i dati desiderati:</span><span class="sxs-lookup"><span data-stu-id="6c741-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="6c741-178">Mostrare le tabelle</span><span class="sxs-lookup"><span data-stu-id="6c741-178">Show tables</span></span>
<span data-ttu-id="6c741-179">Utilizzare hello comando tooshow una tabella di seguito:</span><span class="sxs-lookup"><span data-stu-id="6c741-179">Use hello following command tooshow a table:</span></span>

    select * from potluck;

<span data-ttu-id="6c741-180">output di Hello è:</span><span class="sxs-lookup"><span data-stu-id="6c741-180">hello output is:</span></span>

![immagine](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="6c741-182">Eliminare dati in una tabella</span><span class="sxs-lookup"><span data-stu-id="6c741-182">Delete data in a table</span></span>
<span data-ttu-id="6c741-183">Utilizzare hello comando toodelete dati in una tabella seguenti:</span><span class="sxs-lookup"><span data-stu-id="6c741-183">Use hello following command toodelete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="6c741-184">Vengono eliminate tutte le informazioni nella riga "John" hello hello.</span><span class="sxs-lookup"><span data-stu-id="6c741-184">This deletes all hello information in hello "John" row.</span></span> <span data-ttu-id="6c741-185">output di Hello è:</span><span class="sxs-lookup"><span data-stu-id="6c741-185">hello output is:</span></span>

![immagine](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="6c741-187">Aggiornare dati in una tabella</span><span class="sxs-lookup"><span data-stu-id="6c741-187">Update data in a table</span></span>
<span data-ttu-id="6c741-188">Utilizzare hello segue comando tooupdate dati in una tabella.</span><span class="sxs-lookup"><span data-stu-id="6c741-188">Use hello following command tooupdate data in a table.</span></span> <span data-ttu-id="6c741-189">In questo caso, Sandy ha confermato che lei partecipazione, in modo verrà modificata la RSVP da "N" troppo "Y":</span><span class="sxs-lookup"><span data-stu-id="6c741-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" too"Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="6c741-190">Per altre informazioni su PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6c741-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="6c741-191">Ora che è stata completata installazione hello di PostgreSQL in una macchina virtuale Linux di Azure, è possibile utilizzare l'uso in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c741-191">Now that you have completed hello installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="6c741-192">toolearn ulteriori informazioni su PostgreSQL, visitare hello [sito Web PostgreSQL](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="6c741-192">toolearn more about PostgreSQL, visit hello [PostgreSQL website](http://www.postgresql.org/).</span></span>

