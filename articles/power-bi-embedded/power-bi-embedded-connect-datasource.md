---
title: Power BI Embedded - connessione origine dati di tooa aaaMicrosoft
description: Power BI incorporato, connettere origini toodata
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Connessione origine dati tooa
Con **Power BI Embedded**è possibile incorporare report in proprie app. Quando si incorpora un report di Power BI nell'app, report hello si connette toohello sottostante dei dati da **importazione** una copia di dati hello o da **la connessione diretta** toohello origine dati mediante  **DirectQuery**.

Di seguito sono differenze nell'utilizzo hello **importazione** e **DirectQuery**.

| Importa | DirectQuery |
| --- | --- |
| Tabelle, colonne, *e dati* sono importato o copiato in set di dati del report hello. toosee modifica i dati sottostanti toohello durante l'esecuzione, è necessario aggiornare o importare, nuovamente un dataset corrente non completato. |Solo *tabelle e colonne* sono importato o copiato in set di dati del report hello. È sempre possibile visualizzare dati più recenti di hello. |

Con Power BI Embedded è attualmente possibile usare DirectQuery con le origini dati cloud ma non su origini dati locali.

> [!NOTE]
> Hello Gateway dati locale non è supportata con Power BI incorporato in questo momento. Non è quindi possibile usare DirectQuery con origini dati locali.

## <a name="supported-data-sources"></a>Origini dati supportate

**DirectQuery**
* Database SQL di Azure
* Azure SQL Data Warehouse

**Import (Importa) (Import (Importa)a)**

È possibile importare tramite tutte le origini dati disponibili hello in Power BI Desktop. Sarà possibile **non** essere in grado di toorefresh dati all'interno di Power BI Embedded. Sarà necessario modifiche tooupload tooyour PBIX file tooPower BI incorporata. Questo è dovuto toono disponibile gateway. 

## <a name="benefits-of-using-directquery"></a>Vantaggi di DirectQuery
L'uso di **DirectQuery**presenta due vantaggi principali:

* **DirectQuery** consente di creare visualizzazioni su set di dati molto grandi, in cui in caso contrario non sarebbe fattibile toofirst Importa tutti i dati di hello.
* Modifica dei dati sottostanti può richiedere un aggiornamento dei dati e per alcuni report, hello necessitano toodisplay corrente dati può richiedere trasferimenti di dati di grandi dimensioni, rendendo impraticabile reimportare i dati. I report **DirectQuery** usano invece sempre dati correnti.

## <a name="limitations-of-directquery"></a>Limitazioni di DirectQuery
   Esistono alcune limitazioni toousing **DirectQuery**:

* Tutte le tabelle devono provenire da un database singolo.
* Se la query hello è eccessivamente complessa, si verificherà un errore. Errore di hello tooremedy deve effettuare il refactoring query hello è meno complessa. Se query hello devono essere complesse, sarà necessario dati hello tooimport anziché **DirectQuery**.
* Il filtro delle relazioni è limitato tooa unica direzione, invece di entrambe le direzioni.
* È possibile modificare il tipo di dati hello di una colonna.
* Per impostazione predefinita, alle espressioni DAX valide per le misure sono imposte limitazioni. Vedere [DirectQuery e misure](#measures).

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery e misure
le query di tooensure inviate l'origine dati sottostante toohello hanno prestazioni accettabili, vengono imposte limitazioni alle misure. Quando si utilizza **Power BI Desktop**avanzate gli utenti possono scegliere toobypass questa limitazione selezionando **File > Opzioni e impostazioni > Opzioni**. In hello **opzioni** finestra di dialogo, scegliere **DirectQuery**e selezionare l'opzione hello **Consenti misure senza limitazioni in modalità DirectQuery**. Se tale opzione viene selezionata, è possibile usare qualsiasi espressione DAX valida per una misura. Gli utenti devono tenere; Tuttavia, che alcune espressioni che prestazioni molto elevate quando si importano dati hello può comportare back-end toohello query molto lente nell'origine **DirectQuery** modalità. 

## <a name="see-also"></a>Vedere anche
* [Introduzione a Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

Altre domande? [Provare a hello Community di Power BI](http://community.powerbi.com/)

