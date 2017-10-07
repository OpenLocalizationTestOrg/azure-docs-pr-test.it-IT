---
title: supporto di gestione risorse di bilanciamento del carico aaaAzure | Documenti Microsoft
description: Usare PowerShell per il bilanciamento del carico con Azure Resource Manager. Uso di modelli per il bilanciamento del carico
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: d0394f11-ee5a-4407-9d86-79c936297265
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 3c02d9382de00fefe6af8f4f8a2b7b62b344f285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="1aded-104">Usare il supporto di Azure Resource Manager per Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="1aded-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="1aded-105">Gestione risorse di Azure è il framework di gestione Preferiti hello per servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="1aded-105">Azure Resource Manager is hello preferred management framework for services in Azure.</span></span> <span data-ttu-id="1aded-106">È ora possibile gestire Azure Load Balancer con API e strumenti basati su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="1aded-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="1aded-107">Concetti</span><span class="sxs-lookup"><span data-stu-id="1aded-107">Concepts</span></span>

<span data-ttu-id="1aded-108">Gestione risorse di bilanciamento del carico di Azure contiene hello risorse figlio seguenti:</span><span class="sxs-lookup"><span data-stu-id="1aded-108">With Resource Manager, Azure Load Balancer contains hello following child resources:</span></span>

* <span data-ttu-id="1aded-109">Configurazione IP front-end: un bilanciamento del carico può includere uno o più indirizzi IP front-end, anche noti come IP virtuali (indirizzi VIP).</span><span class="sxs-lookup"><span data-stu-id="1aded-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="1aded-110">In ingresso per il traffico hello fungono da questi indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="1aded-110">These IP addresses serve as ingress for hello traffic.</span></span>
* <span data-ttu-id="1aded-111">Pool di indirizzi di back-end: questi sono gli indirizzi IP associati alla macchina virtuale hello scheda interfaccia di rete (NIC) toowhich carico verrà distribuito.</span><span class="sxs-lookup"><span data-stu-id="1aded-111">Back-end address pool – these are IP addresses associated with hello virtual machine Network Interface Card (NIC) toowhich load will be distributed.</span></span>
* <span data-ttu-id="1aded-112">Regole di bilanciamento del carico: una proprietà della regola esegue il mapping di un indirizzo IP front-end specificato e porta set tooa combinazione di indirizzi IP back-end e combinazione di porta.</span><span class="sxs-lookup"><span data-stu-id="1aded-112">Load balancing rules – a rule property maps a given front end IP and port combination tooa set of back end IP addresses and port combination.</span></span> <span data-ttu-id="1aded-113">Un bilanciamento del carico singolo può avere più regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="1aded-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="1aded-114">Ogni regola è una combinazione di un IP e una porta front-end e un IP e una porta back-end associata alle VM.</span><span class="sxs-lookup"><span data-stu-id="1aded-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="1aded-115">Probe – probe abilitare si tookeep traccia dello stato di hello di istanze di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="1aded-115">Probes – probes enable you tookeep track of hello health of VM instances.</span></span> <span data-ttu-id="1aded-116">Se un probe di integrità non riesce, istanza di macchina virtuale hello verrà eseguita automaticamente dalla rotazione.</span><span class="sxs-lookup"><span data-stu-id="1aded-116">If a health probe fails, hello VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="1aded-117">Le regole NAT in ingresso: hello di regole NAT che definiscono il traffico in ingresso che passano attraverso IP front-end hello e distribuita toohello nuovamente IP finale.</span><span class="sxs-lookup"><span data-stu-id="1aded-117">Inbound NAT rules – NAT rules defining hello inbound traffic flowing through hello front end IP and distributed toohello back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="1aded-118">Modelli di Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="1aded-118">Quickstart templates</span></span>

<span data-ttu-id="1aded-119">Gestione risorse di Azure consente tooprovision delle applicazioni utilizzando un modello dichiarativo.</span><span class="sxs-lookup"><span data-stu-id="1aded-119">Azure Resource Manager allows you tooprovision your applications using a declarative template.</span></span> <span data-ttu-id="1aded-120">In un unico modello, è possibile distribuire più servizi con le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="1aded-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="1aded-121">Utilizzare hello stesso modello toorepeatedly distribuire l'applicazione durante ogni fase del ciclo di vita dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="1aded-121">You use hello same template toorepeatedly deploy your application during every stage of hello application lifecycle.</span></span>

<span data-ttu-id="1aded-122">I modelli possono includere definizioni per macchine virtuali, reti virtuali, set di disponibilità, interfacce di rete, account di archiviazione, bilanciamenti del carico, gruppi di sicurezza di rete e IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="1aded-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="1aded-123">Con i modelli è possibile creare tutto il necessario per un'applicazione complessa.</span><span class="sxs-lookup"><span data-stu-id="1aded-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="1aded-124">file di modello Hello possa essere verificato nel sistema di gestione dei contenuti per il controllo della versione e la collaborazione.</span><span class="sxs-lookup"><span data-stu-id="1aded-124">hello template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="1aded-125">Altre informazioni sui modelli</span><span class="sxs-lookup"><span data-stu-id="1aded-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="1aded-126">Altre informazioni sulle risorse di rete</span><span class="sxs-lookup"><span data-stu-id="1aded-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="1aded-127">I modelli di avvio rapido che usano Azure Load Balancer sono disponibili in un [repository GitHub](https://github.com/Azure/azure-quickstart-templates) che ospita un set di modelli generati dalla community.</span><span class="sxs-lookup"><span data-stu-id="1aded-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="1aded-128">Esempi di modelli:</span><span class="sxs-lookup"><span data-stu-id="1aded-128">Examples of templates:</span></span>

* [<span data-ttu-id="1aded-129">2 macchine virtuali in un bilanciamento del carico e regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1aded-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="1aded-130">2 macchine virtuali in una rete virtuale con un bilanciamento del carico interno e regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1aded-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="1aded-131">2 macchine virtuali in un bilanciamento del carico e configurare le regole NAT in hello LB</span><span class="sxs-lookup"><span data-stu-id="1aded-131">2 VMs in a Load Balancer and configure NAT rules on hello LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="1aded-132">Configurazione del bilanciamento del carico di Azure con PowerShell o l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="1aded-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="1aded-133">Introduzione ai cmdlet, agli strumenti da riga di comando e alle API REST di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="1aded-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="1aded-134">[Cmdlet di servizi di rete di Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) può essere utilizzato toocreate un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="1aded-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used toocreate a Load Balancer.</span></span>
* [<span data-ttu-id="1aded-135">Come toocreate un bilanciamento del carico con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1aded-135">How toocreate a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="1aded-136">Utilizzo di hello CLI di Azure con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1aded-136">Using hello Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="1aded-137">API REST di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="1aded-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="1aded-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1aded-138">Next steps</span></span>

<span data-ttu-id="1aded-139">È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="1aded-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="1aded-140">Informazioni su come toomanage [impostazioni di timeout TCP per un servizio di bilanciamento del carico di inattività](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="1aded-140">Learn how toomanage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="1aded-141">Questo è importante quando l'applicazione necessita di connessioni tookeep alive per i server di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="1aded-141">This is important when your application needs tookeep connections alive for servers behind a load balancer.</span></span>
