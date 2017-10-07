---
title: set di dati di aaaUse hello campione in Machine Learning Studio | Documenti Microsoft
description: "Descrizioni dei set di dati hello utilizzati nei modelli di esempio inclusi in Machine Learning Studio. È possibile usare questi set di dati di esempio per gli esperimenti."
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 03a0b844-e8a7-4896-996f-d3c7a0db7a50
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: c7786478db82d40aaf27c37b3947ded5f042dd70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-sample-datasets-in-azure-machine-learning-studio"></a>Utilizzare i set di dati di esempio hello in Azure Machine Learning Studio
[top]: #machine-learning-sample-datasets

Quando si crea una nuova area di lavoro in Azure Machine Learning, per impostazione predefinita è inclusa una serie di set di dati e di esperimenti di esempio. Molti di questi set di dati di esempio vengono utilizzate dai modelli di esempio hello in hello [Azure Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/). Altri sono inclusi come esempi di diversi tipi di dati usati in genere per l'apprendimento automatico.

Alcuni di questi set di dati sono disponibili nell'archivio BLOB di Azure. Per questi set di dati, hello nella tabella seguente fornisce un collegamento diretto. È possibile utilizzare questi set di dati in esperimenti con hello [l'importazione dei dati] [ import-data] modulo.

rest Hello di questi set di dati di esempio sono disponibili nell'area di lavoro in **Saved Datasets** in hello modulo tavolozza toohello a sinistra dell'area di sperimentazione hello quando si apre o crea un nuovo esperimento in Machine Learning Studio.
È possibile utilizzare uno di questi set di dati in un esperimento trascinandolo tooyour esperimento canvas.


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<table>

<tr>
  <th align=left>Nome del set di dati</th>
  <th align=left>Descrizione del set di dati</th>
</tr>

<tr>
  <td valign=top>Adult Census Income Binary Classification dataset</td>
  <td valign=top>
Un subset di database di censimento hello 1994, usando gli adulti lavoro età hello di 16 con un indice di reddito > 100.<p> </p><b>Utilizzo:</b> classificare gli utenti che utilizzano dati demografici toopredict se una persona guadagna oltre 50 K all'anno.<p> </p><b>Ricerca correlata:</b> Kohavi, R., Becker, B., (1996). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=airport-codes-dataset>
  <td valign=top>Airport Codes Dataset</td>
  <td valign=top>
Codici degli aeroporti degli Stati Uniti.<p> </p>Questo set di dati contiene una riga per ogni aeroporto di Stati Uniti, fornire il numero di ID aeroporto hello e nome insieme hello percorso città e stato.
  </td>
</tr>

<tr>
  <td valign=top>Automobile price data (Raw)</td>
  <td valign=top>
Informazioni automobili per marca e modello, tra cui il prezzo di hello, funzionalità, ad esempio il numero di hello di cilindri MPG, nonché un punteggio di rischi assicurativi.<p> </p>Punteggio di rischio Hello inizialmente associata automaticamente prezzo e sono state modificate per un rischio effettivo in un processo noto tooactuaries come symboling. Un valore di + 3 indica che è rischiosa automatica hello e un valore di -3 che si è probabilmente sicura.<p> </p><b>Utilizzo:</b> punteggio di rischio hello Predict dalle funzionalità, utilizza la classificazione di regressione o multivariate. <p> </p><b>Ricerca correlata:</b> Schlimmer, J.C. (1987). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=bike-rental-uci-dataset>
  <td valign=top>Bike Rental UCI dataset</td>
  <td valign=top>
Set di dati UCI relativo al noleggio di biciclette basato su dati reali della società Capital Bikeshare che gestisce una rete di noleggio di biciclette a Washington DC.<p> </p>Hello dispone di una riga per ogni ora del giorno in 2011 e 2012, per un totale di 17,379 righe. intervallo di Hello di noleggio di hourly bike è compreso tra 1 too977.

  </td>
</tr>

<tr ID=bill-gates-rgb-image>
  <td valign=top>Bill Gates RGB Image</td>
  <td valign=top>
Convertire il file di immagine disponibile pubblicamente tooCSV dati.<p> </p>Hello codice per la conversione di immagine hello viene fornito in hello <strong>colore quantizzazione tramite clustering K-Means</strong> pagina dei dettagli del modello.
  </td>
