---
title: immagine aaaCreate e caricamento di una VM FreeBSD | Documenti Microsoft
description: Informazioni su toocreate e caricare un disco rigido virtuale (VHD) che contiene hello FreeBSD del sistema operativo toocreate una macchina virtuale di Azure
services: virtual-machines-linux
documentationcenter: 
author: KylieLiang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 1ef30f32-61c1-4ba8-9542-801d7b18e9bf
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/08/2017
ms.author: kyliel
ms.openlocfilehash: f3bd155e496f1a2713d36bb66ea9824ed4c210ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a>Creare e caricare un tooAzure FreeBSD VHD
Questo articolo illustra come toocreate e caricare un disco rigido virtuale (VHD) che contiene hello FreeBSD del sistema operativo. Dopo aver caricato il, è possibile utilizzare, come la propria toocreate immagine una macchina virtuale (VM) in Azure.

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni. Per informazioni sul caricamento di un disco rigido virtuale utilizzando il modello di gestione risorse hello, vedere [qui](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="prerequisites"></a>Prerequisiti
Questo articolo si presuppone di aver hello seguenti elementi:

* **Una sottoscrizione Azure**: se non è già disponibile un account, è possibile crearne uno in pochi minuti. Se si ha un abbonamento a MSDN, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/). In caso contrario, informazioni su come troppo[creare un account di prova](https://azure.microsoft.com/pricing/free-trial/).  
* **Strumenti di Azure PowerShell**-modulo di Azure PowerShell hello deve essere installato e configurato toouse la sottoscrizione di Azure. modulo hello toodownload, vedere [download di Azure](https://azure.microsoft.com/downloads/). In questa esercitazione viene descritto come tooinstall e configurare il modulo di hello è disponibile qui. Hello utilizzare [download di Azure](https://azure.microsoft.com/downloads/) hello tooupload cmdlet disco rigido virtuale.
* **Sistema operativo FreeBSD installato in un file con estensione vhd**disco rigido virtuale tooa: il sistema operativo di FreeBSD supportato deve essere installato. Più strumenti esistono toocreate file con estensione vhd. Ad esempio, è possibile usare una soluzione di virtualizzazione, ad esempio file con estensione vhd di Hyper-V toocreate hello e installare hello del sistema operativo. Per istruzioni su come tooinstall e utilizzare Hyper-V, vedere [installare Hyper-V e creare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).

> [!NOTE]
> il formato VHDX più recente di Hello non è supportato in Azure. È possibile convertire il formato di tooVHD di hello disco tramite la gestione di Hyper-V o hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx). Inoltre, è un [esercitazione su MSDN sul toouse FreeBSD con Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).
>
>

Questa attività include hello cinque passaggi:

## <a name="step-1-prepare-hello-image-for-upload"></a>Passaggio 1: Preparare l'immagine di hello per il caricamento
Nella macchina virtuale hello in cui è installato hello FreeBSD del sistema operativo, completare hello seguire le procedure seguenti:

1. Abilitare DHCP.

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. Abilitare SSH.

    Verificare che server SSH hello sia installato e configurato toostart in fase di avvio. SSH è abilitato per impostazione predefinita dopo l'installazione dal disco FreeBSD. 
3. Configurare la console seriale.

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. Installare sudo.

    account radice Hello è disabilitata in Azure. Ciò significa che è necessario sudo tooutilize dai comandi di toorun utente senza privilegi con privilegi elevati.

        # pkg install sudo
   
5. Prerequisiti per l'agente di Azure.

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. Installare l'agente di Azure.

    Hello versione più recente dell'agente di Azure hello è sempre disponibile nel [github](https://github.com/Azure/WALinuxAgent/releases). Hello versione 2.0.10 + supporta ufficialmente 10 FreeBSD & 10.1 e la versione di hello 2.1.4 + (inclusi 2.2) supporta ufficialmente 10.2 FreeBSD e versioni successive.

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    Per la versione 2.0 verrà usata come esempio la versione 2.0.16:

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    Per la versione 2.1 verrà usata come esempio la versione 2.1.4:

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > Dopo aver installato l'agente di Azure, è un tooverify buona norma che è in esecuzione:
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. Eseguire il deprovisioning sistema hello.

    Deprovisioning hello tooclean di sistema e verificare che è adatto per la riconfigurazione. Hello seguente comando Elimina inoltre ultimo account di provisioning utente hello e dati hello associata:

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    Ora è possibile arrestare la macchina virtuale.

## <a name="step-2-create-a-storage-account-in-azure"></a>Passaggio 2: creare un account di archiviazione in Microsoft Azure
È necessario un account di archiviazione in Azure tooupload un file con estensione vhd in modo da poterli toocreate usato una macchina virtuale. È possibile utilizzare hello Azure toocreate portale classico un account di archiviazione.

1. Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).
2. Nella barra dei comandi di hello, selezionare **New**.
3. Fare clic su **Servizi dati** > **Archiviazione** > **Creazione rapida**.

    ![Creazione rapida di un account di archiviazione](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. Compilare i campi hello come indicato di seguito:

   * In hello **URL** , digitare un toouse nome di sottodominio in hello URL di account di archiviazione. voce Hello può contenere da 3 a 24 numeri e lettere minuscole. Questo nome diventa il nome host hello in URL hello tooaddress usato nell'archiviazione Blob di Azure, l'archiviazione delle code di Azure o le risorse di archiviazione tabelle di Azure per sottoscrizione hello.
   * In hello **posizione/gruppo di affinità** dal menu a discesa scegliere hello **percorso o gruppo di affinità** hello account di archiviazione. Un gruppo di affinità consente di inserire i servizi cloud e archiviazione in hello nello stesso data center.
   * In hello **replica** campo, decidere se toouse **con ridondanza geografica** replica hello account di archiviazione. La replica geografica è attivata per impostazione predefinita. Questa opzione consente di replicare i dati tooa posizione secondaria, in tooyou alcun costo, si verifica in modo che lo spazio di archiviazione viene eseguito il failover toothat percorso se un errore grave nella posizione primaria hello. percorso secondario Hello viene assegnato automaticamente e non può essere modificato. Se è necessario maggiore controllo sulla posizione hello dello spazio di archiviazione basato su cloud a causa di requisiti toolegal o criteri dell'organizzazione, è possibile disattivare la replica geografica. Tuttavia, tenere presente che se si attiva in un secondo momento replica geo, verranno addebitati una sola volta tooreplicate tariffa di trasferimento dei dati del percorso secondario toohello dati esistente. I servizi di archiviazione senza replica geografica sono offerti a un prezzo scontato. Altri dettagli sulla gestione della replica geografica degli account di archiviazione sono disponibili nell'articolo [Replica dell'archiviazione di Azure](../../../storage/common/storage-redundancy.md).

     ![Immissione dei dettagli dell'account di archiviazione](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. Fai clic su **Crea account di archiviazione**. Hello account viene visualizzato in **archiviazione**.

    ![Creazione dell'account di archiviazione completata](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. Creare quindi un contenitore per i VHD caricati. Nome account di archiviazione hello, scegliere quindi **contenitori**.

    ![Dettaglio dell'account di archiviazione](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. Selezionare **Crea contenitore**.

    ![Dettaglio dell'account di archiviazione](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. In hello **nome** , digitare un nome per il contenitore. Quindi, nel hello **accesso** -menu a discesa, seleziona il tipo di criterio di accesso desiderato.

    ![Nome contenitore](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > Per impostazione predefinita, il contenitore di hello è privato e accessibile solo dal proprietario dell'account hello. tooallow accesso in lettura pubblico toohello BLOB nel contenitore di hello, ma non le proprietà del contenitore toohello e i metadati, usare hello **Blob pubblici** opzione. accesso in lettura pubblico completo tooallow per hello contenitori e BLOB, utilizzare hello **contenitore pubblico** opzione.
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a>Passaggio 3: Preparare hello connessione tooAzure
Prima di poter caricare un file con estensione vhd, è necessario tooestablish una connessione sicura tra il computer e la sottoscrizione di Azure. È possibile utilizzare il metodo di Azure Active Directory (Azure AD) hello o hello certificato metodo toodo è.

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a>Utilizzare tooupload metodo hello Azure AD un file con estensione vhd
1. Console di hello aprire Azure PowerShell.
2. Digitare hello comando seguente:  
    `Add-AzureAccount`

    Questo comando consente di aprire una finestra in cui è possibile eseguire l'accesso con l'account aziendale o dell'istituto di istruzione.

    ![Finestra di PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. Azure autentica e Salva le informazioni sulle credenziali hello. Quindi chiude la finestra hello.

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a>Utilizzare tooupload di metodo hello certificato un file con estensione vhd
1. Console di hello aprire Azure PowerShell.
2. Digitare `Get-AzurePublishSettingsFile`.
3. Una finestra del browser verrà aperto e richiede si toodownload hello file con estensione publishsettings. che contiene informazioni e un certificato per la sottoscrizione di Azure.

    ![Pagina di download del browser](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. Salva file con estensione publishsettings hello.
5. Tipo: `Import-AzurePublishSettingsFile <PathToFile>`, dove `<PathToFile>` è file. publishsettings toohello hello percorso completo.

   Per altre informazioni, vedere [Iniziare a usare i cmdlet di Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).

   Per ulteriori informazioni sull'installazione e configurazione di PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).

## <a name="step-4-upload-hello-vhd-file"></a>Passaggio 4: Caricare il file con estensione vhd hello
Quando si carica file con estensione vhd hello, è possibile inserirlo in un punto qualsiasi all'interno dell'archiviazione Blob. Di seguito sono alcuni dei termini verrà utilizzato quando si carica il file hello.

* **BlobStorageURL** è hello URL hello account di archiviazione creato nel passaggio 2.
* **YourImagesFolder** è il contenitore di hello nell'archiviazione Blob in cui si desidera toostore le immagini.
* **VHDName** è hello etichetta visualizzata nel disco rigido virtuale di hello Azure tooidentify portale classico hello.
* **PathToVHDFile** è hello di percorso completo e il nome del file con estensione vhd hello.

Dalla finestra di PowerShell Azure hello utilizzata nel passaggio precedente hello, digitare:

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a>Passaggio 5: Creare una macchina virtuale con file con estensione vhd caricato hello
Dopo aver caricato i file con estensione vhd hello, è possibile aggiungerlo come un elenco di immagini toohello di immagini personalizzate che sono associati alla sottoscrizione e creare una macchina virtuale con questa immagine personalizzata.

1. Dalla finestra di PowerShell Azure hello utilizzata nel passaggio precedente hello, digitare:

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > Utilizzare Linux come sistema operativo hello. versione di Azure PowerShell corrente Hello accetta solo "Linux" o "Windows" come parametro.
   >
   >
2. Dopo aver completato i passaggi precedenti hello, nuova immagine hello è elencato quando si sceglie di hello **immagini** scheda hello portale di Azure classico.  

    ![Scegli un'immagine](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. Creare una macchina virtuale dalla raccolta hello. La nuova immagine è ora disponibile in **Immagini personali**.
4. Selezionare una nuova immagine di hello. Passare quindi tramite hello tooset di richieste di un nome host, la password, chiave SSH e così via.

    ![Immagine personalizzata](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. Dopo aver completato il provisioning di hello, si noterà FreeBSD VM in esecuzione in Azure.

    ![immagine di FreeBSD in Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
