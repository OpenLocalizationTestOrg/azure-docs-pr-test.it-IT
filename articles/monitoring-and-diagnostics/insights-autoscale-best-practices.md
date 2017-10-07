---
title: "aaaBest procedure consigliate per la scalabilità automatica | Documenti Microsoft"
description: "Modelli di scalabilità automatica in Azure per App Web, set di scalabilità di macchine virtuali e Servizi cloud"
author: anirudhcavale
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 9fa2b94b-dfa5-4106-96ff-74fd1fba4657
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: ancav
ms.openlocfilehash: eb731c15e440af93a2675210583878814d0d8818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-autoscale"></a>Procedure consigliate per la scalabilità automatica
In questo articolo illustra procedure consigliate tooautoscale in Azure. Azure scalabilità automatica di monitoraggio si applica solo troppo[set di scalabilità di macchine virtuali](https://azure.microsoft.com/services/virtual-machine-scale-sets/), [servizi Cloud](https://azure.microsoft.com/services/cloud-services/), e [servizio App: app Web](https://azure.microsoft.com/services/app-service/web/). Altri servizi Azure usano metodi di ridimensionamento diversi.

## <a name="autoscale-concepts"></a>Concetti di scalabilità automatica
* Una risorsa può avere *una* sola impostazione di scalabilità automatica.
* Un'impostazione di scalabilità automatica può avere uno o più profili e ogni profilo può avere una o più regole di scalabilità automatica.
* Un'impostazione di scalabilità automatica ridimensiona le istanze in senso orizzontale, ovvero *out* aumentando le istanze di hello e *in* riducendo il numero di hello di istanze.
  Un'impostazione di scalabilità automatica ha un valore massimo, uno minimo e uno predefinito di istanze.
* Un processo di scalabilità automatica legge sempre hello associata tooscale metrica controllando, se è superato hello soglia configurata per la scalabilità orizzontale o in scala. Per un elenco delle metriche in base alle quali può essere applicata la scalabilità automatica, vedere [Metriche comuni per la scalabilità automatica di Monitoraggio di Azure](insights-autoscale-common-metrics.md).
* Tutte le soglie vengono calcolate a livello di istanza. Ad esempio, "scala può essere estratto da 1 istanza quando medio della CPU > 80% quando il numero di istanze è 2", significa che la scalabilità orizzontale hello utilizzo medio della CPU tra tutte le istanze è superiore all'80%.
* Le notifiche di errore vengono sempre ricevute tramite posta elettronica. In particolare, hello proprietario, collaboratore e lettori di risorsa di destinazione hello riceveranno posta elettronica. Si riceverà sempre un messaggio di posta elettronica di *ripristino* anche quando la scalabilità automatica viene ripristinata dopo un errore e inizia a funzionare normalmente.
* È possibile acconsentire esplicitamente tooreceive una notifica di azione scala ha esito positivo tramite posta elettronica e ai webhook.

## <a name="autoscale-best-practices"></a>Procedure consigliate per la scalabilità automatica
Utilizzare hello seguono le procedure consigliate durante l'utilizzo di scalabilità automatica.

### <a name="ensure-hello-maximum-and-minimum-values-are-different-and-have-an-adequate-margin-between-them"></a>Verificare i valori minimo e massimo hello sono diversi e dispongono di un margine sufficiente tra di essi
Se si dispone di un'impostazione con minimo = 2, massimo = 2 e il numero di istanze correnti di hello è 2, non può verificarsi Nessuna azione di scalabilità. Mantenere un margine sufficiente tra numero totale di istanze minimo e massimo hello, che sono inclusivi. La scalabilità automatica viene sempre applicata entro questi limiti.

### <a name="manual-scaling-is-reset-by-autoscale-min-and-max"></a>La scalabilità manuale viene reimpostata dai valori minimo e massimo della scalabilità automatica
Se si manualmente Aggiorna hello istanza tooa valore del conteggio sopra o sotto massimo hello hello automaticamente il motore di scalabilità automatica scala back toohello minimo (se di sotto) o hello massimo (se in precedenza). Ad esempio, impostare l'intervallo hello compreso tra 3 e 6. Se si dispone di un'istanza in esecuzione, il motore di scalabilità automatica hello scala too3 istanze la successiva esecuzione. Allo stesso modo, sarebbe scala aggiuntivo 8 istanze di eseguire il backup too6 la successiva esecuzione.  Ridimensionamento manuale è molto temporaneo a meno che non si reimposta anche le regole di scalabilità automatica hello.

### <a name="always-use-a-scale-out-and-scale-in-rule-combination-that-performs-an-increase-and-decrease"></a>Usare sempre una combinazione di regole di aumento e di riduzione del numero di istanze
Se si utilizza solo una parte di una combinazione di hello, scalabilità automatica scala aggiuntivo singolo, o, fino a quando hello massimo o minimo, è stato raggiunto.

### <a name="do-not-switch-between-hello-azure-portal-and-hello-azure-classic-portal-when-managing-autoscale"></a>Non passare hello portale di Azure e hello portale di Azure classico per la gestione di scalabilità automatica
Per servizi Cloud e servizi di App (app Web), utilizzare hello del portale di Azure (portal.azure.com) toocreate e gestire le impostazioni di scalabilità automatica. Per il set di scalabilità di macchine virtuali utilizzare toocreate PowerShell, CLI o l'API REST e gestire le impostazioni di scalabilità automatica. Non passare hello portale di Azure classico (manage.windowsazure.com) hello del portale di Azure (portal.azure.com) quando la gestione delle configurazioni di scalabilità automatica. portale di Azure classico Hello e il relativo back-end sottostante presenta limitazioni. Spostare la scalabilità automatica toomanage portale Azure toohello utilizzando un'interfaccia utente grafica. opzioni di Hello sono toouse hello autoscale PowerShell, CLI o l'API REST (tramite Esplora risorse di Azure).

### <a name="choose-hello-appropriate-statistic-for-your-diagnostics-metric"></a>Scegliere statistica appropriato di hello per la metrica di diagnostica
Per la metrica di diagnostica, è possibile scegliere tra *Media*, *minimo*, *massimo* e *totale* come una metrica tooscale da. statistica più comune di Hello è *Media*.

### <a name="choose-hello-thresholds-carefully-for-all-metric-types"></a>Scegliere le soglie di hello attentamente per tutti i tipi di metrica
È consigliabile scegliere con attenzione soglie diverse per aumentare e ridurre il numero di istanze a seconda delle situazioni concrete.

Abbiamo *non è consigliabile* hello di impostazioni di scalabilità automatica, come negli esempi di hello seguenti con i valori di soglia identiche o molto simili per disconnettersi e condizioni:

* Aumentare le istanze di 1 quando il conteggio dei thread è <= 600
* Ridurre le istanze di 1 quando il conteggio dei thread è >= 600

Esaminiamo un esempio di ciò che può causare il comportamento tooa che potrebbe sembrare poco chiaro. Prendere in considerazione hello seguente sequenza.

1. Si supponga che esistono 2 istanze toobegin con e quindi aumentare too625 del numero medio di hello di thread per ogni istanza.
2. Il numero di istanze viene aumentato automaticamente aggiungendo una terza istanza.
3. Successivamente, si supponga che il conteggio thread medio hello tra l'istanza rientra too575.
4. Prima di riduzione, scalabilità automatica tenta tooestimate lo stato finale che hello sarà se ridimensionata. Ad esempio, 575 x 3 (conteggio corrente delle istanze) = 1.725 / 2 (numero finale di istanze dopo la riduzione delle prestazioni) = 862,5 thread. Ciò significa scalabilità automatica sarebbero tooimmediately scalabilità orizzontale nuovamente anche dopo che ridimensionata, hello thread medio conteggio rimane hello stesso o persino rientra solo una piccola quantità. Tuttavia, se ridimensionato verso l'alto, sarebbe necessario ripetere l'intero processo hello, iniziali tooan di ciclo infinito.
5. tooavoid questa situazione (indicata come "Ali"), ridimensionamento automatico non scalare verso il basso affatto. Invece, vengono ignorati e Rivaluta hello condizione nuovamente il processo di hello successiva ora hello del servizio viene eseguito. Questa operazione potrebbe confondere molte persone scalabilità automatica non saranno toowork numero medio di thread di hello stato 575.

Stima durante una scala è previsto tooavoid "instabile" situazioni in cui le azioni di scalabilità e di scalabilità orizzontale continuamente andare avanti e indietro. Quando si sceglie di hello stessa soglia di scalabilità orizzontale in, tenere presente questo comportamento.

Si consiglia di scegliere un margine sufficiente tra hello scalabilità orizzontale e le soglie. Ad esempio, prendere in considerazione hello seguente combinazione di regola migliore.

* Aumentare le istanze di 1 quando la percentuale di CPU è >= 80
* Ridurre le istanze di 1 quando la percentuale di CPU è <= 60

In questo caso  

1. Si supponga 2 istanze toostart con.
2. Se too80, Percentuale CPU Media hello tra più istanze di scalabilità automatica consente una scalabilità orizzontale aggiungendo una terza istanza.
3. Si supponga che nel tempo CPU di hello % rientra too60.
4. Regola di scalabilità della scalabilità automatica stima stato finale hello se fosse tooscale-in. Ad esempio, 60 x 3 (conteggio corrente delle istanze) = 180 / 2 (numero finale di istanze dopo la riduzione delle prestazioni) = 90. Pertanto, scalabilità automatica non scala-in perché ha nuovamente immediatamente tooscale-out. Al contrario, evita di ridurre le prestazioni.
5. scalabilità automatica di tempo successiva Hello controlla hello della CPU continua toofall too50. Stima nuovamente - istanza 50 x 3 = 150 / 2 istanze = 75, che è inferiore a soglia di scalabilità orizzontale hello pari a 80, pertanto si adatta in istanze di too2 correttamente.

### <a name="considerations-for-scaling-threshold-values-for-special-metrics"></a>Considerazioni sul ridimensionamento dei valori di soglia per le metriche speciali
 Per la metrica speciale, ad esempio metrica lunghezza coda del Bus di servizio o di archiviazione, soglia hello è numero medio di hello di messaggi disponibili per il numero corrente di istanze. Scegliere con attenzione hello scegliere hello valore di soglia per questa metrica.

Di seguito viene illustrato con tooensure un esempio è comprendere meglio il comportamento di hello.

* Aumentare le istanze di 1 quando il conteggio dei messaggi della coda di archiviazione è >= 50
* Ridurre le istanze di 1 quando il conteggio dei messaggi della coda di archiviazione è <= 10

Prendere in considerazione hello seguente sequenza:

1. Esistono 2 istanze di coda di archiviazione.
2. Ancora messaggi e quando si verifica la coda di archiviazione hello, totale hello legge 50. Si potrebbe pensare che la scalabilità automatica debba avviare un'azione di aumento del numero di istanze. Si noti tuttavia che si tratta comunque di 50/2 = 25 messaggi per ogni istanza. L'aumento del numero di istanze non viene quindi eseguito. Per hello prima toohappen di scalabilità orizzontale, il numero totale di messaggi hello nella coda di archiviazione hello deve essere 100.
3. Si supponga ora che numero totale di messaggi hello raggiunge i 100.
4. Un'istanza di coda di archiviazione 3 viene aggiunto a causa di tooa azione di scalabilità orizzontale.  Hello successiva azione di scalabilità orizzontale non avverrà finché hello totale conteggio dei messaggi nella coda di hello raggiunge 150 perché 150/3 = 50.
5. Numero di hello di messaggi nella coda di hello Ottiene ora più piccolo. Con 3 istanze, hello prima scala azione si verifica quando hello totale messaggi in tutte le code di sommare too30 perché 30/3 = 10 messaggi per ogni istanza, ovvero una soglia di scala hello.

### <a name="considerations-for-scaling-when-multiple-profiles-are-configured-in-an-autoscale-setting"></a>Considerazioni sul ridimensionamento quando vengono configurati più profili in un'impostazione di scalabilità automatica
In un'impostazione di scalabilità automatica è possibile scegliere un profilo predefinito, che viene sempre applicato indipendentemente da qualsiasi pianificazione o orario, oppure è possibile scegliere un profilo ricorrente o un profilo per un periodo fisso con un intervallo di data e ora.

Quando li elabora di servizio di scalabilità automatica, verificare sempre in hello seguente ordine:

1. Profilo con data fissa
2. Profilo ricorrente
3. Profilo predefinito ("sempre")

Se viene soddisfatta una condizione di profilo, scalabilità automatica non verifica la condizione profilo successiva hello sotto di essa. La scalabilità automatica elabora solo un profilo alla volta. Questo significa che se si desidera tooalso includono una condizione di elaborazione da un profilo di livello inferiore, è necessario includere anche le regole nel profilo corrente hello.

Per spiegarlo, verrà usato un esempio:

immagine di Hello seguente mostra un'impostazione di scalabilità automatica con un profilo predefinito di istanze minime = 2 e massime di istanze = 10. In questo esempio, le regole sono configurato tooscale-out quando il numero di messaggi hello nella coda di hello è maggiore di 10 e scala-in quando il numero di messaggi hello nella coda di hello è inferiore a 3. Risorsa hello ora possibile applicare la scalabilità tra 2 e 10 istanze.

È anche stato impostato un profilo ricorrente per il lunedì. È stato impostato per un numero minimo di istanze = 2 e un numero massimo di istanze = 12. Ciò significa che il lunedì hello scalabilità automatica di tempo prima controlla questa condizione, se il numero di istanze di hello è 2, che viene ampliato toohello nuovo minimo di 3. Finché la scalabilità automatica continua toofind questa condizione profilo corrispondente (lunedì), elabora solo hello CPU regole basate su scale-out/in configurato per questo profilo. In questo momento, non controlla per lunghezza coda hello. Tuttavia, se si desidera toobe condizione lunghezza coda di hello selezionata, è necessario includere le regole da profilo predefinito hello anche nel profilo di lunedì.

Analogamente, quando scalabilità automatica è attiva profilo predefinito toohello indietro, verifica innanzitutto se vengono soddisfatte le condizioni di hello minimo e massimo. Se il numero di hello delle istanze in esecuzione hello è 12, ridimensiona nel too10, hello massimo consentito per profilo predefinito hello.

![Impostazioni di scalabilità automatica](./media/insights-autoscale-best-practices/insights-autoscale-best-practices-2.png)

### <a name="considerations-for-scaling-when-multiple-rules-are-configured-in-a-profile"></a>Considerazioni sul ridimensionamento quando vengono configurate più regole in un profilo
Vi sono casi in cui è possibile tooset più regole in un profilo. Quando sono impostate più regole, Hello seguente set di regole di scalabilità automatica è usato dai servizi.

In caso di *aumento del numero di istanze*, la scalabilità automatica viene eseguita se risulta soddisfatta una regola qualsiasi.
In *scala aggiuntivo*, scalabilità automatica richiede tutte le regole toobe soddisfatti.

tooillustrate, si supponga di disporre delle seguenti regole di scalabilità automatica 4 hello:

* Se la CPU è < 30%, ridurre il numero di istanze di 1
* Se la memoria è < 50%, ridurre il numero di istanze di 1
* Se la CPU è > 75%, aumentare il numero di istanze di 1
* Se la memoria è > 75%, aumentare il numero di istanze di 1

Viene quindi eseguito hello seguenti:

* Se la CPU è pari al 76% e la memoria è pari al 50%, il numero di istanze viene aumentato.
* Se la CPU è pari al 50% e la memoria è pari al 76%, il numero di istanze viene aumentato.

Hello d'altra parte, se la CPU è 25% e della memoria è la scalabilità automatica 51% **non** scala-in. Tooscale-in, della CPU deve essere % 29 e memoria 49%.

### <a name="always-select-a-safe-default-instance-count"></a>Selezionare sempre un conteggio di istanze predefinito sicuro
numero di istanza predefinito Hello è importante scalabilità automatica ridimensiona il conteggio toothat servizio quando la metrica non è disponibile. Selezionare quindi un conteggio di istanze predefinito sicuro per i carichi di lavoro.

### <a name="configure-autoscale-notifications"></a>Configurare le notifiche relative alla scalabilità automatica
Scalabilità automatica invia una notifica agli amministratori di hello e dai collaboratori della risorsa hello tramite posta elettronica se si verifica una delle seguenti condizioni hello:

* servizio di scalabilità automatica ha esito negativo tootake un'azione.
* Le metriche non sono disponibili per la scalabilità automatica servizio toomake una decisione di scala.
* Sono disponibile (ripristino) nuovamente toomake una decisione di scala.
  Inoltre toohello condizioni riportate sopra, è possibile configurare posta elettronica o webhook tooget notifiche ricevere una notifica per le azioni di scalabilità ha esito positivo.
  
È inoltre possibile utilizzare uno stato di integrità hello toomonitor avviso Log attività del motore di scalabilità automatica hello. Ecco alcuni esempi troppo[creare tutte le operazioni del motore di scalabilità automatica per la sottoscrizione di un avviso di Log attività toomonitor](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert) o troppo[creare un avviso di Log attività toomonitor tutti non riuscito di scala di scalabilità automatica in / operazioni di scala la sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).

## <a name="next-steps"></a>Passaggi successivi
- [Creare un avviso di Log attività toomonitor tutte le operazioni del motore di scalabilità automatica per la sottoscrizione.](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [Creare un avviso di Log attività toomonitor tutti non riuscito di scala di scalabilità automatica in / scalabilità operazioni per la sottoscrizione](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)
