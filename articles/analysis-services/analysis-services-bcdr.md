---
title: "disponibilità elevata di Analysis Services aaaAzure | Documenti Microsoft"
description: "Assicurare la disponibilità elevata di Azure Analysis Services."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 6e09536c5bd7dc7f88f9b662e1a9f42d2b8c969b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="d808c-103">Disponibilità elevata di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="d808c-103">Analysis Services high availability</span></span>
<span data-ttu-id="d808c-104">Questo articolo descrive come garantire la disponibilità elevata dei server di Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="d808c-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="d808c-105">Garantire la disponibilità elevata durante un'interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="d808c-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="d808c-106">Sebbene accada raramente, un data center di Azure può subire un'interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="d808c-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="d808c-107">Quando si verifica un'interruzione, viene generata un'interruzione delle attività che può durare pochi minuti oppure alcune ore.</span><span class="sxs-lookup"><span data-stu-id="d808c-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="d808c-108">La disponibilità elevata è ottenuta spesso con la ridondanza dei server.</span><span class="sxs-lookup"><span data-stu-id="d808c-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="d808c-109">Azure Analysis Services consente di ottenere tale ridondanza tramite la creazione di server secondari e aggiuntivi in una o più aree.</span><span class="sxs-lookup"><span data-stu-id="d808c-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="d808c-110">Quando la creazione di server ridondanti, tooassure hello dati e i metadati di tali server sia sincronizzato con il server di hello in un'area che è non in linea, è possibile:</span><span class="sxs-lookup"><span data-stu-id="d808c-110">When creating redundant servers, tooassure hello data and metadata on those servers is in-sync with hello server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="d808c-111">Distribuire modelli tooredundant server in altri paesi.</span><span class="sxs-lookup"><span data-stu-id="d808c-111">Deploy models tooredundant servers in other regions.</span></span> <span data-ttu-id="d808c-112">Questo metodo richiede l'elaborazione dei dati in parallelo sia sul server primario sia sui server, assicurando così la sincronizzazione di tutti i server.</span><span class="sxs-lookup"><span data-stu-id="d808c-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="d808c-113">Eseguire il backup dei database dal server primario e il ripristino nei server ridondanti.</span><span class="sxs-lookup"><span data-stu-id="d808c-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="d808c-114">Ad esempio, automatizzare archiviazione tooAzure notturna backup e ripristino tooother server ridondanti in altre aree.</span><span class="sxs-lookup"><span data-stu-id="d808c-114">For example, you can automate nightly backups tooAzure storage, and restore tooother redundant servers in other regions.</span></span> 

<span data-ttu-id="d808c-115">In entrambi i casi, se il server principale si verifica un'interruzione, è necessario modificare le stringhe di connessione hello in client tooconnect toohello server in un altro Data Center regionale di report.</span><span class="sxs-lookup"><span data-stu-id="d808c-115">In either case, if your primary server experiences an outage, you must change hello connection strings in reporting clients tooconnect toohello server in a different regional datacenter.</span></span> <span data-ttu-id="d808c-116">Questa modifica deve essere presa in considerazione come soluzione estrema e solo quando si verifica un'interruzione del data center dell'area.</span><span class="sxs-lookup"><span data-stu-id="d808c-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="d808c-117">È più probabile che un'interruzione del data center che ospita il server principale venga risolta prima che sia possibile aggiornare le connessioni in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="d808c-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="d808c-118">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="d808c-118">Related information</span></span>
<span data-ttu-id="d808c-119">[Backup e ripristino](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="d808c-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="d808c-120">Gestire Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="d808c-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

