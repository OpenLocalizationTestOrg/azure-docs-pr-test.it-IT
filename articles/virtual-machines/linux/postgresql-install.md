---
title: Impostare PostgreSQL su una macchina virtuale Linux | Microsoft Docs
description: Informazioni su come installare e configurare PostgreSQL in una macchina virtuale Linux in Azure.
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
ms.openlocfilehash: 0bccdc1cfdbda06b57da8cd662373ef137768672
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-configure-postgresql-on-azure"></a><span data-ttu-id="65042-103">Installare e configurare PostgreSQL in Azure</span><span class="sxs-lookup"><span data-stu-id="65042-103">Install and configure PostgreSQL on Azure</span></span>
<span data-ttu-id="65042-104">PostgreSQL è un database open source avanzato simile a Oracle e DB2.</span><span class="sxs-lookup"><span data-stu-id="65042-104">PostgreSQL is an advanced open-source database similar to Oracle and DB2.</span></span> <span data-ttu-id="65042-105">Questo database include funzionalità aziendali quali la conformità ACID completa, l'elaborazione transazionale affidabile e il controllo della concorrenza per più versioni.</span><span class="sxs-lookup"><span data-stu-id="65042-105">It includes enterprise-ready features such as full ACID compliance, reliable transactional processing, and multi-version concurrency control.</span></span> <span data-ttu-id="65042-106">Supporta anche standard come ANSI SQL e SQL/MED (compresi wrapper di dati esterni per Oracle, MySQL, MongoDB e molti altri).</span><span class="sxs-lookup"><span data-stu-id="65042-106">It also supports standards such as ANSI SQL and SQL/MED (including foreign data wrappers for Oracle, MySQL, MongoDB, and many others).</span></span> <span data-ttu-id="65042-107">È inoltre altamente estendibile, supportando oltre 12 linguaggi procedurali, gli indici GIN e GIST, i dati spaziali e più funzionalità di tipo NoSQL per le applicazioni basate su chiave-valore o JSON.</span><span class="sxs-lookup"><span data-stu-id="65042-107">It is highly extensible with support for over 12 procedural languages, GIN and GiST indexes, spatial data support, and multiple NoSQL-like features for JSON or key-value-based applications.</span></span>

<span data-ttu-id="65042-108">Questo articolo illustrerà come installare e configurare PostgreSQL in una macchina virtuale di Azure che esegue Linux.</span><span class="sxs-lookup"><span data-stu-id="65042-108">In this article, you will learn how to install and configure PostgreSQL on an Azure virtual machine running Linux.</span></span>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="install-postgresql"></a><span data-ttu-id="65042-109">Installare PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="65042-109">Install PostgreSQL</span></span>
> [!NOTE]
> <span data-ttu-id="65042-110">Per poter completare questa esercitazione, è necessario disporre già di una macchina virtuale di Microsoft Azure che esegue Linux.</span><span class="sxs-lookup"><span data-stu-id="65042-110">You must already have an Azure virtual machine running Linux in order to complete this tutorial.</span></span> <span data-ttu-id="65042-111">Prima di procedere, vedere l' [esercitazione relativa alle macchine virtuali Linux di Azure](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)per creare e impostare una macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="65042-111">To create and set up a Linux VM before proceeding, see the [Azure Linux VM tutorial](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
> 
> 

<span data-ttu-id="65042-112">In questo caso, usare la porta 1999 come porta di PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="65042-112">In this case, use port 1999 as the PostgreSQL port.</span></span>  

<span data-ttu-id="65042-113">Connettersi tramite PuTTY alla macchina virtuale Linux creata.</span><span class="sxs-lookup"><span data-stu-id="65042-113">Connect to the Linux VM you created via PuTTY.</span></span> <span data-ttu-id="65042-114">Se questa è la prima volta che si sta usando una macchina virtuale Linux di Azure, vedere [usare SSH con Linux in Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) per imparare a usare PuTTY per connettersi a una VM Linux.</span><span class="sxs-lookup"><span data-stu-id="65042-114">If this is the first time you're using an Azure Linux VM, see [How to Use SSH with Linux on Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) to learn how to use PuTTY to connect to a Linux VM.</span></span>

1. <span data-ttu-id="65042-115">Eseguire il comando seguente per passare alla directory radice (admin):</span><span class="sxs-lookup"><span data-stu-id="65042-115">Run the following command to switch to the root (admin):</span></span>
   
        # sudo su -
