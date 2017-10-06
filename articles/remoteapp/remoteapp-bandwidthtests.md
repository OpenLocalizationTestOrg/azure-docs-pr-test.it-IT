---
title: aaaAzure RemoteApp - test l'utilizzo della larghezza di banda di rete con alcuni scenari comuni | Documenti Microsoft
description: Informazioni sugli scenari di utilizzo comune che consentono di determinare le esigenze di larghezza di banda di rete di Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 06417c75-0c63-4ecf-b9d1-66a7af6b7b91
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 22c1dbb61d956d58d01eb4e11363266168e337e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-remoteapp---testing-your-network-bandwidth-usage-with-some-common-scenarios"></a>Azure RemoteApp - Scenari comuni di test relativi all'utilizzo della larghezza di banda di rete
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.
> 
> 

Come accennato [utilizzo della larghezza di banda di rete di stima Azure RemoteApp](remoteapp-bandwidth.md), hello toofigure modo migliore l'impatto di hello della rete di Azure RemoteApp tooyour è toorun alcuni test di utilizzo. Eseguire questi test per un set tempo periodo e misura hello larghezza di banda necessaria per ogni scenario. Se si dispone di funzionalità hello, è possibile anche valutare hello pacchetto perdita schemi e di rete rete instabilità toounderstand hello rete che verranno creati nell'ambiente specifico.

