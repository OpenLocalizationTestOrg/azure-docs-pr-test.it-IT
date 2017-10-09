---
title: aaaProvision StorSimple Array virtuale in Hyper-V | Documenti Microsoft
description: Questa seconda esercitazione sulla distribuzione di array virtuali StorSimple implica il provisioning di un array virtuale in Hyper-V.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 4354963c-e09d-41ac-9c8b-f21abeae9913
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f47d642f740827ae1440b819e07067c6a183527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-hyper-v"></a>Distribuire StorSimple Virtual Array: eseguire il provisioning in Hyper-V
![](./media/storsimple-virtual-array-deploy2-provision-hyperv/hyperv4.png)

## <a name="overview"></a>Panoramica
In questa esercitazione viene descritto come tooprovision una virtuale StorSimple di matrice in un sistema host in esecuzione Hyper-V in Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. Questo articolo riguarda la distribuzione di toohello di matrici virtuale StorSimple nel portale di Azure e Cloud di Microsoft Azure per enti pubblici.

È necessario tooprovision privilegi di amministratore e configurare un array virtuale. l'installazione iniziale e provisioning Hello può richiedere circa 10 minuti toocomplete.

## <a name="provisioning-prerequisites"></a>Prerequisiti di provisioning
Qui noterai hello prerequisiti tooprovision un array virtuale in un sistema host in esecuzione Hyper-V in Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2.

### <a name="for-hello-storsimple-device-manager-service"></a>Per il servizio di gestione di dispositivi StorSimple hello
Prima di iniziare, verificare che:

