---
title: aaaStorSimple componenti hardware e lo stato | Documenti Microsoft
description: Informazioni su come toomonitor hello componenti hardware del dispositivo StorSimple tramite hello servizio StorSimple Manager.
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 0d56a2ba-daf0-45ad-9610-8b8712dd5750
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 12a62c0ffc4a5b5e72a25e9e1d976009be03c598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-manager-service-toomonitor-hardware-components-and-status"></a>Utilizzare componenti di hardware toomonitor servizio StorSimple Manager hello e stato
## <a name="overview"></a>Panoramica
Questo articolo descrive hello vari componenti fisici e logici nel dispositivo StorSimple locale. Viene inoltre spiegato come toomonitor hello lo stato dei componenti di dispositivo utilizzando hello **manutenzione** pagina hello servizio StorSimple Manager. 

Hello **manutenzione** pagina Mostra stato hardware hello di tutti i componenti del dispositivo StorSimple hello. 

Nell'elenco di hello dei componenti per 8100, sono disponibili tre sezioni che descrivono:

* **I componenti condivisi** – questi non fanno parte del controller di hello, ad esempio unità disco, enclosure, componenti PCM e temperatura PCM, tensione di linea e sensori di corrente di riga.
* **Componenti controller 0** – componenti hello che si trovano nel Controller 0, ad esempio controller, espansore e connettore SAS, sensori di temperatura del controller e hello varie interfacce di rete.
* **Componenti controller 1** : hello componenti che costituiscono Controller 1, analoghi toothose dettagliate per il Controller 0.

Un dispositivo 8600 dispone di componenti aggiuntivi corrispondenti toohello enclosure EBOD Extended Bunch of dischi (). Nell'elenco di hello dei componenti, sono disponibili cinque sezioni. Le opzioni sono disponibili tre sezioni che contengono componenti hello enclosure principale hello e sono identico toohello quelli descritti per 8100. Esistono due sezioni aggiuntive per l'enclosure EBOD hello che descrivono:

* **Componenti condivisi enclosure EBOD** : hello componenti presenti nell'enclosure EBOD hello e nel PCM che non fanno parte del controller EBOD hello.
* **Componenti Controller 0 EBOD** : hello componenti che si trovano sull'enclosure EBOD 0, ad esempio controller EBOD hello, sensori di temperatura espansore e connettore e controller SAS.
* **Componenti Controller 1 EBOD** : hello componenti che costituiscono l'enclosure EBOD 1, analoghi toothose dettagliate per l'enclosure EBOD 0.

> [!NOTE]
> **sezione stato di Hello hardware non è presente nella pagina Manutenzione hello per un dispositivo virtuale StorSimple (1100).**
> 
> 

## <a name="monitor-hello-hardware-status"></a>Monitorare lo stato dell'hardware hello
Eseguire hello stato dell'hardware hello tooview passaggi di un componente di dispositivo seguenti:

