---
title: Creare e caricare un'immagine della macchina virtuale FreeBSD | Microsoft Docs
description: Informazioni su come creare e caricare un disco rigido virtuale (VHD) che contiene il sistema operativo FreeBSD per creare una macchina virtuale di Azure.
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
ms.openlocfilehash: 918f454784a9676297077c2e94c3e49ab2872d2f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-freebsd-vhd-to-azure"></a><span data-ttu-id="c91ea-103">Creare e caricare un disco rigido virtuale con FreeBSD in Azure</span><span class="sxs-lookup"><span data-stu-id="c91ea-103">Create and upload a FreeBSD VHD to Azure</span></span>
<span data-ttu-id="c91ea-104">Questo articolo descrive come creare e caricare un disco rigido virtuale (VHD) che contiene il sistema operativo FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="c91ea-104">This article shows you how to create and upload a virtual hard disk (VHD) that contains the FreeBSD operating system.</span></span> <span data-ttu-id="c91ea-105">Dopo il caricamento, è possibile usarlo come immagine personalizzata per creare una macchina virtuale in Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-105">After you upload it, you can use it as your own image to create a virtual machine (VM) in Azure.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="c91ea-106">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="c91ea-107">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="c91ea-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="c91ea-108">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="c91ea-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="c91ea-109">Per informazioni sul caricamento di un disco rigido virtuale usando il modello di Resource Manager, vedere [qui](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c91ea-109">For information about uploading a VHD using the Resource Manager model, see [here](../upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c91ea-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c91ea-110">Prerequisites</span></span>
<span data-ttu-id="c91ea-111">In questo articolo si presuppone che l'utente disponga degli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c91ea-111">This article assumes that you have the following items:</span></span>

* <span data-ttu-id="c91ea-112">**Una sottoscrizione Azure**: se non è già disponibile un account, è possibile crearne uno in pochi minuti.</span><span class="sxs-lookup"><span data-stu-id="c91ea-112">**An Azure subscription**--If you don't have an account, you can create one in just a couple of minutes.</span></span> <span data-ttu-id="c91ea-113">Se si ha un abbonamento a MSDN, vedere [Credito Azure mensile per sottoscrittori di Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span><span class="sxs-lookup"><span data-stu-id="c91ea-113">If you have an MSDN subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span> <span data-ttu-id="c91ea-114">Altrimenti, vedere [Crea subito il tuo account Azure gratuito](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c91ea-114">Otherwise, learn how to [create a free trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span>  
* <span data-ttu-id="c91ea-115">**Strumenti di Azure PowerShell**: è necessario che il modulo Microsoft Azure PowerShell sia installato e configurato per usare la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-115">**Azure PowerShell tools**--The Azure PowerShell module must be installed and configured to use your Azure subscription.</span></span> <span data-ttu-id="c91ea-116">Per scaricare il modulo, vedere la pagina dei [download di Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="c91ea-116">To download the module, see [Azure downloads](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="c91ea-117">Qui è disponibile un'esercitazione che descrive come installare e configurare il modulo.</span><span class="sxs-lookup"><span data-stu-id="c91ea-117">A tutorial that describes how to install and configure the module is available here.</span></span> <span data-ttu-id="c91ea-118">Per caricare il disco rigido virtuale usare il cmdlet nella pagina [Download di Azure](https://azure.microsoft.com/downloads/) .</span><span class="sxs-lookup"><span data-stu-id="c91ea-118">Use the [Azure Downloads](https://azure.microsoft.com/downloads/) cmdlet to upload the VHD.</span></span>
* <span data-ttu-id="c91ea-119">**Sistema operativo FreeBSD installato in un file VHD**: è necessario installare un sistema operativo FreeBSD supportato in un disco rigido virtuale.</span><span class="sxs-lookup"><span data-stu-id="c91ea-119">**FreeBSD operating system installed in a .vhd file**--A supported   FreeBSD operating system must be installed to a virtual hard disk.</span></span> <span data-ttu-id="c91ea-120">Sono disponibili vari strumenti per la creazione di file VHD.</span><span class="sxs-lookup"><span data-stu-id="c91ea-120">Multiple tools exist to create .vhd files.</span></span> <span data-ttu-id="c91ea-121">Ad esempio, per creare il file VHD e installare il sistema operativo, è possibile usare soluzioni di virtualizzazione come Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="c91ea-121">For example, you can use a virtualization solution such as Hyper-V to create the .vhd file and install the operating system.</span></span> <span data-ttu-id="c91ea-122">Per istruzioni, vedere su come installare e usare Hyper-V, vedere [Installare Hyper-V e creare una macchina virtuale](http://technet.microsoft.com/library/hh846766.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91ea-122">For instructions about how to install and use Hyper-V, see [Install Hyper-V and create a virtual machine](http://technet.microsoft.com/library/hh846766.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="c91ea-123">Il formato VHDX più recente non è supportato in Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-123">The newer VHDX format is not supported in Azure.</span></span> <span data-ttu-id="c91ea-124">È possibile convertire il disco in formato VHD tramite la console di gestione di Hyper-V o il cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91ea-124">You can convert the disk to VHD format by using Hyper-V Manager or the cmdlet [convert-vhd](https://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="c91ea-125">È disponibile anche un' [esercitazione in MSDN sull'uso di FreeBSD con Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91ea-125">In addition, there is a [tutorial on MSDN about how to use FreeBSD with Hyper-V](http://blogs.msdn.com/b/kylie/archive/2014/12/25/running-freebsd-on-hyper-v.aspx).</span></span>
>
>

<span data-ttu-id="c91ea-126">Questa attività include i cinque passaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="c91ea-126">This task includes the following five steps:</span></span>

## <a name="step-1-prepare-the-image-for-upload"></a><span data-ttu-id="c91ea-127">Passaggio 1: preparare l'immagine da caricare</span><span class="sxs-lookup"><span data-stu-id="c91ea-127">Step 1: Prepare the image for upload</span></span>
<span data-ttu-id="c91ea-128">Dalla macchina virtuale in cui è stato installato il sistema operativo FreeBSD, completare le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="c91ea-128">On the virtual machine where you installed the FreeBSD operating system, complete the following procedures:</span></span>

1. <span data-ttu-id="c91ea-129">Abilitare DHCP.</span><span class="sxs-lookup"><span data-stu-id="c91ea-129">Enable DHCP.</span></span>

        # echo 'ifconfig_hn0="SYNCDHCP"' >> /etc/rc.conf
        # service netif restart
2. <span data-ttu-id="c91ea-130">Abilitare SSH.</span><span class="sxs-lookup"><span data-stu-id="c91ea-130">Enable SSH.</span></span>

    <span data-ttu-id="c91ea-131">Verificare che il server SSH sia installato e configurato per l'esecuzione all'avvio.</span><span class="sxs-lookup"><span data-stu-id="c91ea-131">Ensure that the SSH server is installed and configured to start at boot time.</span></span> <span data-ttu-id="c91ea-132">SSH è abilitato per impostazione predefinita dopo l'installazione dal disco FreeBSD.</span><span class="sxs-lookup"><span data-stu-id="c91ea-132">By default it is enabled after installation from FreeBSD disc.</span></span> 
3. <span data-ttu-id="c91ea-133">Configurare la console seriale.</span><span class="sxs-lookup"><span data-stu-id="c91ea-133">Set up a serial console.</span></span>

        # echo 'console="comconsole vidconsole"' >> /boot/loader.conf
        # echo 'comconsole_speed="115200"' >> /boot/loader.conf
4. <span data-ttu-id="c91ea-134">Installare sudo.</span><span class="sxs-lookup"><span data-stu-id="c91ea-134">Install sudo.</span></span>

    <span data-ttu-id="c91ea-135">L'account radice è disabilitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-135">The root account is disabled in Azure.</span></span> <span data-ttu-id="c91ea-136">Ciò significa che per eseguire comandi con privilegi elevati da un account utente senza privilegi è necessario usare sudo.</span><span class="sxs-lookup"><span data-stu-id="c91ea-136">This means you need to utilize sudo from an unprivileged user to run commands with elevated privileges.</span></span>

        # pkg install sudo
   
5. <span data-ttu-id="c91ea-137">Prerequisiti per l'agente di Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-137">Prerequisites for Azure Agent.</span></span>

        # pkg install python27  
        # pkg install Py27-setuptools  
        # ln -s /usr/local/bin/python2.7 /usr/bin/python   
        # pkg install git
6. <span data-ttu-id="c91ea-138">Installare l'agente di Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-138">Install Azure Agent.</span></span>

    <span data-ttu-id="c91ea-139">L'ultima versione dell'agente di Azure è sempre disponibile in [github](https://github.com/Azure/WALinuxAgent/releases).</span><span class="sxs-lookup"><span data-stu-id="c91ea-139">The latest release of the Azure Agent can always be found on [github](https://github.com/Azure/WALinuxAgent/releases).</span></span> <span data-ttu-id="c91ea-140">La versione 2.0.10+ supporta ufficialmente FreeBSD 10 e 10.1, mentre la versione 2.1.4+ (inclusa la 2.2.x) supporta ufficialmente FreeBSD 10.2 e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="c91ea-140">The version 2.0.10 + officially supports FreeBSD 10 & 10.1, and the version 2.1.4 + (including 2.2.x) officially supports FreeBSD 10.2 and later releases.</span></span>

        # git clone https://github.com/Azure/WALinuxAgent.git  
        # cd WALinuxAgent  
        # git tag  
        …
        WALinuxAgent-2.0.16
        …
        v2.1.4
        v2.1.4.rc0
        v2.1.4.rc1

    <span data-ttu-id="c91ea-141">Per la versione 2.0 verrà usata come esempio la versione 2.0.16:</span><span class="sxs-lookup"><span data-stu-id="c91ea-141">For 2.0, let's use 2.0.16 as an example:</span></span>

        # git checkout WALinuxAgent-2.0.16
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  

    <span data-ttu-id="c91ea-142">Per la versione 2.1 verrà usata come esempio la versione 2.1.4:</span><span class="sxs-lookup"><span data-stu-id="c91ea-142">For 2.1, let's use 2.1.4 as an example:</span></span>

        # git checkout v2.1.4
        # python setup.py install  
        # ln -sf /usr/local/sbin/waagent /usr/sbin/waagent  
        # ln -sf /usr/local/sbin/waagent2.0 /usr/sbin/waagent2.0

   > [!IMPORTANT]
   > <span data-ttu-id="c91ea-143">Dopo aver installato l'agente di Azure, è consigliabile verificare che sia in esecuzione:</span><span class="sxs-lookup"><span data-stu-id="c91ea-143">After you install Azure Agent, it's a good idea to verify that it's running:</span></span>
   >
   >

        # waagent -version
        WALinuxAgent-2.1.4 running on freebsd 10.3
        Python: 2.7.11
        # ps auxw | grep waagent
        root   639   0.0  0.5 104620 17520 u0- I    05:17    0:00.20 python /usr/local/sbin/waagent -daemon (python2.7)
        # cat /var/log/waagent.log
7. <span data-ttu-id="c91ea-144">Eseguire il deprovisioning del sistema.</span><span class="sxs-lookup"><span data-stu-id="c91ea-144">Deprovision the system.</span></span>

    <span data-ttu-id="c91ea-145">Eseguire il deprovisioning del sistema per pulire il sistema e renderlo idoneo per un nuovo provisioning.</span><span class="sxs-lookup"><span data-stu-id="c91ea-145">Deprovision the system to clean it and make it suitable for reprovisioning.</span></span> <span data-ttu-id="c91ea-146">Il comando seguente elimina anche l'ultimo account utente di cui è stato effettuato il provisioning e i dati associati:</span><span class="sxs-lookup"><span data-stu-id="c91ea-146">The following command also deletes the last provisioned user account and the associated data:</span></span>

        # echo "y" |  /usr/local/sbin/waagent -deprovision+user  
        # echo  'waagent_enable="YES"' >> /etc/rc.conf

    <span data-ttu-id="c91ea-147">Ora è possibile arrestare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c91ea-147">Now you can shut down your VM.</span></span>

## <a name="step-2-create-a-storage-account-in-azure"></a><span data-ttu-id="c91ea-148">Passaggio 2: creare un account di archiviazione in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c91ea-148">Step 2: Create a storage account in Azure</span></span>
<span data-ttu-id="c91ea-149">È necessario avere un account di archiviazione di Azure per caricare un file VHD da usare per la creazione di una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="c91ea-149">You need a storage account in Azure to upload a .vhd file so it can be used to create a virtual machine.</span></span> <span data-ttu-id="c91ea-150">Per creare un account di archiviazione, è possibile utilizzare il portale classico di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-150">You can use the Azure classic portal to create a storage account.</span></span>

1. <span data-ttu-id="c91ea-151">Accedere al [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c91ea-151">Sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c91ea-152">Sulla barra dei comandi selezionare **Nuovo**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-152">On the command bar, select **New**.</span></span>
3. <span data-ttu-id="c91ea-153">Fare clic su **Servizi dati** > **Archiviazione** > **Creazione rapida**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-153">Select **Data Services** > **Storage** > **Quick Create**.</span></span>

    ![Creazione rapida di un account di archiviazione](./media/freebsd-create-upload-vhd/Storage-quick-create.png)
4. <span data-ttu-id="c91ea-155">Compilare i campi come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="c91ea-155">Fill out the fields as follows:</span></span>

   * <span data-ttu-id="c91ea-156">In **URL** digitare il nome di un sottodominio da usare nell'URL dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c91ea-156">In the **URL** field, type a subdomain name to use in the storage account URL.</span></span> <span data-ttu-id="c91ea-157">La voce può contenere da 3 a 24 lettere minuscole e numeri.</span><span class="sxs-lookup"><span data-stu-id="c91ea-157">The entry can contain from 3-24 numbers and lowercase letters.</span></span> <span data-ttu-id="c91ea-158">Questo nome diventa il nome host all'interno dell'URL utilizzato per fare riferimento alle risorse di archiviazione BLOB di Azure, archiviazione code di Azure o archiviazione tabelle di Azure per la sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="c91ea-158">This name becomes the host name within the URL that is used to address Azure Blob storage, Azure Queue storage, or Azure Table storage resources for the subscription.</span></span>
   * <span data-ttu-id="c91ea-159">Nel menu a discesa **Località/gruppo di affinità** scegliere la **località o il gruppo di affinità** per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c91ea-159">In the **Location/Affinity Group** drop-down menu, choose the **location or affinity group** for the storage account.</span></span> <span data-ttu-id="c91ea-160">Un gruppo di affinità consente di inserire i servizi cloud e le risorse di archiviazione nello stesso data center.</span><span class="sxs-lookup"><span data-stu-id="c91ea-160">An affinity group lets you put your cloud services and storage in the same data center.</span></span>
   * <span data-ttu-id="c91ea-161">Nel campo **Replica** decidere se usare la replica **Con ridondanza geografica** per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c91ea-161">In the **Replication** field, decide whether to use **Geo-Redundant** replication for the storage account.</span></span> <span data-ttu-id="c91ea-162">La replica geografica è attivata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="c91ea-162">Geo-replication is turned on by default.</span></span> <span data-ttu-id="c91ea-163">Se questa opzione è selezionata, i dati vengono replicati in una posizione secondaria, senza alcun costo aggiuntivo, per garantire il failover a tale posizione qualora si verifichi un errore grave nella posizione primaria.</span><span class="sxs-lookup"><span data-stu-id="c91ea-163">This option replicates your data to a secondary location, at no cost to you, so that your storage fails over to that location if a major failure occurs at the primary location.</span></span> <span data-ttu-id="c91ea-164">La località secondaria viene assegnata automaticamente e non può essere modificata.</span><span class="sxs-lookup"><span data-stu-id="c91ea-164">The secondary location is assigned automatically and can't be changed.</span></span> <span data-ttu-id="c91ea-165">Se è necessario un maggiore controllo sulla posizione dell'archiviazione basata sul cloud a causa di requisiti legali o criteri dell'organizzazione, è possibile disattivare la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="c91ea-165">If you need more control over the location of your cloud-based storage due to legal requirements or organizational policy, you can turn off geo-replication.</span></span> <span data-ttu-id="c91ea-166">Tenere presente che se si attiva la replica geografica in un momento successivo, verrà addebitato un corrispettivo di trasferimento dati una tantum per la replica dei dati esistenti nella posizione secondaria.</span><span class="sxs-lookup"><span data-stu-id="c91ea-166">However, be aware that if you later turn on geo-replication, you will be charged a one-time data transfer fee to replicate your existing data to the secondary location.</span></span> <span data-ttu-id="c91ea-167">I servizi di archiviazione senza replica geografica sono offerti a un prezzo scontato.</span><span class="sxs-lookup"><span data-stu-id="c91ea-167">Storage services without geo-replication are offered at a discount.</span></span> <span data-ttu-id="c91ea-168">Altri dettagli sulla gestione della replica geografica degli account di archiviazione sono disponibili nell'articolo [Replica dell'archiviazione di Azure](../../../storage/common/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="c91ea-168">More details about managing geo-replication of storage accounts can be found here: [Azure Storage replication](../../../storage/common/storage-redundancy.md).</span></span>

     ![Immissione dei dettagli dell'account di archiviazione](./media/freebsd-create-upload-vhd/Storage-create-account.png)
5. <span data-ttu-id="c91ea-170">Fai clic su **Crea account di archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-170">Select **Create Storage Account**.</span></span> <span data-ttu-id="c91ea-171">L'account verrà visualizzato in **Archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-171">The account now appears under **storage**.</span></span>

    ![Creazione dell'account di archiviazione completata](./media/freebsd-create-upload-vhd/Storagenewaccount.png)
6. <span data-ttu-id="c91ea-173">Creare quindi un contenitore per i VHD caricati.</span><span class="sxs-lookup"><span data-stu-id="c91ea-173">Next, create a container for your uploaded .vhd files.</span></span> <span data-ttu-id="c91ea-174">Selezionare il nome dell'account di archiviazione e quindi **Contenitori**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-174">Select the storage account name, and then select **Containers**.</span></span>

    ![Dettaglio dell'account di archiviazione](./media/freebsd-create-upload-vhd/storageaccount_detail.png)
7. <span data-ttu-id="c91ea-176">Selezionare **Crea contenitore**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-176">Select **Create a Container**.</span></span>

    ![Dettaglio dell'account di archiviazione](./media/freebsd-create-upload-vhd/storageaccount_container.png)
8. <span data-ttu-id="c91ea-178">Nel campo **Nome** digitare un nome per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="c91ea-178">In the **Name** field, type a name for your container.</span></span> <span data-ttu-id="c91ea-179">Quindi nel menu a discesa **Accesso** selezionare il tipo di criteri di accesso desiderato.</span><span class="sxs-lookup"><span data-stu-id="c91ea-179">Then, in the **Access** drop-down menu, select what type of access policy you want.</span></span>

    ![Nome del contenitore](./media/freebsd-create-upload-vhd/storageaccount_containervalues.png)

   > [!NOTE]
   > <span data-ttu-id="c91ea-181">Per impostazione predefinita, il contenitore è privato ed è accessibile solo al proprietario dell'account.</span><span class="sxs-lookup"><span data-stu-id="c91ea-181">By default, the container is private and can only be accessed by the account owner.</span></span> <span data-ttu-id="c91ea-182">Per consentire l'accesso pubblico in lettura ai BLOB nel contenitore, ma non alle proprietà e ai metadati del contenitore, usare l'opzione **BLOB pubblico** .</span><span class="sxs-lookup"><span data-stu-id="c91ea-182">To allow public read access to the blobs in the container, but not to the container properties and metadata, use the **Public Blob** option.</span></span> <span data-ttu-id="c91ea-183">Per consentire l'accesso in lettura pubblico completo per contenitori e BLOB, usare l'opzione **Contenitore pubblico** .</span><span class="sxs-lookup"><span data-stu-id="c91ea-183">To allow full public read access for the container and blobs, use the **Public Container** option.</span></span>
   >
   >

## <a name="step-3-prepare-the-connection-to-azure"></a><span data-ttu-id="c91ea-184">Passaggio 3: preparare la connessione a Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c91ea-184">Step 3: Prepare the connection to Azure</span></span>
<span data-ttu-id="c91ea-185">Prima di poter caricare un file VHD, è necessario stabilire una connessione sicura tra il computer e la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-185">Before you can upload a .vhd file, you need to establish a secure connection between your computer and your Azure subscription.</span></span> <span data-ttu-id="c91ea-186">A questo scopo, è possibile usare il metodo basato su Azure Active Directory (Azure AD) o sul certificato.</span><span class="sxs-lookup"><span data-stu-id="c91ea-186">You can use the Azure Active Directory (Azure AD) method or the certificate method to do it.</span></span>

### <a name="use-the-azure-ad-method-to-upload-a-vhd-file"></a><span data-ttu-id="c91ea-187">Usare il metodo Azure AD per caricare un file VHD</span><span class="sxs-lookup"><span data-stu-id="c91ea-187">Use the Azure AD method to upload a .vhd file</span></span>
1. <span data-ttu-id="c91ea-188">Aprire la console di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c91ea-188">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="c91ea-189">Digitare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c91ea-189">Type the following command:</span></span>  
    `Add-AzureAccount`

    <span data-ttu-id="c91ea-190">Questo comando consente di aprire una finestra in cui è possibile eseguire l'accesso con l'account aziendale o dell'istituto di istruzione.</span><span class="sxs-lookup"><span data-stu-id="c91ea-190">This command opens a sign-in window where you can sign in with your work or school account.</span></span>

    ![Finestra di PowerShell](./media/freebsd-create-upload-vhd/add_azureaccount.png)
3. <span data-ttu-id="c91ea-192">Le informazioni delle credenziali vengono autenticate e salvate in Azure,</span><span class="sxs-lookup"><span data-stu-id="c91ea-192">Azure authenticates and saves the credential information.</span></span> <span data-ttu-id="c91ea-193">quindi la finestra viene chiusa.</span><span class="sxs-lookup"><span data-stu-id="c91ea-193">Then it closes the window.</span></span>

### <a name="use-the-certificate-method-to-upload-a-vhd-file"></a><span data-ttu-id="c91ea-194">Usare il metodo basato sul certificato per caricare un file VHD</span><span class="sxs-lookup"><span data-stu-id="c91ea-194">Use the certificate method to upload a .vhd file</span></span>
1. <span data-ttu-id="c91ea-195">Aprire la console di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c91ea-195">Open the Azure PowerShell console.</span></span>
2. <span data-ttu-id="c91ea-196">Digitare `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="c91ea-196">Type:  `Get-AzurePublishSettingsFile`.</span></span>
3. <span data-ttu-id="c91ea-197">Viene aperta una finestra del browser in cui viene chiesto se scaricare il file con estensione publishsettings,</span><span class="sxs-lookup"><span data-stu-id="c91ea-197">A browser window opens and prompts you to download the .publishsettings file.</span></span> <span data-ttu-id="c91ea-198">che contiene informazioni e un certificato per la sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-198">This file contains information and a certificate for your Azure subscription.</span></span>

    ![Pagina di download del browser](./media/freebsd-create-upload-vhd/Browser_download_GetPublishSettingsFile.png)
4. <span data-ttu-id="c91ea-200">Salvare il file .publishsettings.</span><span class="sxs-lookup"><span data-stu-id="c91ea-200">Save the .publishsettings file.</span></span>
5. <span data-ttu-id="c91ea-201">Digitare `Import-AzurePublishSettingsFile <PathToFile>`, dove `<PathToFile>` è il percorso completo del file con estensione publishsettings.</span><span class="sxs-lookup"><span data-stu-id="c91ea-201">Type:  `Import-AzurePublishSettingsFile <PathToFile>`, where `<PathToFile>` is the full path to the .publishsettings file.</span></span>

   <span data-ttu-id="c91ea-202">Per altre informazioni, vedere [Iniziare a usare i cmdlet di Azure](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span><span class="sxs-lookup"><span data-stu-id="c91ea-202">For more information, see [Get started with Azure cmdlets](http://msdn.microsoft.com/library/windowsazure/jj554332.aspx).</span></span>

   <span data-ttu-id="c91ea-203">Per altre informazioni sull'installazione e la configurazione di Azure PowerShell, vedere [Come installare e configurare Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="c91ea-203">For more information about installing and configuring PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="step-4-upload-the-vhd-file"></a><span data-ttu-id="c91ea-204">Passaggio 4: caricare il file VHD</span><span class="sxs-lookup"><span data-stu-id="c91ea-204">Step 4: Upload the .vhd file</span></span>
<span data-ttu-id="c91ea-205">È possibile caricare il file VHD in qualsiasi posizione all'interno dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="c91ea-205">When you upload the .vhd file, you can place it anywhere within your Blob storage.</span></span> <span data-ttu-id="c91ea-206">Di seguito sono riportati alcuni termini che verranno usati durante il caricamento del file:</span><span class="sxs-lookup"><span data-stu-id="c91ea-206">Following are some terms you will use when you upload the file:</span></span>

* <span data-ttu-id="c91ea-207">**BlobStorageURL** è l'URL dell'account di archiviazione creato nel passaggio 2.</span><span class="sxs-lookup"><span data-stu-id="c91ea-207">**BlobStorageURL** is the URL for the storage account that you created in Step 2.</span></span>
* <span data-ttu-id="c91ea-208">**YourImagesFolder** è il contenitore all'interno dell'archivio BLOB in cui si vogliono archiviare le immagini.</span><span class="sxs-lookup"><span data-stu-id="c91ea-208">**YourImagesFolder** is the container within Blob storage where you want to store your images.</span></span>
* <span data-ttu-id="c91ea-209">**VHDName** è l'etichetta che identifica il disco rigido virtuale visualizzata nel portale di Azure classico.</span><span class="sxs-lookup"><span data-stu-id="c91ea-209">**VHDName** is the label that appears in the Azure classic portal to identify the virtual hard disk.</span></span>
* <span data-ttu-id="c91ea-210">**PathToVHDFile** è il percorso completo e il nome del file VHD.</span><span class="sxs-lookup"><span data-stu-id="c91ea-210">**PathToVHDFile** is the full path and name of the .vhd file.</span></span>

<span data-ttu-id="c91ea-211">Nella finestra di Azure PowerShell usata nel passaggio precedente, digitare:</span><span class="sxs-lookup"><span data-stu-id="c91ea-211">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVhd -Destination "<BlobStorageURL>/<YourImagesFolder>/<VHDName>.vhd" -LocalFilePath <PathToVHDFile>

## <a name="step-5-create-a-vm-with-the-uploaded-vhd-file"></a><span data-ttu-id="c91ea-212">Passaggio 5: Creare una macchina virtuale con il file VHD caricato</span><span class="sxs-lookup"><span data-stu-id="c91ea-212">Step 5: Create a VM with the uploaded .vhd file</span></span>
<span data-ttu-id="c91ea-213">Dopo avere caricato il file VHD, è possibile aggiungerlo come immagine all'elenco di immagini personalizzate associate alla propria sottoscrizione e creare una macchina virtuale con questa immagine personalizzata.</span><span class="sxs-lookup"><span data-stu-id="c91ea-213">After you upload the .vhd file, you can add it as an image to the list of custom images that are associated with your subscription and create a virtual machine with this custom image.</span></span>

1. <span data-ttu-id="c91ea-214">Nella finestra di Azure PowerShell usata nel passaggio precedente, digitare:</span><span class="sxs-lookup"><span data-stu-id="c91ea-214">From the Azure PowerShell window you used in the previous step, type:</span></span>

        Add-AzureVMImage -ImageName <Your Image's Name> -MediaLocation <location of the VHD> -OS <Type of the OS on the VHD>

   > [!NOTE]
   > <span data-ttu-id="c91ea-215">Usare Linux come tipo di sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c91ea-215">Use Linux as the OS type.</span></span> <span data-ttu-id="c91ea-216">La versione corrente di Azure PowerShell accetta solo "Linux" o "Windows" come parametro.</span><span class="sxs-lookup"><span data-stu-id="c91ea-216">The current Azure PowerShell version accepts only “Linux” or “Windows” as a parameter.</span></span>
   >
   >
2. <span data-ttu-id="c91ea-217">Una volta completati i passaggi precedenti, quando si seleziona la scheda **Immagini** nel portale di Azure classico, la nuova immagine risulta inclusa nell'elenco.</span><span class="sxs-lookup"><span data-stu-id="c91ea-217">After you complete the previous steps, the new image is listed when you choose the **Images** tab on the Azure classic portal.</span></span>  

    ![Scegli un'immagine](./media/freebsd-create-upload-vhd/addfreebsdimage.png)
3. <span data-ttu-id="c91ea-219">Creare una macchina virtuale dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="c91ea-219">Create a virtual machine from the gallery.</span></span> <span data-ttu-id="c91ea-220">La nuova immagine è ora disponibile in **Immagini personali**.</span><span class="sxs-lookup"><span data-stu-id="c91ea-220">This new image is now available under **My Images**.</span></span>
4. <span data-ttu-id="c91ea-221">Selezionare la nuova immagine.</span><span class="sxs-lookup"><span data-stu-id="c91ea-221">Select the new image.</span></span> <span data-ttu-id="c91ea-222">Seguire quindi le istruzioni visualizzate per configurare nome host, password/chiave SSH e così via.</span><span class="sxs-lookup"><span data-stu-id="c91ea-222">Next, go through the prompts to set up a host name, password, SSH key, and so on.</span></span>

    ![Immagine personalizzata](./media/freebsd-create-upload-vhd/createfreebsdimageinazure.png)
5. <span data-ttu-id="c91ea-224">Dopo avere completato il provisioning, la macchina virtuale FreeBSD in esecuzione sarà visibile in Azure.</span><span class="sxs-lookup"><span data-stu-id="c91ea-224">After you complete the provisioning, you'll see your FreeBSD VM running in Azure.</span></span>

    ![immagine di FreeBSD in Azure](./media/freebsd-create-upload-vhd/freebsdimageinazure.png)
