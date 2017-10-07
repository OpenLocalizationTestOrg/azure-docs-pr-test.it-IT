---
title: aaaOverview di metriche in Microsoft Azure | Documenti Microsoft
description: Informazioni su come toocustomize monitoraggio grafici in Azure.
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c36031eb-4df5-4cd5-9479-311d493a40d2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: robb
ms.openlocfilehash: 4196b2e9bda713e9a0abc349eed78685abcaf194
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-metrics-in-microsoft-azure"></a>Panoramica delle metriche in Microsoft Azure
Tutti i servizi di Azure di tenere traccia delle metriche chiave che consentono di integrità hello toomonitor, prestazioni, disponibilità e utilizzo dei servizi. È possibile visualizzare queste metriche nel portale di Azure hello ed è anche possibile usare hello [API REST](https://msdn.microsoft.com/library/azure/dn931930.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello set completo di metriche a livello di codice.

Per alcuni servizi, potrebbe essere necessario tooturn sulla diagnostica in ordine toosee delle metriche. Per altri utenti, ad esempio macchine virtuali, si otterrà un set di metriche di base, ma necessario tooenable hello set completo di metriche di ad alta frequenza. Vedere [attivazione del monitoraggio e diagnostica](insights-how-to-use-diagnostics.md) toolearn altre.

## <a name="using-monitoring-charts"></a>Uso di grafici di monitoraggio
È possibile grafico delle metriche hello usarle in qualsiasi periodo di tempo scelto.

1. In hello [portale Azure](https://portal.azure.com/), fare clic su **Sfoglia**, e quindi una risorsa si desidera monitorare.
2. Hello **monitoraggio** sezione contiene le metriche più importanti di hello per ogni risorsa di Azure. Ad esempio, un'app Web contiene **Richieste ed errori**, mentre una macchina virtuale includerebbe **Percentuale CPU** e **Lettura e scrittura disco**: ![Sezione Monitoraggio](./media/insights-how-to-customize-monitoring/Insights_MonitoringChart.png)
3. Facendo clic su qualsiasi grafico mostrerà hello **metrica** blade. Nel pannello hello inoltre toohello grafico, è una tabella che mostra le aggregazioni di metriche di hello (ad esempio Media, minimo e massimo, in intervallo di tempo hello scelto). Di seguito che è hello le regole di avviso per la risorsa hello.
    ![Pannello Metrica](./media/insights-how-to-customize-monitoring/Insights_MetricBlade.png)
4. linee di hello toocustomize visualizzate, fare clic su hello **modifica** pulsante grafico hello o hello **Modifica grafico** comando blade metriche hello.
5. Nel Pannello di modifica Query hello è possibile eseguire tre operazioni:
   
   * Modificare l'intervallo di tempo hello
   * Cambiare l'aspetto di hello tra barra e linea
   * Scegliere metriche diverse ![Modifica query](./media/insights-how-to-customize-monitoring/Insights_EditQuery.png)
6. Modifica intervallo di tempo hello è sufficiente selezionare un intervallo diverso (ad esempio **ora precedente**) e fare clic su **salvare** nella parte inferiore di hello del pannello hello. È anche possibile scegliere **personalizzata**, che consente di toochoose qualsiasi periodo di tempo su hello ultime 2 settimane. Ad esempio, è possibile visualizzare hello interi due settimane o, semplicemente 1 ora da ieri. Digitare un altro in tooenter casella di testo hello ora.
    ![Intervallo di tempo personalizzato](./media/insights-how-to-customize-monitoring/Insights_CustomTime.png)
7. Sotto l'intervallo di tempo hello, il canale è scegliere un numero qualsiasi di tooshow metriche sul grafico hello.
8. Quando si fa clic su Salva, verranno salvate le modifiche per quella specifica risorsa. Ad esempio, se si dispone di due macchine virtuali e si modifica un grafico in una, non influirà sugli altri hello.

## <a name="creating-side-by-side-charts"></a>Creazione di grafici affiancati
Con personalizzate nel portale di hello hello è possibile aggiungere il numero di grafici desiderato.

1. In hello **...**  menu nella parte superiore di hello di fare clic su Pannello hello **aggiungere riquadri**:  
    ![Menu di aggiunta](./media/insights-how-to-customize-monitoring/Insights_AddMenu.png)
2. Quindi, è possibile selezionare un grafico da hello **raccolta** hello destra dello schermo: ![raccolta](./media/insights-how-to-customize-monitoring/Insights_Gallery.png)
3. Se non viene visualizzato metriche hello desiderate, è sempre possibile aggiungere uno di hello preimpostato, metriche e **modifica** hello metrica di hello tooshow grafico che è necessario.

## <a name="monitoring-usage-quotas"></a>Monitoraggio delle quote di utilizzo
La maggior parte delle metriche mostrano le tendenze nel tempo, ma alcuni dati, come le quote di utilizzo, sono informazioni temporizzate con una soglia.

È inoltre possibile visualizzare le quote di utilizzo nel Pannello di hello per le risorse che dispone di quote:

![Utilizzo](./media/insights-how-to-customize-monitoring/Insights_UsageChart.png)

Come con le metriche, è possibile utilizzare hello [API REST](https://msdn.microsoft.com/library/azure/dn931963.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooaccess hello set completo di quote di utilizzo a livello di codice.

## <a name="next-steps"></a>Passaggi successivi
* [Ricevere notifiche di avviso](insights-receive-alert-notifications.md) ogni volta che una metrica supera una soglia.
* [Attivazione del monitoraggio e diagnostica](insights-how-to-use-diagnostics.md) toocollect dettagliate ad alta frequenza metriche sul servizio.
* [Ridimensionamento automatico di conteggio delle istanze](insights-how-to-scale.md) toomake che il servizio sia disponibile e reattiva.
* [Monitorare le prestazioni dell'applicazione](../application-insights/app-insights-azure-web-apps.md) se si desidera toounderstand esattamente come il codice viene eseguito nel cloud hello.
* Utilizzare [Application Insights per le app JavaScript e pagine web](../application-insights/app-insights-web-track-usage.md) analitica client tooget sui browser hello che visita una pagina web.
* [Monitorare la disponibilità e i tempi di risposta di qualsiasi pagina Web](../application-insights/app-insights-monitor-web-app-availability.md) con Application Insights per definire se la pagina è inattiva.

