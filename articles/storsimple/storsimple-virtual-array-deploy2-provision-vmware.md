---
title: Array virtuale StorSimple in VMware aaaProvision | Documenti Microsoft
description: Questa seconda esercitazione sulla serie di distribuzione di StorSimple Virtual Array implica il provisioning di un dispositivo virtuale in VMware.
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 0425b2a9-d36f-433d-8131-ee0cacef95f8
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/15/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0912c1c315a04ea46b6373a8fcd5554ecae14e61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---provision-in-vmware"></a>Distribuire StorSimple Virtual Array: eseguire il provisioning in VMware
![](./media/storsimple-virtual-array-deploy2-provision-vmware/vmware4.png)

## <a name="overview"></a>Panoramica
Questa esercitazione viene descritto come tooprovision e connettersi tooa Array virtuale StorSimple su un sistema di host che esegue VMware ESXi 5.5 e versioni successive. Questo articolo riguarda la distribuzione di toohello di matrici virtuale StorSimple nel portale di Azure e hello Cloud di Microsoft Azure per enti pubblici.

È necessario tooprovision privilegi di amministratore e connettersi tooa di dispositivo virtuale. l'installazione iniziale e provisioning Hello può richiedere circa 10 minuti toocomplete.

## <a name="provisioning-prerequisites"></a>Prerequisiti di provisioning
Prerequisiti tooprovision un dispositivo virtuale su un sistema host che eseguono VMware ESXi 5.5 Hello e sopra, sono i seguenti.

### <a name="for-hello-storsimple-device-manager-service"></a>Per il servizio di gestione di dispositivi StorSimple hello
Prima di iniziare, verificare che:

* Sono stati completati tutti i passaggi di hello in [portale hello preparazione per Array virtuale StorSimple](storsimple-virtual-array-deploy1-portal-prep.md).
* È stato scaricato l'immagine del dispositivo virtuale hello per VMware da hello portale di Azure. Per ulteriori informazioni, vedere **passaggio 3: immagine del dispositivo virtuale hello Download** di [portale hello preparazione per la Guida di StorSimple Virtual Array](storsimple-virtual-array-deploy1-portal-prep.md).

### <a name="for-hello-storsimple-virtual-device"></a>Per il dispositivo virtuale StorSimple di hello
Prima di distribuire un dispositivo virtuale, è necessario:

* Si dispone di accesso tooa host sistema che esegue Hyper-V (2008 R2 o versioni successive) che può essere utilizzato tooa effettuare il provisioning di un dispositivo.
* sistema host Hello è in grado di toodedicate hello seguenti tooprovision risorse del dispositivo virtuale:

  * Un minimo di 4 memorie centrali.
  * Almeno 8 GB di RAM. Se si prevede di tooconfigure hello virtual array file server, 8 GB supporta i file meno di 2 milioni. 16 GB RAM toosupport 2-4 milioni file necessari.
  * Un'interfaccia di rete.
  * Un disco virtuale da 500 GB per i dati di sistema.

### <a name="for-hello-network-in-datacenter"></a>Per la rete hello nel Data Center
Prima di iniziare, verificare che:

* Aver esaminato hello rete requisiti toodeploy un dispositivo virtuale StorSimple, rete di Data Center hello configurata in base ai requisiti di hello. 

## <a name="step-by-step-provisioning"></a>Provisioning passo per passo
tooprovision e connettere tooa di dispositivo virtuale, è necessario hello tooperform alla procedura seguente:

1. Verificare che il sistema host hello abbia i requisiti minimi del dispositivo virtuale hello toomeet risorse sufficienti.
2. Eseguire il provisioning di un dispositivo virtuale in hypervisor.
3. Avviare la periferica virtuale hello e ottenere l'indirizzo IP hello.

## <a name="step-1-ensure-host-system-meets-minimum-virtual-device-requirements"></a>Passaggio 1: Verificare che il sistema host soddisfi i requisiti minimi del dispositivo virtuale
toocreate un dispositivo virtuale, è necessario:

* Sistema host tooa di accesso che esegue VMware ESXi Server 5.5 e versioni successive.
* VMware vSphere client nell'host ESXi hello toomanage sistema.

  * Un minimo di 4 memorie centrali.
  * Almeno 8 GB di RAM. Se si prevede di tooconfigure hello virtual array file server, 8 GB supporta i file meno di 2 milioni. 16 GB RAM toosupport 2-4 milioni file necessari.
  * Un'interfaccia di rete connessa toohello rete in grado di routing del traffico tooInternet. larghezza di banda Internet minima Hello deve essere 5 Mbps tooallow per l'utilizzo ottimale del dispositivo hello.
  * Un disco virtuale da 500 GB per i dati.

