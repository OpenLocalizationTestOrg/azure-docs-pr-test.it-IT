---
title: Catalogo dati di domande frequenti aaaAzure | Documenti Microsoft
description: "Domande frequenti relative al Catalogo dati di Azure, incluse le funzionalità per la gestione, l'annotazione e l'individuazione dell'origine dati."
services: data-catalog
documentationcenter: 
author: steelanddata
manager: NA
editor: 
tags: 
ms.assetid: 5c7e209a-458c-4bb4-96bb-7ed178f9528a
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 08/15/2017
ms.author: maroche
ms.openlocfilehash: 03f9f4b801640b2e14232c62c8fc168e42e2c393
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-catalog-frequently-asked-questions"></a>Domande frequenti sul Catalogo dati di Azure
Questo articolo fornisce le risposte toofrequently frequenti domande riguardo toohello servizio di Azure Data Catalog.

## <a name="what-is-azure-data-catalog"></a>Che cos'è il Catalogo dei dati di Azure?
Data Catalog è un servizio completamente gestito, ospitato in Microsoft Azure, che funge da sistema di registrazione e di individuazione per origini dati aziendali. Con il catalogo dati, qualsiasi utente, gli esperti toodata gli analisti e sviluppatori, può registrare, individuare, comprendere e utilizzare le origini dati.

## <a name="what-customer-challenges-does-it-solve"></a>Quali sono le problematiche dei clienti che consente di risolvere?
Gli indirizzi dei dati del catalogo hello difficoltà di individuazione dell'origine dati e di "dati scuri" in modo che gli utenti possono individuare e comprendere origini dati aziendali.

## <a name="what-are-its-target-audiences"></a>A chi è destinato?
Data Catalog è progettato per gli utenti tecnici e non tecnici, tra cui:

* Dati sviluppatori e professionisti di Business Intelligence e analitica: responsabili per la creazione di dati e analitica di contenuto per altri tooconsume.
* Amministratori dei dati: gli utenti che dispongono di conoscenza di hello hello dati, cosa significa e come è previsto toobe utilizzato.
* Consumer di dati: persone che necessario toobe tooeasily in grado di individuare, comprendere e connettere i dati toohello devono toodo relativo processo, lo strumento hello di propria scelta.
* Centrale IT: gli utenti che necessitano individuabile toomake centinaia di origini dati da parte degli utenti di business e che necessitano di supervisione toomaintain sulla modalità di utilizzo dei dati e da chi.

## <a name="what-is-its-availability-by-region"></a>Qual è la disponibilità per area?
Servizi di catalogo dati attualmente disponibili in hello centri dati seguenti:

* Stati Uniti occidentali
* Stati Uniti Orientali
* Europa occidentale
* Europa settentrionale
* Australia orientale
* Asia sudorientale

## <a name="what-are-its-limits-on-hello-number-of-data-assets"></a>Quali sono i limiti sul numero di hello di asset di dati?
Hello edizione gratuita di catalogo dati è limitato too5, asset di dati registrati 000.

supporta l'edizione Standard di catalogo dati Hello backup too100, 000 registrato asset di dati.

