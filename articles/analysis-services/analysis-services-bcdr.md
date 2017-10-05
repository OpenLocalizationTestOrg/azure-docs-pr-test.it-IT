---
title: "Disponibilità elevata di Azure Analysis Services | Documentazione Microsoft"
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
ms.openlocfilehash: 84b4c59bac1feeb8611b3a8d783d093ba073e532
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="8f69a-103">Disponibilità elevata di Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8f69a-103">Analysis Services high availability</span></span>
<span data-ttu-id="8f69a-104">Questo articolo descrive come garantire la disponibilità elevata dei server di Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="8f69a-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="8f69a-105">Garantire la disponibilità elevata durante un'interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="8f69a-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="8f69a-106">Sebbene accada raramente, un data center di Azure può subire un'interruzione del servizio.</span><span class="sxs-lookup"><span data-stu-id="8f69a-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="8f69a-107">Quando si verifica un'interruzione, viene generata un'interruzione delle attività che può durare pochi minuti oppure alcune ore.</span><span class="sxs-lookup"><span data-stu-id="8f69a-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="8f69a-108">La disponibilità elevata è ottenuta spesso con la ridondanza dei server.</span><span class="sxs-lookup"><span data-stu-id="8f69a-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="8f69a-109">Azure Analysis Services consente di ottenere tale ridondanza tramite la creazione di server secondari e aggiuntivi in una o più aree.</span><span class="sxs-lookup"><span data-stu-id="8f69a-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="8f69a-110">Per garantire che i dati e i metadati presenti sui server ridondanti creati siano sincronizzati con il server posizionato nell'area non in linea, è possibile:</span><span class="sxs-lookup"><span data-stu-id="8f69a-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="8f69a-111">Distribuire i modelli nei server ridondanti in altre aree.</span><span class="sxs-lookup"><span data-stu-id="8f69a-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="8f69a-112">Questo metodo richiede l'elaborazione dei dati in parallelo sia sul server primario sia sui server, assicurando così la sincronizzazione di tutti i server.</span><span class="sxs-lookup"><span data-stu-id="8f69a-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="8f69a-113">Eseguire il backup dei database dal server primario e il ripristino nei server ridondanti.</span><span class="sxs-lookup"><span data-stu-id="8f69a-113">Back up databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="8f69a-114">È possibile ad esempio automatizzare i backup notturni nell'archiviazione di Azure e il ripristino nei server ridondanti in altre aree.</span><span class="sxs-lookup"><span data-stu-id="8f69a-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="8f69a-115">In entrambi i casi, se il server principale subisce un'interruzione, è necessario modificare le stringhe di connessione nei client di segnalazione report affinché eseguano la connessione al server del data center di un'altra area.</span><span class="sxs-lookup"><span data-stu-id="8f69a-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="8f69a-116">Questa modifica deve essere presa in considerazione come soluzione estrema e solo quando si verifica un'interruzione del data center dell'area.</span><span class="sxs-lookup"><span data-stu-id="8f69a-116">This change should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="8f69a-117">È più probabile che un'interruzione del data center che ospita il server principale venga risolta prima che sia possibile aggiornare le connessioni in tutti i client.</span><span class="sxs-lookup"><span data-stu-id="8f69a-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 



## <a name="related-information"></a><span data-ttu-id="8f69a-118">Informazioni correlate</span><span class="sxs-lookup"><span data-stu-id="8f69a-118">Related information</span></span>
<span data-ttu-id="8f69a-119">[Backup e ripristino](analysis-services-backup.md) </span><span class="sxs-lookup"><span data-stu-id="8f69a-119">[Backup and restore](analysis-services-backup.md) </span></span>  
[<span data-ttu-id="8f69a-120">Gestire Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="8f69a-120">Manage Azure Analysis Services</span></span>](analysis-services-manage.md) 

