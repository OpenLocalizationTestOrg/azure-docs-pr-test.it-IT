---
title: Come un Server di Database di Azure per PostgreSQL tooRestore | Documenti Microsoft
description: Questo articolo viene descritto come un server di Database di Azure per l'utilizzo di PostgreSQL toorestore hello portale di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: bc7351f384607397806d837afd3e1d7a26575e0e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobackup-and-restore-a-server-in-azure-database-for-postgresql-using-hello-azure-portal"></a><span data-ttu-id="9abb4-103">Come tooBackup e il ripristino di un server di Database di Azure per l'utilizzo di PostgreSQL hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="9abb4-103">How tooBackup and Restore a server in Azure Database for PostgreSQL using hello Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="9abb4-104">Il backup viene eseguito automaticamente</span><span class="sxs-lookup"><span data-stu-id="9abb4-104">Backup happens Automatically</span></span>
<span data-ttu-id="9abb4-105">Quando si utilizza il Database di Azure per PostgreSQL, il servizio di database hello rende automaticamente un backup del servizio hello ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="9abb4-105">When using Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="9abb4-106">Quando si utilizza il livello di base e 35 giorni, sono disponibili per 7 giorni backup di Hello quando si usa il livello Standard.</span><span class="sxs-lookup"><span data-stu-id="9abb4-106">hello backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="9abb4-107">Per altre informazioni, vedere [Livelli di servizio del Database di Azure per PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="9abb4-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="9abb4-108">Utilizzare questa funzionalità di backup automatico è possibile ripristinare server hello e tutti i database in un nuovo server tooan precedente punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="9abb4-108">Using this automatic backup feature you may restore hello server and all its databases into a new server tooan earlier point-in-time.</span></span>

## <a name="restore-in-hello-azure-portal"></a><span data-ttu-id="9abb4-109">Ripristinare nel portale di Azure hello</span><span class="sxs-lookup"><span data-stu-id="9abb4-109">Restore in hello Azure portal</span></span>
<span data-ttu-id="9abb4-110">Il Database di Azure per PostgreSQL consente toorestore hello server back-tooa punto nel tempo e in tooa nuova copia del server di hello.</span><span class="sxs-lookup"><span data-stu-id="9abb4-110">Azure Database for PostgreSQL allows you toorestore hello server back tooa point in time and into tooa new copy of hello server.</span></span> <span data-ttu-id="9abb4-111">È possibile utilizzare questo nuovo toorecover server i dati.</span><span class="sxs-lookup"><span data-stu-id="9abb4-111">You can use this new server toorecover your data.</span></span> 

<span data-ttu-id="9abb4-112">Ad esempio, se una tabella è stato accidentalmente eliminato a mezzogiorno oggi, si potrebbe ripristinare toohello ora prima di mezzogiorno e recuperare hello mancante nella tabella e i dati dalla nuova copia del server di hello.</span><span class="sxs-lookup"><span data-stu-id="9abb4-112">For example, if a table was accidentally dropped at noon today, you could restore toohello time just before noon and retrieve hello missing table and data from that new copy of hello server.</span></span>

<span data-ttu-id="9abb4-113">Hello seguenti passaggi punto di ripristino hello esempio server tooa nel tempo:</span><span class="sxs-lookup"><span data-stu-id="9abb4-113">hello following steps restore hello sample server tooa point in time:</span></span>
1. <span data-ttu-id="9abb4-114">Sign in hello [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="9abb4-114">Sign into hello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="9abb4-115">Individuare il Database di Azure per il server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="9abb4-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="9abb4-116">Nel portale di Azure hello, fare clic su **tutte le risorse** dal menu a sinistra hello e digitare il nome di hello, ad esempio **mypgserver 20170401**, toosearch per il server esistente.</span><span class="sxs-lookup"><span data-stu-id="9abb4-116">In hello Azure portal, click **All Resources** from hello left-hand menu and type in hello name, such as **mypgserver-20170401**, toosearch for your existing server.</span></span> <span data-ttu-id="9abb4-117">Fare clic su un nome server hello elencato nei risultati di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="9abb4-117">Click hello server name listed in hello search result.</span></span> <span data-ttu-id="9abb4-118">Hello **Panoramica** pagina per il server viene aperto e offre opzioni per un'ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="9abb4-118">hello **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portale di Azure - il server di ricerca toolocate](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="9abb4-120">Nella parte superiore di hello del pannello della panoramica hello server, fare clic su **ripristinare** sulla barra degli strumenti hello.</span><span class="sxs-lookup"><span data-stu-id="9abb4-120">On hello top of hello server overview blade, click **Restore** on hello toolbar.</span></span> <span data-ttu-id="9abb4-121">verrà visualizzata la finestra di pannello Ripristina Hello.</span><span class="sxs-lookup"><span data-stu-id="9abb4-121">hello Restore blade opens.</span></span>

   ![Database di Azure per PostgreSQL - Panoramica - Pulsante Ripristino](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="9abb4-123">Compilare il modulo ripristino hello con le informazioni necessarie hello:</span><span class="sxs-lookup"><span data-stu-id="9abb4-123">Fill out hello Restore form with hello required information:</span></span>

   ![<span data-ttu-id="9abb4-124">Database di Azure per PostgreSQL - Informazioni di ripristino</span><span class="sxs-lookup"><span data-stu-id="9abb4-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="9abb4-125">**Punto di ripristino**: selezionare un punto nel tempo che si verifica prima che il server di hello è stato modificato</span><span class="sxs-lookup"><span data-stu-id="9abb4-125">**Restore point**: Select a point-in-time that occurs before hello server was changed</span></span>
  - <span data-ttu-id="9abb4-126">**Server di destinazione**: fornire un nuovo nome del server desiderato toorestore per</span><span class="sxs-lookup"><span data-stu-id="9abb4-126">**Target server**: Provide a new server name you want toorestore to</span></span>
  - <span data-ttu-id="9abb4-127">**Percorso**: non è possibile selezionare l'area di hello, per impostazione predefinita è uguale al server di origine hello</span><span class="sxs-lookup"><span data-stu-id="9abb4-127">**Location**: You cannot select hello region, by default it is same as hello source server</span></span>
  - <span data-ttu-id="9abb4-128">**Piano tariffario**: non è possibile modificare questo valore quando si ripristina un server.</span><span class="sxs-lookup"><span data-stu-id="9abb4-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="9abb4-129">È uguale al server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="9abb4-129">It is same as hello source server.</span></span> 

5. <span data-ttu-id="9abb4-130">Fare clic su **OK** toorestore hello server toorestore tooa punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="9abb4-130">Click **OK** toorestore hello server toorestore tooa point in time.</span></span> 

6. <span data-ttu-id="9abb4-131">Al termine del ripristino di hello, individuare hello nuovo server in cui viene creato hello tooverify ripristino dei dati nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="9abb4-131">Once hello restore finishes, locate hello new server that is created tooverify hello data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9abb4-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9abb4-132">Next steps</span></span>
- [<span data-ttu-id="9abb4-133">Raccolte connessioni per il Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9abb4-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
