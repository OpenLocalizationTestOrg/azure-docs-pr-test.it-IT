---
title: "un'unità disco in un dispositivo StorSimple aaaReplace | Documenti Microsoft"
description: "Viene illustrato come unità di tooreplace un disco in un'enclosure EBOD o di una enclosure principale StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 98890d36-b613-40fd-994e-330dd907a8a1
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: d2c78a6d951b0f00ac42e74a34cf1bc83952a3c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-disk-drive-on-your-storsimple-device"></a>Sostituzione di un'unità disco nel dispositivo StorSimple
## <a name="overview"></a>Panoramica
In questa esercitazione viene illustrato come rimuovere e sostituire un'unità disco rigido che non funziona correttamente o guasta in un dispositivo Microsoft Azure StorSimple. tooreplace un'unità disco, è necessario:

* Disattivare antimanomissione hello
* Rimuovere l'unità disco hello
* Installare il disco sostitutivo hello

> [!IMPORTANT]
> Prima di rimozione e sostituzione di un'unità disco, esaminare le informazioni di sicurezza hello in [sostituzione dei componenti hardware StorSimple](storsimple-hardware-component-replacement.md).
> 
> 

## <a name="disengage-hello-antitamper-lock"></a>Disattivare antimanomissione hello
Questa procedura illustra come possono essere occupati o non innestate quando si sostituiscono le unità disco hello chiusure antimanomissione di hello nel dispositivo StorSimple. chiusure antimanomissione Hello sono montati in hello unità vettore handle e vi si accede tramite una piccola apertura nel fermo hello dell'handle hello. Le unità vengono fornite con blocchi hello imposta la posizione toohello bloccato.

#### <a name="toounlock-hello-antitamper-lock"></a>chiusura antimanomissione hello toounlock
1. Inserire delicatamente chiave hello (un cacciavite T10 "chiusura" fornito da Microsoft) nell'apertura hello hello maniglia e nel relativo attacco. 
   
   > [!NOTE]
   > Se è attivata antimanomissione hello, indicatore rosso hello è visibile nell'apertura hello.
   > 
   > 
   
    ![Unità disco bloccata](./media/storsimple-disk-drive-replacement/IC741056.png)
   
    **Figura 1** Blocco antimanomissione attivato
   
   | Etichetta | Descrizione |
   |:--- |:--- |
   | 1 |Apertura indicatore |
   | 2 |Blocco antimanomissione |
2. Chiave di hello Ruota in senso antiorario finché l'indicatore rosso hello non è visibile nell'apertura di hello sopra hello chiave.
3. Rimuovere la chiave hello.
   
    ![Unità disco sbloccata](./media/storsimple-disk-drive-replacement/IC741057.png)
   
    **Figura 2** Unità disco sbloccata
4. è ora possibile rimuovere l'unità disco Hello.

Seguire i passaggi di hello in blocco hello tooengage inversa.

## <a name="remove-hello-disk-drive"></a>Rimuovere l'unità disco hello
Il dispositivo StorSimple supporta la configurazione degli spazi di archiviazione di tipo RAID 10. Ciò implica che può funzionare normalmente con un'unità a stato solido (SSD), un'unità disco rigido (HDD) o un disco guasto. 

> [!IMPORTANT]
> * Se il sistema dispone di più di un disco danneggiato, non rimuovere più di una unità SSD o HDD dal sistema hello in qualsiasi punto nel tempo. Ciò potrebbe causare una perdita dei dati.
> * Assicurarsi di inserire un'unità SSD sostitutiva in uno slot che in precedenza conteneva un'unità SSD. Analogamente, inserire un'unità HDD sostitutiva in uno slot che in precedenza conteneva un'unità HDD.
> * Nel portale di Azure classico hello, gli slot sono numerati da 0 a 11. Pertanto, se il portale di hello mostra che un disco nello slot 2 non riuscita, sul dispositivo hello, cercare hello disco nel terzo slot hello hello in alto a sinistra.
> 
> 

Unità possono essere rimosse e sostituite mentre sistema hello è operativo.

#### <a name="tooremove-a-drive"></a>tooremove un'unità
1. tooidentify hello disco danneggiato, in hello portale di Azure classico, andare troppo**dispositivi** > **manutenzione** > **stato Hardware**. Poiché può avere esito negativo di un disco nell'enclosure principale hello e/o in un'enclosure EBOD (se si utilizza un modello 8600), esaminare lo stato di hello di dischi hello in **componenti condivisi** e in **componenti condivisi enclosure EBOD**. Un disco guasto verrà visualizzato con uno stato rosso in entrambi gli chassis.
2. Individuare l'unità di hello nella parte anteriore hello di enclosure principale hello o enclosure EBOD hello. 
3. Se il disco di hello è sbloccato, continuare toohello successivo. Se il disco di hello è bloccato, sbloccarlo seguendo la procedura hello in [disattivare antimanomissione hello](#disengage-the-antitamper-lock).
4. Premere hello nero latch nel modulo di gestione delle spedizioni di hello unità e tirare maniglia di hello verso l'esterno dalla parte anteriore hello dello chassis hello. 
   
    ![Rilascio del punto di manipolazione dell'unità disco](./media/storsimple-disk-drive-replacement/IC741051.png)
   
    **Figura 3** rilascio dell'handle dell'unità hello
5. Quando maniglia di hello sia estesa completamente, far scorrere estraibile hello esterno dello chassis hello. 
   
    ![Scorrimento del disco fuori dall'unità disco](./media/storsimple-disk-drive-replacement/IC741052.png)
   
    **Figura 4** scorrimento all'unità disco hello fuori vettore hello

## <a name="install-hello-replacement-disk-drive"></a>Installare il disco sostitutivo hello
Dopo aver rimosso un'unità non è riuscito nel dispositivo StorSimple, seguire questa tooreplace procedura con una nuova unità.

#### <a name="tooinsert-a-drive"></a>tooinsert un'unità
1. Assicurarsi maniglia di hello sia estesa completamente, come mostrato nella seguente immagine hello.
   
    ![Unità disco con punto di manipolazione esteso](./media/storsimple-disk-drive-replacement/IC741044.png)
   
    **Figura 5** Unità con punto di manipolazione esteso
2. Diapositiva estraibile hello modo hello tutti nello chassis hello. 
   
    ![Scorrimento del disco nel supporto dell'unità disco](./media/storsimple-disk-drive-replacement/IC741045.png)
   
    **Figura 6** estendibile supporto estraibile hello nello chassis hello
3. Con hello vettore hello inserito, chiudere unità maniglia durante la continuazione toopush hello estraibile nello chassis di hello, fino a quando non hello maniglia scatta in posizione di blocco.
4. Tasto BLOC hello utilizzare fornita da maniglia a Microsoft (chiusura cacciavite Torx) toosecure hello in posizione ruotando vite hello un quarto di giro in senso orario.
5. Verificare che la sostituzione hello ha avuto esito positivo e hello unità sia operativa, accesso hello portale di Azure classico e la navigazione troppo**manutenzione** > **stato Hardware**. In **componenti condivisi** o **componenti condivisi enclosure EBOD**, lo stato di unità hello deve essere verde, che indica che è integro.
   
   > [!NOTE]
   > Può richiedere diverse ore hello disco stato tooturn verde dopo la sostituzione di hello.
   > 
   > 

## <a name="next-steps"></a>Passaggi successivi
Leggere ulteriori informazioni sulla [Sostituzione dei componenti hardware di StorSimple](storsimple-hardware-component-replacement.md).

