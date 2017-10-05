---
title: Filtri connessioni IP dell'hub IoT di Azure | Microsoft Docs
description: "Come usare i filtri IP per bloccare le connessioni da indirizzi IP specifici all'hub IoT di Azure. È possibile bloccare le connessioni da singoli indirizzi IP o da intervalli di indirizzi IP."
services: iot-hub
documentationcenter: 
author: BeatriceOltean
manager: timlt
editor: 
ms.assetid: f833eac3-5b5f-46a7-a47b-f4f6fc927f3f
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/23/2017
ms.author: boltean
ms.openlocfilehash: 85f5f044faddd5180f0c19d3f2c235b20f6373d5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="8d978-104">Usare i filtri IP</span><span class="sxs-lookup"><span data-stu-id="8d978-104">Use IP filters</span></span>

<span data-ttu-id="8d978-105">La sicurezza è un aspetto importante di qualsiasi soluzione IoT basata su un hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="8d978-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="8d978-106">Talvolta è necessario specificare in modo esplicito gli indirizzi IP da cui possono connettersi i dispositivi come parte della configurazione di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="8d978-106">Sometimes you need to explicitly specify the IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="8d978-107">La funzionalità _Filtro IP_ consente di configurare regole per rifiutare o accettare il traffico da specifici indirizzi IPv4.</span><span class="sxs-lookup"><span data-stu-id="8d978-107">The _IP filter_ feature enables you to configure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-to-use"></a><span data-ttu-id="8d978-108">Quando usare le autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="8d978-108">When to use</span></span>

<span data-ttu-id="8d978-109">Esistono due casi d'uso specifici in cui è utile bloccare gli endpoint dell'hub IoT per determinati indirizzi IP:</span><span class="sxs-lookup"><span data-stu-id="8d978-109">There are two specific use-cases when it is useful to block the IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="8d978-110">L'hub IoT deve ricevere il traffico solo da un intervallo di indirizzi IP specificato e rifiutare tutto il resto.</span><span class="sxs-lookup"><span data-stu-id="8d978-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="8d978-111">Si usa ad esempio l'hub IoT con [Azure ExpressRoute] per creare connessioni private tra un hub IoT e l'infrastruttura locale.</span><span class="sxs-lookup"><span data-stu-id="8d978-111">For example, you are using your IoT hub with [Azure Express Route] to create private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="8d978-112">È necessario rifiutare il traffico proveniente da indirizzi IP identificati come sospetti dall'amministratore dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8d978-112">You need to reject traffic from IP addresses that have been identified as suspicious by the IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="8d978-113">Come vengono applicate le regole di filtro</span><span class="sxs-lookup"><span data-stu-id="8d978-113">How filter rules are applied</span></span>

<span data-ttu-id="8d978-114">Le regole del filtro IP vengono applicate a livello del servizio dell'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8d978-114">The IP filter rules are applied at the IoT Hub service level.</span></span> <span data-ttu-id="8d978-115">Le regole del filtro IP vengono quindi applicate a tutte le connessioni provenienti dai dispositivi e dalle app back-end con qualsiasi protocollo supportato.</span><span class="sxs-lookup"><span data-stu-id="8d978-115">Therefore the IP filter rules apply to all connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="8d978-116">Qualsiasi tentativo di connessione da un indirizzo IP corrispondente a una regola di rifiuto nell'hub IoT riceve un codice di stato 401 - Non autorizzato e la descrizione.</span><span class="sxs-lookup"><span data-stu-id="8d978-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="8d978-117">Il messaggio di risposta non indica la regola IP.</span><span class="sxs-lookup"><span data-stu-id="8d978-117">The response message does not mention the IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="8d978-118">Impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="8d978-118">Default setting</span></span>

<span data-ttu-id="8d978-119">Per impostazione predefinita, la griglia **Filtro IP** nel portale di un hub IoT è vuota.</span><span class="sxs-lookup"><span data-stu-id="8d978-119">By default, the **IP Filter** grid in the portal for an IoT hub is empty.</span></span> <span data-ttu-id="8d978-120">Questa impostazione predefinita indica che l'hub accetta connessioni da qualsiasi indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="8d978-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="8d978-121">Questa impostazione predefinita equivale a una regola che accetta l'intervallo di indirizzi IP 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="8d978-121">This default setting is equivalent to a rule that accepts the 0.0.0.0/0 IP address range.</span></span>

