---
title: "Aumentare automaticamente le unità elaborate di Hub eventi di Azure | Microsoft Docs"
description: "Abilitare Aumento automatico in uno spazio dei nomi per aumentare le unità elaborate"
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
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="3ce64-103">Aumentare automaticamente le unità elaborate di Hub eventi di Azure</span><span class="sxs-lookup"><span data-stu-id="3ce64-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="3ce64-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="3ce64-104">Overview</span></span>

<span data-ttu-id="3ce64-105">Hub eventi di Azure è una piattaforma di streaming dei dati altamente scalabile.</span><span class="sxs-lookup"><span data-stu-id="3ce64-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="3ce64-106">In quanto tale, i clienti di Hub eventi aumentano spesso il loro uso dopo l'onboarding al servizio.</span><span class="sxs-lookup"><span data-stu-id="3ce64-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="3ce64-107">Questi aumenti richiedono un aumento delle unità elaborate (TU) predeterminate per scalare Hub eventi e gestire velocità di trasferimento più alte.</span><span class="sxs-lookup"><span data-stu-id="3ce64-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="3ce64-108">La funzionalità *Aumento automatico* di Hub eventi aumenta automaticamente il numero di unità elaborate per soddisfare le esigenze di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="3ce64-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="3ce64-109">L'aumento delle unità elaborate previene scenari di limitazione, in cui:</span><span class="sxs-lookup"><span data-stu-id="3ce64-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="3ce64-110">Le velocità di ingresso dei dati superano le unità elaborate impostate.</span><span class="sxs-lookup"><span data-stu-id="3ce64-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="3ce64-111">Le velocità di richiesta di uscita dei dati superano le unità elaborate impostate.</span><span class="sxs-lookup"><span data-stu-id="3ce64-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="3ce64-112">Funzionamento di Aumento automatico</span><span class="sxs-lookup"><span data-stu-id="3ce64-112">How Auto-inflate works</span></span>

<span data-ttu-id="3ce64-113">Il traffico di Hub eventi è controllato tramite le unità elaborate.</span><span class="sxs-lookup"><span data-stu-id="3ce64-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="3ce64-114">Una singola unità elaborata consente l'ingresso di 1 MB al secondo e l'uscita del doppio.</span><span class="sxs-lookup"><span data-stu-id="3ce64-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="3ce64-115">Gli Hub eventi standard possono essere configurati con 1-20 unità elaborate.</span><span class="sxs-lookup"><span data-stu-id="3ce64-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="3ce64-116">Aumento automatico consente di iniziare gradualmente con il minimo di unità elaborate richiesto.</span><span class="sxs-lookup"><span data-stu-id="3ce64-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="3ce64-117">La funzionalità aumenta quindi automaticamente le unità elaborate fino al limite massimo necessario, a seconda dell'aumento del traffico.</span><span class="sxs-lookup"><span data-stu-id="3ce64-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="3ce64-118">Aumento automatico offre i seguenti vantaggi:</span><span class="sxs-lookup"><span data-stu-id="3ce64-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="3ce64-119">Un meccanismo di scala efficiente per iniziare con poche unità elaborate e aumentarle al bisogno.</span><span class="sxs-lookup"><span data-stu-id="3ce64-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="3ce64-120">Aumenta automaticamente le unità elaborate fino al limite superiore specificato senza problemi di limitazioni.</span><span class="sxs-lookup"><span data-stu-id="3ce64-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="3ce64-121">Offre maggiore controllo sulle dimensioni perché consente di specificare quando e come gestire l'aumento.</span><span class="sxs-lookup"><span data-stu-id="3ce64-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="3ce64-122">Abilitare Aumento automatico in uno spazio dei nomi</span><span class="sxs-lookup"><span data-stu-id="3ce64-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="3ce64-123">È possibile abilitare o disabilitare Aumento automatico in uno spazio dei nomi usando uno dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="3ce64-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="3ce64-124">Il [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="3ce64-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="3ce64-125">Un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ce64-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="3ce64-126">Abilitare Aumento automatico tramite il portale</span><span class="sxs-lookup"><span data-stu-id="3ce64-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="3ce64-127">È possibile abilitare la funzionalità Aumento automatico in uno spazio dei nomi quando si crea uno spazio dei nomi Hub eventi:</span><span class="sxs-lookup"><span data-stu-id="3ce64-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="3ce64-128">Dopo aver abilitato questa opzione, è possibile iniziare con un numero ridotto di unità elaborate e aumentarle in funzione delle esigenze di utilizzo.</span><span class="sxs-lookup"><span data-stu-id="3ce64-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="3ce64-129">Il limite superiore per l'aumento non influisce sul prezzo, che dipende dal numero di unità elaborate usate all'ora.</span><span class="sxs-lookup"><span data-stu-id="3ce64-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="3ce64-130">È possibile anche abilitare la funzionalità Aumento automatico usando l'opzione di **ridimensionamento** nel pannello Impostazioni del portale:</span><span class="sxs-lookup"><span data-stu-id="3ce64-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="3ce64-131">Abilitare Aumento automatico usando un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="3ce64-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="3ce64-132">È possibile abilitare Aumento automatico durante la distribuzione di un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3ce64-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="3ce64-133">Ad esempio, impostare la proprietà `isAutoInflateEnabled` su **true**, quindi impostare `maximumThroughputUnits` su 10.</span><span class="sxs-lookup"><span data-stu-id="3ce64-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

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

<span data-ttu-id="3ce64-134">Per il modello completo, vedere il modello [Create Event Hubs namespace and enable inflate (Creare uno spazio dei nomi Hub eventi e abilitare l'aumento)](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) in GitHub.</span><span class="sxs-lookup"><span data-stu-id="3ce64-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3ce64-135">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3ce64-135">Next steps</span></span>

<span data-ttu-id="3ce64-136">Per ulteriori informazioni su Hub eventi visitare i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="3ce64-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="3ce64-137">Panoramica di Hub eventi</span><span class="sxs-lookup"><span data-stu-id="3ce64-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* <span data-ttu-id="3ce64-138">[Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)</span><span class="sxs-lookup"><span data-stu-id="3ce64-138">[Create an Event Hub](event-hubs-create.md)</span></span>
