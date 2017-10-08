---
title: "Verificare l'unità d: di una macchina virtuale un disco dati hello | Documenti Microsoft"
description: "Descrive la modalità di lettere di unità toochange per una macchina virtuale Windows in modo che è possibile utilizzare l'unità d: hello come un'unità dati."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 0867a931-0055-4e31-8403-9b38a3eeb904
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/31/2017
ms.author: cynthn
ms.openlocfilehash: 43939da1a890ac4049266487951e3889aa0ed9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-d-drive-as-a-data-drive-on-a-windows-vm"></a>Utilizzare l'unità d: hello come un'unità di dati in una macchina virtuale Windows
Se l'applicazione deve hello toouse dati toostore di unità D, seguire questi toouse istruzioni una lettera di unità diversa per il disco temporaneo hello. Non utilizzare mai hello disco temporaneo toostore che i dati necessari tookeep.

Se si ridimensiona o **arresto (deallocazione)** una macchina virtuale, si può attivare la selezione di hello macchina virtuale tooa nuovo hypervisor. Tale posizionamento può attivare un evento di manutenzione pianificato o non pianificato. In questo scenario, il disco temporaneo hello sarà toohello riassegnati prima lettera di unità disponibili. Se si dispone di un'applicazione che richiede l'unità d: hello in particolare, è necessario toofollow questi passaggi tootemporarily spostamento hello pagefile.sys, collegare un nuovo disco dati e assegnargli hello lettera D e spostamento hello pagefile.sys unità temporanea toohello di eseguire il backup. Una volta completato, Azure non porterà hello d: se hello VM si sposta tooa diversi hypervisor.

Per ulteriori informazioni sull'utilizzo disco temporaneo hello in Azure, vedere [informazioni sulle unità temporanea hello in macchine virtuali di Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="attach-hello-data-disk"></a>Collegare il disco dati hello
In primo luogo, è necessario tooattach hello macchina virtuale di dati su disco toohello. toodo questo tramite il portale di hello, vedere [come disco di tooattach dati gestiti nel portale di Azure hello](attach-managed-disk-portal.md).

## <a name="temporarily-move-pagefilesys-tooc-drive"></a>Spostare pagefile.sys tooC unità
1. Connessione macchina virtuale toohello. 
2. Pulsante destro del mouse hello **avviare** dal menu **sistema**.
3. Nel menu a sinistra di hello, selezionare **impostazioni di sistema avanzate**.
4. In hello **prestazioni** selezionare **impostazioni**.
5. Seleziona hello **avanzate** scheda.
6. In hello **memoria virtuale** selezionare **modifica**.
7. Seleziona hello **C** unità e quindi fare clic su **dimensioni gestite dal sistema** e quindi fare clic su **impostare**.
8. Seleziona hello **D** unità e quindi fare clic su **Nessun file di paging** e quindi fare clic su **impostare**.
9. Fare clic su Applica. Verrà visualizzato un avviso che computer hello deve toobe riavviare hello modifiche tootake effetto.
10. Riavviare la macchina virtuale hello.

## <a name="change-hello-drive-letters"></a>Le lettere di unità hello
1. Una volta hello riavvio della macchina virtuale, eseguire nuovamente l'accesso toohello macchina virtuale.
2. Fare clic su hello **avviare** menu e il tipo **diskmgmt.msc** e premere INVIO. Verrà avviato Gestione disco.
3. Fare clic su **D**, unità di archiviazione temporanea di hello e selezionare **Cambia lettera di unità e percorsi**.
4. In Lettera unità selezionare una nuova unità, ad esempio **T**, e quindi fare clic su **OK**. 
5. Fare clic sul disco dati hello e selezionare **Cambia lettera di unità e percorsi**.
6. In Lettera unità selezionare l'unità **D** e quindi fare clic su **OK**. 

## <a name="move-pagefilesys-back-toohello-temporary-storage-drive"></a>Spostare pagefile.sys unità di archiviazione temporanea toohello indietro
1. Pulsante destro del mouse hello **avviare** dal menu **sistema**
2. Nel menu a sinistra di hello, selezionare **impostazioni di sistema avanzate**.
3. In hello **prestazioni** selezionare **impostazioni**.
4. Seleziona hello **avanzate** scheda.
5. In hello **memoria virtuale** selezionare **modifica**.
6. Selezionare l'unità del sistema operativo hello **C** e fare clic su **Nessun file di paging** e quindi fare clic su **impostare**.
7. Selezionare l'unità di archiviazione temporanea hello **T** e quindi fare clic su **dimensioni gestite dal sistema** e quindi fare clic su **impostare**.
8. Fare clic su **Apply**. Verrà visualizzato un avviso che computer hello deve toobe riavviare hello modifiche tootake effetto.
9. Riavviare la macchina virtuale hello.

## <a name="next-steps"></a>Passaggi successivi
* È possibile aumentare hello archiviazione tooyour disponibili per macchina virtuale [collegando un disco dati aggiuntivo](attach-managed-disk-portal.md).

