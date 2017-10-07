---
title: indirizzi di gestione dell'ambiente del servizio App aaaAzure
description: Gli indirizzi di gestione di elenchi hello utilizzati toocommand un ambiente del servizio App
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: a7738a24-89ef-43d3-bff1-77f43d5a3952
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: b34b6266dc3a35915421b14bf34eddc07c2825c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-management-addresses"></a><span data-ttu-id="41362-103">Indirizzi di gestione dell'Ambiente del servizio app</span><span class="sxs-lookup"><span data-stu-id="41362-103">App Service Environment management addresses</span></span>

<span data-ttu-id="41362-104">Hello Environment(ASE) di servizio App è una distribuzione di hello servizio App di Azure in una subnet nella rete virtuale di Azure (VNet).</span><span class="sxs-lookup"><span data-stu-id="41362-104">hello App Service Environment(ASE) is a deployment of hello Azure App Service into a subnet in your Azure Virtual Network (VNet).</span></span>  <span data-ttu-id="41362-105">Hello ASE deve essere accessibile da hello Azure App Service in modo che possa essere gestito.</span><span class="sxs-lookup"><span data-stu-id="41362-105">hello ASE must be accessible from hello Azure App Service so that it can be managed.</span></span>  <span data-ttu-id="41362-106">Il traffico di gestione di ASE attraversa rete controllata dall'utente hello.</span><span class="sxs-lookup"><span data-stu-id="41362-106">This ASE management traffic traverses hello user controlled network.</span></span>  <span data-ttu-id="41362-107">Proviene da Azure App Service management server toohello VIP pubblico associato ASE hello.</span><span class="sxs-lookup"><span data-stu-id="41362-107">It comes from Azure App Service management servers toohello public VIP that is associated with hello ASE.</span></span>  <span data-ttu-id="41362-108">Per informazioni dettagliate su hello ASE rete di dipendenze leggere [rete hello ambiente del servizio App e considerazioni sulla][networking].</span><span class="sxs-lookup"><span data-stu-id="41362-108">For details on hello ASE networking dependencies read [Networking considerations and hello App Service Environment][networking].</span></span>  <span data-ttu-id="41362-109">Per informazioni generali su ASE hello è possibile iniziare con [toohello introduzione ambiente del servizio App][intro].</span><span class="sxs-lookup"><span data-stu-id="41362-109">For general information on hello ASE you can start with [Introduction toohello App Service Environment][intro].</span></span>

<span data-ttu-id="41362-110">Questo documento vengono elencati gli IP di origine hello per gestione traffico toohello ASE.</span><span class="sxs-lookup"><span data-stu-id="41362-110">This document lists hello source IPs for management traffic toohello ASE.</span></span> <span data-ttu-id="41362-111">È possibile utilizzare questi toolock di gruppi di sicurezza di rete toocreate indirizzi il traffico in ingresso verso il basso o utilizzare in tabelle di routing in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="41362-111">You can use these addresses toocreate Network Security Groups toolock down incoming traffic or use them in Route Tables as needed.</span></span>  <span data-ttu-id="41362-112">toouse queste informazioni è necessario toouse:</span><span class="sxs-lookup"><span data-stu-id="41362-112">toouse this information you need toouse:</span></span>

* <span data-ttu-id="41362-113">indirizzi IP Hello elencati per tutte le aree</span><span class="sxs-lookup"><span data-stu-id="41362-113">hello IP addresses that are listed for All regions</span></span>
* <span data-ttu-id="41362-114">area che viene distribuito il ASE in toohello corrispondenza di indirizzi IP di Hello.</span><span class="sxs-lookup"><span data-stu-id="41362-114">hello IP addresses that match toohello region that your ASE is deployed into.</span></span>

<span data-ttu-id="41362-115">traffico di gestione Hello in arrivo provenienti da questi indirizzi IP tooports 454 e 455.</span><span class="sxs-lookup"><span data-stu-id="41362-115">hello incoming management traffic comes in from these IP addresses tooports 454 and 455.</span></span>

