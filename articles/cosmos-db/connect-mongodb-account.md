---
title: stringa di connessione aaaMongoDB per un account Azure Cosmos DB | Documenti Microsoft
description: Informazioni su come tooconnect il tooan app MongoDB Azure Cosmos DB account utilizzando una stringa di connessione di MongoDB.
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="c29df-104">Connettersi a un tooAzure applicazione MongoDB Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c29df-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="c29df-105">Informazioni su come tooconnect il tooan app MongoDB Azure Cosmos DB account utilizzando una stringa di connessione di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c29df-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="c29df-106">È quindi possibile utilizzare un database di Azure Cosmos DB come dati hello archiviare per l'app di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c29df-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="c29df-107">In questa esercitazione fornisce due metodi tooretrieve informazioni della stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="c29df-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="c29df-108">[metodo di avvio rapido di Hello](#QuickstartConnection), per l'utilizzo con i driver .NET, Node.js, MongoDB Shell, Java e Python</span><span class="sxs-lookup"><span data-stu-id="c29df-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="c29df-109">[il metodo di stringhe di connessione personalizzata Hello](#GetCustomConnection), per l'uso con altri driver</span><span class="sxs-lookup"><span data-stu-id="c29df-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c29df-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c29df-110">Prerequisites</span></span>

- <span data-ttu-id="c29df-111">Un account Azure.</span><span class="sxs-lookup"><span data-stu-id="c29df-111">An Azure account.</span></span> <span data-ttu-id="c29df-112">Se non si ha un account Azure, creare un [account Azure gratuito](https://azure.microsoft.com/free/) ora.</span><span class="sxs-lookup"><span data-stu-id="c29df-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="c29df-113">Account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c29df-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="c29df-114">Per istruzioni, vedere [compilare un'app web API MongoDB con .NET e hello Azure portal](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c29df-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="c29df-115"><a id="QuickstartConnection"></a>Ottenere stringa di connessione hello MongoDB con avvio rapido hello</span><span class="sxs-lookup"><span data-stu-id="c29df-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="c29df-116">In un browser Internet, accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c29df-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c29df-117">In hello **Azure Cosmos DB** pannello selezionare hello API per conto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c29df-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="c29df-118">Nel riquadro di sinistra hello del Pannello di hello account, fare clic su **avvio rapido**.</span><span class="sxs-lookup"><span data-stu-id="c29df-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="c29df-119">Scegliere la piattaforma (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="c29df-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="c29df-120">Se il driver o lo strumento non compare nell'elenco, ricordare che altri frammenti di codice di connessione vengono continuamente documentati.</span><span class="sxs-lookup"><span data-stu-id="c29df-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="c29df-121">Commentare di seguito si desidera toosee.</span><span class="sxs-lookup"><span data-stu-id="c29df-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="c29df-122">toolearn modalità di lettura, la connessione di toocraft [ottenere informazioni sulla stringa di connessione dell'account hello](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="c29df-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="c29df-123">Copiare e incollare il frammento di codice hello app MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c29df-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Pannello di avvio rapido](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="c29df-125"><a id="GetCustomConnection"></a>Ottenere hello MongoDB connessione stringa toocustomize</span><span class="sxs-lookup"><span data-stu-id="c29df-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="c29df-126">In un browser Internet, accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c29df-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c29df-127">In hello **Azure Cosmos DB** pannello selezionare hello API per conto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c29df-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="c29df-128">Nel riquadro di sinistra hello del Pannello di hello account, fare clic su **stringa di connessione**.</span><span class="sxs-lookup"><span data-stu-id="c29df-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="c29df-129">Hello **stringa di connessione** apre blade.</span><span class="sxs-lookup"><span data-stu-id="c29df-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="c29df-130">Dispone di tutti i hello informazioni tooconnect necessarie toohello account utilizzando un driver per MongoDB, tra cui una stringa di connessione partendo.</span><span class="sxs-lookup"><span data-stu-id="c29df-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Pannello Stringa di connessione](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="c29df-132">Requisiti della stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="c29df-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="c29df-133">Azure Cosmos DB presenta standard e requisiti di sicurezza restrittivi.</span><span class="sxs-lookup"><span data-stu-id="c29df-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="c29df-134">Gli account Azure Cosmos DB richiedono l'autenticazione e la comunicazione sicura tramite *SSL*.</span><span class="sxs-lookup"><span data-stu-id="c29df-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="c29df-135">DB Cosmos Azure supporta hello standard MongoDB formato stringa di connessione URI, con un paio di requisiti specifici: account di Azure Cosmos DB richiedono l'autenticazione e comunicazioni protette tramite SSL.</span><span class="sxs-lookup"><span data-stu-id="c29df-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="c29df-136">In tal caso, è formato di stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="c29df-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="c29df-137">i valori Hello di questa stringa sono disponibili in hello **stringa di connessione** pannello illustrato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="c29df-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="c29df-138">Nome utente (obbligatorio): nome dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c29df-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="c29df-139">Password (obbligatorio): password dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c29df-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="c29df-140">Host (obbligatorio): nome di dominio completo di hello account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c29df-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="c29df-141">Porta (obbligatorio): 10255.</span><span class="sxs-lookup"><span data-stu-id="c29df-141">Port (required): 10255.</span></span>
* <span data-ttu-id="c29df-142">Database (facoltativo): utilizza database hello hello connessione.</span><span class="sxs-lookup"><span data-stu-id="c29df-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="c29df-143">Se viene specificato alcun database, database di hello predefinito è "test".</span><span class="sxs-lookup"><span data-stu-id="c29df-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="c29df-144">ssl=true (obbligatorio)</span><span class="sxs-lookup"><span data-stu-id="c29df-144">ssl=true (required)</span></span>

<span data-ttu-id="c29df-145">Si consideri ad esempio account hello nella hello **stringa di connessione** blade.</span><span class="sxs-lookup"><span data-stu-id="c29df-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="c29df-146">Una stringa di connessione valida è la seguente:</span><span class="sxs-lookup"><span data-stu-id="c29df-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="c29df-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c29df-147">Next steps</span></span>
* <span data-ttu-id="c29df-148">Informazioni su come troppo[utilizzare MongoChef](mongodb-mongochef.md) con un'API DB Cosmos di Azure per conto di MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c29df-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="c29df-149">Esplorare hello Azure Cosmos DB API per MongoDB visualizzando [esempi](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c29df-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