</tr>

<tr>
  <td valign=top>Blood donation data</td>
  <td valign=top>
Un subset dei dati dal database di donatori di sangue hello di hello trasfusioni servizio centro di Hsin Chu City, Taiwan.<p> </p>I dati dei donatori includono mesi hello dall'ultimo donato) e frequenza o hello il numero totale di donazioni, tempo trascorso dall'ultimo donato e quantità di sangue donato.<p> </p><b>Utilizzo:</b> obiettivo hello è toopredict tramite classificazione se donatori hello donato sangue nel marzo 2007, dove 1 indica un donatori durante il periodo di destinazione hello e 0 un non-donatori. <p> </p><b>Ricerca correlata:</b> Yeh, I.C., (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>Yeh, I-Cheng, Yang, King-Jang, and Ting, Tao-Ming, "Knowledge discovery on RFM model using Bernoulli sequence", Expert Systems with Applications, 2008, <a href="http://dx.doi.org/10.1016/j.eswa.2008.07.018">http://dx.doi.org/10.1016/j.eswa.2008.07.018</a>
  </td>
</tr>

<tr ID=book-reviews-from-amazon>
  <td valign=top>Book Reviews from Amazon</td>
  <td valign=top>
Revisioni di libri in Amazon, impiegato dal sito Web amazon.com hello da ricercatori University di Pennsylvania (<a href="http://www.cs.jhu.edu/~mdredze/datasets/sentiment/">sentiment</a>). Vedere il documento di ricerca di hello, "biografie, Bollywood, braccio caselle e Blenders: dominio adeguamento Sentiment Classification" John Blitzer, Mark Dredze e Fernando Pereira; Associazione di calcolo Linguistics (ACL), 2007.<p> </p>set di dati originale Hello è K 975 revisioni con classificazione 1, 2, 3, 4 o 5. revisioni Hello sono stati scritti in inglese e sono di hello 1997-2007 periodo di tempo. Questo set di dati è stato eseguito too10K revisioni.
  </td>
</tr>

<tr>
  <td valign=top>Breast cancer data</td>
  <td valign=top>
Uno dei tre cancer relativi set di dati forniti da hello Institute Oncology che viene visualizzato spesso nella documentazione di machine learning. Combina informazioni diagnostiche con funzionalità relative ad analisi di laboratorio effettuate su circa 300 campioni di tessuto.<p> </p><b>Utilizzo:</b> classificare tipo hello di cancer, in base agli 9 attributi, alcune delle quali sono lineare e alcune siano categoriche. <p> </p><b>Ricerca correlata:</b> Wohlberg, W.H., Street, W.N., & Mangasarian, O.L. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=breast-cancer-features>
  <td valign=top>Breast Cancer Features <td valign=top>
Hello set di dati contiene informazioni per le aree sospette 102K (candidati) delle immagini raggi x, descritti dalla 117 funzionalità. funzionalità di Hello sono proprietarie e il relativo significato non è indicato dalla creatori di set di dati hello (Siemens Healthcare). 
  </td>
</tr>

<tr ID=breast-cancer-info>
  <td valign=top>Breast Cancer Info</td>
  <td valign=top>
set di dati Hello contiene informazioni aggiuntive per ogni area sospetta dell'immagine a raggi x. Ogni esempio vengono fornite informazioni (ad esempio, etichetta, paziente ID, le coordinate dell'intera immagine di patch toohello relativo) sul numero di riga nel set di dati Breast Cancer funzionalità hello corrispondente hello. Per ogni paziente sono disponibili diversi esempi. Per i pazienti in cui è stato riscontrato un tumore, alcuni esempio sono positivi ed altri sono negativi. Per i pazienti sani, tutti gli esempi sono negativi. set di dati Hello presenta esempi di K 102. dataset Hello è influenzato, 0,6% dei punti di hello sono positivi, negativi rest hello. set di dati Hello è stato reso disponibile dal Siemens Healthcare.
  </td>
</tr>

<tr ID=crm-appetency-labels-shared>
  <td valign=top>CRM Appetency Labels Shared</td>
  <td valign=top>
