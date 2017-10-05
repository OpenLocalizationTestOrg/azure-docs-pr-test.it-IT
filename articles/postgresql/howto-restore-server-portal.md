---
title: Come ripristinare un server nel Database di Azure per PostgreSQL | Microsoft Docs
description: In questo articolo viene descritta la procedura per ripristinare un server nel Database di Azure per PostgreSQL usando il portale di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/20/2017
ms.openlocfilehash: 3fbdb7741481bd3620466c3489d3609f9ea6961f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-backup-and-restore-a-server-in-azure-database-for-postgresql-using-the-azure-portal"></a><span data-ttu-id="70a09-103">Come eseguire la procedura di backup e ripristino di un server nel Database di Azure per PostgreSQL usando il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="70a09-103">How To Backup and Restore a server in Azure Database for PostgreSQL using the Azure portal</span></span>

## <a name="backup-happens-automatically"></a><span data-ttu-id="70a09-104">Il backup viene eseguito automaticamente</span><span class="sxs-lookup"><span data-stu-id="70a09-104">Backup happens Automatically</span></span>
<span data-ttu-id="70a09-105">Quando si usa Database di Azure per PostgreSQL, il servizio di database esegue automaticamente il backup del servizio ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="70a09-105">When using Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="70a09-106">La disponibilità dei backup è di 7 giorni per il livello Basic e 35 giorni per il livello Standard.</span><span class="sxs-lookup"><span data-stu-id="70a09-106">The backups are available for 7 days when using Basic Tier, and 35 days when using Standard Tier.</span></span> <span data-ttu-id="70a09-107">Per altre informazioni, vedere [Livelli di servizio del Database di Azure per PostgreSQL](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="70a09-107">For more information, see [Azure Database for PostgreSQL service tiers](concepts-service-tiers.md)</span></span>

<span data-ttu-id="70a09-108">L'uso di questa funzionalità di backup automatico permette di ripristinare il server e tutti i suoi database in un nuovo server a un precedente punto temporizzato.</span><span class="sxs-lookup"><span data-stu-id="70a09-108">Using this automatic backup feature you may restore the server and all its databases into a new server to an earlier point-in-time.</span></span>

## <a name="restore-in-the-azure-portal"></a><span data-ttu-id="70a09-109">Ripristino nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="70a09-109">Restore in the Azure portal</span></span>
<span data-ttu-id="70a09-110">Il Database di Azure per PostgreSQL consente di ripristinare il server a un punto temporizzato e in una nuova copia del server.</span><span class="sxs-lookup"><span data-stu-id="70a09-110">Azure Database for PostgreSQL allows you to restore the server back to a point in time and into to a new copy of the server.</span></span> <span data-ttu-id="70a09-111">È possibile usare questo nuovo server per ripristinare i dati.</span><span class="sxs-lookup"><span data-stu-id="70a09-111">You can use this new server to recover your data.</span></span> 

<span data-ttu-id="70a09-112">Ad esempio, se oggi una tabella è stata accidentalmente eliminata a mezzogiorno, è possibile eseguire il ripristino a un'ora prima di mezzogiorno per recuperare la tabella e i dati mancanti dalla nuova copia del server.</span><span class="sxs-lookup"><span data-stu-id="70a09-112">For example, if a table was accidentally dropped at noon today, you could restore to the time just before noon and retrieve the missing table and data from that new copy of the server.</span></span>

<span data-ttu-id="70a09-113">La procedura seguente consente di ripristinare il server di esempio ad un punto temporizzato.</span><span class="sxs-lookup"><span data-stu-id="70a09-113">The following steps restore the sample server to a point in time:</span></span>
1. <span data-ttu-id="70a09-114">Accedere al [portale di Azure](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="70a09-114">Sign into the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="70a09-115">Individuare il Database di Azure per il server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="70a09-115">Locate your Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="70a09-116">Nel portale di Azure fare clic su **Tutte le risorse** dal menu a sinistra e digitare il nome, ad esempio **mypgserver-20170401**, per cercare il server esistente.</span><span class="sxs-lookup"><span data-stu-id="70a09-116">In the Azure portal, click **All Resources** from the left-hand menu and type in the name, such as **mypgserver-20170401**, to search for your existing server.</span></span> <span data-ttu-id="70a09-117">Fare clic sul nome del server elencato nei risultati della ricerca.</span><span class="sxs-lookup"><span data-stu-id="70a09-117">Click the server name listed in the search result.</span></span> <span data-ttu-id="70a09-118">Si apre la pagina **Panoramica** relativa al server, con le opzioni per un'ulteriore configurazione.</span><span class="sxs-lookup"><span data-stu-id="70a09-118">The **Overview** page for your server opens and provides options for further configuration.</span></span>

   ![Portale di Azure - Effettuare la ricerca del server](media/postgresql-howto-restore-server-portal/1-locate.png)

3. <span data-ttu-id="70a09-120">Nella parte superiore del pannello Panoramica server, fare clic su **Ripristina** nella barra degli strumenti.</span><span class="sxs-lookup"><span data-stu-id="70a09-120">On the top of the server overview blade, click **Restore** on the toolbar.</span></span> <span data-ttu-id="70a09-121">Viene aperto il pannello Ripristina.</span><span class="sxs-lookup"><span data-stu-id="70a09-121">The Restore blade opens.</span></span>

   ![Database di Azure per PostgreSQL - Panoramica - Pulsante Ripristino](./media/postgresql-howto-restore-server-portal/2_server.png)

4. <span data-ttu-id="70a09-123">Compilare il modulo Ripristina con le informazioni obbligatorie:</span><span class="sxs-lookup"><span data-stu-id="70a09-123">Fill out the Restore form with the required information:</span></span>

   ![<span data-ttu-id="70a09-124">Database di Azure per PostgreSQL - Informazioni di ripristino</span><span class="sxs-lookup"><span data-stu-id="70a09-124">Azure Database for PostgreSQL - Restore information</span></span> ](./media/postgresql-howto-restore-server-portal/3_restore.png)
  - <span data-ttu-id="70a09-125">**Punto di ripristino**: selezionare un punto nel tempo precedente alla modifica del server</span><span class="sxs-lookup"><span data-stu-id="70a09-125">**Restore point**: Select a point-in-time that occurs before the server was changed</span></span>
  - <span data-ttu-id="70a09-126">**Server di destinazione**: fornire un nuovo nome del server che si desidera ripristinare</span><span class="sxs-lookup"><span data-stu-id="70a09-126">**Target server**: Provide a new server name you want to restore to</span></span>
  - <span data-ttu-id="70a09-127">**Posizione**: non è possibile selezionare l'area, per impostazione predefinita è la stessa del server di origine</span><span class="sxs-lookup"><span data-stu-id="70a09-127">**Location**: You cannot select the region, by default it is same as the source server</span></span>
  - <span data-ttu-id="70a09-128">**Piano tariffario**: non è possibile modificare questo valore quando si ripristina un server.</span><span class="sxs-lookup"><span data-stu-id="70a09-128">**Pricing tier**: You cannot change this value when restoring a server.</span></span> <span data-ttu-id="70a09-129">È uguale al server di origine.</span><span class="sxs-lookup"><span data-stu-id="70a09-129">It is same as the source server.</span></span> 

5. <span data-ttu-id="70a09-130">Fare clic su **OK** per ripristinare il server al punto di ripristino temporizzato.</span><span class="sxs-lookup"><span data-stu-id="70a09-130">Click **OK** to restore the server to restore to a point in time.</span></span> 

6. <span data-ttu-id="70a09-131">Al termine del ripristino, individuare il nuovo server creato per verificare che il ripristino dei dati sia avvenuto come previsto.</span><span class="sxs-lookup"><span data-stu-id="70a09-131">Once the restore finishes, locate the new server that is created to verify the data was restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="70a09-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="70a09-132">Next steps</span></span>
- [<span data-ttu-id="70a09-133">Raccolte connessioni per il Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="70a09-133">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
