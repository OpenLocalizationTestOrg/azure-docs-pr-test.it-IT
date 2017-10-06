---
title: campi aaaCustom Log Analitica | Documenti Microsoft
description: "funzionalità di campi personalizzati Hello del Log Analitica consente toocreate campi ricercabili personalizzati dai dati OMS che aggiunge toohello le proprietà di un record raccolto.  In questo articolo descrive hello processo toocreate un campo personalizzato e fornisce una procedura dettagliata con un evento di esempio."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 31572b51-6b57-4945-8208-ecfc3b5304fc
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 1aa0e497d5b1d7898b0da6a5ef40f568e63bc589
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="custom-fields-in-log-analytics"></a>Campi personalizzati in Log Analytics
Hello **campi personalizzati** di Log Analitica consente i record esistenti nel repository OMS hello tooextend aggiungendo i campi ricercabili.  I campi personalizzati vengono popolati automaticamente dati estratti dalle altre proprietà di hello stesso record.

![Panoramica dei campi personalizzati](media/log-analytics-custom-fields/overview.png)

Ad esempio, record di esempio hello riportato di seguito ha dati utili nascosti nella descrizione dell'evento hello.  L'estrazione di tali dati in proprietà separate li rende disponibili per azioni come l'ordinamento e il filtro.

![Pulsante di ricerca log](media/log-analytics-custom-fields/sample-extract.png)

> [!NOTE]
> In hello Preview, si è limitati too100 campi personalizzati nell'area di lavoro.  Tale limite verrà esteso con il passaggio della funzionalità alla disponibilità generale.
> 
> 

## <a name="creating-a-custom-field"></a>Creazione di un campo personalizzato
Quando si crea un campo personalizzato, Log Analitica deve comprendere quali toopopulate toouse dati il relativo valore.  Viene usata una tecnologia di Microsoft Research chiamata FlashExtract tooquickly identificare i dati.  Anziché richiedere tooprovide istruzioni esplicite, Log Analitica apprende sui dati hello desiderato tooextract dagli esempi forniti.

Hello le sezioni seguenti fornisce procedure hello per la creazione di un campo personalizzato.  Hello nella parte inferiore di questo articolo è una procedura dettagliata di un'estrazione di esempio.

> [!NOTE]
> campo personalizzato Hello viene popolato con i record corrispondente hello specificato vengono aggiunti l'archivio dati OMS di toohello, criteri in modo che verrà visualizzato solo per record raccolti dopo la creazione di campo personalizzato hello.  campo personalizzato Hello non verrà aggiunto toorecords già presenti nell'archivio dati hello quando viene creato.
> 
> 

### <a name="step-1--identify-records-that-will-have-hello-custom-field"></a>Passaggio 1: identificare i record che disporranno di campo personalizzato hello
primo passaggio Hello è record hello tooidentify che verrà hello di campo personalizzato.  Iniziare con un [ricerca log standard](log-analytics-log-searches.md) e quindi selezionare un record tooact come modello hello Analitica Log da cui apprenderà.  Quando si specifica che si sta tooextract dati in un campo personalizzato, hello **procedura guidata estrazione di campi** viene aperto in cui si convalidano e perfezionano i criteri di hello.

1. Andare troppo**ricerca nei Log** e utilizzare un [query record hello tooretrieve](log-analytics-log-searches.md) che avranno un campo personalizzato hello.
2. Selezionare un record di Log Analitica verranno utilizzati tooact come un modello per l'estrazione di campi personalizzati hello toopopulate di dati.  Sarà possibile identificare i dati di hello che si desidera tooextract da questo record e Log Analitica questo campo verrà utilizzato informazioni toodetermine hello logica toopopulate hello personalizzati per tutti i record simili.
3. Fare clic su hello pulsante toohello sinistra di qualsiasi proprietà di testo di hello record e seleziona **estrarre i campi da**.
4. Hello **procedura guidata estrazione di campi viene aperto**, e i record di hello selezionato viene visualizzato nel hello **Main Example** colonna.  campo personalizzato Hello verrà definito per i record con hello stessi valori di proprietà hello selezionate.  
5. Se la selezione hello è presente esattamente ciò che si desidera, selezionare i campi aggiuntivi toonarrow hello criteri.  Ordine toochange hello valori dei campi per i criteri di hello, è necessario annullare e selezionare un altro record corrispondente hello criteri desiderati.

