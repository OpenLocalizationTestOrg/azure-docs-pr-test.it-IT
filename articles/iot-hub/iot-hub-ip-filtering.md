---
title: i filtri di connessione IP Hub IoT aaaAzure | Documenti Microsoft
description: "Come toouse filtro connessioni tooblock da IP specifici indirizzi per l'hub IoT Azure tooyour. È possibile bloccare le connessioni da singoli indirizzi IP o da intervalli di indirizzi IP."
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
ms.openlocfilehash: 45e5906a494561b6108895d86d6a04fc3b52b8fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-ip-filters"></a><span data-ttu-id="52f85-104">Usare i filtri IP</span><span class="sxs-lookup"><span data-stu-id="52f85-104">Use IP filters</span></span>

<span data-ttu-id="52f85-105">La sicurezza è un aspetto importante di qualsiasi soluzione IoT basata su un hub IoT di Azure.</span><span class="sxs-lookup"><span data-stu-id="52f85-105">Security is an important aspect of any IoT solution based on Azure IoT Hub.</span></span> <span data-ttu-id="52f85-106">Talvolta è necessario tooexplicitly specificare gli indirizzi IP hello da cui i dispositivi possano connettersi come parte della configurazione di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="52f85-106">Sometimes you need tooexplicitly specify hello IP addresses from which devices can connect as part of your security configuration.</span></span> <span data-ttu-id="52f85-107">Hello _filtro IP_ funzionalità permette tooconfigure regole per il rifiuto o accettare il traffico da specifici indirizzi IPv4.</span><span class="sxs-lookup"><span data-stu-id="52f85-107">hello _IP filter_ feature enables you tooconfigure rules for rejecting or accepting traffic from specific IPv4 addresses.</span></span>

## <a name="when-toouse"></a><span data-ttu-id="52f85-108">Quando toouse</span><span class="sxs-lookup"><span data-stu-id="52f85-108">When toouse</span></span>

<span data-ttu-id="52f85-109">Esistono due casi di utilizzo specifici, in questo caso gli endpoint Hub IoT di hello tooblock utili per determinati indirizzi IP:</span><span class="sxs-lookup"><span data-stu-id="52f85-109">There are two specific use-cases when it is useful tooblock hello IoT Hub endpoints for certain IP addresses:</span></span>

- <span data-ttu-id="52f85-110">L'hub IoT deve ricevere il traffico solo da un intervallo di indirizzi IP specificato e rifiutare tutto il resto.</span><span class="sxs-lookup"><span data-stu-id="52f85-110">Your IoT hub should receive traffic only from a specified range of IP addresses and reject everything else.</span></span> <span data-ttu-id="52f85-111">Ad esempio, si utilizza l'hub IoT con [Express Route di Azure] toocreate connessioni private tra un hub IoT e l'infrastruttura locale.</span><span class="sxs-lookup"><span data-stu-id="52f85-111">For example, you are using your IoT hub with [Azure Express Route] toocreate private connections between an IoT hub and your on-premises infrastructure.</span></span>
- <span data-ttu-id="52f85-112">È necessario tooreject traffico da indirizzi IP che sono stati identificati come sospetto dall'amministratore di hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-112">You need tooreject traffic from IP addresses that have been identified as suspicious by hello IoT hub administrator.</span></span>

## <a name="how-filter-rules-are-applied"></a><span data-ttu-id="52f85-113">Come vengono applicate le regole di filtro</span><span class="sxs-lookup"><span data-stu-id="52f85-113">How filter rules are applied</span></span>

<span data-ttu-id="52f85-114">regole di filtro IP Hello vengono applicate a livello di servizio IoT Hub hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-114">hello IP filter rules are applied at hello IoT Hub service level.</span></span> <span data-ttu-id="52f85-115">Pertanto le regole di filtro IP hello applicano tooall connessioni dai dispositivi e applicazioni back-end utilizzando qualsiasi protocollo supportato.</span><span class="sxs-lookup"><span data-stu-id="52f85-115">Therefore hello IP filter rules apply tooall connections from devices and back-end apps using any supported protocol.</span></span>

<span data-ttu-id="52f85-116">Qualsiasi tentativo di connessione da un indirizzo IP corrispondente a una regola di rifiuto nell'hub IoT riceve un codice di stato 401 - Non autorizzato e la descrizione.</span><span class="sxs-lookup"><span data-stu-id="52f85-116">Any connection attempt from an IP address that matches a rejecting IP rule in your IoT hub receives an unauthorized 401 status code and description.</span></span> <span data-ttu-id="52f85-117">messaggio di risposta Hello non è menzionato regola IP hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-117">hello response message does not mention hello IP rule.</span></span>

## <a name="default-setting"></a><span data-ttu-id="52f85-118">Impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="52f85-118">Default setting</span></span>

