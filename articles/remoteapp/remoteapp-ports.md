---
title: Elenco di porte e URL da aggiungere all'elenco elementi consentiti per Azure RemoteApp distribuito nella rete virtuale del cliente | Documentazione Microsoft
description: Informazioni sulle porte e gli URL da configurare per la comunicazione con RemoteApp di Azure.
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
ms.openlocfilehash: c17ff8d5441ca92f7b893edb541a1e9730c2a847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="dcbff-103">Elenco di porte e URL per consentire l'accesso a RemoteApp di Azure distribuito sulla rete virtuale cliente</span><span class="sxs-lookup"><span data-stu-id="dcbff-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="dcbff-104">Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017.</span><span class="sxs-lookup"><span data-stu-id="dcbff-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="dcbff-105">Per i dettagli, vedere l' [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) .</span><span class="sxs-lookup"><span data-stu-id="dcbff-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="dcbff-106">Se si distribuisce una raccolta ibrida o un cloud di Azure RemoteApp in una rete virtuale, esaminare le informazioni sulle porte seguenti.</span><span class="sxs-lookup"><span data-stu-id="dcbff-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="dcbff-107">Per altre informazioni sulle reti virtuali, vedere la [panoramica sulle reti virtuali](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="dcbff-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="dcbff-108">Se è stato creato un gruppo di sicurezza di rete (NSG) che limita il traffico alle risorse di rete virtuale nella raccolta, verificare che le porte seguenti siano accessibili e consentite tramite i criteri di sicurezza della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="dcbff-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="dcbff-109">Per altre informazioni sui gruppi di sicurezza di rete, vedere [Gruppi di sicurezza di rete (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="dcbff-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="dcbff-110">La subnet di RemoteApp di Azure necessita dell'accesso ai seguenti endpoint e URL:</span><span class="sxs-lookup"><span data-stu-id="dcbff-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="dcbff-111">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="dcbff-111">*.servicebus.windows.net</span></span>
* <span data-ttu-id="dcbff-112">*. servicebus.net</span><span class="sxs-lookup"><span data-stu-id="dcbff-112">*.servicebus.net</span></span>
* <span data-ttu-id="dcbff-113">https://*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="dcbff-113">https://*.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="dcbff-114">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="dcbff-114">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="dcbff-115">https://*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="dcbff-115">https://*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="dcbff-116">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="dcbff-116">https://*.core.windows.net</span></span>  
* <span data-ttu-id="dcbff-117">In uscita:TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="dcbff-117">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="dcbff-118">Facoltativo: UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="dcbff-118">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="dcbff-119">I client RemoteApp di Azure devono accedere ai seguenti endpoint e URL:</span><span class="sxs-lookup"><span data-stu-id="dcbff-119">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="dcbff-120">Per client si intende desktop, dispositivi e così via, usati per connettersi alle app distribuite nella raccolta RemoteApp di Azure.</span><span class="sxs-lookup"><span data-stu-id="dcbff-120">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* <span data-ttu-id="dcbff-121">https://telemetry.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="dcbff-121">https://telemetry.remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="dcbff-122">https://*.remoteapp.windowsazure.com (le porte UDP facoltative riguardano questo indirizzo)</span><span class="sxs-lookup"><span data-stu-id="dcbff-122">https://*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* <span data-ttu-id="dcbff-123">https://login.windows.net</span><span class="sxs-lookup"><span data-stu-id="dcbff-123">https://login.windows.net</span></span>  
* <span data-ttu-id="dcbff-124">https://login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="dcbff-124">https://login.microsoftonline.com</span></span>  
* <span data-ttu-id="dcbff-125">https://www.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="dcbff-125">https://www.remoteapp.windowsazure.com</span></span> 
* <span data-ttu-id="dcbff-126">https://*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="dcbff-126">https://*.core.windows.net</span></span>  
* <span data-ttu-id="dcbff-127">In uscita: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="dcbff-127">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="dcbff-128">Facoltativo: UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="dcbff-128">Optional - UDP: 3391</span></span> 