## <a name="step-2-provision-a-virtual-device-in-hypervisor"></a>Passaggio 2: Eseguire il provisioning di un dispositivo virtuale in hypervisor
Eseguire i seguenti passaggi tooprovision un dispositivo virtuale nell'hypervisor hello.

1. Copiare l'immagine del dispositivo virtuale hello nel sistema. Questa immagine virtuale tramite il portale di Azure hello è stato scaricato.

   1. Verificare che sia stato scaricato il file di immagine più recente hello. Se l'immagine di hello è stato scaricato in precedenza, scaricarlo di nuovo tooensure immagine più recente di hello. immagine più recente di Hello include due file (invece di uno).
   2. Prendere nota del percorso hello in cui è stata copiata hello immagine quando si utilizza questa immagine in un secondo momento nella procedura di hello.

2. Accedi toohello server ESXi utilizzando hello vSphere client. È necessario toocreate privilegi di amministratore toohave una macchina virtuale.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image1.png)
3. Nel client di vSphere hello nella sezione inventario hello nel riquadro di sinistra hello, selezionare ESXi Server hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image2.png)
4. Caricare i server di hello VMDK toohello ESXi. Passare toohello **configurazione** scheda nel riquadro di destra hello. In **Hardware** selezionare **Storage** (Archiviazione).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image3.png)
5. In hello destro in riquadro **archivi dati**, selezionare hello archivio dati in cui si desidera hello tooupload VMDK. archivio dati Hello devono avere sufficiente spazio libero per hello del sistema operativo e i dischi dati.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image4.png)
6. Fare clic con il pulsante destro del mouse e scegliere **Browse Datastore** (Sfoglia archivio dati).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image5.png)
7. Viene visualizzata una finestra **Datastore Browser** (Browser archivio dati).

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image6.png)
8. Nella barra degli strumenti hello, fare clic su ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image7.png) icona toocreate una nuova cartella. Specificare il nome di cartella hello e prendere nota di esso. Il nome di questa cartella verrà usato più avanti durante la creazione di una macchina virtuale (procedura consigliata). Fare clic su **OK**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image8.png)
9. Hello nuova cartella verrà visualizzata nel riquadro di sinistra hello di hello **Datastore Browser**.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image9.png)
10. Fare clic sull'icona di caricamento hello ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image10.png) e selezionare **carica File**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image11.png)
11. Individuare e selezionare i file VMDK toohello scaricato. Sono disponibili due file. Selezionare un tooupload di file.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image12m.png)
12. Fare clic su **Apri**. caricamento di Hello di toohello file VMDK di hello specificato viene avviato l'archivio dati. Potrebbe richiedere alcuni minuti per tooupload file hello.
13. Dopo aver completato il caricamento di hello, vedrai file hello nell'archivio dati hello nella cartella hello che è stato creato.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image14.png)

    Ora caricare toohello di file VMDK secondo hello stesso archivio dati.
14. Finestra di client vSphere toohello restituito. Con il server ESXi selezionato, fare click con il tasto destro del mouse e selezionare **New Virtual Machine**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image15.png)
15. Viene visualizzata una finestra **Create New Virtual Machine** . In hello **configurazione** pagina, seleziona hello **personalizzato** opzione. Fare clic su **Avanti**.
    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image16.png)
