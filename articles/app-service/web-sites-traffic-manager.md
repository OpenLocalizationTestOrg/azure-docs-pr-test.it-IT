---
title: Controllo del traffico delle app Web di Azure con Gestione traffico di Azure
description: Questo articolo fornisce informazioni di riepilogo per Gestione traffico di Azure in relazione alle app Web di Azure.
services: app-service\web
documentationcenter: 
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: dabda633-e72f-4dd4-bf1c-6e945da456fd
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/25/2016
ms.author: cephalin
ms.openlocfilehash: fb7d391e3118a9dccde5501c3f30c6f580932a30
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Controllo del traffico delle app Web di Azure con Gestione traffico di Azure
> [!NOTE]
> In questo articolo vengono fornite informazioni di riepilogo per Gestione traffico di Azure di Microsoft in relazione alle app Web di Azure App Service. Per ulteriori informazioni su Gestione traffico di Azure, visitare i collegamenti forniti alla fine di questo articolo.
> 
> 

## <a name="introduction"></a>Introduzione
È possibile usare Gestione traffico di Azure per controllare il modo in cui le richieste dai client Web vengono distribuite alle app Web in Azure App Service. Quando si aggiungono endpoint delle app Web a un profilo di Gestione traffico di Azure, questo tiene traccia dello stato delle app Web (in esecuzione, arrestate o eliminate) in modo da poter decidere quali di questi endpoint devono ricevere il traffico.

## <a name="load-balancing-methods"></a>Metodi di bilanciamento del carico.
Gestione traffico di Azure utilizza tre metodi diversi per il bilanciamento del carico. Questi metodi vengono descritti nell'elenco seguente, in quanto pertinenti alle app Web di Azure.

* **Failover**: se sono presenti cloni di app Web in aree diverse, è possibile utilizzare questo metodo per configurare un'app Web in modo da gestire tutto il traffico dei client Web e un'altra, in un'area diversa, per gestire tale traffico nel caso in cui il primo sito Web risulti non disponibile.
* **Round Robin**: se sono presenti cloni di app Web in aree diverse, è possibile utilizzare questo metodo per distribuire equamente il traffico tra app Web in aree diverse.
* **Performance**: il metodo Prestazioni consente di distribuire il traffico in base al tempo di round trip più breve per il raggiungimento dei client. Il metodo Prestazioni può essere utilizzato sia per le app Web all'interno della stessa area, sia per quelle in aree diverse.

## <a name="web-apps-and-traffic-manager-profiles"></a>App Web e profili di Gestione traffico
Per configurare il controllo del traffico delle app Web, è possibile creare un profilo in Gestione traffico di Azure che utilizzi uno dei tre metodi di bilanciamento del carico, descritti in precedenza, e quindi aggiungere gli endpoint (in questo caso, le app Web) per i quali si desidera controlla il traffico diretto al profilo. Lo stato dell'app Web app (in esecuzione, interrotta o eliminata) viene comunicato regolarmente al profilo in modo che Gestione traffico di Azure possa instradare il traffico di conseguenza.

Quando si utilizza Gestione traffico con Azure, è opportuno tenere presenti i fattori seguenti:

* Per le distribuzioni di sole app We all'interno della stessa area, App Web fornisce già la funzionalità di failover e round-robin che non tengono conto della modalità delle app Web.
* Per distribuzioni nella stessa area in cui App Web viene utilizzato insieme a un altro servizio cloud di Azure, è possibile combinare entrambi i tipi di endpoint per abilitare scenari ibridi.
* È possibile specificare solo un endpoint dell'app Web per area in un profilo. Quando si seleziona un'app Web come endpoint per un'area, le app Web rimanenti in quell'area non saranno più disponibili per la selezione per quel profilo.
* Gli endpoint delle app Web che si specificano in un profilo di Gestione traffico di Azure verranno visualizzati nella sezione **Nomi domini** della pagina Configura per le app Web nel profilo, ma non saranno configurabili in quel contesto.
* Dopo l'aggiunta di un'app Web a un profilo, in **URL del sito** nel dashboard della pagina del portale dell'app Web verrà visualizzato l'URL del dominio personalizzato dell'app Web, se configurato. In caso contrario, verrà visualizzato l'URL del profilo di Gestione traffico, ad esempio `contoso.trafficmgr.com`. Sia il nome di dominio diretto dell'app Web, sia l'URL di Gestione traffico saranno visibili nella pagina Configura dell'app Web nella sezione **Nomi domini** .
* I nomi di dominio personalizzato funzioneranno come previsto, ma oltre ad aggiungerli alle app Web, sarà necessario configurare il mapping DNS in modo da puntare all'URL di Gestione traffico. Per informazioni sulla configurazione di un nome di dominio personalizzato per un'app Web di Azure, vedere [Configurazione di un nome di dominio personalizzato per un sito Web di Azure](app-service-web-tutorial-custom-domain.md).
* È possibile aggiungere al profilo di Gestione traffico di Azure solo app Web che si trovano in modalità Standard o Premium.

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica concettuale e tecnica di Gestione traffico di Azure, vedere [Panoramica di Gestione traffico](../traffic-manager/traffic-manager-overview.md).

Per altre informazioni sull'uso di Gestione traffico con App Web, vedere i post di blog relativi all'[uso di Gestione traffico di Azure con Siti Web di Azure](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) e [all'integrazione di Gestione traffico di Azure con Siti Web di Azure](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

