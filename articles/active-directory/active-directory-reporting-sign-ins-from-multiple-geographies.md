---
title: "Accessi da più aree geografiche"
description: "Report che segnala agli utenti situazioni in cui due accessi sembrano provenire da diverse aree, ma dato il tempo intercorso tra gli accessi non è possibile che l'utente si sia spostato da un'area all'altra."
services: active-directory
documentationcenter: 
author: SSalahAhmed
manager: gchander
editor: 
ms.assetid: 79259c8a-2388-4747-b41e-c07434ea9a02
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/04/2016
ms.author: saah;kenhoff
ms.openlocfilehash: 1de57f64692ade442f9ef8d1e3b587ffee35d7cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="sign-ins-from-multiple-geographies"></a>Accessi da più aree geografiche
Questo report mostra gli accessi effettuati da un utente e due di questi sembrano provenire da aree diverse. Dato il tempo intercorso tra gli accessi non è possibile che l'utente si sia spostato da un'area all'altra. Le possibili cause includono:

* L'utente sta condividendo la password
* L'utente usa un desktop remoto per avviare un Web browser per l'accesso
* Un pirata informatico ha effettuato l'accesso all'account di un utente da un altro paese
* L’utente sta usando una VPN o un proxy
* L'utente ha eseguito l'accesso da più dispositivi contemporaneamente, ad esempio da un computer desktop e da un cellulare, e l'indirizzo IP del cellulare è insolito.

Nei risultati del report verranno mostrati gli eventi di accesso riuscito, nonché il tempo tra gli accessi, le aree da cui gli accessi sembrano provenire e il tempo di spostamento stimato tra queste aree. Il tempo di spostamento mostrato è solo una stima e può essere diverso da quello effettivamente necessario per spostarsi da una posizione all’altra.

![Accessi da più aree geografiche](./media/active-directory-reporting-sign-ins-from-multiple-geographies/signInsFromMultipleGeographies.PNG)

