---
title: Come ripristinare un server nel Database di Azure per MySQL | Microsoft Docs
description: In questo articolo viene descritta la procedura per ripristinare un server nel Database di Azure per MySQL usando il portale di Azure.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 8c06dce534b628a602127fd02b152c8e04e02cc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-mysql-using-the-azure-portal"></a><span data-ttu-id="d392f-103">Come eseguire la procedura di backup e ripristino di un server nel Database di Azure per MySQL usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d392f-103">How To Backup and Restore a server in Azure Database for MySQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="d392f-104">Il backup viene eseguito automaticamente</span><span class="sxs-lookup"><span data-stu-id="d392f-104">Backup happens Automatically</span></span>
<span data-ttu-id="d392f-105">Quando si usa Database di Azure per MySQL, il servizio di database esegue automaticamente il backup del servizio ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="d392f-105">When using Azure Database for MySQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="d392f-106">La disponibilità dei backup è di 7 giorni per il livello Basic e 35 giorni per il livello Standard.</span><span class="sxs-lookup"><span data-stu-id="d392f-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="d392f-107">Per altre informazioni, vedere [Livelli di servizio del Database di Azure per MySQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="d392f-107">For more information, see [Azure Database for MySQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="d392f-108">L'uso di questa funzionalità di backup automatico permette di ripristinare il server e tutti i suoi database in un nuovo server a un precedente punto temporizzato.</span><span class="sxs-lookup"><span data-stu-id="d392f-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="d392f-109">Ripristino nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="d392f-109">Restore in the Azure portal</span></span>
<span data-ttu-id="d392f-110">Il Database di Azure per MySQL consente di ripristinare il server a un punto temporizzato e in una nuova copia del server.</span><span class="sxs-lookup"><span data-stu-id="d392f-110">Azure Database for MySQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="d392f-111">È possibile usare questo nuovo server per ripristinare i dati.</span><span class="sxs-lookup"><span data-stu-id="d392f-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="d392f-112">Ad esempio, se oggi una tabella è stata accidentalmente eliminata a mezzogiorno, è possibile eseguire il ripristino a un'ora prima di mezzogiorno per recuperare la tabella e i dati mancanti dalla nuova copia del server.</span><span class="sxs-lookup"><span data-stu-id="d392f-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="d392f-113">La procedura seguente consente di ripristinare il server di esempio ad un punto temporizzato.</span><span class="sxs-lookup"><span data-stu-id="d392f-113">The following steps restore the sample server to a point in time:</span></span>

1. <span data-ttu-id="d392f-114">Accedere al [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="d392f-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>

2. <span data-ttu-id="d392f-115">Individuare il Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="d392f-115">Locate your Azure Database for MySQL server.</span></span> <span data-ttu-id="d392f-116">Nel riquadro a sinistra selezionare **All resources** (Tutte le risorse) e il server dall'elenco.</span><span class="sxs-lookup"><span data-stu-id="d392f-116">In the left pane, select **All resources**, then select your server from the list.</span></span>

3.  <span data-ttu-id="d392f-117">Nella parte superiore del pannello Panoramica server, fare clic su **Ripristina** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="d392f-117">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="d392f-118">Viene aperto il pannello Ripristina.</span><span class="sxs-lookup"><span data-stu-id="d392f-118">The Restore blade opens.</span></span>
<span data-ttu-id="d392f-119">![fare clic sul pulsante Ripristina](./media/howto-restore-server-portal/click-restore-button.png)</span><span class="sxs-lookup"><span data-stu-id="d392f-119">![click restore button](./media/howto-restore-server-portal/click-restore-button.png)</span></span>

4. <span data-ttu-id="d392f-120">Compilare il modulo Ripristina con le informazioni obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="d392f-120">Fill out the Restore form with the required information:</span></span>

- <span data-ttu-id="d392f-121">**Punto di ripristino (UTC)**: usando i controlli Selezione data e Selezione ora, scegliere un punto di ripristino temporizzato.</span><span class="sxs-lookup"><span data-stu-id="d392f-121">**Restore point (UTC)**: Using the Date picker and time picker, select a point-in-time to restore to.</span></span> <span data-ttu-id="d392f-122">L'ora specificata è nel formato UTC, pertanto è probabile che si debba convertire l'ora locale in UTC.</span><span class="sxs-lookup"><span data-stu-id="d392f-122">The time specified is in UTC format, so you likely need to convert the local time into UTC.</span></span>
- <span data-ttu-id="d392f-123">**Ripristina al nuovo server**: specificare il nome del nuovo server in cui ripristinare il server esistente.</span><span class="sxs-lookup"><span data-stu-id="d392f-123">**Restore to new server**: Provide a new server name to restore the existing server into.</span></span>
- <span data-ttu-id="d392f-124">**Percorso**: la scelta dell'area viene effettuata automaticamente ricalcando l'area del server di origine e non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="d392f-124">**Location**: The region choice automatically populates with the source server region, and cannot be changed.</span></span>
- <span data-ttu-id="d392f-125">**Piano tariffario**: la scelta del piano tariffario viene effettuata automaticamente con lo stesso livello di prezzo del server di origine e non può essere modificata qui.</span><span class="sxs-lookup"><span data-stu-id="d392f-125">**Pricing tier**: The pricing tier choice automatically populates with the same pricing tier as the source server, and cannot be changed here.</span></span> 
<span data-ttu-id="d392f-126">![Ripristino temporizzato](./media/howto-restore-server-portal/pitr-restore.png)</span><span class="sxs-lookup"><span data-stu-id="d392f-126">![PITR Restore](./media/howto-restore-server-portal/pitr-restore.png)</span></span>

5. <span data-ttu-id="d392f-127">Fare clic su **OK** per ripristinare il server al punto di ripristino temporizzato.</span><span class="sxs-lookup"><span data-stu-id="d392f-127">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="d392f-128">Al termine del ripristino, individuare il nuovo server creato per verificare che il ripristino dei database sia avvenuto come previsto.</span><span class="sxs-lookup"><span data-stu-id="d392f-128">After the restore finishes, locate the new server that was created to verify the databases were restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d392f-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d392f-129">Next steps</span></span>
- [<span data-ttu-id="d392f-130">Raccolte connessioni per il Database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="d392f-130">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)