* Sono stati completati tutti i passaggi di hello in [portale hello preparazione per Array virtuale StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* È stato scaricato l'immagine array virtuale hello per Hyper-V da hello portale di Azure. Per ulteriori informazioni, vedere **passaggio 3: immagine di Download hello array virtuale** di [portale hello preparazione per la Guida di StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

  > [!IMPORTANT]
  > software Hello in esecuzione su hello Array virtuale StorSimple può essere utilizzato solo con il servizio di gestione di dispositivi StorSimple hello.
  >
  >

### <a name="for-hello-storsimple-virtual-array"></a>Per hello Array virtuale StorSimple
Prima di distribuire un array virtuale, è necessario:

* Si dispone di accesso tooa host sistema che esegue Hyper-V in Windows Server 2008 R2 o versioni successive che può essere utilizzato tooa effettuare il provisioning di un dispositivo.
* sistema host Hello è in grado di toodedicate hello seguenti risorse tooprovision l'array virtuale:

  * Un minimo di 4 memorie centrali.
  * Almeno 8 GB di RAM. Se si prevede di tooconfigure hello virtual array file server, 8 GB supporta i file meno di 2 milioni. 16 GB RAM toosupport 2-4 milioni file necessari.
  * Un'interfaccia di rete.
  * Un disco virtuale da 500 GB per i dati.

### <a name="for-hello-network-in-hello-datacenter"></a>Per la rete hello in Data Center hello
Prima di iniziare, esaminare hello requisiti toodeploy un Array virtuale StorSimple di rete e configurare la rete di Data Center hello in modo appropriato. Per altre informazioni, vedere [Requisiti di sistema StorSimple Virtual Array](storsimple-ova-system-requirements.md#networking-requirements).

## <a name="step-by-step-provisioning"></a>Provisioning passo per passo
tooprovision e connessione array virtuale tooa, è necessario hello tooperform alla procedura seguente:

1. Verificare che il sistema di host hello sufficienti risorse toomeet hello minimo array virtuale requisiti.
2. Eseguire il provisioning di un array virtuale in hypervisor.
3. Avviare array virtuale hello e ottenere l'indirizzo IP hello.

Ognuno di questi passaggi è illustrato in hello le sezioni seguenti.

## <a name="step-1-ensure-that-hello-host-system-meets-minimum-virtual-array-requirements"></a>Passaggio 1: Verificare che il sistema di host hello soddisfi i requisiti minimi array virtuale
toocreate un array virtuale, è necessario:

* ruolo di Hello Hyper-V installato in Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2 SP1.
* Microsoft Hyper-V Manager in un client di Microsoft Windows connesso toohello host.

Verificare che tale hello sottostante hardware (sistema host) in cui si sta creando una matrice virtuale hello è in grado di toodedicate hello array virtuale tooyour di risorse seguenti:

* Un minimo di 4 memorie centrali.
* Almeno 8 GB di RAM. Se si prevede di tooconfigure hello virtual array file server, 8 GB supporta i file meno di 2 milioni. 16 GB RAM toosupport 2-4 milioni file necessari.
* Un'interfaccia di rete.
* Un disco virtuale da 500 GB per i dati di sistema.

## <a name="step-2-provision-a-virtual-array-in-hypervisor"></a>Passaggio 2: Eseguire il provisioning di un array virtuale in hypervisor
Eseguire i seguenti passaggi tooprovision un dispositivo nell'hypervisor hello.

#### <a name="tooprovision-a-virtual-array"></a>tooprovision un array virtuale
1. Nell'host Windows Server, copiare l'unità locale tooa hello array virtuale immagine. Questa immagine (file VHD o VHDX) è stato scaricato tramite hello portale di Azure. Prendere nota del percorso hello in cui è stata copiata hello immagine quando si utilizza questa immagine in un secondo momento nella procedura di hello.
2. Aprire **Server Manager**. In hello angolo superiore destro, fare clic su **strumenti** e selezionare **Hyper-V Manager**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image1.png)  

   Se si esegue Windows Server 2008 R2, aprire hello Hyper-V Manager. In Server Manager fare clic su **Ruoli > Hyper-V > Console di gestione di Hyper-V**.
3. In **gestione di Hyper-V**, nel riquadro ambito hello, fare doppio clic su del menu contestuale del sistema nodo tooopen hello e quindi fare clic su **New** > **macchina virtuale**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image2.png)
4. In hello **prima di iniziare** fare clic su pagina della creazione guidata macchina virtuale, hello **Avanti**.
5. In hello **specificare nome e percorso** pagina, fornire un **nome** per l'array virtuale. Fare clic su **Avanti**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image4.png)
6. In hello **specificare generazione** pagina Scegli tipo di immagine dispositivo hello e quindi fare clic su **Avanti**. Se si usa Windows Server 2008 R2, questa pagina non verrà visualizzata.

   * Se è stata scaricata un'immagine VHDX per Windows Server 2012 o versione successiva, scegliere **Generazione 2** .
   * Se è stata scaricata un'immagine VHD per Windows Server 2008 R2 o versione successiva, scegliere **Generazione 1** .

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image5.png)
7. In hello **assegnazione memoria** , specificare un **memoria di avvio** di almeno **MB 8192**, non abilitare la memoria dinamica e quindi fare clic su **Avanti**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image6.png)  
8. In hello **Configura rete** pagina, specificare hello commutatore virtuale connesso toohello Internet e quindi fare clic su **Avanti**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image7.png)
9. In hello **connessione disco rigido virtuale** pagina, scegliere **utilizzare un disco rigido virtuale esistente**, specificare il percorso di hello dell'immagine di hello array virtuale (vhdx o VHD) e quindi fare clic su **Avanti**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image8m.png)
10. Hello revisione **riepilogo** e quindi fare clic su **fine** macchina virtuale di toocreate hello.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image9.png)
11. requisiti minimi di hello toomeet, è necessario 4 core. tooadd 4 processori virtuali, selezionare il sistema host in hello **Hyper-V Manager** finestra. Nel riquadro di destra hello in elenco hello di **macchine virtuali**, individuare una macchina virtuale hello appena creato. Selezionare e fare doppio clic su nome computer hello e selezionare **impostazioni**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image10.png)
12. In hello **impostazioni** in hello riquadro di sinistra fare clic su **processore**. Nel riquadro a destra hello, impostare **numero di processori virtuali** too4 (o più). Fare clic su **Apply**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image11.png)
13. requisiti minimi di hello toomeet, è necessario anche tooadd un disco dati virtuale da 500 GB. In hello **impostazioni** pagina:

    1. Nel riquadro sinistro hello selezionare **Controller SCSI**.
    2. Nel riquadro di destra hello, selezionare **unità disco rigido,** e fare clic su **Aggiungi**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image12.png)