2. <span data-ttu-id="65042-116">Alcune distribuzioni dispongono di dipendenze che è necessario installare prima di eseguire l'installazione di PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="65042-116">Some distributions have dependencies that you must install before installing PostgreSQL.</span></span> <span data-ttu-id="65042-117">Nell'elenco individuare la distribuzione in uso ed eseguire il comando appropriato:</span><span class="sxs-lookup"><span data-stu-id="65042-117">Check for your distro in this list and run the appropriate command:</span></span>
   
   * <span data-ttu-id="65042-118">Linux basato su Red Hat:</span><span class="sxs-lookup"><span data-stu-id="65042-118">Red Hat base Linux:</span></span>
     
           # yum install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="65042-119">Linux basato su Debian:</span><span class="sxs-lookup"><span data-stu-id="65042-119">Debian base Linux:</span></span>
     
            # apt-get install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam libxslt-devel tcl-devel python-devel -y  
   * <span data-ttu-id="65042-120">SUSE Linux:</span><span class="sxs-lookup"><span data-stu-id="65042-120">SUSE Linux:</span></span>
     
           # zypper install readline-devel gcc make zlib-devel openssl openssl-devel libxml2-devel pam-devel pam  libxslt-devel tcl-devel python-devel -y  
3. <span data-ttu-id="65042-121">Scaricare PostgreSQL nella directory radice e quindi decomprimere il pacchetto:</span><span class="sxs-lookup"><span data-stu-id="65042-121">Download PostgreSQL into the root directory, and then unzip the package:</span></span>
   
        # wget https://ftp.postgresql.org/pub/source/v9.3.5/postgresql-9.3.5.tar.bz2 -P /root/
   
        # tar jxvf  postgresql-9.3.5.tar.bz2
   
    <span data-ttu-id="65042-122">Quello precedente è un esempio.</span><span class="sxs-lookup"><span data-stu-id="65042-122">The above is an example.</span></span> <span data-ttu-id="65042-123">Per l'indirizzo di download più dettagliato, vedere [Indice di /pub/source/](https://ftp.postgresql.org/pub/source/).</span><span class="sxs-lookup"><span data-stu-id="65042-123">You can find the more detailed download address in the [Index of /pub/source/](https://ftp.postgresql.org/pub/source/).</span></span>
4. <span data-ttu-id="65042-124">Per avviare la compilazione, eseguire questi comandi:</span><span class="sxs-lookup"><span data-stu-id="65042-124">To start the build, run these commands:</span></span>
   
        # cd postgresql-9.3.5
   
        # ./configure --prefix=/opt/postgresql-9.3.5
5. <span data-ttu-id="65042-125">Se si intende compilare tutti gli elementi compilabili, inclusi la documentazione (pagine HTML e man) e i moduli aggiuntivi (contrib), eseguire invece il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-125">If  you want to build everything that can be built, including the documentation (HTML and man pages) and additional modules (contrib), run the following command instead:</span></span>
   
        # gmake install-world
   
    <span data-ttu-id="65042-126">Dovrebbe venire visualizzato il messaggio di conferma seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-126">You should receive the following confirmation message:</span></span>
   
        PostgreSQL, contrib, and documentation successfully made. Ready to install.

## <a name="configure-postgresql"></a><span data-ttu-id="65042-127">Configurare PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="65042-127">Configure PostgreSQL</span></span>
1. <span data-ttu-id="65042-128">(Facoltativo) Creare un collegamento simbolico per abbreviare il riferimento a PostgreSQL in modo da non includere il numero di versione:</span><span class="sxs-lookup"><span data-stu-id="65042-128">(Optional) Create a symbolic link to shorten the PostgreSQL reference to not include the version number:</span></span>
   
        # ln -s /opt/pgsql9.3.5 /opt/pgsql
2. <span data-ttu-id="65042-129">Creare una directory per il database:</span><span class="sxs-lookup"><span data-stu-id="65042-129">Create a directory for the database:</span></span>
   
        # mkdir -p /opt/pgsql_data
