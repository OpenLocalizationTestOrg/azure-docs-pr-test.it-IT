---
title: i limiti di sistema serie 8000 aaaStorSimple | Documenti Microsoft
description: Descrive i limiti di sistema e le dimensioni consigliate per le connessioni e i componenti StorSimple serie 8000.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: c7392678-0924-46c6-9c59-1665cb9b6586
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 03/28/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: def89a2c1d0ddc71f1743e592c5112b09d72e971
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-storsimple-8000-series-system-limits"></a>Quali sono i limiti relativi al sistema StorSimple serie 8000?

## <a name="overview"></a>Panoramica

StorSimple fornisce una risorsa di archiviazione scalabile e flessibile per il datacenter. Esistono tuttavia alcuni limiti che è necessario tenere in considerazione quando si pianifica, distribuisce e utilizza una soluzione StorSimple. Hello nella tabella seguente vengono descritti questi limiti e fornisce alcuni suggerimenti, in modo che è possibile ottenere più hello fuori la soluzione StorSimple.

| Identificatore limite | Limite | Commenti |
| --- | --- | --- |
| Numero massimo di credenziali dell'account di archiviazione |64 | |
| Numero massimo di contenitori di volumi |64 | |
| Numero massimo di volumi |255 | |
| Numero massimo di volumi aggiunti in locale |32 | |
| Numero massimo di pianificazioni per ogni modello di larghezza di banda |168 |Una pianificazione per ogni ora, ogni giorno della settimana hello (24 * 7). |
| Dimensioni massime di un volume a livelli nei dispositivi fisici |64 TB per 8100 e 8600 |8100 e 8600 sono dispositivi fisici. |
| Dimensioni massime di un volume a livelli su dispositivi virtuali di Azure |30 TB per 8010  <br></br> 64 TB per 8020 |8010 e 8020 sono dispositivi virtuali di Azure che usano rispettivamente archiviazione Standard e Premium. |
| Dimensioni massime di un volume aggiunto in locale nei dispositivi fisici |8,5 TB per 8100 <br></br> 22.5 TB per 8600 |8100 e 8600 sono dispositivi fisici. |
| Numero massimo di connessioni iSCSI |512 | |
| Numero massimo di connessioni iSCSI dagli iniziatori |512 | |
| Numero massimo di record di controllo di accesso per dispositivo |64 | |
| Numero massimo di volumi per criteri di backup |20 | |
| Numero massimo di backup mantenuti per pianificazione (in un criterio di backup) |64 | |
| Numero massimo di pianificazioni per criteri di backup |10 | |
| Numero massimo di snapshot di qualsiasi tipo che è possibile mantenere per volume |256 |Questo numero include gli snapshot locali e quelli cloud. |
| Numero massimo di snapshot che possono essere presenti in qualsiasi dispositivo |10.000 | |
| Numero massimo di volumi che possono essere elaborati in parallelo per backup, ripristino o clonazione |16 |<ul><li>Se sono presenti più di 16 volumi, questi verranno elaborati in sequenza man mano che gli slot di elaborazione si rendono disponibili.</li><li>I nuovi backup di un duplicato o un volume a livelli ripristinato non può verificarsi fino a quando non hello operazione è stata completata. Per un volume locale, tuttavia, sono consentiti i backup dopo che il volume di hello è online.</li></ul> |
| Ripristino e clonazione del tempo di ripristino per volumi a livelli |< 2 minuti |<ul><li>volume Hello viene reso disponibile entro 2 minuti dell'operazione di ripristino o clonazione, indipendentemente dalle dimensioni del volume hello.</li><li>prestazioni del volume Hello inizialmente potrebbero essere più lente del normale come la maggior parte dei dati hello e i metadati si trova ancora nel cloud hello. Le prestazioni possono migliorare come flussi di dati dal dispositivo di StorSimple toohello cloud hello.</li><li>Hello tempo totale toodownload metadati dipende da hello dimensione volume allocata. I metadati vengono inseriti automaticamente nel dispositivo hello in background hello velocità hello di 5 minuti per TB di dati di volume allocato. Questa velocità può dipendere dal cloud toohello di larghezza di banda Internet.</li><li>ripristino di Hello o operazione di clonazione è completa quando tutti i metadati di hello sono sul dispositivo hello.</li><li>Non è possibile eseguire operazioni di backup fino al ripristino hello o operazione di clonazione è stata completata. |
| Ripristinare il tempo di ripristino per i volumi aggiunti in locale |< 2 minuti |<ul><li>volume Hello viene reso disponibile entro 2 minuti dell'operazione di ripristino hello, indipendentemente dalle dimensioni del volume hello.</li><li>prestazioni del volume Hello inizialmente potrebbero essere più lente del normale come la maggior parte dei dati hello e i metadati si trova ancora nel cloud hello. Le prestazioni possono migliorare come flussi di dati dal dispositivo di StorSimple toohello cloud hello.</li><li>Hello tempo totale toodownload metadati dipende da hello dimensione volume allocata. I metadati vengono inseriti automaticamente nel dispositivo hello in background hello velocità hello di 5 minuti per TB di dati di volume allocato. Questa velocità può dipendere dal cloud toohello di larghezza di banda Internet.</li><li>A differenza dei volumi a livelli, per i volumi aggiunti in locale, i dati di volume hello anche venga scaricati localmente nel dispositivo hello. operazione di ripristino Hello è completa quando tutti i dati di volume hello è stata portata toohello dispositivo.</li><li>le operazioni di ripristino Hello potrebbero essere lunghi. Hello tempo totale toocomplete hello ripristino dipende dalle dimensioni di hello del volume locale hello il provisioning, la larghezza di banda Internet e dati esistenti di hello sul dispositivo hello. Operazioni di backup nel volume aggiunto in locale hello sono consentite mentre l'operazione di ripristino hello è in corso. |
| Velocità di elaborazione per gli snapshot cloud |15 minuti/TB |<ul><li>Tempo minimo toomake hello snapshot cloud pronto per il caricamento, per ogni TB di dati del volume allocati nel backup. </li><li> Ora dello snapshot cloud totale viene calcolato aggiungendo questo tempo toohello snapshot tempo di caricamento, che è interessato dalla toocloud di larghezza di banda Internet hello. |
| Velocità effettiva di lettura/scrittura numero massimo di client (quando servita dal livello SSD hello) * |920/720 MB/s con una singola interfaccia di rete 10 GbE |Backup too2x con MPIO e due interfacce di rete. |
| Velocità effettiva di lettura/scrittura numero massimo di client (quando servita dal livello HDD hello) * |120/250 MB/s | |
| Velocità effettiva di lettura/scrittura numero massimo di client (quando servita dal livello cloud hello) * per Update 3 e versioni successive * * |40/60 MB/s per i volumi a livelli<br><br>60/80 MB/s per i volumi a livelli con opzione di archiviazione selezionata durante la creazione del volume |La velocità effettiva di lettura dipende dai client che generano e gestiscono una profondità della coda I/O sufficiente. <br><br>Velocità ottenuta dipende dalla velocità hello hello sottostante dell'account di archiviazione utilizzato. |

&#42; La velocità effettiva massima per ciascun tipo di I/O è stata misurata con scenari di scrittura al 100% e scenari di lettura al 100%. La velocità effettiva potrebbe essere inferiore a seconda delle condizioni della rete e della combinazione I/O.

&#42; &#42; Prestazioni numeri precedenti tooUpdate 3 può essere inferiore.

## <a name="next-steps"></a>Passaggi successivi
Hello revisione [requisiti di sistema StorSimple](storsimple-8000-system-requirements.md).