14. In hello **unità disco rigido** pagina, seleziona hello **disco rigido virtuale** opzione e fare clic su **New**. Hello **Creazione guidata disco rigido virtuale** viene avviato.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image13.png)
15. In hello **prima di iniziare** fare clic su pagina della creazione guidata disco rigido virtuale, hello **Avanti**.
16. In hello **pagina Selezione formato disco**, accettare l'opzione predefinita hello **VHDX** formato. Fare clic su **Avanti**. Se si esegue Windows Server 2008 R2, questa schermata non viene visualizzata.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image15.png)
17. In hello **pagina Selezione tipo di disco**, impostare il tipo di disco rigido virtuale come **ad espansione dinamica** (scelta consigliata). **Dimensioni fisse** disco funzionerà ma toowait potrebbe essere necessario molto tempo. È consigliabile non utilizzare hello **differenze** opzione. Fare clic su **Avanti**. In Windows Server 2012 R2 e Windows Server 2012, **ad espansione dinamica** è l'opzione predefinita hello mentre in Windows Server 2008 R2, hello è **dimensioni fisse**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image16.png)
18. In hello **impostazione nome e percorso** pagina, fornire un **nome** nonché **percorso** (è possibile esplorare tooone) per il disco dati hello. Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image17.png)
19. In hello **configurazione disco** pagina opzione hello selezionare **creare un nuovo disco rigido virtuale vuoto** e specificare le dimensioni di hello come **500 GB** (o più). Mentre 500 GB è il requisito minimo di hello, è sempre possibile eseguire il provisioning di un disco più grande. Si noti che non è possibile espandere o compattare il disco di hello una volta eseguito il provisioning. Per ulteriori informazioni sulle dimensioni hello tooprovision disco, nella sezione hello ridimensionamento in hello [documento di best practices](storsimple-ova-best-practices.md). Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image18.png)
20. In hello **riepilogo** pagina, esaminare i dettagli di hello del disco dati virtuale e se soddisfatti, fare clic su **fine** disco hello toocreate. procedura guidata Hello e un disco rigido virtuale viene aggiunto tooyour macchina.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image19.png)
21. Restituire toohello **impostazioni** pagina. Fare clic su **OK** tooclose hello **impostazioni** pagina e restituire finestra Gestione tooHyper-V.

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image20.png)

## <a name="step-3-start-hello-virtual-array-and-get-hello-ip"></a>Passaggio 3: Avviare array virtuale hello e ottenere l'indirizzo IP di hello
Eseguire hello seguendo i passaggi toostart l'array virtuale e connettersi tooit.

#### <a name="toostart-hello-virtual-array"></a>Matrice di toostart hello virtuale
1. Avviare array virtuale hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image21.png)
2. Quando il dispositivo hello è in esecuzione, selezionare il dispositivo di hello, fare clic e selezionare **Connetti**.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image22.png)
3. È possibile toowait 5-10 minuti per hello dispositivo toobe pronto. Viene visualizzato un messaggio di stato sullo stato di avanzamento hello tooindicate console hello. Quando il dispositivo hello è pronto, andare troppo**azione**. Premere `Ctrl + Alt + Delete` toolog toohello virtuale matrice. utente predefinito Hello *StorSimpleAdmin* e la password predefinita hello è *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image23.png)
4. Per motivi di sicurezza, password amministratore del dispositivo hello scade al primo accesso hello. Si è password hello toochange richiesta.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image24.png)

   Immettere una password contenente almeno 8 caratteri. Hello password deve soddisfare almeno 3 fuori hello 4 requisiti seguenti: caratteri maiuscoli, minuscoli, numerici e speciali. Immettere nuovamente tooconfirm password hello è. Notifica che la password hello è stato modificato.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image25.png)
