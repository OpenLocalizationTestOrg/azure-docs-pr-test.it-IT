---
title: aaaInternet affiancate Panoramica del servizio di bilanciamento del carico | Documenti Microsoft
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
ms.openlocfilehash: 3514f945d69ec576ed256cdd01069491e3e43936
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="internet-facing-load-balancer-overview"></a><span data-ttu-id="311d3-104">Panoramica del bilanciamento del carico Internet</span><span class="sxs-lookup"><span data-stu-id="311d3-104">Internet facing load balancer overview</span></span>

<span data-ttu-id="311d3-105">Servizio di bilanciamento del carico di Azure esegue il mapping hello pubblica IP indirizzo numero di porta e in ingresso traffico toohello privato IP indirizzo e numero di porta della macchina virtuale hello e viceversa per il traffico di risposta hello dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-105">Azure load balancer maps hello public IP address and port number of incoming traffic toohello private IP address and port number of hello virtual machine and vice versa for hello response traffic from hello virtual machine.</span></span> <span data-ttu-id="311d3-106">Regole di bilanciamento del carico consentono di toodistribute specifici tipi di traffico tra più macchine virtuali o servizi.</span><span class="sxs-lookup"><span data-stu-id="311d3-106">Load balancing rules allow you toodistribute specific types of traffic between multiple virtual machines or services.</span></span> <span data-ttu-id="311d3-107">Ad esempio, è possibile distribuire il carico di hello del traffico di richiesta web in più server web o ruoli web.</span><span class="sxs-lookup"><span data-stu-id="311d3-107">For example, you can spread hello load of web request traffic across multiple web servers or web roles.</span></span>

<span data-ttu-id="311d3-108">Per un servizio cloud contenente istanze di ruoli web o ruoli di lavoro, è possibile definire un endpoint pubblico nel file di definizione (con estensione csdef) servizio hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-108">For a cloud service that contains instances of web roles or worker roles, you can define a public endpoint in hello service definition (.csdef) file.</span></span>

<span data-ttu-id="311d3-109">Hello *servicedefinition* file contiene la configurazione di endpoint hello e quando si dispone di più istanze del ruolo per una distribuzione di ruolo web o di lavoro, bilanciamento del carico hello verrà configurato appositamente.</span><span class="sxs-lookup"><span data-stu-id="311d3-109">hello *servicedefinition.csdef* file contains hello endpoint configuration and when you have multiple role instances for a web or worker role deployment, hello load balancer will be setup for it.</span></span> <span data-ttu-id="311d3-110">distribuzione del cloud tooyour Hello modo tooadd istanze è Modifica numero di istanze di hello nel file di configurazione del servizio hello (con estensione csfg).</span><span class="sxs-lookup"><span data-stu-id="311d3-110">hello way tooadd instances tooyour cloud deployment is changing hello instance count on hello service configuration file (.csfg).</span></span>

<span data-ttu-id="311d3-111">Hello figura riportata di seguito viene illustrato un endpoint con bilanciamento del carico per il traffico web che viene condiviso tra tre macchine virtuali per hello porta pubblica e privata TCP 80.</span><span class="sxs-lookup"><span data-stu-id="311d3-111">hello following figure shows a load-balanced endpoint for web traffic that is shared among three virtual machines for hello public and private TCP port of 80.</span></span> <span data-ttu-id="311d3-112">Queste tre macchine virtuali appartengono a un set con carico bilanciato.</span><span class="sxs-lookup"><span data-stu-id="311d3-112">These three virtual machines are in a load-balanced set.</span></span>

![esempio di bilanciamento del carico pubblico](./media/load-balancer-internet-overview/IC727496.png)

<span data-ttu-id="311d3-114">Figura 1. Endpoint con bilanciamento del carico per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="311d3-114">Figure 1 - Load-balanced endpoint for web traffic</span></span>

<span data-ttu-id="311d3-115">Quando i client Internet inviano richieste di pagine web toohello indirizzo IP pubblico del servizio cloud hello sulla porta TCP 80, hello bilanciamento del carico di Azure distribuisce le richieste di hello tra hello tre macchine virtuali nel set di bilanciamento del carico hello.</span><span class="sxs-lookup"><span data-stu-id="311d3-115">When Internet clients send web page requests toohello public IP address of hello cloud service on TCP port 80, hello Azure Load Balancer distributes hello requests between hello three virtual machines in hello load-balanced set.</span></span> <span data-ttu-id="311d3-116">Per ulteriori informazioni sugli algoritmi di bilanciamento di carico, vedere hello [pagina Panoramica di bilanciamento carico](load-balancer-overview.md#load-balancer-features).</span><span class="sxs-lookup"><span data-stu-id="311d3-116">For more information about load balancer algorithms, see hello [load balancer overview page](load-balancer-overview.md#load-balancer-features).</span></span>

<span data-ttu-id="311d3-117">Per impostazione predefinita, Azure Load Balancer distribuisce il traffico di rete in modo uniforme tra più istanze di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="311d3-117">By default, Azure Load Balancer distributes network traffic equally among multiple virtual machine instances.</span></span> <span data-ttu-id="311d3-118">È inoltre possibile configurare l'affinità di sessione. Per altre informazioni, vedere l'articolo [Modalità di distribuzione del servizio di bilanciamento del carico](load-balancer-distribution-mode.md).</span><span class="sxs-lookup"><span data-stu-id="311d3-118">You can also configure session affinity, For more information, see [load balancer distribution mode](load-balancer-distribution-mode.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="311d3-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="311d3-119">Next steps</span></span>

<span data-ttu-id="311d3-120">Informazioni su [bilanciamento del carico interno](load-balancer-internal-overview.md) toobetter capire quale servizio di bilanciamento del carico è una soluzione migliore per la distribuzione cloud.</span><span class="sxs-lookup"><span data-stu-id="311d3-120">Learn about [Internal load balancer](load-balancer-internal-overview.md) toobetter understand which load balancer is a better fit for your cloud deployment.</span></span>

<span data-ttu-id="311d3-121">È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="311d3-121">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for an specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="311d3-122">Se l'applicazione deve tookeep connessioni attive per i server di bilanciamento del carico, è possibile comprendere più su [impostazioni di timeout TCP per un servizio di bilanciamento del carico di inattività](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="311d3-122">If your application needs tookeep connections alive for servers behind a load balancer, you can understand more about [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="311d3-123">Quando si utilizza Bilanciamento carico di Azure, questo risulterà utile toolearn sul comportamento di connessione inattiva.</span><span class="sxs-lookup"><span data-stu-id="311d3-123">It will help toolearn about idle connection behavior when you are using Azure Load Balancer.</span></span>
