---
title: Panoramica del bilanciamento del carico Internet | Documentazione Microsoft
description: "Panoramica del bilanciamento del carico Internet e delle relative funzionalità. Modalità di funzionamento del bilanciamento del carico per Azure con macchine virtuali e servizi cloud."
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 529b37aa-a45c-41d1-8877-fee8cc1fa375
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: c420b38fbe8054bc4b701f89ebc417677ca47a27
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="1eb3c-104">Panoramica del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="1eb3c-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="1eb3c-105">Il bilanciamento del carico di Azure esegue il mapping dell'indirizzo IP pubblico e del numero di porta del traffico in ingresso all'indirizzo IP privato e al numero di porta della macchina virtuale e viceversa per il traffico di risposta proveniente dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-105">Azure load balancer maps the public IP address and port number of incoming traffic to the private IP address and port number of the virtual machine and vice versa for the response traffic from the virtual machine.</span></span> <span data-ttu-id="1eb3c-106">Le regole di bilanciamento del carico consentono di distribuire tipi di traffico specifici tra più macchine virtuali o servizi.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-106">Load balancing rules allow you to distribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="1eb3c-107">È ad esempio possibile dividere il carico del traffico delle richieste Web tra più server Web o ruoli Web.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-107">For example, you can spread the load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="1eb3c-108">Per un servizio cloud contenente istanze di ruoli Web o ruoli di lavoro, è possibile definire un endpoint pubblico nel file di definizione del servizio (con estensione csdef).</span><span class="sxs-lookup"><span data-stu-id="1eb3c-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in the service definition (.csdef) file.</span></span>

<span data-ttu-id="1eb3c-109">Il file *servicedefinition.csdef* contiene la configurazione dell'endpoint e, se sono presenti più istanze per la distribuzione di un ruolo Web o di lavoro, il bilanciamento del carico verrà configurato di conseguenza.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-109">The *servicedefinition.csdef* file contains the endpoint configuration and when you have multiple role instances for a web or worker role deployment, the load balancer will be setup for it.</span></span> <span data-ttu-id="1eb3c-110">La modalità di aggiunta di istanze alla distribuzione cloud comporta la modifica del numero di istanze nel file di configurazione del servizio (con estensione csfg).</span><span class="sxs-lookup"><span data-stu-id="1eb3c-110">The way to add instances to your cloud deployment is changing the instance count on the service configuration file (.csfg).</span></span>

<span data-ttu-id="1eb3c-111">La figura seguente mostra un endpoint con carico bilanciato per il traffico Web condiviso tra tre macchine virtuali per la porta TCP 80, pubblica e privata.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-111">The following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for the public and private TCP port of 80.</span></span> <span data-ttu-id="1eb3c-112">Queste tre macchine virtuali appartengono a un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-112">These three virtual machines are in a load-balanced set.</span></span>

![esempio di bilanciamento del carico pubblico](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="1eb3c-114">Figura 1. Endpoint con bilanciamento del carico per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="1eb3c-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="1eb3c-115">Quando i client Internet inviano richieste di pagine Web all'indirizzo IP pubblico del servizio cloud sulla porta TCP 80, Azure Load Balancer distribuisce le richieste tra le tre macchine virtuali del set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-115">When Internet clients send web page requests to the public IP address of the cloud service on TCP port 80, the Azure Load Balancer distributes the requests between the three virtual machines in the load-balanced set.</span></span> <span data-ttu-id="1eb3c-116">Per altre informazioni sull'algoritmo di bilanciamento di carico, vedere la [pagina di panoramica del bilanciamento di carico](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="1eb3c-116">For more information about load balancer algorithms, see the [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="1eb3c-117">Per impostazione predefinita, Azure Load Balancer distribuisce il traffico di rete in modo uniforme tra più istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="1eb3c-118">È inoltre possibile configurare l'affinità di sessione. Per altre informazioni, vedere l'articolo [Modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="1eb3c-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eb3c-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1eb3c-119">Next steps</span></span>

<span data-ttu-id="1eb3c-120">Leggere le informazioni sul [bilanciamento del carico interno](load-balancer-internal-overview.md) per capire quale sia il bilanciamento del carico più adatto per la propria distribuzione cloud.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) to better understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="1eb3c-121">È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="1eb3c-122">Se l'applicazione deve mantenere attive le connessioni per i server dietro il servizio di bilanciamento del carico, è possibile ottenere altre informazioni sulle [impostazioni di timeout delle connessioni TCP inattive per un bilanciamento del carico](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="1eb3c-122">If your application needs to keep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="1eb3c-123">Ciò consente di ottenere informazioni sul comportamento delle connessioni inattive quando si usa il servizio di bilanciamento del carico di Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb3c-123">It will help to learn about idle connection behavior when you are using Azure Load Balancer.</span></span>
