---
title: aaaAutoscaling e v1 ambiente del servizio App
description: Ridimensionamento automatico e ambiente del servizio app
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: c23af2d8-d370-4b1f-9b3e-8782321ddccb
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 1a03cf494309e80596b64471d1a067b2f64a9fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="autoscaling-and-app-service-environment-v1"></a>Ridimensionamento automatico e ambiente del servizio app (versione 1)

> [!NOTE]
> Questo articolo è sull'ambiente del servizio App v1 hello.  È una versione più recente di hello ambiente del servizio App che è più facile toouse e viene eseguito sull'infrastruttura più potente. informazioni sulla nuova versione di hello iniziare con hello toolearn [toohello introduzione ambiente del servizio App](../app-service/app-service-environment/intro.md).
> 

Gli ambienti del servizio app di Azure supportano il *ridimensionamento automatico*. È possibile ridimensionare automaticamente singoli pool di lavoro in base alle metriche o alla pianificazione.

![Opzioni di ridimensionamento automatico per un pool di lavoro.][intro]

La scalabilità automatica consente di ottimizzare l'utilizzo delle risorse mediante automaticamente l'espansione e riduzione di un toofit di ambiente del servizio App profilo budget e di carico.

## <a name="configure-worker-pool-autoscale"></a>Configurare il ridimensionamento automatico del pool di lavoro
È possibile accedere a funzionalità di scalabilità automatica hello da hello **impostazioni** tab di pool di lavoro hello.

![Scheda Impostazioni del pool di lavoro hello.][settings-scale]

Da qui, hello interfaccia deve essere piuttosto familiare perché è hello pianificare la stessa esperienza che viene visualizzato quando si scala di un servizio App. 

![Impostazioni di ridimensionamento manuale.][scale-manual]

È anche possibile configurare un profilo di ridimensionamento automatico.

![Impostazioni di ridimensionamento automatico.][scale-profile]

Profili di scalabilità automatica sono limiti di tooset utili sulla scala. Ciò consente di ottenere prestazioni coerenti impostando un valore del piano con un limite minimo (1) e un tetto di spesa prevedibile impostando un limite massimo (2).

![Impostazioni di ridimensionamento nel profilo.][scale-profile2]

Dopo aver definito un profilo, è possibile aggiungere tooscale regole di scalabilità automatica verso l'alto o verso il basso il numero di hello di istanze nel pool di lavoro hello all'interno dei limiti di hello definiti dal profilo hello. Le regole di ridimensionamento automatico sono basate su metriche.

![Regola di ridimensionamento.][scale-rule]

 Qualsiasi metrica front-end o un pool di lavoro può essere toodefine utilizzate regole di scalabilità automatica. Queste metriche sono hello stesse metriche è possibile monitorare in diagrammi di pannello risorse hello o impostare gli avvisi per.

## <a name="autoscale-example"></a>Esempio di ridimensionamento automatico
Per illustrare il ridimensionamento automatico di un ambiente del servizio app, si userà uno scenario con procedure dettagliate.

Questo articolo illustra tutte le considerazioni necessarie hello quando si configura scalabilità automatica. articolo Hello illustra hello interazioni che entrano riprodurre quando si analizzano la scalabilità automatica gli ambienti del servizio App che sono ospitati nell'ambiente del servizio App.

### <a name="scenario-introduction"></a>Introduzione dello scenario
Frank è un sysadmin per un'azienda che ha eseguito la migrazione di una parte dei carichi di lavoro hello che egli gestisce tooan ambiente del servizio App.

Hello servizio App di ambiente è configurato scala toomanual come segue:

* **Front-end:** 3
* **Pool di lavoro 1**: 10
* **Pool di lavoro 2**: 5
* **Pool di lavoro 3**: 5

Il pool di lavoro 1 viene usato per i carichi di lavoro di produzione, mentre il pool di lavoro 2 e il pool di lavoro 3 sono usati per il controllo di qualità e i carichi di lavoro di sviluppo.

Hello App piani di servizio per il controllo della qualità e sviluppo sono configurati toomanual scala. produzione Hello piano di servizio App è impostato toodeal tooautoscale con le variazioni del carico e il traffico.