## <a name="what-are-its-supported-data-source-and-asset-types"></a>Quali sono i tipi di origine dati e di asset supportati?
Per un elenco di origini dati attualmente supportate, vedere [Riferimento per l'origine dati di Azure Data Catalog](data-catalog-dsr.md).

## <a name="how-do-i-request-support-for-another-data-source"></a>Come si richiede il supporto per un'altra origine dati?
toosubmit funzionalità richieste e altri commenti e suggerimenti, andare toohello [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-do-i-get-started-with-data-catalog"></a>Come si inizia a usare Data Catalog?
Hello tooget modo migliore avviato è passando troppo[Introduzione al catalogo dati](data-catalog-get-started.md). Questo articolo è una panoramica di end-to-end delle funzionalità di hello nel servizio hello.

## <a name="how-do-i-register-my-data"></a>Come si registrano i dati?
tooregister i dati nel catalogo dati:
1. Nel portale di Azure Data Catalog, hello hello **pubblica** area, lo strumento di registrazione iniziale hello Azure Data Catalog. 
2. Nel catalogo dati hello pubblicazione dell'applicazione, accedere con hello stesso credenziali utilizzate tooaccess hello portale catalogo dati.
3. Selezionare l'origine dati hello e beni di hello specifici che si desidera tooregister.

## <a name="what-properties-does-it-extract-for-data-assets-that-are-registered"></a>Quali proprietà estrae per gli asset di dati registrati?
proprietà specifiche di Hello differisce dall'origine toodata di origine dati, ma, in generale, hello del servizio pubblicazione sul catalogo di dati estrae hello le seguenti informazioni:

* Nome dell’asset
* Tipo di risorsa
* Descrizione dell’asset
* Nomi di colonna/attributo
* Tipi di dati di colonna/attributo
* Descrizione di colonna/attributo

> [!IMPORTANT]
> La registrazione di asset di dati con Data Catalog non spostare o copiare i dati nel cloud toohello. Registrazione delle risorse da un'origine dati copie hello tooAzure i metadati degli asset, ma hello dati rimangono nella posizione di origine dati esistente hello. regola di Hello eccezione toothis è se si sceglie record di anteprima tooupload o un profilo dati quando si registra l'attività hello. Quando si include un'anteprima, backup too20 record vengono copiati da ogni asset e archiviati come snapshot nel catalogo dati. Quando si include un profilo dati, informazioni di aggregazione vengano calcolate e inclusi nei metadati hello che vengono archiviati nel catalogo di hello. Informazioni di aggregazione possono includere hello dimensione delle tabelle, hello percentuale di valori null per ogni colonna o hello minimo, massimo e medi i valori per le colonne. 
>
>

> [!NOTE]
> Per le origini dati, ad esempio SQL Server Analysis Services con un costrutto **descrizione** proprietà hello catalogo dati di pubblicazione dell'applicazione estrae il valore della proprietà. Per i database relazionali di SQL Server, che non dispongono di un costrutto **descrizione** proprietà hello applicazione per la pubblicazione del catalogo dati estrae il valore di hello da hello **ms_description** proprietà estesa per gli oggetti e colonne. Per altre informazioni, vedere [Uso di proprietà estese su oggetti di database](https://technet.microsoft.com/library/ms190243%28v=sql.105%29.aspx).
>
>

## <a name="how-long-should-it-take-for-newly-registered-assets-tooappear-in-hello-catalog"></a>Quanto tempo necessario per tooappear asset appena registrati nel catalogo di hello?
Dopo aver registrato gli asset con il catalogo dati, potrebbe esserci un periodo di 5 secondi too10 prima che vengano visualizzati nel portale di hello catalogo dati.

## <a name="how-do-i-annotate-and-enrich-hello-metadata-for-my-registered-data-assets"></a>Come aggiungere annotazioni e arricchire hello metadati per l'asset di dati registrati?
Hello più semplice modo tooprovide i metadati per gli asset registrati è bene hello tooselect nel portale di catalogo dati hello e quindi immettere i valori hello nel riquadro Proprietà hello o dello schema per l'oggetto selezionato hello.

È anche possibile fornire alcuni metadati, ad esempio esperti e tag, durante il processo di registrazione hello. i valori di Hello fornito nel servizio di pubblicazione del catalogo dati hello validi tooall asset viene registrato in quel momento. oggetti tooview hello recentemente registrati nel portale di hello per un'ulteriore annotazione, seleziona hello **portale visualizzazione** pulsante nella schermata finale di hello di hello applicazione per la pubblicazione del catalogo dati.

## <a name="how-do-i-delete-my-registered-data-objects"></a>Come si eliminano gli oggetti dati registrati?
È possibile eliminare un oggetto dal catalogo dati selezionando oggetto hello nel portale di hello e quindi fare clic su hello **eliminare** pulsante. Rimozione oggetto hello rimuove i metadati dal catalogo dati, ma non modifica origine dati sottostante hello.

## <a name="what-is-an-expert"></a>Che cos'è un esperto?
Un esperto è una persona che ha una prospettiva informata su un oggetto dati. Un oggetto può avere più esperti. Un esperto non necessita di hello toobe "proprietario" per un oggetto, ma è semplicemente un utente che sa come dati hello possono e deve essere utilizzato.

## <a name="how-do-i-share-information-with-hello-data-catalog-team-if-i-encounter-problems"></a>Come è possibile condividere informazioni con il team di catalogo dati hello se verificano problemi?
problemi di tooreport, condividere informazioni e porre domande, visita toohello [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="does-hello-catalog-work-with-another-data-source-that-im-interested-in"></a>Esegue operazioni di catalogo hello con un'altra origine dati che desidero?
Si sta lavorando attivamente aggiungendo ulteriori tooData di origini dati del catalogo. Se si desidera toosee un'origine dati specifica supportata, consigliabile (o voice il supporto tecnico se è già stato suggerito) da passare toohello [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409).

## <a name="how-is-azure-data-catalog-related-toohello-data-catalog-in-power-bi-for-office-365"></a>Come è Azure Data Catalog correlati toohello catalogo dati in Power BI per Office 365?
È possibile considerare come un'evoluzione del catalogo dati in Power BI hello Azure Data Catalog. A partire da spring 2017, Azure Data Catalog è usato tooenable hello condivisione e l'individuazione di query in Excel 2016 e Power Query per Excel. Funzionalità di catalogo dati di Excel sono disponibili toousers con licenze di Power BI Pro.

## <a name="what-permissions-do-i-need-tooregister-assets-with-data-catalog"></a>Cosa fare le autorizzazioni sono necessarie risorse tooregister con catalogo dati?
strumento di registrazione toorun hello catalogo dati, sono necessarie autorizzazioni sull'origine dati hello che consente di determinare i metadati di hello tooread dall'origine di hello. tooalso includono un'anteprima, è necessario disporre delle autorizzazioni che consentono di tooread nei dati hello dagli oggetti hello in corso la registrazione.

## <a name="will-data-catalog-be-made-available-for-on-premises-deployment-as-well"></a>Data Catalog sarà disponibile anche per la distribuzione locale?
Catalogo dati è un servizio cloud che può funzionare con toodeliver di origini dati sia in locale e cloud soluzione ibrida individuazione origine dati. Non è attualmente previsto per una versione di hello servizio Catalogo dati che viene eseguito in locale.

## <a name="can-i-extract-more-or-richer-metadata-from-hello-data-sources-i-register"></a>È possibile estrarre metadati più completi o altre origini di dati hello che la registrazione?
Stiamo lavorando attivamente funzionalità hello tooexpand del catalogo dati. Se si desidera toohave metadati aggiuntivi estratti dall'origine dati hello durante la registrazione, suggerire (oppure voto perché, se è già stato suggerito) in hello [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). In futuro hello, verrà consentito a terzi tooadd nuovi tipi di origini dati tramite un'API di estensibilità.

## <a name="how-do-i-restrict-hello-visibility-of-registered-data-assets-so-that-only-certain-people-can-discover-them"></a>Come limitare la visibilità di hello degli asset di dati registrata, in modo che solo determinati utenti possono individuarli?
Selezionare asset di dati hello in hello catalogo dati e quindi fare clic su hello **Take Ownership** pulsante. I proprietari degli asset di dati nel catalogo dati è possono modificare la visibilità di hello tooeither impostazioni hello di toodiscover utenti tutte le risorse di proprietà come consentire o limitare gli utenti toospecific visibilità.

## <a name="how-do-i-update-hello-registration-for-a-data-asset-so-that-changes-in-hello-data-source-are-reflected-in-hello-catalog"></a>Come aggiornare la registrazione di hello per un asset di dati in modo che le modifiche nell'origine dati hello vengono riflesse nel catalogo di hello?
semplicemente tooupdate hello metadati per gli asset di dati che sono già registrati nel catalogo di hello, registrare nuovamente origine dati hello che contiene risorse hello. Tutte le modifiche nell'origine dati hello, ad esempio aggiunta o rimozione di tabelle o viste, le colonne vengono aggiornate nel catalogo di hello, ma vengono mantenute tutte le annotazioni fornite dagli utenti.

## <a name="my-question-isnt-answered-here-where-can-i-go-for-answers"></a>Non sono disponibili risposte a una domanda. Dove è possibile trovarle?
Passare toohello [forum di Azure Data Catalog](http://go.microsoft.com/fwlink/?LinkID=616424&clcid=0x409). dove le domande frequenti trovano risposta.
