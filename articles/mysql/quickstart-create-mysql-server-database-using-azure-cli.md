---
title: 'Avvio rapido: Creare un database di Azure per il server MySQL - Interfaccia della riga di comando di Azure | Microsoft Docs'
description: Questa Guida rapida viene descritto come toouse hello toocreate CLI di Azure un Database di Azure per il server MySQL in un gruppo di risorse di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: hero-article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 708d0cce12e812cb464adcf7e83e6f85c196bafe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-cli"></a><span data-ttu-id="f8386-103">Creare un database di Azure per il server MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f8386-103">Create an Azure Database for MySQL server using Azure CLI</span></span>
<span data-ttu-id="f8386-104">Questa Guida rapida viene descritto come toouse hello toocreate CLI di Azure un Database di Azure per il server MySQL in un gruppo di risorse di Azure in circa cinque minuti.</span><span class="sxs-lookup"><span data-stu-id="f8386-104">This quickstart describes how toouse hello Azure CLI toocreate an Azure Database for MySQL server in an Azure resource group in about five minutes.</span></span> <span data-ttu-id="f8386-105">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="f8386-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span>

<span data-ttu-id="f8386-106">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="f8386-106">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f8386-107">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="f8386-107">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f8386-108">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="f8386-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="f8386-109">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f8386-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="f8386-110">Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata di hello in cui esistano risorse hello o viene fatturata per.</span><span class="sxs-lookup"><span data-stu-id="f8386-110">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="f8386-111">Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="f8386-111">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f8386-112">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="f8386-112">Create a resource group</span></span>
<span data-ttu-id="f8386-113">Creare un [gruppo di risorse](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) utilizzando hello [gruppo az creare](https://docs.microsoft.com/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="f8386-113">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) using hello [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="f8386-114">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="f8386-114">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="f8386-115">esempio Hello crea un gruppo di risorse denominato `myresourcegroup` in hello `westus` percorso.</span><span class="sxs-lookup"><span data-stu-id="f8386-115">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="f8386-116">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="f8386-116">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="f8386-117">Creare un Database di Azure per il server MySQL con hello **creare server mysql az** comando.</span><span class="sxs-lookup"><span data-stu-id="f8386-117">Create an Azure Database for MySQL server with hello **az mysql server create** command.</span></span> <span data-ttu-id="f8386-118">Un server può gestire più database.</span><span class="sxs-lookup"><span data-stu-id="f8386-118">A server can manage multiple databases.</span></span> <span data-ttu-id="f8386-119">In genere, viene usato un database separato per ogni progetto o per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="f8386-119">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="f8386-120">esempio Hello crea un Database di Azure per il server MySQL situato in `westus` nel gruppo di risorse hello `myresourcegroup` con nome `myserver4demo`.</span><span class="sxs-lookup"><span data-stu-id="f8386-120">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `myresourcegroup` with name `myserver4demo`.</span></span> <span data-ttu-id="f8386-121">Hello server dispone di un accesso di amministratore in denominato `myadmin` e la password `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="f8386-121">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="f8386-122">Hello server viene creato con **base** livello di prestazioni e **50** unità condivisa tra tutti i database hello server hello di calcolo.</span><span class="sxs-lookup"><span data-stu-id="f8386-122">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="f8386-123">È possibile applicare la scalabilità di calcolo e archiviazione verso l'alto o verso il basso a seconda delle esigenze dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="f8386-123">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group myresourcegroup --name myserver4demo --location westus --admin-user myadmin --admin-password Password01! --performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="f8386-124">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="f8386-124">Configure firewall rule</span></span>
<span data-ttu-id="f8386-125">Creare un Database di Azure per la regola del firewall a livello di server MySQL mediante hello **az mysql regola firewall del server-creare** comando.</span><span class="sxs-lookup"><span data-stu-id="f8386-125">Create an Azure Database for MySQL server-level firewall rule using hello **az mysql server firewall-rule create** command.</span></span> <span data-ttu-id="f8386-126">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio hello **mysql.exe** strumento da riga di comando o un server di tooyour tooconnect MySQL Workbench tramite firewall del servizio Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="f8386-126">A server-level firewall rule allows an external application, such as hello **mysql.exe** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="f8386-127">Hello esempio seguente viene creata una regola del firewall per un intervallo di indirizzi predefiniti, ovvero in questo esempio hello intera possibili intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="f8386-127">hello following example creates a firewall rule for a predefined address range, which in this example is hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group myresourcegroup --server myserver4demo --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
## <a name="configure-ssl-settings"></a><span data-ttu-id="f8386-128">Configurare le impostazioni SSL</span><span class="sxs-lookup"><span data-stu-id="f8386-128">Configure SSL settings</span></span>
<span data-ttu-id="f8386-129">Per impostazione predefinita, tra il server e le applicazioni client vengono applicate connessioni SSL.</span><span class="sxs-lookup"><span data-stu-id="f8386-129">By default, SSL connections between your server and client applications are enforced.</span></span>  <span data-ttu-id="f8386-130">In questo modo di sicurezza di "in movimento" hello di dati mediante la crittografia di flusso di dati hello su internet.</span><span class="sxs-lookup"><span data-stu-id="f8386-130">This ensures security of "in-motion" data by encrypting hello data stream over hello internet.</span></span>  <span data-ttu-id="f8386-131">toomake questa rapida più semplice, abbiamo disabilitato le connessioni SSL per il server.</span><span class="sxs-lookup"><span data-stu-id="f8386-131">toomake this quick start easier, we disable SSL connections for your server.</span></span>  <span data-ttu-id="f8386-132">Questo comportamento non è consigliato per i server di produzione.</span><span class="sxs-lookup"><span data-stu-id="f8386-132">This is not recommended for production servers.</span></span>  <span data-ttu-id="f8386-133">Per ulteriori informazioni, vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](./howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f8386-133">For more information, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span>

<span data-ttu-id="f8386-134">Hello esempio seguente viene disabilitato l'applicazione SSL sul server MySQL.</span><span class="sxs-lookup"><span data-stu-id="f8386-134">hello following example disables enforcing SSL on your MySQL server.</span></span>
 
 ```azurecli-interactive
 az mysql server update --resource-group myresourcegroup --name myserver4demo -g -n --ssl-enforcement Disabled
 ```

## <a name="get-hello-connection-information"></a><span data-ttu-id="f8386-135">Ottenere informazioni sulla connessione hello</span><span class="sxs-lookup"><span data-stu-id="f8386-135">Get hello connection information</span></span>

<span data-ttu-id="f8386-136">tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.</span><span class="sxs-lookup"><span data-stu-id="f8386-136">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>

```azurecli-interactive
az mysql server show --resource-group myresourcegroup --name myserver4demo
```

<span data-ttu-id="f8386-137">il risultato di Hello è nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f8386-137">hello result is in JSON format.</span></span> <span data-ttu-id="f8386-138">Prendere nota di hello **fullyQualifiedDomainName** e **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="f8386-138">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "myserver4demo.mysql.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforMySQL/servers/myserver4demo",
  "location": "westus",
  "name": "myserver4demo",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-toohello-server-using-hello-mysqlexe-command-line-tool"></a><span data-ttu-id="f8386-139">Connessione server toohello utilizzando lo strumento da riga di comando di hello mysql.exe</span><span class="sxs-lookup"><span data-stu-id="f8386-139">Connect toohello server using hello mysql.exe command-line tool</span></span>
<span data-ttu-id="f8386-140">Connessione server tooyour utilizzando hello **mysql.exe** strumento da riga di comando.</span><span class="sxs-lookup"><span data-stu-id="f8386-140">Connect tooyour server using hello **mysql.exe** command-line tool.</span></span> <span data-ttu-id="f8386-141">È possibile scaricare MySQL da [qui](https://dev.mysql.com/downloads/) e installarlo nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="f8386-141">You can download MySQL from [here](https://dev.mysql.com/downloads/) and install it on your computer.</span></span> <span data-ttu-id="f8386-142">È invece possibile scegliere hello **Provalo** pulsante esempi di codice o hello `>_` pulsante hello superiore destro della barra degli strumenti in hello portale di Azure e avviare hello **Azure Cloud Shell**.</span><span class="sxs-lookup"><span data-stu-id="f8386-142">Instead you may also click hello **Try It** button on code samples, or hello  `>_` button from hello upper right toolbar in hello Azure portal, and launch hello **Azure Cloud Shell**.</span></span>

<span data-ttu-id="f8386-143">Digitare i comandi successivi hello:</span><span class="sxs-lookup"><span data-stu-id="f8386-143">Type hello next commands:</span></span> 

1. <span data-ttu-id="f8386-144">Connessione tramite server toohello **mysql** strumento da riga di comando:</span><span class="sxs-lookup"><span data-stu-id="f8386-144">Connect toohello server using **mysql** command-line tool:</span></span>
```azurecli-interactive
 mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
```

2. <span data-ttu-id="f8386-145">Visualizzare lo stato del server:</span><span class="sxs-lookup"><span data-stu-id="f8386-145">View server status:</span></span>
```sql
 mysql> status
```
<span data-ttu-id="f8386-146">Se tutto va bene, lo strumento da riga di comando hello deve restituire come output hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="f8386-146">If everything goes well, hello command-line tool should output hello following text:</span></span>

```dos
C:\Users\>mysql -h myserver4demo.mysql.database.azure.com -u myadmin@myserver4demo -p
Enter password: ***********
Welcome toohello MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 65512
Server version: 5.6.26.0 MySQL Community Server (GPL)

Copyright (c) 2000, 2016, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.

mysql> status
--------------
mysql  Ver 14.14 Distrib 5.6.35, for Win64 (x86_64)

Connection id:          65512
Current database:
Current user:           myadmin@116.230.243.143
SSL:                    Not in use
Using delimiter:        ;
Server version:         5.6.26.0 MySQL Community Server (GPL)
Protocol version:       10
Connection:             myserver4demo.mysql.database.azure.com via TCP/IP
Server characterset:    latin1
Db     characterset:    latin1
Client characterset:    gbk
Conn.  characterset:    gbk
TCP port:               3306
Uptime:                 2 days 9 hours 47 min 20 sec

Threads: 4  Questions: 34833  Slow queries: 2  Opens: 84  Flush tables: 4  Open tables: 1  Queries per second avg: 0.167
--------------

mysql>
```

> [!TIP]
> <span data-ttu-id="f8386-147">Per altri comandi, vedere il capitolo 4.5.1 di [MySQL 5.7 Reference Manual](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) (Manuale di riferimento di MySQL 5.7).</span><span class="sxs-lookup"><span data-stu-id="f8386-147">For additional commands, see [MySQL 5.7 Reference Manual - Chapter 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).</span></span>

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a><span data-ttu-id="f8386-148">Connessione server toohello strumento GUI Workbench MySQL hello</span><span class="sxs-lookup"><span data-stu-id="f8386-148">Connect toohello server using hello MySQL Workbench GUI tool</span></span>
1.  <span data-ttu-id="f8386-149">Avviare hello applicazione Workbench di MySQL nel computer client.</span><span class="sxs-lookup"><span data-stu-id="f8386-149">Launch hello MySQL Workbench application on your client computer.</span></span> <span data-ttu-id="f8386-150">È possibile scaricare e installare MySQL Workbench da [qui](https://dev.mysql.com/downloads/workbench/).</span><span class="sxs-lookup"><span data-stu-id="f8386-150">You can download and install MySQL Workbench from [here](https://dev.mysql.com/downloads/workbench/).</span></span>

2.  <span data-ttu-id="f8386-151">In hello **il programma di installazione nuova connessione** finestra di dialogo immettere le seguenti informazioni hello **parametri** scheda:</span><span class="sxs-lookup"><span data-stu-id="f8386-151">In hello **Setup New Connection** dialog box, enter hello following information on **Parameters** tab:</span></span>

   ![Setup New Connection (Configura nuova connessione)](./media/quickstart-create-mysql-server-database-using-azure-cli/setup-new-connection.png)

| <span data-ttu-id="f8386-153">**Impostazione**</span><span class="sxs-lookup"><span data-stu-id="f8386-153">**Setting**</span></span> | <span data-ttu-id="f8386-154">**Valore consigliato**</span><span class="sxs-lookup"><span data-stu-id="f8386-154">**Suggested Value**</span></span> | <span data-ttu-id="f8386-155">**Descrizione**</span><span class="sxs-lookup"><span data-stu-id="f8386-155">**Description**</span></span> |
|---|---|---|
|   <span data-ttu-id="f8386-156">Connection Name (Nome connessione)</span><span class="sxs-lookup"><span data-stu-id="f8386-156">Connection Name</span></span> | <span data-ttu-id="f8386-157">Connessione in uso</span><span class="sxs-lookup"><span data-stu-id="f8386-157">My Connection</span></span> | <span data-ttu-id="f8386-158">Specificare un'etichetta per la connessione (può essere qualsiasi nome)</span><span class="sxs-lookup"><span data-stu-id="f8386-158">Specify a label for this connection (this can be anything)</span></span> |
| <span data-ttu-id="f8386-159">Connection Method (Metodo di connessione)</span><span class="sxs-lookup"><span data-stu-id="f8386-159">Connection Method</span></span> | <span data-ttu-id="f8386-160">Scegliere Standard (TCP/IP)</span><span class="sxs-lookup"><span data-stu-id="f8386-160">choose Standard (TCP/IP)</span></span> | <span data-ttu-id="f8386-161">Utilizzare TCP/IP protocollo tooconnect tooAzure Database per MySQL ></span><span class="sxs-lookup"><span data-stu-id="f8386-161">Use TCP/IP protocol tooconnect tooAzure Database for MySQL></span></span> |
| <span data-ttu-id="f8386-162">Nome host</span><span class="sxs-lookup"><span data-stu-id="f8386-162">Hostname</span></span> | <span data-ttu-id="f8386-163">myserver4demo.mysql.database.azure.com</span><span class="sxs-lookup"><span data-stu-id="f8386-163">myserver4demo.mysql.database.azure.com</span></span> | <span data-ttu-id="f8386-164">Nome del server annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f8386-164">Server name you previously noted.</span></span> |
| <span data-ttu-id="f8386-165">Porta</span><span class="sxs-lookup"><span data-stu-id="f8386-165">Port</span></span> | <span data-ttu-id="f8386-166">3306</span><span class="sxs-lookup"><span data-stu-id="f8386-166">3306</span></span> | <span data-ttu-id="f8386-167">viene utilizzata la porta predefinita Hello per MySQL.</span><span class="sxs-lookup"><span data-stu-id="f8386-167">hello default port for MySQL is used.</span></span> |
| <span data-ttu-id="f8386-168">Username</span><span class="sxs-lookup"><span data-stu-id="f8386-168">Username</span></span> | myadmin@myserver4demo | <span data-ttu-id="f8386-169">Hello amministratore account di accesso server annotato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f8386-169">hello server admin login you previously noted.</span></span> |
| <span data-ttu-id="f8386-170">Password</span><span class="sxs-lookup"><span data-stu-id="f8386-170">Password</span></span> | **** | <span data-ttu-id="f8386-171">Utilizzare password dell'account admin hello configurati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="f8386-171">Use hello admin account password you configured earlier.</span></span> |

<span data-ttu-id="f8386-172">Fare clic su **Test connessione** tootest se tutti i parametri siano configurati correttamente.</span><span class="sxs-lookup"><span data-stu-id="f8386-172">Click **Test Connection** tootest if all parameters are correctly configured.</span></span>
<span data-ttu-id="f8386-173">A questo punto, è possibile fare clic su connessione hello toosuccessfully connettersi toohello server.</span><span class="sxs-lookup"><span data-stu-id="f8386-173">Now, you can click hello connection toosuccessfully connect toohello server.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f8386-174">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="f8386-174">Clean up resources</span></span>
<span data-ttu-id="f8386-175">Se queste risorse non è necessario per un altro conosca, è possibile eliminare effettuando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f8386-175">If you don't need these resources for another quickstart/tutorial, you can delete them by doing hello following command:</span></span> 

```azurecli-interactive
az group delete --name myresourcegroup
```

## <a name="next-steps"></a><span data-ttu-id="f8386-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f8386-176">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8386-177">Progettare un database MySQL con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f8386-177">Design a MySQL Database with Azure CLI</span></span>](./tutorial-design-database-using-cli.md)
