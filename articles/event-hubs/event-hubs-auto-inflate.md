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
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a>Aumentare automaticamente le unità elaborate di Hub eventi di Azure

## <a name="overview"></a>Panoramica

Hub eventi di Azure è una piattaforma di streaming dei dati altamente scalabile. Di conseguenza, i clienti di hub eventi aumentare spesso il loro utilizzo dopo caricamento toohello servizio. Tale aumento richiede tooscale unità (TUs) velocità effettiva hello predeterminato incremento hub eventi e gestione una maggiore velocità di trasferimento. Hello *ingrandimento automatico* funzionalità degli hub di eventi può essere ridimensionato automaticamente il numero di hello di TUs toomeet esigenze per l'utilizzo. L'aumento delle unità elaborate previene scenari di limitazione, in cui:

* Le velocità di ingresso dei dati superano le unità elaborate impostate.
* Le velocità di richiesta di uscita dei dati superano le unità elaborate impostate.

## <a name="how-auto-inflate-works"></a>Funzionamento di Aumento automatico

Il traffico di Hub eventi è controllato tramite le unità elaborate. Una singola unità elaborata consente l'ingresso di 1 MB al secondo e l'uscita del doppio. Gli Hub eventi standard possono essere configurati con 1-20 unità elaborate. Aumento automatico consente toostart piccole unità di velocità effettiva necessario minima hello. funzionalità di Hello quindi si adatta automaticamente toohello il limite massimo di unità di velocità effettiva, che è necessario, a seconda di hello aumento del traffico. Aumento automatico fornisce hello seguenti vantaggi:

- Un efficiente toostart meccanismo scalabilità piccoli e scalabilità verticale come si aumentano.
- Applicare la scalabilità automatica toohello limite superiore specificato senza problemi di limitazione delle richieste.
- Maggiore controllo sulla scalabilità, come è possibile controllare quando la quantità tooscale e.

## <a name="enable-auto-inflate-on-a-namespace"></a>Abilitare Aumento automatico in uno spazio dei nomi

È possibile abilitare o disabilitare l'aumento automatico in uno spazio dei nomi utilizzando uno dei seguenti metodi hello:

1. Hello [portale di Azure](https://portal.azure.com).
2. Un modello di Azure Resource Manager.

### <a name="enable-auto-inflate-through-hello-portal"></a>Abilitare l'aumento automatico tramite il portale di hello

È possibile abilitare funzionalità di aumento automatico di hello in uno spazio dei nomi durante la creazione di uno spazio dei nomi dell'hub eventi:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

Dopo aver abilitato questa opzione, è possibile iniziare con un numero ridotto di unità elaborate e aumentarle in funzione delle esigenze di utilizzo. Hello limite superiore per inflazione non influisce sui prezzi, che dipende dal numero di hello di TUs utilizzata ogni ora.

È inoltre possibile abilitare l'aumento automatico utilizzando hello **scala** opzione nel pannello impostazioni hello nel portale di hello:
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a>Abilitare Aumento automatico usando un modello di Azure Resource Manager

È possibile abilitare Aumento automatico durante la distribuzione di un modello di Azure Resource Manager. Ad esempio, set hello `isAutoInflateEnabled` proprietà troppo**true** e impostare `maximumThroughputUnits` too10.

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

Per il modello di hello completo, vedere hello [dello spazio dei nomi creare hub eventi e abilitare ingrandimento](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modello su GitHub.

## <a name="next-steps"></a>Passaggi successivi

Sono disponibili ulteriori informazioni sugli hub di eventi visitando hello seguenti collegamenti:

* [Panoramica di Hub eventi](event-hubs-what-is-event-hubs.md)
* [Create an Event Hub](event-hubs-create.md) (Creare un Hub eventi)
