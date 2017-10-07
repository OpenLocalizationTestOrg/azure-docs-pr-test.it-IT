---
title: Aggiornamento 0,5 in StorSimple Virtual Array aaaInstall | Documenti Microsoft
description: Viene descritto come toouse hello Array virtuale StorSimple web aggiornamenti dell'interfaccia utente tooapply utilizzando hello Azure portale e l'aggiornamento rapido (metodo)
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/10/2017
ms.author: alkohli
ms.openlocfilehash: c38daa85daa0086e67cf0206d76cb19d9c8b21b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-update-05-on-your-storsimple-virtual-array"></a>Installare l'aggiornamento 0.5 nell'array virtuale StorSimple

## <a name="overview"></a>Panoramica

Questo articolo descrive hello passaggi necessari tooinstall aggiornamento 0,5 nell'Array virtuale StorSimple tramite l'interfaccia utente web locale hello e tramite hello portale di Azure. È necessario tooapply software aggiornamenti o hotfix tookeep l'Array virtuale StorSimple aggiornato.

Prima di applicare un aggiornamento, è consigliabile eseguire volumi hello o condivisioni offline in hello innanzitutto l'host e quindi hello dispositivo. Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati. Dopo aver hello volumi o condivisioni sono offline, è inoltre necessario eseguire il manuale di un backup del dispositivo hello.

> [!IMPORTANT]
> - Aggiornamento 0,5 corrisponde troppo**10.0.10290.0** versione del software nel dispositivo. Per informazioni sulle novità in questo aggiornamento, visitare troppo[note sulla versione di aggiornamento 0,5](storsimple-virtual-array-update-05-release-notes.md).
>
> - Se si esegue l'aggiornamento 0,2 o versioni successive, è consigliabile installare aggiornamenti hello tramite hello portale di Azure. Se si esegue l'aggiornamento 0,1 o versioni del software GA, è necessario utilizzare il metodo di aggiornamento rapido hello tramite tooinstall di interfaccia utente web locale hello aggiornamento 0,5.
>
> - Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo. Dato che hello Array virtuale StorSimple è un dispositivo singolo nodo, viene interrotta qualsiasi i/o in corso e il dispositivo si verifica nel tempo di inattività.

## <a name="use-hello-azure-portal"></a>Utilizzare hello portale di Azure

Se l'esecuzione di Update 0,2 e versioni successive, è consigliabile installare gli aggiornamenti tramite hello portale di Azure. procedure portale Hello richiede hello utente tooscan, scaricare e installare gli aggiornamenti di hello. Questa procedura accetta toocomplete circa 7 minuti. Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.

[!INCLUDE [storsimple-virtual-array-install-update-via-portal](../../includes/storsimple-virtual-array-install-update-via-portal-04.md)]

Dopo aver hello installazione è completata, passare tooyour servizio di gestione di dispositivi StorSimple. Selezionare **dispositivi** selezionare e fare clic su dispositivo hello hai appena aggiornato. Andare troppo**Impostazioni > Gestisci > gli aggiornamenti del dispositivo**. la versione software Hello visualizzato deve essere **10.0.10290.0**.

## <a name="use-hello-local-web-ui"></a>Utilizzare l'interfaccia utente web locale hello

Quando si utilizza l'interfaccia utente web locale hello, sono disponibili due passaggi:

* Scaricare l'aggiornamento di hello o un hotfix di hello
* Installare l'aggiornamento di hello o un hotfix di hello

### <a name="download-hello-update-or-hello-hotfix"></a>Scaricare l'aggiornamento di hello o un hotfix di hello

Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>hotfix di aggiornamento o hello hello toodownload

1. Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).

2. Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.

3. Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload. Immettere **4021576** per l'aggiornamento 0.5 e quindi fare clic su **Cerca**.
   
    Hello hotfix elenco viene visualizzato, ad esempio, **StorSimple Virtual Array aggiornamento 0,5**.
   
    ![Cercare nel catalogo](./media/storsimple-virtual-array-install-update-05/download1.png)

