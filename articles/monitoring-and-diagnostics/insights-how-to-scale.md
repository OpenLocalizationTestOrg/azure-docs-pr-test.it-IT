---
title: "aaaScale istanza conteggio manualmente o con scalabilità automatica con il portale di Azure | Documenti Microsoft"
description: Informazioni su come tooscale i servizi di Azure.
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 2397596a-071f-4d49-8893-bec5f735bd7b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/06/2017
ms.author: ancav
ms.openlocfilehash: 8cb78f18416bd3caecce52702a8d630aa434d776
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-instance-count-manually-or-automatically"></a>Scalare il conteggio delle istanze manualmente o automaticamente
In hello [portale Azure](https://portal.azure.com/), è possibile impostare manualmente il numero di istanze hello del servizio o, è possibile impostare parametri toohave automaticamente scalati in base alle esigenze. Si tratta in genere indicati tooas *scalabilità* o *ridimensionare in*.

Prima di ridimensionamento in base al numero di istanza, è consigliabile che la scalabilità è interessata dalla **tariffario** nel conteggio tooinstance aggiunta. Diversi livelli di prezzo possono avere diversi numeri core e la memoria e pertanto hanno un miglioramento delle prestazioni hello stesso numero di istanze (ovvero *scalabilità verticale* o *scalare verso il basso*). Questo articolo descrive in particolare la *riduzione* e l'*aumento del numero di istanze*.

È possibile scalare nel portale di hello ed è anche possibile usare hello [API REST](https://msdn.microsoft.com/library/azure/dn931953.aspx) o [.NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Management.Monitor) tooadjust ridimensionare manualmente o automaticamente.

> [!NOTE]
> Questo articolo viene descritto come toocreate un'impostazione nel portale di hello all'indirizzo di scalabilità automatica [http://portal.azure.com](http://portal.azure.com). Le impostazioni di scalabilità automatica create in questo portale non possono essere modificata, portale classico hello ([http://manage.windowsazure.com](http://manage.windowsazure.com)).
> 
> 

## <a name="scaling-manually"></a>Scalabilità manuale
1. In hello [portale Azure](https://portal.azure.com/), fare clic su **Sfoglia**, quindi passare toohello risorsa desiderata tooscale, ad esempio un **piano di servizio App**.
2. Fare clic su **Impostazioni > Scalabilità orizzontale (piano di servizio app).**
3. Nella parte superiore di hello di hello **scala** pannello è possibile visualizzare una cronologia delle azioni di scalabilità automatica del servizio hello.
   
    ![Scale blade](./media/insights-how-to-scale/Insights_ScaleBladeDayZero.png)
   
   > [!NOTE]
   > In questo grafico verranno visualizzate solo le azioni eseguite con la scalabilità automatica. Se si modifica manualmente il numero di istanze di hello, modifica hello non si rifletteranno nel grafico.
   > 
   > 
4. È possibile modificare manualmente il numero di hello **istanze** con dispositivo di scorrimento.
5. Fare clic su hello **salvare** comando e si verrà ridimensionato toothat numero di istanze quasi immediatamente.

## <a name="scaling-based-on-a-pre-set-metric"></a>Scalabilità basata su una metrica preimpostata
Se si desidera hello numero di istanze tooautomatically regolare in base a una metrica, selezionare hello metriche desiderate in hello **scalare** elenco a discesa. Ad esempio, per un **piano di servizio app** è possibile scalare in base alla **Percentuale CPU**.

1. Quando si seleziona una metrica si otterrà un dispositivo di scorrimento e/o, numero tooenter hello caselle di testo di istanze desiderato tooscale tra:
   
    ![Scale blade with CPU Percentage](./media/insights-how-to-scale/Insights_ScaleBladeCPU.png)
   
    Scalabilità automatica non avrà mai il servizio di sotto o di sopra dei limiti di hello impostate, indipendentemente dal carico di.
2. In secondo luogo, scegliere l'intervallo di destinazione hello per metrica hello. Ad esempio, se si sceglie **percentuale di CPU**, è possibile impostare una destinazione per hello utilizzo medio della CPU tra tutte le istanze di hello nel servizio. Una scalabilità orizzontale si verificherà quando hello utilizzo medio della CPU supera il massimo di hello che è definire, in modo analogo, una scala in verrà eseguito ogni volta che hello utilizzo medio della CPU scende di sotto di hello minimo.
3. Fare clic su hello **salvare** comando. Scalabilità automatica controllerà ogni pochi toomake minuti che siano intervallo istanza hello e di destinazione per l'unità di misura. Quando il servizio riceve altro traffico, il numero di istanze aumenterà automaticamente.

## <a name="scale-based-on-other-metrics"></a>Scalabilità in base ad altre metriche
È possibile scalare in base alle metriche diverso dal set di impostazioni di hello che vengono visualizzati in hello **scalare** elenco a discesa e anche possono avere un set complesso di scalabilità orizzontale e scalabilità nelle regole.

### <a name="adding-or-changing-a-rule"></a>Aggiunta o modifica di una regola
1. Scegliere hello **le regole di pianificazione e delle prestazioni** in hello **scalare** elenco a discesa: ![le regole di prestazioni](./media/insights-how-to-scale/Insights_PerformanceRules.png)
2. Se in precedenza era di scalabilità automatica, in si noterà una visualizzazione di regole precise hello che era.
3. tooscale in base a un'altra metrica fare clic su hello **Aggiungi regola** riga. È anche possibile scegliere uno di hello toochange di righe esistenti da metrica hello in precedenza era toohello metrica da tooscale da.
   ![Add rule](./media/insights-how-to-scale/Insights_AddRule.png)
4. È ora necessario tooselect la metrica desiderata tooscale da. Si è scelta una metrica sono tooconsider un paio di cose:
   
   * Hello *risorse* metrica hello proviene da. In genere, questo verrà essere hello stesso come risorsa hello è possibile scalare. Tuttavia, se si desidera tooscale dalla profondità hello di una coda di archiviazione, risorse hello sono coda hello che si desidera tooscale da.
   * Hello *nome metrica* stesso.
   * Hello *ora aggregazione* della metrica hello. Si tratta come dati hello sono combinare su hello *durata*.
5. Dopo aver scelto l'unità di misura è scegliere soglia hello per metrica hello e operatore hello. Ad esempio, è possibile specificare **Maggiore di** **80%**.
6. Quindi scegliere hello azione che si desidera tootake. Esistono diversi tipi di azioni:
   
   * Aumentare o diminuire di, si aggiungerà o rimuoverà hello **valore** numero di istanze è definire
   * Aumentare o diminuire percentuale - conteggio delle istanze hello verrà modificato da una percentuale. È possibile ad esempio, inserire 25 in hello **valore** campo, e se si dispone attualmente di 8 istanze, verrebbe aggiunta 2.
   * Aumentare o diminuire troppo, questo verrà impostato hello istanza conteggio toohello **valore** si definisce.
7. Infine, è possibile scegliere di raffreddamento - il tempo questa regola di attesa dopo hello precedente scala azione tooscale nuovamente.
8. Dopo avere configurato la regola, fare clic su **OK**.
9. Dopo aver configurato le regole di hello che si desidera essere certi toohit hello **salvare** comando.

### <a name="scaling-with-multiple-steps"></a>Ridimensionamento in più passaggi
esempi di Hello precedenti sono piuttosto semplici. Tuttavia, se si desidera toobe più aggressiva per scalare (verticale), è possibile anche aggiungere scala di più regole per hello stesso metrica. Ad esempio, è possibile definire due regole di scalabilità per la percentuale CPU:

1. Aumentare di 1 istanza se la percentuale CPU supera il 60%
2. Aumentare di 3 istanze se la percentuale CPU supera l'85%

![Regole multiple di scalabilità](./media/insights-how-to-scale/Insights_MultipleScaleRules.png)

Con questa regola aggiuntiva, se il carico supera l'85% prima che si verifichi un ridimensionamento, si otterranno non una ma due istanze aggiuntive.

## <a name="scale-based-on-a-schedule"></a>Scalare in base a una pianificazione
Per impostazione predefinita, una regola di scalabilità, una volta creata, viene applicata sempre. È possibile vedere che, quando si fa clic sull'intestazione di profilo hello:

![Profilo](./media/insights-how-to-scale/Insights_Profile.png)

Tuttavia, è consigliabile toohave più aggressiva proporzione durante hello giorno o settimana hello, rispetto a quella nel fine settimana hello. Si può persino arrestare completamente il servizio nelle ore non lavorative.

1. toodo, nel profilo hello si dispone, selezionare **ricorrenza** anziché **sempre,** e scegliere hello volte che si desidera tooapply profilo hello.
2. Ad esempio, un profilo che si applica durante la settimana hello, hello di toohave **giorni** elenco a discesa deselezionare **sabato** e **domenica**.
3. un profilo che si applica durante hello diurno, impostare di hello toohave **ora di inizio** toohello l'ora del giorno che si desidera toostart in.
   
    ![Ricorrenza predefinita](./media/insights-how-to-scale/Insights_ProfileRecurrence.png)
4. Fare clic su **OK**.
5. Successivamente, sarà necessario profilo hello tooadd che si desidera tooapply in altri momenti. Fare clic su hello **Aggiungi profilo** riga.
    ![Non al lavoro](./media/insights-how-to-scale/Insights_ProfileOffWork.png)
6. Assegnare un nome al secondo nuovo profilo, ad esempio **Non al lavoro**.
7. Selezionare quindi **ricorrenza** nuovamente, scegliere l'intervallo di conteggio istanza hello desiderato durante questo periodo.
8. Come con hello profilo predefinito, scegliere hello **giorni** si desidera tooapply questo profilo a e hello **ora di inizio** durante il giorno hello.
   
   > [!NOTE]
   > Scalabilità automatica utilizzerà regole relative all'ora legale hello per qualunque **fuso orario** selezionate. Tuttavia, durante l'ora legale offset UTC di hello mostrerà hello base del fuso orario, non offset di hello legale risparmi UTC.
   > 
   > 
9. Fare clic su **OK**.
10. A questo punto, sarà necessario tooadd qualsiasi regole che si desidera tooapply durante il secondo profilo. Fare clic su **Aggiungi regola**, e quindi è possibile costruire hello stessa regola durante profilo predefinito hello.
    
    ![Aggiungere regola toooff lavoro](./media/insights-how-to-scale/Insights_RuleOffWork.png)
11. Essere toocreate che sia una regola per la scalabilità orizzontale e scalabilità in, If o else durante hello profilo hello numero di istanze verrà solo aumento delle dimensioni (o ridurre).
12. Infine, fare clic su **Salva**.

## <a name="next-steps"></a>Passaggi successivi
* [Monitorare le metriche di servizio](insights-how-to-customize-monitoring.md) toomake che il servizio sia disponibile e reattiva.
* [Attivazione del monitoraggio e diagnostica](insights-how-to-use-diagnostics.md) toocollect dettagliate ad alta frequenza metriche sul servizio.
* [Ricevere notifiche di avviso](insights-receive-alert-notifications.md) ogni volta che si verificano eventi operativi o le metriche superano una soglia.
* [Monitorare le prestazioni dell'applicazione](../application-insights/app-insights-azure-web-apps.md) se si desidera toounderstand esattamente come il codice viene eseguito nel cloud hello.
* [Visualizzare eventi e log attività](insights-debugging-with-events.md) toolearn tutto ciò che si è verificato nel servizio.
* [Monitorare la disponibilità e i tempi di risposta di qualsiasi pagina Web](../application-insights/app-insights-monitor-web-app-availability.md) con Application Insights per definire se la pagina è inattiva.