### <a name="step-2---perform-initial-extract"></a>Passaggio 2: Eseguire l'estrazione iniziale
Dopo aver identificato i record di hello che disporranno di campo personalizzato hello, si identificano i dati di hello che si desidera tooextract.  Log Analitica utilizzerà questo simili tooidentify informazioni record simili.  Nel passaggio hello in seguito verrà essere in grado di toovalidate risultati hello e fornire altri dettagli per Log Analitica toouse nell'analisi.

1. Evidenziare il testo hello nel record di esempio hello che si desidera toopopulate campo personalizzato di hello.  Si verrà quindi visualizzata con un tooprovide finestra di dialogo un nome per hello campo e tooperform hello estrazione iniziale.  Hello caratteri  **\_CF** verranno aggiunti automaticamente.
2. Fare clic su **estrarre** tooperform un'analisi di record raccolti.  
3. Hello **riepilogo** e **risultati della ricerca** sezioni visualizzano i risultati di hello di hello estratto in modo sia possibile verificarne l'accuratezza.  **Riepilogo** Visualizza hello criteri usati tooidentify record e un conteggio per ognuno dei valori di dati hello identificati.  **I risultati della ricerca** fornisce un elenco dettagliato di record corrispondenti ai criteri di hello.

### <a name="step-3--verify-accuracy-of-hello-extract-and-create-custom-field"></a>Passaggio 3: verificare l'accuratezza di hello estratto e creare campi personalizzati
Dopo aver eseguito l'estrazione iniziale hello, Log Analitica visualizzerà i risultati in base ai dati che sono già stati raccolti.  Se hello risultati sono accurati è possibile creare campi personalizzati hello senza ulteriore lavoro.  In caso contrario, quindi è possibile perfezionare i risultati di hello in modo che Log Analitica può migliorare la propria logica.

1. Se i valori nell'estrazione iniziale hello non sono corretti, quindi fare clic su hello **modifica** record icona successivo tooan corrette e selezionare **modificare questa evidenziazione** nella selezione di hello toomodify dell'ordine.
2. voce Hello è copiato toohello **esempi aggiuntivi** sezione sottostante hello **Main Example**.  È possibile regolare l'evidenziazione hello qui toohelp Log Analitica comprendere hello selezione che avrebbe dovuto effettuare.
3. Fare clic su **estrarre** toouse registra questa nuova tooevaluate informazioni tutti hello esistente.  è possibile modificare i risultati di Hello per record diversi da hello uno che è stato appena modificato in base a questa nuova informazione.
4. Continuare fino a quando tutti i record di hello estrarre correttamente le correzioni di tooadd identificano hello dati toopopulate hello nuovo campo personalizzato.
5. Fare clic su **Save Extract** quando si è soddisfatti dei risultati di hello.  campo personalizzato Hello è ora definito, ma non verrà aggiunto il record tooany ancora.
6. Attesa per i nuovi record corrispondenti hello specificati criteri toobe raccolti e quindi eseguirla di nuovo la ricerca dei registri di hello. È necessario campo personalizzato hello nuovi record.
7. Usare hello campo personalizzato come qualsiasi altra proprietà di record.  È possibile usarlo tooaggregate e raggruppamento dei dati e utilizzare anche tooproduce nuovi approfondimenti.

## <a name="viewing-custom-fields"></a>Visualizzazione di campi personalizzati
È possibile visualizzare un elenco di tutti i campi personalizzati nel gruppo di gestione da hello **impostazioni** sezioni del dashboard OMS hello.  Selezionare **Dati** e quindi **Campi personalizzati** per visualizzare un elenco di tutti i campi personalizzati nell'area di lavoro.  

![Campi personalizzati](media/log-analytics-custom-fields/list.png)

## <a name="removing-a-custom-field"></a>Rimozione di un campo personalizzato
Esistono due modi tooremove un campo personalizzato.  Hello per primo è hello **rimuovere** opzione per ogni campo quando si visualizza l'elenco completo di hello come descritto in precedenza.  Hello altro metodo è un toohello pulsante hello record e fare clic a sinistra del campo hello tooretrieve.  menu di Hello conterrà un campo personalizzato di opzione tooremove hello.

