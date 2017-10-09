---
title: macchine virtuali di Windows Azure aaaBackup | Microsoft documenti
description: Proteggere le macchine virtuali Windows eseguendo il backup con Backup di Azure.
services: virtual-machines-windows
documentationcenter: virtual-machines
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/27/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 1cd3e1940a83aacd160cba3c8613b63b6f3c11d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-virtual-machines-in-azure"></a>Eseguire il backup di macchine virtuali Windows in Azure

È possibile proteggere i dati eseguendo backup a intervalli regolari. Backup di Azure crea punti di recupero che vengono archiviati negli insiemi di credenziali di ripristino con ridondanza geografica. Quando si ripristina da un punto di ripristino, è possibile ripristinare hello intera macchina virtuale o a specifici file. Questo articolo viene illustrato come toorestore un singolo file tooa macchina virtuale che esegue Windows Server e IIS. Se si dispone già di un toouse VM, è possibile crearne uno utilizzando hello [Guida introduttiva a Windows](quick-create-portal.md). In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Creare un backup di una macchina virtuale
> * Pianificare un backup giornaliero
> * Ripristinare un file da un backup




## <a name="backup-overview"></a>Panoramica del servizio Backup

Quando hello servizio Backup di Azure avvia un processo di backup, attiva hello estensione backup tootake uno snapshot del punto nel tempo. Hello servizio Azure Backup utilizza hello _VMSnapshot_ estensione. estensione Hello viene installato durante il backup di VM prima hello se hello macchina virtuale è in esecuzione. Se hello VM non è in esecuzione, il servizio di Backup hello crea uno snapshot di hello archiviazione sottostante (poiché non scritte dall'applicazione si verificano durante hello che macchina virtuale è stato arrestato).

Quando si acquisisce uno snapshot delle macchine virtuali di Windows, il servizio di Backup hello interagisce con hello del servizio Copia Shadow del Volume (VSS) tooget uno snapshot coerenza dei dischi della macchina virtuale hello. Una volta hello servizio Azure Backup istantanea hello, dati hello sono toohello trasferite insieme di credenziali. l'efficienza toomaximize servizio hello identifica e i trasferimenti di dati che sono stati modificati dal backup precedente hello solo i blocchi hello.

Una volta completato il trasferimento dei dati di hello, snapshot hello viene rimosso e viene creato un punto di ripristino.


## <a name="create-a-backup"></a>Creare un backup
Creare un semplice pianificata giornaliera backup tooa insieme di credenziali di servizi di ripristino. 

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Dal menu hello hello sinistra, selezionare **macchine virtuali**. 
3. Dall'elenco di hello, selezionare una macchina virtuale tooback backup.
4. Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**. Hello **Abilita backup** apre blade.
5. In **insieme di credenziali di servizi di ripristino**, fare clic su **Crea nuovo** e specificare il nome di hello per nuovo insieme di credenziali hello. Viene creato un nuovo insieme di credenziali in hello stesso gruppo di risorse e il percorso come macchina virtuale hello.
6. Fare clic su **Criterio di Backup**. Per questo esempio, mantenere i valori predefiniti di hello e fare clic su **OK**.
7. In hello **Abilita backup** pannello, fare clic su **Abilita Backup**. Verrà creato un backup giornaliero in base alla pianificazione predefinita hello.
10. un punto di ripristino iniziale, su hello toocreate **Backup** fare clic su pannello **Backup ora**.
11. In hello **Esegui Backup** pannello, fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.
12. In hello **Backup** pannello per la macchina virtuale, viene visualizzato un numero di punti di ripristino che sono state completate hello.

    ![Punti di ripristino](./media/tutorial-backup-vms/backup-complete.png)
    
il primo backup di Hello richiede circa 20 minuti. Al termine del backup, procedere toohello parte successiva di questa esercitazione.

## <a name="recover-a-file"></a>Recupero di un file

Se accidentalmente si elimina o si apporta modifiche tooa file, è possibile utilizzare file di ripristino di File toorecover hello dall'insieme di credenziali di backup. Ripristino di file usa uno script eseguito nella macchina virtuale, hello toomount hello di punto di ripristino come unità locale. Queste unità rimarrà montate per 12 ore in modo che è possibile copiare i file dal punto di ripristino hello e ripristinarli toohello macchina virtuale.  

In questo esempio, ecco come toorecover hello file di immagine che viene utilizzata nella pagina web predefinita di hello per IIS. 

1. Aprire un browser e connettersi toohello di indirizzo IP della pagina di hello VM tooshow hello predefinita IIS.

    ![Pagina Web IIS predefinita](./media/tutorial-backup-vms/iis-working.png)

2. Connettersi toohello macchina virtuale.
3. In hello macchina virtuale, aprire **Esplora File** e passare too\inetpub\wwwroot ed eliminare file hello **iisstart.png**.
4. Nel computer locale, l'aggiornamento hello browser toosee che hello immagine nella pagina IIS predefinita hello venga rimossa.

    ![Pagina Web IIS predefinita](./media/tutorial-backup-vms/iis-broken.png)

5. Nel computer locale, aprire una nuova scheda e hello hello passare [portale di Azure](https://portal.azure.com).
6. Dal menu hello hello sinistra, selezionare **macchine virtuali** e selezionare hello VM modulo hello elenco.
8. Nel pannello VM hello in hello **impostazioni** fare clic su **Backup**. Hello **Backup** apre blade. 
9. Nel menu di hello nella parte superiore di hello del pannello hello, selezionare **ripristino File**. Hello **ripristino File** apre blade.
10. In **passaggio 1: selezionare il punto di ripristino**, selezionare un punto di ripristino dall'elenco a discesa hello.
11. In **passaggio 2: scaricare script toobrowse e recuperare i file**, fare clic su hello **scaricare eseguibile** pulsante. Salvare hello file tooyour **Scarica** cartella.
12. Nel computer locale, aprire **Esplora File** e passare tooyour **Scarica** hello cartella e copia scaricato file .exe. nome file Hello è preceduto dal nome macchina virtuale. 
13. La macchina virtuale (sulla connessione RDP hello) incollare hello .exe file toohello Desktop della macchina virtuale. 
14. Passare toohello desktop della macchina virtuale e fare doppio clic su .exe hello. Verrà avviato un prompt dei comandi e quindi montare il punto di ripristino hello come condivisione file che è possibile accedere. Al termine Crea condivisione hello, digitare **q** tooclose hello il prompt dei comandi.
15. Nella macchina virtuale, aprire **Esplora File** e passare toohello lettera di unità utilizzata per la condivisione di file hello.
16. Passare too\inetpub\wwwroot e copia **iisstart.png** dal file hello condividere e incollarlo in \Inetpub\Wwwroot.. Ad esempio, copiare F:\inetpub\wwwroot\iisstart.png e incollarlo nel file di c:\inetpub\wwwroot toorecover hello.
17. Nel computer locale, aprire scheda del browser hello in cui si è connessi toohello di indirizzo IP della pagina predefinita di hello VM con hello IIS. Premere CTRL + F5 pagina nel browser toorefresh hello. Si noterà ora che hello immagine è stata ripristinata.
18. Nel computer locale, tornare indietro toohello per hello portale di Azure e nella scheda del browser **passaggio 3: smontare dischi hello dopo il ripristino** fare clic su hello **smontare dischi** pulsante. Se si dimentica toodo questo passaggio, punto di montaggio toohello hello connessione è chiusa automaticamente dopo 12 ore. Dopo queste 12 ore, è necessario toodownload un nuovo toocreate script un nuovo punto di montaggio.


## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Creare un backup di una macchina virtuale
> * Pianificare un backup giornaliero
> * Ripristinare un file da un backup

Spostare toohello toolearn esercitazione successiva sul monitoraggio delle macchine virtuali.

> [!div class="nextstepaction"]
> [Monitorare le macchine virtuali](tutorial-monitoring.md)









