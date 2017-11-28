---
title: aaaDesign di Azure prima di Database per database MySQL - portale di Azure | Documenti Microsoft
description: In questa esercitazione viene illustrato come toocreate e gestire i Database di Azure per il server MySQL e di database tramite il portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 06/06/2017
ms.custom: mvc
ms.openlocfilehash: 06dd952acc5356b8cccaf36917df1ff8db4f7139
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="d7394-103">Progettare il primo database di Azure per il database MySQL</span><span class="sxs-lookup"><span data-stu-id="d7394-103">Design your first Azure Database for MySQL database</span></span>
<span data-ttu-id="d7394-104">Il Database di Azure per MySQL è un servizio gestito che consente di toorun, gestire e scalare il database MySQL a disponibilità elevata nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-104">Azure Database for MySQL is a managed service that enables you toorun, manage, and scale highly available MySQL databases in hello cloud.</span></span> <span data-ttu-id="d7394-105">Utilizza hello portale di Azure, è possibile facilmente gestire il server e progettare un database.</span><span class="sxs-lookup"><span data-stu-id="d7394-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="d7394-106">In questa esercitazione, utilizzare la modalità hello toolearn portale Azure per:</span><span class="sxs-lookup"><span data-stu-id="d7394-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7394-107">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="d7394-107">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="d7394-108">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="d7394-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="d7394-109">Utilizzare lo strumento da riga di comando di mysql toocreate un database</span><span class="sxs-lookup"><span data-stu-id="d7394-109">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="d7394-110">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="d7394-110">Load sample data</span></span>
> * <span data-ttu-id="d7394-111">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="d7394-111">Query data</span></span>
> * <span data-ttu-id="d7394-112">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="d7394-112">Update data</span></span>
> * <span data-ttu-id="d7394-113">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="d7394-113">Restore data</span></span>

