---
title: Supporto di Azure Resource Manager per il bilanciamento del carico | Documentazione Microsoft
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
ms.openlocfilehash: d06c924f384a2684b5a91c202039c581796c1091
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-resource-manager-support-with-azure-load-balancer"></a><span data-ttu-id="d94d8-104">Usare il supporto di Azure Resource Manager per Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="d94d8-104">Using Azure Resource Manager Support with Azure Load Balancer</span></span>

<span data-ttu-id="d94d8-105">Azure Resource Manager è il framework di gestione preferito dei servizi in Azure.</span><span class="sxs-lookup"><span data-stu-id="d94d8-105">Azure Resource Manager is the preferred management framework for services in Azure.</span></span> <span data-ttu-id="d94d8-106">È ora possibile gestire Azure Load Balancer con API e strumenti basati su Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d94d8-106">Azure Load Balancer can be managed using Azure Resource Manager-based APIs and tools.</span></span>

## <a name="concepts"></a><span data-ttu-id="d94d8-107">Concetti</span><span class="sxs-lookup"><span data-stu-id="d94d8-107">Concepts</span></span>

<span data-ttu-id="d94d8-108">Con Resource Manager, Azure Load Balancer contiene le seguenti risorse figlio:</span><span class="sxs-lookup"><span data-stu-id="d94d8-108">With Resource Manager, Azure Load Balancer contains the following child resources:</span></span>

* <span data-ttu-id="d94d8-109">Configurazione IP front-end: un bilanciamento del carico può includere uno o più indirizzi IP front-end, anche noti come IP virtuali (indirizzi VIP).</span><span class="sxs-lookup"><span data-stu-id="d94d8-109">Front-end IP configuration – a Load balancer can include one or more front end IP addresses, otherwise known as a virtual IPs (VIPs).</span></span> <span data-ttu-id="d94d8-110">Questi indirizzi IP vengono usati come ingresso per il traffico.</span><span class="sxs-lookup"><span data-stu-id="d94d8-110">These IP addresses serve as ingress for the traffic.</span></span>
* <span data-ttu-id="d94d8-111">Pool di indirizzi back-end: indirizzi IP associati alle schede di interfaccia di rete della macchina virtuale a cui viene distribuito il carico.</span><span class="sxs-lookup"><span data-stu-id="d94d8-111">Back-end address pool – these are IP addresses associated with the virtual machine Network Interface Card (NIC) to which load will be distributed.</span></span>
* <span data-ttu-id="d94d8-112">Regole di bilanciamento del carico: una proprietà della regola esegue il mapping di una specifica combinazione di IP e porte front-end a un set di combinazioni di indirizzi IP e porte back-end.</span><span class="sxs-lookup"><span data-stu-id="d94d8-112">Load balancing rules – a rule property maps a given front end IP and port combination to a set of back end IP addresses and port combination.</span></span> <span data-ttu-id="d94d8-113">Un bilanciamento del carico singolo può avere più regole di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d94d8-113">A single load balancer can have multiple load balancing rules.</span></span> <span data-ttu-id="d94d8-114">Ogni regola è una combinazione di un IP e una porta front-end e un IP e una porta back-end associata alle VM.</span><span class="sxs-lookup"><span data-stu-id="d94d8-114">Each rule is a combination of a front-end IP and port and back-end IP and port associated with VMs.</span></span>
* <span data-ttu-id="d94d8-115">Probe: le probe consentono di tenere traccia dell'integrità delle istanze della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d94d8-115">Probes – probes enable you to keep track of the health of VM instances.</span></span> <span data-ttu-id="d94d8-116">Se la probe di integrità non riesce, l'istanza della macchina virtuale viene esclusa automaticamente dalla rotazione.</span><span class="sxs-lookup"><span data-stu-id="d94d8-116">If a health probe fails, the VM instance will be taken out of rotation automatically.</span></span>
* <span data-ttu-id="d94d8-117">Regole NAT in ingresso: regole NAT che definiscono il traffico in ingresso che attraversa l'IP front-end e viene distribuito all'IP back-end.</span><span class="sxs-lookup"><span data-stu-id="d94d8-117">Inbound NAT rules – NAT rules defining the inbound traffic flowing through the front end IP and distributed to the back end IP.</span></span>

![](./media/load-balancer-arm/load-balancer-arm.png)

## <a name="quickstart-templates"></a><span data-ttu-id="d94d8-118">Modelli di Guida introduttiva</span><span class="sxs-lookup"><span data-stu-id="d94d8-118">Quickstart templates</span></span>

<span data-ttu-id="d94d8-119">Gestione risorse di Azure consente di effettuare il provisioning delle applicazioni usando un modello dichiarativo.</span><span class="sxs-lookup"><span data-stu-id="d94d8-119">Azure Resource Manager allows you to provision your applications using a declarative template.</span></span> <span data-ttu-id="d94d8-120">In un unico modello, è possibile distribuire più servizi con le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d94d8-120">In a single template, you can deploy multiple services along with their dependencies.</span></span> <span data-ttu-id="d94d8-121">Si usa lo stesso modello per distribuire più volte l'applicazione durante ogni fase del ciclo di vita dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d94d8-121">You use the same template to repeatedly deploy your application during every stage of the application lifecycle.</span></span>

