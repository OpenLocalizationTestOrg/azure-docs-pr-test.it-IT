---
title: aaaCreate e gestire i Database di Azure per le regole firewall di MySQL mediante Azure CLI | Documenti Microsoft
description: Questo articolo viene descritto come toocreate e gestire i Database di Azure per le regole firewall di MySQL mediante riga di comando CLI di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="4d315-103">Creare e gestire regole del firewall di Database di Azure per MySQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="4d315-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="4d315-104">Regole del firewall a livello di server abilitare amministratori toomanage accesso tooan Database di Azure per il MySQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="4d315-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="4d315-105">Usare i comandi CLI di Azure pratici, è possibile creare, aggiornare, eliminare, elencare e Mostra toomanage regole firewall del server.</span><span class="sxs-lookup"><span data-stu-id="4d315-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="4d315-106">Per una panoramica dei firewall di Database di Azure per MySQL, vedere [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server MySQL)</span><span class="sxs-lookup"><span data-stu-id="4d315-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d315-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4d315-107">Prerequisites</span></span>
* [<span data-ttu-id="4d315-108">Installare l'interfaccia della riga di comando di Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="4d315-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="4d315-109">Installare Azure Python SDK per PostgreSQL e i servizi MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="4d315-110">Installare il componente di hello CLI di Azure per i servizi MySQL e PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4d315-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="4d315-111">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="4d315-112">Comandi per le regole del firewall:</span><span class="sxs-lookup"><span data-stu-id="4d315-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="4d315-113">Hello **az mysql regola firewall del server-** comando viene utilizzato da toocreate CLI di Azure, eliminare, elenco, visualizzare e aggiornare le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="4d315-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="4d315-114">Comandi:</span><span class="sxs-lookup"><span data-stu-id="4d315-114">Commands:</span></span>
- <span data-ttu-id="4d315-115">**create**: creare una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d315-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4d315-116">**delete**: eliminare una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d315-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4d315-117">**elenco** : elenco di regole firewall del server MySQL a Azure hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="4d315-118">**Mostra** : Mostra i dettagli di hello del server MySQL a Azure regola del firewall.</span><span class="sxs-lookup"><span data-stu-id="4d315-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="4d315-119">**update**: aggiornare una regola del firewall del server MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d315-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="4d315-120">TooAzure account di accesso e l'elenco di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="4d315-121">Connettere in modo sicuro l'interfaccia della riga di comando di Azure all'account Azure.</span><span class="sxs-lookup"><span data-stu-id="4d315-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="4d315-122">Hello utilizzare **accesso az** comando toodo questo.</span><span class="sxs-lookup"><span data-stu-id="4d315-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="4d315-123">Eseguire hello comando seguente dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="4d315-124">Questo comando genera un codice toouse nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="4d315-125">Utilizzare la pagina web browser tooopen hello [https://aka.ms/devicelogin](https://aka.ms/devicelogin) e immettere il codice hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="4d315-126">Al prompt dei comandi hello, accedere con le credenziali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d315-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="4d315-127">Una volta che l'account di accesso è autorizzato, un elenco di sottoscrizioni verrà stampato nella console di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="4d315-128">Id di hello una copia di hello desiderato sottoscrizione tooset hello corrente sottoscrizione toobe usato in futuro.</span><span class="sxs-lookup"><span data-stu-id="4d315-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="4d315-129">Elenco hello i database di Azure per i server di MySQL per il gruppo di risorse e di sottoscrizione se non si è certi di nomi di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="4d315-130">Si noti hello attributo del nome in hello elenco, che sarà utilizzato toospecify quali toowork di server MySQL in.</span><span class="sxs-lookup"><span data-stu-id="4d315-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="4d315-131">Se necessario, verificare i dettagli di hello toousing hello Nome attributo tooconfirm il nome del server sia corretto:</span><span class="sxs-lookup"><span data-stu-id="4d315-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="4d315-132">Elencare le regole del firewall per un'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="4d315-133">Utilizzando il nome di server hello e nome gruppo di risorse hello, elenco hello esistente regole del firewall nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="4d315-134">L'attributo nome server hello è specificato in hello **-server** passa e non hello **-nome** passare.</span><span class="sxs-lookup"><span data-stu-id="4d315-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="4d315-135">output di Hello elencherà regole hello, se presente, per impostazione predefinita in JSON di formato.</span><span class="sxs-lookup"><span data-stu-id="4d315-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="4d315-136">È possibile utilizzare l'opzione hello **-tabella di output** per un formato più leggibile di tabella come output di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4d315-137">Creare una regola del firewall nell'istanza di Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4d315-138">Nome del server MySQL a Azure hello e nome del gruppo di risorse hello di creare una nuova regola firewall nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="4d315-139">Specificare un nome per la regola hello, indirizzo IP iniziale hello e IP finale per hello regola toocover un accesso tooallow di indirizzi IP dell'intervallo.</span><span class="sxs-lookup"><span data-stu-id="4d315-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="4d315-140">Per un indirizzo IP specifico indirizzo toobe consentito l'accesso, fornire hello stesso indirizzo come hello IP iniziale e IP finale, come nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="4d315-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="4d315-141">Al completamento dell'operazione, l'output del comando hello elencherà dettagli hello hello regola del firewall creata per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4d315-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="4d315-142">Se si verifica un errore, output di hello mostrerà testo messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="4d315-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4d315-143">Aggiornare una regola del firewall in Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="4d315-144">Usa nome del server MySQL a Azure hello e nome del gruppo di risorse hello, aggiornare una regola firewall esistente nel server di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="4d315-145">Specificare il nome di hello della regola firewall esistente hello come input e hello inizio IP e fine IP attributi tooupdate.</span><span class="sxs-lookup"><span data-stu-id="4d315-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="4d315-146">Al completamento dell'operazione, l'output del comando hello elencherà dettagli hello hello regola del firewall che sono state aggiornate, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4d315-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="4d315-147">Se si verifica un errore, output di hello mostrerà testo messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="4d315-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="4d315-148">Se non esiste una regola del firewall hello, si verrà creato dal comando di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="4d315-149">Visualizzare i dettagli di una regola del firewall in Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4d315-150">Usa nome del server MySQL a Azure hello e nome del gruppo di risorse hello, dettagli hello esistente firewall regola dal server hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="4d315-151">Specificare il nome di hello della regola firewall esistente hello come input.</span><span class="sxs-lookup"><span data-stu-id="4d315-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4d315-152">Al completamento dell'operazione, l'output del comando hello elencherà dettagli hello hello regola del firewall che è stato specificato, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="4d315-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="4d315-153">Se si verifica un errore, output di hello mostrerà testo messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="4d315-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="4d315-154">Eliminare una regola del firewall in Database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="4d315-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="4d315-155">Nome del server MySQL a Azure hello e nome del gruppo di risorse hello di rimuovere una regola firewall esistente dal server di hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="4d315-156">Specificare il nome di hello della regola firewall esistente hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="4d315-157">Al completamento dell'operazione non verrà visualizzato alcun output.</span><span class="sxs-lookup"><span data-stu-id="4d315-157">Upon success, there is no output.</span></span> <span data-ttu-id="4d315-158">In caso di errore, verrà restituito testo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="4d315-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d315-159">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d315-159">Next steps</span></span>
- <span data-ttu-id="4d315-160">Altre informazioni sulle [regole del firewall di Database di Azure per il server MySQL](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="4d315-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="4d315-161">Creare e gestire i Database di Azure per le regole firewall di MySQL mediante hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="4d315-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
