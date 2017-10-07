---
title: "aaaHow tooBuild pianificazioni complesse e ricorrenza avanzate con utilità di pianificazione di Azure"
description: "Come tooBuild complesso pianifica e ricorrenza avanzate con utilità di pianificazione di Azure"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 5c124986-9f29-4cbc-ad5a-c667b37fbe5a
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: 02172791978b12be0ccb3078125d057b2efe8523
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toobuild-complex-schedules-and-advanced-recurrence-with-azure-scheduler"></a>Come tooBuild complesso pianifica e ricorrenza avanzate con utilità di pianificazione di Azure
## <a name="overview"></a>Panoramica
Fulcro hello di un'utilità di pianificazione di Azure è hello processo *pianificazione*. pianificazione di Hello determina quando e come hello dell'utilità di pianificazione esegue il processo di hello.

Pianificazione di Azure consente toospecify monouso e ricorrenti pianificazioni diverse per un processo. Le pianificazioni *monouso* vengono eseguite una volta sola all'ora specificata. Si tratta in effetti di pianificazioni *ricorrenti* che vengono eseguite solo una volta. Le pianificazioni ricorrenti vengono eseguite con una frequenza predeterminata.

Con questa flessibilità, l’Utilità di pianificazione di Azure consente di supportare un'ampia gamma di scenari aziendali:

* Pulizia periodica dei dati, ad esempio eliminare tutti i post su Twitter più vecchi di 3 mesi
* Archiviazione, ad esempio, ogni mese, il servizio toobackup della cronologia di fatturazione push
* Richieste di dati esterni – ad esempio, ogni 15 minuti, effettuare il prelievo dei nuovi bollettini meteorologici per sciatori dal servizio NOAA
* Immagine di elaborazione, ad esempio, ogni giorno feriale durante le fasce orarie, usare cloud computing toocompress immagini caricate giorno

In questo articolo, presenteremo dei processi di esempio che è possibile creare con l’Utilità di pianificazione di Azure. Si forniscono dati hello JSON che descrive ogni pianificazione. Se si utilizza hello [API REST dell'utilità di pianificazione](https://msdn.microsoft.com/library/mt629143.aspx), è possibile utilizzare questo stesso JSON per [creazione di un processo dell'utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629145.aspx).

## <a name="supported-scenarios"></a>Scenari Supportati
Hello che molti esempi in questo argomento illustrano breadth hello degli scenari che supporta la pianificazione di Azure. Su vasta scala, questi esempi viene illustrato come toocreate pianificazioni per molti modelli di comportamento, tra cui hello quelli seguenti:

* Esecuzione una sola volta in una determinata data e ora
* Esecuzione ricorrente per un numero esplicito di volte
* Esecuzione immediata e in seguito ricorrente
* Esecuzione ricorrente ogni *n* minuti, ore, giorni, settimane o mesi, a partire da un determinato momento
* Esecuzione ricorrente con frequenza settimanale o mensile, ma solo in giorni specifici, giorni specifici della settimana o giorni specifici del mese
* Esecuzione ricorrente più volte in un dato periodo – ad esempio, gli ultimi venerdì e lunedì di ogni mese, o alle 5:15 am e 5:15 pm di ogni giorno

## <a name="dates-and-datetimes"></a>Date e Date-Ore
Le date nei processi dell'utilità di pianificazione di Azure seguono hello [specifica ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) e includere solo hello Data.

I riferimenti di data e ora nei processi dell'utilità di pianificazione di Azure seguono hello [specifica ISO 8601](http://en.wikipedia.org/wiki/ISO_8601) e includere parti sia data e ora. Data e ora che non specifica un offset UTC presuppone toobe UTC.  