<span data-ttu-id="d94d8-122">I modelli possono includere definizioni per macchine virtuali, reti virtuali, set di disponibilità, interfacce di rete, account di archiviazione, bilanciamenti del carico, gruppi di sicurezza di rete e IP pubblici.</span><span class="sxs-lookup"><span data-stu-id="d94d8-122">Templates can include definitions for Virtual Machines, Virtual Networks, Availability Sets, Network Interfaces (NICs), Storage Accounts, Load Balancers, Network Security Groups, and Public IPs.</span></span> <span data-ttu-id="d94d8-123">Con i modelli è possibile creare tutto il necessario per un'applicazione complessa.</span><span class="sxs-lookup"><span data-stu-id="d94d8-123">With templates you can create everything you need for a complex application.</span></span> <span data-ttu-id="d94d8-124">Il file modello può essere verificato nel sistema di gestione dei contenuti per il controllo della versione e la collaborazione.</span><span class="sxs-lookup"><span data-stu-id="d94d8-124">The template file can be checked into content management system for version control and collaboration.</span></span>

[<span data-ttu-id="d94d8-125">Altre informazioni sui modelli</span><span class="sxs-lookup"><span data-stu-id="d94d8-125">Learn more about templates</span></span>](../azure-resource-manager/resource-manager-template-walkthrough.md)

[<span data-ttu-id="d94d8-126">Altre informazioni sulle risorse di rete</span><span class="sxs-lookup"><span data-stu-id="d94d8-126">Learn more about Network Resources</span></span>](../virtual-network/resource-groups-networking.md)

<span data-ttu-id="d94d8-127">I modelli di avvio rapido che usano Azure Load Balancer sono disponibili in un [repository GitHub](https://github.com/Azure/azure-quickstart-templates) che ospita un set di modelli generati dalla community.</span><span class="sxs-lookup"><span data-stu-id="d94d8-127">Quickstart templates using Azure Load Balancer can be found in a [GitHub repository](https://github.com/Azure/azure-quickstart-templates) hosting a set of community generated templates.</span></span>

<span data-ttu-id="d94d8-128">Esempi di modelli:</span><span class="sxs-lookup"><span data-stu-id="d94d8-128">Examples of templates:</span></span>

* [<span data-ttu-id="d94d8-129">2 macchine virtuali in un bilanciamento del carico e regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d94d8-129">2 VMs in a Load Balancer and load balancing rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544799)
* [<span data-ttu-id="d94d8-130">2 macchine virtuali in una rete virtuale con un bilanciamento del carico interno e regole di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d94d8-130">2 VMs in a VNET with an Internal Load Balancer and Load Balancer rules</span></span>](http://go.microsoft.com/fwlink/?LinkId=544800)
* [<span data-ttu-id="d94d8-131">2 macchine virtuali in un bilanciamento del carico e regole NAT di configurazione per il bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d94d8-131">2 VMs in a Load Balancer and configure NAT rules on the LB</span></span>](http://go.microsoft.com/fwlink/?LinkId=544801)

## <a name="setting-up-azure-load-balancer-with-a-powershell-or-cli"></a><span data-ttu-id="d94d8-132">Configurazione del bilanciamento del carico di Azure con PowerShell o l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="d94d8-132">Setting up Azure Load Balancer with a PowerShell or CLI</span></span>

<span data-ttu-id="d94d8-133">Introduzione ai cmdlet, agli strumenti da riga di comando e alle API REST di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d94d8-133">Get started with Azure Resource Manager cmdlets, command line tools, and REST APIs</span></span>

* <span data-ttu-id="d94d8-134">[cmdlet di rete di Azure](https://msdn.microsoft.com/library/azure/mt163510.aspx) possono essere usati per creare un bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d94d8-134">[Azure Networking Cmdlets](https://msdn.microsoft.com/library/azure/mt163510.aspx) can be used to create a Load Balancer.</span></span>
* [<span data-ttu-id="d94d8-135">Come creare un servizio di bilanciamento del carico tramite Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d94d8-135">How to create a load balancer using Azure Resource Manager</span></span>](load-balancer-get-started-ilb-arm-ps.md)
* [<span data-ttu-id="d94d8-136">Uso dell'interfaccia della riga di comando di Azure con Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d94d8-136">Using the Azure CLI with Azure Resource Management</span></span>](../xplat-cli-azure-resource-manager.md)
* [<span data-ttu-id="d94d8-137">API REST di bilanciamento del carico</span><span class="sxs-lookup"><span data-stu-id="d94d8-137">Load Balancer REST APIs</span></span>](https://msdn.microsoft.com/library/azure/mt163651.aspx)

## <a name="next-steps"></a><span data-ttu-id="d94d8-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d94d8-138">Next steps</span></span>

<span data-ttu-id="d94d8-139">È anche possibile [iniziare a creare un bilanciamento del carico con connessione Internet](load-balancer-get-started-internet-arm-ps.md) e configurare il tipo di [modalità di distribuzione](load-balancer-distribution-mode.md) per il comportamento specifico del traffico di rete per il bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d94d8-139">You can also [get started creating an Internet facing load balancer](load-balancer-get-started-internet-arm-ps.md) and configure what type of [distribution mode](load-balancer-distribution-mode.md) for a specific load balancer network traffic behavior.</span></span>

<span data-ttu-id="d94d8-140">Informazioni su come gestire [le impostazioni del timeout di inattività TCP per il bilanciamento del carico](load-balancer-tcp-idle-timeout.md).</span><span class="sxs-lookup"><span data-stu-id="d94d8-140">Learn how to manage [idle TCP timeout settings for a load balancer](load-balancer-tcp-idle-timeout.md).</span></span> <span data-ttu-id="d94d8-141">Questo è importante quando l'applicazione deve mantenere le connessioni attive per i server di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="d94d8-141">This is important when your application needs to keep connections alive for servers behind a load balancer.</span></span>
