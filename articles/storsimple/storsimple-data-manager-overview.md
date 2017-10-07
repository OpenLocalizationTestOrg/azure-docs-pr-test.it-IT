---
title: Panoramica di gestione di dati di Azure StorSimple aaaMicrosoft | Documenti Microsoft
description: Viene fornita una panoramica di hello servizio StorSimple Manager di dati (anteprima privata)
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 11/22/2016
ms.author: vidarmsft
ms.openlocfilehash: 5d29f7d26be9f2b36857526bdea770d991cece6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="storsimple-data-manager-overview-private-preview"></a>Panoramica di StorSimple Data Manager (anteprima privata)

## <a name="overview"></a>Panoramica

Microsoft Azure StorSimple è una soluzione di archiviazione cloud ibrida che indirizzi hello complessità dei dati non strutturati generalmente associati a condivisioni file. StorSimple utilizza l'archiviazione cloud come soluzione locale di un'estensione di hello e livelli automaticamente i dati tra l'archiviazione locale hello e archiviazione cloud. Integrati, protezione dei dati locali e gli snapshot nel cloud, evitando hello un'infrastruttura di archiviazione ha. Archiviazione e ripristino di emergenza è trasparente anche con cloud hello funge da una posizione esterna.

servizio di trasformazione di dati Hello Microsoft sta introducendo in questo documento consente si tooseamlessly accesso hello StorSimple dati nel cloud hello. Questo servizio fornisce i dati di tooextract API da StorSimple e presentarli tooother Azure servizi nei formati che possono essere utilizzati facilmente. formati di Hello è supportati in questa versione di anteprima sono BLOB di Azure e gli asset di servizi multimediali di Azure. Questa trasformazione consente si tooeasily collegare i servizi, ad esempio servizi multimediali di Azure, HDInsight di Azure, Azure Machine Learning e ricerca di Azure dati toooperate nel dispositivo StorSimple serie 8000 locale.

Di seguito viene presentato un diagramma a blocchi di alto livello illustrativo.

![Diagramma di alto livello](./media//storsimple-data-manager-overview/high-level-diagram.png)

Nel documento viene spiegato come iscriversi per un'anteprima privata di questo servizio. Viene inoltre illustrato come utilizzare questa applicazione di servizio toowrite che utilizzano dati di StorSimple e altri servizi di Azure nel cloud hello.

## <a name="sign-up-for-data-manager-preview"></a>Eseguire l'iscrizione per l'anteprima di Data Manager
Prima di iscriversi per il servizio di gestione dati hello, esaminare hello seguenti prerequisiti.

### <a name="prerequisites"></a>Prerequisiti

Questo esercizio presuppone che l'utente abbia
* una sottoscrizione di Azure attiva.
* accesso tooa registrazione dispositivo di StorSimple 8000 series
* tutti hello chiavi associate ai dispositivi serie StorSimple 8000 hello.

### <a name="sign-up"></a>Iscrizione

Hello StorSimple Data Manager è in anteprima privata. Eseguire hello toosign passaggi per l'anteprima privata di questo servizio seguente:

1.  Accedere a hello portale di Azure con estensione della gestione di dati di StorSimple hello in: [https://aka.ms/HybridDataManager](https://aka.ms/HybridDataManager). Utilizzare toolog le credenziali di Azure in.

2.  Fare clic su hello  **+**  toocreate icona un servizio. Fare clic su **archiviazione** e quindi fare clic su **vedere tutti** nel pannello hello visualizzata.

    ![Ricerca dell'icona di StorSimple Data Manager](./media/storsimple-data-manager-overview/search-data-manager-icon.png)

3. Viene visualizzata l'icona di gestione di dati di StorSimple di hello.

    ![Selezione dell'icona di StorSimple Data Manager](./media/storsimple-data-manager-overview/select-data-manager-icon.png)

4. Fare clic sull'icona di StorSimple Data Manager, quindi su **Crea**. Selezionare una sottoscrizione di hello che desidera tooenable per l'anteprima privata hello e quindi fare clic su **iscriversi me!**

    ![Esegui iscrizione](./media/storsimple-data-manager-overview/sign-me-up.png)

5. Consente di inviare una richiesta tooonboard è. che verrà gestita non appena possibile. Dopo l'abilitazione della sottoscrizione, sarà possibile creare un servizio StorSimple Data Manager.

6. tooeasily accedere servizio StorSimple Manager dati hello, fare clic su toopin icona a stella hello è tooyour Preferiti.

    ![Accesso a StorSimple Data Manager](./media/storsimple-data-manager-overview/access-data-managers.png)


## <a name="next-steps"></a>Passaggi successivi

[Utilizzare i dati di interfaccia utente di gestione dati di StorSimple tootransform](storsimple-data-manager-ui.md).
