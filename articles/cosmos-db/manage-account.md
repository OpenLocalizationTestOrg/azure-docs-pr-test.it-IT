---
title: Gestire un account Azure Cosmos DB con il portale di Azure | Microsoft Docs
description: Informazioni su come gestire il proprio account Azure Cosmos DB tramite il portale di Azure. Trovare una guida sull'uso del portale di Azure per visualizzare, copiare, eliminare e accedere agli account.
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
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="61d44-105">Come gestire un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61d44-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="61d44-106">Informazioni su come impostare la coerenza globale, usare le chiavi ed eliminare un account Azure Cosmos DB nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="61d44-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="61d44-107"><a id="consistency"></a>Gestire le impostazioni di coerenza di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61d44-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="61d44-108">La scelta del livello di coerenza giusto dipende dalla semantica dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="61d44-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="61d44-109">È consigliabile acquisire familiarità con i livelli di coerenza disponibili in Azure Cosmos DB leggendo [Uso dei livelli di coerenza per ottimizzare la disponibilità e le prestazioni di Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="61d44-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="61d44-110">Azure Cosmos DB offre garanzia su coerenza, disponibilità e prestazioni a ogni livello di coerenza disponibile per l'account di database.</span><span class="sxs-lookup"><span data-stu-id="61d44-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="61d44-111">La configurazione dell'account di database con un forte livello di coerenza richiede che i dati vengano limitati a una singola area di Azure, senza disponibilità globale.</span><span class="sxs-lookup"><span data-stu-id="61d44-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="61d44-112">D'altra parte, i livelli di coerenza ampi (obsolescenza associata, sessione o finale) consentono di associare tutte le aree di Azure desiderate con l'account di database.</span><span class="sxs-lookup"><span data-stu-id="61d44-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="61d44-113">La semplice procedura seguente mostra come selezionare il livello di coerenza predefinito per l'account di database.</span><span class="sxs-lookup"><span data-stu-id="61d44-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="61d44-114">Per specificare la coerenza predefinita per un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61d44-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="61d44-115">Nel [portale di Azure](https://portal.azure.com/) accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="61d44-116">Nel pannello dell'account fare clic su **Coerenza predefinita**.</span><span class="sxs-lookup"><span data-stu-id="61d44-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="61d44-117">Nel pannello **Default Consistency** (Uniformità predefinita) selezionare il nuovo livello di coerenza e fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="61d44-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="61d44-118">![Sessione Coerenza predefinita][5]</span><span class="sxs-lookup"><span data-stu-id="61d44-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="61d44-119"><a id="keys"></a>Visualizzare, copiare e rigenerare le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="61d44-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="61d44-120">Quando si crea un account Azure Cosmos DB, il servizio genera due chiavi di accesso principali che possono essere usate per l'autenticazione quando si accede all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="61d44-121">Generando due chiavi di accesso, Azure Cosmos DB consente di rigenerare le chiavi senza interruzioni dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="61d44-122">Nel [Portale di Azure](https://portal.azure.com/) accedere al pannello **Chiavi** dal menu delle risorse nel pannello **Account Azure Cosmos DB** per visualizzare, copiare e rigenerare le chiavi di accesso usate per accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Schermata del portale di Azure, pannello delle chiavi](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="61d44-124">Il pannello **Chiavi** include anche le stringhe di connessione primaria e secondaria che possono essere usate per connettersi al proprio account dall' [Utilità di migrazione dati](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="61d44-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="61d44-125">In questo pannello sono anche disponibili chiavi di sola lettura.</span><span class="sxs-lookup"><span data-stu-id="61d44-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="61d44-126">Lettura e query sono operazioni di sola lettura, a differenza di creazione, eliminazione e sostituzione.</span><span class="sxs-lookup"><span data-stu-id="61d44-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="61d44-127">Copiare una chiave di accesso nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="61d44-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="61d44-128">Nel pannello **Keys** (Chiavi) fare clic sul pulsante **Copy** (Copia) a destra della chiave da copiare.</span><span class="sxs-lookup"><span data-stu-id="61d44-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Visualizzare e copiare una chiave di accesso nel portale di Azure, pannello delle chiavi](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="61d44-130">Per rigenerare le chiavi di accesso</span><span class="sxs-lookup"><span data-stu-id="61d44-130">Regenerate access keys</span></span>
<span data-ttu-id="61d44-131">È consigliabile modificare periodicamente le chiavi di accesso all'account Azure Cosmos DB per mantenere più sicure le connessioni.</span><span class="sxs-lookup"><span data-stu-id="61d44-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="61d44-132">Vengono assegnate due chiavi di accesso per consentire di mantenere le connessioni all'account Azure Cosmos DB con una delle due chiavi mentre si rigenera l'altra.</span><span class="sxs-lookup"><span data-stu-id="61d44-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="61d44-133">La rigenerazione delle chiavi di accesso influisce su tutte le applicazioni che dipendono dalla chiave corrente.</span><span class="sxs-lookup"><span data-stu-id="61d44-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="61d44-134">Per usare la nuova chiave è necessario aggiornare tutti i client che usano la chiave di accesso per accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="61d44-135">Se si dispone di applicazioni o servizi cloud che usano l'account Azure Cosmos DB e si rigenerano le chiavi, si perderanno le connessioni, a meno che non si registrino le chiavi.</span><span class="sxs-lookup"><span data-stu-id="61d44-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="61d44-136">I passaggi seguenti illustrano il processo necessario per la registrazione delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="61d44-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="61d44-137">Aggiornare la chiave di accesso nel codice dell'applicazione in modo che faccia riferimento alla chiave di accesso secondaria dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="61d44-138">Rigenerare la chiave di accesso primaria per l'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="61d44-139">Nel [portale di Azure](https://portal.azure.com/) accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="61d44-140">Nel pannello **Account Azure Cosmos DB** fare clic su **Chiavi**.</span><span class="sxs-lookup"><span data-stu-id="61d44-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="61d44-141">Nel pannello **Keys** (Chiavi) fare clic sul comando per rigenerare e quindi su **OK** per confermare che si vuole generare una nuova chiave.</span><span class="sxs-lookup"><span data-stu-id="61d44-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="61d44-142">![Per rigenerare le chiavi di accesso](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="61d44-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="61d44-143">Dopo aver verificato che la nuova chiave sia disponibile per l'utilizzo (circa 5 minuti dopo la rigenerazione), aggiornare la chiave di accesso nel codice dell'applicazione in modo che faccia riferimento alla nuova chiave di accesso primaria.</span><span class="sxs-lookup"><span data-stu-id="61d44-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="61d44-144">Rigenerare la chiave di accesso secondaria.</span><span class="sxs-lookup"><span data-stu-id="61d44-144">Regenerate the secondary access key.</span></span>
   
    ![Per rigenerare le chiavi di accesso](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="61d44-146">Potrebbero trascorrere diversi minuti prima che una chiave appena generata possa essere usata per accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="61d44-147">Ottenere la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="61d44-147">Get the  connection string</span></span>
<span data-ttu-id="61d44-148">Per recuperare la stringa di connessione, eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="61d44-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="61d44-149">Nel [portale di Azure](https://portal.azure.com) accedere all'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="61d44-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="61d44-150">Nel menu delle risorse fare clic su **Keys** (Chiavi).</span><span class="sxs-lookup"><span data-stu-id="61d44-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="61d44-151">Fare clic sul pulsante **Copy** (Copia) accanto alla casella **Primary Connection String** (Stringa di connessione primaria) o **Secondary Connection String** (stringa di connessione secondaria).</span><span class="sxs-lookup"><span data-stu-id="61d44-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="61d44-152">Se si usa la stringa di connessione nello [strumento di migrazione del database di Azure Cosmos DB](import-data.md), aggiungere il nome del database alla fine della stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="61d44-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="61d44-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="61d44-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="61d44-154"><a id="delete"></a> Eliminare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="61d44-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="61d44-155">Per rimuovere un account Azure Cosmos DB non più usato dal portale di Azure, fare clic con il pulsante destro del mouse sul nome dell'account e quindi su **Elimina account**.</span><span class="sxs-lookup"><span data-stu-id="61d44-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Come eliminare un account Azure Cosmos DB nel portale di Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="61d44-157">Nel [portale di Azure](https://portal.azure.com/)accedere all'account Azure Cosmos DB che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="61d44-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="61d44-158">Nel pannello **Account Azure Cosmos DB** fare clic con il pulsante destro del mouse sull'account e quindi su **Elimina account**.</span><span class="sxs-lookup"><span data-stu-id="61d44-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="61d44-159">Nel pannello di conferma risultante digitare il nome dell'account Azure Cosmos DB per confermarne l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="61d44-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="61d44-160">Fare clic sul pulsante **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="61d44-160">Click the **Delete** button.</span></span>

![Come eliminare un account Azure Cosmos DB nel portale di Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="61d44-162"><a id="next"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="61d44-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="61d44-163">Informazioni su come [iniziare a usare l'account Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="61d44-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