## <a name="sign-in-toohello-azure-portal"></a><span data-ttu-id="d7394-114">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d7394-114">Sign in toohello Azure portal</span></span>
<span data-ttu-id="d7394-115">Aprire il browser web preferite e visitare hello [portale Microsoft Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="d7394-115">Open your favorite web browser, and visit hello [Microsoft Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="d7394-116">Immettere le credenziali toosign nel portale toohello.</span><span class="sxs-lookup"><span data-stu-id="d7394-116">Enter your credentials toosign in toohello portal.</span></span> <span data-ttu-id="d7394-117">visualizzazione predefinita Hello è il dashboard del servizio.</span><span class="sxs-lookup"><span data-stu-id="d7394-117">hello default view is your service dashboard.</span></span>

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="d7394-118">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="d7394-118">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="d7394-119">Verrà creato un database di Azure per MySQL con un set definito di [risorse di calcolo e di archiviazione](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="d7394-119">An Azure Database for MySQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="d7394-120">Hello server viene creato all'interno di un [gruppo di risorse](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span><span class="sxs-lookup"><span data-stu-id="d7394-120">hello server is created within an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

1. <span data-ttu-id="d7394-121">Passare troppo**database** > **Database di Azure per MySQL**.</span><span class="sxs-lookup"><span data-stu-id="d7394-121">Navigate too**Databases** > **Azure Database for MySQL**.</span></span> <span data-ttu-id="d7394-122">Se non si trova il MySQL Server con **database** categoria, fare clic su **tutti** tooshow tutti disponibili servizi di database.</span><span class="sxs-lookup"><span data-stu-id="d7394-122">If you cannot find MySQL Server under **Databases** category, click **See all** tooshow all available database services.</span></span> <span data-ttu-id="d7394-123">È anche possibile digitare **Database di Azure per MySQL** nel tooquickly casella di ricerca hello individuare hello servizio.</span><span class="sxs-lookup"><span data-stu-id="d7394-123">You can also type **Azure Database for MySQL** in hello search box tooquickly find hello service.</span></span>
<span data-ttu-id="d7394-124">![2-1 Naviga tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span><span class="sxs-lookup"><span data-stu-id="d7394-124">![2-1 Navigate tooMySQL](./media/tutorial-design-database-using-portal/2_1-Navigate-to-MySQL.png)</span></span>

2. <span data-ttu-id="d7394-125">Fare clic sul riquadro **Database di Azure per MySQL** e quindi fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d7394-125">Click **Azure Database for MySQL** tile, and then click **Create**.</span></span>

<span data-ttu-id="d7394-126">In questo esempio, compilare hello Azure Database MySQL form con hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="d7394-126">In our example, fill out hello Azure Database for MySQL form with hello following information:</span></span>

| <span data-ttu-id="d7394-127">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="d7394-127">**Setting**</span></span> | <span data-ttu-id="d7394-128">**Valore consigliato**</span><span class="sxs-lookup"><span data-stu-id="d7394-128">**Suggested value**</span></span> | <span data-ttu-id="d7394-129">**Descrizione campo**</span><span class="sxs-lookup"><span data-stu-id="d7394-129">**Field Description**</span></span> |
|---|---|---|
| <span data-ttu-id="d7394-130">*Server name* (Nome server)</span><span class="sxs-lookup"><span data-stu-id="d7394-130">*Server name*</span></span> | <span data-ttu-id="d7394-131">myserver4demo</span><span class="sxs-lookup"><span data-stu-id="d7394-131">myserver4demo</span></span>  | <span data-ttu-id="d7394-132">Nome del server ha toobe univoco globale.</span><span class="sxs-lookup"><span data-stu-id="d7394-132">Server name has toobe globally unique.</span></span> |
| <span data-ttu-id="d7394-133">*Sottoscrizione*</span><span class="sxs-lookup"><span data-stu-id="d7394-133">*Subscription*</span></span> | <span data-ttu-id="d7394-134">mysubscription</span><span class="sxs-lookup"><span data-stu-id="d7394-134">mysubscription</span></span> | <span data-ttu-id="d7394-135">Selezionare la sottoscrizione dall'elenco a discesa hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-135">Select your subscription from hello drop-down.</span></span> |
| <span data-ttu-id="d7394-136">*Gruppo di risorse*</span><span class="sxs-lookup"><span data-stu-id="d7394-136">*Resource group*</span></span> | <span data-ttu-id="d7394-137">myresourcegroup</span><span class="sxs-lookup"><span data-stu-id="d7394-137">myresourcegroup</span></span> | <span data-ttu-id="d7394-138">Creare un gruppo di risorse o usarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="d7394-138">Create a resource group or use an existing one.</span></span> |
| <span data-ttu-id="d7394-139">*Nome di accesso amministratore server*</span><span class="sxs-lookup"><span data-stu-id="d7394-139">*Server admin login*</span></span> | <span data-ttu-id="d7394-140">myadmin</span><span class="sxs-lookup"><span data-stu-id="d7394-140">myadmin</span></span> | <span data-ttu-id="d7394-141">Configurare il nome dell'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="d7394-141">Setup admin account name.</span></span> |
| <span data-ttu-id="d7394-142">*Password*</span><span class="sxs-lookup"><span data-stu-id="d7394-142">*Password*</span></span> |  | <span data-ttu-id="d7394-143">Impostare una password complessa per l'account amministratore.</span><span class="sxs-lookup"><span data-stu-id="d7394-143">Set a strong admin account password.</span></span> |
| <span data-ttu-id="d7394-144">*Conferma password*</span><span class="sxs-lookup"><span data-stu-id="d7394-144">*Confirm password*</span></span> |  | <span data-ttu-id="d7394-145">Conferma password dell'account admin hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-145">Confirm hello admin account password.</span></span> |
| <span data-ttu-id="d7394-146">*Posizione*</span><span class="sxs-lookup"><span data-stu-id="d7394-146">*Location*</span></span> |  | <span data-ttu-id="d7394-147">Selezionare un'area disponibile.</span><span class="sxs-lookup"><span data-stu-id="d7394-147">Select an available region.</span></span> |
| <span data-ttu-id="d7394-148">*Versione*</span><span class="sxs-lookup"><span data-stu-id="d7394-148">*Version*</span></span> | <span data-ttu-id="d7394-149">5.7</span><span class="sxs-lookup"><span data-stu-id="d7394-149">5.7</span></span> | <span data-ttu-id="d7394-150">Scegliere la versione più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-150">Choose hello latest version.</span></span> |
| <span data-ttu-id="d7394-151">*Configura prestazioni*</span><span class="sxs-lookup"><span data-stu-id="d7394-151">*Configure performance*</span></span> | <span data-ttu-id="d7394-152">Base con 50 unità di calcolo, 50 GB</span><span class="sxs-lookup"><span data-stu-id="d7394-152">Basic, 50 compute units, 50 GB</span></span>  | <span data-ttu-id="d7394-153">Scegliere **Piano tariffario**, **Unità di calcolo**, **Archiviazione (GB)** e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="d7394-153">Choose **Pricing tier**, **Compute Units**, **Storage (GB)**, and then click **OK**.</span></span> |
| <span data-ttu-id="d7394-154">*PIN tooDashboard*</span><span class="sxs-lookup"><span data-stu-id="d7394-154">*Pin tooDashboard*</span></span> | <span data-ttu-id="d7394-155">Controllo</span><span class="sxs-lookup"><span data-stu-id="d7394-155">Check</span></span> | <span data-ttu-id="d7394-156">Consigliato toocheck questa casella, pertanto è possibile che il server di hello facilmente in un secondo momento</span><span class="sxs-lookup"><span data-stu-id="d7394-156">Recommended toocheck this box so you may find hello server easily later on</span></span> |
<span data-ttu-id="d7394-157">Fare quindi clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="d7394-157">Then, click **Create**.</span></span> <span data-ttu-id="d7394-158">In uno o due minuti, un nuovo Database di Azure per il server MySQL è in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-158">In a minute or two, a new Azure Database for MySQL server is running in hello cloud.</span></span> <span data-ttu-id="d7394-159">È possibile fare clic su **notifiche** pulsante nel processo di distribuzione hello toomonitor hello barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="d7394-159">You can click **Notifications** button on hello toolbar toomonitor hello deployment process.</span></span>

## <a name="configure-firewall"></a><span data-ttu-id="d7394-160">Configurare il firewall</span><span class="sxs-lookup"><span data-stu-id="d7394-160">Configure firewall</span></span>
<span data-ttu-id="d7394-161">I database di Azure per MySQL sono protetti da un firewall.</span><span class="sxs-lookup"><span data-stu-id="d7394-161">Azure Databases for MySQL are protected by a firewall.</span></span> <span data-ttu-id="d7394-162">Per impostazione predefinita, tutte le connessioni toohello database e server hello all'interno di server hello vengono rifiutati.</span><span class="sxs-lookup"><span data-stu-id="d7394-162">By default, all connections toohello server and hello databases inside hello server are rejected.</span></span> <span data-ttu-id="d7394-163">Prima connessione tooAzure Database MySQL per hello prima volta, configurare l'indirizzo IP di rete pubblica hello firewall tooadd hello del computer client (o intervallo di indirizzi IP).</span><span class="sxs-lookup"><span data-stu-id="d7394-163">Before connecting tooAzure Database for MySQL for hello first time, configure hello firewall tooadd hello client machine's public network IP address (or IP address range).</span></span>

1. <span data-ttu-id="d7394-164">Fare clic sul server appena creato e quindi fare clic su **Sicurezza connessione**.</span><span class="sxs-lookup"><span data-stu-id="d7394-164">Click your newly created server, and then click **Connection security**.</span></span>
   <span data-ttu-id="d7394-165">![3-1 Sicurezza della connessione](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span><span class="sxs-lookup"><span data-stu-id="d7394-165">![3-1 Connection security](./media/tutorial-design-database-using-portal/3_1-Connection-security.png)</span></span>
2. <span data-ttu-id="d7394-166">È possibile scegliere **Aggiungi indirizzo IP corrente** o configurare le regole del firewall qui.</span><span class="sxs-lookup"><span data-stu-id="d7394-166">You can **Add My IP**, or configure firewall rules here.</span></span> <span data-ttu-id="d7394-167">Ricordare tooclick **salvare** dopo aver creato le regole di hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-167">Remember tooclick **Save** after you have created hello rules.</span></span>
<span data-ttu-id="d7394-168">È ora possibile connettersi a server toohello strumento della riga di comando di mysql o MySQL Workbench GUI.</span><span class="sxs-lookup"><span data-stu-id="d7394-168">You can now connect toohello server using mysql command-line tool or MySQL Workbench GUI tool.</span></span>

> [!TIP]
> <span data-ttu-id="d7394-169">Il Database di Azure per il server MySQL comunica sulla porta 3306.</span><span class="sxs-lookup"><span data-stu-id="d7394-169">Azure Database for MySQL server communicates over port 3306.</span></span> <span data-ttu-id="d7394-170">Se si sta tentando di tooconnect da una rete aziendale, il traffico in uscita sulla porta 3306 può non essere consentito dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="d7394-170">If you are trying tooconnect from within a corporate network, outbound traffic over port 3306 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="d7394-171">In questo caso, è possibile connettersi tooAzure MySQL server, a meno che il reparto IT apre la porta 3306.</span><span class="sxs-lookup"><span data-stu-id="d7394-171">If so, you cannot connect tooAzure MySQL server unless your IT department opens port 3306.</span></span>

## <a name="get-connection-information"></a><span data-ttu-id="d7394-172">Ottenere informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="d7394-172">Get connection information</span></span>
<span data-ttu-id="d7394-173">Get hello completo **nome Server** e **nome account di accesso di amministratore Server** per il Database di Azure per il server MySQL da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7394-173">Get hello fully qualified **Server name** and **Server admin login name** for your Azure Database for MySQL server from hello Azure portal.</span></span> <span data-ttu-id="d7394-174">Utilizzare hello server completo tooconnect tooyour server dei nomi utilizzando lo strumento da riga di comando di mysql.</span><span class="sxs-lookup"><span data-stu-id="d7394-174">You use hello fully qualified server name tooconnect tooyour server using mysql command-line tool.</span></span> 

1. <span data-ttu-id="d7394-175">In [portale di Azure](https://portal.azure.com/), fare clic su **tutte le risorse** dal menu a sinistra di hello, nome del tipo hello e ricerca per il Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="d7394-175">In [Azure portal](https://portal.azure.com/), click **All resources** from hello left-hand menu, type hello name, and search for your Azure Database for MySQL server.</span></span> <span data-ttu-id="d7394-176">Selezionare i dettagli di hello tooview nome server hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-176">Select hello server name tooview hello details.</span></span>

2. <span data-ttu-id="d7394-177">In impostazioni hello fare clic su **proprietà**.</span><span class="sxs-lookup"><span data-stu-id="d7394-177">Under hello Settings heading, click **Properties**.</span></span> <span data-ttu-id="d7394-178">Prendere nota del **NOME SERVER** e del **NOME DI ACCESSO DELL'AMMINISTRATORE SERVER**.</span><span class="sxs-lookup"><span data-stu-id="d7394-178">Note down **SERVER NAME** and **SERVER ADMIN LOGIN NAME**.</span></span> <span data-ttu-id="d7394-179">È possibile fare clic su hello copia pulsante Avanti tooeach campo toocopy toohello negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="d7394-179">You may click hello copy button next tooeach field toocopy toohello clipboard.</span></span>
   <span data-ttu-id="d7394-180">![4-2 Proprietà del server](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span><span class="sxs-lookup"><span data-stu-id="d7394-180">![4-2 server properties](./media/tutorial-design-database-using-portal/4_2-server-properties.png)</span></span>

<span data-ttu-id="d7394-181">In questo esempio, è il nome di server hello *myserver4demo.mysql.database.azure.com*, e l'account di accesso amministratore server hello è  *myadmin@myserver4demo* .</span><span class="sxs-lookup"><span data-stu-id="d7394-181">In this example, hello server name is *myserver4demo.mysql.database.azure.com*, and hello server admin login is *myadmin@myserver4demo*.</span></span>

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="d7394-182">Connessione server toohello con mysql</span><span class="sxs-lookup"><span data-stu-id="d7394-182">Connect toohello server using mysql</span></span>
<span data-ttu-id="d7394-183">Utilizzare [lo strumento da riga di comando di mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish tooyour una connessione Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="d7394-183">Use [mysql command-line tool](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="d7394-184">È possibile eseguire lo strumento da riga di comando di mysql hello da hello Azure Cloud Shell nel browser hello o dal computer utilizzando gli strumenti di mysql installati localmente.</span><span class="sxs-lookup"><span data-stu-id="d7394-184">You can run hello mysql command-line tool from hello Azure Cloud Shell in hello browser or from your own machine using mysql tools installed locally.</span></span> <span data-ttu-id="d7394-185">hello toolaunch Shell di Cloud di Azure, fare clic su hello `Try It` pulsante in un blocco di codice in questo articolo, o visitare il portale di Azure hello e fare clic su hello `>_` icona in hello superiore destro della barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="d7394-185">toolaunch hello Azure Cloud Shell, click hello `Try It` button on a code block in this article, or visit hello Azure portal and click hello `>_` icon in hello top right toolbar.</span></span> 

<span data-ttu-id="d7394-186">Digitare tooconnect comando hello:</span><span class="sxs-lookup"><span data-stu-id="d7394-186">Type hello command tooconnect:</span></span>
```azurecli-interactive
mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="d7394-187">Creazione di un database vuoto</span><span class="sxs-lookup"><span data-stu-id="d7394-187">Create a blank database</span></span>
<span data-ttu-id="d7394-188">Dopo aver connesso toohello server, creare un database vuoto di toowork con.</span><span class="sxs-lookup"><span data-stu-id="d7394-188">Once you’re connected toohello server, create a blank database toowork with.</span></span>
```sql
CREATE DATABASE mysampledb;
```

<span data-ttu-id="d7394-189">Al prompt dei comandi hello, eseguire hello database toothis appena creati connessione tooswitch di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7394-189">At hello prompt, run hello following command tooswitch connection toothis newly created database:</span></span>
```sql
USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="d7394-190">Creare tabelle nel database di hello</span><span class="sxs-lookup"><span data-stu-id="d7394-190">Create tables in hello database</span></span>
<span data-ttu-id="d7394-191">Ora che è stato appreso come tooconnect toohello Database di Azure per il database MySQL, possiamo andare come toocomplete alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="d7394-191">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="d7394-192">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="d7394-192">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="d7394-193">Creare una tabella che contenga le informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="d7394-193">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="d7394-194">Caricamento dei dati nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="d7394-194">Load data into hello tables</span></span>
<span data-ttu-id="d7394-195">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="d7394-195">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="d7394-196">Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati.</span><span class="sxs-lookup"><span data-stu-id="d7394-196">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="d7394-197">Ora si dispone di due righe di dati di esempio nella tabella hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d7394-197">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="d7394-198">Eseguire una query e aggiornare i dati nelle tabelle di hello hello</span><span class="sxs-lookup"><span data-stu-id="d7394-198">Query and update hello data in hello tables</span></span>
<span data-ttu-id="d7394-199">Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-199">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="d7394-200">È inoltre possibile aggiornare i dati di hello nelle tabelle di hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-200">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="d7394-201">la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="d7394-201">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="d7394-202">Ripristinare un punto precedente tooa di database nel tempo</span><span class="sxs-lookup"><span data-stu-id="d7394-202">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="d7394-203">Si supponga di essere eliminato per una tabella di database più importanti e non è possibile ripristinare facilmente i dati di hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-203">Imagine you have accidentally deleted an important database table, and cannot recover hello data easily.</span></span> <span data-ttu-id="d7394-204">Il Database di Azure per MySQL consente toorestore hello server tooa punto nel tempo, creazione di una copia dei database hello nel nuovo server.</span><span class="sxs-lookup"><span data-stu-id="d7394-204">Azure Database for MySQL allows you toorestore hello server tooa point in time, creating a copy of hello databases into new server.</span></span> <span data-ttu-id="d7394-205">È possibile utilizzare questo nuovo toorecover server i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="d7394-205">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="d7394-206">Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="d7394-206">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1. <span data-ttu-id="d7394-207">Nel portale di Azure hello, individuare il Database di Azure per MySQL.</span><span class="sxs-lookup"><span data-stu-id="d7394-207">In hello Azure portal, locate your Azure Database for MySQL.</span></span> <span data-ttu-id="d7394-208">In hello **Panoramica** pagina, fare clic su **ripristinare** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-208">On hello **Overview** page, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="d7394-209">verrà visualizzata la pagina ripristino Hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-209">hello Restore page opens.</span></span>

   ![10-1 Ripristinare un database](./media/tutorial-design-database-using-portal/10_1-restore-a-db.png)

2. <span data-ttu-id="d7394-211">Compilare hello **ripristinare** form con le informazioni necessarie hello.</span><span class="sxs-lookup"><span data-stu-id="d7394-211">Fill out hello **Restore** form with hello required information.</span></span>
   
   ![10-2 Modulo di ripristino](./media/tutorial-design-database-using-portal/10_2-restore-form.png)
   
   - <span data-ttu-id="d7394-213">**Punto di ripristino**: selezionare un punto-in-time che si desidera toorestore, entro il periodo di hello elencato.</span><span class="sxs-lookup"><span data-stu-id="d7394-213">**Restore point**: Select a point-in-time that you want toorestore to, within hello timeframe listed.</span></span> <span data-ttu-id="d7394-214">Verificare che tooconvert tooUTC il fuso orario locale.</span><span class="sxs-lookup"><span data-stu-id="d7394-214">Make sure tooconvert your local timezone tooUTC.</span></span>
   - <span data-ttu-id="d7394-215">**Ripristinare il server toonew**: fornire un nuovo nome del server desiderato toorestore per.</span><span class="sxs-lookup"><span data-stu-id="d7394-215">**Restore toonew server**: Provide a new server name you want toorestore to.</span></span>
   - <span data-ttu-id="d7394-216">**Percorso**: hello area è lo stesso server di origine hello e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="d7394-216">**Location**: hello region is same as hello source server, and cannot be changed.</span></span>
   - <span data-ttu-id="d7394-217">**Livello di prezzo**: hello tariffario è hello equivale hello server di origine e non può essere modificati.</span><span class="sxs-lookup"><span data-stu-id="d7394-217">**Pricing tier**: hello pricing tier is hello same as hello source server, and cannot be changed.</span></span>
   
3. <span data-ttu-id="d7394-218">Fare clic su **OK** toorestore hello server troppo[tooa punto di ripristino temporizzato](./howto-restore-server-portal.md) prima tabella hello è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="d7394-218">Click **OK** toorestore hello server too[restore tooa point in time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="d7394-219">Ripristino di un server crea una nuova copia del server di hello, a partire da hello punto nel tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="d7394-219">Restoring a server creates a new copy of hello server, as of hello point in time you specify.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d7394-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7394-220">Next steps</span></span>
<span data-ttu-id="d7394-221">In questa esercitazione, utilizzare la modalità hello toolearned portale Azure per:</span><span class="sxs-lookup"><span data-stu-id="d7394-221">In this tutorial, you use hello Azure portal toolearned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d7394-222">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="d7394-222">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="d7394-223">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="d7394-223">Configure hello server firewall</span></span>
> * <span data-ttu-id="d7394-224">Utilizzare lo strumento da riga di comando di mysql toocreate un database</span><span class="sxs-lookup"><span data-stu-id="d7394-224">Use mysql command-line tool toocreate a database</span></span>
> * <span data-ttu-id="d7394-225">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="d7394-225">Load sample data</span></span>
> * <span data-ttu-id="d7394-226">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="d7394-226">Query data</span></span>
> * <span data-ttu-id="d7394-227">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="d7394-227">Update data</span></span>
> * <span data-ttu-id="d7394-228">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="d7394-228">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d7394-229">Database tooconnect applicazioni tooAzure per MySQL</span><span class="sxs-lookup"><span data-stu-id="d7394-229">How tooconnect applications tooAzure Database for MySQL</span></span>](./howto-connection-string.md)
