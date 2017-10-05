---
title: Script dell'interfaccia della riga di comando - Creare un database di Azure per PostgreSQL | Documentazione Microsoft
description: Script dell'interfaccia della riga di comando di Azure - Crea un singolo database di Azure per il server PostgreSQL e configura una regola di firewall a livello di server.
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: e545b568cd57fdcf28ab33a5ebfa34a495111c7f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="b9fb5-103">Creare un database di Azure per il server PostgreSQL e configurare una regola di firewall tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="b9fb5-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="b9fb5-104">Questo esempio di script dell'interfaccia della riga di comando di Azure crea un singolo database di Azure per il server PostgreSQL e configura una regola di firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="b9fb5-105">Dopo aver eseguito correttamente lo script, è possibile accedere al server PostgreSQL da tutti i servizi di Azure e dall'indirizzo IP configurato.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-105">Once the script has been successfully run, the PostgreSQL server can be accessed from all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b9fb5-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="b9fb5-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="b9fb5-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b9fb5-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="b9fb5-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="b9fb5-109">Sample script</span></span>
<span data-ttu-id="b9fb5-110">In questo script di esempio modificare le righe evidenziate per personalizzare il nome utente e la password dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="b9fb5-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Creare un database di Azure per PostgreSQL e regole del firewall di livello server.")]</span><span class="sxs-lookup"><span data-stu-id="b9fb5-111">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b9fb5-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b9fb5-112">Clean up deployment</span></span>
<span data-ttu-id="b9fb5-113">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="b9fb5-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Eliminare il gruppo di risorse.")]</span><span class="sxs-lookup"><span data-stu-id="b9fb5-114">[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="b9fb5-115">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="b9fb5-115">Script explanation</span></span>
<span data-ttu-id="b9fb5-116">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-116">This script uses the following commands.</span></span> <span data-ttu-id="b9fb5-117">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b9fb5-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="b9fb5-118">**Command**</span></span> | <span data-ttu-id="b9fb5-119">**Note**</span><span class="sxs-lookup"><span data-stu-id="b9fb5-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="b9fb5-120">az group create</span><span class="sxs-lookup"><span data-stu-id="b9fb5-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="b9fb5-121">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b9fb5-122">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="b9fb5-122">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="b9fb5-123">Crea un server PostgreSQL che ospita i database.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-123">Creates a PostgreSQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="b9fb5-124">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="b9fb5-124">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="b9fb5-125">Crea una regola di firewall per consentire l'accesso al server e ai database presenti sul server dall'intervallo di indirizzi IP immesso.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="b9fb5-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="b9fb5-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="b9fb5-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="b9fb5-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b9fb5-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b9fb5-128">Next steps</span></span>
- <span data-ttu-id="b9fb5-129">Altre informazioni sull'interfaccia della riga di comando di Azure: [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="b9fb5-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="b9fb5-130">Provare a eseguire altri script: [Esempi dell'interfaccia della riga di comando di Azure per il database di Azure per PostgreSQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b9fb5-130">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
