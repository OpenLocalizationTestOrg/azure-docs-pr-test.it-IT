---
title: "Scalabilità automatica avanzata con macchine virtuali di Azure | Documentazione Microsoft"
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
ms.openlocfilehash: 80955535c8d863cd3d8d1b77e2ab8bc016b6d9f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="4d166-103">Configurazione di scalabilità automatica avanzata con modelli di Resource Manager per set di scalabilità di macchine virtuali di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="4d166-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="4d166-104">È possibile aumentare e ridurre il numero di istanze dei set di scalabilità di macchine virtuali in base ai valori soglia per le metriche delle prestazioni, a una pianificazione ricorrente oppure a una data specifica.</span><span class="sxs-lookup"><span data-stu-id="4d166-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="4d166-105">È anche possibile configurare notifiche di posta elettronica e webhook per le azioni di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="4d166-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="4d166-106">Questa procedura dettagliata illustra un esempio di configurazione di tutti tali oggetti usando in modello di Resource Manager in un set di scalabilità di macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="4d166-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="4d166-107">Mentre la procedura dettagliata illustra i passaggi per il set di scalabilità di macchine virtuali, le stesse informazioni si applicano a [Servizi cloud](https://azure.microsoft.com/services/cloud-services/) e ad [Servizio app - App Web](https://azure.microsoft.com/services/app-service/web/) per la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="4d166-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling [Cloud Services](https://azure.microsoft.com/services/cloud-services/), and [App Service - Web Apps](https://azure.microsoft.com/services/app-service/web/).</span></span>
> <span data-ttu-id="4d166-108">Per una semplice impostazione di riduzione/aumento del numero di istanze in un set di scalabilità di macchine virtuali in base a una semplice metrica delle prestazioni, ad esempio la CPU, vedere i documenti relativi a [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) e [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="4d166-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="4d166-109">Procedura dettagliata</span><span class="sxs-lookup"><span data-stu-id="4d166-109">Walkthrough</span></span>
<span data-ttu-id="4d166-110">In questa procedura dettagliata viene usato [Esplora risorse di Azure](https://resources.azure.com/) per configurare e aggiornare l'impostazione di ridimensionamento automatico per un set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="4d166-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="4d166-111">Esplora risorse di Azure consente di gestire facilmente le risorse di Azure con i modelli di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d166-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="4d166-112">Se non si ha esperienza con lo strumento Esplora risorse di Azure, vedere [questa introduzione](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="4d166-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="4d166-113">Distribuire un nuovo set di scalabilità con un'impostazione di scalabilità automatica di base.</span><span class="sxs-lookup"><span data-stu-id="4d166-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="4d166-114">Questo articolo usa quello della raccolta di guide introduttive di Azure che ha un set di scalabilità Windows con il modello di scalabilità automatica di base.</span><span class="sxs-lookup"><span data-stu-id="4d166-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="4d166-115">I set di scalabilità Linux funzionano allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="4d166-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="4d166-116">Una volta creato il set di scalabilità, passare alla risorsa set di scalabilità da Esplora risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="4d166-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="4d166-117">Sotto il nodo Microsoft.Insights viene visualizzato quanto segue.</span><span class="sxs-lookup"><span data-stu-id="4d166-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](./media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="4d166-119">L'esecuzione del modello ha creato un'impostazione predefinita di ridimensionamento automatico con il nome **"autoscalewad"**.</span><span class="sxs-lookup"><span data-stu-id="4d166-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="4d166-120">Sul lato destro è possibile visualizzare la definizione completa di questa impostazione di ridimensionamento automatico.</span><span class="sxs-lookup"><span data-stu-id="4d166-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="4d166-121">In questo caso, l'impostazione di ridimensionamento automatico predefinita è inclusa in una regola di aumento e riduzione del numero di istanze basata sulla percentuale di CPU.</span><span class="sxs-lookup"><span data-stu-id="4d166-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="4d166-122">Ora è possibile aggiungere altri profili e regole basati sulla pianificazione o su specifici requisiti.</span><span class="sxs-lookup"><span data-stu-id="4d166-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="4d166-123">Viene creata un'impostazione di ridimensionamento automatico con tre profili.</span><span class="sxs-lookup"><span data-stu-id="4d166-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="4d166-124">Per conoscere i profili e le regole nel ridimensionamento automatico, vedere [Procedure consigliate per il ridimensionamento automatico](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="4d166-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="4d166-125">Profili e regole</span><span class="sxs-lookup"><span data-stu-id="4d166-125">Profiles & Rules</span></span> | <span data-ttu-id="4d166-126">Description</span><span class="sxs-lookup"><span data-stu-id="4d166-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="4d166-127">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="4d166-127">**Profile**</span></span> |<span data-ttu-id="4d166-128">**Basato su prestazioni/metrica**</span><span class="sxs-lookup"><span data-stu-id="4d166-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="4d166-129">Regola</span><span class="sxs-lookup"><span data-stu-id="4d166-129">Rule</span></span> |<span data-ttu-id="4d166-130">Numero di messaggi della coda del bus di servizio > x</span><span class="sxs-lookup"><span data-stu-id="4d166-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="4d166-131">Regola</span><span class="sxs-lookup"><span data-stu-id="4d166-131">Rule</span></span> |<span data-ttu-id="4d166-132">Numero di messaggi della coda del bus di servizio < y</span><span class="sxs-lookup"><span data-stu-id="4d166-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="4d166-133">Regola</span><span class="sxs-lookup"><span data-stu-id="4d166-133">Rule</span></span> |<span data-ttu-id="4d166-134">% CPU > n</span><span class="sxs-lookup"><span data-stu-id="4d166-134">CPU% > n</span></span> |
    | <span data-ttu-id="4d166-135">Regola</span><span class="sxs-lookup"><span data-stu-id="4d166-135">Rule</span></span> |<span data-ttu-id="4d166-136">% CPU < p</span><span class="sxs-lookup"><span data-stu-id="4d166-136">CPU% < p</span></span> |
    | <span data-ttu-id="4d166-137">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="4d166-137">**Profile**</span></span> |<span data-ttu-id="4d166-138">**Ore della mattina dei giorni feriali (nessuna regola)**</span><span class="sxs-lookup"><span data-stu-id="4d166-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="4d166-139">**Profilo**</span><span class="sxs-lookup"><span data-stu-id="4d166-139">**Profile**</span></span> |<span data-ttu-id="4d166-140">**Giorno di lancio del prodotto (nessuna regola)**</span><span class="sxs-lookup"><span data-stu-id="4d166-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="4d166-141">Di seguito viene descritto uno senario ipotetico scenario di ridimensionamento per la procedura dettagliata.</span><span class="sxs-lookup"><span data-stu-id="4d166-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="4d166-142">**Basato sul carico** - Si vuole aumentare o ridurre il numero di istanze in base al carico sull'applicazione ospitata nel set di scalabilità.*</span><span class="sxs-lookup"><span data-stu-id="4d166-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.*</span></span>
    * <span data-ttu-id="4d166-143">**Dimensioni della coda di messaggi** - Si usa una coda del bus di servizio per i messaggi in arrivo nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4d166-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="4d166-144">Si usa il numero di messaggi della coda e la percentuale di CPU e si configura un profilo predefinito per attivare un'azione di scalabilità se il numero di messaggi o la percentuale CPU raggiunge la soglia.*</span><span class="sxs-lookup"><span data-stu-id="4d166-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.*</span></span>
    * <span data-ttu-id="4d166-145">**Ora della settimana e del giorno** - Si vuole un profilo basato su un'ora del giorno con ricorrenza settimanale denominato "Ore della mattina dei giorni feriali".</span><span class="sxs-lookup"><span data-stu-id="4d166-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="4d166-146">In base ai dati cronologici, è stato stabilito che è preferibile disporre di un certo numero di istanze di macchine virtuali per gestire il carico dell'applicazione durante questo orario.*</span><span class="sxs-lookup"><span data-stu-id="4d166-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.*</span></span>
    * <span data-ttu-id="4d166-147">**Date speciali** - È stato aggiunto un profilo "Giorni di lancio del prodotto".</span><span class="sxs-lookup"><span data-stu-id="4d166-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="4d166-148">Vengono pianificate in anticipo date specifiche in modo che l'applicazione sia pronta a gestire il carico derivante da annunci di marketing e dall'inserimento di un nuovo prodotto nell'applicazione.*</span><span class="sxs-lookup"><span data-stu-id="4d166-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.*</span></span>
    * <span data-ttu-id="4d166-149">*Gli ultimi due profili possono anche contenere altre regole basate sulla metrica delle prestazioni. In questo caso, ho deciso di non averne e di affidarmi alle regole basate sulla metrica delle prestazioni predefinite. Le regole sono facoltative per i profili ricorrenti e basati sulle date.*</span><span class="sxs-lookup"><span data-stu-id="4d166-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="4d166-150">La classificazione in ordine di priorità dei profili e delle regole con il motore di ridimensionamento automatico è illustrata anche nell'articolo [Procedure consigliate per il ridimensionamento automatico](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="4d166-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="4d166-151">Per un elenco di metriche comuni per la scalabilità automatica, vedere [Metriche comuni per la scalabilità automatica](insights-autoscale-common-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="4d166-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="4d166-152">Verificare che Esplora risorse sia in modalità **Lettura/Scrittura**.</span><span class="sxs-lookup"><span data-stu-id="4d166-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, impostazione di ridimensionamento automatico predefinita](./media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="4d166-154">Fare clic su Edit.</span><span class="sxs-lookup"><span data-stu-id="4d166-154">Click Edit.</span></span> <span data-ttu-id="4d166-155">**Sostituire** l'elemento "profiles" nell'impostazione di scalabilità automatica con la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="4d166-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

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
    <span data-ttu-id="4d166-157">Per i campi e i valori supportati, vedere la [documentazione sull'API REST per il ridimensionamento automatico](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="4d166-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="4d166-158">Ora l'impostazione di scalabilità automatica contiene i tre profili descritti in precedenza.</span><span class="sxs-lookup"><span data-stu-id="4d166-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="4d166-159">Verrà esaminata infine la sezione **notification** per la scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="4d166-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="4d166-160">Le notifiche di ridimensionamento automatico consentono di eseguire tre operazioni quando un'azione di aumento o riduzione del numero di istanze viene correttamente attivata.</span><span class="sxs-lookup"><span data-stu-id="4d166-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="4d166-161">Inviare una notifica all'amministratore e ai coamministratori della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="4d166-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="4d166-162">Inviare un messaggio di posta elettronica a un set di utenti.</span><span class="sxs-lookup"><span data-stu-id="4d166-162">Email a set of users</span></span>
   - <span data-ttu-id="4d166-163">Attivare una chiamata webhook.</span><span class="sxs-lookup"><span data-stu-id="4d166-163">Trigger a webhook call.</span></span> <span data-ttu-id="4d166-164">Se attivato, questo webhook invia i metadati sulla condizione di scalabilità automatica e sulla risorsa del set di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="4d166-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="4d166-165">Per altre informazioni sul payload del webhook di ridimensionamento automatico, vedere [Configurare notifiche webhook e di posta elettronica per il ridimensionamento automatico](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="4d166-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="4d166-166">Aggiungere il codice seguente all'impostazione di ridimensionamento automatico sostituendo l'elemento **notification** il cui valore è null.</span><span class="sxs-lookup"><span data-stu-id="4d166-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

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

   <span data-ttu-id="4d166-167">Fare clic sul pulsante **Put** in Esplora risorse per aggiornare l'impostazione di scalabilità automatica.</span><span class="sxs-lookup"><span data-stu-id="4d166-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="4d166-168">È stata aggiornata un'impostazione di ridimensionamento automatico in un set di scalabilità di macchine virtuali per includere più profili di scalabilità e notifiche di scalabilità.</span><span class="sxs-lookup"><span data-stu-id="4d166-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4d166-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4d166-169">Next Steps</span></span>
<span data-ttu-id="4d166-170">Per altre informazioni sulla scalabilità automatica, usare questi collegamenti.</span><span class="sxs-lookup"><span data-stu-id="4d166-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="4d166-171">Risolvere i problemi di scalabilità automatica con set di scalabilità di macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="4d166-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="4d166-172">Metriche comuni per il ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="4d166-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="4d166-173">Procedure consigliate per il ridimensionamento automatico di Azure</span><span class="sxs-lookup"><span data-stu-id="4d166-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="4d166-174">Gestire il ridimensionamento automatico con PowerShell</span><span class="sxs-lookup"><span data-stu-id="4d166-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="4d166-175">Gestire il ridimensionamento automatico con l'interfaccia della riga di comando</span><span class="sxs-lookup"><span data-stu-id="4d166-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="4d166-176">Configurare notifiche webhook e di posta elettronica per il ridimensionamento automatico</span><span class="sxs-lookup"><span data-stu-id="4d166-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)