| <span data-ttu-id="41362-116">Region</span><span class="sxs-lookup"><span data-stu-id="41362-116">Region</span></span> | <span data-ttu-id="41362-117">Indirizzi</span><span class="sxs-lookup"><span data-stu-id="41362-117">Addresses</span></span> |
|--------|-----------|
| <span data-ttu-id="41362-118">Tutte le aree</span><span class="sxs-lookup"><span data-stu-id="41362-118">All regions</span></span> | <span data-ttu-id="41362-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span><span class="sxs-lookup"><span data-stu-id="41362-119">70.37.57.58, 157.55.208.185, 52.174.22.21,13.94.149.179,13.94.143.126,13.94.141.115, 52.178.195.197, 52.178.190.65, 52.178.184.149, 52.178.177.147, 13.75.127.117, 40.83.125.161, 40.83.121.56, 40.83.120.64, 52.187.56.50, 52.187.63.37, 52.187.59.251, 52.187.63.19, 52.165.158.140, 52.165.152.214, 52.165.154.193, 52.165.153.122, 104.44.129.255, 104.44.134.255, 104.44.129.243, 104.44.129.141</span></span> |
| <span data-ttu-id="41362-120">Stati Uniti centro-meridionali e Stati Uniti centro-settentrionali</span><span class="sxs-lookup"><span data-stu-id="41362-120">South Central US & North Central US</span></span> | <span data-ttu-id="41362-121">23.102.188.65, 191.236.154.88</span><span class="sxs-lookup"><span data-stu-id="41362-121">23.102.188.65, 191.236.154.88</span></span> |
| <span data-ttu-id="41362-122">Australia sudorientale e Australia orientale</span><span class="sxs-lookup"><span data-stu-id="41362-122">Australia Southeast & Australia East</span></span> | <span data-ttu-id="41362-123">23.101.234.41, 104.210.90.65</span><span class="sxs-lookup"><span data-stu-id="41362-123">23.101.234.41, 104.210.90.65</span></span> |
| <span data-ttu-id="41362-124">Stati Uniti occidentali e Stati Uniti orientali</span><span class="sxs-lookup"><span data-stu-id="41362-124">US West & US East</span></span> | <span data-ttu-id="41362-125">104.45.227.37, 191.236.60.72</span><span class="sxs-lookup"><span data-stu-id="41362-125">104.45.227.37, 191.236.60.72</span></span> |
| <span data-ttu-id="41362-126">Europa occidentale ed Europa settentrionale</span><span class="sxs-lookup"><span data-stu-id="41362-126">West Europe & North Europe</span></span> | <span data-ttu-id="41362-127">191.233.94.45, 191.237.222.191</span><span class="sxs-lookup"><span data-stu-id="41362-127">191.233.94.45, 191.237.222.191</span></span> |
| <span data-ttu-id="41362-128">Stati Uniti centro-occidentali e Stati Uniti occidentali 2</span><span class="sxs-lookup"><span data-stu-id="41362-128">West Central US & West US 2</span></span> | <span data-ttu-id="41362-129">13.78.148.75, 13.66.225.188</span><span class="sxs-lookup"><span data-stu-id="41362-129">13.78.148.75, 13.66.225.188</span></span> |
| <span data-ttu-id="41362-130">Stati Uniti centrali e Stati Uniti orientali 2</span><span class="sxs-lookup"><span data-stu-id="41362-130">Central US & East US 2</span></span> | <span data-ttu-id="41362-131">104.43.165.73, 104.46.108.135</span><span class="sxs-lookup"><span data-stu-id="41362-131">104.43.165.73, 104.46.108.135</span></span> |
| <span data-ttu-id="41362-132">Asia orientale e Asia sudorientale</span><span class="sxs-lookup"><span data-stu-id="41362-132">East Asia & Southeast Asia</span></span> | <span data-ttu-id="41362-133">23.99.115.5, 104.215.158.33</span><span class="sxs-lookup"><span data-stu-id="41362-133">23.99.115.5, 104.215.158.33</span></span> |
| <span data-ttu-id="41362-134">Giappone orientale e Giappone occidentale</span><span class="sxs-lookup"><span data-stu-id="41362-134">Japan East & Japan West</span></span> | <span data-ttu-id="41362-135">104.41.185.116, 191.239.104.48</span><span class="sxs-lookup"><span data-stu-id="41362-135">104.41.185.116, 191.239.104.48</span></span> |
| <span data-ttu-id="41362-136">Canada centrale e Canada orientale</span><span class="sxs-lookup"><span data-stu-id="41362-136">Canada Central & Canada East</span></span> | <span data-ttu-id="41362-137">40.85.230.101, 40.86.229.100</span><span class="sxs-lookup"><span data-stu-id="41362-137">40.85.230.101, 40.86.229.100</span></span> |
| <span data-ttu-id="41362-138">Regno Unito occidentale e Regno Unito meridionale</span><span class="sxs-lookup"><span data-stu-id="41362-138">UK West & UK South</span></span> | <span data-ttu-id="41362-139">51.141.8.34, 51.140.185.75</span><span class="sxs-lookup"><span data-stu-id="41362-139">51.141.8.34, 51.140.185.75</span></span> |
| <span data-ttu-id="41362-140">Corea meridionale e Corea centrale</span><span class="sxs-lookup"><span data-stu-id="41362-140">Korea South & Korea Central</span></span> | <span data-ttu-id="41362-141">52.231.200.177, 52.231.32.117</span><span class="sxs-lookup"><span data-stu-id="41362-141">52.231.200.177, 52.231.32.117</span></span> |
| <span data-ttu-id="41362-142">Brasile meridionale e Stati Uniti centro-meridionali</span><span class="sxs-lookup"><span data-stu-id="41362-142">Brazil South & South Central US</span></span>| <span data-ttu-id="41362-143">104.41.46.178, 23.102.188.65</span><span class="sxs-lookup"><span data-stu-id="41362-143">104.41.46.178, 23.102.188.65</span></span> |
| <span data-ttu-id="41362-144">India centrale e India meridionale</span><span class="sxs-lookup"><span data-stu-id="41362-144">Central India & South India</span></span> | <span data-ttu-id="41362-145">104.211.98.24, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="41362-145">104.211.98.24, 104.211.225.66</span></span> |
| <span data-ttu-id="41362-146">India occidentale e India meridionale</span><span class="sxs-lookup"><span data-stu-id="41362-146">West India & South India</span></span> | <span data-ttu-id="41362-147">104.211.160.229, 104.211.225.66</span><span class="sxs-lookup"><span data-stu-id="41362-147">104.211.160.229, 104.211.225.66</span></span> |


<!-- LINKS -->
[networking]: ./network-info.md
[intro]: ./intro.md