## <a name="how-to-use-json-and-rest-api-for-creating-schedules"></a>Procedura: Utilizzare JSON e API REST per la creazione di pianificazioni
una pianificazione semplice utilizzando toocreate hello [API REST dell'utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143), prima [registrare la sottoscrizione con un provider di risorse](https://msdn.microsoft.com/library/azure/dn790548.aspx) (nome del provider hello per utilità di pianificazione è  *Microsoft.Scheduler*), quindi [creare una raccolta di processi](https://msdn.microsoft.com/library/mt629159.aspx)e infine [creare un processo](https://msdn.microsoft.com/library/mt629145.aspx). Quando si crea un processo, è possibile specificare la pianificazione e ricorrenza usando JSON come hello uno tratte sotto:

    {
        "startTime": "2012-08-04T00:00Z", // optional
         …
        "recurrence":                     // optional
        {
            "frequency": "week",     // can be "year" "month" "day" "week" "hour" "minute"
            "interval": 1,                // optional, how often toofire (default too1)
            "schedule":                   // optional (advanced scheduling specifics)
            {
                "weekDays": ["monday", "wednesday", "friday"],
                "hours": [10, 22]                      
            },
            "count": 10,                  // optional (default toorecur infinitely)
            "endTime": "2012-11-04",      // optional (default toorecur infinitely)
        },
        …
    }

## <a name="overview-job-schema-basics"></a>Panoramica: Nozioni di base sugli schemi dei processi
Hello nella tabella seguente fornisce una panoramica generale di hello elementi principali correlati toorecurrence e la pianificazione di un processo:

| **Nome JSON** | **Descrizione** |
|:--- |:--- |
| ***startTime*** |*startTime* è in formato Data-Ora. Per le pianificazioni semplice, *startTime* viene prima occorrenza di hello e per le pianificazioni complesse, hello processo non inizierà a avvenga *startTime*. |
| ***recurrence*** |Hello *ricorrenza* oggetto specifica le regole di ricorrenza per i processi di hello e hello ricorrenza hello verrà eseguita con. oggetto ricorrenza Hello supporta gli elementi di hello *frequenza, intervallo, endTime, conteggio,* e *pianificazione*. Se *ricorrenza* è definito, *frequenza* è obbligatorio; gli altri elementi di hello *ricorrenza* sono facoltativi. |
| ***frequency*** |Hello *frequenza* stringa che rappresenta l'unità di hello frequenza alla quale hello processo si ripete. I valori supportati sono *"minute", "hour", "day", "week",* o *"month"*. |
| ***interval*** |Hello *intervallo* un numero intero positivo e indica l'intervallo di hello per hello *frequenza* che determina la frequenza con cui hello processo verrà eseguito. Ad esempio, se *intervallo* è 3 e *frequenza* è "settimana", il processo di hello ricorre ogni tre settimane. L'Utilità di pianificazione di Azure supporta un oggetto *interval* con valore massimo di 18 mesi per la frequenza mensile, 78 settimane per la frequenza settimanale o 548 giorni per la frequenza giornaliera. Per ora e minuto della frequenza, intervallo hello supportato è 1 < = *intervallo* < = 1000. |
| ***endTime*** |Hello *endTime* stringa specifica data e ora di hello oltre cui hello processo non deve essere eseguita. Non è valido toohave un *endTime* in hello precedente. Se non *endTime* o numero viene specificato, il processo di hello viene eseguito all'infinito. Entrambi *endTime* e *conteggio* non può essere incluso per hello stesso processo. |
| ***count*** |<p>Hello *conteggio* è un numero intero positivo (maggiore di zero) che specifica il numero di hello di volte in cui questo processo deve essere eseguito prima del completamento.</p><p>Hello *conteggio* rappresenta hello numero di volte in cui viene eseguito il processo di hello prima viene determinato come completata. Ad esempio, per un processo che viene eseguito ogni giorno con *conteggio* 5 e data di inizio del lunedì, hello processo viene completato al termine dell'esecuzione venerdì. Se start hello data hello precedente, prima esecuzione hello viene calcolato dal momento della creazione hello.</p><p>Se non *endTime* o *conteggio* viene specificata, il processo di hello viene eseguito all'infinito. Entrambi *endTime* e *conteggio* non può essere incluso per hello stesso processo.</p> |
| ***schedule*** |Un processo con una frequenza specificata modifica la sua ricorrenza in base a una pianificazione di ricorrenza. Un oggetto *schedule* contiene modifiche in base a minuti, ore, giorni della settimana, giorni del mese e numero della settimana. |

## <a name="overview-job-schema-defaults-limits-and-examples"></a>Panoramica: Impostazioni predefinite dello schema del processo, limiti ed esempi
Dopo questa panoramica, esaminiamo ciascuno di questi elementi in modo dettagliato.

| **Nome JSON** | **Tipo di valore** | **Obbligatorio?** | **Valore predefinito** | **Valori validi** | **Esempio** |
|:--- |:--- |:--- |:--- |:--- |:--- |
| ***startTime*** |String |No |None |Date-Ore ISO-8601 |<code>"startTime" : "2013-01-09T09:30:00-08:00"</code> |
| ***recurrence*** |Oggetto |No |None |Oggetto ricorrenza |<code>"recurrence" : { "frequency" : "monthly", "interval" : 1 }</code> |
| ***frequency*** |String |Sì |None |"minute", "hour", "day", "week", "month" |<code>"frequency" : "hour"</code> |
| ***interval*** |Number |No |1 |1 too1000. |<code>"interval":10</code> |
| ***endTime*** |String |No |Nessuno |Valore di data e ora che rappresenta un'ora nel futuro hello |<code>"endTime" : "2013-02-09T09:30:00-08:00"</code> |
| ***count*** |Number |No |None |>= 1 |<code>"count": 5</code> |
| ***schedule*** |Oggetto |No |None |Oggetto pianificazione |<code>"schedule" : { "minute" : [30], "hour" : [8,17] }</code> |

## <a name="deep-dive-starttime"></a>Approfondimenti: *startTime*
tabella che segue Hello acquisizioni come *startTime* controlla le modalità di esecuzione di un processo.

| **valore startTime** | **Nessuna ricorrenza** | **Ricorrenza. Nessuna pianificazione** | **Ricorrenza con pianificazione** |
|:--- |:--- |:--- |:--- |
| **Nessuna ora di inizio** |Eseguire una volta immediatamente |Eseguire una volta immediatamente. Lanciare le esecuzioni successive basandosi sul calcolo dall'ultima esecuzione |<p>Eseguire una volta immediatamente</p><p>Avviare le esecuzioni successive in base alla pianificazione di ricorrenza</p> |
| **Ora di inizio nel passato** |Eseguire una volta immediatamente |<p>Calcolare l'ora della prima esecuzione futura dopo l'ora di inizio e avviare l'esecuzione in corrispondenza di tale orario</p><p>Avviare le esecuzione successive in base al calcolo relativo all'ora dell'ultima esecuzione</p><p>Per altre informazioni, vedere l'esempio disponibile dopo la tabella</p> |<p>Avvio del processo *non prima rispetto a* hello specificato ora di inizio. prima occorrenza di Hello è basato su pianificazione hello calcolato dall'ora di inizio hello</p><p>Avviare le esecuzioni successive in base alla pianificazione di ricorrenza</p> |
| **Ora di inizio nel futuro o nel presente** |Eseguire una sola volta all'ora di inizio specificata |<p>Eseguire una sola volta all'ora di inizio specificata</p><p>Lanciare le esecuzioni successive basandosi sul calcolo dall'ultima esecuzione</p> |<p>Avvio del processo *non prima rispetto a* hello specificato ora di inizio. prima occorrenza di Hello è basato su pianificazione hello calcolato dall'ora di inizio hello</p><p>Avviare le esecuzioni successive in base alla pianificazione di ricorrenza</p> |

Di seguito viene illustrato un esempio di ciò che accade in *startTime* in versioni precedenti di hello con *ricorrenza* ma non *pianificazione*.  Si supponga che hello ora corrente è 2015-04-08 13:00, *startTime* è 2015-04-07 14:00, e *ricorrenza* ogni 2 giorni (definito con *frequenza*: giorno e *intervallo*: 2.) Si noti che hello *startTime* in hello precedente e si verifica prima dell'ora corrente hello

In queste condizioni, hello *prima esecuzione* sarà 2015-04-09 alle 14:00\. il motore di pianificazione Hello calcola le occorrenze di esecuzione dall'ora di inizio hello.  Tutte le istanze in hello precedente vengono eliminate. il motore di Hello utilizza istanza successiva hello che si verifica in hello future.  In questo caso, *startTime* è 2015-04-07 2:00 PM, pertanto hello istanza successiva è 2 giorni a partire da tale ora, ovvero 2015-04-09 2:00 PM.

Si noti che prima esecuzione hello sarebbe hello stesso anche se hello startTime 2015-04-05 14:00 o 14:00\ 2015-04-01. Dopo la prima esecuzione hello, nelle esecuzioni successive vengono calcolate utilizzando hello pianificati, in modo saranno 2015-04-11 2:00 PM, quindi 2015-04-13 2:00 pm, quindi 2015-04-15 ore 2:00, e così via.

Infine, quando un processo dispone di una pianificazione, se le ore e/o minuti non sono impostati nella pianificazione hello, essi ore toohello predefinito e/o minuti della prima esecuzione hello, rispettivamente.

## <a name="deep-dive-schedule"></a>Approfondimenti: *schedule*
In alcuni casi un *pianificazione* possibile *limite* hello numero di esecuzioni del processo.  Ad esempio, se un processo con una frequenza di "month" ha un *pianificazione* che viene eseguito solo giorno 31, hello processo viene eseguito in solo questi mesi che hanno un 31<sup>st</sup> giorno.

Hello d'altro canto, una *pianificazione* può anche *espandere* hello numero di esecuzioni del processo. Ad esempio, se un processo con una frequenza di "month" ha un *pianificazione* che viene eseguita in giorni del mese 1 e 2, hello processo viene eseguito su hello 1<sup>st</sup> e 2<sup>nd</sup> giorni del mese hello anziché una sola volta un mese.

Se vengono specificati più elementi di programmazione, hello di valutazione è più grande hello toosmallest-numero della settimana, giorno, mese, giorno della settimana, ore e minuti.

Hello nella tabella seguente vengono descritti *pianificazione* elementi in modo dettagliato.

| **Nome JSON** | **Descrizione** | **Valori validi** |
|:--- |:--- |:--- |
| **minutes** |Minuti di ora hello in cui hello processo verrà eseguito |<ul><li>Numero intero o</li><li>Matrice di numeri interi</li></ul> |
| **hours** |Ore del giorno hello in cui hello processo verrà eseguito |<ul><li>Numero intero o</li><li>Matrice di numeri interi</li></ul> |
| **weekDays** |Giorni di processo di hello settimana hello verranno eseguito. Può essere specificato solo con una frequenza settimanale. |<ul><li>I valori consentiti sono "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday" o "Sunday"</li><li>Matrice di uno dei hello di sopra di valori (dimensione matrice massima 7)</li></ul>*Non* viene applicata la distinzione tra maiuscole e minuscole |
| **monthlyOccurrences** |Determina quali giorni del processo di hello hello mese verranno eseguito. Può essere specificato solo con una frequenza mensile. |<ul><li>Matrice di oggetti monthlyOccurrence:</li></ul> <pre>{ "day": *day*,<br />  "occurrence": *occurrence*<br />}</pre><p> *giorno* è giorno hello del processo di hello settimana hello verrà eseguito, ad esempio, {domenica} è ogni domenica del mese hello. Obbligatorio.</p><p>Occorrenza *occorrenza* del giorno hello durante il mese di hello, ad esempio {domenica, -1} è hello ultima domenica del mese hello. Facoltativo.</p> |
| **monthDays** |Giorno del processo di hello hello mese verrà eseguito. Può essere specificato solo con una frequenza mensile. |<ul><li>Qualsiasi valore <= -1 e >= -31.</li><li>Qualsiasi valore >= 1 e <= 31.</li><li>Matrice dei valori precedenti</li></ul> |

## <a name="examples-recurrence-schedules"></a>Esempi: Pianificazioni di ricorrenza
di seguito Hello sono vari esempi di pianificazioni di ricorrenza: porre l'attenzione sul oggetto pianificazione hello e i relativi elementi secondari.

le pianificazioni sotto tutti Hello presuppongono che hello *intervallo* è impostato too1\. Inoltre, uno deve presupporre hello frequenza di invio in conformità toowhat è in hello *pianificazione* : ad esempio, uno non è possibile utilizzare "day" frequenza e dispone di una modifica "giorni mese" in pianificazione hello. Tali limitazioni sono state descritte in precedenza.

| **Esempio** | **Descrizione** |
|:--- |:--- |
| <code>{"hours":[5]}</code> |Eseguire alle 5 di mattina di ogni giorno. Utilità di pianificazione Azure corrisponda a ogni valore nella "orario" con ogni valore in "minutes", uno alla volta, eseguire un elenco di tutti i periodi di hello al quale hello processo è toobe toocreate. |
| <code>{"minutes":[15], "hours":[5]}</code> |Eseguire alle 5:15 di mattina di ogni giorno. |
| <code>{"minutes":[15], "hours":[5,17]}</code> |Eseguire alle 5:15 di mattina e alle 17:15 ogni giorno |
| <code>{"minutes":[15,45], "hours":[5,17]}</code> |Eseguire alle 5:15, 5:45, 17:15 e 17:45 ogni giorno |
| <code>{"minutes":[0,15,30,45]}</code> |Eseguire ogni 15 minuti |
| <code>{hours":[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23]}</code> |Eseguire ogni ora. Questo processo viene eseguito ogni ora. minuto Hello è controllato da hello *startTime*, se ne è stato specificato o se non è specificato, dal momento della creazione hello. Ad esempio, se start hello ora o ora di creazione (a seconda del valore si applica) è 12:25 PM, hello processo verrà eseguito 00:25, 25:01, 02:25,..., 23:25. Hello pianificazione è equivalente toohaving un processo con *frequenza* "ora", un *intervallo* 1 e n *pianificazione*. Hello differenza è che la pianificazione può essere utilizzata con diversi *frequenza* e *intervallo* toocreate altri processi troppo. Ad esempio, se hello *frequenza* fosse "month", la pianificazione hello viene eseguito solo una volta al mese anziché ogni giorno se *frequenza* stato "giorno" |
| <code>{minutes:[0]}</code> |Eseguire ogni ora in ora hello. Questo processo viene inoltre eseguito ogni ora, ma ora hello (ad esempio, 12 AM, AM 1, 2 AM, ecc.) Questo è equivalente tooa processo con una frequenza di "ora", un'ora di inizio e zero minuti, nessuna pianificazione se frequenza hello "day", ma se la frequenza di hello "settimana" o "month", pianificazione hello eseguirebbe rispettivamente un solo giorno una settimana o un mese, giorno. |
| <code>{"minutes":[15]}</code> |Eseguire 15 minuti dopo l’inizio di ogni ora. Viene eseguito ogni ora, a partire da 00:15, poi 01:15, 02:15, e così via fino a 22:15 e 23:15. |
| <code>{"hours":[17], "weekDays":["saturday"]}</code> |Eseguire alle 17.00 di ogni sabato |
| <code>{hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Eseguire alle 17 di ogni lunedì, mercoledì e venerdì |
| <code>{"minutes":[15,45], "hours":[17], "weekDays":["monday", "wednesday", "friday"]}</code> |Eseguire alle 17:15 e alle 17:45 di ogni lunedì, mercoledì e venerdì |
| <code>{"hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Eseguire alle 05:00 e alle 17:00 di ogni lunedì, mercoledì e venerdì |
| <code>{"minutes":[15,45], "hours":[5,17], "weekDays":["monday", "wednesday", "friday"]}</code> |Eseguire alle 05:15, alle 05:45, alle 17:15 e alle 17:45 di ogni lunedì, mercoledì e venerdì |
| <code>{"minutes":[0,15,30,45], "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Eseguire ogni 15 minuti nei giorni feriali |
| <code>{"minutes":[0,15,30,45], "hours": [9, 10, 11, 12, 13, 14, 15, 16] "weekDays":["monday", "tuesday", "wednesday", "thursday", "friday"]}</code> |Eseguire ogni 15 minuti nei giorni feriali tra le 09:00 e le 16:45 |
| <code>{"weekDays":["sunday"]}</code> |Eseguire ogni domenica all'ora di inizio |
| <code>{"weekDays":["tuesday", "thursday"]}</code> |Eseguire ogni martedì e giovedì all'ora di inizio |
| <code>{"minutes":[0], "hours":[6], "monthDays":[28]}</code> |Esegui alle ore 6 in hello 28 giorno di ogni mese (presupponendo che la frequenza del mese) |
| <code>{"minutes":[0], "hours":[6], "monthDays":[-1]}</code> |Eseguito alle ore 6 hello ultimo giorno del mese hello. Se si desidera un processo in hello toorun ultimo giorno del mese, utilizzare -1 anziché giorno 28, 29, 30 o 31. |
| <code>{"minutes":[0], "hours":[6], "monthDays":[1,-1]}</code> |Eseguito alle ore 6 hello primo e ultimo giorno di ogni mese |
| <code>{monthDays":[1,-1]}</code> |Eseguire su hello primo e ultimo giorno di ogni mese in fase di avvio |
| <code>{monthDays":[1,14]}</code> |Eseguire in hello primo e il quattordicesimo giorno di ogni mese in fase di avvio |
| <code>{monthDays":[2]}</code> |Eseguire in hello secondo giorno del mese in fase di avvio hello |
| <code>{"minutes":[0], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |Eseguire il primo venerdì di ogni mese alle 05:00 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1}]}</code> |: Eseguire il primo venerdì di ogni mese all’ora di inizio |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":-3}]}</code> |Eseguire il terzultimo venerdì di ogni mese, all'ora di inizio |
| <code>{"minutes":[15], "hours":[5], "monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Eseguire il primo e l’ultimo venerdì di ogni mese alle 05:15 |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":1},{"day":"friday", "occurrence":-1}]}</code> |Eseguire il primo e l’ultimo venerdì di ogni mese all’ora di inizio |
| <code>{"monthlyOccurrences":[{"day":"friday", "occurrence":5}]}</code> |Eseguire il quinto venerdì di ogni mese all’ora di inizio Se è presente alcun venerdì quinto in un mese, questo non viene eseguito, perché è toorun pianificato solo quinto venerdì. È consigliabile utilizzare -1 anziché su 5 occorrenza hello se si desidera toorun hello processo in corso ultimo hello venerdì del mese di hello. |
| <code>{"minutes":[0,15,30,45], "monthlyOccurrences":[{"day":"friday", "occurrence":-1}]}</code> |Eseguire ogni 15 minuti, ultimo venerdì del mese hello |
| <code>{"minutes":[15,45], "hours":[5,17], "monthlyOccurrences":[{"day":"wednesday", "occurrence":3}]}</code> |Eseguire 5:15 AM, 5:45 AM, 17:15:00 e 5:45 PM in hello 3rd mercoledì di ogni mese |

## <a name="see-also"></a>Vedere anche
 [Che cos'è l'Utilità di pianificazione?](scheduler-intro.md)

 [Concetti, terminologia e gerarchia di entità dell'Utilità di pianificazione di Azure](scheduler-concepts-terms.md)

 [Introduzione all'uso dell'utilità di pianificazione nel portale di Azure hello](scheduler-get-started-portal.md)

 [Piani e fatturazione nell'utilità di pianificazione di Azure](scheduler-plans-billing.md)

 [Informazioni di riferimento sull'API REST dell'Utilità di pianificazione di Azure](https://msdn.microsoft.com/library/mt629143)

 [Informazioni di riferimento sui cmdlet PowerShell dell'Utilità di pianificazione di Azure](scheduler-powershell-reference.md)

 [Livelli elevati di disponibilità e affidabilità dell'Utilità di pianificazione di Azure](scheduler-high-availability-reliability.md)

 [Limiti, valori predefiniti e codici di errore dell'Utilità di pianificazione di Azure](scheduler-limits-defaults-errors.md)

 [Autenticazione in uscita dell'Utilità di pianificazione di Azure](scheduler-outbound-authentication.md)