<span data-ttu-id="52f85-119">Per impostazione predefinita, hello **filtro IP** griglia nel portale di hello per un hub IoT è vuota.</span><span class="sxs-lookup"><span data-stu-id="52f85-119">By default, hello **IP Filter** grid in hello portal for an IoT hub is empty.</span></span> <span data-ttu-id="52f85-120">Questa impostazione predefinita indica che l'hub accetta connessioni da qualsiasi indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="52f85-120">This default setting means that your hub accepts connections any IP address.</span></span> <span data-ttu-id="52f85-121">Questa impostazione predefinita è regola tooa equivalente che accetta l'intervallo di indirizzi IP di hello 0.0.0.0/0.</span><span class="sxs-lookup"><span data-stu-id="52f85-121">This default setting is equivalent tooa rule that accepts hello 0.0.0.0/0 IP address range.</span></span>

![Impostazioni predefinite del filtro IP dell'hub IoT][img-ip-filter-default]

## <a name="add-or-edit-an-ip-filter-rule"></a><span data-ttu-id="52f85-123">Aggiungere o modificare una regola del filtro IP</span><span class="sxs-lookup"><span data-stu-id="52f85-123">Add or edit an IP filter rule</span></span>

<span data-ttu-id="52f85-124">Quando si aggiunge una regola di filtro IP, viene chiesto di hello seguenti valori:</span><span class="sxs-lookup"><span data-stu-id="52f85-124">When you add an IP filter rule, you are prompted for hello following values:</span></span>

- <span data-ttu-id="52f85-125">Un **nome regola di filtro IP** che deve essere una stringa di alfanumerica univoca, distinzione dei caratteri too128.</span><span class="sxs-lookup"><span data-stu-id="52f85-125">An **IP filter rule name** that must be a unique, case-insensitive, alphanumeric string up too128 characters long.</span></span> <span data-ttu-id="52f85-126">Solo caratteri alfanumerici di hello ASCII a 7 bit più `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` vengono accettate.</span><span class="sxs-lookup"><span data-stu-id="52f85-126">Only hello ASCII 7-bit alphanumeric characters plus `{'-', ':', '/', '\', '.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '''}` are accepted.</span></span>
- <span data-ttu-id="52f85-127">Selezionare un **rifiutare** o **accettare** come hello **azione** per regola di filtro IP hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-127">Select a **reject** or **accept** as hello **action** for hello IP filter rule.</span></span>
- <span data-ttu-id="52f85-128">Specificare un singolo indirizzo IPv4 o un blocco di indirizzi IP in notazione CIDR.</span><span class="sxs-lookup"><span data-stu-id="52f85-128">Provide a single IPv4 address or a block of IP addresses in CIDR notation.</span></span> <span data-ttu-id="52f85-129">Ad esempio, in CIDR notazione 192.168.100.0/22 rappresenta gli indirizzi IPv4 hello 1024 da 192.168.100.0 too192.168.103.255.</span><span class="sxs-lookup"><span data-stu-id="52f85-129">For example, in CIDR notation 192.168.100.0/22 represents hello 1024 IPv4 addresses from 192.168.100.0 too192.168.103.255.</span></span>

![Aggiungi un hub IoT tooan IP filtro regola][img-ip-filter-add-rule]

<span data-ttu-id="52f85-131">Dopo aver salvato la regola hello, è visualizzato un avviso che indica che gli aggiornamenti di hello in corso.</span><span class="sxs-lookup"><span data-stu-id="52f85-131">After you save hello rule, you see an alert notifying you that hello update is in progress.</span></span>

![Notifica sul salvataggio di una regola di filtro IP][img-ip-filter-save-new-rule]

<span data-ttu-id="52f85-133">Hello **Aggiungi** opzione è disabilitata quando si raggiunge il massimo di hello di 10 regole di filtro IP.</span><span class="sxs-lookup"><span data-stu-id="52f85-133">hello **Add** option is disabled when you reach hello maximum of 10 IP filter rules.</span></span>

<span data-ttu-id="52f85-134">È possibile modificare una regola esistente facendo doppio clic sulla riga hello che contiene la regola di hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-134">You can edit an existing rule by double-clicking hello row that contains hello rule.</span></span>

> [!NOTE]
> <span data-ttu-id="52f85-135">Rifiuto IP indirizzi possono impedire ad altri servizi di Azure (ad esempio Azure flusso Analitica, macchine virtuali di Azure o hello Esplora dispositivi nel portale di hello) l'interazione con l'hub IoT hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-135">Rejecting IP addresses can prevent other Azure Services (such as Azure Stream Analytics, Azure Virtual Machines, or hello Device Explorer in hello portal) from interacting with hello IoT hub.</span></span>

> [!WARNING]
> <span data-ttu-id="52f85-136">Se si utilizzano i messaggi tooread Analitica di flusso di Azure (ASA) da un hub IoT con abilitati i filtri IP, utilizzare hello Hub eventi compatibile con nome e l'endpoint dell'IoT Hub nella stringa di connessione ASA hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-136">If you use Azure Stream Analytics (ASA) tooread messages from an IoT hub with IP filtering enabled, use hello Event Hub-compatible name and endpoint of your IoT Hub in hello ASA connection string.</span></span>

## <a name="delete-an-ip-filter-rule"></a><span data-ttu-id="52f85-137">Eliminare una regola del filtro IP</span><span class="sxs-lookup"><span data-stu-id="52f85-137">Delete an IP filter rule</span></span>

<span data-ttu-id="52f85-138">toodelete una regola di filtro IP, selezionare una o più regole nella griglia di hello e fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="52f85-138">toodelete an IP filter rule, select one or more rules in hello grid and click **Delete**.</span></span>

![Eliminare una regola del filtro IP dell'hub IoT][img-ip-filter-delete-rule]

## <a name="ip-filter-rule-evaluation"></a><span data-ttu-id="52f85-140">Valutazione delle regole del filtro IP</span><span class="sxs-lookup"><span data-stu-id="52f85-140">IP filter rule evaluation</span></span>

<span data-ttu-id="52f85-141">Le regole di filtro IP vengono applicate nell'ordine e regola di hello prima che l'indirizzo IP di corrispondenze hello determina hello accettare o rifiutare l'azione.</span><span class="sxs-lookup"><span data-stu-id="52f85-141">IP filter rules are applied in order and hello first rule that matches hello IP address determines hello accept or reject action.</span></span>

<span data-ttu-id="52f85-142">Ad esempio, se si desidera che gli indirizzi tooaccept 192.168.100.0/22 intervallo hello e rifiutare tutti gli altri elementi, hello prima regola griglia hello deve accettare hello indirizzo intervallo 192.168.100.0/22.</span><span class="sxs-lookup"><span data-stu-id="52f85-142">For example, if you want tooaccept addresses in hello range 192.168.100.0/22 and reject everything else, hello first rule in hello grid should accept hello address range 192.168.100.0/22.</span></span> <span data-ttu-id="52f85-143">la regola successiva Hello dovrebbe rifiutare tutti gli indirizzi tramite 0.0.0.0/0 intervallo hello.</span><span class="sxs-lookup"><span data-stu-id="52f85-143">hello next rule should reject all addresses by using hello range 0.0.0.0/0.</span></span>

<span data-ttu-id="52f85-144">Puoi modificare l'ordine di hello le regole di filtro IP nella griglia hello facendo clic su tre punti verticali hello all'avvio di hello di una riga e mediante trascinamento e rilascio.</span><span class="sxs-lookup"><span data-stu-id="52f85-144">You can change hello order of your IP filter rules in hello grid by clicking hello three vertical dots at hello start of a row and using drag and drop.</span></span>

<span data-ttu-id="52f85-145">filtrare il nuovo indirizzo IP toosave ordine della regola, fare clic su **salvare**.</span><span class="sxs-lookup"><span data-stu-id="52f85-145">toosave your new IP filter rule order, click **Save**.</span></span>

![Modificare l'ordine di hello le regole di filtro IP Hub IoT][img-ip-filter-rule-order]

## <a name="next-steps"></a><span data-ttu-id="52f85-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="52f85-147">Next steps</span></span>

<span data-ttu-id="52f85-148">toofurther esplorare le funzionalità di hello di IoT Hub, vedere:</span><span class="sxs-lookup"><span data-stu-id="52f85-148">toofurther explore hello capabilities of IoT Hub, see:</span></span>

- <span data-ttu-id="52f85-149">[Monitoraggio delle operazioni][lnk-monitor]</span><span class="sxs-lookup"><span data-stu-id="52f85-149">[Operations monitoring][lnk-monitor]</span></span>
- <span data-ttu-id="52f85-150">[Metriche di Hub IoT][lnk-metrics]</span><span class="sxs-lookup"><span data-stu-id="52f85-150">[IoT Hub metrics][lnk-metrics]</span></span>

<!-- Images -->
[img-ip-filter-default]: ./media/iot-hub-ip-filtering/ip-filter-default.png
[img-ip-filter-add-rule]: ./media/iot-hub-ip-filtering/ip-filter-add-rule.png
[img-ip-filter-save-new-rule]: ./media/iot-hub-ip-filtering/ip-filter-save-new-rule.png
[img-ip-filter-delete-rule]: ./media/iot-hub-ip-filtering/ip-filter-delete-rule.png
[img-ip-filter-rule-order]: ./media/iot-hub-ip-filtering/ip-filter-rule-order.png


<!-- Links -->

[IoT Hub developer guide]: iot-hub-devguide.md
[Express Route di Azure]:  https://azure.microsoft.com/en-us/documentation/articles/expressroute-faqs/#supported-services

[lnk-monitor]: iot-hub-operations-monitoring.md
[lnk-metrics]: iot-hub-metrics.md