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
# <a name="rate-limiting-for-sms-messages-emails-and-webhook-posts"></a>Limitazione della frequenza per i messaggi SMS e di posta elettronica e per i post webhook
La limitazione della velocità è una sospensione di notifiche che si verifica quando l'indirizzo di posta elettronica o numero di telefono specifico tooa è vengono inviate le notifiche di un numero eccessivo. La limitazione assicura che gli avvisi siano gestibili ed eseguibili.

le regole di Hello per posta elettronica e SMS sono hello stesso. limite della soglia di frequenza Hello è:

 - **SMS**: 10 messaggi in un'ora.
 - **Messaggi di posta elettronica**: 100 messaggi in un'ora.

## <a name="rate-limit-rules"></a>Regole dei limiti di frequenza
- Un numero di telefono specifico o di un messaggio di posta elettronica è limitato quando riceve più messaggi di quanti soglia hello consente di frequenza.
- Un numero di telefono o un indirizzo di posta elettronica può fare parte di gruppi di azione tra più sottoscrizioni. La limitazione della frequenza viene applicata a tutte le sottoscrizioni. Non appena viene raggiunta la soglia hello, si applica anche se i messaggi vengono inviati da più sottoscrizioni.  
- Quando un numero di telefono o posta elettronica è limitato di velocità, una notifica aggiuntiva verrà inviata toocommunicate hello la limitazione della velocità. Hello stati quando hello limitazione di velocità di notifica di scadenza.

## <a name="rate-limit-of-webhooks"></a>Limitazione della frequenza di webhook ##
Non esiste alcuna limitazione della frequenza per webhook.

## <a name="next-steps"></a>Passaggi successivi ##
* Altre informazioni sul [Comportamento degli avvisi SMS](monitoring-sms-alert-behavior.md).
* Ottenere un [panoramica degli avvisi di log attività](monitoring-overview-alerts.md)e informazioni su come tooreceive avvisi.  
* Informazioni su come troppo[configurare gli avvisi ogni volta che viene registrata una notifica di integrità del servizio](monitoring-activity-log-alerts-on-service-notifications.md).
