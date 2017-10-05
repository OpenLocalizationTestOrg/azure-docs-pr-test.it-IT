---
title: Creare e gestire le regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Questo articolo descrive come creare e gestire regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="83072-103">Creare e gestire regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="83072-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="83072-104">Le regole del firewall a livello di server consentono agli amministratori di gestire l'accesso a un'istanza di Database di Azure per il server MySQL da uno specifico indirizzo IP o intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="83072-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="83072-105">Usando pratici comandi dell'interfaccia della riga di comando di Azure è possibile creare, aggiornare, eliminare, elencare e visualizzare le regole del firewall per gestire il server.</span><span class="sxs-lookup"><span data-stu-id="83072-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="83072-106">Per una panoramica dei firewall di Database di Azure per MySQL, vedere [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server MySQL)</span><span class="sxs-lookup"><span data-stu-id="83072-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83072-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="83072-107">Prerequisites</span></span>
* [<span data-ttu-id="83072-108">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="83072-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="83072-109">Installare Azure Python SDK per PostgreSQL e i servizi MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="83072-110">Installare il componente dell'interfaccia della riga di comando di Azure per PostgreSQL e i servizi MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="83072-111">Creare un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="83072-112">Comandi per le regole del firewall:</span><span class="sxs-lookup"><span data-stu-id="83072-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="83072-113">Il comando **az mysql server firewall-rule** viene usato dall'interfaccia della riga di comando di Azure per creare, eliminare, elencare, visualizzare e aggiornare le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="83072-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="83072-114">Comandi:</span><span class="sxs-lookup"><span data-stu-id="83072-114">Commands:</span></span>
- <span data-ttu-id="83072-115">**create**: creare una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="83072-116">**delete**: eliminare una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="83072-117">**list**: elencare le regole del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="83072-118">**show**: visualizzare i dettagli di una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="83072-119">**update**: aggiornare una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="83072-120">Accedere ad Azure ed elencare le istanze di Database di Azure per i server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="83072-121">Connettere in modo sicuro l'interfaccia della riga di comando di Azure all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="83072-122">A tale scopo, usare il comando **az login**.</span><span class="sxs-lookup"><span data-stu-id="83072-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="83072-123">Eseguire il comando seguente dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="83072-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="83072-124">Questo comando restituirà un codice da usare nel passaggio successivo.</span><span class="sxs-lookup"><span data-stu-id="83072-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="83072-125">Usare un Web browser per aprire la pagina [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e immettere il codice.</span><span class="sxs-lookup"><span data-stu-id="83072-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="83072-126">Al prompt dei comandi, accedere usando le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="83072-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="83072-127">Dopo che l'accesso è stato autorizzato, nella console verrà visualizzato un elenco di sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="83072-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="83072-128">Copiare l'ID della sottoscrizione desiderata per impostare la sottoscrizione corrente da usare per procedere.</span><span class="sxs-lookup"><span data-stu-id="83072-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="83072-129">Elencare le istanze di Database di Azure per i server MySQL per la sottoscrizione e il gruppo di risorse, se non si è certi dei nomi.</span><span class="sxs-lookup"><span data-stu-id="83072-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="83072-130">Prendere nota dell'attributo del nome nell'elenco, che verrà usato per specificare il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="83072-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="83072-131">Se necessario, verificare i dettagli del server usando l'attributo del nome per verificare che il nome sia corretto:</span><span class="sxs-lookup"><span data-stu-id="83072-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="83072-132">Elencare le regole del firewall per un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="83072-133">Usando il nome del server e il nome del gruppo di risorse, elencare le regole del firewall esistenti nel server.</span><span class="sxs-lookup"><span data-stu-id="83072-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="83072-134">Si noti che l'attributo del nome server è specificato nell'opzione **--server** e non nell'opzione **--name**.</span><span class="sxs-lookup"><span data-stu-id="83072-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="83072-135">L'output elencherà le eventuali regole presenti, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="83072-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="83072-136">È possibile usare l'opzione **--output table** per ottenere un formato di tabella più leggibile come output.</span><span class="sxs-lookup"><span data-stu-id="83072-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="83072-137">Creare una regola del firewall nell'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="83072-138">Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, creare una nuova regola del firewall nel server.</span><span class="sxs-lookup"><span data-stu-id="83072-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="83072-139">Specificare un nome per la regola, oltre all'indirizzo IP iniziale e all'indirizzo IP finale per coprire un intervallo di indirizzi IP cui consentire l'accesso.</span><span class="sxs-lookup"><span data-stu-id="83072-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="83072-140">Per consentire l'accesso a un solo indirizzo IP, specificare lo stesso valore come indirizzo IP iniziale e finale, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="83072-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="83072-141">Al termine dell'operazione, l'output del comando elencherà i dettagli della regola del firewall creata, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="83072-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="83072-142">Se si verifica un errore, l'output visualizzerà invece il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="83072-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="83072-143">Aggiornare una regola del firewall in Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="83072-144">Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, aggiornare una regola del firewall esistente nel server.</span><span class="sxs-lookup"><span data-stu-id="83072-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="83072-145">Specificare il nome della regola del firewall esistente come input e gli attributi dell'indirizzo IP iniziale e finale per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="83072-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="83072-146">Al termine dell'operazione, l'output del comando elencherà i dettagli della regola del firewall aggiornata, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="83072-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="83072-147">Se si verifica un errore, l'output visualizzerà invece il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="83072-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="83072-148">Se la regola del firewall non esiste, verrà creata dal comando di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="83072-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="83072-149">Visualizzare i dettagli di una regola del firewall in Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="83072-150">Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, visualizzare i dettagli di una regola del firewall esistente nel server.</span><span class="sxs-lookup"><span data-stu-id="83072-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="83072-151">Specificare il nome della regola del firewall esistente come input.</span><span class="sxs-lookup"><span data-stu-id="83072-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="83072-152">Al termine dell'operazione, l'output del comando elencherà i dettagli della regola del firewall specificata, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="83072-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="83072-153">Se si verifica un errore, l'output visualizzerà invece il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="83072-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="83072-154">Eliminare una regola del firewall in Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="83072-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="83072-155">Usando il nome del server MySQL di Azure e il nome del gruppo di risorse, rimuovere una regola del firewall esistente dal server.</span><span class="sxs-lookup"><span data-stu-id="83072-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="83072-156">Specificare il nome della regola del firewall esistente.</span><span class="sxs-lookup"><span data-stu-id="83072-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="83072-157">Al completamento dell'operazione non verrà visualizzato alcun output.</span><span class="sxs-lookup"><span data-stu-id="83072-157">Upon success, there is no output.</span></span> <span data-ttu-id="83072-158">In caso di errore, verrà restituito il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="83072-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="83072-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="83072-159">Next steps</span></span>
- <span data-ttu-id="83072-160">Altre informazioni sulle [regole del firewall di Database di Azure per il server MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="83072-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="83072-161">Creare e gestire regole del firewall di Database di Azure per MySQL con il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="83072-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