Le etichette dalla richiesta di stima relazione cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_appetency.labels">orange_small_train_appetency.labels</a>).
  </td>
</tr>

<tr ID=crm-churn-labels-shared>
  <td valign=top>CRM Churn Labels Shared</td>
  <td valign=top>
Le etichette dalla richiesta di stima relazione cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_small_train_churn.labels">orange_small_train_churn.labels</a>).
  </td>
</tr>

<tr ID=crm-dataset-shared>
  <td valign=top>CRM Dataset Shared</td>
  <td valign=top>
Questi dati provengono da una richiesta di stima relazione cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/kdd-cup-2009-customer-relationship-prediction - orange_small_train.data.zip">orange_small_train.data.zip</a>).<p> </p>set di dati Hello contiene 50K clienti dalla società di telecomunicazioni francese arancione hello. Ogni cliente dispone di 230 elementi resi anonimi, 190 dei quali numerici e 40 categorici. le funzionalità di Hello sono molto frammentate.
  </td>
</tr>

<tr ID=crm-upselling-labels-shared>
  <td valign=top>CRM Upselling Labels Shared</td>
  <td valign=top>
Le etichette dalla richiesta di stima relazione cliente hello KDD Cup 2009 (<a href="http://www.sigkdd.org/site/2009/files/orange_large_train_upselling.labels">orange_large_train_upselling.labels</a>).
  </td>
</tr>

<tr>
  <td valign=top>Energy Efficiency Regression data</td>
  <td valign=top>
Raccolta di profili energetici simulati, basati su 12 forme di edifici diverse. edifici Hello si differenzino per le funzionalità di 8, ad esempio vetro area hello vetro distribuzione area e l'orientamento.<p> </p><b>Utilizzo:</b> utilizzare regressione o classificazione toopredict hello efficienza energetica classificazione in base a come uno dei due valori reali risposte. Per la classificazione multiclasse, è round toohello variabile di risposta hello numero intero più vicino. <p> </p><b>Ricerca correlata:</b> Xifara, A. &amp; Tsanas, A. (2012). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=flight-delays-data>
  <td valign=top>Flight Delays Data</td>
  <td valign=top>
