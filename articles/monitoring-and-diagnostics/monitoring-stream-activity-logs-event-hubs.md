---
title: "aaaStream hello Log attività Azure tooEvent hub | Documenti Microsoft"
description: "Informazioni su come toostream hello tooEvent Log attività Azure hub."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ec4c2d2c-8907-484f-a910-712403a06829
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/06/2017
ms.author: johnkem
ms.openlocfilehash: 336f92771b9d4379ad9dbcadc6997dfae7fae7bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="stream-hello-azure-activity-log-tooevent-hubs"></a><span data-ttu-id="5b397-103">Flusso hello Log attività Azure tooEvent hub</span><span class="sxs-lookup"><span data-stu-id="5b397-103">Stream hello Azure Activity Log tooEvent Hubs</span></span>
<span data-ttu-id="5b397-104">Hello [ **Log attività Azure** ](monitoring-overview-activity-logs.md) può essere trasmesso quasi in tempo reale tooany applicazione tramite l'opzione "Esporta" incorporato hello nel portale di hello o abilitando hello Id regola Bus di servizio in un profilo di Log tramite hello Cmdlet di Azure PowerShell o Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="5b397-104">hello [**Azure Activity Log**](monitoring-overview-activity-logs.md) can be streamed in near real time tooany application using hello built-in “Export” option in hello portal, or by enabling hello Service Bus Rule Id in a Log Profile via hello Azure PowerShell Cmdlets or Azure CLI.</span></span>

## <a name="what-you-can-do-with-hello-activity-log-and-event-hubs"></a><span data-ttu-id="5b397-105">Operazioni eseguibili con hello Log attività e gli hub di eventi</span><span class="sxs-lookup"><span data-stu-id="5b397-105">What you can do with hello Activity Log and Event Hubs</span></span>
<span data-ttu-id="5b397-106">Ecco alcune modalità è possibile utilizzare hello funzionalità per hello Log attività di streaming:</span><span class="sxs-lookup"><span data-stu-id="5b397-106">Here are just a few ways you might use hello streaming capability for hello Activity Log:</span></span>