16. In hello **nome e percorso** , specificare il nome di hello della macchina virtuale. Questo nome deve corrispondere a quello hello cartella (procedura consigliata) specificato in precedenza nel passaggio 8.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image17.png)
17. In hello **archiviazione** pagina, selezionare un archivio dati si desidera toouse tooprovision la macchina virtuale.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image18.png)
18. In hello **versione della macchina virtuale** selezionare **versione della macchina virtuale: 8**. Versioni 8 too11 tutte supportate.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image19.png)
19. In hello **sistema operativo Guest** pagina, seleziona hello **sistema operativo Guest** come **Windows**. Per **versione**, selezionare nell'elenco a discesa hello **Microsoft Windows Server 2012 (64 bit)**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image20.png)
20. In hello **CPU** , regolare hello pagina **numero di socket virtuale** e **numero di core per socket virtuale** in modo che hello **numero totale di core**è 4 (o più). Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image21.png)
21. In hello **memoria** specificare 8 GB (o più) di RAM. Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image22.png)
22. In hello **rete** , specificare il numero di hello hello delle interfacce di rete. requisito minimo di Hello è un'interfaccia di rete.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image23.png)
23. In hello **Controller SCSI** accettare l'impostazione predefinita hello **controller SAS di LSI Logic**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image24.png)
24. In hello **selezionare un disco** pagina, scegliere **utilizzare un disco virtuale esistente**. Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image25.png)
25. In hello **selezionare un disco esistente** pagina **il percorso di File su disco**, fare clic su **Sfoglia**. Si apre così una finestra di dialogo **Browse Datastores** . Passare toohello percorso in cui è caricato hello VMDK. È ora possibile visualizzare solo un file nell'archivio dati hello come hello due file che è stato caricato inizialmente sono stati uniti. Selezionare il file hello e fare clic su **OK**. Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image26.png)
26. In hello **opzioni avanzate** pagina, accettare l'impostazione predefinita hello e fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image27.png)
27. In hello **tooComplete pronto** verificare tutte le impostazioni di hello associate hello nuova macchina virtuale. Controllare **modificare impostazioni della macchina virtuale hello prima del completamento**. Fare clic su **Continue**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image28.png)
28. In hello **le proprietà delle macchine virtuali** pagina hello **Hardware** , individuare l'hardware dei dispositivi hello. Selezionare **New Hard Disk**. Fare clic su **Aggiungi**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image29.png)
29. Viene visualizzata la finestra **Add Hardware** (Aggiungi hardware). In hello **tipo di dispositivo** nella pagina **scegliere il tipo di dispositivo hello desiderato tooadd**selezionare **disco rigido**, fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image30.png)
30. In hello **selezionare un disco** pagina, scegliere **creare un nuovo disco virtuale**. Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image31.png)
31. In hello **creare un disco** pagina, modificare hello **dimensioni disco** too500 (più GB). Mentre 500 GB è il requisito minimo di hello, è sempre possibile eseguire il provisioning di un disco più grande. Si noti che non è possibile espandere o compattare il disco di hello una volta eseguito il provisioning. Per ulteriori informazioni sulle dimensioni hello tooprovision disco, nella sezione hello ridimensionamento in hello [documento di best practices](storsimple-ova-best-practices.md). In **Disk Provisioning** (Provisioning disco) selezionare **Thin Provision** (Provisioning leggero). Fare clic su **Avanti**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image32.png)
32. In hello **opzioni avanzate** accettare l'impostazione predefinita di hello.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image33.png)
33. In hello **tooComplete pronto** pagina, esaminare le opzioni di hello disco. Fare clic su **Finish**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image34.png)
34. Restituire toohello pagina di proprietà della macchina virtuale. Un nuovo disco rigido viene aggiunta una macchina virtuale tooyour. Fare clic su **Finish**.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image35.png)
35. Con la macchina virtuale selezionata nel riquadro di destra hello, passare toohello **riepilogo** scheda. Esaminare le impostazioni di hello per la macchina virtuale.

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image36.png)

La macchina virtuale viene ora sottoposta a provisioning. passaggio successivo Hello è toopower su questo computer e ottenere l'indirizzo IP hello.

## <a name="step-3-start-hello-virtual-device-and-get-hello-ip"></a>Passaggio 3: Avviare la periferica virtuale hello e ottenere l'indirizzo IP di hello
Eseguire hello seguendo i passaggi toostart dispositivo virtuale e connettersi tooit.

#### <a name="toostart-hello-virtual-device"></a>dispositivo virtuale di hello toostart
1. Avviare la periferica virtuale hello. In vSphere hello Configuration Manager, nel riquadro di sinistra hello, selezionare il dispositivo e fare doppio clic su toobring menu di scelta rapida hello. Selezionare **Power** (Alimentazione) e scegliere **Power on** (Alimentazione attiva). La macchina virtuale deve accendersi. È possibile visualizzare lo stato di hello nella parte inferiore di hello **attività recenti** riquadro del client di vSphere hello.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image37.png)
2. le attività di configurazione Hello richiederà alcuni minuti toocomplete. Quando il dispositivo hello è in esecuzione, passare toohello **Console** scheda. Inviare Ctrl + Alt + Canc toolog toohello dispositivo. In alternativa, è possibile scegliere di cursore hello nella finestra della console hello e premere Ctrl + Alt + ins. utente predefinito Hello *StorSimpleAdmin* e la password predefinita hello è *Password1*.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image38.png)
3. Per motivi di sicurezza, password amministratore del dispositivo hello scade al primo accesso hello. Si è password hello toochange richiesta.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image39.png)
4. Immettere una password contenente almeno 8 caratteri. password di Hello deve contenere 3 su 4 di questi requisiti: caratteri maiuscoli, minuscoli, numerici e speciali. Immettere nuovamente tooconfirm password hello è. Si riceverà una notifica che la password hello è stato modificato.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image40.png)
5. Dopo che la password di hello viene modificata, potrebbe verificarsi un riavvio dispositivo virtuale hello. Attendere toocomplete riavvio hello. console di Windows PowerShell Hello del dispositivo hello potrebbe essere visualizzati insieme a un indicatore di stato.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image41.png)
6. I passaggi da 6 a 8 si applicano solo all'avvio in un ambiente non DHCP. Se si dispone di un ambiente di DHCP, quindi ignorare questi passaggi e passare toostep 9. Se il dispositivo nell'ambiente di DHCP non è avviato, verrà visualizzato hello seguente schermata.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image42m.png)

   Successivamente, configurare la rete hello.
