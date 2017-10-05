---
title: Configurare il metodo di routing del traffico Round robin ponderato tramite Gestione traffico di Azure | Microsoft Docs
description: In questo articolo viene illustrato come bilanciare il carico del traffico con un metodo Round robin in Gestione traffico
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
ms.openlocfilehash: 7aa4c9120d44ff1b3e59a57090ea04e3f8021fc4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="07348-103">Configurare il metodo di routing del traffico Ponderato in Gestione traffico</span><span class="sxs-lookup"><span data-stu-id="07348-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="07348-104">Un modello comune di metodo di routing del traffico consiste nel fornire un set di endpoint identici, che includono servizi cloud e siti Web, e nell'inviare traffico a ciascuno di essi in base a uno schema round robin.</span><span class="sxs-lookup"><span data-stu-id="07348-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="07348-105">I passaggi seguenti illustrano come configurare questo tipo di metodo di routing del traffico.</span><span class="sxs-lookup"><span data-stu-id="07348-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="07348-106">Siti Web di Azure offre già funzionalità di bilanciamento del carico round robin per i siti Web che si trovano all'interno di un data center (nota anche come area).</span><span class="sxs-lookup"><span data-stu-id="07348-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="07348-107">Gestione traffico consente di specificare il metodo di routing del traffico round-robin per i siti web che si trovano in data center diversi.</span><span class="sxs-lookup"><span data-stu-id="07348-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="07348-108">Per configurare il metodo di routing del traffico Ponderato</span><span class="sxs-lookup"><span data-stu-id="07348-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="07348-109">Da un browser accedere al [Portale di Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="07348-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="07348-110">Se non si ha già di un account, è possibile iscriversi per ottenere una [versione di valutazione gratuita della durata di un mese](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="07348-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="07348-111">Nella barra di ricerca del portale cercare i **profili di Gestione traffico** e quindi fare clic sul nome di profilo per cui si vuole configurare il metodo.</span><span class="sxs-lookup"><span data-stu-id="07348-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="07348-112">Nel pannello **Profilo di Gestione traffico** verificare che siano presenti sia i servizi cloud che i siti Web che si intende includere nella configurazione.</span><span class="sxs-lookup"><span data-stu-id="07348-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="07348-113">Nella sezione **Impostazioni** fare clic su **Configurazione** e nel pannello **Configurazione** procedere come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="07348-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="07348-114">In **Metodo di routing del traffico** verificare che il metodo di routing del traffico sia impostato su **Ponderato**.</span><span class="sxs-lookup"><span data-stu-id="07348-114">For **traffic routing method settings**, verify that the traffic routing method is **Weighted**.</span></span> <span data-ttu-id="07348-115">In caso contrario, fare clic su **Ponderato** nell'elenco a discesa.</span><span class="sxs-lookup"><span data-stu-id="07348-115">If it is not, click **Weighted** from the dropdown list.</span></span>
    2. <span data-ttu-id="07348-116">Specificare le stesse le stesse **impostazioni di monitoraggio degli endpoint** per tutti gli endpoint in questo profilo come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="07348-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="07348-117">Selezionare il **protocollo** appropriato e specificare il numero di **porta**.</span><span class="sxs-lookup"><span data-stu-id="07348-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="07348-118">In **Percorso** immettere una barra */*.</span><span class="sxs-lookup"><span data-stu-id="07348-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="07348-119">Per monitorare gli endpoint, è necessario specificare un percorso e un nome file.</span><span class="sxs-lookup"><span data-stu-id="07348-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="07348-120">Una barra ("/") è una voce valida per il percorso relativo e implica che il file si trovi nella directory radice (impostazione predefinita).</span><span class="sxs-lookup"><span data-stu-id="07348-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="07348-121">Nella parte superiore della pagina fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="07348-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="07348-122">Verificare le modifiche apportate alla configurazione come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="07348-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="07348-123">Nella barra di ricerca del portale cercare il nome del profilo di Gestione traffico e fare clic su tale profilo nei risultati visualizzati.</span><span class="sxs-lookup"><span data-stu-id="07348-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="07348-124">Nel pannello **Profilo di Gestione traffico** fare clic su **Informazioni generali**.</span><span class="sxs-lookup"><span data-stu-id="07348-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="07348-125">Il pannello **Profilo di Gestione traffico** visualizza il nome DNS del profilo di Gestione traffico appena creato.</span><span class="sxs-lookup"><span data-stu-id="07348-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="07348-126">Questo nome può essere usato da qualsiasi client (ad esempio raggiungendolo tramite un Web browser) che deve essere indirizzato all'endpoint corretto in base al tipo di routing.</span><span class="sxs-lookup"><span data-stu-id="07348-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="07348-127">In questo caso tutte le richieste vengono instradate a ogni endpoint secondo il metodo Round robin.</span><span class="sxs-lookup"><span data-stu-id="07348-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="07348-128">Dopo aver verificato il funzionamento del profilo di Gestione traffico, modificare il record DNS sul server DNS autorevole per fare in modo che il nome del dominio aziendale punti al nome di dominio di Gestione traffico.</span><span class="sxs-lookup"><span data-stu-id="07348-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Configurare il metodo di routing del traffico Ponderato in Gestione traffico][1]

## <a name="next-steps"></a><span data-ttu-id="07348-130">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="07348-130">Next steps</span></span>

- <span data-ttu-id="07348-131">Informazioni sul [metodo di routing del traffico Priorità](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="07348-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="07348-132">Informazioni sul [metodo di routing del traffico Prestazioni](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="07348-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="07348-133">Informazioni sul [metodo di routing Geografico](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="07348-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="07348-134">Informazioni su come [testare le impostazioni di Gestione traffico](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="07348-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: ./media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png
