---
title: Pannello riepilogo di aaaStorSimple Array virtuale dispositivo | Documenti Microsoft
description: "Descrive pannello riepilogo di hello dispositivo di gestione di dispositivi StorSimple e illustra come toouse, integrità hello toomonitor della matrice virtuale StorSimple."
services: storsimple
documentationcenter: 
author: manuaery
manager: syadav
editor: 
ms.assetid: a13c1ea7-6428-4234-84a6-0ebf51670a85
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/29/2016
ms.author: manuaery
ms.openlocfilehash: 3649eaac8a924a772f310a809ddf9706e912157a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-device-summary-blade-for-storsimple-device-manager-connected-toostorsimple-virtual-array"></a>Pannello di riepilogo dispositivo hello utilizzo di gestione di dispositivi StorSimple connesso tooStorSimple Array virtuale

## <a name="overview"></a>Panoramica

Pannello dispositivo di gestione di dispositivi StorSimple Hello fornisce un riepilogo di una matrice virtuale StorSimple registrato con un determinato StorSimple Manager di dispositivi, evidenziando i problemi dei dispositivi che richiedono attenzione da parte dell'amministratore di sistema. In questa esercitazione presenta Pannello di riepilogo dispositivo hello, spiega (funzione) e il contenuto di hello e vengono descritte le attività di hello che è possibile eseguire questo pannello.

Pannello riepilogo di Hello dispositivo Visualizza hello le seguenti informazioni:

![Pagina dashboard](./media/storsimple-virtual-array-device-summary/device-blade.png)



## <a name="management"></a>gestione

Nel pannello dispositivo di StorSimple hello, vedrai opzioni hello per la gestione del dispositivo StorSimple. Verranno visualizzati i comandi di gestione hello in alto di hello del pannello hello e sul lato sinistro di hello. Usare queste opzioni tooadd condivisioni o volumi, aggiornare o eseguire il failover l'array virtuale.

Hello area essentials acquisisce alcune delle proprietà importanti di hello, ad esempio, lo stato di hello, modello, versione del software, nonché toohello un collegamento **dell'interfaccia utente Web** della matrice hello. Se si utilizza una rete interna, è possibile avviare direttamente hello [interfaccia utente web locale](storsimple-ova-web-ui-admin.md) tooadminister l'array virtuale.

![Informazioni di base sui dispositivi](./media/storsimple-virtual-array-device-summary/device-essentials.png)

## <a name="storsimple-device-summary"></a>Riepilogo dispositivo StorSimple

* Hello **avvisi** riquadro fornisce uno snapshot di tutti gli avvisi attivi hello per l'array virtuale, raggruppato in base alla gravità dell'avviso. Fare clic su hello di hello riquadro tooopen **avvisi** blade e quindi fare clic su un singolo avviso tooview ulteriori dettagli sull'avviso, inclusi eventuali azioni consigliate. È inoltre possibile cancellare avviso hello se hello problema è stato risolto.

* Hello **capacità** riquadro Visualizza hello primario spazio di archiviazione viene eseguito il provisioning e rimanente in hello periferica virtuale toohello relativo spazio di archiviazione totale disponibile per hello stesso. **Il provisioning** fa riferimento toohello quantità di spazio di archiviazione preparata e allocata per l'utilizzo, **rimanente** fa riferimento toohello residua che è possibile effettuare il provisioning in questo dispositivo. Hello **a livelli rimanenti** capacità sia hello disponibile una capacità che è possibile effettuare il provisioning inclusi cloud, mentre hello **rimanenti locale** capacità hello rimanente su dischi hello collegato toothis virtuale matrice.

* In hello **utilizzo** grafico, è possibile visualizzare l'archiviazione primaria di hello usata tra l'array virtuale, nonché l'archiviazione cloud hello consumata in hello ultimi 7 giorni, il periodo di tempo predefinito di hello. Hello utilizzare **modifica** opzione nell'angolo superiore destro di hello di hello grafico toochoose una scala temporale diverso.

* Hello **condivisioni** o **volumi** riquadro fornisce un riepilogo del numero di hello delle condivisioni o volumi nel dispositivo raggruppati per stato. Fare clic su hello di hello riquadro tooopen **condivisioni** o **volumi** elenco pannello, quindi fare clic su un singolo tooview condivisione o volume o modificarne le proprietà. Per ulteriori informazioni, vedere come troppo[gestire condivisioni](storsimple-virtual-array-manage-shares.md) o [gestire volumi](storsimple-virtual-array-manage-volumes.md).

## <a name="next-steps"></a>Passaggi successivi
È possibile passare agli argomenti seguenti:
- [Gestire condivisioni su un array virtuale StorSimple](storsimple-virtual-array-manage-shares.md)
    
- [Gestire volumi su un array virtuale StorSimple](storsimple-virtual-array-manage-volumes.md)

