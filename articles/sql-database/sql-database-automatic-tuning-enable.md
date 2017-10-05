---
title: Abilitare l'ottimizzazione automatica per il database SQL di Azure | Microsoft Docs
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
ms.openlocfilehash: b391b1f7aa37c5a06fc320ce892534187deb4959
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="enable-automatic-tuning"></a><span data-ttu-id="6eae1-103">Abilitare l'ottimizzazione automatica</span><span class="sxs-lookup"><span data-stu-id="6eae1-103">Enable automatic tuning</span></span>

<span data-ttu-id="6eae1-104">Il database SQL di Azure è un servizio dati gestito automaticamente che esegue un monitoraggio costante delle query e identifica l'azione che è possibile eseguire per migliorare le prestazioni del carico di lavoro.</span><span class="sxs-lookup"><span data-stu-id="6eae1-104">Azure SQL Database is an automatically managed data service that constantly monitors your queries and identifies the action that you can perform to improve performance of your workload.</span></span> <span data-ttu-id="6eae1-105">È possibile esaminare le raccomandazioni e applicarle manualmente oppure delegare al database SQL di Azure l'applicazione automatica delle azioni correttive, condizione nota come **modalità di ottimizzazione automatica**.</span><span class="sxs-lookup"><span data-stu-id="6eae1-105">You can review recommendations and manually apply them, or let Azure SQL Database automatically apply corrective actions - this is known as **automatic tuning mode**.</span></span> <span data-ttu-id="6eae1-106">L'ottimizzazione automatica può essere abilitata a livello di server o di database.</span><span class="sxs-lookup"><span data-stu-id="6eae1-106">Automatic tuning can be enabled at the server or the database level.</span></span>

## <a name="enable-automatic-tuning-on-server"></a><span data-ttu-id="6eae1-107">Abilitare l'ottimizzazione automatica nel server</span><span class="sxs-lookup"><span data-stu-id="6eae1-107">Enable automatic tuning on server</span></span>

<span data-ttu-id="6eae1-108">Per abilitare l'ottimizzazione automatica nel server di database SQL di Azure, passare al server nel portale di Azure e quindi selezionare **Ottimizzazione automatica** nel menu.</span><span class="sxs-lookup"><span data-stu-id="6eae1-108">To enable automatic tuning on Azure SQL Database server, navigate to the server in Azure portal and then select **Automatic tuning** in the menu.</span></span> <span data-ttu-id="6eae1-109">Selezionare le opzioni di ottimizzazione automatica che si vuole abilitare e selezionare **Applica**:</span><span class="sxs-lookup"><span data-stu-id="6eae1-109">Select the automatic tuning options you want to enable and select **Apply**:</span></span>

![Server](./media/sql-database-automatic-tuning-enable/server.png)

<span data-ttu-id="6eae1-111">Le opzioni di ottimizzazione automatica nel server vengono applicate a tutti i database nel server.</span><span class="sxs-lookup"><span data-stu-id="6eae1-111">Automatic tuning options on server are applied to all databases on the server.</span></span> <span data-ttu-id="6eae1-112">Per impostazione predefinita, tutti i database ereditano la configurazione dal relativo server padre, ma è possibile modificare questa impostazione e specificarla singolarmente per ogni database.</span><span class="sxs-lookup"><span data-stu-id="6eae1-112">By default, all databases inherit the configuration from their parent server, but this can be overridden and specified for each database individually.</span></span>

## <a name="configure-automatic-tuning-on-database"></a><span data-ttu-id="6eae1-113">Configurare l'ottimizzazione automatica per il database</span><span class="sxs-lookup"><span data-stu-id="6eae1-113">Configure automatic tuning on database</span></span>

<span data-ttu-id="6eae1-114">Il portale di Azure consente di specificare singolarmente la configurazione di ottimizzazione automatica in ogni database.</span><span class="sxs-lookup"><span data-stu-id="6eae1-114">The Azure portal enables you to individually specify the automatic tuning configuration on each database.</span></span>

> [!NOTE]
> <span data-ttu-id="6eae1-115">La raccomandazione generale suggerisce di gestire la configurazione di ottimizzazione automatica a livello del server, in modo che le stesse impostazioni di configurazione possano essere applicate automaticamente in ogni database.</span><span class="sxs-lookup"><span data-stu-id="6eae1-115">The general recommendation is to manage the automatic tuning configuration at server level so the same configuration settings can be applied on every database automatically.</span></span> <span data-ttu-id="6eae1-116">Configurare l'ottimizzazione automatica per un singolo database se il database è diverso dagli altri nello stesso server.</span><span class="sxs-lookup"><span data-stu-id="6eae1-116">Configure automatic tuning on an individual database if the database is different that others on the same server.</span></span>
>

<span data-ttu-id="6eae1-117">Per abilitare l'ottimizzazione automatica per un singolo database, passare al database nel portale di Azure e quindi selezionare **Ottimizzazione automatica**.</span><span class="sxs-lookup"><span data-stu-id="6eae1-117">To enable automatic tuning on a single database, navigate to the database in the Azure portal and then and select **Automatic tuning**.</span></span> <span data-ttu-id="6eae1-118">È possibile configurare un singolo database in modo che erediti le impostazioni dal database selezionando la casella di controllo oppure è possibile specificare la configurazione per un database singolarmente.</span><span class="sxs-lookup"><span data-stu-id="6eae1-118">You can configure a single database to inherit the settings from the database by selecting the checkbox or you can specify the configuration for a database individually.</span></span>

![Database](./media/sql-database-automatic-tuning-enable/database.png)

<span data-ttu-id="6eae1-120">Dopo aver selezionato la configurazione appropriata, fare clic su **Applica**.</span><span class="sxs-lookup"><span data-stu-id="6eae1-120">Once you have selected appropriate configuration, click **Apply**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6eae1-121">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6eae1-121">Next steps</span></span>
* <span data-ttu-id="6eae1-122">Leggere l'[articolo sull'ottimizzazione automatica](sql-database-automatic-tuning.md) per altre informazioni sull'ottimizzazione automatica e sull'utilità di questa funzione per il miglioramento delle prestazioni.</span><span class="sxs-lookup"><span data-stu-id="6eae1-122">Read the [Automatic tuning article](sql-database-automatic-tuning.md) to learn more about automatic tuning and how it can help you improve your performance.</span></span>
* <span data-ttu-id="6eae1-123">Vedere le [Raccomandazioni per le prestazioni](sql-database-advisor.md) per una panoramica delle raccomandazioni per le prestazioni per il database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6eae1-123">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="6eae1-124">Vedere l'articolo [Informazioni dettagliate prestazioni query](sql-database-query-performance.md) per informazioni sull'analisi dell'impatto sulle prestazioni delle query principali.</span><span class="sxs-lookup"><span data-stu-id="6eae1-124">See [Query Performance Insights](sql-database-query-performance.md) to learn about viewing the performance impact of your top queries.</span></span>
