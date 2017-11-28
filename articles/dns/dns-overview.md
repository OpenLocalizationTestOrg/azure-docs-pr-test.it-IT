---
title: aaaOverview di DNS di Azure | Documenti Microsoft
description: Panoramica del servizio di hosting DNS in Microsoft Azure. Ospitare il dominio in Microsoft Azure.
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 68747a0d-b358-4b8e-b5e2-e2570745ec3f
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/19/2017
ms.author: gwallace
ms.openlocfilehash: a10f87c488356469e9c04aabde31129049563891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-dns-overview"></a><span data-ttu-id="3b921-104">Panoramica di DNS di Azure</span><span class="sxs-lookup"><span data-stu-id="3b921-104">Azure DNS overview</span></span>

<span data-ttu-id="3b921-105">Hello Domain Name System o DNS, è responsabile della conversione (o nel risolvere) un sito Web o servizio name tooits indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="3b921-105">hello Domain Name System, or DNS, is responsible for translating (or resolving) a website or service name tooits IP address.</span></span> <span data-ttu-id="3b921-106">DNS di Azure è un servizio di hosting per i domini DNS, che fornisce la risoluzione dei nomi usando l'infrastruttura di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-106">Azure DNS is a hosting service for DNS domains, providing name resolution using Microsoft Azure infrastructure.</span></span> <span data-ttu-id="3b921-107">Ospitando i domini in Azure, è possibile gestire il servizio DNS i record mediante hello credenziali, API, strumenti e fatturazione come altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-107">By hosting your domains in Azure, you can manage your DNS records using hello same credentials, APIs, tools, and billing as your other Azure services.</span></span>

![Panoramica del servizio DNS](./media/dns-overview/scenario.png)

## <a name="features"></a><span data-ttu-id="3b921-109">Funzionalità</span><span class="sxs-lookup"><span data-stu-id="3b921-109">Features</span></span>

* <span data-ttu-id="3b921-110">**Affidabilità e prestazioni**: i domini DNS nel servizio DNS di Azure sono ospitati nella rete globale di Azure dei server dei nomi DNS.</span><span class="sxs-lookup"><span data-stu-id="3b921-110">**Reliability and performance** - DNS domains in Azure DNS are hosted on Azure's global network of DNS name servers.</span></span> <span data-ttu-id="3b921-111">Utilizziamo Anycast di rete in modo che ogni query DNS è stata risposta dal server DNS disponibile più vicino di hello.</span><span class="sxs-lookup"><span data-stu-id="3b921-111">We use Anycast networking so that each DNS query is answered by hello closest available DNS server.</span></span> <span data-ttu-id="3b921-112">Ciò consente di accelerare le prestazioni e ottenere la disponibilità elevata per il dominio.</span><span class="sxs-lookup"><span data-stu-id="3b921-112">This provides both fast performance and high availability for your domain.</span></span>

* <span data-ttu-id="3b921-113">**Perfetta integrazione** -servizio DNS di Azure hello può essere utilizzato toomanage i record DNS per i servizi di Azure e può essere utilizzato tooprovide DNS per le risorse esterne, nonché.</span><span class="sxs-lookup"><span data-stu-id="3b921-113">**Seamless integration** - hello Azure DNS service can be used toomanage DNS records for your Azure services and can be used tooprovide DNS for your external resources as well.</span></span> <span data-ttu-id="3b921-114">DNS di Azure è integrato nel portale di Azure hello e utilizza hello stesse credenziali, fatturazione e il contratto di assistenza come altri servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-114">Azure DNS is integrated in hello Azure portal and uses hello same credentials, billing and support contract as your other Azure services.</span></span>

* <span data-ttu-id="3b921-115">**Sicurezza** -hello servizio DNS di Azure si basa su Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-115">**Security** - hello Azure DNS service is based on Azure Resource Manager.</span></span> <span data-ttu-id="3b921-116">Usufruisce quindi delle funzionalità di Resource Manager, come il controllo degli accessi in base al ruolo, i log di controllo e il blocco delle risorse.</span><span class="sxs-lookup"><span data-stu-id="3b921-116">As such, it benefits from Resource Manager features such as role-based access control, audit logs, and resource locking.</span></span> <span data-ttu-id="3b921-117">I domini e i record possono essere gestiti tramite hello portale di Azure, i cmdlet di Azure PowerShell e hello multipiattaforma CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-117">Your domains and records can be managed via hello Azure portal, Azure PowerShell cmdlets, and hello cross-platform Azure CLI.</span></span> <span data-ttu-id="3b921-118">Le applicazioni che richiedono la gestione automatica di DNS è possono integrare con il servizio di hello tramite hello SDK e API REST.</span><span class="sxs-lookup"><span data-stu-id="3b921-118">Applications requiring automatic DNS management can integrate with hello service via hello REST API and SDKs.</span></span>