Frank è dimestichezza con l'applicazione hello. Questi conosce ore di punta hello per il carico siano tra 9:00:00 e le 18.00 poiché si tratta di un'applicazione di line-of-business (LOB) che i dipendenti usano mentre si trovano in office hello. L'utilizzo si riduce al termine della giornata lavorativa degli utenti. Di fuori ore di punta, è ancora presente un carico in quanto gli utenti possono accedere in remoto hello app usando i dispositivi mobili o home PC. produzione di Hello piano di servizio App è già configurato tooautoscale in base all'utilizzo della CPU con hello seguenti regole:

![Impostazioni specifiche per l'app LOB.][asp-scale]

| **Profilo di ridimensionamento automatico - Giorni feriali - Piano di servizio app** | **Profilo di ridimensionamento automatico - Fine settimana - Piano di servizio app** |
| --- | --- |
| **Nome:** profilo Giorno feriale |**Nome:** profilo Fine settimana |
| **Ridimensiona in base a:** regole per la pianificazione e le prestazioni |**Ridimensiona in base a:** regole per la pianificazione e le prestazioni |
| **Profilo:** giorni della settimana |**Profilo:** fine settimana |
| **Tipo:** ricorrenza |**Tipo:** ricorrenza |
| **Intervallo di destinazione:** 5 istanze too20 |**Intervallo di destinazione:** 3 istanze too10 |
| **Giorni:** Lunedì, Martedì, Mercoledì, Giovedì, Venerdì |**Giorni:** Sabato, Domenica |
| **Ora di inizio:** 9:00 |**Ora di inizio:** 9:00 |
| **Fuso orario:** UTC -08 |**Fuso orario:** UTC -08 |
|  | |
| **Regola di ridimensionamento automatico (aumento)** |**Regola di ridimensionamento automatico (aumento)** |
| **Risorsa:** produzione (Ambiente del servizio app) |**Risorsa:** produzione (Ambiente del servizio app) |
| **Metrica:** % CPU |**Metrica:** % CPU |
| **Operazione:** maggiore del 60% |**Operazione:** maggiore del 80% |
| **Durata:** 5 minuti |**Durata:** 10 minuti |
| **Aggregazione temporale:** media |**Aggregazione temporale:** media |
| **Azione:** aumenta numero di 2 |**Azione:** aumenta numero di 1 |
| **Disattiva regole dopo (minuti):** 15 |**Disattiva regole dopo (minuti):** 20 |
|  | |
| **Regola di ridimensionamento automatico (riduzione)** |**Regola di ridimensionamento automatico (riduzione)** |
| **Risorsa:** produzione (Ambiente del servizio app) |**Risorsa:** produzione (Ambiente del servizio app) |
| **Metrica:** % CPU |**Metrica:** % CPU |
| **Operazione:** inferiore al 30% |**Operazione:** inferiore al 20% |
| **Durata:** 10 minuti |**Durata:** 15 minuti |
| **Aggregazione temporale:** media |**Aggregazione temporale:** media |
| **Azione:** riduci numero di 1 |**Azione:** riduci numero di 1 |
| **Disattiva regole dopo (minuti):** 20 |**Disattiva regole dopo (minuti):** 10 |

### <a name="app-service-plan-inflation-rate"></a>Tasso di inflazione del piano di servizio app
Piani di servizio App che sono tooautoscale configurato a tale scopo una velocità massima di ogni ora. Questa velocità può essere calcolata in base ai valori hello specificati nella regola di scalabilità automatica hello.

Comprensione e il calcolo hello *tasso di un piano di servizio App* è importante per la scalabilità automatica di servizio App ambiente perché il pool di lavoro tooa modifiche di scala non hanno effetto immediato.

frequenza di un piano di servizio App Hello viene calcolata come segue:

![Calcolo del tasso di inflazione del piano di servizio app.][ASP-Inflation]

Basato su hello Autoscale-regola di scalabilità verticale per il profilo del giorno feriale hello di produzione hello piano di servizio App:

![Tasso di inflazione del piano di servizio app per i giorni feriali basato su Ridimensionamento automatico - Regola di aumento.][Equation1]

Nel caso di hello di scalabilità automatica: regola di scalabilità verticale per il profilo del fine settimana hello di produzione hello piano di servizio App, hello formula hello viene risolto in:

![Tasso di inflazione del piano di servizio app per i fine settimana basato su Ridimensionamento automatico - Regola di aumento.][Equation2]

Questo valore può anche essere calcolato per le operazioni di riduzione.

In base a hello Autoscale-regola di scalabilità verso il basso per il profilo del giorno feriale hello di produzione hello piano di servizio App, ciò si presenterebbe come segue:

![Tasso di inflazione del piano di servizio app per i giorni feriali basato su Ridimensionamento automatico - Regola di riduzione.][Equation3]

Nel caso di hello di scalabilità automatica: regola scalabilità verso il basso per il profilo del fine settimana hello di produzione hello piano di servizio App, hello formula hello viene risolto in:  

![Tasso di inflazione del piano di servizio app per i fine settimana basato su Ridimensionamento automatico - Regola di riduzione.][Equation4]

produzione Hello piano di servizio App può raggiungere una velocità massima di otto istanze all'ora durante la settimana hello e quattro le istanze all'ora durante il weekend hello. È possibile rilasciare le istanze di una velocità massima di quattro istanze/ora settimana hello e sei istanze/ora durante il fine settimana.

Se più piani di servizio App sono ospitati in un pool di lavoro, è necessario hello toocalculate *frequenza un totale* come somma hello hello un tasso di per hello tutti i piani di servizio App che vengono hosting del pool di lavoro.

![Calcolo del tasso di inflazione totale per più piani di servizio app ospitati in un pool di lavoro.][ASP-Total-Inflation]

### <a name="use-hello-app-service-plan-inflation-rate-toodefine-worker-pool-autoscale-rules"></a>Hello utilizzare servizio App di pianificare le regole di scalabilità automatica di un tasso toodefine lavoro pool
Pool di lavoro che ospitano i piani di servizio App che sono configurati tooautoscale necessario allocare un buffer di capacità. buffer Hello consente toogrow di operazioni di scalabilità automatica hello e ridurre il piano di servizio App in base alle esigenze. minima del buffer Hello sarebbe hello calcolato totale App servizio prevede un tasso.

Le operazioni di ridimensionamento di servizio App ambiente richiedono alcuni tooapply ora, qualsiasi modifica dovrebbe tenere in considerazione ulteriori modifiche di richiesta che poteva verificarsi durante un'operazione di scala è in corso. tooaccommodate questa latenza, si consiglia di utilizzare hello calcolato totale App servizio prevede un tasso come numero minimo di hello di istanze che vengono aggiunti per ogni operazione di scalabilità automatica.

Con queste informazioni, Frank possono definire hello seguente profilo di scalabilità automatica e le regole:

![Regole del profilo di ridimensionamento automatico per l'esempio LOB.][Worker-Pool-Scale]

| **Profilo di ridimensionamento automatico - Giorni feriali** | **Profilo di ridimensionamento automatico - Fine settimana** |
| --- | --- |
| **Nome:** profilo Giorno feriale |**Nome:** profilo Fine settimana |
| **Ridimensiona in base a:** regole per la pianificazione e le prestazioni |**Ridimensiona in base a:** regole per la pianificazione e le prestazioni |
| **Profilo:** giorni della settimana |**Profilo:** fine settimana |
| **Tipo:** ricorrenza |**Tipo:** ricorrenza |
| **Intervallo di destinazione:** istanze too25 13 |**Intervallo di destinazione:** 6 istanze too15 |
| **Giorni:** Lunedì, Martedì, Mercoledì, Giovedì, Venerdì |**Giorni:** Sabato, Domenica |
| **Ora di inizio:** 7:00 |**Ora di inizio:** 9:00 |
| **Fuso orario:** UTC -08 |**Fuso orario:** UTC -08 |
|  | |
| **Regola di ridimensionamento automatico (aumento)** |**Regola di ridimensionamento automatico (aumento)** |
| **Risorsa:** Pool di lavoro 1 |**Risorsa:** Pool di lavoro 1 |
| **Metrica:** Pool di lavoro disponibili |**Metrica:** Pool di lavoro disponibili |
| **Operazione:** minore di 8 |**Operazione:** minore di 3 |
| **Durata:** 20 minuti |**Durata:** 30 minuti |
| **Aggregazione temporale:** media |**Aggregazione temporale:** media |
| **Azione:** aumenta numero di 8 |**Azione:** aumenta numero di 3 |
| **Disattiva regole dopo (minuti):** 180 |**Disattiva regole dopo (minuti):** 180 |
|  | |
| **Regola di ridimensionamento automatico (riduzione)** |**Regola di ridimensionamento automatico (riduzione)** |
| **Risorsa:** Pool di lavoro 1 |**Risorsa:** Pool di lavoro 1 |
| **Metrica:** Pool di lavoro disponibili |**Metrica:** Pool di lavoro disponibili |
| **Operazione:** maggiore di 8 |**Operazione:** maggiore di 3 |
| **Durata:** 20 minuti |**Durata:** 15 minuti |
| **Aggregazione temporale:** media |**Aggregazione temporale:** media |
| **Azione:** riduci numero di 2 |**Azione:** riduci numero di 3 |
| **Disattiva regole dopo (minuti):** 120 |**Disattiva regole dopo (minuti):** 120 |

intervallo di destinazione definito nel profilo hello Hello viene calcolato da istanze di hello minimo definite nel profilo per il piano di servizio App hello + buffer.

intervallo massimo Hello sarebbe somma hello di tutti gli intervalli massimo hello per tutti i piani di servizio App ospitati nel pool di lavoro hello.

conteggio di aumento per l'aumento di hello regole Hello deve essere set tooat almeno 1 X la frequenza di un piano di servizio App per la scala backup.

Conteggio di riduzione può essere adattata toosomething compreso tra 1/2 X o X 1 hello velocità di un piano di servizio App per la scalabilità verso il basso.

### <a name="autoscale-for-front-end-pool"></a>Ridimensionamento automatico per il pool front-end
Le regole per il ridimensionamento automatico front-end sono più semplici rispetto ai pool di lavoro. È prima di tutto necessario  
Assicurarsi che la durata della misurazione hello e timer di raffreddamento hello considera che le operazioni di ridimensionamento in un piano di servizio App non sono istantanee.

Per questo scenario, Frank SA tale tasso di errore hello aumenta dopo front-end di raggiungere l'80% della CPU e imposta la scalabilità automatica hello istanze tooincrease regola nel modo seguente:

![Impostazioni di ridimensionamento automatico per il pool front-end.][Front-End-Scale]

| **Profilo di ridimensionamento automatico - Front-end** |
| --- |
| **Nome:** Ridimensionamento automatico - Front-end |
| **Ridimensiona in base a:** regole per la pianificazione e le prestazioni |
| **Profilo:** ogni giorno |
| **Tipo:** ricorrenza |
| **Intervallo di destinazione:** 3 istanze too10 |
| **Giorni:** ogni giorno |
| **Ora di inizio:** 9:00 |
| **Fuso orario:** UTC -08 |
|  |
| **Regola di ridimensionamento automatico (aumento)** |
| **Risorsa:** pool front-end |
| **Metrica:** % CPU |
| **Operazione:** maggiore del 60% |
| **Durata:** 20 minuti |
| **Aggregazione temporale:** media |
| **Azione:** aumenta numero di 3 |
| **Disattiva regole dopo (minuti):** 120 |
|  |
| **Regola di ridimensionamento automatico (riduzione)** |
| **Risorsa:** Pool di lavoro 1 |
| **Metrica:** % CPU |
| **Operazione:** inferiore al 30% |
| **Durata:** 20 minuti |
| **Aggregazione temporale:** media |
| **Azione:** riduci numero di 3 |
| **Disattiva regole dopo (minuti):** 120 |

<!-- IMAGES -->
[intro]: ./media/app-service-environment-auto-scale/introduction.png
[settings-scale]: ./media/app-service-environment-auto-scale/settings-scale.png
[scale-manual]: ./media/app-service-environment-auto-scale/scale-manual.png
[scale-profile]: ./media/app-service-environment-auto-scale/scale-profile.png
[scale-profile2]: ./media/app-service-environment-auto-scale/scale-profile-2.png
[scale-rule]: ./media/app-service-environment-auto-scale/scale-rule.png
[asp-scale]: ./media/app-service-environment-auto-scale/asp-scale.png
[ASP-Inflation]: ./media/app-service-environment-auto-scale/asp-inflation-rate.png
[Equation1]: ./media/app-service-environment-auto-scale/equation1.png
[Equation2]: ./media/app-service-environment-auto-scale/equation2.png
[Equation3]: ./media/app-service-environment-auto-scale/equation3.png
[Equation4]: ./media/app-service-environment-auto-scale/equation4.png
[ASP-Total-Inflation]: ./media/app-service-environment-auto-scale/asp-total-inflation-rate.png
[Worker-Pool-Scale]: ./media/app-service-environment-auto-scale/wp-scale.png
[Front-End-Scale]: ./media/app-service-environment-auto-scale/fe-scale.png
