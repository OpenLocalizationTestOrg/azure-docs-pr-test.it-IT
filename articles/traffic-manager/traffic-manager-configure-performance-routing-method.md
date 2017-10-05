---
title: Configurare un metodo di routing del traffico delle prestazioni con Gestione traffico di Azure | Microsoft Docs
description: "Questo articolo descrive come configurare Gestione traffico per instradare il traffico all'endpoint con latenza più bassa"
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 014aa646459cd64fca7c697419324caa3edaeeea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-performance-traffic-routing-method"></a><span data-ttu-id="5a025-103">Configurare un metodo di routing del traffico delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="5a025-103">Configure the performance traffic routing method</span></span>

<span data-ttu-id="5a025-104">Il metodo di routing del traffico Prestazioni consente di indirizzare il traffico all'endpoint con latenza più bassa dalla rete del client.</span><span class="sxs-lookup"><span data-stu-id="5a025-104">The Performance traffic routing method allows you to direct traffic to the endpoint with the lowest latency from the client's network.</span></span> <span data-ttu-id="5a025-105">In genere, il data center con latenza più bassa è quello più vicino in termini di distanza geografica.</span><span class="sxs-lookup"><span data-stu-id="5a025-105">Typically, the datacenter with the lowest latency is the closest in geographic distance.</span></span> <span data-ttu-id="5a025-106">Questo metodo di routing del traffico non può basarsi per le modifiche in tempo reale sul carico o sulla configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="5a025-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="to-configure-performance-routing-method"></a><span data-ttu-id="5a025-107">Per configurare un metodo di routing del traffico delle prestazioni</span><span class="sxs-lookup"><span data-stu-id="5a025-107">To configure performance routing method</span></span>

1. <span data-ttu-id="5a025-108">In un browser accedere al [portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5a025-108">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="5a025-109">Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="5a025-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="5a025-110">Nella barra di ricerca del portale cercare i **profili di Gestione traffico** e quindi fare clic sul nome di profilo per cui si vuole configurare il metodo.</span><span class="sxs-lookup"><span data-stu-id="5a025-110">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="5a025-111">Nel pannello **Profilo di Gestione traffico** verificare che siano presenti sia i servizi cloud che i siti Web che si intende includere nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="5a025-111">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="5a025-112">Nella sezione **Impostazioni** fare clic su **Configurazione** e nel pannello **Configurazione** procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5a025-112">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="5a025-113">Nelle **impostazioni del metodo di routing del traffico** per **Metodo di routing** selezionare **Prestazioni**.</span><span class="sxs-lookup"><span data-stu-id="5a025-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="5a025-114">Specificare le stesse le stesse **impostazioni di monitoraggio degli endpoint** per tutti gli endpoint in questo profilo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5a025-114">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="5a025-115">Selezionare il **protocollo** appropriato e specificare il numero di **porta**.</span><span class="sxs-lookup"><span data-stu-id="5a025-115">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="5a025-116">In **Percorso** immettere una barra */*.</span><span class="sxs-lookup"><span data-stu-id="5a025-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="5a025-117">Per monitorare gli endpoint, è necessario specificare un percorso e un nome file.</span><span class="sxs-lookup"><span data-stu-id="5a025-117">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="5a025-118">Una barra ("/") è una voce valida per il percorso relativo e implica che il file si trovi nella directory radice (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="5a025-118">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="5a025-119">Nella parte superiore della pagina fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="5a025-119">At the top of the page, click **Save**.</span></span>
5.  <span data-ttu-id="5a025-120">Verificare le modifiche apportate alla configurazione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="5a025-120">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="5a025-121">Nella barra di ricerca del portale cercare il nome del profilo di Gestione traffico e fare clic su tale profilo nei risultati visualizzati.</span><span class="sxs-lookup"><span data-stu-id="5a025-121">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="5a025-122">Nel pannello **Profilo di Gestione traffico** fare clic su **Informazioni generali**.</span><span class="sxs-lookup"><span data-stu-id="5a025-122">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="5a025-123">Nel pannello **Profilo di Gestione traffico** viene visualizzato il nome DNS del profilo di Gestione traffico creato.</span><span class="sxs-lookup"><span data-stu-id="5a025-123">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="5a025-124">Questo nome può essere usato da qualsiasi client (ad esempio accedendovi tramite un Web browser) per essere indirizzato all'endpoint corretto in base al tipo di routing.</span><span class="sxs-lookup"><span data-stu-id="5a025-124">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="5a025-125">In questo caso tutte le richieste vengono indirizzate all'endpoint con latenza più bassa dalla rete del client.</span><span class="sxs-lookup"><span data-stu-id="5a025-125">In this case all requests are routed to the endpoint with the lowest latency from the client's network.</span></span>
6. <span data-ttu-id="5a025-126">Dopo aver verificato il funzionamento del profilo di Gestione traffico, modificare il record DNS sul server DNS autorevole per fare in modo che il nome del dominio aziendale punti al nome di dominio di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="5a025-126">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Configurazione del metodo di routing del traffico delle prestazioni con Gestione traffico][1]

## <a name="next-steps"></a><span data-ttu-id="5a025-128">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5a025-128">Next steps</span></span>

- <span data-ttu-id="5a025-129">Informazioni sul [metodo di routing del traffico Ponderato](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="5a025-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="5a025-130">Informazioni sul [metodo di routing Priorità](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="5a025-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="5a025-131">Informazioni sul [metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="5a025-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="5a025-132">Informazioni su come [testare le impostazioni di Gestione traffico](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="5a025-132">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png