3. <span data-ttu-id="65042-130">Creare un utente non ROOT e modificare il relativo profilo.</span><span class="sxs-lookup"><span data-stu-id="65042-130">Create a non-root user and modify that user’s profile.</span></span> <span data-ttu-id="65042-131">Passare quindi a tale nuovo utente (denominato *postgres* nell'esempio):</span><span class="sxs-lookup"><span data-stu-id="65042-131">Then, switch to this new user (called *postgres* in our example):</span></span>
   
        # useradd postgres
   
        # chown -R postgres.postgres /opt/pgsql_data
   
        # su - postgres
   
   > [!NOTE]
   > <span data-ttu-id="65042-132">Per motivi di sicurezza, PostgreSQL usa un utente non ROOT per inizializzare, avviare o arrestare il database.</span><span class="sxs-lookup"><span data-stu-id="65042-132">For security reasons, PostgreSQL uses a non-root user to initialize, start, or shut down the database.</span></span>
   > 
   > 
4. <span data-ttu-id="65042-133">Modificare il file *bash_profile* immettendo i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="65042-133">Edit the *bash_profile* file by entering the commands below.</span></span> <span data-ttu-id="65042-134">Queste righe verranno aggiunte alla fine del file *bash_profile*:</span><span class="sxs-lookup"><span data-stu-id="65042-134">These lines will be added to the end of the *bash_profile* file:</span></span>
   
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
5. <span data-ttu-id="65042-135">Eseguire il file *bash_profile*:</span><span class="sxs-lookup"><span data-stu-id="65042-135">Execute the *bash_profile* file:</span></span>
   
        $ source .bash_profile
6. <span data-ttu-id="65042-136">Convalidare l'installazione con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-136">Validate your installation by using the following command:</span></span>
   
        $ which psql
   
    <span data-ttu-id="65042-137">Se l'installazione ha avuto esito positivo, verrà visualizzata la risposta seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-137">If your installation is successful, you will see the following response:</span></span>
   
        /opt/pgsql/bin/psql
7. <span data-ttu-id="65042-138">È anche possibile verificare la versione di PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="65042-138">You can also check the PostgreSQL version:</span></span>
   
        $ psql -V
8. <span data-ttu-id="65042-139">Inizializzare il database:</span><span class="sxs-lookup"><span data-stu-id="65042-139">Initialize the database:</span></span>
   
        $ initdb -D $PGDATA -E UTF8 --locale=C -U postgres -W
   
    <span data-ttu-id="65042-140">Dovrebbero venire visualizzato l'output seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-140">You should receive the following output:</span></span>

![immagine](./media/postgresql-install/no1.png)

## <a name="set-up-postgresql"></a><span data-ttu-id="65042-142">Impostare PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="65042-142">Set up PostgreSQL</span></span>
<!--    [postgres@ test ~]$ exit -->

<span data-ttu-id="65042-143">Eseguire i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="65042-143">Run the following commands:</span></span>

    # cd /root/postgresql-9.3.5/contrib/start-scripts

    # cp linux /etc/init.d/postgresql

<span data-ttu-id="65042-144">Modificare due variabili nel file /etc/init.d/postgresql.</span><span class="sxs-lookup"><span data-stu-id="65042-144">Modify two variables in the /etc/init.d/postgresql file.</span></span> <span data-ttu-id="65042-145">Il prefisso è impostato sul percorso di installazione di PostgreSQL: **/opt/pgsql**.</span><span class="sxs-lookup"><span data-stu-id="65042-145">The prefix is set to the installation path of PostgreSQL: **/opt/pgsql**.</span></span> <span data-ttu-id="65042-146">PGDATA è impostato sul percorso di archiviazione dati di PostgreSQL: **/opt/pgsql_data**.</span><span class="sxs-lookup"><span data-stu-id="65042-146">PGDATA is set to the data storage path of PostgreSQL: **/opt/pgsql_data**.</span></span>

    # sed -i '32s#usr/local#opt#' /etc/init.d/postgresql

    # sed -i '35s#usr/local/pgsql/data#opt/pgsql_data#' /etc/init.d/postgresql

![immagine](./media/postgresql-install/no2.png)

<span data-ttu-id="65042-148">Modificare il file per renderlo eseguibile:</span><span class="sxs-lookup"><span data-stu-id="65042-148">Change the file to make it executable:</span></span>

    # chmod +x /etc/init.d/postgresql

<span data-ttu-id="65042-149">Avviare PostgreSQL:</span><span class="sxs-lookup"><span data-stu-id="65042-149">Start PostgreSQL:</span></span>

    # /etc/init.d/postgresql start

<span data-ttu-id="65042-150">Controllare se l'endpoint di PostgreSQL è attivo:</span><span class="sxs-lookup"><span data-stu-id="65042-150">Check if the endpoint of PostgreSQL is on:</span></span>

    # netstat -tunlp|grep 1999

<span data-ttu-id="65042-151">Dovrebbe venire visualizzato l'output seguente.</span><span class="sxs-lookup"><span data-stu-id="65042-151">You should see the following output:</span></span>

![immagine](./media/postgresql-install/no3.png)

## <a name="connect-to-the-postgres-database"></a><span data-ttu-id="65042-153">Connessione al database Postgres</span><span class="sxs-lookup"><span data-stu-id="65042-153">Connect to the Postgres database</span></span>
<span data-ttu-id="65042-154">Proseguire e passare di nuovo all'utente postgres:</span><span class="sxs-lookup"><span data-stu-id="65042-154">Switch to the postgres user once again:</span></span>

    # su - postgres

<span data-ttu-id="65042-155">Creare un database Postgres:</span><span class="sxs-lookup"><span data-stu-id="65042-155">Create a Postgres database:</span></span>

    $ createdb events

<span data-ttu-id="65042-156">Connettersi al database events appena creato:</span><span class="sxs-lookup"><span data-stu-id="65042-156">Connect to the events database that you just created:</span></span>

    $ psql -d events

## <a name="create-and-delete-a-postgres-table"></a><span data-ttu-id="65042-157">Come creare ed eliminare una tabella Postgres</span><span class="sxs-lookup"><span data-stu-id="65042-157">Create and delete a Postgres table</span></span>
<span data-ttu-id="65042-158">Ora che ci si è connessi al database, è possibile crearvi tabelle.</span><span class="sxs-lookup"><span data-stu-id="65042-158">Now that you have connected to the database, you can create tables in it.</span></span>

<span data-ttu-id="65042-159">Ad esempio, creare una nuova tabella Postgres di esempio con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-159">For example, create a new example Postgres table by using the following command:</span></span>

    CREATE TABLE potluck (name VARCHAR(20),    food VARCHAR(30),    confirmed CHAR(1), signup_date DATE);

<span data-ttu-id="65042-160">È stata così impostata una tabella di quattro colonne con i nomi e le restrizioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="65042-160">You have now set up a four-column table with the following column names and restrictions:</span></span>

1. <span data-ttu-id="65042-161">La colonna "name" è stata limitata dal comando VARCHAR a una lunghezza inferiore a 20 caratteri.</span><span class="sxs-lookup"><span data-stu-id="65042-161">The “name” column has been limited by the VARCHAR command to be under 20 characters long.</span></span>
2. <span data-ttu-id="65042-162">La colonna "food" indica la pietanza che verrà portata da ogni persona.</span><span class="sxs-lookup"><span data-stu-id="65042-162">The “food” column indicates the food item that each person will bring.</span></span> <span data-ttu-id="65042-163">VARCHAR limita questo testo a una lunghezza inferiore a 30 caratteri.</span><span class="sxs-lookup"><span data-stu-id="65042-163">VARCHAR limits this text to be under 30 characters.</span></span>
3. <span data-ttu-id="65042-164">La colonna "confirmed" registra se la persona ha dato conferma della propria partecipazione.</span><span class="sxs-lookup"><span data-stu-id="65042-164">The “confirmed” column records whether the person has RSVP’d to the potluck.</span></span> <span data-ttu-id="65042-165">I valori consentiti sono "Y" e "N".</span><span class="sxs-lookup"><span data-stu-id="65042-165">The acceptable values are "Y" and "N".</span></span>
4. <span data-ttu-id="65042-166">La colonna "date" indicherà quando la persona si è iscritta per l'evento.</span><span class="sxs-lookup"><span data-stu-id="65042-166">The “date” column shows when they signed up for the event.</span></span> <span data-ttu-id="65042-167">Postgres richiede che le date vengano immesse nel formato aaaa-mm-gg.</span><span class="sxs-lookup"><span data-stu-id="65042-167">Postgres requires that dates be written as yyyy-mm-dd.</span></span>

<span data-ttu-id="65042-168">Se la tabella è stata creata correttamente, dovrebbe venire visualizzato quanto segue:</span><span class="sxs-lookup"><span data-stu-id="65042-168">You should see the following if your table has been successfully created:</span></span>

![immagine](./media/postgresql-install/no4.png)

<span data-ttu-id="65042-170">È anche possibile verificare la struttura della tabella con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-170">You can also check the table structure by using the following command:</span></span>

![immagine](./media/postgresql-install/no5.png)

### <a name="add-data-to-a-table"></a><span data-ttu-id="65042-172">Aggiungere dati a una tabella</span><span class="sxs-lookup"><span data-stu-id="65042-172">Add data to a table</span></span>
<span data-ttu-id="65042-173">Inserire innanzitutto le informazioni in una riga:</span><span class="sxs-lookup"><span data-stu-id="65042-173">First, insert information into a row:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('John', 'Casserole', 'Y', '2012-04-11');

<span data-ttu-id="65042-174">Dovrebbe venire visualizzato questo output:</span><span class="sxs-lookup"><span data-stu-id="65042-174">You should see this output:</span></span>

![immagine](./media/postgresql-install/no6.png)

<span data-ttu-id="65042-176">È anche possibile aggiungere altre persone alla tabella.</span><span class="sxs-lookup"><span data-stu-id="65042-176">You can add a couple more people to the table as well.</span></span> <span data-ttu-id="65042-177">Ecco alcuni esempi oppure è possibile inserire i dati desiderati:</span><span class="sxs-lookup"><span data-stu-id="65042-177">Here are some options, or you can create your own:</span></span>

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Sandy', 'Key Lime Tarts', 'N', '2012-04-14');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES ('Tom', 'BBQ','Y', '2012-04-18');

    INSERT INTO potluck (name, food, confirmed, signup_date) VALUES('Tina', 'Salad', 'Y', '2012-04-18');

### <a name="show-tables"></a><span data-ttu-id="65042-178">Mostrare le tabelle</span><span class="sxs-lookup"><span data-stu-id="65042-178">Show tables</span></span>
<span data-ttu-id="65042-179">Per mostrare una tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-179">Use the following command to show a table:</span></span>

    select * from potluck;

<span data-ttu-id="65042-180">L'output è:</span><span class="sxs-lookup"><span data-stu-id="65042-180">The output is:</span></span>

![immagine](./media/postgresql-install/no7.png)

### <a name="delete-data-in-a-table"></a><span data-ttu-id="65042-182">Eliminare dati in una tabella</span><span class="sxs-lookup"><span data-stu-id="65042-182">Delete data in a table</span></span>
<span data-ttu-id="65042-183">Per eliminare dati in una tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-183">Use the following command to delete data in a table:</span></span>

    delete from potluck where name=’John’;

<span data-ttu-id="65042-184">Consente di eliminare tutte le informazioni nella riga "John".</span><span class="sxs-lookup"><span data-stu-id="65042-184">This deletes all the information in the "John" row.</span></span> <span data-ttu-id="65042-185">L'output è:</span><span class="sxs-lookup"><span data-stu-id="65042-185">The output is:</span></span>

![immagine](./media/postgresql-install/no8.png)

### <a name="update-data-in-a-table"></a><span data-ttu-id="65042-187">Aggiornare dati in una tabella</span><span class="sxs-lookup"><span data-stu-id="65042-187">Update data in a table</span></span>
<span data-ttu-id="65042-188">Per aggiornare dati in una tabella, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="65042-188">Use the following command to update data in a table.</span></span> <span data-ttu-id="65042-189">In questo caso, Sandy ha confermato la sua partecipazione, pertanto lo stato di conferma verrà modificato da "N" a "Y":</span><span class="sxs-lookup"><span data-stu-id="65042-189">For this one, Sandy has confirmed that she is attending, so we will change her RSVP from "N" to "Y":</span></span>

     UPDATE potluck set confirmed = 'Y' WHERE name = 'Sandy';


## <a name="get-more-information-about-postgresql"></a><span data-ttu-id="65042-190">Per altre informazioni su PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="65042-190">Get more information about PostgreSQL</span></span>
<span data-ttu-id="65042-191">Ora che è stata completata l'installazione di PostgreSQL in una macchina virtuale Linux di Azure, è possibile utilizzarlo in Azure.</span><span class="sxs-lookup"><span data-stu-id="65042-191">Now that you have completed the installation of PostgreSQL in an Azure Linux VM, you can enjoy using it in Azure.</span></span> <span data-ttu-id="65042-192">Per ulteriori informazioni su PostgreSQL, visitare il [sito Web PostgreSQL](http://www.postgresql.org/).</span><span class="sxs-lookup"><span data-stu-id="65042-192">To learn more about PostgreSQL, visit the [PostgreSQL website](http://www.postgresql.org/).</span></span>

