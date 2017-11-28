---
title: aaaList di porte e gli URL toowhitelist per Azure RemoteApp distribuito nella rete virtuale cliente | Documenti Microsoft
description: Informazioni sulle porte e gli URL, occorre tooconfigure per le comunicazioni tramite Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 039866f7b64ac763ca833d66031ade3def1d3543
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="list-of-ports-and-urls-toopermit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="1c23f-103">Elenco di porte e gli URL accesso toopermit per Azure RemoteApp distribuito nella rete virtuale cliente</span><span class="sxs-lookup"><span data-stu-id="1c23f-103">List of Ports and URLs toopermit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1c23f-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="1c23f-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="1c23f-105">Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="1c23f-105">Read hello [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="1c23f-106">Se si distribuisce un insieme di cloud o ibrida di Azure RemoteApp in una rete virtuale (VNET), esaminare le seguenti informazioni porta hello.</span><span class="sxs-lookup"><span data-stu-id="1c23f-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review hello following port information.</span></span> <span data-ttu-id="1c23f-107">Per altre informazioni sulle reti virtuali, vedere la [panoramica sulle reti virtuali](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c23f-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="1c23f-108">Se è stato creato un gruppo di sicurezza di rete (gruppo) limitando le risorse di rete virtuale toohello traffico nella raccolta, assicurarsi che hello seguenti porte siano accessibili e sono consentite tramite criteri di sicurezza hello nella rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="1c23f-108">If you have created a network security group (NSG) restricting traffic toohello virtual network resources in your collection, make sure hello following ports are accessible and allowed through hello security policies on hello virtual network.</span></span> <span data-ttu-id="1c23f-109">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="1c23f-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-toothese-endpoints-and-urls"></a><span data-ttu-id="1c23f-110">Subnet di Azure RemoteApp deve endpoint toothese di accesso e gli URL:</span><span class="sxs-lookup"><span data-stu-id="1c23f-110">Azure RemoteApp subnet needs access toothese endpoints and URLs:</span></span>
* <span data-ttu-id="1c23f-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="1c23f-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="1c23f-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="1c23f-112">*.servicebus.net</span></span>
* <span data-ttu-id="1c23f-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="1c23f-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="1c23f-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="1c23f-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="1c23f-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="1c23f-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="1c23f-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1c23f-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="1c23f-117">In uscita:TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="1c23f-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="1c23f-118">Facoltativo: UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="1c23f-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-toothese-endpoints-and-urls"></a><span data-ttu-id="1c23f-119">I client di Azure RemoteApp è necessario accedere a endpoint toothese e URL:</span><span class="sxs-lookup"><span data-stu-id="1c23f-119">Azure RemoteApp clients need access toothese endpoints and URLs:</span></span>
<span data-ttu-id="1c23f-120">Dai client che si intende hello desktop, dispositivi e così via, che gli utenti utilizzare tooconnect toohello App distribuite in hello raccolta di Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="1c23f-120">By clients I mean hello desktops, devices etc. that people use tooconnect toohello apps deployed in hello Azure RemoteApp collection.</span></span>

* <span data-ttu-id="1c23f-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="1c23f-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="1c23f-122">https://*.RemoteApp.windowsazure.com (per questo indirizzo sono le porte UDP hello facoltative)</span><span class="sxs-lookup"><span data-stu-id="1c23f-122">https://*.remoteapp.windowsazure.com (hello optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="1c23f-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="1c23f-123">https://login.windows.net</span></span>  
* <span data-ttu-id="1c23f-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="1c23f-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="1c23f-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="1c23f-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="1c23f-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="1c23f-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="1c23f-127">In uscita: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="1c23f-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="1c23f-128">Facoltativo: UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="1c23f-128">Optional - UDP: 3391</span></span> 

