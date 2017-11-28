---
title: limitazione di aaaRate per SMS, messaggi di posta elettronica e ai webhook | Documenti Microsoft
description: Comprendere in che modo Azure limita il numero di hello delle possibili notifiche SMS, posta elettronica o webhook da un gruppo di azioni.
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
ms.openlocfilehash: 1cd08a5b982c82bb02e0bf93451aa1fcd9bc34af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a><span data-ttu-id="15212-103">Limitazione della frequenza per i messaggi SMS e di posta elettronica e per i post webhook</span><span class="sxs-lookup"><span data-stu-id="15212-103">Rate limiting for SMS messages, emails, and webhook posts</span></span>
<span data-ttu-id="15212-104">La limitazione della velocità è una sospensione di notifiche che si verifica quando l'indirizzo di posta elettronica o numero di telefono specifico tooa è vengono inviate le notifiche di un numero eccessivo.</span><span class="sxs-lookup"><span data-stu-id="15212-104">Rate limiting is a suspension of notifications that occurs when too many notifications are sent tooa particular phone number or email address.</span></span> <span data-ttu-id="15212-105">La limitazione assicura che gli avvisi siano gestibili ed eseguibili.</span><span class="sxs-lookup"><span data-stu-id="15212-105">Rate limiting ensures that alerts are manageable and actionable.</span></span>

<span data-ttu-id="15212-106">le regole di Hello per posta elettronica e SMS sono hello stesso.</span><span class="sxs-lookup"><span data-stu-id="15212-106">hello rules for SMS and email are hello same.</span></span> <span data-ttu-id="15212-107">limite della soglia di frequenza Hello è:</span><span class="sxs-lookup"><span data-stu-id="15212-107">hello rate limit threshold is:</span></span>

 - <span data-ttu-id="15212-108">**SMS**: 10 messaggi in un'ora.</span><span class="sxs-lookup"><span data-stu-id="15212-108">**SMS**: 10 messages in an hour.</span></span>
 - <span data-ttu-id="15212-109">**Messaggi di posta elettronica**: 100 messaggi in un'ora.</span><span class="sxs-lookup"><span data-stu-id="15212-109">**Email**: 100 messages in an hour.</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="15212-110">Regole dei limiti di frequenza</span><span class="sxs-lookup"><span data-stu-id="15212-110">Rate limit rules</span></span>
- <span data-ttu-id="15212-111">Un numero di telefono specifico o di un messaggio di posta elettronica è limitato quando riceve più messaggi di quanti soglia hello consente di frequenza.</span><span class="sxs-lookup"><span data-stu-id="15212-111">A particular phone number or email is rate limited when it receives more messages than hello threshold allows.</span></span>
- <span data-ttu-id="15212-112">Un numero di telefono o un indirizzo di posta elettronica può fare parte di gruppi di azione tra più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="15212-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="15212-113">La limitazione della frequenza viene applicata a tutte le sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="15212-113">Rate limiting applies across all subscriptions.</span></span> <span data-ttu-id="15212-114">Non appena viene raggiunta la soglia hello, si applica anche se i messaggi vengono inviati da più sottoscrizioni.</span><span class="sxs-lookup"><span data-stu-id="15212-114">It applies as soon as hello threshold is reached, even if messages are sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="15212-115">Quando un numero di telefono o posta elettronica è limitato di velocità, una notifica aggiuntiva verrà inviata toocommunicate hello la limitazione della velocità.</span><span class="sxs-lookup"><span data-stu-id="15212-115">When a phone number or email is rate limited, an additional notification is sent toocommunicate hello rate limiting.</span></span> <span data-ttu-id="15212-116">Hello stati quando hello limitazione di velocità di notifica di scadenza.</span><span class="sxs-lookup"><span data-stu-id="15212-116">hello notification states when hello rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="15212-117">Limitazione della frequenza di webhook</span><span class="sxs-lookup"><span data-stu-id="15212-117">Rate limit of webhooks</span></span> ##
<span data-ttu-id="15212-118">Non esiste alcuna limitazione della frequenza per webhook.</span><span class="sxs-lookup"><span data-stu-id="15212-118">There is no rate limiting in place for webhooks.</span></span>

## <a name="next-steps"></a><span data-ttu-id="15212-119">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15212-119">Next steps</span></span> ##
* <span data-ttu-id="15212-120">Altre informazioni sul [Comportamento degli avvisi SMS](monitoring-sms-alert-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="15212-120">Learn more about [SMS alert behavior](monitoring-sms-alert-behavior.md).</span></span>
* <span data-ttu-id="15212-121">Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md)e informazioni su come tooreceive avvisi.</span><span class="sxs-lookup"><span data-stu-id="15212-121">Get an [overview of activity log alerts](monitoring-overview-alerts.md), and learn how tooreceive alerts.</span></span>  
* <span data-ttu-id="15212-122">Informazioni su come troppo[configurare gli avvisi ogni volta che viene registrata una notifica di integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).</span><span class="sxs-lookup"><span data-stu-id="15212-122">Learn how too[configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md).</span></span>
