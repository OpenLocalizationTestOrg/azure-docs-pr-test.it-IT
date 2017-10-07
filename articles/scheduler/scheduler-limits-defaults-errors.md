---
title: aaaScheduler limiti e i valori predefiniti
description: "Limiti e impostazioni predefinite dell'Utilità di pianificazione"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 88f4a3e9-6dbd-4943-8543-f0649d423061
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 6fe0600d3ce3249d5aab1b877369b175316b5437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-limits-and-defaults"></a>Limiti e impostazioni predefinite dell'Utilità di pianificazione
## <a name="scheduler-quotas-limits-defaults-and-throttles"></a>Quote, limiti, impostazioni predefinite e limiti dell'utilità di pianificazione
[!INCLUDE [scheduler-limits-table](../../includes/scheduler-limits-table.md)]

## <a name="hello-x-ms-request-id-header"></a>Hello x-ms-request-id intestazione
Ogni richiesta effettuata hello servizio Utilità di pianificazione restituisce un'intestazione di risposta denominata**x-ms-request-id**. Questa intestazione contiene un valore opaco che identifica in modo univoco la richiesta hello.

Se una richiesta è costantemente esito negativo e si sono verificate che hello corretta formulazione è, è possibile utilizzare questo errore tooMicrosoft di valore tooreport hello. Nel report, includere il valore di hello di x-ms-request-id, hello ora approssimativa in cui è stata effettuata la richiesta di hello, hello identificatore di sottoscrizione hello, raccolta di processi e/o processo e tipo di operazione hello richiesta ha tentato di hello.

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

