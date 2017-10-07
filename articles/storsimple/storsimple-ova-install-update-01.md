---
title: aaaInstall aggiornamenti in un Array virtuale StorSimple | Documenti Microsoft
description: Viene descritto come toouse hello Array virtuale StorSimple web UI tooapply Aggiorna metodo hello portale e l'aggiornamento rapido
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: 7f1b1e7d-04d0-4ca2-9dbb-77077ff19bb9
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 09/07/2016
ms.author: alkohli
ms.openlocfilehash: 10af0f52abb75a5b41562704194157f0d35710bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-updates-on-your-storsimple-virtual-array"></a>Installare aggiornamenti nell'array virtuale StorSimple
## <a name="overview"></a>Panoramica
Questo articolo descrive hello passaggi tooinstall necessari aggiornamenti sull'Array virtuale StorSimple tramite l'interfaccia utente web locale hello e tramite hello portale di Azure classico. È necessario tooapply software aggiornamenti o hotfix tookeep l'Array virtuale StorSimple aggiornato. 

Tenere presente che l'installazione di un aggiornamento o un hotfix potrebbe riavviare il dispositivo. Dato che hello Array virtuale StorSimple è un dispositivo singolo nodo, viene interrotta qualsiasi i/o in corso e il dispositivo si verifica nel tempo di inattività. 

Prima di applicare un aggiornamento, è consigliabile eseguire volumi hello o condivisioni offline in hello innanzitutto l'host e quindi hello dispositivo. Questa operazione consente di eliminare qualsiasi rischio di danneggiamento dei dati.

> [!IMPORTANT]
> Se si esegue l'aggiornamento 0,1 o versioni del software GA, è necessario utilizzare il metodo di aggiornamento rapido hello tramite l'aggiornamento di tooinstall dell'interfaccia utente web locale hello 0,3. Se si esegue l'aggiornamento 0,2, è consigliabile installare gli aggiornamenti di hello tramite hello portale di Azure classico.
> 
> 

## <a name="use-hello-local-web-ui"></a>Utilizzare l'interfaccia utente web locale hello
Quando si utilizza l'interfaccia utente web locale hello, sono disponibili due passaggi:

* Scaricare l'aggiornamento di hello o un hotfix di hello
* Installare l'aggiornamento di hello o un hotfix di hello

### <a name="download-hello-update-or-hello-hotfix"></a>Scaricare l'aggiornamento di hello o un hotfix di hello
Eseguire hello dopo l'aggiornamento software di passaggi toodownload hello da hello Microsoft Update Catalog.

#### <a name="toodownload-hello-update-or-hello-hotfix"></a>hotfix di aggiornamento o hello hello toodownload
1. Avviare Internet Explorer e passare troppo[http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).
2. Se questa è la prima volta tramite Microsoft Update Catalog hello in questo computer, fare clic su **installare** quando richiesta tooinstall hello componente aggiuntivo di Microsoft Update Catalog.
3. Nella casella di ricerca hello di hello Microsoft Update Catalog, immettere il numero di articolo della Knowledge Base (KB) hello di hotfix hello desiderato toodownload. Digitare **3182061** per l'aggiornamento 0.3, quindi fare clic su **Cerca**.
   
    Hello hotfix elenco viene visualizzato, ad esempio, **StorSimple Virtual Array aggiornamento 0.3**.
   
    ![Cercare nel catalogo](./media/storsimple-ova-install-update-01/download1.png)
4. Fare clic su **Aggiungi**. aggiornamento di Hello viene aggiunto toohello carrello.
5. Fare clic su **Visualizza carrello**.
6. Fare clic su **Download**. Specificare o **Sfoglia** tooa percorso locale in cui si desidera hello Scarica tooappear. Hello gli aggiornamenti vengono scaricati toohello percorso specificato e inserito in una sottocartella con stesso nome come aggiornamento hello hello. cartella Hello può essere copiati tooa condivisione di rete che sia raggiungibile dal dispositivo hello.
7. Aprire hello copiati cartella, dovrebbe essere un file di pacchetto autonomo Microsoft Update `WindowsTH-KB3011067-x64`. Questo file è un hotfix o aggiornamento hello tooinstall utilizzato.

### <a name="install-hello-update-or-hello-hotfix"></a>Installare l'aggiornamento di hello o un hotfix di hello
Installazione di un hotfix o aggiornamento precedente toohello, assicurarsi che si dispone di hello aggiornamento o hotfix hello scaricato localmente nell'host o accessibile tramite una condivisione di rete. 

Utilizzare questo metodo tooinstall Aggiorna su un dispositivo che esegue GA o aggiornare le versioni di software 0,1. Questa procedura richiede minore toocomplete 2 minuti. Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.

#### <a name="tooinstall-hello-update-or-hello-hotfix"></a>hotfix di aggiornamento o hello hello tooinstall
1. In hello interfaccia utente web locale, andare troppo**manutenzione** > **aggiornamento Software**.
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update1m.png)
2. In **percorso del file di aggiornamento**, immettere il nome di file hello per l'aggiornamento di hello o hello hotfix. È inoltre possibile esplorare i file di installazione di un hotfix o aggiornamento toohello se inserito in una condivisione di rete. Fare clic su **Apply**.
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update2m.png)
3. Verrà visualizzato un avviso. Dato questo è un dispositivo singolo nodo, dopo che viene applicato l'aggiornamento di hello, hello dispositivo si riavvia e vi sia tempo di inattività. Fare clic sull'icona di controllo di hello.
   
   ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update3m.png)
4. avvio dell'aggiornamento Hello. Dopo aver completato l'aggiornamento dispositivo hello, viene riavviato. Hello dell'interfaccia utente locale non è accessibile in tale intervallo di tempo.
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update5m.png)
5. Dopo aver completato il riavvio di hello, che viene visualizzata toohello **Accedi** pagina. tooverify dispone di aggiornamento software per dispositivi hello nel web locale hello dell'interfaccia utente, andare troppo**manutenzione** > **aggiornamento Software**. la versione software Hello visualizzato deve essere **10.0.0.0.0.10288.0** per l'aggiornamento 0.3.
   
   > [!NOTE]
   > I report versioni del software hello in modo leggermente diverso nell'interfaccia utente web locale hello hello portale di Azure classico. Ad esempio, hello report dell'interfaccia utente web locale **10.0.0.0.0.10288** e i report del portale di Azure classici hello **10.0.10288.0** per hello stessa versione. 
   > 
   > 
   
    ![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/update6m.png)

## <a name="use-hello-azure-classic-portal"></a>Utilizzare hello portale di Azure classico
Se l'esecuzione di Update 0,2, è consigliabile installare gli aggiornamenti tramite hello portale di Azure classico. procedure portale Hello richiede hello utente tooscan, scaricare e installare gli aggiornamenti di hello. Questa procedura accetta toocomplete circa 7 minuti. Eseguire l'esempio hello passaggi tooinstall hello aggiornamento o un hotfix.

[!INCLUDE [storsimple-ova-install-update-via-portal](../../includes/storsimple-ova-install-update-via-portal.md)]

Hello dopo l'installazione è stata completata (come indicato in base allo stato di processo al 100%), andare troppo**dispositivi > manutenzione > gli aggiornamenti Software**. versione del software Hello visualizzato deve essere 10.0.10288.0.

![aggiornamento dispositivo](./media/storsimple-ova-install-update-01/azupdate12m.png)

## <a name="next-steps"></a>Passaggi successivi
Scoprire di più su come [amministrazione StorSimple Virtual Array](storsimple-ova-web-ui-admin.md).