<span data-ttu-id="3b921-119">DNS di Azure attualmente non supporta l'acquisto dei nomi di dominio.</span><span class="sxs-lookup"><span data-stu-id="3b921-119">Azure DNS does not currently support purchasing of domain names.</span></span> <span data-ttu-id="3b921-120">Se si desidera toopurchase domini, è necessario toouse un registrar di nomi di dominio di terze parti.</span><span class="sxs-lookup"><span data-stu-id="3b921-120">If you want toopurchase domains, you need toouse a third-party domain name registrar.</span></span> <span data-ttu-id="3b921-121">registrar Hello in genere una tariffa small annuale.</span><span class="sxs-lookup"><span data-stu-id="3b921-121">hello registrar typically charges a small annual fee.</span></span> <span data-ttu-id="3b921-122">domini Hello possono quindi essere ospitati in DNS di Azure per la gestione dei record DNS.</span><span class="sxs-lookup"><span data-stu-id="3b921-122">hello domains can then be hosted in Azure DNS for management of DNS records.</span></span> <span data-ttu-id="3b921-123">Vedere [tooAzure un dominio DNS delegato](dns-domain-delegation.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="3b921-123">See [Delegate a Domain tooAzure DNS](dns-domain-delegation.md) for details.</span></span>

## <a name="pricing"></a><span data-ttu-id="3b921-124">Prezzi</span><span class="sxs-lookup"><span data-stu-id="3b921-124">Pricing</span></span>

<span data-ttu-id="3b921-125">DNS fatturazione si basa sul numero di hello di zone DNS ospitate in Azure e dal numero di hello di query DNS.</span><span class="sxs-lookup"><span data-stu-id="3b921-125">DNS billing is based on hello number of DNS zones hosted in Azure and by hello number of DNS queries.</span></span> <span data-ttu-id="3b921-126">ulteriori informazioni sui prezzi visitare toolearn [dei prezzi di Azure DNS](https://azure.microsoft.com/pricing/details/dns/).</span><span class="sxs-lookup"><span data-stu-id="3b921-126">toolearn more about pricing visit [Azure DNS Pricing](https://azure.microsoft.com/pricing/details/dns/).</span></span>

## <a name="faq"></a><span data-ttu-id="3b921-127">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="3b921-127">FAQ</span></span>

<span data-ttu-id="3b921-128">Per domande frequenti su DNS di Azure, vedere hello [domande frequenti su DNS di Azure](dns-faq.md).</span><span class="sxs-lookup"><span data-stu-id="3b921-128">For frequently asked questions about Azure DNS, see hello [Azure DNS FAQ](dns-faq.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b921-129">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3b921-129">Next steps</span></span>

<span data-ttu-id="3b921-130">Per informazioni sui record e le zone DNS visitare la pagina [Panoramica delle zone e dei record DNS](dns-zones-records.md).</span><span class="sxs-lookup"><span data-stu-id="3b921-130">Learn about DNS zones and records by visiting: [DNS zones and records overview](dns-zones-records.md).</span></span>

<span data-ttu-id="3b921-131">Informazioni su come troppo[creare una zona DNS](./dns-getstarted-create-dnszone-portal.md) nel sistema DNS di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-131">Learn how too[create a DNS zone](./dns-getstarted-create-dnszone-portal.md) in Azure DNS.</span></span>

<span data-ttu-id="3b921-132">Informazioni su alcune delle hello altre chiavi [funzionalità di rete](../networking/networking-overview.md) di Azure.</span><span class="sxs-lookup"><span data-stu-id="3b921-132">Learn about some of hello other key [networking capabilities](../networking/networking-overview.md) of Azure.</span></span>