7. Hello utilizzare `Get-HcsIpAddress` comando interfacce di rete hello toolist abilitate nel dispositivo virtuale. Se il dispositivo dispone di una singola interfaccia di rete abilitata, interfaccia toothis di hello predefinita nome assegnato è `Ethernet`.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image43m.png)
8. Hello utilizzare `Set-HcsIpAddress` rete hello tooconfigure di cmdlet. Di seguito è riportato un esempio:

    `Set-HcsIpAddress –Name Ethernet –IpAddress 10.161.22.90 –Netmask 255.255.255.0 –Gateway 10.161.22.1`

    ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image44.png)
9. Dopo aver completata la configurazione iniziale di hello e dispositivo hello è avviato, verrà visualizzato testo dell'intestazione dispositivo hello. Prendere nota dell'indirizzo IP hello e hello URL visualizzato nel dispositivo di hello banner testo toomanage hello. Si utilizzerà questo web di toohello tooconnect indirizzo IP dell'interfaccia utente di dispositivo virtuale e l'installazione locale completa hello e di registrazione.

   ![](./media/storsimple-virtual-array-deploy2-provision-vmware/image45.png)
10. (Facoltativo) Eseguire questo passaggio solo se si distribuisce il dispositivo in hello Government Cloud. È ora verrà abilitare la modalità di Stati Uniti elaborazione Standard FIPS (Federal Information) hello sul dispositivo. standard di Hello FIPS 140 definisce gli algoritmi di crittografia approvati per l'utilizzo dai sistemi di computer governo federale US per la protezione dei dati sensibili hello.

    1. modalità FIPS di hello di tooenable, eseguire hello seguente cmdlet:

        `Enable-HcsFIPSMode`
    2. Dopo aver attivato la modalità FIPS hello in modo che le convalide di crittografia hello abbiano effetto, riavviare il dispositivo.

       > [!NOTE]
       > È possibile abilitare o disabilitare la modalità FIPS sul dispositivo. Dispositivo hello alternarsi tra la modalità FIPS e non FIPS non è supportata.
       >
       >

Se il dispositivo non soddisfa i requisiti minimi delle configurazioni di hello, si verrà visualizzato un errore nel testo dell'intestazione hello (mostrato sotto). Configurazione del dispositivo hello toomodify sarà necessario in modo che abbia i requisiti minimi di risorse adatte toomeet hello. È quindi possibile avviare e connettere il dispositivo toohello. Consultare i requisiti minimi di configurazione toohello in [passaggio 1: verificare che il sistema di host hello soddisfi i requisiti minimi del dispositivo virtuale](#step-1-ensure-host-system-meets-minimum-virtual-device-requirements).

![](./media/storsimple-virtual-array-deploy2-provision-vmware/image46.png)

Se si trovano ad affrontare eventuali altri errori durante la configurazione iniziale hello tramite interfaccia utente web locale hello, vedere toohello flussi di lavoro seguente:

* Eseguire i test diagnostici troppo[risolvere i problemi di installazione dell'interfaccia utente web](storsimple-ova-web-ui-admin.md#troubleshoot-web-ui-setup-errors).
* [Generare un pacchetto di log e visualizzare i file di log](storsimple-ova-web-ui-admin.md#generate-a-log-package).

## <a name="next-steps"></a>Passaggi successivi
* [Configurare StorSimple Virtual Array come file server](storsimple-virtual-array-deploy3-fs-setup.md)
* [Configurare StorSimple Virtual Array come server iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md)