4. Fare clic su **Download**. 

5. Due toodownload di file, verrà visualizzato un *msu* e *CAB* file. Scaricare ciascun tali tooa cartella dei file. cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.

6. Aprire la cartella hello in cui si trovano i file hello.
    ![File di pacchetto hello](./media/storsimple-virtual-array-install-update-05/update05folder.png)

    Verranno visualizzati:
    -  Un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`. Questo file è un software di dispositivo hello tooupdate utilizzato.
    - Un file di pacchetto dell'agente di monitoraggio Geneva `GenevaMonitoringAgentPackageInstaller`. Questo file è utilizzato tooupdate hello monitoraggio e diagnostica (MDS) agente del servizio. Fare doppio clic sul file cab hello. Verrà visualizzato un file con estensione msi. File hello selezionare pulsante destro del mouse, quindi **estrarre** file hello. Si utilizzerà hello _con estensione msi_ agente hello tooupdate.

        ![Estrarre il file di aggiornamento dell'agente del servizio di monitoraggio e diagnostica (MDS)](./media/storsimple-virtual-array-install-update-05/extract-geneva-monitoring-agent-installer.png)
        
    

### <a name="install-hello-update-or-hello-hotfix"></a>Installare l'aggiornamento di hello o un hotfix di hello

Installazione di un hotfix o aggiornamento precedente toohello, assicurarsi che si dispone di hello aggiornamento o hotfix hello scaricato localmente nell'host o accessibile tramite una condivisione di rete.

Utilizzare questo metodo tooinstall Aggiorna su un dispositivo che esegue GA o aggiornare le versioni di software 0,1. Questa procedura richiede minore toocomplete 2 minuti. Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>hotfix di aggiornamento o hello hello tooinstall

1. In hello interfaccia utente web locale, andare troppo**manutenzione** > **aggiornamento Software**.
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update1m.png)

2. In **percorso del file di aggiornamento**, immettere il nome di file hello per l'aggiornamento di hello o hello hotfix. È inoltre possibile esplorare i file di installazione di un hotfix o aggiornamento toohello se inserito in una condivisione di rete. Fare clic su **Apply**.
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update2m.png)

3. Verrà visualizzato un avviso. Dato questo è un dispositivo singolo nodo, dopo che viene applicato l'aggiornamento di hello, hello dispositivo si riavvia e vi sia tempo di inattività. Fare clic sull'icona di controllo di hello.
   
   ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update3m.png)

4. avvio dell'aggiornamento Hello. Dopo aver completato l'aggiornamento dispositivo hello, viene riavviato. Hello dell'interfaccia utente locale non è accessibile in tale intervallo di tempo.
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update5m.png)

5. Dopo aver completato il riavvio di hello, che viene visualizzata toohello **Accedi** pagina. tooverify dispone di aggiornamento software per dispositivi hello nel web locale hello dell'interfaccia utente, andare troppo**manutenzione** > **aggiornamento Software**. la versione software Hello visualizzato deve essere **10.0.0.0.0.10290.0** per l'aggiornamento di 0,5.
   
   > [!NOTE]
   > I report versioni del software hello in modo leggermente diverso nell'interfaccia utente web locale hello hello portale di Azure. Ad esempio, hello report dell'interfaccia utente web locale **10.0.0.0.0.10290** e i report del portale Azure hello **10.0.10290.0** per hello stessa versione.
   
    ![aggiornamento dispositivo](./media/storsimple-virtual-array-install-update-05/update6m.png)

6. passaggio successivo Hello è l'agente tooupdate hello MDS. In hello **aggiornamento Software** pagina, visitare toohello **percorso del file di aggiornamento** ed esplorare toohello `GenevaMonitoringAgentPackageInstaller.msi` file. Ripetere i passaggi da 2 a 4. Dopo il riavvio di array virtuale hello, effettuano l'interfaccia utente web locale hello.

aggiornamento di Hello è stata completata.

## <a name="next-steps"></a>Passaggi successivi

Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

