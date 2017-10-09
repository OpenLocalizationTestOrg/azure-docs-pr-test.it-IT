---
title: "aaaAdvanced scalabilità automatica utilizzando macchine virtuali di Azure | Documenti Microsoft"
description: "Usa Resource Manager e i set di scalabilità di macchine virtuali di Microsoft Azure con più regole e profili che inviano messaggi di posta elettronica e chiamano URL di webhook con azioni di scalabilità."
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ancav
ms.openlocfilehash: ecb01e3094f715837b75ef07a7dbecdf0f2e78f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a>Configurazione di scalabilità automatica avanzata con modelli di Resource Manager per set di scalabilità di macchine virtuali di Microsoft Azure
È possibile aumentare e ridurre il numero di istanze dei set di scalabilità di macchine virtuali in base ai valori soglia per le metriche delle prestazioni, a una pianificazione ricorrente oppure a una data specifica. È anche possibile configurare notifiche di posta elettronica e webhook per le azioni di scalabilità. Questa procedura dettagliata illustra un esempio di configurazione di tutti tali oggetti usando in modello di Resource Manager in un set di scalabilità di macchine virtuali.

> [!NOTE]
> Durante questa procedura dettagliata vengono illustrati i passaggi di hello per set di scalabilità di macchine Virtuali, hello possono essere applicati anche tooautoscaling [servizi Cloud](https://azure.microsoft.com/services/cloud-services/), e [servizio App: app Web](https://azure.microsoft.com/services/app-service/web/).
> Per una scala minima in/out impostazione su un Set di scalabilità della macchina virtuale in base a una misurazione delle prestazioni di semplice, ad esempio CPU, fare riferimento toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) e [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documenti
>
>

## <a name="walkthrough"></a>Procedura dettagliata
In questa procedura dettagliata, si usa [Esplora inventario risorse di Azure](https://resources.azure.com/) tooconfigure e Aggiorna impostazioni di scalabilità automatica hello per un set di scalabilità. Esplora inventario risorse di Azure è un modo semplice di toomanage risorse di Azure tramite modelli di gestione risorse. Nel caso di nuovo strumento di Esplora inventario risorse tooAzure, leggere [questa introduzione](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).

1. Distribuire un nuovo set di scalabilità con un'impostazione di scalabilità automatica di base. Questo articolo Usa hello dalla raccolta di avvio rapido di Azure, che ha un Windows hello set di scalabilità con un modello di base di scalabilità automatica. Scala Linux imposta lavoro hello allo stesso modo.
2. Dopo la creazione di set di scalabilità hello passare toohello scala set di risorse da Esplora risorse di Azure. Vedere di seguito hello nel nodo Insights.

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    esecuzione di Hello modello ha creato un'impostazione di scalabilità automatica con nome hello **'autoscalewad'**. Sul lato destro hello, è possibile visualizzare la definizione completa di hello di questa impostazione di scalabilità automatica. In questo caso, impostazione di scalabilità automatica hello dotato di una regola di scalabilità orizzontale e scalabilità in base % CPU.  

3. È ora possibile aggiungere più profili e regole basate su pianificazione hello o requisiti specifici. Viene creata un'impostazione di ridimensionamento automatico con tre profili. toounderstand profili e le regole di scalabilità automatica, esaminare [le procedure consigliate di scalabilità automatica](insights-autoscale-best-practices.md).  

    | Profili e regole | Description |
    |--- | --- |
    | **Profilo** |**Basato su prestazioni/metrica** |
    | Regola |Numero di messaggi della coda del bus di servizio > x |
    | Regola |Numero di messaggi della coda del bus di servizio < y |
    | Regola |% CPU > n |
    | Regola |% CPU < p |
    | **Profilo** |**Ore della mattina dei giorni feriali (nessuna regola)** |
    | **Profilo** |**Giorno di lancio del prodotto (nessuna regola)** |

4. Di seguito viene descritto uno senario ipotetico scenario di ridimensionamento per la procedura dettagliata.

    * **Carico basato su** -Vorrei tooscale o in base al carico hello per l'applicazione ospitata in my set.* scala
    * **Dimensione coda di messaggi** -usare una coda del Bus di servizio per un'applicazione in ingresso messaggi toomy hello. Si utilizza il numero di messaggi della coda hello e % della CPU e configurare un tootrigger profilo predefinito un'azione di scalabilità, se il numero di messaggi o CPU riscontri hello threshold.*
    * **Ora del giorno della settimana,** -desidera un profilo di 'ora del giorno hello' base ricorrente settimanale chiamato 'Ore della mattina giorno della settimana'. Basato su dati cronologici, conoscere che è migliore toohave determinato numero di VM istanze toohandle carico dell'applicazione in uso durante questo videochiamate
    * **Date speciali** - È stato aggiunto un profilo "Giorni di lancio del prodotto". Prevedere date specifiche dell'applicazione è pronta toohandle hello carico a causa di annunci di marketing e quando è stato inserito un nuovo prodotto hello Error
    * *ultimi due profili di Hello possono avere anche altre regole in base metrica di prestazioni all'interno di essi. In questo caso, ho deciso di non toohave uno e invece toorely nella metrica di prestazioni hello predefinito basato su regole. Le regole sono facoltative per i profili basati su date e ricorrenti hello.*

    Definizione delle priorità del motore di scalabilità automatica di regole e i profili di hello inoltre viene acquisito in hello [procedure consigliate per la scalabilità automatica](insights-autoscale-best-practices.md) articolo.
    Per un elenco di metriche comuni per la scalabilità automatica, vedere [Metriche comuni per la scalabilità automatica](insights-autoscale-common-metrics.md).

5. Verificare di disporre in hello **lettura/scrittura** modalità in Esplora inventario risorse

    ![Autoscalewad, impostazione di ridimensionamento automatico predefinita](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. Fare clic su Edit. **Sostituire** elemento profili' hello' nelle impostazioni di scalabilità automatica con hello seguente configurazione:

    ![Profili](./media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    Per i campi e i valori supportati, vedere la [documentazione sull'API REST per il ridimensionamento automatico](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx). Ora l'impostazione di scalabilità automatica contiene tre profili hello illustrati in precedenza.

7. Infine, esaminare hello scalabilità automatica **notifica** sezione. Le notifiche di scalabilità automatica consentono di toodo tre operazioni quando un messaggio di scalabilità orizzontale o in azione avviato correttamente.
   - Notifica salve e co-amministratori della sottoscrizione
   - Inviare un messaggio di posta elettronica a un set di utenti.
   - Attivare una chiamata webhook. Quando viene attivato, questo webhook invia i metadati relativi a condizione per la scalabilità automatica hello e set di scalabilità hello della risorsa. toolearn ulteriori informazioni sui payload hello del webhook scalabilità automatica, vedere [Webhook configurare & notifiche tramite posta elettronica per la scalabilità automatica](insights-autoscale-to-webhook-email.md).

   Aggiungere hello dopo l'impostazione di scalabilità automatica toohello sostituendo il **notifica** elemento il cui valore è null

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]

   ```

   Riscontri **inserire** pulsante nelle impostazioni di scalabilità automatica hello tooupdate Esplora inventario risorse.

È stato aggiornato a un'impostazione in un tooinclude di set di scalabilità della macchina virtuale più profili di scalabilità di scalabilità automatica e ridimensionare le notifiche.

## <a name="next-steps"></a>Passaggi successivi
Utilizzare questi collegamenti di toolearn ulteriori informazioni sulla scalabilità automatica.

[Risolvere i problemi di scalabilità automatica con set di scalabilità di macchine virtuali](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[Metriche comuni per il ridimensionamento automatico](insights-autoscale-common-metrics.md)

[Procedure consigliate per il ridimensionamento automatico di Azure](insights-autoscale-best-practices.md)

[Gestire il ridimensionamento automatico con PowerShell](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[Gestire il ridimensionamento automatico con l'interfaccia della riga di comando](insights-cli-samples.md#autoscale)

[Configurare notifiche webhook e di posta elettronica per il ridimensionamento automatico](insights-autoscale-to-webhook-email.md)
