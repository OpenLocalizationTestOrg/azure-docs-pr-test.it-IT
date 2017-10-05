---
title: Script dell'interfaccia della riga di comando di Azure - Creare un database di Azure per MySQL | Microsoft Docs
description: Questo script dell'interfaccia della riga di comando di Azure di esempio crea un singolo database di Azure per il server MySQL e configura una regola di firewall a livello di server.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.custom: mvc
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: 201db294ce362ef3e09cbe62f48bd51c8ea94dbb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-mysql-server-and-configure-a-firewall-rule-using-the-azure-cli"></a><span data-ttu-id="65397-103">Creare un server MySQL e configurare una regola di firewall tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="65397-103">Create a MySQL server and configure a firewall rule using the Azure CLI</span></span>
<span data-ttu-id="65397-104">Questo script dell'interfaccia della riga di comando di Azure di esempio crea un singolo database di Azure per il server MySQL e configura una regola di firewall a livello di server.</span><span class="sxs-lookup"><span data-stu-id="65397-104">This sample CLI script creates an Azure Database for MySQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="65397-105">Una volta che lo script è stato eseguito correttamente, il server MySQL è accessibile da tutti i servizi di Azure e dall'indirizzo IP configurato.</span><span class="sxs-lookup"><span data-stu-id="65397-105">Once the script runs successfully, the MySQL server is accessible by all Azure services and the configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="65397-106">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="65397-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="65397-107">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="65397-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="65397-108">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="65397-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="65397-109">Script di esempio</span><span class="sxs-lookup"><span data-stu-id="65397-109">Sample script</span></span>
<span data-ttu-id="65397-110">In questo script di esempio modificare le righe evidenziate per personalizzare il nome utente e la password dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="65397-110">In this sample script, edit the highlighted lines to customize the admin username and password.</span></span>
<span data-ttu-id="65397-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Creare un database di Azure per MySQL e regole del firewall di livello server.")]</span><span class="sxs-lookup"><span data-stu-id="65397-111">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/create-mysql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for MySQL, and server-level firewall rule.")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="65397-112">Pulire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="65397-112">Clean up deployment</span></span>
<span data-ttu-id="65397-113">Dopo l'esecuzione dello script di esempio, è possibile usare il comando seguente per rimuovere il gruppo di risorse e tutte le risorse ad esso associate.</span><span class="sxs-lookup"><span data-stu-id="65397-113">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>
<span data-ttu-id="65397-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Eliminare il gruppo di risorse.")]</span><span class="sxs-lookup"><span data-stu-id="65397-114">[!code-azurecli-interactive[main](../../../cli_scripts/mysql/create-mysql-server-and-firewall-rule/delete-mysql.sh "Delete the resource group.")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="65397-115">Spiegazione dello script</span><span class="sxs-lookup"><span data-stu-id="65397-115">Script explanation</span></span>
<span data-ttu-id="65397-116">Questo script usa i comandi seguenti.</span><span class="sxs-lookup"><span data-stu-id="65397-116">This script uses the following commands.</span></span> <span data-ttu-id="65397-117">Ogni comando della tabella include collegamenti alla documentazione specifica del comando.</span><span class="sxs-lookup"><span data-stu-id="65397-117">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="65397-118">**Comando**</span><span class="sxs-lookup"><span data-stu-id="65397-118">**Command**</span></span> | <span data-ttu-id="65397-119">**Note**</span><span class="sxs-lookup"><span data-stu-id="65397-119">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="65397-120">az group create</span><span class="sxs-lookup"><span data-stu-id="65397-120">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="65397-121">Consente di creare un gruppo di risorse in cui sono archiviate tutte le risorse.</span><span class="sxs-lookup"><span data-stu-id="65397-121">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="65397-122">az mysql server create</span><span class="sxs-lookup"><span data-stu-id="65397-122">az mysql server create</span></span>](/cli/azure/mysql/server#create) | <span data-ttu-id="65397-123">Crea un server MySQL che ospita i database.</span><span class="sxs-lookup"><span data-stu-id="65397-123">Creates a MySQL server that hosts the databases.</span></span> |
| [<span data-ttu-id="65397-124">az mysql server firewall create</span><span class="sxs-lookup"><span data-stu-id="65397-124">az mysql server firewall create</span></span>](/cli/azure/mysql/server/firewall-rule#create) | <span data-ttu-id="65397-125">Crea una regola di firewall per consentire l'accesso al server e ai database presenti sul server dall'intervallo di indirizzi IP immesso.</span><span class="sxs-lookup"><span data-stu-id="65397-125">Creates a firewall rule to allow access to the server and databases under it from the entered IP address range.</span></span> |
| [<span data-ttu-id="65397-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="65397-126">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="65397-127">Consente di eliminare un gruppo di risorse incluse tutte le risorse annidate.</span><span class="sxs-lookup"><span data-stu-id="65397-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="65397-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="65397-128">Next steps</span></span>
- <span data-ttu-id="65397-129">Altre informazioni sull'interfaccia della riga di comando di Azure: [documentazione sull'interfaccia della riga di comando di Azure](/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="65397-129">Read more information on the Azure CLI: [Azure CLI documentation](/cli/azure/overview).</span></span>
- <span data-ttu-id="65397-130">Provare a eseguire altri script: [Esempi dell'interfaccia della riga di comando di Azure per il database di Azure per MySQL](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="65397-130">Try additional scripts: [Azure CLI samples for Azure Database for MySQL](../sample-scripts-azure-cli.md)</span></span>