Quando si valuta l'utilizzo della larghezza di banda hello, tenere presente che l'utilizzo varia tra i diversi utenti all'interno della società. Ad esempio, gli utenti che leggono o scrivono contenuti testuali in genere usano meno larghezza di banda rispetto agli utenti che lavorano con i video. Per ottenere risultati ottimali, esaminare le proprie esigenze e creare una combinazione di hello seguenti scenari che meglio rappresenta utenti hello nell'azienda. Ricordare troppo[revisione hello fattori influiscono sull'utilizzo della larghezza di banda e utente esperienza](remoteapp-bandwidthexperience.md) -che consenta di identificare i test ideale hello.

Prima di leggere informazioni sui test di hello, scegliere la combinazione e quindi eseguirli. È possibile utilizzare la tabella hello di sotto delle prestazioni di traccia toohelp.

> [!NOTE]
> Se non è possibile eseguire la propria rete di test o non dispone pertanto hello ora toodo, consultare il nostro [le stime della larghezza di banda di rete di base/indicazioni](remoteapp-bandwidthguidelines.md). Dal momento che il chilometraggio può variare, nei limiti del possibile è *consigliabile* eseguire test propri.
> 
> 

## <a name="hello-usage-tests"></a>test con un utilizzo Hello
Ogni test ha una durata diversa e verifica funzioni/funzionalità differenti che utilizzano la larghezza di banda di rete. Ricordare di combinazione di hello toochoose di test che corrisponde maggiormente gli utenti della società.

### <a name="executivecomplex-powerpoint---run-for-900-1000-seconds"></a>PowerPoint complesso/esecutivo: esecuzione per 900-1000 secondi 
Un utente presenta 45-50 diapositive ad alta fedeltà usando Microsoft Office PowerPoint in modalità schermo intero. diapositive Hello devono contenere immagini, le transizioni (con animazioni) e gli sfondi con sfumatura di colore che sono tipici dell'azienda. utente Hello dedicare almeno 20 secondi in ogni diapositiva.

Questo scenario viene creato traffico bursty, quando una diapositiva passa toohello diapositiva successiva nella presentazione hello.

### <a name="simple-powerpoint---run-for-620-seconds"></a>PowerPoint semplice: esecuzione per ~620 secondi
Un utente presenta un file di PowerPoint semplice con circa 30 diapositive usando Microsoft Office PowerPoint in modalità schermo intero. diapositive Hello sono testo con maggiore frequenza rispetto in uno scenario di hello PowerPoint Executive/complessi e più semplice sfondi e immagini (diagrammi neri). 

### <a name="internet-explorer---run-for-250-seconds"></a>Internet Explorer: esecuzione per ~250 secondi
Un utente accede web hello utilizzando Internet Explorer. Hello l'utente accede e scorre una combinazione di testo, immagini naturali e alcuni diagrammi. Hello pagine web memorizzate sul disco rigido locale hello del server Host sessione Desktop remoto (Host sessione Desktop remoto) hello come un. File MHT. Hello scorre utilizzando PGSU, PGGIÙ, su e giù chiavi, con intervalli diversi per ogni chiave o il tipo di scorrimento:

    - Giù - 250 pressioni di tasto ogni 500 ms
    - PGSU - 36 pressioni di tasti ogni 1.000 ms
    - Giù - 75 pressioni di tasto ogni 100 ms
    - PGGIÙ - 20 pressioni di tasto ogni 500 ms
    - Su - 120 pressioni di tasto ogni 300 ms

### <a name="pdf-document---simple---run-for-610-seconds"></a>Documento PDF semplice: esecuzione per ~610 secondi
Un utente legge ed esegue ricerche in un documento PDF in vari modi con Adobe Acrobat Reader. documento Hello deve essere costituita da tabelle, grafici semplici e più caratteri di testo. documento Hello è 35-40 pagine. utente Hello scorre a velocità diverse due, con le versioni precedenti e inoltra, quattro dimensioni di zoom (adatta toopage, toowidth appropriato, 100% e l'altra scelta). Hello zoom assicura che il testo hello (font) esegue il rendering di diverse dimensioni. È lo scorrimento verso il basso utilizzo hello PGSU, PGGIÙ, su e giù chiavi, con intervalli diversi per ogni tipo di scorrimento.

### <a name="pdf-document---mixed---run-for-320-seconds"></a>Documento PDF misto: esecuzione per ~320 secondi
Un utente legge ed esegue ricerche in un documento PDF in vari modi con Adobe Acrobat Reader. documento Hello è costituito da immagini di alta qualità (inclusi fotografie), tabelle, grafici semplici e più caratteri di testo. utente Hello scorre a velocità diverse due, con le versioni precedenti e inoltra, quattro dimensioni di zoom (adatta toopage, toowidth appropriato, 100% e l'altra scelta). Hello zoom assicura che il testo hello (font) esegue il rendering di diverse dimensioni. È lo scorrimento verso il basso utilizzo hello PGSU, PGGIÙ, su e giù chiavi, con intervalli diversi per ogni tipo di scorrimento.

### <a name="flash-video-playback---run-for-180-seconds"></a>Riproduzione di video Flash - esecuzione per ~180 secondi
Un utente visualizza un video codificato in Adobe Flash incorporato in una pagina Web. pagina web Hello viene archiviato nell'unità disco rigido locale hello del server Host sessione Desktop remoto hello. Hello video viene riprodotto in Internet Explorer da un lettore incorporato plug-in.

Questo scenario emula la visualizzazione di pagine Web inclusive di contenuti formattati multimediali da parte degli utenti. La maggior parte dei dati hello deve bo tramite VOBR.

### <a name="word-remote-typing---run-for-1800-seconds"></a>Digitazione remota in Word: esecuzione per ~1800 secondi
Un utente digita un documento in una sessione RDP. Le sequenze di tasti vengono inviati dal lato client hello tramite hello RDP sessione tooa documento di Microsoft Word in esecuzione nella sessione remota hello. la velocità di digitazione Hello è un carattere di ogni 250 ms (totale 7050 caratteri). 

Questo è uno degli scenari più comuni di hello per un knowledge worker. Questo scenario verifica la velocità di risposta hello di un utente digita in un processore moderno. Questo scenario è tooeven sensibili piccole variazioni nell'utilizzo della larghezza di banda.

## <a name="tracking-hello-test-results"></a>Risultati test di verifica hello
È possibile utilizzare i seguenti scenari di hello tooevaluate tabella nell'ambiente hello. dati Hello riportati di seguito sono solo per completezza, potrebbe essere molto diverso da è osservare. 

Per semplicità, si presuppone che tutti gli scenari vengono testati utilizzando la risoluzione dello schermo di hello 1920x1080 stesso pixel e i trasporti TCP su una rete con latenza (ritardo) inferiore a 200 ms e rete variazione in hello 120 ms + segno di circa l'1%.

Sulla tabella hello:

* **Media esperienza** contiene hello larghezza di banda in cui la produttività degli utenti non influisce notevolmente sulle ma non esclude piccoli guasti occasionali di video o audio. sistema Hello è in grado di toorecover rapidamente sfruttando logica dinamica hello. Hello rete larghezza di banda stime tentativo tooguarantee hello qualità hello esperienza dell'utente.
  * **Problemi rilevanti (punto di interruzione)** contiene hello larghezza di banda in consente di rilevare problemi significativi nell'esperienza e la produttività è interessata per periodi di tempo percettibile. A questo punto gli algoritmi RDP hello lavorano e non possono garantire la qualità dell'utente hello dell'esperienza a causa della larghezza di banda di rete insufficienti.
  * **Consigliato** contiene larghezza di banda di rete hello consigliato per un'esperienza ottima o eccellente. È in genere un passaggio superiore al valore hello hello corrispondente **Media esperienza** colonna.
  * **Note** include osservazioni e commenti.

| Test | Utilizzo medio | Problemi evidenti (punto di interruzione) | Larghezza di banda di rete raccomandata | Note |
| --- | --- | --- | --- | --- |
| PPT complesso/esecutivo |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s preferito |A 1 MB/s vengono perse molte animazioni |
| PPT semplice |5 MB/s |256 KB/s |10 MB/s |256 KB/s diapositive hello caricare con ritardo notevole |
| Internet Explorer |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s preferito |A 1 MB/s i video Web sono sfocati e irregolari, lo scorrimento veloce presenta problemi |
| PDF semplice |1 MB/s |256 KB/s |5 MB/s |256 KB/s occorre un po' di tempo pagina hello tooload |
| PDF misto |1 MB/s |256 KB/s |5 MB/s |256 KB/s pagina hello richiede una quantità notevole di tooload ora |
| Riproduzione di video Flash |10 MB/s |1 MB/s |> 10 MB/s, 100 MB/s preferito |1 MB/s è muove hello video e alcuni i fotogrammi vengono rimossi |
| Digitazione remota in Word |256 KB/s |128 KB/s |1 MB/s |256 KB/s utente potrebbero essere presenti tempo hello tra le sequenze di tasti |

tooevaluate hello larghezza di banda per ogni utente, creare una combinazione di hello sopra gli scenari e le proporzioni corrispondente di hello di larghezza di banda di rete necessarie. Selezionare numero più alto di hello necessario per gli scenari. Poiché gli utenti non usano quasi mai sistema hello da solo, prendere in considerazione alcune riserva per gli utenti che lavorano contemporaneamente nella stessa rete di hello.

## <a name="learn-more"></a>Altre informazioni
* [Uso previsto della larghezza di banda di rete di Azure RemoteApp](remoteapp-bandwidth.md)
* [Azure RemoteApp - In che modo la larghezza di banda di rete influisce sulla qualità dell'esperienza?](remoteapp-bandwidthexperience.md)
* [Larghezza di banda di rete di Azure RemoteApp - Linee guida generali (se non è possibile verificare direttamente)](remoteapp-bandwidthguidelines.md)

