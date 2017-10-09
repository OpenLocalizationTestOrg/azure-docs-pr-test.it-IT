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
# <a name="create-and-upload-a-freebsd-vhd-tooazure"></a><span data-ttu-id="fbf44-103">Creare e caricare un tooAzure FreeBSD VHD</span><span class="sxs-lookup"><span data-stu-id="fbf44-103">Create and upload a FreeBSD VHD tooAzure</span></span>
<span data-ttu-id="fbf44-104">Questo articolo illustra come toocreate e caricare un disco rigido virtuale (VHD) che contiene hello FreeBSD del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fbf44-104">This article shows you how toocreate and upload a virtual hard disk (VHD) that contains hello FreeBSD operating system.</span></span> <span data-ttu-id="fbf44-105">Dopo aver caricato il, è possibile utilizzare, come la propria toocreate immagine una macchina virtuale (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-105">After you upload it, you can use it as your own image toocreate a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="fbf44-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="fbf44-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="fbf44-107">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="fbf44-108">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="fbf44-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="fbf44-109">Per informazioni sul caricamento di un disco rigido virtuale utilizzando il modello di gestione risorse hello, vedere [qui](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fbf44-109">For information about uploading a VHD using hello Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbf44-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="fbf44-110">Prerequisites</span></span>
<span data-ttu-id="fbf44-111">Questo articolo si presuppone di aver hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="fbf44-111">This article assumes that you have hello following items:</span></span>

