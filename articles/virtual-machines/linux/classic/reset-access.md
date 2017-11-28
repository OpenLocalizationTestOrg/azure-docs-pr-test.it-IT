---
title: aaaReset password VM Linux e SSH chiave hello CLI | Documenti Microsoft
description: Come correggere configurazione SSH hello hello toouse estensione VMAccess da hello Azure interfaccia della riga di comando (CLI) tooreset una password di Linux VM o una chiave SSH e verificare la coerenza del disco
services: virtual-machines-linux
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 1650ad64fb982627ae9f90b1a8209bb56bac7004
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-a-linux-vm-password-or-ssh-key-fix-hello-ssh-configuration-and-check-disk-consistency-using-hello-vmaccess-extension"></a><span data-ttu-id="d3dfe-103">Come tooreset una password di Linux VM o una chiave SSH, correggere configurazione SSH hello e verificare la coerenza del disco tramite l'estensione VMAccess hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-103">How tooreset a Linux VM password or SSH key, fix hello SSH configuration, and check disk consistency using hello VMAccess extension</span></span>
<span data-ttu-id="d3dfe-104">Se non è possibile connettersi macchina virtuale di Linux tooa in Azure a causa di una password dimenticata, una chiave non corretta di Secure Shell (SSH) o un problema con la configurazione SSH hello, utilizzare l'estensione VMAccessForLinux hello con hello Azure CLI tooreset hello password o chiave SSH, correggere Hello configurazione SSH, quindi verificare la coerenza del disco.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-104">If you can't connect tooa Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with hello SSH configuration, use hello VMAccessForLinux extension with hello Azure CLI tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="d3dfe-105">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d3dfe-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d3dfe-106">In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-106">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="d3dfe-107">Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-107">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="d3dfe-108">Informazioni su come troppo[eseguire questi passaggi tramite il modello di gestione risorse di hello](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="d3dfe-108">Learn how too[perform these steps using hello Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="d3dfe-109">Con hello CLI di Azure, utilizzare hello **set di estensioni di macchina virtuale di azure** comando dai comandi di tooaccess interfaccia della riga di comando (Bash, Terminal, prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="d3dfe-109">With hello Azure CLI, you use hello **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) tooaccess commands.</span></span> <span data-ttu-id="d3dfe-110">Per informazioni dettagliate sull'uso dell'estensione, eseguire **azure help vm extension set** .</span><span class="sxs-lookup"><span data-stu-id="d3dfe-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="d3dfe-111">Con hello CLI di Azure, è possibile eseguire hello quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d3dfe-111">With hello Azure CLI, you can do hello following tasks:</span></span>

