---
title: "aaaSign aggiuntivi dopo più errori"
description: "Un report indica gli utenti che hanno eseguito correttamente l'accesso dopo più tentativi di accesso consecutivi non riusciti."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: femila
editor: 
ms.assetid: e4ec1a39-9c20-418f-8a75-6497d0117176
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 48d137dc3abf65287cb3b9ba8a6ff10340f6741f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sign-ins-after-multiple-failures"></a>Accessi dopo più errori
Questo report indica gli utenti che hanno eseguito correttamente l'accesso dopo più tentativi di accesso consecutivi non riusciti. Le possibili cause includono:

* L'utente ha dimenticato la password</li><li>Utente è vittima hello di una password ha esito positivo di un'ipotesi di attacco di forza bruta

Nei risultati del report verranno mostrati hello numero di tentativi consecutivi non accedi apportati toohello precedente ha esito positivo Accedi e un timestamp associato hello primo ha esito positivo Accedi.

**Report impostazioni**: È possibile configurare il numero minimo di hello di accesso non riusciti consecutivi tentativi che devono verificarsi prima che possono essere visualizzato nel report hello. Quando si apportano modifiche toothis impostarlo è toonote importante che tali modifiche non verranno applicati tooany esistente non riuscita accessi che attualmente visualizzati nel rapporto. Tuttavia, saranno applicati tooall future-accessi. Le modifiche toothis report può essere apportata esclusivamente dagli amministratori autorizzati.

![Accessi dopo più errori](./media/active-directory-reporting-sign-ins-after-multiple-failures/signInsAfterMultipleFailures.PNG)

