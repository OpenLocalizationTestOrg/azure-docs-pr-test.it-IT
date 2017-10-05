---
title: Limitazione della frequenza per SMS, messaggi di posta elettronica e Webhook | Microsoft Docs
description: Informazioni su come Azure limita il numero di possibili notifiche tramite SMS, posta elettronica o webhook da un gruppo di azione.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: bde645624ab1860d19ba18470f55845855a7d1fb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="e4d00-103">Limitazione della frequenza per i messaggi SMS e di posta elettronica e per i post webhook</span><span class="sxs-lookup"><span data-stu-id="e4d00-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="e4d00-104">La limitazione della frequenza è una sospensione delle notifiche che si verifica quando un numero eccessivo di notifiche viene inviato a un particolare numero telefono o indirizzo di posta elettronica.</span><span class="sxs-lookup"><span data-stu-id="e4d00-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent to a particular phone number or email address.</span></span> <span data-ttu-id="e4d00-105">La limitazione assicura che gli avvisi siano gestibili ed eseguibili.</span><span class="sxs-lookup"><span data-stu-id="e4d00-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="e4d00-106">Le regole per SMS e messaggi di posta elettronica sono uguali.</span><span class="sxs-lookup"><span data-stu-id="e4d00-106">The rules for SMS and email are the same.</span></span> <span data-ttu-id="e4d00-107">Il limite della soglia di frequenza è:</span><span class="sxs-lookup"><span data-stu-id="e4d00-107">The rate limit threshold is:</span></span>

 - <span data-ttu-id="e4d00-108">**SMS**: 10 messaggi in un'ora.</span><span class="sxs-lookup"><span data-stu-id="e4d00-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="e4d00-109">**Messaggi di posta elettronica**: 100 messaggi in un'ora.</span><span class="sxs-lookup"><span data-stu-id="e4d00-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="e4d00-110">Regole dei limiti di frequenza</span><span class="sxs-lookup"><span data-stu-id="e4d00-110">Rate limit rules</span></span>
- <span data-ttu-id="e4d00-111">Vengono messi i limiti di frequenza per uno specifico numero di telefono o un indirizzo di posta elettronica quando si ricevono più avvisi rispetto alla soglia di frequenza.</span><span class="sxs-lookup"><span data-stu-id="e4d00-111">A particular phone number or email is rate limited when it receives more messages than the threshold allows.</span></span>
- <span data-ttu-id="e4d00-112">Un numero di telefono o un indirizzo di posta elettronica può fare parte di gruppi di azione tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e4d00-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="e4d00-113">La limitazione della frequenza viene applicata a tutte le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e4d00-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="e4d00-114">Al raggiungimento della soglia, si applica anche se i messaggi vengono inviati da più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="e4d00-114">It applies as soon as the threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="e4d00-115">Quando un numero di telefono o un messaggio di posta elettronica ha una limitazione della frequenza, viene inviata una notifica aggiuntiva per comunicare tale limitazione.</span><span class="sxs-lookup"><span data-stu-id="e4d00-115">When a phone number or email is rate limited, an additional notification is sent to communicate the rate limiting.</span></span> <span data-ttu-id="e4d00-116">La notifica indica la scadenza della limitazione della frequenza.</span><span class="sxs-lookup"><span data-stu-id="e4d00-116">The notification states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="e4d00-117">Limitazione della frequenza di webhook</span><span class="sxs-lookup"><span data-stu-id="e4d00-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="e4d00-118">Non esiste alcuna limitazione della frequenza per webhook.</span><span class="sxs-lookup"><span data-stu-id="e4d00-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4d00-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e4d00-119">Next steps</span></span> ##
* <span data-ttu-id="e4d00-120">Altre informazioni sul [Comportamento degli avvisi SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="e4d00-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="e4d00-121">Leggere una [panoramica degli avvisi del log attività](monitoring-overview-alerts.md) e informazioni su come ricevere gli avvisi.</span><span class="sxs-lookup"><span data-stu-id="e4d00-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how to receive alerts.</span></span>  
* <span data-ttu-id="e4d00-122">Informazioni su come [configurare gli avvisi ogni volta che viene inviata una notifica sull'integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="e4d00-122">Learn how to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