* [<span data-ttu-id="d3dfe-112">Reimpostare la password di hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-112">Reset hello password</span></span>](#pwresetcli)
* [<span data-ttu-id="d3dfe-113">Reimpostare la chiave SSH hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-113">Reset hello SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="d3dfe-114">Reimpostare la chiave SSH password e hello hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-114">Reset hello password and hello SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="d3dfe-115">Creare un nuovo account utente sudo</span><span class="sxs-lookup"><span data-stu-id="d3dfe-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="d3dfe-116">Reimposta configurazione SSH hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-116">Reset hello SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="d3dfe-117">Eliminare un utente</span><span class="sxs-lookup"><span data-stu-id="d3dfe-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="d3dfe-118">Visualizzare lo stato di hello di hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="d3dfe-118">Display hello status of hello VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="d3dfe-119">Verificare la coerenza dei dischi aggiunti</span><span class="sxs-lookup"><span data-stu-id="d3dfe-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="d3dfe-120">Ripristinare i dischi aggiunti nella VM Linux</span><span class="sxs-lookup"><span data-stu-id="d3dfe-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="d3dfe-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d3dfe-121">Prerequisites</span></span>
<span data-ttu-id="d3dfe-122">È necessario seguente hello toodo:</span><span class="sxs-lookup"><span data-stu-id="d3dfe-122">You will need toodo hello following:</span></span>

* <span data-ttu-id="d3dfe-123">Sarà necessario troppo[installare hello Azure CLI](../../../cli-install-nodejs.md) e [connettere sottoscrizione tooyour](../../../xplat-cli-connect.md) toouse Azure le risorse associate all'account.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-123">You will need too[install hello Azure CLI](../../../cli-install-nodejs.md) and [connect tooyour subscription](../../../xplat-cli-connect.md) toouse Azure resources associated with your account.</span></span>
* <span data-ttu-id="d3dfe-124">Impostare la modalità corretta per il modello di distribuzione classica hello hello digitando hello segue al prompt dei comandi di hello:</span><span class="sxs-lookup"><span data-stu-id="d3dfe-124">Set hello correct mode for hello classic deployment model by typing hello following at hello command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="d3dfe-125">Disporre di una nuova password o un set di chiavi SSH, se si desidera tooreset dei due.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-125">Have a new password or set of SSH keys, if you want tooreset either one.</span></span> <span data-ttu-id="d3dfe-126">Questi non sono necessari se si desidera tooreset hello SSH configurazione.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-126">You don't need these if you want tooreset hello SSH configuration.</span></span>

## <span data-ttu-id="d3dfe-127"><a name="pwresetcli"></a>Reimpostare la password di hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-127"><a name="pwresetcli"></a>Reset hello password</span></span>
1. <span data-ttu-id="d3dfe-128">Creare un file denominato PrivateConf.json nel computer locale con queste righe.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="d3dfe-129">Sostituire **myUserName** e  **myP@ssW0rd**  con il proprio nome utente e password e impostare la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="d3dfe-130">Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-130">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="d3dfe-131"><a name="sshkeyresetcli"></a>Reimpostare la chiave SSH hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-131"><a name="sshkeyresetcli"></a>Reset hello SSH key</span></span>
1. <span data-ttu-id="d3dfe-132">Creare un file denominato PrivateConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="d3dfe-133">Sostituire hello **myUserName** e **mySSHKey** valori con le proprie informazioni.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-133">Replace hello **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="d3dfe-134">Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-134">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="d3dfe-135"><a name="resetbothcli"></a>Reimpostare la chiave SSH hello e la password di hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-135"><a name="resetbothcli"></a>Reset both hello password and hello SSH key</span></span>
1. <span data-ttu-id="d3dfe-136">Creare un file denominato PrivateConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="d3dfe-137">Sostituire hello **myUserName**, **mySSHKey** e  **myP@ssW0rd**  valori con le proprie informazioni.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-137">Replace hello **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="d3dfe-138">Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-138">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="d3dfe-139"><a name="createnewsudocli"></a>Creare un nuovo account utente sudo</span><span class="sxs-lookup"><span data-stu-id="d3dfe-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="d3dfe-140">Se si dimentica il nome utente, è possibile utilizzare uno nuovo con autorità sudo hello toocreate VMAccess.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-140">If you forget your user name, you can use VMAccess toocreate a new one with hello sudo authority.</span></span> <span data-ttu-id="d3dfe-141">In questo caso, hello esistente nome utente e password non verranno modificate.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-141">In this case, hello existing user name and password will not be modified.</span></span>

<span data-ttu-id="d3dfe-142">un nuovo utente sudo con accesso con password, utilizzare script hello toocreate [hello di reimpostazione password](#pwresetcli) e specificare nuovi nome utente di hello.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-142">toocreate a new sudo user with password access, use hello script in [Reset hello password](#pwresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="d3dfe-143">un nuovo utente sudo con accesso alla chiave SSH, utilizza script di hello in toocreate [la chiave SSH hello reimpostazione](#sshkeyresetcli) e specificare nuovi nome utente di hello.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-143">toocreate a new sudo user with SSH key access, use hello script in [Reset hello SSH key](#sshkeyresetcli) and specify hello new user name.</span></span>

<span data-ttu-id="d3dfe-144">È inoltre possibile utilizzare [reimpostare password hello e chiave SSH hello](#resetbothcli) toocreate un nuovo utente con accesso alla chiave SSH e la password.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-144">You can also use [Reset hello password and hello SSH key](#resetbothcli) toocreate a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="d3dfe-145"><a name="sshconfigresetcli"></a>Reimposta configurazione SSH hello</span><span class="sxs-lookup"><span data-stu-id="d3dfe-145"><a name="sshconfigresetcli"></a>Reset hello SSH configuration</span></span>
<span data-ttu-id="d3dfe-146">Se in uno stato indesiderato configurazione SSH hello, si potrebbe perdere anche l'accesso toohello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-146">If hello SSH configuration is in an undesired state, you might also lose access toohello VM.</span></span> <span data-ttu-id="d3dfe-147">È possibile utilizzare hello VMAccess estensione tooreset hello configurazione tooits stato predefinito.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-147">You can use hello VMAccess extension tooreset hello configuration tooits default state.</span></span> <span data-ttu-id="d3dfe-148">toodo in tal caso, è sufficiente chiave di "reset_ssh" hello tooset troppo "True".</span><span class="sxs-lookup"><span data-stu-id="d3dfe-148">toodo so, you just need tooset hello “reset_ssh” key too“True”.</span></span> <span data-ttu-id="d3dfe-149">estensione Hello verrà riavviare i server SSH hello, aprire la porta SSH hello nella VM e reimpostare i valori hello SSH configurazione toodefault.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-149">hello extension will restart hello SSH server, open hello SSH port on your VM, and reset hello SSH configuration toodefault values.</span></span> <span data-ttu-id="d3dfe-150">account utente di Hello (nome, la password o le chiavi SSH) non verranno modificate.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-150">hello user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="d3dfe-151">file di configurazione di SSH Hello reimpostato si trova in /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-151">hello SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="d3dfe-152">Creare un file denominato PrivateConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="d3dfe-153">Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-153">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="d3dfe-154"><a name="deletecli"></a>Eliminare un utente</span><span class="sxs-lookup"><span data-stu-id="d3dfe-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="d3dfe-155">Se si desidera toodelete un account utente senza registrazione direttamente toohello VM, è possibile utilizzare questo script.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-155">If you want toodelete a user account without logging into toohello VM directly, you can use this script.</span></span>

1. <span data-ttu-id="d3dfe-156">Creare un file denominato PrivateConf.json con questo contenuto, sostituendo hello utente nome tooremove per **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-156">Create a file named PrivateConf.json with this content, substituting hello user name tooremove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="d3dfe-157">Eseguire questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-157">Run this command, substituting hello name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="d3dfe-158"><a name="statuscli"></a>Visualizzare lo stato di hello di hello estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="d3dfe-158"><a name="statuscli"></a>Display hello status of hello VMAccess extension</span></span>
<span data-ttu-id="d3dfe-159">stato hello toodisplay di hello estensione VMAccess, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-159">toodisplay hello status of hello VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="d3dfe-160"><a name='checkdisk'></a>Verificare la coerenza dei dischi aggiunti</span><span class="sxs-lookup"><span data-stu-id="d3dfe-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="d3dfe-161">sfck toorun su tutti i dischi nella macchina virtuale di Linux, è necessario seguente hello toodo:</span><span class="sxs-lookup"><span data-stu-id="d3dfe-161">toorun fsck on all disks in your Linux virtual machine, you will need toodo hello following:</span></span>

1. <span data-ttu-id="d3dfe-162">Creare un file denominato PublicConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="d3dfe-163">Controllo disco accetta un valore booleano per se toocheck dischi associato macchina virtuale tooyour o meno.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-163">Check Disk takes a boolean for whether toocheck disks attached tooyour virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="d3dfe-164">Eseguire tooexecute questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-164">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="d3dfe-165"><a name='repairdisk'></a>Riparare i dischi</span><span class="sxs-lookup"><span data-stu-id="d3dfe-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="d3dfe-166">i dischi toorepair che non vengono montato o presentano errori di configurazione di montaggio, utilizzare configurazione di montaggio hello tooreset estensione VMAccess hello sulla macchina virtuale di Linux.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-166">toorepair disks that are not mounting or have mount configuration errors, use hello VMAccess extension tooreset hello mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="d3dfe-167">Nome hello sostituendo del disco per **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-167">Substituting hello name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="d3dfe-168">Creare un file denominato PublicConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="d3dfe-169">Eseguire tooexecute questo comando, sostituendo il nome della macchina virtuale per hello **myVM**.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-169">Run this command tooexecute, substituting hello name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="d3dfe-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d3dfe-170">Next steps</span></span>
* <span data-ttu-id="d3dfe-171">Se si desidera toouse cmdlet di Azure PowerShell o la password di Azure Resource Manager modelli tooreset hello o chiave SSH, correggere la configurazione SSH, hello e verificare la coerenza del disco, vedere hello [documentazione estensione VMAccess su GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="d3dfe-171">If you want toouse Azure PowerShell cmdlets or Azure Resource Manager templates tooreset hello password or SSH key, fix hello SSH configuration, and check disk consistency, see hello [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="d3dfe-172">È inoltre possibile utilizzare hello [portale di Azure](https://portal.azure.com) tooreset hello password o una chiave SSH di una VM Linux distribuito nel modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-172">You can also use hello [Azure portal](https://portal.azure.com) tooreset hello password or SSH key of a Linux VM deployed in hello classic deployment model.</span></span> <span data-ttu-id="d3dfe-173">Non è possibile utilizzare hello portale toothis per una VM Linux distribuito nel modello di distribuzione di gestione risorse di hello.</span><span class="sxs-lookup"><span data-stu-id="d3dfe-173">You can't currently use hello portal do toothis for a Linux VM deployed in hello Resource Manager deployment model.</span></span>
* <span data-ttu-id="d3dfe-174">Per altre informazioni sull'uso di estensioni VM per macchine virtuali di Azure vedere [Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3dfe-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

