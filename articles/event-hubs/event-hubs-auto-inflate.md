---
title: "scala aaaAutomatically le unità di velocità effettiva di hub eventi di Azure | Documenti Microsoft"
description: "Abilitare l'aumento automatico su una scala tooautomatically dello spazio dei nomi di unità di velocità effettiva"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="301f1-103">Aumentare automaticamente le unità elaborate di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="301f1-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="301f1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="301f1-104">Overview</span></span>

<span data-ttu-id="301f1-105">Hub eventi di Azure è una piattaforma di streaming dei dati altamente scalabile.</span><span class="sxs-lookup"><span data-stu-id="301f1-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="301f1-106">Di conseguenza, i clienti di hub eventi aumentare spesso il loro utilizzo dopo caricamento toohello servizio.</span><span class="sxs-lookup"><span data-stu-id="301f1-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="301f1-107">Tale aumento richiede tooscale unità (TUs) velocità effettiva hello predeterminato incremento hub eventi e gestione una maggiore velocità di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="301f1-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="301f1-108">Hello *ingrandimento automatico* funzionalità degli hub di eventi può essere ridimensionato automaticamente il numero di hello di TUs toomeet esigenze per l'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="301f1-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="301f1-109">L'aumento delle unità elaborate previene scenari di limitazione, in cui:</span><span class="sxs-lookup"><span data-stu-id="301f1-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="301f1-110">Le velocità di ingresso dei dati superano le unità elaborate impostate.</span><span class="sxs-lookup"><span data-stu-id="301f1-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="301f1-111">Le velocità di richiesta di uscita dei dati superano le unità elaborate impostate.</span><span class="sxs-lookup"><span data-stu-id="301f1-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="301f1-112">Funzionamento di Aumento automatico</span><span class="sxs-lookup"><span data-stu-id="301f1-112">How Auto-inflate works</span></span>

<span data-ttu-id="301f1-113">Il traffico di Hub eventi è controllato tramite le unità elaborate.</span><span class="sxs-lookup"><span data-stu-id="301f1-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="301f1-114">Una singola unità elaborata consente l'ingresso di 1 MB al secondo e l'uscita del doppio.</span><span class="sxs-lookup"><span data-stu-id="301f1-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="301f1-115">Gli Hub eventi standard possono essere configurati con 1-20 unità elaborate.</span><span class="sxs-lookup"><span data-stu-id="301f1-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="301f1-116">Aumento automatico consente toostart piccole unità di velocità effettiva necessario minima hello.</span><span class="sxs-lookup"><span data-stu-id="301f1-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="301f1-117">funzionalità di Hello quindi si adatta automaticamente toohello il limite massimo di unità di velocità effettiva, che è necessario, a seconda di hello aumento del traffico.</span><span class="sxs-lookup"><span data-stu-id="301f1-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="301f1-118">Aumento automatico fornisce hello seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="301f1-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="301f1-119">Un efficiente toostart meccanismo scalabilità piccoli e scalabilità verticale come si aumentano.</span><span class="sxs-lookup"><span data-stu-id="301f1-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="301f1-120">Applicare la scalabilità automatica toohello limite superiore specificato senza problemi di limitazione delle richieste.</span><span class="sxs-lookup"><span data-stu-id="301f1-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="301f1-121">Maggiore controllo sulla scalabilità, come è possibile controllare quando la quantità tooscale e.</span><span class="sxs-lookup"><span data-stu-id="301f1-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="301f1-122">Abilitare Aumento automatico in uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="301f1-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="301f1-123">È possibile abilitare o disabilitare l'aumento automatico in uno spazio dei nomi utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="301f1-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="301f1-124">Hello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="301f1-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="301f1-125">Un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="301f1-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="301f1-126">Abilitare l'aumento automatico tramite il portale di hello</span><span class="sxs-lookup"><span data-stu-id="301f1-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="301f1-127">È possibile abilitare funzionalità di aumento automatico di hello in uno spazio dei nomi durante la creazione di uno spazio dei nomi dell'hub eventi:</span><span class="sxs-lookup"><span data-stu-id="301f1-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="301f1-128">Dopo aver abilitato questa opzione, è possibile iniziare con un numero ridotto di unità elaborate e aumentarle in funzione delle esigenze di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="301f1-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="301f1-129">Hello limite superiore per inflazione non influisce sui prezzi, che dipende dal numero di hello di TUs utilizzata ogni ora.</span><span class="sxs-lookup"><span data-stu-id="301f1-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="301f1-130">È inoltre possibile abilitare l'aumento automatico utilizzando hello **scala** opzione nel pannello impostazioni hello nel portale di hello:</span><span class="sxs-lookup"><span data-stu-id="301f1-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="301f1-131">Abilitare Aumento automatico usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="301f1-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="301f1-132">È possibile abilitare Aumento automatico durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="301f1-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="301f1-133">Ad esempio, set hello `isAutoInflateEnabled` proprietà troppo**true** e impostare `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="301f1-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="301f1-134">Per il modello di hello completo, vedere hello [dello spazio dei nomi creare hub eventi e abilitare ingrandimento](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modello su GitHub.</span><span class="sxs-lookup"><span data-stu-id="301f1-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="301f1-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="301f1-135">Next steps</span></span>

<span data-ttu-id="301f1-136">Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:</span><span class="sxs-lookup"><span data-stu-id="301f1-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="301f1-137">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="301f1-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="301f1-138">[Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="301f1-138">[Create an Event Hub](event-hubs-create.md)</span></span>