## <a name="sample-walkthrough"></a>Procedura dettagliata di esempio
Hello nella sezione seguente vengono illustrati un esempio completo di creazione di un campo personalizzato.  In questo esempio estrae il nome del servizio hello negli eventi di Windows che indicano una modifica dello stato del servizio.  Questo comportamento si basa sugli eventi creati da Gestione controllo servizi nel Registro di sistema hello nei computer Windows.  Se si desidera toofollow in questo esempio, è necessario essere [la raccolta di eventi di informazione per il Registro di sistema hello](log-analytics-data-sources-windows-events.md).

Si immette hello seguente query tooreturn tutti gli eventi da Gestione controllo servizi con un ID evento 7036, cioè hello evento che indica l'avvio o arresto di un servizio.

![Query](media/log-analytics-custom-fields/query.png)

Selezionare quindi uno dei record con ID evento 7036.

![Record di origine](media/log-analytics-custom-fields/source-record.png)

È necessario hello nome del servizio che viene visualizzato in hello **RenderedDescription** hello selezionare pulsante Avanti toothis proprietà e.

![Estrarre i campi](media/log-analytics-custom-fields/extract-fields.png)

Hello **procedura guidata estrazione di campi** viene aperto e hello **EventLog** e **EventID** nella hello sono selezionati campi **Main Example** colonna.  Indica che il campo personalizzato hello verrà definito per gli eventi dal Registro di sistema hello con un ID evento 7036.  Ciò è sufficiente, quindi non è più necessario tooselect tutti gli altri campi.

![Main example](media/log-analytics-custom-fields/main-example.png)

È evidenziare il nome di hello del servizio hello hello **RenderedDescription** proprietà e utilizzare **servizio** tooidentify nome del servizio hello.  campo personalizzato Hello verrà chiamato **Service_CF**.

![Nome del campo](media/log-analytics-custom-fields/field-title.png)

È possibile notare che il nome servizio hello è identificato in modo corretto per alcuni record ma non per altri utenti.   Hello **risultati della ricerca** mostrano che parte del nome hello per hello **scheda WMI Performance** non è stata selezionata.  Hello **riepilogo** indica che i record con quattro **DPRMA** servizio include erroneamente una parola aggiuntiva e due record identificato **Installer moduli** anziché **Moduli di Windows Installer**.  

![Search Results](media/log-analytics-custom-fields/search-results-01.png)

Iniziamo con hello **scheda WMI Performance** record.  Fare clic sulla relativa icona di modifica e quindi su **Modify this highlight**.  

![Modificare l'evidenziazione](media/log-analytics-custom-fields/modify-highlight.png)

Si aumenta parola hello di hello evidenziazione tooinclude **WMI** e ripetere l'estrazione di hello.  

![Altro esempio](media/log-analytics-custom-fields/additional-example-01.png)

Possiamo vedere che hello voci per **scheda WMI Performance** sono state corrette e Analitica Log utilizzata anche tale record di hello informazioni toocorrect per **modulo di Windows Installer**.  Possiamo vedere in hello **riepilogo** sezione che **DPMRA** è ancora stato identificato correttamente.

![Search Results](media/log-analytics-custom-fields/search-results-02.png)

Scorrere fino a tooa record con il servizio DPMRA hello e utilizzare hello stessa procedura adottata toocorrect tale record.

![Altro esempio](media/log-analytics-custom-fields/additional-example-02.png)

 Quando si esegue l'estrazione di hello, si noterà che tutti i risultati sono ora precisi.

![Search Results](media/log-analytics-custom-fields/search-results-03.png)

È possibile osservare che **Service_CF** viene creato, ma non ancora aggiunto tooany record.

![Conteggio iniziale](media/log-analytics-custom-fields/initial-count.png)

Dopo che è trascorso tempo così nuovi eventi vengono raccolti, possiamo vedere che hello **Service_CF** campo ora viene aggiunto toorecords che corrispondono ai criteri.

![Risultati finali](media/log-analytics-custom-fields/final-results.png)

È ora possibile usare campo personalizzato di hello come qualsiasi altra proprietà di record.  tooillustrate, si crea una query che raggruppa in base al nuovo hello **Service_CF** tooinspect campo quali servizi sono più attivo hello.

![Raggruppa per query](media/log-analytics-custom-fields/query-group.png)

## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [log ricerche](log-analytics-log-searches.md) toobuild query utilizzando i campi personalizzati per i criteri.
* Monitorare i [file di log personalizzati](log-analytics-data-sources-custom-logs.md) analizzati usando campi personalizzati.

