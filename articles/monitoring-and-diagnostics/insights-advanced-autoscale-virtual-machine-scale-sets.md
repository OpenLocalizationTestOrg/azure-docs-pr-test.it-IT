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
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="e5fea-103">Configurazione di scalabilità automatica avanzata con modelli di Resource Manager per set di scalabilità di macchine virtuali di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="e5fea-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="e5fea-104">È possibile aumentare e ridurre il numero di istanze dei set di scalabilità di macchine virtuali in base ai valori soglia per le metriche delle prestazioni, a una pianificazione ricorrente oppure a una data specifica.</span><span class="sxs-lookup"><span data-stu-id="e5fea-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="e5fea-105">È anche possibile configurare notifiche di posta elettronica e webhook per le azioni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e5fea-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="e5fea-106">Questa procedura dettagliata illustra un esempio di configurazione di tutti tali oggetti usando in modello di Resource Manager in un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="e5fea-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="e5fea-107">Durante questa procedura dettagliata vengono illustrati i passaggi di hello per set di scalabilità di macchine Virtuali, hello possono essere applicati anche tooautoscaling [servizi Cloud](https://azure.microsoft.com/services/cloud-services/), e [servizio App: app Web](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="e5fea-107">While this walkthrough explains hello steps for VM Scale Sets, hello same information applies tooautoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="e5fea-108">Per una scala minima in/out impostazione su un Set di scalabilità della macchina virtuale in base a una misurazione delle prestazioni di semplice, ad esempio CPU, fare riferimento toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) e [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documenti</span><span class="sxs-lookup"><span data-stu-id="e5fea-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer toohello [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="e5fea-109">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="e5fea-109">Walkthrough</span></span>
<span data-ttu-id="e5fea-110">In questa procedura dettagliata, si usa [Esplora inventario risorse di Azure](https://resources.azure.com/) tooconfigure e Aggiorna impostazioni di scalabilità automatica hello per un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="e5fea-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) tooconfigure and update hello autoscale setting for a scale set.</span></span> <span data-ttu-id="e5fea-111">Esplora inventario risorse di Azure è un modo semplice di toomanage risorse di Azure tramite modelli di gestione risorse.</span><span class="sxs-lookup"><span data-stu-id="e5fea-111">Azure Resource Explorer is an easy way toomanage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="e5fea-112">Nel caso di nuovo strumento di Esplora inventario risorse tooAzure, leggere [questa introduzione](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="e5fea-112">If you are new tooAzure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="e5fea-113">Distribuire un nuovo set di scalabilità con un'impostazione di scalabilità automatica di base.</span><span class="sxs-lookup"><span data-stu-id="e5fea-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="e5fea-114">Questo articolo Usa hello dalla raccolta di avvio rapido di Azure, che ha un Windows hello set di scalabilità con un modello di base di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="e5fea-114">This article uses hello one from hello Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="e5fea-115">Scala Linux imposta lavoro hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="e5fea-115">Linux scale sets work hello same way.</span></span>
2. <span data-ttu-id="e5fea-116">Dopo la creazione di set di scalabilità hello passare toohello scala set di risorse da Esplora risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="e5fea-116">After hello scale set is created, navigate toohello scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="e5fea-117">Vedere di seguito hello nel nodo Insights.</span><span class="sxs-lookup"><span data-stu-id="e5fea-117">You see hello following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="e5fea-119">esecuzione di Hello modello ha creato un'impostazione di scalabilità automatica con nome hello **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="e5fea-119">hello template execution has created a default autoscale setting with hello name **'autoscalewad'**.</span></span> <span data-ttu-id="e5fea-120">Sul lato destro hello, è possibile visualizzare la definizione completa di hello di questa impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="e5fea-120">On hello right-hand side, you can view hello full definition of this autoscale setting.</span></span> <span data-ttu-id="e5fea-121">In questo caso, impostazione di scalabilità automatica hello dotato di una regola di scalabilità orizzontale e scalabilità in base % CPU.</span><span class="sxs-lookup"><span data-stu-id="e5fea-121">In this case, hello default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="e5fea-122">È ora possibile aggiungere più profili e regole basate su pianificazione hello o requisiti specifici.</span><span class="sxs-lookup"><span data-stu-id="e5fea-122">You can now add more profiles and rules based on hello schedule or specific requirements.</span></span> <span data-ttu-id="e5fea-123">Viene creata un'impostazione di ridimensionamento automatico con tre profili.</span><span class="sxs-lookup"><span data-stu-id="e5fea-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="e5fea-124">toounderstand profili e le regole di scalabilità automatica, esaminare [le procedure consigliate di scalabilità automatica](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="e5fea-124">toounderstand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="e5fea-125">Profili e regole</span><span class="sxs-lookup"><span data-stu-id="e5fea-125">Profiles & Rules</span></span> | <span data-ttu-id="e5fea-126">Description</span><span class="sxs-lookup"><span data-stu-id="e5fea-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="e5fea-127">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="e5fea-127">**Profile**</span></span> |<span data-ttu-id="e5fea-128">**Basato su prestazioni/metrica**</span><span class="sxs-lookup"><span data-stu-id="e5fea-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="e5fea-129">Regola</span><span class="sxs-lookup"><span data-stu-id="e5fea-129">Rule</span></span> |<span data-ttu-id="e5fea-130">Numero di messaggi della coda del bus di servizio > x</span><span class="sxs-lookup"><span data-stu-id="e5fea-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="e5fea-131">Regola</span><span class="sxs-lookup"><span data-stu-id="e5fea-131">Rule</span></span> |<span data-ttu-id="e5fea-132">Numero di messaggi della coda del bus di servizio < y</span><span class="sxs-lookup"><span data-stu-id="e5fea-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="e5fea-133">Regola</span><span class="sxs-lookup"><span data-stu-id="e5fea-133">Rule</span></span> |<span data-ttu-id="e5fea-134">% CPU > n</span><span class="sxs-lookup"><span data-stu-id="e5fea-134">CPU% > n</span></span> |
    | <span data-ttu-id="e5fea-135">Regola</span><span class="sxs-lookup"><span data-stu-id="e5fea-135">Rule</span></span> |<span data-ttu-id="e5fea-136">% CPU < p</span><span class="sxs-lookup"><span data-stu-id="e5fea-136">CPU% < p</span></span> |
    | <span data-ttu-id="e5fea-137">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="e5fea-137">**Profile**</span></span> |<span data-ttu-id="e5fea-138">**Ore della mattina dei giorni feriali (nessuna regola)**</span><span class="sxs-lookup"><span data-stu-id="e5fea-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="e5fea-139">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="e5fea-139">**Profile**</span></span> |<span data-ttu-id="e5fea-140">**Giorno di lancio del prodotto (nessuna regola)**</span><span class="sxs-lookup"><span data-stu-id="e5fea-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="e5fea-141">Di seguito viene descritto uno senario ipotetico scenario di ridimensionamento per la procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="e5fea-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="e5fea-142">**Carico basato su** -Vorrei tooscale o in base al carico hello per l'applicazione ospitata in my set.* scala</span><span class="sxs-lookup"><span data-stu-id="e5fea-142">**Load based** - I'd like tooscale out or in based on hello load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="e5fea-143">**Dimensione coda di messaggi** -usare una coda del Bus di servizio per un'applicazione in ingresso messaggi toomy hello.</span><span class="sxs-lookup"><span data-stu-id="e5fea-143">**Message Queue size** - I use a Service Bus Queue for hello incoming messages toomy application.</span></span> <span data-ttu-id="e5fea-144">Si utilizza il numero di messaggi della coda hello e % della CPU e configurare un tootrigger profilo predefinito un'azione di scalabilità, se il numero di messaggi o CPU riscontri hello threshold.*</span><span class="sxs-lookup"><span data-stu-id="e5fea-144">I use hello queue's message count and CPU% and configure a default profile tootrigger a scale action if either of message count or CPU hits hello threshold.*</span></span>
    * <span data-ttu-id="e5fea-145">**Ora del giorno della settimana,** -desidera un profilo di 'ora del giorno hello' base ricorrente settimanale chiamato 'Ore della mattina giorno della settimana'.</span><span class="sxs-lookup"><span data-stu-id="e5fea-145">**Time of week and day** - I want a weekly recurring 'time of hello day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="e5fea-146">Basato su dati cronologici, conoscere che è migliore toohave determinato numero di VM istanze toohandle carico dell'applicazione in uso durante questo videochiamate</span><span class="sxs-lookup"><span data-stu-id="e5fea-146">Based on historical data, I know it is better toohave certain number of VM instances toohandle my application's load during this time.*</span></span>
    * <span data-ttu-id="e5fea-147">**Date speciali** - È stato aggiunto un profilo "Giorni di lancio del prodotto".</span><span class="sxs-lookup"><span data-stu-id="e5fea-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="e5fea-148">Prevedere date specifiche dell'applicazione è pronta toohandle hello carico a causa di annunci di marketing e quando è stato inserito un nuovo prodotto hello Error</span><span class="sxs-lookup"><span data-stu-id="e5fea-148">I plan ahead for specific dates so my application is ready toohandle hello load due marketing announcements and when we put a new product in hello application.*</span></span>
    * <span data-ttu-id="e5fea-149">*ultimi due profili di Hello possono avere anche altre regole in base metrica di prestazioni all'interno di essi. In questo caso, ho deciso di non toohave uno e invece toorely nella metrica di prestazioni hello predefinito basato su regole. Le regole sono facoltative per i profili basati su date e ricorrenti hello.*</span><span class="sxs-lookup"><span data-stu-id="e5fea-149">*hello last two profiles can also have other performance metric based rules within them. In this case, I decided not toohave one and instead toorely on hello default performance metric based rules. Rules are optional for hello recurring and date-based profiles.*</span></span>

    <span data-ttu-id="e5fea-150">Definizione delle priorità del motore di scalabilità automatica di regole e i profili di hello inoltre viene acquisito in hello [procedure consigliate per la scalabilità automatica](insights-autoscale-best-practices.md) articolo.</span><span class="sxs-lookup"><span data-stu-id="e5fea-150">Autoscale engine's prioritization of hello profiles and rules is also captured in hello [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="e5fea-151">Per un elenco di metriche comuni per la scalabilità automatica, vedere [Metriche comuni per la scalabilità automatica](insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="e5fea-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="e5fea-152">Verificare di disporre in hello **lettura/scrittura** modalità in Esplora inventario risorse</span><span class="sxs-lookup"><span data-stu-id="e5fea-152">Make sure you are on hello **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, impostazione di ridimensionamento automatico predefinita](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="e5fea-154">Fare clic su Edit.</span><span class="sxs-lookup"><span data-stu-id="e5fea-154">Click Edit.</span></span> <span data-ttu-id="e5fea-155">**Sostituire** elemento profili' hello' nelle impostazioni di scalabilità automatica con hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="e5fea-155">**Replace** hello 'profiles' element in autoscale setting with hello following configuration:</span></span>

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
    <span data-ttu-id="e5fea-157">Per i campi e i valori supportati, vedere la [documentazione sull'API REST per il ridimensionamento automatico](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="e5fea-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="e5fea-158">Ora l'impostazione di scalabilità automatica contiene tre profili hello illustrati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="e5fea-158">Now your autoscale setting contains hello three profiles explained previously.</span></span>

7. <span data-ttu-id="e5fea-159">Infine, esaminare hello scalabilità automatica **notifica** sezione.</span><span class="sxs-lookup"><span data-stu-id="e5fea-159">Finally, look at hello Autoscale **notification** section.</span></span> <span data-ttu-id="e5fea-160">Le notifiche di scalabilità automatica consentono di toodo tre operazioni quando un messaggio di scalabilità orizzontale o in azione avviato correttamente.</span><span class="sxs-lookup"><span data-stu-id="e5fea-160">Autoscale notifications allow you toodo three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="e5fea-161">Notifica salve e co-amministratori della sottoscrizione</span><span class="sxs-lookup"><span data-stu-id="e5fea-161">Notify hello admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="e5fea-162">Inviare un messaggio di posta elettronica a un set di utenti.</span><span class="sxs-lookup"><span data-stu-id="e5fea-162">Email a set of users</span></span>
   - <span data-ttu-id="e5fea-163">Attivare una chiamata webhook.</span><span class="sxs-lookup"><span data-stu-id="e5fea-163">Trigger a webhook call.</span></span> <span data-ttu-id="e5fea-164">Quando viene attivato, questo webhook invia i metadati relativi a condizione per la scalabilità automatica hello e set di scalabilità hello della risorsa.</span><span class="sxs-lookup"><span data-stu-id="e5fea-164">When fired, this webhook sends metadata about hello autoscaling condition and hello scale set resource.</span></span> <span data-ttu-id="e5fea-165">toolearn ulteriori informazioni sui payload hello del webhook scalabilità automatica, vedere [Webhook configurare & notifiche tramite posta elettronica per la scalabilità automatica](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="e5fea-165">toolearn more about hello payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="e5fea-166">Aggiungere hello dopo l'impostazione di scalabilità automatica toohello sostituendo il **notifica** elemento il cui valore è null</span><span class="sxs-lookup"><span data-stu-id="e5fea-166">Add hello following toohello Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="e5fea-167">Riscontri **inserire** pulsante nelle impostazioni di scalabilità automatica hello tooupdate Esplora inventario risorse.</span><span class="sxs-lookup"><span data-stu-id="e5fea-167">Hit **Put** button in Resource Explorer tooupdate hello autoscale setting.</span></span>

<span data-ttu-id="e5fea-168">È stato aggiornato a un'impostazione in un tooinclude di set di scalabilità della macchina virtuale più profili di scalabilità di scalabilità automatica e ridimensionare le notifiche.</span><span class="sxs-lookup"><span data-stu-id="e5fea-168">You have updated an autoscale setting on a VM Scale set tooinclude multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5fea-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e5fea-169">Next Steps</span></span>
<span data-ttu-id="e5fea-170">Utilizzare questi collegamenti di toolearn ulteriori informazioni sulla scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="e5fea-170">Use these links toolearn more about autoscaling.</span></span>

[<span data-ttu-id="e5fea-171">Risolvere i problemi di scalabilità automatica con set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="e5fea-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="e5fea-172">Metriche comuni per il ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="e5fea-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="e5fea-173">Procedure consigliate per il ridimensionamento automatico di Azure</span><span class="sxs-lookup"><span data-stu-id="e5fea-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="e5fea-174">Gestire il ridimensionamento automatico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5fea-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="e5fea-175">Gestire il ridimensionamento automatico con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="e5fea-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="e5fea-176">Configurare notifiche webhook e di posta elettronica per il ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="e5fea-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
