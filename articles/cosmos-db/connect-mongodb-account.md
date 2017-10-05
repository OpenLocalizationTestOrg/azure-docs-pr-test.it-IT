---
title: Stringa di connessione MongoDB per un account Azure Cosmos DB | Microsoft Docs
description: Informazioni su come connettere l'app MongoDB a un account Azure Cosmos DB usando una stringa di connessione MongoDB.
keywords: stringa di connessione mongodb
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="d6299-104">Connettere un'applicazione MongoDB ad Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="d6299-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="d6299-105">Informazioni su come connettere l'app MongoDB a un account Azure Cosmos DB usando una stringa di connessione MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6299-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="d6299-106">È quindi possibile usare un database di Azure Cosmos DB come archivio dati per l'app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6299-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="d6299-107">Questa esercitazione illustra due modi per recuperare le informazioni della stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="d6299-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="d6299-108">[Metodo di avvio rapido](#QuickstartConnection), per l'uso con i driver .NET, Node.js, MongoDB Shell, Java e Python</span><span class="sxs-lookup"><span data-stu-id="d6299-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="d6299-109">[Metodo basato su stringa di connessione personalizzata](#GetCustomConnection), da usare con altri driver</span><span class="sxs-lookup"><span data-stu-id="d6299-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6299-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d6299-110">Prerequisites</span></span>

- <span data-ttu-id="d6299-111">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="d6299-111">An Azure account.</span></span> <span data-ttu-id="d6299-112">Se non si ha un account Azure, creare un [account Azure gratuito](https://azure.microsoft.com/free/) ora.</span><span class="sxs-lookup"><span data-stu-id="d6299-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="d6299-113">Account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6299-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="d6299-114">Per istruzioni, vedere [Creare un'app Web API MongoDB con .NET e il portale di Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d6299-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="d6299-115"><a id="QuickstartConnection"></a>Ottenere la stringa di connessione MongoDB usando il metodo di avvio rapido</span><span class="sxs-lookup"><span data-stu-id="d6299-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="d6299-116">In un browser Internet accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6299-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6299-117">Nel pannello **Azure Cosmos DB** selezionare l'API per l'account MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6299-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="d6299-118">Nel riquadro sinistro del pannello dell'account fare clic su **Avvio rapido**.</span><span class="sxs-lookup"><span data-stu-id="d6299-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="d6299-119">Scegliere la piattaforma (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="d6299-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="d6299-120">Se il driver o lo strumento non compare nell'elenco, ricordare che altri frammenti di codice di connessione vengono continuamente documentati.</span><span class="sxs-lookup"><span data-stu-id="d6299-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="d6299-121">Commentare di seguito ciò che si vorrebbe vedere.</span><span class="sxs-lookup"><span data-stu-id="d6299-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="d6299-122">Per informazioni su come realizzare la propria connessione, leggere [Ottenere informazioni sulla stringa di connessione dell'account](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="d6299-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="d6299-123">Copiare e incollare il frammento di codice nell'app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6299-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Pannello di avvio rapido](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="d6299-125"><a id="GetCustomConnection"></a> Ottenere la stringa di connessione MongoDB da personalizzare</span><span class="sxs-lookup"><span data-stu-id="d6299-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="d6299-126">In un browser Internet accedere al [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="d6299-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="d6299-127">Nel pannello **Azure Cosmos DB** selezionare l'API per l'account MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6299-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="d6299-128">Nel riquadro sinistro del pannello dell'account, fare clic su **Stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="d6299-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="d6299-129">Viene aperto il pannello **Stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="d6299-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="d6299-130">Contiene tutte le informazioni necessarie per connettersi all'account usando un driver per MongoDB, inclusa una stringa di connessione precostruita.</span><span class="sxs-lookup"><span data-stu-id="d6299-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Pannello Stringa di connessione](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="d6299-132">Requisiti della stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="d6299-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="d6299-133">Azure Cosmos DB presenta standard e requisiti di sicurezza restrittivi.</span><span class="sxs-lookup"><span data-stu-id="d6299-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="d6299-134">Gli account Azure Cosmos DB richiedono l'autenticazione e la comunicazione sicura tramite *SSL*.</span><span class="sxs-lookup"><span data-stu-id="d6299-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="d6299-135">Azure Cosmos DB supporta il formato URI della stringa di connessione di MongoDB standard, con un paio di requisiti specifici: gli account Azure Cosmos DB richiedono l'autenticazione e la comunicazione sicura tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="d6299-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="d6299-136">Il formato della stringa di connessione sarà quindi:</span><span class="sxs-lookup"><span data-stu-id="d6299-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="d6299-137">I valori di questa stringa sono disponibili nel pannello **Stringa di connessione** mostrato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="d6299-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="d6299-138">Nome utente (obbligatorio): nome dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6299-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="d6299-139">Password (obbligatorio): password dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6299-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="d6299-140">Host (obbligatorio): nome di dominio completo dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="d6299-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="d6299-141">Porta (obbligatorio): 10255.</span><span class="sxs-lookup"><span data-stu-id="d6299-141">Port (required): 10255.</span></span>
* <span data-ttu-id="d6299-142">Database (facoltativo): il database utilizzato dalla connessione.</span><span class="sxs-lookup"><span data-stu-id="d6299-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="d6299-143">Se viene specificato alcun database, il database predefinito è "test".</span><span class="sxs-lookup"><span data-stu-id="d6299-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="d6299-144">ssl=true (obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="d6299-144">ssl=true (required)</span></span>

<span data-ttu-id="d6299-145">Si consideri l'account mostrato nel pannello **Stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="d6299-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="d6299-146">Una stringa di connessione valida è la seguente:</span><span class="sxs-lookup"><span data-stu-id="d6299-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="d6299-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d6299-147">Next steps</span></span>
* <span data-ttu-id="d6299-148">Informazioni su come [utilizzare MongoChef](mongodb-mongochef.md) con un'API di Azure Cosmos DB per l'account MongoDB.</span><span class="sxs-lookup"><span data-stu-id="d6299-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="d6299-149">Esaminare l'API di Azure Cosmos DB per MongoDB visualizzando gli [esempi](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d6299-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
