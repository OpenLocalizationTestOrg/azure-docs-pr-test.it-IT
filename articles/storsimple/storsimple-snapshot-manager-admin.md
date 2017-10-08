---
title: amministrazione di gestione Snapshot aaaStorSimple | Documenti Microsoft
description: "Fornisce una panoramica e collegamenti toomore informazioni sulle attività di amministrazione di gestione Snapshot StorSimple soluzioni e flussi di lavoro."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 1cdbb61d-bd16-4be4-ade2-ceab11508acb
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2016
ms.author: v-sharos
ms.openlocfilehash: d875f2efbdeb844b412cf8d9f1f971f18da7526e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-tooadminister-your-storsimple-solution"></a>Utilizzare Gestione Snapshot StorSimple tooadminister la soluzione StorSimple

## <a name="overview"></a>Panoramica
Gestione Snapshot StorSimple è uno snap-in Microsoft Management Console (MMC) che semplifica la protezione dei dati e la gestione dei backup in un ambiente di Microsoft Azure StorSimple. Con gestione Snapshot StorSimple, è possibile gestire dati di Microsoft Azure StorSimple in data center di hello e nel cloud hello come una soluzione di archiviazione integrata singolo, pertanto semplificando i processi di backup e riducendo i costi.

console di gestione centrale di gestione Snapshot StorSimple Hello consente toocreate coerente, in un momento copie di backup locale e i dati nel cloud. Ad esempio, è possibile utilizzare la console di hello per:

* Configurare, eseguire il backup ed eliminare volumi.
* Configurare il volume tooensure gruppi di dati di backup è coerente con l'applicazione.
* Gestire criteri di backup in modo che il backup dei dati venga eseguito in una pianificazione predeterminata.
* Creare copie indipendenti dei dati, che possono essere archiviati nel cloud hello e utilizzati per il ripristino di emergenza.

Questo articolo fornisce collegamenti tootutorials che descrivono gestione Snapshot StorSimple e come toouse è toocomplete flussi di lavoro e attività di amministrazione di sistema.

* Per ulteriori informazioni sull'architettura e i componenti di gestione Snapshot StorSimple, vedere [che cos'è Gestione Snapshot StorSimple?](storsimple-what-is-snapshot-manager.md) 
* toodownload StorSimple Snapshot Manager, andare troppo[pagina di download di gestione Snapshot StorSimple hello](https://www.microsoft.com/download/details.aspx?id=44220).
* Per le procedure di distribuzione di gestione Snapshot StorSimple, andare troppo[distribuire StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).

> [!NOTE]
> Non è possibile utilizzare toomanage gestione Snapshot StorSimple Microsoft Azure StorSimple Virtual Array (noto anche come StorSimple locale dispositivi virtuali).


## <a name="storsimple-snapshot-manager-tasks-and-workflows"></a>Flussi di lavoro e attività di gestione Snapshot StorSimple
È possibile utilizzare Gestione Snapshot StorSimple toomonitor hello e gestire i processi di backup correnti, pianificati e completati. Inoltre, gestione Snapshot StorSimple offre un catalogo di backup too64 completato. È possibile utilizzare toofind catalogo hello e ripristinare volumi o i singoli file. 

| Se si desidera tooDO THIS... | UTILIZZARE QUESTA ESERCITAZIONE... |
|:--- |:--- |
| Ulteriori informazioni su StorSimple Snapshot Manager |[Che cos’è Gestione snapshot StorSimple? ](storsimple-what-is-snapshot-manager.md) |
| Installare Gestione Snapshot StorSimple<br>Reinstallare StorSimple Snapshot Manager<br>rimuovere Gestione Snapshot StorSimple |[Distribuire Gestione snapshot StorSimple](storsimple-snapshot-manager-deployment.md) |
| Usare Gestione Snapshot StorSimple menu e funzionalità:<ul><li>Barra dei menu</li><li>Barra degli strumenti</li><li>Riquadro Ambito</li><li>Riquadro Risultati</li><li>Riquadro Azioni</li><li>Navigazione da tastiera e tasti di scelta rapida</li></ul> |[Interfaccia utente di gestione Snapshot StorSimple](storsimple-use-snapshot-manager.md) |
| Utilizzare hello comuni MMC funzionalità inclusa in Gestione Snapshot StorSimple:<ul><li>Visualizza</li><li>Nuova finestra da qui</li><li>Aggiorna</li><li>Esporta elenco</li><li>Guida</li></ul> |[Usare azioni di menu MMC hello in Gestione Snapshot StorSimple](storsimple-snapshot-manager-mmc-menu.md) |
| Aggiunta o sostituzione di un dispositivo<br>Collegare un dispositivo<br>Verificare i gruppi di volumi importati<br>Aggiornamento dei dispositivi connessi<br>Autenticazione di un dispositivo<br>Visualizzazione dei dettagli del dispositivo<br>Eliminazione della configurazione di un dispositivo<br>Modifica della password di un dispositivo<br>Sostituzione di un dispositivo guasto<br> |[Utilizzare Gestione Snapshot StorSimple tooconnect e gestire i dispositivi StorSimple](storsimple-snapshot-manager-manage-devices.md) |
| Montare i volumi<br>Visualizzare informazioni sui volumi<br>Eliminare un volume<br>Ripetere la scansione dei volumi<br>Configurare ed eseguire il backup di un volume di base<br>Configura e backup di un volume con mirroring dinamico |[Utilizzare Gestione Snapshot StorSimple tooview e gestire volumi](storsimple-snapshot-manager-manage-volumes.md) |
| Visualizzazione dei gruppi di volumi<br>Creare un gruppo di volumi<br>Eseguire il backup di un gruppo di volumi<br>Modificare un gruppo di volumi<br>Eliminare un gruppo di volumi |[Utilizzare Gestione Snapshot StorSimple toocreate e gestire gruppi di volumi](storsimple-snapshot-manager-manage-volume-groups.md) |
| Creare un criterio di backup <br>Modifica di un criterio di backup<br>Eliminare un criterio di backup |[Utilizzare Gestione Snapshot StorSimple toocreate e gestire i criteri di backup](storsimple-snapshot-manager-manage-backup-policies.md) |
| Visualizzare e gestire processi di backup pianificati<br>Visualizzare e gestire processi di backup recenti<br>visualizzazione e gestire processi di backup attualmente in esecuzione |[Utilizzare Gestione Snapshot StorSimple tooview e gestire i processi di backup](storsimple-snapshot-manager-manage-backup-jobs.md) |
| Ripristino di un volume<br>Clonazione di un volume o di un gruppo di volumi<br>Eliminazione di un backup<br>Recupero di un file<br>Ripristinare il database di gestione Snapshot StorSimple hello |[Catalogo di backup hello toomanage usare Gestione Snapshot StorSimple](storsimple-snapshot-manager-manage-backup-catalog.md) |

## <a name="next-steps"></a>Passaggi successivi
[Scaricare Gestione snapshot StorSimple](https://www.microsoft.com/download/details.aspx?id=44220).

