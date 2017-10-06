---
title: aaaUse Robomongo per Azure Cosmos DB | Documenti Microsoft
description: 'Informazioni su come toouse Robomongo con un database di Azure Cosmos: API per conto di MongoDB'
keywords: robomongo
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="e0ecb-104">Usare Robomongo con un account Azure Cosmos DB: API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="e0ecb-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="e0ecb-105">tooconnect tooan DB Cosmos Azure: API per conto di MongoDB mediante Robomongo, è necessario:</span><span class="sxs-lookup"><span data-stu-id="e0ecb-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="e0ecb-106">Scaricare e installare [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="e0ecb-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="e0ecb-107">Verificare che siano disponibili le informazioni sulla [stringa di connessione](connect-mongodb-account.md) dell'account Azure Cosmos DB: API per MongoDB</span><span class="sxs-lookup"><span data-stu-id="e0ecb-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="e0ecb-108">Connettersi tramite Robomongo</span><span class="sxs-lookup"><span data-stu-id="e0ecb-108">Connect using Robomongo</span></span>
<span data-ttu-id="e0ecb-109">tooadd del database di Azure Cosmos: API per conto di MongoDB toohello Robomongo MongoDB connessioni, eseguire hello alla procedura seguente.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="e0ecb-110">Recuperare il database di Azure Cosmos: API MongoDB account informazioni di connessione utilizzando le istruzioni di hello [qui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="e0ecb-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Cattura di schermata del pannello stringa di connessione hello](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="e0ecb-112">Eseguire *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="e0ecb-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="e0ecb-113">Fare clic sul pulsante di connessione hello in **File** toomanage le connessioni.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="e0ecb-114">Quindi, fare clic su **crea** in hello **connessioni MongoDB** finestra verrà aperta hello **le impostazioni di connessione** finestra.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="e0ecb-115">In hello **le impostazioni di connessione** finestra, scegliere un nome.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="e0ecb-116">Quindi, individuare hello **Host** e **porta** da informazioni di connessione nel passaggio 1 e immetterli in **indirizzo** e **porta**rispettivamente .</span><span class="sxs-lookup"><span data-stu-id="e0ecb-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Cattura di schermata di hello Robomongo Gestisci connessioni](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="e0ecb-118">In hello **autenticazione** scheda, fare clic su **Esegui autenticazione**.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="e0ecb-119">Immettere il valore nel campo **User Name** (Nome utente) (il valore predefinito è *Admin*) e la **password**.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="e0ecb-120">I valori per i campi **User Name** (Nome utente) e **Password** possono essere trovati nelle informazioni di connessione nel Passaggio 1.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Cattura di schermata della scheda autenticazione Robomongo hello](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="e0ecb-122">In hello **SSL** scheda **protocollo Usa SSL**, quindi modificare hello **metodo di autenticazione** troppo**certificato autofirmato**.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Cattura di schermata della scheda SSL Robomongo hello](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="e0ecb-124">Infine, fare clic su **Test** tooverify che si è in grado di tooconnect, **salvare**.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0ecb-125">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e0ecb-125">Next steps</span></span>
* <span data-ttu-id="e0ecb-126">Esaminare gli [esempi](mongodb-samples.md) di Azure Cosmos DB: API per MongoDB.</span><span class="sxs-lookup"><span data-stu-id="e0ecb-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
