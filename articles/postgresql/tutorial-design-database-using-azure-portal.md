---
title: Progettare il primo Database di Azure per PostgreSQL tramite il portale di Azure | Documentazione Microsoft
description: In questa esercitazione viene illustrato come tooDesign di Azure prima di Database per PostgreSQL utilizzando hello portale di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: tutorial, mvc
ms.topic: tutorial
ms.date: 05/10/2017
ms.openlocfilehash: fde7e9d1ae2bad4291d18bebd3356f4f8a2ac86a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="9c45a-103">Progettazione di un Database di Azure per PostgreSQL utilizzando hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9c45a-103">Design your first Azure Database for PostgreSQL using hello Azure portal</span></span>

<span data-ttu-id="9c45a-104">Il Database di Azure per PostgreSQL è un servizio gestito che consente di toorun, gestire e scalare database PostgreSQL a disponibilità elevata nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="9c45a-105">Utilizza hello portale di Azure, è possibile facilmente gestire il server e progettare un database.</span><span class="sxs-lookup"><span data-stu-id="9c45a-105">Using hello Azure portal, you can easily manage your server and design a database.</span></span>

<span data-ttu-id="9c45a-106">In questa esercitazione, utilizzare la modalità hello toolearn portale Azure per:</span><span class="sxs-lookup"><span data-stu-id="9c45a-106">In this tutorial, you use hello Azure portal toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9c45a-107">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9c45a-107">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="9c45a-108">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="9c45a-108">Configure hello server firewall</span></span>
> * <span data-ttu-id="9c45a-109">Utilizzare [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilità un database</span><span class="sxs-lookup"><span data-stu-id="9c45a-109">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="9c45a-110">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="9c45a-110">Load sample data</span></span>
> * <span data-ttu-id="9c45a-111">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-111">Query data</span></span>
> * <span data-ttu-id="9c45a-112">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-112">Update data</span></span>
> * <span data-ttu-id="9c45a-113">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-113">Restore data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c45a-114">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="9c45a-114">Prerequisites</span></span>
<span data-ttu-id="9c45a-115">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="9c45a-115">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="9c45a-116">Accedi toohello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9c45a-116">Log in toohello Azure portal</span></span>
<span data-ttu-id="9c45a-117">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9c45a-117">Log in toohello [Azure portal](https://portal.azure.com).</span></span>

## <a name="create-an-azure-database-for-postgresql"></a><span data-ttu-id="9c45a-118">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9c45a-118">Create an Azure Database for PostgreSQL</span></span>

<span data-ttu-id="9c45a-119">Verrà creato un database di Azure per il server PostgreSQL con un set definito di [risorse di calcolo e di archiviazione](./concepts-compute-unit-and-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9c45a-119">An Azure Database for PostgreSQL server is created with a defined set of [compute and storage resources](./concepts-compute-unit-and-storage.md).</span></span> <span data-ttu-id="9c45a-120">Hello server viene creato all'interno di un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9c45a-120">hello server is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

<span data-ttu-id="9c45a-121">Seguire questi toocreate passaggi un Database di Azure per PostgreSQL server:</span><span class="sxs-lookup"><span data-stu-id="9c45a-121">Follow these steps toocreate an Azure Database for PostgreSQL server:</span></span>
1.  <span data-ttu-id="9c45a-122">Fare clic su hello **+ nuovo** pulsante disponibile nella hello angolo superiore sinistro del portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-122">Click hello **+ New**  button found on hello upper left-hand corner of hello Azure portal.</span></span>
2.  <span data-ttu-id="9c45a-123">Selezionare **database** da hello **New** pagina e selezionare **Database di Azure per PostgreSQL** da hello **database** pagina.</span><span class="sxs-lookup"><span data-stu-id="9c45a-123">Select **Databases** from hello **New** page, and select **Azure Database for PostgreSQL** from hello **Databases** page.</span></span>
 <span data-ttu-id="9c45a-124">![Il Database di Azure per PostgreSQL - creare database hello](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span><span class="sxs-lookup"><span data-stu-id="9c45a-124">![Azure Database for PostgreSQL - Create hello database](./media/tutorial-design-database-using-azure-portal/1-create-database.png)</span></span>

3.  <span data-ttu-id="9c45a-125">Compilare hello nuovi server Dettagli modulo con hello le seguenti informazioni, come mostrato nella precedente immagine hello:</span><span class="sxs-lookup"><span data-stu-id="9c45a-125">Fill out hello new server details form with hello following information, as shown on hello preceding image:</span></span>
    - <span data-ttu-id="9c45a-126">Nome del server: **mypgserver 20170401** (nome di un server esegue il mapping nome tooDNS ed è pertanto necessario toobe univoco globale)</span><span class="sxs-lookup"><span data-stu-id="9c45a-126">Server name: **mypgserver-20170401** (name of a server maps tooDNS name and is thus required toobe globally unique)</span></span> 
    - <span data-ttu-id="9c45a-127">Sottoscrizione: Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata di hello in cui esistano risorse hello o viene fatturata per.</span><span class="sxs-lookup"><span data-stu-id="9c45a-127">Subscription: If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span>
    - <span data-ttu-id="9c45a-128">Gruppo di risorse: **myresourcegroup**</span><span class="sxs-lookup"><span data-stu-id="9c45a-128">Resource group: **myresourcegroup**</span></span>
    - <span data-ttu-id="9c45a-129">L'accesso dell'amministratore del server e la password scelta</span><span class="sxs-lookup"><span data-stu-id="9c45a-129">Server admin login and password of your choice</span></span>
    - <span data-ttu-id="9c45a-130">Località</span><span class="sxs-lookup"><span data-stu-id="9c45a-130">Location</span></span>
    - <span data-ttu-id="9c45a-131">Versione di PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9c45a-131">PostgreSQL Version</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9c45a-132">account di accesso amministratore server Hello e una password che è possibile specificare sono necessari toolog toohello server e i relativi database più avanti in questa Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="9c45a-132">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="9c45a-133">Prendere nota di queste informazioni per usarle in seguito.</span><span class="sxs-lookup"><span data-stu-id="9c45a-133">Remember or record this information for later use.</span></span>

4.  <span data-ttu-id="9c45a-134">Fare clic su **tariffario** toospecify hello servizio livello di prestazioni e per il nuovo database.</span><span class="sxs-lookup"><span data-stu-id="9c45a-134">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="9c45a-135">Per questa guida di avvio rapido, selezionare il livello **Basic**, **50 unità di calcolo** e **50 GB** di spazio di archiviazione incluso.</span><span class="sxs-lookup"><span data-stu-id="9c45a-135">For this quick start, select **Basic** Tier, **50 Compute Units** and **50 GB** of included storage.</span></span>
 <span data-ttu-id="9c45a-136">![Database di Azure per PostgreSQL - livello di servizio hello selezione](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span><span class="sxs-lookup"><span data-stu-id="9c45a-136">![Azure Database for PostgreSQL - pick hello service tier](./media/tutorial-design-database-using-azure-portal/2-service-tier.png)</span></span>
5.  <span data-ttu-id="9c45a-137">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-137">Click **Ok**.</span></span>
6.  <span data-ttu-id="9c45a-138">Fare clic su **crea** server hello tooprovision.</span><span class="sxs-lookup"><span data-stu-id="9c45a-138">Click **Create** tooprovision hello server.</span></span> <span data-ttu-id="9c45a-139">Il provisioning richiede alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9c45a-139">Provisioning takes a few minutes.</span></span>

  > [!TIP]
  > <span data-ttu-id="9c45a-140">Controllare hello **toodashboard Pin** rilevamento semplice di opzione tooallow delle distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="9c45a-140">Check hello **Pin toodashboard** option tooallow easy tracking of your deployments.</span></span>

7.  <span data-ttu-id="9c45a-141">Sulla barra degli strumenti hello, fare clic su **notifiche** toomonitor processo di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-141">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>
 <span data-ttu-id="9c45a-142">![Database di Azure per PostgreSQL - Vedere le notifiche](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span><span class="sxs-lookup"><span data-stu-id="9c45a-142">![Azure Database for PostgreSQL - See notifications](./media/tutorial-design-database-using-azure-portal/3-notifications.png)</span></span>
   
  <span data-ttu-id="9c45a-143">Per impostazione predefinita, il database **postgres** viene creato nel server.</span><span class="sxs-lookup"><span data-stu-id="9c45a-143">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="9c45a-144">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database è un database predefinito può essere utilizzata per gli utenti, utilità e applicazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="9c45a-144">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 

## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="9c45a-145">Configurare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="9c45a-145">Configure a server-level firewall rule</span></span>

<span data-ttu-id="9c45a-146">Hello Azure Database PostgreSQL servizio consente di creare un firewall a livello di server hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-146">hello Azure Database for PostgreSQL service creates a firewall at hello server-level.</span></span> <span data-ttu-id="9c45a-147">Questo firewall impedisce la applicazioni esterne e gli strumenti connessione toohello server e tutti i database nel server di hello solo una regola del firewall creata firewall hello tooopen per indirizzi IP specifici.</span><span class="sxs-lookup"><span data-stu-id="9c45a-147">This firewall prevents external applications and tools from connecting toohello server and any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> 

1.  <span data-ttu-id="9c45a-148">Al termine della distribuzione di hello, fare clic su **tutte le risorse** dal menu a sinistra hello e digitare il nome di hello **mypgserver 20170401** toosearch per il server appena creato.</span><span class="sxs-lookup"><span data-stu-id="9c45a-148">After hello deployment completes, click **All Resources** from hello left-hand menu and type in hello name **mypgserver-20170401** toosearch for your newly created server.</span></span> <span data-ttu-id="9c45a-149">Fare clic su un nome server hello elencato nei risultati di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-149">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="9c45a-150">Hello **Panoramica** pagina per il server viene aperto e offre opzioni per un'ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="9c45a-150">hello **Overview** page for your server opens and provides options for further configuration.</span></span>
 
 ![<span data-ttu-id="9c45a-151">Database di Azure per PostgreSQL - Cercare il server</span><span class="sxs-lookup"><span data-stu-id="9c45a-151">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

2.  <span data-ttu-id="9c45a-152">Nel Pannello di hello server, selezionare **sicurezza della connessione**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-152">In hello server blade, select **Connection Security**.</span></span> 
3.  <span data-ttu-id="9c45a-153">Fare clic nella casella di testo hello in **nome della regola,** e aggiungere un nuovo firewall regola toowhitelist hello intervallo IP per la connettività.</span><span class="sxs-lookup"><span data-stu-id="9c45a-153">Click in hello text box under **Rule Name,** and add a new firewall rule toowhitelist hello IP range for connectivity.</span></span> <span data-ttu-id="9c45a-154">Per questa esercitazione, consentire tutti gli indirizzi IP digitando **Rule Name = AllowAllIps**, **IP iniziale = 0.0.0.0** e **IP finale = 255.255.255.255** e quindi fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-154">For this tutorial, let's allow all IPs by typing in **Rule Name = AllowAllIps**, **Start IP = 0.0.0.0** and **End IP = 255.255.255.255** and then click **Save**.</span></span> <span data-ttu-id="9c45a-155">È possibile impostare una regola del firewall che copre un intervallo IP toobe tooconnect in grado di dalla rete.</span><span class="sxs-lookup"><span data-stu-id="9c45a-155">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span>
 
 ![Database di Azure per PostgreSQL - Creare una regola del firewall](./media/tutorial-design-database-using-azure-portal/5-firewall-2.png)

4.  <span data-ttu-id="9c45a-157">Fare clic su **salvare** e quindi fare clic su hello **X** tooclose hello **sicurezza connessioni** pagina.</span><span class="sxs-lookup"><span data-stu-id="9c45a-157">Click **Save** and then click hello **X** tooclose hello **Connections Security** page.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9c45a-158">Il server PostgreSQL Azure comunica sulla porta 5432.</span><span class="sxs-lookup"><span data-stu-id="9c45a-158">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="9c45a-159">Se si sta tentando di tooconnect da una rete aziendale, il traffico in uscita sulla porta 5432 può non essere consentito dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="9c45a-159">If you are trying tooconnect from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="9c45a-160">In questo caso, non sarà server di Database SQL di Azure in grado di tooconnect tooyour, a meno che il reparto IT apre la porta 5432.</span><span class="sxs-lookup"><span data-stu-id="9c45a-160">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 5432.</span></span>
  >


## <a name="get-hello-connection-information"></a><span data-ttu-id="9c45a-161">Ottenere informazioni sulla connessione hello</span><span class="sxs-lookup"><span data-stu-id="9c45a-161">Get hello connection information</span></span>

<span data-ttu-id="9c45a-162">Quando abbiamo creato il Database di Azure per server PostgreSQL, hello predefinito **postgres** database viene inoltre creato.</span><span class="sxs-lookup"><span data-stu-id="9c45a-162">When we created our Azure Database for PostgreSQL server, hello default **postgres** database also gets created.</span></span> <span data-ttu-id="9c45a-163">server di database tooyour tooconnect, sono necessarie credenziali di accesso e le informazioni di host tooprovide.</span><span class="sxs-lookup"><span data-stu-id="9c45a-163">tooconnect tooyour database server, you need tooprovide host information and access credentials.</span></span>

1. <span data-ttu-id="9c45a-164">Dal menu a sinistra di hello nel portale di Azure, fare clic su **tutte le risorse** cercare hello server appena creato e **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-164">From hello left-hand menu in Azure portal, click **All resources** and search for hello server you just created **mypgserver-20170401**.</span></span>

  ![<span data-ttu-id="9c45a-165">Database di Azure per PostgreSQL - Cercare il server</span><span class="sxs-lookup"><span data-stu-id="9c45a-165">Azure Database for PostgreSQL - Search for server</span></span> ](./media/tutorial-design-database-using-azure-portal/4-locate.png)

3. <span data-ttu-id="9c45a-166">Fare clic sul nome di server hello **mypgserver 20170401**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-166">Click hello server name **mypgserver-20170401**.</span></span>
4. <span data-ttu-id="9c45a-167">Server di selezionare hello **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="9c45a-167">Select hello server's **Overview** page.</span></span> <span data-ttu-id="9c45a-168">Prendere nota di hello **nome Server** e **nome account di accesso di amministratore Server**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-168">Make a note of hello **Server name** and **Server admin login name**.</span></span>

 ![Database di Azure per PostgreSQL - Accesso dell'amministratore del server](./media/tutorial-design-database-using-azure-portal/6-server-name.png)


## <a name="connect-toopostgresql-database-using-psql-in-cloud-shell"></a><span data-ttu-id="9c45a-170">La connessione a database tooPostgreSQL utilizzando psql nella Shell di Cloud</span><span class="sxs-lookup"><span data-stu-id="9c45a-170">Connect tooPostgreSQL database using psql in Cloud Shell</span></span>

<span data-ttu-id="9c45a-171">Verrà ora utilizzare hello psql utilità della riga di comando tooconnect toohello Azure Database PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="9c45a-171">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span> 
1. <span data-ttu-id="9c45a-172">Avviare hello Shell di Cloud di Azure tramite l'icona di terminal hello nel riquadro di spostamento superiore hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-172">Launch hello Azure Cloud Shell via hello terminal icon on hello top navigation pane.</span></span>

   ![Database di Azure per PostgreSQL - Icona del terminale di Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/7-cloud-shell.png)

2. <span data-ttu-id="9c45a-174">Hello Azure Cloud Shell apre nel browser, consentendo tootype bash comandi.</span><span class="sxs-lookup"><span data-stu-id="9c45a-174">hello Azure Cloud Shell opens in your browser, enabling you tootype bash commands.</span></span>

   ![Database di Azure per PostgreSQL - Prompt Bash di Azure Cloud Shell](./media/tutorial-design-database-using-azure-portal/8-bash.png)

3. <span data-ttu-id="9c45a-176">Al prompt della Shell Cloud hello connettersi tooyour Database di Azure per server PostgreSQL utilizzando i comandi psql hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-176">At hello Cloud Shell prompt, connect tooyour Azure Database for PostgreSQL server using hello psql commands.</span></span> <span data-ttu-id="9c45a-177">il formato seguente Hello è tooan tooconnect utilizzati Database di Azure per server PostgreSQL con hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utilità:</span><span class="sxs-lookup"><span data-stu-id="9c45a-177">hello following format is used tooconnect tooan Azure Database for PostgreSQL server with hello [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility:</span></span>
   ```bash
   psql --host=<myserver> --port=<port> --username=<server admin login> --dbname=<database name>
   ```

   <span data-ttu-id="9c45a-178">Ad esempio, hello comando seguente si connette a database predefinito toohello chiamato **postgres** sul server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizzando le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="9c45a-178">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="9c45a-179">Quando richiesto, immettere la password di amministratore del server.</span><span class="sxs-lookup"><span data-stu-id="9c45a-179">Enter your server admin password when prompted.</span></span>

   ```bash
   psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
   ```

## <a name="create-a-new-database"></a><span data-ttu-id="9c45a-180">Creare un nuovo database</span><span class="sxs-lookup"><span data-stu-id="9c45a-180">Create a New Database</span></span>
<span data-ttu-id="9c45a-181">Dopo aver connesso toohello server, è possibile creare un database vuoto al prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-181">Once you're connected toohello server, create a blank database at hello prompt.</span></span>
```bash
CREATE DATABASE mypgsqldb;
```

<span data-ttu-id="9c45a-182">Al prompt dei comandi hello, eseguire hello seguente database toohello appena creato di comando tooswitch connessione **mypgsqldb**.</span><span class="sxs-lookup"><span data-stu-id="9c45a-182">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**.</span></span>
```bash
\c mypgsqldb
```
## <a name="create-tables-in-hello-database"></a><span data-ttu-id="9c45a-183">Creare tabelle nel database di hello</span><span class="sxs-lookup"><span data-stu-id="9c45a-183">Create tables in hello database</span></span>
<span data-ttu-id="9c45a-184">Ora che è stato appreso come tooconnect toohello Database di Azure per PostgreSQL, possiamo andare come toocomplete alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="9c45a-184">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="9c45a-185">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="9c45a-185">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="9c45a-186">Creare una tabella che tiene traccia delle informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="9c45a-186">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="9c45a-187">È possibile visualizzare hello appena creato tabella nell'elenco di hello di tabvles ora digitando:</span><span class="sxs-lookup"><span data-stu-id="9c45a-187">You can see hello newly created table in hello list of tabvles now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="9c45a-188">Caricamento dei dati nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="9c45a-188">Load data into hello tables</span></span>
<span data-ttu-id="9c45a-189">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="9c45a-189">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="9c45a-190">Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-190">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="9c45a-191">È ora due righe di dati di esempio nella tabella hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="9c45a-191">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="9c45a-192">Eseguire una query e aggiornare i dati nelle tabelle di hello hello</span><span class="sxs-lookup"><span data-stu-id="9c45a-192">Query and update hello data in hello tables</span></span>
<span data-ttu-id="9c45a-193">Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-193">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="9c45a-194">È inoltre possibile aggiornare i dati di hello nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="9c45a-194">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="9c45a-195">la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="9c45a-195">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-data-tooa-previous-point-in-time"></a><span data-ttu-id="9c45a-196">Dati tooa precedente punto di ripristino temporizzato</span><span class="sxs-lookup"><span data-stu-id="9c45a-196">Restore data tooa previous point in time</span></span>
<span data-ttu-id="9c45a-197">Si supponga di aver eliminato accidentalmente questa tabella.</span><span class="sxs-lookup"><span data-stu-id="9c45a-197">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="9c45a-198">Questa situazione non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="9c45a-198">This situation is something you cannot easily recover from.</span></span> <span data-ttu-id="9c45a-199">Il Database di Azure per PostgreSQL consente toogo tooany indietro punto nel tempo (in hello ultimo backup too7 giorni (Basic) e 35 giorni (Standard)) e il ripristino di questo nuovo server tooa punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="9c45a-199">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="9c45a-200">È possibile utilizzare questo nuovo toorecover server i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="9c45a-200">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="9c45a-201">Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="9c45a-201">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

1.  <span data-ttu-id="9c45a-202">Hello Azure Database PostgreSQL pagina per il server, scegliere **ripristinare** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-202">On hello Azure Database for PostgreSQL page for your server, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="9c45a-203">Hello **ripristinare** verrà visualizzata la pagina.</span><span class="sxs-lookup"><span data-stu-id="9c45a-203">hello **Restore** page opens.</span></span>
  <span data-ttu-id="9c45a-204">![Portale di Azure - Opzioni del modulo di ripristino](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span><span class="sxs-lookup"><span data-stu-id="9c45a-204">![Azure portal - Restore form options](./media/tutorial-design-database-using-azure-portal/9-azure-portal-restore.png)</span></span>
2.  <span data-ttu-id="9c45a-205">Compilare hello **ripristinare** form con le informazioni necessarie hello:</span><span class="sxs-lookup"><span data-stu-id="9c45a-205">Fill out hello **Restore** form with hello required information:</span></span>

  ![Portale di Azure - Opzioni del modulo di ripristino](./media/tutorial-design-database-using-azure-portal/10-azure-portal-restore.png)
  - <span data-ttu-id="9c45a-207">**Punto di ripristino**: selezionare un punto nel tempo che si verifica prima che il server di hello è stato modificato</span><span class="sxs-lookup"><span data-stu-id="9c45a-207">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="9c45a-208">**Server di destinazione**: fornire un nuovo nome del server desiderato toorestore per</span><span class="sxs-lookup"><span data-stu-id="9c45a-208">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="9c45a-209">**Percorso**: non è possibile selezionare l'area di hello, per impostazione predefinita è uguale al server di origine hello</span><span class="sxs-lookup"><span data-stu-id="9c45a-209">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="9c45a-210">**Piano tariffario**: non è possibile modificare questo valore quando si ripristina un server.</span><span class="sxs-lookup"><span data-stu-id="9c45a-210">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="9c45a-211">È uguale al server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="9c45a-211">It is same as hello source server.</span></span> 
3.  <span data-ttu-id="9c45a-212">Fare clic su **OK** toorestore hello server troppo[tooa momento di ripristinare](./howto-restore-server-portal.md) prima tabelle hello è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="9c45a-212">Click **OK** toorestore hello server too[restore tooa point-in-time](./howto-restore-server-portal.md) before hello tables was deleted.</span></span> <span data-ttu-id="9c45a-213">Ripristino di un punto diverso di server tooa nel tempo crea un duplicato nuovo server come server originale hello come hello punto nel tempo specificato, purché tale valore entro il periodo di memorizzazione hello per le [livello di servizio](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="9c45a-213">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9c45a-214">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9c45a-214">Next Steps</span></span>
<span data-ttu-id="9c45a-215">In questa esercitazione, si è appreso come toouse hello portale di Azure e altre utilità per:</span><span class="sxs-lookup"><span data-stu-id="9c45a-215">In this tutorial, you learned how toouse hello Azure portal and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="9c45a-216">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9c45a-216">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="9c45a-217">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="9c45a-217">Configure hello server firewall</span></span>
> * <span data-ttu-id="9c45a-218">Utilizzare [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilità un database</span><span class="sxs-lookup"><span data-stu-id="9c45a-218">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="9c45a-219">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="9c45a-219">Load sample data</span></span>
> * <span data-ttu-id="9c45a-220">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-220">Query data</span></span>
> * <span data-ttu-id="9c45a-221">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-221">Update data</span></span>
> * <span data-ttu-id="9c45a-222">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="9c45a-222">Restore data</span></span>

<span data-ttu-id="9c45a-223">Per ulteriori informazioni come attività simili toodo CLI di Azure toouse, rivedere l'esercitazione: [di progettazione di un Database di Azure per PostgreSQL mediante Azure CLI](tutorial-design-database-using-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9c45a-223">Next, learn how toouse Azure CLI toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using Azure CLI](tutorial-design-database-using-azure-cli.md)</span></span>
