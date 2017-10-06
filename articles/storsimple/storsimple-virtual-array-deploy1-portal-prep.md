---
title: Prepara aaaPortal per Array virtuale StorSimple | Documenti Microsoft
description: Primo toodeploy esercitazione array virtuale StorSimple consiste nel preparare hello portale di Azure
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 68a4cfd3-94c9-46cb-805c-46217290ce02
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5332b235e7296a9274f2e7dafcdf72f4b9cdadf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-storsimple-virtual-array---prepare-hello-azure-portal"></a>Distribuire StorSimple Virtual Array - preparazione hello portale di Azure

![](./media/storsimple-virtual-array-deploy1-portal-prep/getstarted4.png)
## <a name="overview"></a>Panoramica

Si tratta di hello primo articolo hello serie di esercitazioni per la distribuzione necessaria toocompletely distribuire l'array virtuale come un file server o server iSCSI usando il modello di gestione risorse hello. Questo articolo descrive toocreate di preparazione necessarie hello e configurare la gestione di dispositivi StorSimple servizio precedenti tooprovisioning un array virtuale. In questo articolo è anche possibile collegare out tooa distribuzione elenco di controllo e la configurazione prerequisiti di configurazione.

È necessario amministratore privilegi toocomplete hello il programma di installazione e configurazione processo. È consigliabile rivedere l'elenco di controllo configurazione distribuzione hello prima di iniziare. Preparazione del portale Hello richiede meno di 10 minuti.

informazioni di Hello pubblicate in questo articolo si applicano distribuzione toohello di StorSimple array virtuale nel portale di Azure hello e Cloud di Microsoft Azure per enti pubblici.

### <a name="get-started"></a>Attività iniziali
flusso di lavoro distribuzione Hello è costituito da portale hello preparazione, il provisioning di un array virtuale nell'ambiente virtualizzato e il completamento dell'installazione di hello. tooget avviato con la distribuzione di StorSimple Virtual Array hello come un file server o server iSCSI, è necessario toohello toorefer seguente tabulari risorse.

#### <a name="deployment-articles"></a>Articoli sulla distribuzione

toodeploy l'Array virtuale StorSimple, fare riferimento toohello seguenti articoli in hello prescritte sequenza.

| **#** | **In questo passaggio** | **A questo scopo:** | **Usare questi documenti.** |
| --- | --- | --- | --- |
| 1. |**Impostare hello portale di Azure** |Creare e configurare la gestione di dispositivi StorSimple servizio precedenti tooprovisioning un Array virtuale StorSimple. |[Preparare portale hello](storsimple-virtual-array-deploy1-portal-prep.md) |
| 2. |**Eseguire il provisioning di hello Array virtuale** |Per Hyper-V, eseguire il provisioning e connettersi tooa Array virtuale StorSimple su un sistema host in esecuzione Hyper-V in Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2. <br></br> <br></br> Per VMware, eseguire il provisioning e connettersi tooa Array virtuale StorSimple su un sistema di host che esegue VMware ESXi 5.5 e versioni successive.<br></br> |[Eseguire il provisioning di un array virtuale in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md) <br></br> <br></br> [Eseguire il provisioning di un array virtuale in VMware](storsimple-virtual-array-deploy2-provision-vmware.md) |
| 3. |**Impostare hello Array virtuale** |Per il file server, eseguire la configurazione iniziale, registrare il server di file StorSimple e completare la configurazione di dispositivo hello. È quindi possibile eseguire il provisioning delle condivisioni SMB. <br></br> <br></br> Per il server iSCSI, eseguire la configurazione iniziale, registrare il server iSCSI StorSimple e completare la configurazione di dispositivo hello. È quindi possibile eseguire il provisioning dei volumi iSCSI. |[Configurare l'array virtuale come file server](storsimple-virtual-array-deploy3-fs-setup.md)<br></br> <br></br>[Configurare l'array virtuale come server iSCSI](storsimple-virtual-array-deploy3-iscsi-setup.md) |

È ora possibile iniziare tooset backup hello portale di Azure.

## <a name="configuration-checklist"></a>Elenco di controllo configurazione

elenco di controllo configurazione Hello descrive informazioni hello necessarie toocollect prima di configurare il software di hello nell'Array virtuale StorSimple. Preparazione informazioni avanti rispetto all'ora consente semplificata hello processo di distribuzione del dispositivo StorSimple hello nell'ambiente in uso. A seconda se l'Array virtuale StorSimple viene distribuito come un file server o server iSCSI, è necessario uno dei seguenti elenchi di controllo hello.

