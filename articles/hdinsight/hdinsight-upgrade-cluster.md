---
title: "versione più recente tooa cluster HDInsight aaaUpgrade-Azure | Documenti Microsoft"
description: "Informazioni su come tooUpgrade HDInsight cluster tooa di versione più recente."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="3bd55-103">L'aggiornamento di versione più recente tooa del cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="3bd55-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="3bd55-104">sfruttare tootake hello funzionalità più recenti di HDInsight, è consigliabile che il cluster HDInsight versione toolatest aggiornato.</span><span class="sxs-lookup"><span data-stu-id="3bd55-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="3bd55-105">Seguire hello sotto tooupgrade linee guida per le versioni cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bd55-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="3bd55-106">Le versioni 3.2 e 3.3 dei cluster HDInsight sono prossime alla data di ritiro.</span><span class="sxs-lookup"><span data-stu-id="3bd55-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="3bd55-107">Per altre informazioni sulle versioni di HDInsight vedere [Versioni del componente HDInsight](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="3bd55-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="3bd55-108">Procedure di aggiornamento</span><span class="sxs-lookup"><span data-stu-id="3bd55-108">Upgrade tasks</span></span>
<span data-ttu-id="3bd55-109">Hello del flusso di lavoro tooupgrade HDInsight Cluster è come indicato di seguito.</span><span class="sxs-lookup"><span data-stu-id="3bd55-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Diagramma del flusso di lavoro di aggiornamento](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="3bd55-111">Leggere ogni sezione di questo documento toounderstand modifiche che possono essere necessari durante l'aggiornamento del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3bd55-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="3bd55-112">Creare un cluster come ambiente di test/controllo qualità.</span><span class="sxs-lookup"><span data-stu-id="3bd55-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="3bd55-113">Per ulteriori informazioni sulla creazione di un cluster, vedere [informazioni su come i cluster HDInsight basati su Linux di toocreate](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="3bd55-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="3bd55-114">Copia esistente processi, origini dati e sink toohello nuovo ambiente.</span><span class="sxs-lookup"><span data-stu-id="3bd55-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="3bd55-115">Vedere [tooTest copia dati ambiente](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) per altri dettagli.</span><span class="sxs-lookup"><span data-stu-id="3bd55-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="3bd55-116">Eseguire test toomake assicurarsi che i processi di funzionano come previsto nel nuovo cluster hello di convalida.</span><span class="sxs-lookup"><span data-stu-id="3bd55-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="3bd55-117">Dopo avere verificato che tutto funzioni come previsto, pianificare i tempi di inattività per la migrazione di hello.</span><span class="sxs-lookup"><span data-stu-id="3bd55-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="3bd55-118">Durante questo periodo di inattività, hello le seguenti operazioni:</span><span class="sxs-lookup"><span data-stu-id="3bd55-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="3bd55-119">Eseguire il backup dei dati temporanei archiviati in locale sui nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="3bd55-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="3bd55-120">ad esempio se i dati sono archiviati direttamente in un nodo head.</span><span class="sxs-lookup"><span data-stu-id="3bd55-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="3bd55-121">Eliminare il cluster esistente hello.</span><span class="sxs-lookup"><span data-stu-id="3bd55-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="3bd55-122">Creare un cluster in hello stessa rete virtuale subnet con più recente (o supportate) HDI versione utilizzando hello allo stesso archivio dati predefinito che hello precedente cluster utilizzato.</span><span class="sxs-lookup"><span data-stu-id="3bd55-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="3bd55-123">In questo modo hello nuovo cluster toocontinue utilizzano i dati di produzione esistente.</span><span class="sxs-lookup"><span data-stu-id="3bd55-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="3bd55-124">Importare i dati temporanei di cui è stata eseguita una copia di backup.</span><span class="sxs-lookup"><span data-stu-id="3bd55-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="3bd55-125">Avvia processi/continua l'elaborazione tramite il nuovo cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="3bd55-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bd55-126">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3bd55-126">Next Steps</span></span>
* [<span data-ttu-id="3bd55-127">Informazioni su come i cluster HDInsight basati su Linux di toocreate</span><span class="sxs-lookup"><span data-stu-id="3bd55-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="3bd55-128">Connettersi tramite SSH tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="3bd55-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="3bd55-129">Gestire un cluster basato su Linux tramite Ambari</span><span class="sxs-lookup"><span data-stu-id="3bd55-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

