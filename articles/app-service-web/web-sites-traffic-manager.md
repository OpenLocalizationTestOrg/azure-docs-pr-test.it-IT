---
title: aaaControlling il traffico di app web di Azure con gestione traffico di Azure
description: In questo articolo fornisce informazioni di riepilogo per gestione traffico di Azure per quanto riguarda le applicazioni web tooAzure.
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
ms.openlocfilehash: a93d4c9370046d54e401e36e7b495af8b711a2aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="controlling-azure-web-app-traffic-with-azure-traffic-manager"></a>Controllo del traffico delle app Web di Azure con Gestione traffico di Azure
> [!NOTE]
> In questo articolo fornisce informazioni di riepilogo per gestione traffico di Microsoft Azure in relazione tooAzure App del servizio Web App. Sono disponibili ulteriori informazioni su gestione traffico di Azure stesso, visitare i collegamenti di hello alla fine di hello di questo articolo.
> 
> 

## <a name="introduction"></a>Introduzione
È possibile utilizzare Azure Traffic Manager toocontrol come le richieste dai client web vengono distribuite tooweb App in Azure App Service. Quando gli endpoint di app web vengono aggiunte tooa profilo di Traffic Manager di Azure, gestione traffico di Azure tiene traccia di stato hello delle App web (in esecuzione, interrotta o eliminata) in modo che è possibile decidere quale di questi endpoint deve ricevere il traffico.

## <a name="load-balancing-methods"></a>Metodi di bilanciamento del carico.
Gestione traffico di Azure utilizza tre metodi diversi per il bilanciamento del carico. Questi elementi sono descritti nel seguente elenco come si riferiscono le app web tooAzure hello.

* **Failover**: se si dispone di cloni di app web in aree diverse, è possibile utilizzare questo tooservice di app web uno tooconfigure metodo tutto il traffico client web e configurare un'altra app web in tooservice un'area diversa di traffico in case hello prima web app non è più disponibile.
* **Round Robin**: se si dispone di cloni di app web in aree diverse, è possibile utilizzare equamente il traffico toodistribute (metodo) tra le applicazioni web hello in aree diverse.
* **Prestazioni**: hello metodo prestazioni distribuisce il traffico in base a tooclients tempo di round trip più breve hello. metodo prestazioni Hello può essere utilizzato per le applicazioni web all'interno di hello stessa area o in aree diverse.

## <a name="web-apps-and-traffic-manager-profiles"></a>App Web e profili di Gestione traffico
tooconfigure hello controllo del traffico di app web, si crea un profilo di Traffic Manager di Azure che utilizza uno dei metodi descritti in precedenza di bilanciamento del carico di hello tre e quindi aggiungere gli endpoint hello (in questo caso, le applicazioni web) per il quale si desidera toocontrol traffico toohello profilo. Lo stato di app web (in esecuzione, interrotta o eliminata) è toohello regolarmente comunicata del profilo in modo che Traffic Manager di Azure può indirizzare il traffico, di conseguenza.

Quando si utilizza Traffic Manager di Azure con Azure, tenere hello presente seguenti punti:

* Per le distribuzioni solo web app all'interno di hello stessa area, già l'App Web fornisce funzionalità di failover e round-robin senza la modalità dell'app tooweb conto.
* Per le distribuzioni in hello stessa regione che usano le app Web in combinazione con un altro servizio cloud di Azure, è possibile combinare entrambi i tipi di scenari ibridi tooenable di endpoint.
* È possibile specificare solo un endpoint dell'app Web per area in un profilo. Quando si seleziona un'app web come endpoint per un'area, hello rimanenti App web in tale area diventano non disponibili per la selezione per il profilo.
* gli endpoint di app web Hello specificato in un profilo di Traffic Manager di Azure verranno visualizzato in hello **i nomi di dominio** sezione nella pagina di configurazione hello per app web hello nel profilo di hello, ma non è possibile configurare non esiste.
* Dopo aver aggiunto un profilo di tooa app web, hello **URL del sito** in hello Dashboard Web hello pagina dell'app del portale visualizzerà hello URL di dominio personalizzato dell'app web hello se è stato configurato uno. In caso contrario, verrà visualizzato hello URL del profilo di gestione traffico (ad esempio, `contoso.trafficmgr.com`). Entrambi hello nome di dominio diretto dell'app web hello e hello URL di gestione traffico sarà visibile nella pagina Configura dell'app web hello in hello **i nomi di dominio** sezione.
* I nomi di dominio personalizzato funziona come previsto, ma in aggiunta tooadding li tooyour web App, è necessario configurare anche le toohello toopoint di mappa DNS URL di gestione traffico. Per informazioni su come tooset di un dominio personalizzato per un'app web di Azure, vedere [configurazione di un nome di dominio personalizzato per un sito web Azure](app-service-web-tutorial-custom-domain.md).
* È possibile aggiungere solo le app web in modalità standard o premium tooa profilo di Traffic Manager di Azure.

## <a name="next-steps"></a>Passaggi successivi
Per una panoramica concettuale e tecnica di Gestione traffico di Azure, vedere [Panoramica di Gestione traffico](../traffic-manager/traffic-manager-overview.md).

Per ulteriori informazioni sull'utilizzo di gestione traffico con le app Web, vedere il post di blog di hello [tramite Traffic Manager di Azure con siti Web di Azure](http://blogs.msdn.com/b/waws/archive/2014/03/18/using-windows-azure-traffic-manager-with-waws.aspx) e [Traffic Manager di Azure è ora possibile integrare con siti Web di Azure](https://azure.microsoft.com/blog/2014/03/27/azure-traffic-manager-can-now-integrate-with-azure-web-sites/).

