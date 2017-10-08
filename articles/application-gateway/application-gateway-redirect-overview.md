---
title: Panoramica di aaaRedirect per il Gateway applicazione Azure | Documenti Microsoft
description: "Informazioni sulle funzionalità di reindirizzamento hello in Gateway applicazione Azure"
services: application-gateway
documentationcenter: na
author: amsriva
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/18/2017
ms.author: amsriva
ms.openlocfilehash: 7149e3bd000d336c51995fb0e90f971b4d9ba2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="application-gateway-redirect-overview"></a>Panoramica del reindirizzamento nel gateway applicazione

Uno scenario comune per numerose applicazioni web è toosupport automatico HTTP tooHTTPS reindirizzamento tooensure che tutte le comunicazioni tra applicazioni e gli utenti si verificano su un percorso crittografato. Nelle ultime hello, i clienti utilizzare tecniche, ad esempio la creazione di un pool back-end dedicato con l'unico scopo è tooredirect richieste ricevute in tooHTTPS HTTP.  Gateway applicazione supporta ora il possibilità tooredirect traffico sul Gateway applicazione hello. Questo semplifica la configurazione dell'applicazione, ottimizza l'utilizzo delle risorse hello e supporta i nuovi scenari di reindirizzamento, tra cui globale e basata sul percorso di reindirizzamento. Supporto per il reindirizzamento Gateway applicazione non è limitato tooHTTP -> solo il reindirizzamento di HTTPS. Si tratta di un meccanismo di reindirizzamento generico, che consente il reindirizzamento del traffico ricevuto al listener di un listener tooanother nel Gateway applicazione. Supporta inoltre il reindirizzamento tooan esterno anche nel sito. Supporto per il reindirizzamento Gateway applicazione offre hello seguenti funzionalità:

1. Reindirizzamento globale dal listener tooanother un listener su hello Gateway. In questo modo il reindirizzamento tooHTTPS HTTP in un sito.
2. Reindirizzamento basato sul percorso. Questo tipo di reindirizzamento consente il reindirizzamento tooHTTPS HTTP solo in un'area del sito specifico, ad esempio un'area del carrello acquisti indicato dal carrello / *.
3. Reindirizzamento tooexternal sito.

![Reindirizzamento](./media/application-gateway-redirect-overview/redirect.png)

Con questa modifica, i clienti sarà necessario un nuovo oggetto di configurazione di reindirizzamento, che specifica il listener di destinazione hello toocreate o reindirizzamento toowhich sito esterno è desiderato. elemento di configurazione Hello supporta inoltre opzioni tooenable aggiungendo il percorso URI hello e query toohello stringa URL di reindirizzamento. I clienti possono anche scegliere se il reindirizzamento è temporaneo (codice di stato HTTP 302) o permanente (codice di stato HTTP 301). Una volta creata questa configurazione di reindirizzamento è listener origine toohello collegati tramite una nuova regola. Quando si utilizza una regola di base, configurazione di reindirizzamento hello è associata a un listener di origine e un reindirizzamento globale. Quando viene utilizzata una regola di percorso, configurazione di reindirizzamento hello è definito nella mappa del percorso URL hello e pertanto si applica solo toohello area di un percorso specifico di un sito.

### <a name="next-steps"></a>Passaggi successivi

[Configure URL redirection on an application gateway (Configurare il reindirizzamento dell'URL in un gateway applicazione)](application-gateway-configure-redirect-powershell.md)
