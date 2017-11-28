---
title: un account Azure Cosmos DB tramite il portale di Azure hello aaaManage | Documenti Microsoft
description: Informazioni su come toomanage account del database di Azure Cosmos tramite hello portale di Azure. Trovare una Guida sull'uso di hello Azure Portal tooview, copia, gli account di accesso e di eliminazione.
keywords: Portale di Azure, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="5fe30-105">Come un account Azure Cosmos DB toomanage</span><span class="sxs-lookup"><span data-stu-id="5fe30-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="5fe30-106">Informazioni su come tooset coerenza globale, utilizzare chiavi ed eliminare un account Azure Cosmos DB hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5fe30-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="5fe30-107"><a id="consistency"></a>Gestire le impostazioni di coerenza di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5fe30-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="5fe30-108">Selezionare il livello di coerenza destra hello dipende dalla semantica hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="5fe30-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="5fe30-109">È consigliabile acquisire familiarità con livelli di coerenza disponibili hello in Azure Cosmos DB leggendo [con coerenza livelli toomaximize disponibilità e le prestazioni nel database di Azure Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="5fe30-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="5fe30-110">Azure Cosmos DB offre garanzia su coerenza, disponibilità e prestazioni a ogni livello di coerenza disponibile per l'account di database.</span><span class="sxs-lookup"><span data-stu-id="5fe30-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="5fe30-111">La configurazione dell'account del database con un livello di coerenza di sicuro richiede che i dati siano tooa ristretto singola regione di Azure e non è disponibile a livello globale.</span><span class="sxs-lookup"><span data-stu-id="5fe30-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="5fe30-112">In hello invece, i livelli di coerenza relaxed - con obsolescenza associata, sessione o eventuale abilitazione hello tooassociate è un numero qualsiasi di aree di Azure con l'account di database.</span><span class="sxs-lookup"><span data-stu-id="5fe30-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="5fe30-113">Hello semplici passaggi Mostra come tooselect hello a livello di coerenza predefinita per l'account di database.</span><span class="sxs-lookup"><span data-stu-id="5fe30-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="5fe30-114">coerenza di toospecify hello predefinito per un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5fe30-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="5fe30-115">In hello [portale di Azure](https://portal.azure.com/), accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="5fe30-116">Nel Pannello di hello account, fare clic su **predefinito coerenza**.</span><span class="sxs-lookup"><span data-stu-id="5fe30-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="5fe30-117">In hello **uniformità predefinita** pannello, il nuovo livello di coerenza selezionare hello e fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="5fe30-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="5fe30-118">![Sessione coerenza predefinita][5]</span><span class="sxs-lookup"><span data-stu-id="5fe30-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="5fe30-119"><a id="keys"></a>Visualizzare, copiare e rigenerare le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="5fe30-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="5fe30-120">Quando si crea un account Azure Cosmos DB, il servizio di hello genera due chiavi di accesso generale che possono essere utilizzate per l'autenticazione quando si accede a hello account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="5fe30-121">Fornendo due chiavi di accesso, Azure Cosmos DB consente chiavi hello tooregenerate con nessun tooyour interruzione account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="5fe30-122">In hello [portale di Azure](https://portal.azure.com/), hello accesso **chiavi** blade dal menu di risorsa hello hello **account Azure Cosmos DB** tooview pannello, copia e hello Rigenera chiavi di accesso sono tooaccess utilizzato l'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Schermata del portale di Azure, pannello delle chiavi](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="5fe30-124">Hello **chiavi** pannello include anche primaria e le stringhe di connessione secondaria che possono essere utilizzati tooconnect tooyour account da hello [utilità di migrazione dati](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="5fe30-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="5fe30-125">In questo pannello sono anche disponibili chiavi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="5fe30-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="5fe30-126">Lettura e query sono operazioni di sola lettura, a differenza di creazione, eliminazione e sostituzione.</span><span class="sxs-lookup"><span data-stu-id="5fe30-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="5fe30-127">Copiare la chiave di accesso nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="5fe30-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="5fe30-128">In hello **chiavi** pannello, fare clic su hello **copia** toohello pulsante a destra della chiave di hello desiderato toocopy.</span><span class="sxs-lookup"><span data-stu-id="5fe30-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Visualizzare e copiare la chiave di accesso nel portale di Azure, pannello chiavi hello](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="5fe30-130">Per rigenerare le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="5fe30-130">Regenerate access keys</span></span>
<span data-ttu-id="5fe30-131">È necessario impostare account di Azure Cosmos DB tooyour di hello accesso chiavi periodicamente toohelp rendere più sicuro le connessioni.</span><span class="sxs-lookup"><span data-stu-id="5fe30-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="5fe30-132">Due chiavi di accesso assegnate tooenable si toomaintain connessioni toohello account Azure Cosmos DB usando una chiave di accesso, mentre si rigenera hello altre chiavi di accesso.</span><span class="sxs-lookup"><span data-stu-id="5fe30-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="5fe30-133">Rigenerare le chiavi di accesso, influisce su tutte le applicazioni che dipendono dalla chiave corrente hello.</span><span class="sxs-lookup"><span data-stu-id="5fe30-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="5fe30-134">Tutti i client che utilizzano hello accesso tooaccess chiave hello Azure Cosmos DB account devono essere una nuova chiave di hello toouse aggiornato.</span><span class="sxs-lookup"><span data-stu-id="5fe30-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="5fe30-135">Se si dispone di applicazioni o servizi cloud tramite hello Azure Cosmos DB account, si perderanno le connessioni hello se si rigenerano le chiavi, a meno che non si esegue il rollback delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="5fe30-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="5fe30-136">Hello passaggi seguenti delineano il processo di hello coinvolto nella sequenza delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="5fe30-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="5fe30-137">Aggiornare la chiave di accesso hello la chiave di accesso secondaria applicazione codice tooreference hello di hello account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="5fe30-138">Rigenerare la chiave di accesso primaria hello per l'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="5fe30-139">In hello [portale Azure](https://portal.azure.com/), accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="5fe30-140">In hello **Azure Cosmos DB Account** pannello, fare clic su **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="5fe30-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="5fe30-141">In hello **chiavi** pannello, fare clic sul pulsante rigenerare hello, quindi fare clic su **Ok** tooconfirm che si desidera toogenerate una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="5fe30-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="5fe30-142">![Per rigenerare le chiavi di accesso](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="5fe30-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="5fe30-143">Dopo avere verificato la nuova chiave hello è disponibile per l'utilizzo (circa 5 minuti dopo la rigenerazione), aggiornare la chiave di accesso hello nell'applicazione codice tooreference hello nuova chiave di accesso primaria.</span><span class="sxs-lookup"><span data-stu-id="5fe30-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="5fe30-144">Rigenerare la chiave di accesso secondaria hello.</span><span class="sxs-lookup"><span data-stu-id="5fe30-144">Regenerate hello secondary access key.</span></span>
   
    ![Per rigenerare le chiavi di accesso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="5fe30-146">Può richiedere alcuni minuti prima che una chiave appena generata può essere utilizzato tooaccess l'account di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="5fe30-147">Ottiene la stringa di connessione hello</span><span class="sxs-lookup"><span data-stu-id="5fe30-147">Get hello  connection string</span></span>
<span data-ttu-id="5fe30-148">tooretrieve la connessione di stringa, hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="5fe30-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="5fe30-149">In hello [portale di Azure](https://portal.azure.com), accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="5fe30-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="5fe30-150">Scegliere dal menu risorse hello **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="5fe30-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="5fe30-151">Fare clic su hello **copia** pulsante Avanti toohello **stringa di connessione primaria** o **stringa di connessione secondaria** casella.</span><span class="sxs-lookup"><span data-stu-id="5fe30-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="5fe30-152">Se si utilizza la stringa di connessione hello in hello [strumento di migrazione di Database di Azure Cosmos DB](import-data.md), accodare end toohello nome del database hello hello della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="5fe30-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="5fe30-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="5fe30-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="5fe30-154"><a id="delete"></a> Eliminare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="5fe30-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="5fe30-155">un database di Azure Cosmos tooremove account dal portale di Azure non è più in uso, nome dell'account hello pulsante destro del mouse, hello e fare clic su **eliminare account**.</span><span class="sxs-lookup"><span data-stu-id="5fe30-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Come account di un database di Azure Cosmos toodelete in hello portale di Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="5fe30-157">In hello [portale di Azure](https://portal.azure.com/), hello Azure Cosmos DB quale account toodelete di accesso.</span><span class="sxs-lookup"><span data-stu-id="5fe30-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="5fe30-158">In hello **account Azure Cosmos DB** pannello, fare doppio clic su account hello e quindi fare clic su **Elimina Account**.</span><span class="sxs-lookup"><span data-stu-id="5fe30-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="5fe30-159">Nel Pannello di conferma risultante hello, digitare il nome account di hello Azure Cosmos DB tooconfirm che si desidera account hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="5fe30-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="5fe30-160">Fare clic su hello **eliminare** pulsante.</span><span class="sxs-lookup"><span data-stu-id="5fe30-160">Click hello **Delete** button.</span></span>

![Come account di un database di Azure Cosmos toodelete in hello portale di Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="5fe30-162"><a id="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5fe30-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="5fe30-163">Informazioni su come troppo[iniziare con il proprio account Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="5fe30-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
