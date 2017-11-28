---
title: aaaHow tooRestore un Server di Database di Azure per MySQL | Documenti Microsoft
description: Questo articolo viene descritto come un server di Database di Azure per l'utilizzo di MySQL toorestore hello portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b990d5b37c5d4924de9571192b923e3c81094ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-mysql-using-hello-azure-portal"></a><span data-ttu-id="e626a-103">Come tooBackup e il ripristino di un server di Database di Azure per l'utilizzo di MySQL hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="e626a-103">How tooBackup and Restore a server in Azure Database for MySQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="e626a-104">Il backup viene eseguito automaticamente</span><span class="sxs-lookup"><span data-stu-id="e626a-104">Backup happens Automatically</span></span>
<span data-ttu-id="e626a-105">Quando si utilizza il Database di Azure per MySQL, il servizio di database hello rende automaticamente un backup del servizio hello ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="e626a-105">When using Azure Database for MySQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="e626a-106">Quando si utilizza il livello di base e 35 giorni, sono disponibili per 7 giorni backup di Hello quando si usa il livello Standard.</span><span class="sxs-lookup"><span data-stu-id="e626a-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="e626a-107">Per altre informazioni, vedere [Livelli di servizio del Database di Azure per MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="e626a-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="e626a-108">Utilizzare questa funzionalità di backup automatico è possibile ripristinare server hello e tutti i database in un nuovo server tooan precedente punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="e626a-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="e626a-109">Ripristinare nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="e626a-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="e626a-110">Il Database di Azure per MySQL consente toorestore hello server back-tooa punto nel tempo e in tooa nuova copia del server di hello.</span><span class="sxs-lookup"><span data-stu-id="e626a-110">Azure Database for MySQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="e626a-111">È possibile utilizzare questo nuovo toorecover server i dati.</span><span class="sxs-lookup"><span data-stu-id="e626a-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="e626a-112">Ad esempio, se una tabella è stato accidentalmente eliminato a mezzogiorno oggi, si potrebbe ripristinare toohello ora prima di mezzogiorno e recuperare hello mancante nella tabella e i dati dalla nuova copia del server di hello.</span><span class="sxs-lookup"><span data-stu-id="e626a-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="e626a-113">Hello seguenti passaggi punto di ripristino hello esempio server tooa nel tempo:</span><span class="sxs-lookup"><span data-stu-id="e626a-113">hello following steps restore hello sample server tooa point in time:</span></span>

1. <span data-ttu-id="e626a-114">Sign in hello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="e626a-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="e626a-115">Individuare il Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="e626a-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="e626a-116">Nel riquadro sinistro hello selezionare **tutte le risorse**, quindi selezionare il server dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="e626a-116">In hello left pane, select **All resources**, then select your server from hello list.</span></span>

3.  <span data-ttu-id="e626a-117">Nella parte superiore di hello del pannello della panoramica hello server, fare clic su **ripristinare** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="e626a-117">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="e626a-118">verrà visualizzata la finestra di pannello Ripristina Hello.</span><span class="sxs-lookup"><span data-stu-id="e626a-118">hello Restore blade opens.</span></span>
<span data-ttu-id="e626a-119">![fare clic sul pulsante Ripristina](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="e626a-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="e626a-120">Compilare il modulo ripristino hello con le informazioni necessarie hello:</span><span class="sxs-lookup"><span data-stu-id="e626a-120">Fill out hello Restore form with hello required information:</span></span>

- <span data-ttu-id="e626a-121">**(UTC) punto di ripristino**: utilizzando selezione data hello e selezione ora, selezionare toorestore un punto nel tempo per.</span><span class="sxs-lookup"><span data-stu-id="e626a-121">**Restore point (UTC)**: Using hello Date picker and time picker, select a point-in-time toorestore to.</span></span> <span data-ttu-id="e626a-122">tempo Hello specificato è in formato UTC, pertanto è possibile sia necessario tooconvert hello locale ora in formato UTC.</span><span class="sxs-lookup"><span data-stu-id="e626a-122">hello time specified is in UTC format, so you likely need tooconvert hello local time into UTC.</span></span>
- <span data-ttu-id="e626a-123">**Ripristinare il server toonew**: fornire un nuovo server di server esistente nome toorestore hello in.</span><span class="sxs-lookup"><span data-stu-id="e626a-123">**Restore toonew server**: Provide a new server name toorestore hello existing server into.</span></span>
- <span data-ttu-id="e626a-124">**Percorso**: hello area scelta automaticamente compilata con l'area del server di origine hello e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="e626a-124">**Location**: hello region choice automatically populates with hello source server region, and cannot be changed.</span></span>
- <span data-ttu-id="e626a-125">**Livello di prezzo**: hello prezzi scelta livello automaticamente popola con hello prezzi stesso livello del server di origine hello e non possono essere modificate qui.</span><span class="sxs-lookup"><span data-stu-id="e626a-125">**Pricing tier**: hello pricing tier choice automatically populates with hello same pricing tier as hello source server, and cannot be changed here.</span></span> 
<span data-ttu-id="e626a-126">![Ripristino temporizzato](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="e626a-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="e626a-127">Fare clic su **OK** toorestore hello server toorestore tooa punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="e626a-127">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="e626a-128">Al termine del ripristino di hello, individuare hello nuovo server in cui è stato creato hello tooverify sono stati ripristinati i database, come previsto.</span><span class="sxs-lookup"><span data-stu-id="e626a-128">After hello restore finishes, locate hello new server that was created tooverify hello databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e626a-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e626a-129">Next steps</span></span>
- [<span data-ttu-id="e626a-130">Raccolte connessioni per il Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="e626a-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)