* Scaricare hello [StorSimple Virtual Array File Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayFileServerConfigurationChecklist.pdf).
* Scaricare hello [iSCSI StorSimple Virtual Array Server Configuration Checklist](http://download.microsoft.com/download/E/E/6/EE690BB0-B442-4B84-8165-4731EE727ACF/MicrosoftAzureStorSimpleVirtualArrayiSCSIServerConfigurationChecklist.pdf).

## <a name="prerequisites"></a>Prerequisiti

Qui disponibili prerequisiti di configurazione hello per il servizio di gestione di dispositivi StorSimple, l'Array virtuale StorSimple e hello datacenter rete.

### <a name="for-hello-storsimple-device-manager-service"></a>Per il servizio di gestione di dispositivi StorSimple hello

Prima di iniziare, verificare che:

* Si dispone dell'account Microsoft con credenziali di accesso.
* Si dispone dell'account di archiviazione di Microsoft Azure con credenziali di accesso.
* La sottoscrizione di Microsoft Azure deve essere abilitata per il servizio Gestione dispositivi StorSimple.

### <a name="for-hello-storsimple-virtual-array"></a>Per hello Array virtuale StorSimple

Prima di distribuire un array virtuale, è necessario:

* Si dispone di accesso tooa host sistema che esegue Hyper-V in Windows Server 2008 R2 o versioni successive o VMware (ESXi 5.5 o versione successiva) che può essere utilizzato tooa effettuare il provisioning di un dispositivo.
* sistema host Hello è in grado di toodedicate hello seguenti risorse tooprovision l'array virtuale:
  
  * Un minimo di 4 memorie centrali.
  * Almeno 8 GB di RAM. Se si prevede di tooconfigure hello virtual array file server, 8 GB supporta 2 milioni di file. 16 GB RAM toosupport 2-4 milioni file necessari.
  * Un'interfaccia di rete.
  * Un disco virtuale da 500 GB per i dati di sistema.

### <a name="for-hello-datacenter-network"></a>Per la rete di Data Center hello

Prima di iniziare, verificare che:

* rete Hello nel Data Center è configurata in base ai requisiti di rete hello per il dispositivo StorSimple. Per ulteriori informazioni, vedere hello [requisiti di sistema StorSimple Virtual Array](storsimple-ova-system-requirements.md).
* L'array virtuale StorSimple dispone di una larghezza di banda Internet dedicata a 5 Mbps (o superiore) sempre disponibile. La larghezza di banda non deve essere condivisa con altre applicazioni.

## <a name="step-by-step-preparation"></a>Preparazione dettagliata

Utilizzare il portale di hello seguendo le istruzioni dettagliate tooprepare per hello del servizio di gestione di dispositivi StorSimple.

## <a name="step-1-create-a-new-service"></a>Passaggio 1: Creare un nuovo servizio

Una singola istanza del servizio di gestione di dispositivi StorSimple hello può gestire più array virtuale StorSimple. Eseguire i seguenti passaggi toocreate un'istanza del servizio di gestione di dispositivi StorSimple hello hello. Se si dispone di un esistente toomanage servizio di gestione di dispositivi StorSimple gli array virtuali, ignorare questo passaggio e andare troppo[passaggio 2: chiave di registrazione del servizio Get hello](#step-2-get-the-service-registration-key).

[!INCLUDE [storsimple-virtual-array-create-new-service](../../includes/storsimple-virtual-array-create-new-service.md)]

> [!IMPORTANT]
> Se non si abilita la creazione automatica di un account di archiviazione hello con il servizio, sarà necessario toocreate almeno un account di archiviazione, dopo avere creato un servizio.
> 
> * Se non è stato creato automaticamente un account di archiviazione, andare troppo[configurare un nuovo account di archiviazione per il servizio hello](#optional-step-configure-a-new-storage-account-for-the-service) per istruzioni dettagliate.
> * Se è abilitata la creazione automatica di hello di un account di archiviazione, andare troppo[passaggio 2: chiave di registrazione del servizio Get hello](#step-2-get-the-service-registration-key).
> 
> 

## <a name="step-2-get-hello-service-registration-key"></a>Passaggio 2: Ottenere una chiave di registrazione del servizio hello

Dopo che il servizio di gestione di dispositivi StorSimple hello sia in esecuzione, sarà necessario chiave di registrazione del servizio tooget hello. Questa chiave è utilizzata tooregister e connettere il dispositivo StorSimple con servizio hello.

Eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com/).

[!INCLUDE [storsimple-virtual-array-get-service-registration-key](../../includes/storsimple-virtual-array-get-service-registration-key.md)]

> [!NOTE]
> chiave di registrazione Hello è usato tooregister tutti hello dispositivi dispositivo StorSimple Manager necessario tooregister con il servizio di gestione di dispositivi StorSimple.
> 
> 

## <a name="step-3-download-hello-virtual-array-image"></a>Passaggio 3: Scaricare l'immagine di hello array virtuale

Dopo aver creato una chiave di registrazione del servizio hello, sarà necessario toodownload hello array virtuale appropriato immagine tooprovision un array virtuale nel sistema host. le immagini di Hello array virtuale sono specifiche del sistema operativo e possono essere scaricate dalla pagina avvio rapido hello in hello portale di Azure.

> [!IMPORTANT]
> software Hello in esecuzione su hello Array virtuale StorSimple può essere utilizzato solo con il servizio di gestione di dispositivi StorSimple hello.
> 
> 

Eseguire i passaggi hello hello [portale di Azure](https://portal.azure.com/).

#### <a name="tooget-hello-virtual-array-image"></a>immagine di array virtuale hello tooget

1. Sign in hello [portale di Azure](https://portal.azure.com/). 
2. Nel portale di Azure hello, fare clic su **Sfoglia > Manager dispositivi StorSimple**.
3. Selezionare un servizio Gestione dispositivi StorSimple esistente. In hello **Gestione dispositivi StorSimple** pannello, fare clic su **avvio rapido**. 
4. Fare clic su hello collegamento toohello immagine corrispondente che si desidera toodownload da hello Microsoft Download Center. file di immagine Hello sono circa 4,8 GB.
   
   * VHDX per Hyper-V in Windows Server 2012 e versioni successive
   * VHD per Hyper-V in Windows Server 2008 R2 e versioni successive
   * VMDK per VMWare ESXi 5.5 e versioni successive
5. Scaricare e decomprimere hello tooa locale unità del file, rendendo nota dei file decompressi hello in cui si trova.

## <a name="optional-step-configure-a-new-storage-account-for-hello-service"></a>Passaggio facoltativo: configurare un nuovo account di archiviazione per il servizio hello

Questo passaggio è facoltativo e deve essere eseguito solo se non si abilita la creazione automatica di un account di archiviazione hello con il servizio.

Se è necessario un account di archiviazione di Azure in un'area diversa toocreate, vedere [come un account di archiviazione toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account) per istruzioni dettagliate.

Eseguire i passaggi hello hello [portale di Azure](https://ms.portal.azure.com/) nel servizio di gestione dispositivi StorSimple hello, tooadd pagina un account di archiviazione di Microsoft Azure esistente.

#### <a name="tooadd-a-storage-account-credential-that-has-hello-same-azure-subscription-as-hello-device-manager-service"></a>una credenziale dell'account di archiviazione con tooadd hello stessa sottoscrizione di Azure come servizio di Gestione periferiche hello

1. Passare tooyour del servizio di Gestione periferiche, seleziona e fare doppio clic. Verrà visualizzata hello **Panoramica** blade.
2. Selezionare **le credenziali dell'account di archiviazione** all'interno di hello **configurazione** sezione.
3. Fare clic su **Aggiungi**.
4. In hello **aggiungere un account di archiviazione** pannello hello seguenti:
   
    1. Per **Sottoscrizione** selezionare **Corrente**.
   
    2. Specificare il nome di hello dell'account di archiviazione di Azure.
   
    3. Selezionare **abilitare** toocreate un canale sicuro per la comunicazione di rete tra il cloud di dispositivo e hello StorSimple. Selezionare **Disabilita** solo se si opera all'interno di un cloud privato.
   
    4. Fare clic su **Aggiungi**. Ricevono una notifica dopo la creazione dell'account di archiviazione hello.<br></br>
   
     ![Aggiungere le credenziali di un account di archiviazione esistente](./media/storsimple-virtual-array-manage-storage-accounts/ova-add-storageacct.png)

## <a name="next-step"></a>Passaggio successivo

passaggio successivo Hello è tooprovision una macchina virtuale per l'Array virtuale StorSimple. A seconda del sistema operativo host, vedere hello dettagliate in:

* [Eseguire il provisioning di un array virtuale StorSimple in Hyper-V](storsimple-virtual-array-deploy2-provision-hyperv.md)
* [Eseguire il provisioning di un array virtuale StorSimple in VMware](storsimple-virtual-array-deploy2-provision-vmware.md)