Volo passeggeri in fase di dati sulle prestazioni prelevati hello TranStats di raccolta dati di hello Stati Uniti Dipartimento dei trasporti degli Stati Uniti (<a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">On-Time</a>).<p> </p>set di dati Hello copre hello periodo di tempo, aprile-ottobre 2013. Prima di caricare tooAzure Machine Learning Studio, i set di dati di hello è stato elaborato come indicato di seguito:<ul><li>set di dati Hello è stato filtrato toocover solo hello 70 più movimentati aeroporti continentali hello Stati Uniti</li><li>I voli cancellati sono stati etichettati in modo da indicare un ritardo superiore a 15 minuti</li><li>I voli deviati sono stati esclusi</li><li>Hello colonne seguenti sono state selezionate: anno, mese, DayofMonth, DayOfWeek, vettore, OriginAirportID, DestAirportID, CRSDepTime, DepDelay, DepDel15, CRSArrTime, ArrDelay, ArrDel15, Canceled</li></ul>
</td>
</tr>

<tr>
  <td valign=top>Flight on-time performance (Raw)</td>
  <td valign=top>
Record degli arrivi e delle partenze dei voli all'interno degli Stati Uniti da ottobre 2011.<p> </p><b>Utilizzo:</b> prevedere i ritardi dei voli. <p> </p><b>Ricerca correlata:</b> dal Ministero dei Trasporti statunitense <a href="http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time">http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&amp;DB_Short_Name=On-Time</a>.
  </td>
</tr>

<tr>
  <td valign=top>Forest fires data</td>
  <td valign=top>
Contiene dati climatici, ad esempio temperatura, indici di umidità e velocità del vento, relativi a un'area nella parte nordorientale del Portogallo, combinati con record relativi agli incendi nei boschi.<p> </p><b>Utilizzo:</b> questa caratteristica è un'attività difficile regressione in obiettivo hello toopredict hello masterizzata area dell'insieme di strutture generato. <p> </p><b>Ricerca correlata:</b> Cortez, P., &amp; Morais, A. (2008). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>[Cortez e Morais, 2007] P. Cortez e A. Morais. Un approccio di Data Mining tooPredict foresta generato utilizzando i dati meteorologici. In J. Neves, M. F. Santos e J. Machado Eds., nuove tendenze in intelligenza artificiale, svolgimento di hello 13 EPIA 2007 - portoghese conferenza Intelligence 523-Guimarães, (Portogallo), pagine 512, artificiale, dicembre 2007. APPIA, ISBN-13 978-989-95618-0-9. Disponibile all'indirizzo: <a href="http://www.dsi.uminho.pt/~pcortez/fires.pdf">http://www.dsi.uminho.pt/~pcortez/fires.pdf</a>.
  </td>
</tr>

<tr ID=german-credit-card-uci-dataset>
  <td valign=top>German Credit Card UCI dataset</td>
  <td valign=top>
Hello UCI Statlog (German Credit Card) set di dati (<a href="http://archive.ics.uci.edu/ml/datasets/Statlog+(German+Credit+Data)">Statlog + tedesco + + dati di credito</a>), utilizzando file german.data hello.<p> </p>set di dati Hello classifica persone, descritte da un set di attributi, come i rischi di credito low o high. Ogni esempio rappresenta una persona. Sono disponibili funzionalità di 20, sia numeriche che categoriche e un'etichetta binaria (valore rischio di credito hello). Le voci che rappresentano un rischio di credito elevato hanno l'etichetta 2, quelle che rappresentano un rischio di credito hanno l'etichetta 1. costo Hello interpretato come un esempio di basso rischio al livello più elevato è 1, mentre il costo di hello del interpretato come un esempio ad alto rischio il minimo è 5.
  </td>
</tr>

<tr ID=imdb-movie-titles>
  <td valign=top>IMDB Movie Titles</td>
  <td valign=top>
set di dati Hello contiene informazioni su filmati che sono stati classificati nel TWEET Twitter: IMDB film ID, nome film, genre e anno di produzione. Sono presenti K 17 filmati nel set di dati hello. set di dati Hello è stata introdotta in carta hello "S. Dooms, T. De Pessemier e L. Martens. "MovieTweetings: a Movie Rating Dataset Collected From Twitter. Workshop on Crowdsourcing and Human Computation for Recommender Systems, CrowdRec at RecSys 2013."
  </td>
</tr>

<tr>
  <td valign=top>Iris two class data</td>
  <td valign=top>
Questo è probabilmente hello famosa database toobe trovato nella documentazione di riconoscimento modello hello. set di dati Hello è relativamente limitato, che contiene 50 sono riportati esempi di misurazioni petalo dalle tre varietà di iris.<p> </p><b>Utilizzo:</b> stimare tipo iris hello in base alle misurazioni hello.  <p> </p><b>Ricerca correlata:</b> Fisher, R.A. (1988). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr ID=movie-tweets>
  <td valign=top>Movie Tweets</td>
  <td valign=top>
set di dati Hello è una versione estesa del set di dati di hello Tweetings film. set di dati di Hello include 170K classificazioni per i film, estratto da ben strutturati TWEET su Twitter. Ogni istanza rappresenta un tweet ed è una tupla: ID utente, ID del film nel database IMDB, valutazione, data e ora, numero di preferenze per questo tweet e numero di retweet. set di dati Hello è stato reso disponibile dal detto A., Dooms s, B. Loni e Tikk D. per 2014 Challenge sistemi di raccomandazione.
  </td>
</tr>

<tr>
  <td valign=top>MPG data for various automobiles</td>
  <td valign=top>
Questo set di dati è una versione leggermente modificata del set di dati hello forniti dalla libreria StatLib hello della Carnegie Mellon University. set di dati Hello è stato utilizzato in hello 1983 American illustrativo statistica di associazione.<p> </p>dati Hello elencano carburante per vari automobili in chilometri al litro, insieme con le informazioni, ad esempio numeri hello di cilindri, spostamento di motore, potenza, peso e l'accelerazione.<p> </p><b>Utilizzo:</b> prevedere il risparmio di carburante in base a 3 attributi discreti multivalore e 5 attributi continui. <p> </p><b>Ricerca correlata:</b> StatLib, Carnegie Mellon University, (1993). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>Pima Indians Diabetes Binary Classification dataset</td>
  <td valign=top>
Un subset dei dati dal database di National Institute di diabete e quest ' e il relativo Diseases hello. set di dati Hello è stato filtrato toofocus su pazienti femmine del patrimonio indiano Pima. dati Hello includono dati medicali, ad esempio glucosio e livelli sciroppo, nonché dello stile di vita.<p> </p><b>Utilizzo:</b> stimare se il soggetto hello è diabete (classificazione binaria). <p> </p><b>Ricerca correlata:</b> Sigillito, V. (1990). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml"</a>. Irvine, CA: University of California, School of Information and Computer Science  </td>
</tr>

<tr>
  <td valign=top>Restaurant customer data</td>
  <td valign=top>
Set di metadati relativi ai clienti, inclusi dati demografici e preferenze.<p> </p><b>Utilizzo:</b> usare questo set di dati, in combinazione con altri due ristorante set di dati, tootrain di hello e test di un sistema di raccomandazione. <p> </p><b>Ricerca correlata:</b> Bache, K. e Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Restaurant feature data</td>
  <td valign=top>
Set di metadati relativi ai ristoranti e alle rispettive caratteristiche, ad esempio tipo di cibo, stile del ristorante e ubicazione.<p> </p><b>Utilizzo:</b> usare questo set di dati, in combinazione con altri due ristorante set di dati, tootrain di hello e test di un sistema di raccomandazione. <p> </p><b>Ricerca correlata:</b> Bache, K. e Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Restaurant ratings</td>
  <td valign=top>
Contiene le classificazioni fornite da utenti toorestaurants su una scala da 0 too2.<p> </p><b>Utilizzo:</b> usare questo set di dati, in combinazione con altri due ristorante set di dati, tootrain di hello e test di un sistema di raccomandazione. <p> </p><b>Ricerca correlata:</b> Bache, K. e Lichman, M. (2013). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science.
  </td>
</tr>

<tr>
  <td valign=top>Steel Annealing multi-class dataset</td>
  <td valign=top>
Questo set di dati contiene una serie di record da steel annealing sperimentazioni con gli attributi fisici hello di larghezza (spessore, (serpentina, foglio e così via) di hello risultante acciaio tipi.<p> </p><b>Utilizzo:</b> prevedere uno dei due attributi numerici della classe, ovvero durezza o forza. È anche possibile analizzare le correlazioni tra gli attributi.<p> </p>Le designazioni dell'acciaio sono basate su uno standard definito da SAE e da altre organizzazioni. Si sta cercando di uno specifico 'livello di (variabile di classe hello) e si desiderano valori hello toounderstand necessari. <p> </p><b>Ricerca correlata:</b> Sterling, D. & Buntine, W. (NA). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information and Computer Science  <p> </p>Livelli di toosteel una guida utile è reperibile qui: <a href="http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf">http://www.outokumpu.com/SiteCollectionDocuments/Outokumpu-steel-grades-properties-global-standards.pdf</a>
  </td>
</tr>

<tr>
  <td valign=top>Telescope data</td>
  <td valign=top>
Record di esplosioni di particelle gamma a energia elevata insieme alla radiazione di fondo, simulate entrambe tramite un processo Monte Carlo.<p> </p>scopo di Hello di simulazione hello è accuratezza hello tooimprove di terra senso Cherenkov gamma ottici, usando metodi statistici toodifferentiate tra segnale desiderato hello (Cherenkov ionizzanti docce) e rumore di fondo (hadronic docce avviate da raggi cosmici in atmosfera superiore hello).<p> </p>Hello dati sono stata pre-elaborato toocreate un cluster con allungato asse lungo hello è orientato verso il centro di fotocamera hello. sono riportate le caratteristiche di Hello di questa ellisse (spesso chiamati parametri Hillas) tra i parametri di immagine hello che possono essere utilizzati per l'analisi discriminante.<p> </p><b>Utilizzo:</b> prevedere se l'immagine di una pioggia rappresenta un segnale o radiazioni di fondo.<p> </p><b>Note:</b> la semplice precisione della classificazione non è significativa per questi dati, poiché la classificazione di un evento di fondo come segnale è ritenuta peggiore della classificazione di un evento di segnale come evento di fondo. Per il confronto dei classificatori diversi grafico ROC hello deve essere utilizzato. probabilità di accettazione di un evento in background come segnale deve essere inferiore a una delle seguenti soglie hello Hello: 0,01, 0,02, 0,05, 0,1 o 0,2.<p> </p>Si noti inoltre che è sottovalutato numero hello di eventi in background (per docce hadronic h), mentre nelle misure reale, classe h o rumore hello rappresenta maggioranza hello di eventi. <p> </p><b>Ricerca correlata:</b> Bock, R.K. (1995). UCI Machine Learning Repository <a href="http://archive.ics.uci.edu/ml">http://archive.ics.uci.edu/ml</a>. Irvine, CA: University of California, School of Information </td>
</tr>

<tr ID=weather-dataset>
  <td valign=top>Weather Dataset</td>
  <td valign=top>
Osservazioni terra weather oraria da NOAA (<a href="http://cdo.ncdc.noaa.gov/qclcd_ascii/, merged data from 201304 too201310">unire dati da too201310 201304</a>).<p> </p>dati meteorologici Hello coprono osservazioni effettuate da aeroporto weather stazioni, copertura hello periodo di tempo, aprile-ottobre 2013. Prima di caricare tooAzure Machine Learning Studio, i set di dati di hello è stato elaborato come indicato di seguito:<ul><li>ID stazione meteo sono state mappate toocorresponding aeroporto ID</li><li>Sono state filtrate Weather stazioni non associate a aeroporti più movimentati 70 hello</li><li>colonna Data Hello è stato suddiviso in colonne distinte di anno, mese e giorno</li><li>Hello colonne seguenti sono state selezionate: AirportID, anno, mese, giorno, ora, fuso orario, SkyCondition, visibilità, WeatherType, DryBulbFarenheit, DryBulbCelsius, WetBulbFarenheit, WetBulbCelsius, DewPointFarenheit, DewPointCelsius, RelativeHumidity, Velocità del vento, WindDirection, ValueForWindCharacter, StationPressure, PressureTendency, PressureChange, SeaLevelPressure, RecordType, HourlyPrecip, Altimeter</li></ul>
  </td>
</tr>

<tr ID=wikipedia-sp-500-dataset>
  <td valign=top>Wikipedia SP 500 Dataset</td>
  <td valign=top>
I dati sono tratti da articoli di Wikipedia (<a href="http://www.wikipedia.org/">http://www.wikipedia.org/</a>)su ognuna delle società incluse nell'indice S&P 500, archiviati come dati XML.<p> </p>Prima di caricare tooAzure Machine Learning Studio, i set di dati di hello è stato elaborato come indicato di seguito:<ul><li>Estrazione del contenuto di testo per ogni specifica società</li><li>Rimozione della formattazione wiki</li><li>Rimozione dei caratteri non alfanumerici</li><li>Convertire tutte toolowercase testo</li><li>Aggiunta delle categorie di società note</li></ul><p> </p>Si noti che per alcune società un articolo potrebbe non essere trovato, pertanto il numero di hello di record è minore di 500.
  </td>
</tr>





<tr ID=direct-marketing>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/direct_marketing.csv">direct_marketing.csv</a></td>
  <td valign=top>
set di dati Hello contiene i dati dei clienti e le indicazioni sulla campagna di mailing diretto tooa di risposta. Ogni riga rappresenta un cliente. set di dati Hello contiene 9 funzionalità sui dati demografici utente e il comportamento e 3 colonne di etichetta (visita, conversione e spesa).  Visita è una colonna di dati binari che indica che un cliente visitato dopo hello campagna di marketing, conversione indica che un cliente ha acquistato un elemento e spesa è quantità hello impiegato.  set di dati Hello è stato reso disponibile dal Kevin Hillstrom per MineThatData posta elettronica Analitica e Data Mining di verifica.
  </td>
</tr>

<tr ID=lyrl2004-tokens-test>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_test.csv">lyrl2004_tokens_test.csv</a></td>
  <td valign=top>
Funzionalità degli esempi di test nel set di dati notizie hello Reuters RCV1-V2. set di dati di Hello include articoli K 781 insieme ai relativi ID (prima colonna del set di dati hello). Ogni articolo è stato analizzato per identificare token, parole non significative e sottoposto a stemming. set di dati Hello è stato reso disponibile da David. D. Lewis.
  </td>
</tr>

<tr ID=lyrl2004-tokens-train>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/lyrl2004_tokens_train.csv">lyrl2004_tokens_train.csv</a></td>
  <td valign=top>
Funzionalità di esempi di training nel set di dati notizie hello Reuters RCV1-V2. set di dati di Hello include articoli 23K insieme ai relativi ID (prima colonna del set di dati hello). Ogni articolo è stato analizzato per identificare token, parole non significative e sottoposto a stemming. set di dati Hello è stato reso disponibile da David. D. Lewis.
  </td>
</tr>

<tr ID=intrusion-detection>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a><br></td>
  <td valign=top>
Set di dati da hello KDD Cup 1999 l'individuazione delle informazioni e dati concorrenza di strumenti di Data Mining (<a href="http://kdd.ics.uci.edu/databases/kddcup99/kddcup99.html">kddcup99.html</a>).<p> </p>set di dati Hello è stata scaricata e archiviati nell'archiviazione Blob di Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/network_intrusion_detection.csv">network_intrusion_detection.csv</a>) e include training e il set di dati di testing. Hello training set contiene circa 126K righe e 43 colonne, incluse le etichette di hello. Tre colonne fanno parte delle informazioni di etichetta hello e 40 colonne, costituito da funzionalità numerici e stringa/categoria, sono disponibili per il training del modello di hello. dati di test hello sono circa 22,5 KB esempi con colonne hello 43 stesso come dati di training hello di test.

  </td>
</tr>

<tr ID=rcv1-v2-topics-qrels>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/rcv1-v2.topics.qrels.csv">rcv1-v2.topics.qrels.csv</a></td>
  <td valign=top>
Assegnazioni di argomento per gli articoli di notizie nel set di dati notizie hello Reuters RCV1-V2. Argomenti tooseveral può essere assegnato da un articolo. formato Hello di ogni riga è "&lt;il nome dell'argomento&gt; &lt;id documento&gt; 1". set di dati Hello contiene assegnazioni argomento 2.6M. set di dati Hello è stato reso disponibile da David. D. Lewis.
  </td>
</tr>

<tr ID=student-performance>
  <td valign=top><a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a></td>
  <td valign=top>
Questi dati provengono da una richiesta di valutazione delle prestazioni KDD Cup 2010 studente hello (<a href="http://www.kdd.org/kdd-cup-2010-student-performance-evaluation">la valutazione delle prestazioni degli studenti</a>). dati utilizzati Hello sono hello Algebra_2008_2009 training set (Niculescu su chi ha apposto, J.,-Mizil, r., Ritter, s, Gordon, G.J. & Koedinger, K.R. (2010). Algebra I 2008-2009. Set di dati di competizione dalla KDD Cup 2010 dedicata al data mining in ambito didattico. Il training è disponibile in <a href="http://pslcdatashop.web.cmu.edu/KDDCup/downloads.jsp">downloads.jsp</a> o <a href="http://www.kdd.org/sites/default/files/kddcup/site/2010/files/algebra_2008_2009.zip">algebra_2008_2009.zip</a>.<p> </p>set di dati Hello è stata scaricata e archiviati nell'archiviazione Blob di Azure (<a href="https://azuremlsampleexperiments.blob.core.windows.net/datasets/student_performance.txt">student_performance.txt</a>) e contiene i file di log da uno studente lezioni private di sistema. le funzionalità di Hello fornito includono l'ID problema e la relativa descrizione breve, ID dello studente, timestamp, e quanti tentativi studente hello apportato prima di risolvere il problema di hello in hello modo a destra. set di dati originale Hello ha record 8,9 M. Questo set di dati è stato eseguito toohello prima K 100 righe. set di dati di Hello ha 23 colonne delimitati da tabulazioni dei vari tipi: numerico, organizzato per categorie e timestamp.

  </td>
</tr>




</table>


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
