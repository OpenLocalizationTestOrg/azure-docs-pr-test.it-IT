---
title: "Attività di accesso irregolare"
description: Questo report include accessi identificati come anomali dagli algoritmi di Machine Learning.
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: a5a270a9-a0eb-4a99-b04c-ccde3829ffe4
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 565321b6f3ad5988f383a701cb9d8bd5c9937795
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="irregular-sign-in-activity"></a>Attività di accesso irregolare
Gli accessi irregolari sono quelli individuati dagli algoritmi di Machine Learning in base a una condizione di tipo "tempo di spostamento impossibile" combinata con una posizione e un dispositivo di accesso anomali. È possibile che un pirata informatico abbia eseguito l'accesso con questo account.
Microsoft invierà una notifica tramite posta elettronica agli amministratori globali se si verificano 10 o più eventi di accesso anomalo in un intervallo di 30 giorni o meno. Assicurarsi di includere aad-alerts-noreply@mail.windowsazure.com nell'elenco dei mittenti attendibili.

