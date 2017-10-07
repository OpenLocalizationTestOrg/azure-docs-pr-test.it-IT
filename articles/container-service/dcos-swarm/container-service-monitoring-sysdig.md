---
title: un servizio di contenitore di Azure aaaMonitor cluster con Sysdig | Documenti Microsoft
description: Monitorare un cluster del servizio contenitore di Azure con Sysdig.
services: container-service
documentationcenter: 
author: sauryadas
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: Contenitori, controller di dominio/sistema operativo, Azure
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2016
ms.author: saudas
ms.custom: mvc
ms.openlocfilehash: 72f2d3d6f6885f9876fa158b88aae58b84a4610f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-an-azure-container-service-cluster-with-sysdig"></a>Monitorare un cluster del servizio contenitore di Azure con Sysdig
In questo articolo, si distribuirà Sysdig agenti tooall hello agente i nodi del cluster del servizio di contenitore di Azure. Per questa configurazione, è necessario un account con Sysdig. 

## <a name="prerequisites"></a>Prerequisiti
[Distribuire](container-service-deployment.md) e [connettere](../container-service-connect.md) un cluster configurato dal servizio contenitore di Azure. Esplorare hello [dell'interfaccia utente maratona](container-service-mesos-marathon-ui.md). Andare troppo[http://app.sysdigcloud.com](http://app.sysdigcloud.com) tooset di un account cloud Sysdig. 

## <a name="sysdig"></a>Sysdig
Sysdig è un servizio di monitoraggio che consente di toomonitor ai contenitori all'interno del cluster. Sysdig è noto toohelp la risoluzione dei problemi, ma include anche le metriche di monitoraggio di base per la CPU, rete, memoria e i/o. Sysdig rende facile toosee utilizzano i contenitori hello più difficili o essenzialmente utilizzando hello la maggior parte di memoria e CPU. Questa visualizzazione è nella sezione "Overview", in cui è attualmente in versione beta di hello. 

![Interfaccia utente di Sysdig](./media/container-service-monitoring-sysdig/sysdig6.png) 

## <a name="configure-a-sysdig-deployment-with-marathon"></a>Configurare una distribuzione Sysdig con Marathon
Questa procedura viene illustrato come tooconfigure e la distribuzione Sysdig applicazioni tooyour cluster con maratona. 

Accedere all'interfaccia del controller di dominio o del sistema operativo tramite [http://localhost:80 /](http://localhost:80/) una volta nell'interfaccia utente di controller di dominio/OS hello passare toohello "Universo", che si trova in hello in basso a sinistra e quindi cerca "Sysdig".

![Sysdig in Universe (Universo) per il controller di dominio/sistema operativo](./media/container-service-monitoring-sysdig/sysdig1.png)

Ora configuration hello toocomplete è necessario un Sysdig cloud account o un account di prova. Dopo aver eseguito il nel sito Web di toohello Sysdig cloud, fare clic sul nome utente e nella pagina di hello si dovrebbe visualizzare la "chiave di accesso". 

![Chiave API di Sysdig](./media/container-service-monitoring-sysdig/sysdig2.png) 

Quindi immettere la chiave di accesso alla configurazione Sysdig hello all'interno di hello l'universo dei controller di dominio o del sistema operativo. 

![Configurazione Sysdig in hello l'universo dei controller di dominio o del sistema operativo](./media/container-service-monitoring-sysdig/sysdig3.png)

Ora impostato hello istanze too10000000 pertanto ogni volta che viene aggiunto un nuovo nodo cluster toohello Sysdig distribuirà automaticamente un agente toothat nuovo nodo. Si tratta di un toomake soluzione temporanea che Sysdig distribuirà tooall nuovi agenti all'interno di cluster hello. 

![Configurazione Sysdig nel controller di dominio o del sistema operativo universo-le istanze di hello](./media/container-service-monitoring-sysdig/sysdig4.png)

Dopo aver installato il pacchetto di hello spostarsi indietro toohello Sysdig UI e sarà in grado di tooexplore hello diversi le metriche di utilizzo contenitori hello all'interno del cluster. 

È anche possibile installare i dashboard specifici di Mesos e Marathon tramite la [creazione guidata nuovo dashboard](https://app.sysdigcloud.com/#/dashboards/new).