* <span data-ttu-id="5b397-107">**Sistemi di registrazione e telemetria toothird parti del flusso** – nel tempo, gli hub di eventi di flusso diventeranno hello meccanismo toopipe il Log di attività in Siem di terze parti e soluzioni analitica di log.</span><span class="sxs-lookup"><span data-stu-id="5b397-107">**Stream toothird-party logging and telemetry systems** – Over time, Event Hubs streaming will become hello mechanism toopipe your Activity Log into third-party SIEMs and log analytics solutions.</span></span>
* <span data-ttu-id="5b397-108">**Compilare una piattaforma di registrazione e i dati di telemetria personalizzati** : se si dispone già di una piattaforma dati di telemetria personalizzati o sono solo le compilazione uno, hello altamente scalabile di pubblicazione-sottoscrizione natura degli hub di eventi consente tooflexibly inserimento hello registro attività.</span><span class="sxs-lookup"><span data-stu-id="5b397-108">**Build a custom telemetry and logging platform** – If you already have a custom-built telemetry platform or are just thinking about building one, hello highly scalable publish-subscribe nature of Event Hubs allows you tooflexibly ingest hello activity log.</span></span> [<span data-ttu-id="5b397-109">Vedere toousing di Guida di Dan Rosanova hub eventi in una piattaforma di dati di telemetria di su scala globale.</span><span class="sxs-lookup"><span data-stu-id="5b397-109">See Dan Rosanova’s guide toousing Event Hubs in a global scale telemetry platform here.</span></span>](https://azure.microsoft.com/documentation/videos/build-2015-designing-and-sizing-a-global-scale-telemetry-platform-on-azure-event-Hubs/)

## <a name="enable-streaming-of-hello-activity-log"></a><span data-ttu-id="5b397-110">Abilitare lo streaming di hello Log attività</span><span class="sxs-lookup"><span data-stu-id="5b397-110">Enable streaming of hello Activity Log</span></span>
<span data-ttu-id="5b397-111">È possibile abilitare lo streaming di hello Log attività a livello di codice o tramite il portale di hello.</span><span class="sxs-lookup"><span data-stu-id="5b397-111">You can enable streaming of hello Activity Log either programmatically or via hello portal.</span></span> <span data-ttu-id="5b397-112">In entrambi i casi, si sceglie un Namespace Bus di servizio e un criterio di accesso condiviso per tale spazio dei nomi e un Hub eventi viene creato nello spazio dei nomi quando si verifica hello primo nuovo evento di registro attività.</span><span class="sxs-lookup"><span data-stu-id="5b397-112">Either way, you pick a Service Bus Namespace and a shared access policy for that namespace, and an Event Hub is created in that namespace when hello first new Activity Log event occurs.</span></span> <span data-ttu-id="5b397-113">Se non si dispone di un Namespace Bus di servizio, è necessario innanzitutto toocreate uno.</span><span class="sxs-lookup"><span data-stu-id="5b397-113">If you do not have a Service Bus Namespace, you first need toocreate one.</span></span> <span data-ttu-id="5b397-114">Se si hanno in precedenza di flusso attività Log eventi toothis Service Bus Namespace, verrà riutilizzata hello Hub di eventi che è stato creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5b397-114">If you have previously streamed Activity Log events toothis Service Bus Namespace, hello Event Hub that was previously created will be reused.</span></span> <span data-ttu-id="5b397-115">i criteri di accesso condiviso Hello definiscono hello autorizzazioni meccanismo streaming hello.</span><span class="sxs-lookup"><span data-stu-id="5b397-115">hello shared access policy defines hello permissions that hello streaming mechanism has.</span></span> <span data-ttu-id="5b397-116">Oggi, streaming hub eventi tooan richiede **Gestisci**, **inviare**, e **ascolto** autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="5b397-116">Today, streaming tooan Event Hubs requires **Manage**, **Send**, and **Listen** permissions.</span></span> <span data-ttu-id="5b397-117">È possibile creare o modificare i criteri di accesso condiviso di Service Bus Namespace nel portale classico di hello nella scheda "Configurazione" hello per le Namespace Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="5b397-117">You can create or modify Service Bus Namespace shared access policies in hello classic portal under hello “Configure” tab for your Service Bus Namespace.</span></span> <span data-ttu-id="5b397-118">tooupdate hello Log attività log profilo tooinclude streaming, l'utente hello modifica hello deve disporre dell'autorizzazione ListKey hello tale regola di autorizzazione del Bus di servizio.</span><span class="sxs-lookup"><span data-stu-id="5b397-118">tooupdate hello Activity Log log profile tooinclude streaming, hello user making hello change must have hello ListKey permission on that Service Bus Authorization Rule.</span></span>

<span data-ttu-id="5b397-119">Hello service bus o evento hub dello spazio dei nomi non presenti toobe hello stessa sottoscrizione come sottoscrizione hello la creazione di log come utente di hello che configura l'impostazione di hello dispone di sottoscrizioni di tooboth accesso RBAC appropriate.</span><span class="sxs-lookup"><span data-stu-id="5b397-119">hello service bus or event hub namespace does not have toobe in hello same subscription as hello subscription emitting logs as long as hello user who configures hello setting has appropriate RBAC access tooboth subscriptions.</span></span>

### <a name="via-azure-portal"></a><span data-ttu-id="5b397-120">Tramite il portale di Azure</span><span class="sxs-lookup"><span data-stu-id="5b397-120">Via Azure portal</span></span>
1. <span data-ttu-id="5b397-121">Passare toohello **Log attività** pannello utilizzando il menu di hello hello il lato sinistro di portale hello.</span><span class="sxs-lookup"><span data-stu-id="5b397-121">Navigate toohello **Activity Log** blade using hello menu on hello left side of hello portal.</span></span>
   
    ![Passare tooActivity Log nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="5b397-123">Fare clic su hello **esportare** pulsante nella parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="5b397-123">Click hello **Export** button at hello top of hello blade.</span></span>
   
    ![Pulsante Esporta nel portale](./media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="5b397-125">Nel pannello hello che viene visualizzata, è possibile selezionare le aree di hello per il quale si desidera toostream eventi e hello Service Bus Namespace nel quale si desidera toobe un Hub eventi creato per lo streaming di questi eventi.</span><span class="sxs-lookup"><span data-stu-id="5b397-125">In hello blade that appears, you can select hello regions for which you would like toostream events and hello Service Bus Namespace in which you would like an Event Hub toobe created for streaming these events.</span></span>
   
    ![Pannello Esporta log di controllo](./media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="5b397-127">Fare clic su **salvare** toosave queste impostazioni.</span><span class="sxs-lookup"><span data-stu-id="5b397-127">Click **Save** toosave these settings.</span></span> <span data-ttu-id="5b397-128">le impostazioni di Hello sono immediatamente di essere applicati tooyour sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="5b397-128">hello settings are immediately be applied tooyour subscription.</span></span>

### <a name="via-powershell-cmdlets"></a><span data-ttu-id="5b397-129">Tramite i cmdlet di PowerShell</span><span class="sxs-lookup"><span data-stu-id="5b397-129">Via PowerShell Cmdlets</span></span>
<span data-ttu-id="5b397-130">Se esiste già un profilo di log, è necessario innanzitutto tooremove tale profilo.</span><span class="sxs-lookup"><span data-stu-id="5b397-130">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="5b397-131">Utilizzare `Get-AzureRmLogProfile` tooidentify se esiste un profilo di log</span><span class="sxs-lookup"><span data-stu-id="5b397-131">Use `Get-AzureRmLogProfile` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="5b397-132">In questo caso, utilizzare `Remove-AzureRmLogProfile` tooremove è.</span><span class="sxs-lookup"><span data-stu-id="5b397-132">If so, use `Remove-AzureRmLogProfile` tooremove it.</span></span>
3. <span data-ttu-id="5b397-133">Utilizzare `Set-AzureRmLogProfile` toocreate un profilo:</span><span class="sxs-lookup"><span data-stu-id="5b397-133">Use `Set-AzureRmLogProfile` toocreate a profile:</span></span>

```
Add-AzureRmLogProfile -Name my_log_profile -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

<span data-ttu-id="5b397-134">Hello ID regola Bus di servizio è una stringa con questo formato: {ID risorsa bus di servizio} /authorizationrules/ {nome}, ad esempio</span><span class="sxs-lookup"><span data-stu-id="5b397-134">hello Service Bus Rule ID is a string with this format: {service bus resource ID}/authorizationrules/{key name}, for example</span></span> 

### <a name="via-azure-cli"></a><span data-ttu-id="5b397-135">Tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="5b397-135">Via Azure CLI</span></span>
<span data-ttu-id="5b397-136">Se esiste già un profilo di log, è necessario innanzitutto tooremove tale profilo.</span><span class="sxs-lookup"><span data-stu-id="5b397-136">If a log profile already exists, you first need tooremove that profile.</span></span>

1. <span data-ttu-id="5b397-137">Utilizzare `azure insights logprofile list` tooidentify se esiste un profilo di log</span><span class="sxs-lookup"><span data-stu-id="5b397-137">Use `azure insights logprofile list` tooidentify if a log profile exists</span></span>
2. <span data-ttu-id="5b397-138">In questo caso, utilizzare `azure insights logprofile delete` tooremove è.</span><span class="sxs-lookup"><span data-stu-id="5b397-138">If so, use `azure insights logprofile delete` tooremove it.</span></span>
3. <span data-ttu-id="5b397-139">Utilizzare `azure insights logprofile add` toocreate un profilo:</span><span class="sxs-lookup"><span data-stu-id="5b397-139">Use `azure insights logprofile add` toocreate a profile:</span></span>

```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

<span data-ttu-id="5b397-140">Hello ID regola Bus di servizio è una stringa con questo formato: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="5b397-140">hello Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

## <a name="how-do-i-consume-hello-log-data-from-event-hubs"></a><span data-ttu-id="5b397-141">Come utilizzano i dati del log hello dagli hub eventi?</span><span class="sxs-lookup"><span data-stu-id="5b397-141">How do I consume hello log data from Event Hubs?</span></span>
<span data-ttu-id="5b397-142">[schema di Hello per hello Log attività è disponibile qui](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5b397-142">[hello schema for hello Activity Log is available here](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="5b397-143">Ogni evento si trova in una matrice di BLOB JSON denominati "record".</span><span class="sxs-lookup"><span data-stu-id="5b397-143">Each event is in an array of JSON blobs called “records.”</span></span>

## <a name="next-steps"></a><span data-ttu-id="5b397-144">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5b397-144">Next Steps</span></span>
* [<span data-ttu-id="5b397-145">Hello archivio account di archiviazione tooa Log attività</span><span class="sxs-lookup"><span data-stu-id="5b397-145">Archive hello Activity Log tooa storage account</span></span>](monitoring-archive-activity-log.md)
* [<span data-ttu-id="5b397-146">Panoramica di hello di hello Log attività di Azure</span><span class="sxs-lookup"><span data-stu-id="5b397-146">Read hello overview of hello Azure Activity Log</span></span>](monitoring-overview-activity-logs.md)
* <span data-ttu-id="5b397-147">[Set up an alert based on an Activity Log event](insights-auditlog-to-webhook-email.md) (Configurare un avviso in base a un evento del log attività)</span><span class="sxs-lookup"><span data-stu-id="5b397-147">[Set up an alert based on an Activity Log event](insights-auditlog-to-webhook-email.md)</span></span>