* <span data-ttu-id="fbf44-112">**Una sottoscrizione Azure**: se non è già disponibile un account, è possibile crearne uno in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="fbf44-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="fbf44-113">Se si ha un abbonamento a MSDN, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="fbf44-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="fbf44-114">In caso contrario, informazioni su come troppo[creare un account di prova](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="fbf44-114">Otherwise, learn how too[create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="fbf44-115">**Strumenti di Azure PowerShell**-modulo di Azure PowerShell hello deve essere installato e configurato toouse la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-115">**Azure PowerShell tools**--hello Azure PowerShell module must be installed and configured toouse your Azure subscription.</span></span> <span data-ttu-id="fbf44-116">modulo hello toodownload, vedere [download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="fbf44-116">toodownload hello module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="fbf44-117">In questa esercitazione viene descritto come tooinstall e configurare il modulo di hello è disponibile qui.</span><span class="sxs-lookup"><span data-stu-id="fbf44-117">A tutorial that describes how tooinstall and configure hello module is available here.</span></span> <span data-ttu-id="fbf44-118">Hello utilizzare [download di Azure](https://azure.microsoft.com/downloads/) hello tooupload cmdlet disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbf44-118">Use hello [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet tooupload hello VHD.</span></span>
* <span data-ttu-id="fbf44-119">**Sistema operativo FreeBSD installato in un file con estensione vhd**disco rigido virtuale tooa: il sistema operativo di FreeBSD supportato deve essere installato.</span><span class="sxs-lookup"><span data-stu-id="fbf44-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed tooa virtual hard disk.</span></span> <span data-ttu-id="fbf44-120">Più strumenti esistono toocreate file con estensione vhd.</span><span class="sxs-lookup"><span data-stu-id="fbf44-120">Multiple tools exist toocreate .vhd files.</span></span> <span data-ttu-id="fbf44-121">Ad esempio, è possibile usare una soluzione di virtualizzazione, ad esempio file con estensione vhd di Hyper-V toocreate hello e installare hello del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="fbf44-121">For example, you can use a virtualization solution such as Hyper-V toocreate hello .vhd file and install hello operating system.</span></span> <span data-ttu-id="fbf44-122">Per istruzioni su come tooinstall e utilizzare Hyper-V, vedere [installare Hyper-V e creare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbf44-122">For instructions about how tooinstall and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="fbf44-123">il formato VHDX più recente di Hello non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-123">hello newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="fbf44-124">È possibile convertire il formato di tooVHD di hello disco tramite la gestione di Hyper-V o hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbf44-124">You can convert hello disk tooVHD format by using Hyper-V Manager or hello cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="fbf44-125">Inoltre, è un [esercitazione su MSDN sul toouse FreeBSD con Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbf44-125">In addition, there is a [tutorial on MSDN about how toouse FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="fbf44-126">Questa attività include hello cinque passaggi:</span><span class="sxs-lookup"><span data-stu-id="fbf44-126">This task includes hello following five steps:</span></span>

## <a name="step-1-prepare-hello-image-for-upload"></a><span data-ttu-id="fbf44-127">Passaggio 1: Preparare l'immagine di hello per il caricamento</span><span class="sxs-lookup"><span data-stu-id="fbf44-127">Step 1: Prepare hello image for upload</span></span>
<span data-ttu-id="fbf44-128">Nella macchina virtuale hello in cui è installato hello FreeBSD del sistema operativo, completare hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="fbf44-128">On hello virtual machine where you installed hello FreeBSD operating system, complete hello following procedures:</span></span>

1. <span data-ttu-id="fbf44-129">Abilitare DHCP.</span><span class="sxs-lookup"><span data-stu-id="fbf44-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="fbf44-130">Abilitare SSH.</span><span class="sxs-lookup"><span data-stu-id="fbf44-130">Enable SSH.</span></span>

    <span data-ttu-id="fbf44-131">Verificare che server SSH hello sia installato e configurato toostart in fase di avvio.</span><span class="sxs-lookup"><span data-stu-id="fbf44-131">Ensure that hello SSH server is installed and configured toostart at boot time.</span></span> <span data-ttu-id="fbf44-132">SSH è abilitato per impostazione predefinita dopo l'installazione dal disco FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="fbf44-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="fbf44-133">Configurare la console seriale.</span><span class="sxs-lookup"><span data-stu-id="fbf44-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="fbf44-134">Installare sudo.</span><span class="sxs-lookup"><span data-stu-id="fbf44-134">Install sudo.</span></span>

    <span data-ttu-id="fbf44-135">account radice Hello è disabilitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-135">hello root account is disabled in Azure.</span></span> <span data-ttu-id="fbf44-136">Ciò significa che è necessario sudo tooutilize dai comandi di toorun utente senza privilegi con privilegi elevati.</span><span class="sxs-lookup"><span data-stu-id="fbf44-136">This means you need tooutilize sudo from an unprivileged user toorun commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="fbf44-137">Prerequisiti per l'agente di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="fbf44-138">Installare l'agente di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-138">Install Azure Agent.</span></span>

    <span data-ttu-id="fbf44-139">Hello versione più recente dell'agente di Azure hello è sempre disponibile nel [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="fbf44-139">hello latest release of hello Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="fbf44-140">Hello versione 2.0.10 + supporta ufficialmente 10 FreeBSD & 10.1 e la versione di hello 2.1.4 + (inclusi 2.2) supporta ufficialmente 10.2 FreeBSD e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="fbf44-140">hello version 2.0.10 + officially supports FreeBSD 10 & 10.1, and hello version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="fbf44-141">Per la versione 2.0 verrà usata come esempio la versione 2.0.16:</span><span class="sxs-lookup"><span data-stu-id="fbf44-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="fbf44-142">Per la versione 2.1 verrà usata come esempio la versione 2.1.4:</span><span class="sxs-lookup"><span data-stu-id="fbf44-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="fbf44-143">Dopo aver installato l'agente di Azure, è un tooverify buona norma che è in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="fbf44-143">After you install Azure Agent, it's a good idea tooverify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="fbf44-144">Eseguire il deprovisioning sistema hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-144">Deprovision hello system.</span></span>

    <span data-ttu-id="fbf44-145">Deprovisioning hello tooclean di sistema e verificare che è adatto per la riconfigurazione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-145">Deprovision hello system tooclean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="fbf44-146">Hello seguente comando Elimina inoltre ultimo account di provisioning utente hello e dati hello associata:</span><span class="sxs-lookup"><span data-stu-id="fbf44-146">hello following command also deletes hello last provisioned user account and hello associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="fbf44-147">Ora è possibile arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbf44-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="fbf44-148">Passaggio 2: creare un account di archiviazione in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="fbf44-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="fbf44-149">È necessario un account di archiviazione in Azure tooupload un file con estensione vhd in modo da poterli toocreate usato una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="fbf44-149">You need a storage account in Azure tooupload a .vhd file so it can be used toocreate a virtual machine.</span></span> <span data-ttu-id="fbf44-150">È possibile utilizzare hello Azure toocreate portale classico un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-150">You can use hello Azure classic portal toocreate a storage account.</span></span>

1. <span data-ttu-id="fbf44-151">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="fbf44-151">Sign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="fbf44-152">Nella barra dei comandi di hello, selezionare **New**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-152">On hello command bar, select **New**.</span></span>
3. <span data-ttu-id="fbf44-153">Fare clic su **Servizi dati** > **Archiviazione** > **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Creazione rapida di un account di archiviazione](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="fbf44-155">Compilare i campi hello come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="fbf44-155">Fill out hello fields as follows:</span></span>

   * <span data-ttu-id="fbf44-156">In hello **URL** , digitare un toouse nome di sottodominio in hello URL di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-156">In hello **URL** field, type a subdomain name toouse in hello storage account URL.</span></span> <span data-ttu-id="fbf44-157">voce Hello può contenere da 3 a 24 numeri e lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="fbf44-157">hello entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="fbf44-158">Questo nome diventa il nome host hello in URL hello tooaddress usato nell'archiviazione Blob di Azure, l'archiviazione delle code di Azure o le risorse di archiviazione tabelle di Azure per sottoscrizione hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-158">This name becomes hello host name within hello URL that is used tooaddress Azure Blob storage, Azure Queue storage, or Azure Table storage resources for hello subscription.</span></span>
   * <span data-ttu-id="fbf44-159">In hello **posizione/gruppo di affinità** dal menu a discesa scegliere hello **percorso o gruppo di affinità** hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-159">In hello **Location/Affinity Group** drop-down menu, choose hello **location or affinity group** for hello storage account.</span></span> <span data-ttu-id="fbf44-160">Un gruppo di affinità consente di inserire i servizi cloud e archiviazione in hello nello stesso data center.</span><span class="sxs-lookup"><span data-stu-id="fbf44-160">An affinity group lets you put your cloud services and storage in hello same data center.</span></span>
   * <span data-ttu-id="fbf44-161">In hello **replica** campo, decidere se toouse **con ridondanza geografica** replica hello account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-161">In hello **Replication** field, decide whether toouse **Geo-Redundant** replication for hello storage account.</span></span> <span data-ttu-id="fbf44-162">La replica geografica è attivata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fbf44-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="fbf44-163">Questa opzione consente di replicare i dati tooa posizione secondaria, in tooyou alcun costo, si verifica in modo che lo spazio di archiviazione viene eseguito il failover toothat percorso se un errore grave nella posizione primaria hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-163">This option replicates your data tooa secondary location, at no cost tooyou, so that your storage fails over toothat location if a major failure occurs at hello primary location.</span></span> <span data-ttu-id="fbf44-164">percorso secondario Hello viene assegnato automaticamente e non può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="fbf44-164">hello secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="fbf44-165">Se è necessario maggiore controllo sulla posizione hello dello spazio di archiviazione basato su cloud a causa di requisiti toolegal o criteri dell'organizzazione, è possibile disattivare la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="fbf44-165">If you need more control over hello location of your cloud-based storage due toolegal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="fbf44-166">Tuttavia, tenere presente che se si attiva in un secondo momento replica geo, verranno addebitati una sola volta tooreplicate tariffa di trasferimento dei dati del percorso secondario toohello dati esistente.</span><span class="sxs-lookup"><span data-stu-id="fbf44-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee tooreplicate your existing data toohello secondary location.</span></span> <span data-ttu-id="fbf44-167">I servizi di archiviazione senza replica geografica sono offerti a un prezzo scontato.</span><span class="sxs-lookup"><span data-stu-id="fbf44-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="fbf44-168">Altri dettagli sulla gestione della replica geografica degli account di archiviazione sono disponibili nell'articolo [Replica dell'archiviazione di Azure](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="fbf44-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Immissione dei dettagli dell'account di archiviazione](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="fbf44-170">Fai clic su **Crea account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="fbf44-171">Hello account viene visualizzato in **archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-171">hello account now appears under **storage**.</span></span>

    ![Creazione dell'account di archiviazione completata](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="fbf44-173">Creare quindi un contenitore per i VHD caricati.</span><span class="sxs-lookup"><span data-stu-id="fbf44-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="fbf44-174">Nome account di archiviazione hello, scegliere quindi **contenitori**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-174">Select hello storage account name, and then select **Containers**.</span></span>

    ![Dettaglio dell'account di archiviazione](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="fbf44-176">Selezionare **Crea contenitore**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-176">Select **Create a Container**.</span></span>

    ![Dettaglio dell'account di archiviazione](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="fbf44-178">In hello **nome** , digitare un nome per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="fbf44-178">In hello **Name** field, type a name for your container.</span></span> <span data-ttu-id="fbf44-179">Quindi, nel hello **accesso** -menu a discesa, seleziona il tipo di criterio di accesso desiderato.</span><span class="sxs-lookup"><span data-stu-id="fbf44-179">Then, in hello **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nome contenitore](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="fbf44-181">Per impostazione predefinita, il contenitore di hello è privato e accessibile solo dal proprietario dell'account hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-181">By default, hello container is private and can only be accessed by hello account owner.</span></span> <span data-ttu-id="fbf44-182">tooallow accesso in lettura pubblico toohello BLOB nel contenitore di hello, ma non le proprietà del contenitore toohello e i metadati, usare hello **Blob pubblici** opzione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-182">tooallow public read access toohello blobs in hello container, but not toohello container properties and metadata, use hello **Public Blob** option.</span></span> <span data-ttu-id="fbf44-183">accesso in lettura pubblico completo tooallow per hello contenitori e BLOB, utilizzare hello **contenitore pubblico** opzione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-183">tooallow full public read access for hello container and blobs, use hello **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-hello-connection-tooazure"></a><span data-ttu-id="fbf44-184">Passaggio 3: Preparare hello connessione tooAzure</span><span class="sxs-lookup"><span data-stu-id="fbf44-184">Step 3: Prepare hello connection tooAzure</span></span>
<span data-ttu-id="fbf44-185">Prima di poter caricare un file con estensione vhd, è necessario tooestablish una connessione sicura tra il computer e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-185">Before you can upload a .vhd file, you need tooestablish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="fbf44-186">È possibile utilizzare il metodo di Azure Active Directory (Azure AD) hello o hello certificato metodo toodo è.</span><span class="sxs-lookup"><span data-stu-id="fbf44-186">You can use hello Azure Active Directory (Azure AD) method or hello certificate method toodo it.</span></span>

### <a name="use-hello-azure-ad-method-tooupload-a-vhd-file"></a><span data-ttu-id="fbf44-187">Utilizzare tooupload metodo hello Azure AD un file con estensione vhd</span><span class="sxs-lookup"><span data-stu-id="fbf44-187">Use hello Azure AD method tooupload a .vhd file</span></span>
1. <span data-ttu-id="fbf44-188">Console di hello aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbf44-188">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="fbf44-189">Digitare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="fbf44-189">Type hello following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="fbf44-190">Questo comando consente di aprire una finestra in cui è possibile eseguire l'accesso con l'account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="fbf44-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Finestra di PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="fbf44-192">Azure autentica e Salva le informazioni sulle credenziali hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-192">Azure authenticates and saves hello credential information.</span></span> <span data-ttu-id="fbf44-193">Quindi chiude la finestra hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-193">Then it closes hello window.</span></span>

### <a name="use-hello-certificate-method-tooupload-a-vhd-file"></a><span data-ttu-id="fbf44-194">Utilizzare tooupload di metodo hello certificato un file con estensione vhd</span><span class="sxs-lookup"><span data-stu-id="fbf44-194">Use hello certificate method tooupload a .vhd file</span></span>
1. <span data-ttu-id="fbf44-195">Console di hello aprire Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fbf44-195">Open hello Azure PowerShell console.</span></span>
2. <span data-ttu-id="fbf44-196">Digitare `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="fbf44-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="fbf44-197">Una finestra del browser verrà aperto e richiede si toodownload hello file con estensione publishsettings.</span><span class="sxs-lookup"><span data-stu-id="fbf44-197">A browser window opens and prompts you toodownload hello .publishsettings file.</span></span> <span data-ttu-id="fbf44-198">che contiene informazioni e un certificato per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Pagina di download del browser](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="fbf44-200">Salva file con estensione publishsettings hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-200">Save hello .publishsettings file.</span></span>
5. <span data-ttu-id="fbf44-201">Tipo: `Import-AzurePublishSettingsFile <PathToFile>`, dove `<PathToFile>` è file. publishsettings toohello hello percorso completo.</span><span class="sxs-lookup"><span data-stu-id="fbf44-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is hello full path toohello .publishsettings file.</span></span>

   <span data-ttu-id="fbf44-202">Per altre informazioni, vedere [Iniziare a usare i cmdlet di Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="fbf44-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="fbf44-203">Per ulteriori informazioni sull'installazione e configurazione di PowerShell, vedere [come tooinstall e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fbf44-203">For more information about installing and configuring PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-hello-vhd-file"></a><span data-ttu-id="fbf44-204">Passaggio 4: Caricare il file con estensione vhd hello</span><span class="sxs-lookup"><span data-stu-id="fbf44-204">Step 4: Upload hello .vhd file</span></span>
<span data-ttu-id="fbf44-205">Quando si carica file con estensione vhd hello, è possibile inserirlo in un punto qualsiasi all'interno dell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="fbf44-205">When you upload hello .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="fbf44-206">Di seguito sono alcuni dei termini verrà utilizzato quando si carica il file hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-206">Following are some terms you will use when you upload hello file:</span></span>

* <span data-ttu-id="fbf44-207">**BlobStorageURL** è hello URL hello account di archiviazione creato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="fbf44-207">**BlobStorageURL** is hello URL for hello storage account that you created in Step 2.</span></span>
* <span data-ttu-id="fbf44-208">**YourImagesFolder** è il contenitore di hello nell'archiviazione Blob in cui si desidera toostore le immagini.</span><span class="sxs-lookup"><span data-stu-id="fbf44-208">**YourImagesFolder** is hello container within Blob storage where you want toostore your images.</span></span>
* <span data-ttu-id="fbf44-209">**VHDName** è hello etichetta visualizzata nel disco rigido virtuale di hello Azure tooidentify portale classico hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-209">**VHDName** is hello label that appears in hello Azure classic portal tooidentify hello virtual hard disk.</span></span>
* <span data-ttu-id="fbf44-210">**PathToVHDFile** è hello di percorso completo e il nome del file con estensione vhd hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-210">**PathToVHDFile** is hello full path and name of hello .vhd file.</span></span>

<span data-ttu-id="fbf44-211">Dalla finestra di PowerShell Azure hello utilizzata nel passaggio precedente hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="fbf44-211">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-hello-uploaded-vhd-file"></a><span data-ttu-id="fbf44-212">Passaggio 5: Creare una macchina virtuale con file con estensione vhd caricato hello</span><span class="sxs-lookup"><span data-stu-id="fbf44-212">Step 5: Create a VM with hello uploaded .vhd file</span></span>
<span data-ttu-id="fbf44-213">Dopo aver caricato i file con estensione vhd hello, è possibile aggiungerlo come un elenco di immagini toohello di immagini personalizzate che sono associati alla sottoscrizione e creare una macchina virtuale con questa immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="fbf44-213">After you upload hello .vhd file, you can add it as an image toohello list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="fbf44-214">Dalla finestra di PowerShell Azure hello utilizzata nel passaggio precedente hello, digitare:</span><span class="sxs-lookup"><span data-stu-id="fbf44-214">From hello Azure PowerShell window you used in hello previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of hello VHD> -OS <Type of hello OS on hello VHD>

   > [!NOTE]
   > <span data-ttu-id="fbf44-215">Utilizzare Linux come sistema operativo hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-215">Use Linux as hello OS type.</span></span> <span data-ttu-id="fbf44-216">versione di Azure PowerShell corrente Hello accetta solo "Linux" o "Windows" come parametro.</span><span class="sxs-lookup"><span data-stu-id="fbf44-216">hello current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="fbf44-217">Dopo aver completato i passaggi precedenti hello, nuova immagine hello è elencato quando si sceglie di hello **immagini** scheda hello portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="fbf44-217">After you complete hello previous steps, hello new image is listed when you choose hello **Images** tab on hello Azure classic portal.</span></span>  

    ![Scegli un'immagine](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="fbf44-219">Creare una macchina virtuale dalla raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-219">Create a virtual machine from hello gallery.</span></span> <span data-ttu-id="fbf44-220">La nuova immagine è ora disponibile in **Immagini personali**.</span><span class="sxs-lookup"><span data-stu-id="fbf44-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="fbf44-221">Selezionare una nuova immagine di hello.</span><span class="sxs-lookup"><span data-stu-id="fbf44-221">Select hello new image.</span></span> <span data-ttu-id="fbf44-222">Passare quindi tramite hello tooset di richieste di un nome host, la password, chiave SSH e così via.</span><span class="sxs-lookup"><span data-stu-id="fbf44-222">Next, go through hello prompts tooset up a host name, password, SSH key, and so on.</span></span>

    ![Immagine personalizzata](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="fbf44-224">Dopo aver completato il provisioning di hello, si noterà FreeBSD VM in esecuzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="fbf44-224">After you complete hello provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![immagine di FreeBSD in Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