![Impostazioni predefinite del filtro IP dell'hub IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="8d978-123">Aggiungere o modificare una regola del filtro IP</span><span class="sxs-lookup"><span data-stu-id="8d978-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="8d978-124">Quando si aggiunge una regola del filtro IP, vengono richiesti i valori seguenti:</span><span class="sxs-lookup"><span data-stu-id="8d978-124">When you add an IP filter rule, you are prompted for the following values:</span></span>

- <span data-ttu-id="8d978-125">Un **nome della regola del filtro IP** che deve essere una stringa univoca, senza distinzione tra maiuscole e minuscole e alfanumerica con un massimo di 128 caratteri.</span><span class="sxs-lookup"><span data-stu-id="8d978-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up to 128 characters long.</span></span> <span data-ttu-id="8d978-126">Sono ammessi solo caratteri alfanumerici ASCII a 7 bit più `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}`.</span><span class="sxs-lookup"><span data-stu-id="8d978-126">Only the ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="8d978-127">Selezionare il **rifiuto** o l'**accettazione** come **azione** per la regola del filtro IP.</span><span class="sxs-lookup"><span data-stu-id="8d978-127">Select a **reject** or **accept** as the **action** for the IP filter rule.</span></span>
- <span data-ttu-id="8d978-128">Specificare un singolo indirizzo IPv4 o un blocco di indirizzi IP in notazione CIDR.</span><span class="sxs-lookup"><span data-stu-id="8d978-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="8d978-129">In notazione CIDR, ad esempio, 192.168.100.0/22 rappresenta gli indirizzi IPv4 1024 da 192.168.100.0 a 192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="8d978-129">For example, in CIDR notation 192.168.100.0/22 represents the 1024 IPv4 addresses from 192.168.100.0 to 192.168.103.255.</span></span>

![Aggiungere una regola di filtro IP a un hub IoT][img-ip-filter-add-rule]

<span data-ttu-id="8d978-131">Dopo aver salvato la regola viene visualizzato un avviso che informa che l'aggiornamento è in corso.</span><span class="sxs-lookup"><span data-stu-id="8d978-131">After you save the rule, you see an alert notifying you that the update is in progress.</span></span>

![Notifica sul salvataggio di una regola di filtro IP][img-ip-filter-save-new-rule]

<span data-ttu-id="8d978-133">L'opzione **Aggiungi** è disabilitata quando si raggiunge il numero massimo di dieci regole del filtro IP.</span><span class="sxs-lookup"><span data-stu-id="8d978-133">The **Add** option is disabled when you reach the maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="8d978-134">È possibile modificare una regola esistente facendo doppio clic sulla riga corrispondente.</span><span class="sxs-lookup"><span data-stu-id="8d978-134">You can edit an existing rule by double-clicking the row that contains the rule.</span></span>

> [!NOTE]
> <span data-ttu-id="8d978-135">Il rifiuto di indirizzi IP può impedire l'interazione di altri servizi di Azure (ad esempio Analisi di flusso di Azure, Macchine virtuali di Azure o Device Explorer nel portale) con l'hub IoT.</span><span class="sxs-lookup"><span data-stu-id="8d978-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or the Device Explorer in the portal) from interacting with the IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="8d978-136">Se si usa Analisi di flusso di Azure (ASA) per leggere i messaggi da un hub IoT con i filtri IP abilitati, usare il nome e l'endpoint compatibile con l'hub eventi dell'hub IoT nella stringa di connessione ASA.</span><span class="sxs-lookup"><span data-stu-id="8d978-136">If you use Azure Stream Analytics (ASA) to read messages from an IoT hub with IP filtering enabled, use the Event Hub-compatible name and endpoint of your IoT Hub in the ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="8d978-137">Eliminare una regola del filtro IP</span><span class="sxs-lookup"><span data-stu-id="8d978-137">Delete an IP filter rule</span></span>

<span data-ttu-id="8d978-138">Selezionare una o più regole del filtro IP nella griglia e fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="8d978-138">To delete an IP filter rule, select one or more rules in the grid and click **Delete**.</span></span>

![Eliminare una regola del filtro IP dell'hub IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="8d978-140">Valutazione delle regole del filtro IP</span><span class="sxs-lookup"><span data-stu-id="8d978-140">IP filter rule evaluation</span></span>

<span data-ttu-id="8d978-141">Le regole del filtro IP vengono applicate in ordine e la prima regola corrispondente all'indirizzo IP determina l'azione di accettazione o rifiuto.</span><span class="sxs-lookup"><span data-stu-id="8d978-141">IP filter rules are applied in order and the first rule that matches the IP address determines the accept or reject action.</span></span>

<span data-ttu-id="8d978-142">Se ad esempio si vogliono accettare gli indirizzi nell'intervallo 192.168.100.0/22 e rifiutare tutti gli altri, la prima regola nella griglia dovrà accettare l'intervallo di indirizzi 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="8d978-142">For example, if you want to accept addresses in the range 192.168.100.0/22 and reject everything else, the first rule in the grid should accept the address range 192.168.100.0/22.</span></span> <span data-ttu-id="8d978-143">La regola successiva dovrà rifiutare tutti gli indirizzi usando l'intervallo 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="8d978-143">The next rule should reject all addresses by using the range 0.0.0.0/0.</span></span>

<span data-ttu-id="8d978-144">È possibile modificare l'ordine delle regole del filtro IP nella griglia facendo clic sui tre punti verticali all'inizio di una riga e trascinando la selezione.</span><span class="sxs-lookup"><span data-stu-id="8d978-144">You can change the order of your IP filter rules in the grid by clicking the three vertical dots at the start of a row and using drag and drop.</span></span>

<span data-ttu-id="8d978-145">Per salvare il nuovo ordine delle regole del filtro IP, fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="8d978-145">To save your new IP filter rule order, click **Save**.</span></span>

![Modificare l'ordine delle regole del filtro IP dell'hub IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="8d978-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8d978-147">Next steps</span></span>

<span data-ttu-id="8d978-148">Per altre informazioni sulle funzionalità dell'hub IoT, vedere:</span><span class="sxs-lookup"><span data-stu-id="8d978-148">To further explore the capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="8d978-149">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="8d978-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="8d978-150">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="8d978-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
<span data-ttu-id="8d978-151">[Azure ExpressRoute]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span><span class="sxs-lookup"><span data-stu-id="8d978-151">[Azure Express Route]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services</span></span>

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md