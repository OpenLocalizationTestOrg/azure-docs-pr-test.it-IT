---
title: ottimizzazione di Database SQL di Azure automatica aaaEnable | Documenti Microsoft
description: "È possibile abilitare facilmente l'ottimizzazione automatica nel database SQL di Azure."
services: sql-database
documentationcenter: 
author: vvasic
manager: drasumic
editor: vvasic
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: NA
ms.date: 06/05/2016
ms.author: vvasic
ms.openlocfilehash: af9da161eabc0f8c4cb100c050288f234efb8093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="e81ba-103">Abilitare l'ottimizzazione automatica</span><span class="sxs-lookup"><span data-stu-id="e81ba-103">Enable automatic tuning</span></span>

<span data-ttu-id="e81ba-104">Database SQL di Azure è un servizio di dati gestiti automaticamente che costantemente controlla le query e identifica l'azione di hello che è possibile eseguire tooimprove delle prestazioni del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e81ba-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies hello action that you can perform tooimprove performance of your workload.</span></span> <span data-ttu-id="e81ba-105">È possibile esaminare le raccomandazioni e applicarle manualmente oppure delegare al database SQL di Azure l'applicazione automatica delle azioni correttive, condizione nota come **modalità di ottimizzazione automatica**.</span><span class="sxs-lookup"><span data-stu-id="e81ba-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="e81ba-106">L'ottimizzazione automatica può essere abilitata a livello di database di hello server hello o.</span><span class="sxs-lookup"><span data-stu-id="e81ba-106">Automatic tuning can be enabled at hello server or hello database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="e81ba-107">Abilitare l'ottimizzazione automatica nel server</span><span class="sxs-lookup"><span data-stu-id="e81ba-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="e81ba-108">tooenable automatico ottimizzazione sul server di Database SQL di Azure, passare toohello server in Azure nel portale e quindi selezionare **ottimizzazione automatica** nel menu hello.</span><span class="sxs-lookup"><span data-stu-id="e81ba-108">tooenable automatic tuning on Azure SQL Database server, navigate toohello server in Azure portal and then select **Automatic tuning** in hello menu.</span></span> <span data-ttu-id="e81ba-109">Selezionare opzioni di ottimizzazione automatica tooenable desiderata e scegliere di hello **applica**:</span><span class="sxs-lookup"><span data-stu-id="e81ba-109">Select hello automatic tuning options you want tooenable and select **Apply**:</span></span>

![Server](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="e81ba-111">Opzioni nel server di ottimizzazione automatici sono applicati tooall database server hello.</span><span class="sxs-lookup"><span data-stu-id="e81ba-111">Automatic tuning options on server are applied tooall databases on hello server.</span></span> <span data-ttu-id="e81ba-112">Per impostazione predefinita, tutti i database ereditano la configurazione di hello dal relativo server padre, ma ciò può essere sottoposto a override e specificare singolarmente per ogni database.</span><span class="sxs-lookup"><span data-stu-id="e81ba-112">By default, all databases inherit hello configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="e81ba-113">Configurare l'ottimizzazione automatica per il database</span><span class="sxs-lookup"><span data-stu-id="e81ba-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="e81ba-114">Hello Azure attiva portale si tooindividually specificare la configurazione di ottimizzazione automatica di hello in ciascun database.</span><span class="sxs-lookup"><span data-stu-id="e81ba-114">hello Azure portal enables you tooindividually specify hello automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="e81ba-115">raccomandazione generale Hello è toomanage hello ottimizzazione configurazione automatica a livello di server in questo caso hello stesse impostazioni di configurazione possono essere applicate automaticamente in ogni database.</span><span class="sxs-lookup"><span data-stu-id="e81ba-115">hello general recommendation is toomanage hello automatic tuning configuration at server level so hello same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="e81ba-116">Configurare l'ottimizzazione automatica in un singolo database se hello database diversi che gli altri hello nello stesso server.</span><span class="sxs-lookup"><span data-stu-id="e81ba-116">Configure automatic tuning on an individual database if hello database is different that others on hello same server.</span></span>
>

<span data-ttu-id="e81ba-117">tooenable automatico ottimizzazione su un singolo database, passare toohello database nel portale di Azure hello e poi selezionare **ottimizzazione automatica**.</span><span class="sxs-lookup"><span data-stu-id="e81ba-117">tooenable automatic tuning on a single database, navigate toohello database in hello Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="e81ba-118">È possibile configurare le impostazioni di hello tooinherit un singolo database dal database hello selezionando la casella di controllo hello oppure è possibile specificare singolarmente configurazione hello per un database.</span><span class="sxs-lookup"><span data-stu-id="e81ba-118">You can configure a single database tooinherit hello settings from hello database by selecting hello checkbox or you can specify hello configuration for a database individually.</span></span>

![Database](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="e81ba-120">Dopo aver selezionato la configurazione appropriata, fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="e81ba-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e81ba-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e81ba-121">Next steps</span></span>
* <span data-ttu-id="e81ba-122">Hello lettura [articolo ottimizzazione automatica](sql-database-automatic-tuning.md) toolearn ulteriori informazioni sull'ottimizzazione automatica e la modalità consente di migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e81ba-122">Read hello [Automatic tuning article](sql-database-automatic-tuning.md) toolearn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="e81ba-123">Vedere le [Raccomandazioni per le prestazioni](sql-database-advisor.md) per una panoramica delle raccomandazioni per le prestazioni per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="e81ba-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="e81ba-124">Vedere [informazioni dettagliate prestazioni Query](sql-database-query-performance.md) toolearn sulla visualizzazione impatto sulle prestazioni hello per le prime query.</span><span class="sxs-lookup"><span data-stu-id="e81ba-124">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>