1. Passare troppo**dispositivi**, selezionare un dispositivo StorSimple specifico. Fare clic su toogo nel menu a livello di dispositivo hello e quindi fare clic su **manutenzione**. 
2. Individuare hello **stato Hardware** sezione e scegliere tra i componenti disponibili hello (come descritto in precedenza). Fare clic su una freccia che precede hello etichetta tooexpand hello elenco e visualizzazione hello stato componente di hello vari componenti del dispositivo. Vedere hello [elenco dettagliata dei componenti per l'enclosure principale hello](#component-list-for-primary-enclosure-of-storsimple-device) hello e [elenco dettagliata dei componenti per l'enclosure EBOD hello](#component-list-for-ebod-enclosure-of-storsimple-device).
3. Utilizzare hello seguente lo stato del componente toointerpret lo schema di codifica a colori hello:
   
   * **Segno di spunta verde**: indica che un componente è **Integro** oppure **OK**.
   * **Giallo**: indica un componente in stato di **Avviso**.
   * **Punto esclamativo rosso**: indica che un componente è nello stato di **Errore** o **Richiede attenzione**.
   * **Bianco con testo nero** : indica che un componente non è presente.
4. Se si rileva un componente che non si trova in uno stato **Integro** , contattare il supporto tecnico Microsoft. Se gli avvisi sono attivati sul dispositivo, si riceverà un messaggio di avviso. Se è necessario tooreplace un componente hardware non riusciti, vedere [sostituzione dei componenti hardware StorSimple](storsimple-hardware-component-replacement.md).

## <a name="component-list-for-primary-enclosure-of-storsimple-device"></a>Elenco di componenti per l’enclosure principale del dispositivo StorSimple
Hello tabella seguente vengono illustrati hello componenti fisici e logici contenuti nell'enclosure principale di hello del dispositivo StorSimple locale.

| Componente | Modulo | Tipo | Percorso | Unità sostituibile sul campo (FRU)? | Descrizione |
| --- | --- | --- | --- | --- | --- |
| Unità in slot [0-11] |Unità disco |Fisico |Condiviso |Sì |Viene visualizzata una riga per ogni unità SSD hello o nelle unità HDD hello enclosure principale hello. |
| Sensore di temperatura ambientale |Chassis |Fisico |Condiviso |No |Le misure hello temperatura all'interno dello chassis hello. |
| Sensore di temperatura piano intermedio |Chassis |Fisico |Condiviso |No |Le misure hello temperatura del midplane hello. |
| Allarme acustico |Chassis |Fisico |Condiviso |No |Indica se il sottosistema di allarme acustico hello all'interno dello chassis hello è funzionale. |
| Chassis |Chassis |Fisico |Condiviso |Sì |Indica la presenza di hello dello chassis. |
| Impostazioni chassis |Chassis |Fisico |Condiviso |No |Si riferisce toohello pannello anteriore dello chassis hello. |
| Sensori di tensione linea |PCM |Fisico |Condiviso |No |Molti sensori di tensione di linea sono visualizzato lo stato che indica se hello misurata tensione è all'interno di tolleranza. |
| Sensori di corrente linea |PCM |Fisico |Condiviso |No |Molti sensori di corrente di linea sono visualizzato lo stato che indica se hello corrente misurata rientra tolleranza di errore. |
| Sensori di temperatura in PCM |PCM |Fisico |Condiviso |No |Molti sensori di temperatura come i sensori di entrata e l'area sensibile hanno visualizzato lo stato che indica se hello misurata temperatura è all'interno di tolleranza. |
| Alimentazione [0-1] |PCM |Fisico |Condiviso |Sì |Per ognuno degli alimentatori hello in hello viene visualizzata una riga due moduli PCM nella hello parte posteriore dispositivo hello. |
| Raffreddamento [0-1] |PCM |Fisico |Condiviso |Sì |Per ogni hello viene visualizzata una riga quattro ventole di raffreddamento situate in hello due moduli PCM. |
| Batteria [0-1] |PCM |Fisico |Condiviso |Sì |Viene visualizzata una riga per ognuno dei moduli di hello batteria di backup situato nel PCM hello. |
| Metis |N/D |Logico |Condiviso |N/D |Mostra lo stato di hello delle batterie hello: se necessari ad addebitare i costi e si stanno avvicinando fine del ciclo di vita. |
| HDInsight |N/D |Logico |Condiviso |N/D |Consente di visualizzare hello stato del cluster hello creato tra due moduli controller integrati di hello. |
| Nodo del cluster |N/D |Logico |Condiviso |N/D |Indica lo stato di hello del controller hello come parte del cluster di hello. |
| Quorum del cluster |N/D |Logico | |N/D |Indica la presenza di hello di hello maggioranza disco l'appartenenza al pool di archiviazione delle unità disco rigido hello. |
| Spazio dati unità disco rigido |N/D |Logico |Condiviso |N/D |spazio di archiviazione Hello che viene utilizzato per i dati nel pool di archiviazione di hello unità disco rigido (HDD). |
| Spazio di gestione di unità disco rigido |N/D |Logico |Condiviso |N/D |Hello riservato in hello pool di archiviazione delle unità disco rigido per attività di gestione. |
| Spazio quorum unità disco rigido |N/D |Logico |Condiviso |N/D |Hello riservato in hello pool di archiviazione delle unità disco rigido per il quorum del cluster. |
| Spazio sostituzione unità disco rigido |N/D |Logico |Condiviso |N/D |Hello riservato in hello pool di archiviazione unità disco rigido per la sostituzione del controller. |
| Spazio dati unità SSD |N/D |Logico |Condiviso |N/D |spazio di archiviazione Hello utilizzato per i dati nel pool di archiviazione di hello SSD unità SSD. |
| Spazio NVRAM SSD |N/D |Logico |Condiviso |N/D |spazio di archiviazione Hello in hello pool di archiviazione SSD dedicato alla logica NVRAM. |
| Pool di archiviazione di unità disco rigido |N/D |Logico |Condiviso |N/D |Consente di visualizzare hello stato del pool di archiviazione logico hello creato dalle unità disco rigido del dispositivo. |
| Pool di archiviazione di unità SSD |N/D |Logico |Condiviso |N/D |Consente di visualizzare hello lo stato del pool di archiviazione logico hello creata dall'unità SSD del dispositivo. |
| Controller [0-1] [stato] |I/O |Fisico |Controller |Sì |Mostra lo stato di hello del controller hello, e se è in modalità attiva o standby all'interno dello chassis hello. |
| Sensori di temperatura nel controller |I/O |Fisico |Controller |No |Molti sensori di temperatura come modulo dei / o, temperatura CPU, sensori DIMM e PCIe hanno lo stato visualizzato, che indica se è o meno temperatura hello rilevata nei limiti di tolleranza. |
| Espansore SAS |I/O |Fisico |Controller |No |Indica stato hello di hello seriale collegato SCSI (SAS) espansore tooconnect utilizzati hello archiviazione integrata toohello controller. |
| Connettore SAS [0-1] |I/O |Fisico |Controller |No |Indica lo stato di hello di ogni connettore SAS, ovvero espansore SAS toohello di archiviazione utilizzato tooconnect integrato. |
| Interconnessione piano intermedio SBB |I/O |Fisico |Controller |No |Indica lo stato di hello del connettore midplane hello è tooconnect usato ogni midplane toohello controller. |
| Core del processore |I/O |Fisico |Controller |No |Indica lo stato di hello hello di core del processore all'interno di ogni controller. |
| Alimentatore elettronica dello chassis |I/O |Fisico |Controller |No |Indica lo stato di hello del sistema di alimentazione hello usato dall'enclosure hello. |
| Diagnostica elettronica dello chassis |I/O |Fisico |Controller |No |Indica lo stato di hello dei sottosistemi di diagnostica hello fornito dal controller hello. |
| Baseboard Management Controller (BMC) |I/O |Fisico |Controller |No |Indica lo stato di hello di hello baseboard management controller (BMC), che è un processore di servizio specializzato che consente di monitorare i dispositivi hardware hello mediante sensori e comunica con l'amministratore di sistema hello tramite una connessione indipendente. |
| Ethernet |I/O |Fisico |Controller |No |Indica lo stato di hello di ognuna delle interfacce di rete hello, vale a dire gestione hello e le porte dati fornite nel controller hello. |
| NVRAM |I/O |Fisico |Controller |No |Indica lo stato di hello della NVRAM, una memoria ad accesso casuale non volatile backup dalla batteria hello che svolge informazioni importanti delle applicazioni tooretain nell'evento hello dell'interruzione dell'alimentazione. |

## <a name="component-list-for-ebod-enclosure-of-storsimple-device"></a>Elenco di componenti per l’enclosure EBOD del dispositivo StorSimple
Hello tabella seguente vengono illustrati hello componenti fisici e logici contenuti in hello enclosure EBOD del dispositivo StorSimple locale.

| Componente | Modulo | Tipo | Percorso | FRU? | Descrizione |
| --- | --- | --- | --- | --- | --- |
| Unità in slot [0-11] |Unità disco |Fisico |Condiviso |Sì |Viene visualizzata una riga per ogni unità HDD in primo piano hello hello enclosure EBOD hello. |
| Sensore di temperatura ambientale |Chassis |Fisico |Condiviso |No |Le misure hello temperatura all'interno dello chassis hello. |
| Sensore di temperatura piano intermedio |Chassis |Fisico |Condiviso |No |Le misure hello temperatura del midplane hello. |
| Allarme acustico |Chassis |Fisico |Condiviso |No |Indica se il sottosistema di allarme acustico hello all'interno dello chassis hello è funzionale. |
| Chassis |Chassis |Fisico |Condiviso |Sì |Indica la presenza di hello dello chassis. |
| Impostazioni chassis |Chassis |Fisico |Condiviso |No |Si riferisce toohello OPS o il pannello anteriore di hello dello chassis hello. |
| Sensori di tensione linea |PCM |Fisico |Condiviso |No |Molti sensori di tensione di linea sono visualizzato lo stato che indica se hello misurata tensione è all'interno di tolleranza. |
| Sensori di corrente linea |PCM |Fisico |Condiviso |No |Molti sensori di corrente di linea sono visualizzato lo stato che indica se hello corrente misurata rientra tolleranza di errore. |
| Sensori di temperatura in PCM |PCM |Fisico |Condiviso |No |Molti sensori di temperatura come i sensori di entrata e l'area sensibile hanno lo stato visualizzato, che indica se hello misurata temperatura è all'interno di tolleranza. |
| Alimentazione [0-1] |PCM |Fisico |Condiviso |Sì |Per ognuno degli alimentatori hello in hello viene visualizzata una riga due moduli PCM nella hello parte posteriore dispositivo hello. |
| Raffreddamento [0-1] |PCM |Fisico |Condiviso |Sì |Per ogni hello viene visualizzata una riga quattro ventole di raffreddamento situate in hello due moduli PCM. |
| Archiviazione locale [HDD] |N/D |Logico |Condiviso |N/D |Consente di visualizzare hello stato del pool di archiviazione logico hello creato dalle unità disco rigido del dispositivo. |
| Controller [0-1] [stato] |I/O |Fisico |Controller |Sì |Consente di visualizzare hello stato dei controller hello nel modulo EBOD hello. |
| Sensori di temperatura in EBOD |I/O |Fisico |Controller |No |Molti sensori di temperatura da ogni controller hanno lo stato visualizzato, che indica se temperatura di hello rilevata rientra nei limiti di tolleranza. |
| Espansore SAS |I/O |Fisico |Controller |No |Indica lo stato di hello dell'espansore SAS hello tooconnect utilizzati hello archiviazione integrata toohello controller. |
| Connettore SAS [0-2] |I/O |Fisico |Controller |No |Indica lo stato di hello di ogni connettore SAS, ovvero espansore SAS toohello di archiviazione utilizzato tooconnect integrato. |
| Interconnessione piano intermedio SBB |I/O |Fisico |Controller |No |Indica lo stato di hello del connettore midplane hello è tooconnect usato ogni midplane toohello controller. |
| Alimentatore elettronica dello chassis |I/O |Fisico |Controller |No |Indica lo stato di hello del sistema di alimentazione hello usato dall'enclosure hello. |
| Diagnostica elettronica dello chassis |I/O |Fisico |Controller |No |Indica lo stato di hello dei sottosistemi di diagnostica hello fornito dal controller hello. |
| Controller toodevice connessione |I/O |Fisico |Controller |No |Indica lo stato di hello della connessione hello tra il modulo dei / o EBOD hello e controller del dispositivo hello. |

## <a name="next-steps"></a>Passaggi successivi
* toouse hello tooadminister servizio StorSimple Manager il dispositivo, andare troppo[utilizzare hello tooadminister servizio StorSimple Manager dispositivo StorSimple](storsimple-manager-service-administration.md).
* Se è necessario tootroubleshoot un componente di dispositivi con stato ridotto o non riuscito, fare riferimento troppo [indicatori di monitoraggio di StorSimple](storsimple-monitoring-indicators.md). 
* tooreplace un componente hardware non riusciti, vedere [sostituzione dei componenti hardware StorSimple](storsimple-hardware-component-replacement.md).
* Se si continuano, problemi dei dispositivi tooexperience [contattare il supporto Microsoft](storsimple-contact-microsoft-support.md).