5. Dopo che la password di hello viene modificata, potrebbe essere riavviato array virtuale hello. Attendere toostart dispositivo hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image26.png)

    console di Windows PowerShell Hello del dispositivo hello viene visualizzata insieme a un indicatore di stato.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image27.png)
6. I passaggi da 6 a 8 si applicano solo all'avvio in un ambiente non DHCP. Se si dispone di un ambiente di DHCP, quindi ignorare questi passaggi e passare toostep 9. Se il dispositivo nell'ambiente di DHCP non è avviato, verrà visualizzato hello seguente schermata.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image28m.png)

    Successivamente, configurare la rete hello.
7. Hello utilizzare `Get-HcsIpAddress` comando interfacce di rete hello toolist attivate l'array virtuale. Se il dispositivo dispone di una singola interfaccia di rete abilitata, interfaccia toothis di hello predefinita nome assegnato è `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image29m.png)
8. Hello utilizzare `Set-HcsIpAddress` rete hello tooconfigure di cmdlet. Vedere hello di esempio seguente:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image30.png)
9. Dopo aver completata la configurazione iniziale di hello e dispositivo hello è avviato, verrà visualizzato testo dell'intestazione dispositivo hello. Prendere nota dell'indirizzo IP hello e hello URL visualizzato nel dispositivo di hello banner testo toomanage hello. Utilizzare questa web di toohello tooconnect indirizzo IP dell'interfaccia utente di array virtuale e l'installazione locale completa hello e di registrazione.

   ![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image31m.png)
10. (Facoltativo) Eseguire questo passaggio solo se si distribuisce il dispositivo in hello Government Cloud. È ora verrà abilitare la modalità di Stati Uniti elaborazione Standard FIPS (Federal Information) hello sul dispositivo. standard di Hello FIPS 140 definisce gli algoritmi di crittografia approvati per l'utilizzo dai sistemi di computer governo federale US per la protezione dei dati sensibili hello.

    1. modalità FIPS di hello di tooenable, eseguire hello seguente cmdlet:

        `Enable-HcsFIPSMode`
    2. Dopo aver attivato la modalità FIPS hello in modo che le convalide di crittografia hello abbiano effetto, riavviare il dispositivo.

       > [!NOTE]
       > È possibile abilitare o disabilitare la modalità FIPS sul dispositivo. Dispositivo hello alternarsi tra la modalità FIPS e non FIPS non è supportata.
       >
       >

Se il dispositivo non soddisfa i requisiti minimi delle configurazioni di hello, viene visualizzato il seguente errore nel testo dell'intestazione hello (mostrato sotto) hello. Modificare la configurazione dei dispositivi hello in modo che hello computer disponga di risorse adatte toomeet hello requisiti minimi. È quindi possibile avviare e connettere il dispositivo toohello. Consultare i requisiti minimi di configurazione toohello in [passaggio 1: verificare che il sistema di host hello soddisfi i requisiti di array virtuale minimo](#step-1-ensure-that-the-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-hyperv/image32.png)

Se si trovano ad affrontare eventuali altri errori durante la configurazione iniziale hello tramite interfaccia utente web locale hello, vedere toohello flussi di lavoro seguente:

* Eseguire i test diagnostici troppo[risolvere i problemi di installazione dell'interfaccia utente web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Generare un pacchetto di log e visualizzare i file di log](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Passaggi successivi
* [Configurare StorSimple Virtual Array come file server](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurare StorSimple Virtual Array come server iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
