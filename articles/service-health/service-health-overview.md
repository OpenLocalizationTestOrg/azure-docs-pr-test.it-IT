---
title: "Panoramica dell'integrità del servizio aaaAzure | Documenti Microsoft"
description: Informazioni personalizzate su come le app di Azure sono interessate dalla manutenzione e dai problemi attuali e futuri dei servizi di Azure.
services: Resource health
documentationcenter: 
author: rboucher
manager: 
editor: 
ms.assetid: 
ms.service: service-health
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: Supportability
ms.date: 07/07/2017
ms.author: robb
ms.openlocfilehash: 2b536ee2f19757d4f2baf5529866c3d159a4670c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-health"></a>Integrità dei servizi di Azure
Integrità dei servizi di Azure offre informazioni tempestive e personalizzate quando nei servizi di Azure si verificano problemi che influiscono sui servizi.  Consente inoltre di preparare una manutenzione pianificata per il futuro.

## <a name="service-health-events"></a>Eventi di Integrità dei servizi
Integrità dei servizi registra tre tipi di eventi di integrità che possono influire sulle risorse:
1. **Problemi del servizio** -hello di eventuali problemi nei servizi di Azure che influiscono su è al momento. 
2. **La manutenzione pianificata** -manutenzione programmata che può influire sulla disponibilità hello dei servizi in hello future.  
3. **Avvisi sull'integrità**: modifiche apportate ai servizi di Azure che richiedono attenzione, ad esempio quando le funzionalità di Azure sono deprecate o si supera una quota di utilizzo.

    ![Eventi di Integrità dei servizi](./media/service-health-overview/azure-service-health-overview-7.png)

## <a name="get-started-with-service-health"></a>Introduzione a Integrità dei servizi
il dashboard di integrità del servizio, seleziona hello servizio integrità toolaunch riquadro nel dashboard del portale. Se in precedenza si è rimosso riquadro hello o dashboard personalizzati in uso, cercare il servizio di integrità del servizio in "Più servizi" (in basso a sinistra nel dashboard).
![Introduzione a Integrità dei servizi](./media/service-health-overview/azure-service-health-overview-1.png)

## <a name="see-current-issues-which-impact-your-services"></a>Vedere i problemi che attualmente influiscono su servizi
Hello **problemi del servizio** visualizzazione mostra eventuali problemi in corso in servizi di Azure che incidono sulle risorse. È possibile comprendere quando è iniziata problema hello e i servizi e le aree sono interessate. È inoltre possibile leggere toounderstand aggiornamento più recente di hello ciò che Azure esegue problema hello tooresolve. 
![Gestire il problema del servizio](./media/service-health-overview/azure-service-health-overview-2.png)

Scegliere hello **potenziale impatto** scheda toosee hello specifico elenco di risorse si è proprietari e che potrebbero essere interessati dal problema hello. È possibile scaricare un elenco CSV di tooshare queste risorse con il team.
![Gestire il problema del servizio - Impatto](./media/service-health-overview/azure-service-health-overview-4.png)

## <a name="get-links-and-downloadable-explanations"></a>Ottenere i collegamenti e spiegazioni scaricabili 
È possibile ottenere un collegamento per hello problema toouse nel sistema di gestione del problema. È possibile scaricare PDF e talvolta tooshare file CSV con utenti che non hanno accesso toohello portale di Azure.   
![Gestire il problema del servizio - Gestione dei problemi](./media/service-health-overview/azure-service-health-overview-3.png)

## <a name="get-support-from-microsoft"></a>Ricevere assistenza da Microsoft
Se la risorsa viene lasciata in uno stato non valido, anche dopo hello problema viene risolto, contattare il supporto tecnico.  Utilizzare collegamenti per il supporto di hello hello destra della pagina hello.  

## <a name="pin-a-personalized-health-map-tooyour-dashboard"></a>Aggiungere un dashboard di integrità personalizzato mappa tooyour
Filtrare tooshow di integrità dei servizi business-critical sottoscrizioni e le aree, tipi di risorse. Salvare il filtro hello e pin un integrità personalizzato world mappa tooyour del dashboard del portale. 
![Filtro con mappa dell'integrità personalizzata](./media/service-health-overview/azure-service-health-overview-6a.png)
![Aggiungere una mappa dell'integrità personalizzata](./media/service-health-overview/azure-service-health-overview-6b.png)

## <a name="configure-service-health-alerts"></a>Configurare gli avvisi di Integrità dei servizi
Integrità del servizio Azure si integra con Azure monitoraggio tooalert è tramite messaggi di posta elettronica, messaggi di testo e le notifiche di webhook quando le risorse aziendali critici sono interessate. Impostare un avviso di log attività per l'evento servizio integrità di hello appropriato. Route toohello persone appropriate nell'organizzazione tramite gruppi di azioni di avviso. Per altre informazioni, vedere [Configurare gli avvisi per Integrità dei servizi](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md)

# <a name="next-steps"></a>Passaggi successivi
Impostare gli avvisi per ricevere notifiche sui problemi di integrità. Per altre informazioni, vedere [Configurare gli avvisi per Integrità dei servizi](../monitoring-and-diagnostics/monitoring-activity-log-alerts-on-service-notifications.md). 