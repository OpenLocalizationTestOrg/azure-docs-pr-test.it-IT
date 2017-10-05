---
title: Reimpostare la password e la chiave SSH di VM Linux dall'interfaccia della riga di comando | Microsoft Docs
description: Come usare l'estensione VMAccess dall'interfaccia della riga di comando di Azure per reimpostare la password o la chiave SSH di una VM Linux, correggere la configurazione SSH e verificare la coerenza dei dischi
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
ms.openlocfilehash: 74765877e7836d6878284b350a25d8355dc83d7d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="f11f3-103">Come reimpostare la password o la chiave SSH di una VM Linux, correggere la configurazione SSH e verificare la coerenza dei dischi che utilizzano l'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="f11f3-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="f11f3-104">Se non è possibile connettersi a una macchina virtuale Linux su Azure perché si è dimenticata la password o una chiave SSH (Secure Shell) non è valida o per un problema di configurazione di SSH, usare l'estensione VMAccessForLinux con l'interfaccia della riga di comando di Azure per reimpostare la password o la chiave SSH, correggere la configurazione SSH e verificare la coerenza del disco.</span><span class="sxs-lookup"><span data-stu-id="f11f3-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="f11f3-105">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f11f3-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f11f3-106">Questo articolo illustra l'uso del modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="f11f3-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f11f3-107">Microsoft consiglia di usare il modello di Gestione risorse per le distribuzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="f11f3-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f11f3-108">Informazioni su come [eseguire questa procedura con il modello di Resource Manager](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="f11f3-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="f11f3-109">Con l'interfaccia della riga di comando di Azure, per accedere ai comandi si usa il comando **azure vm extension set** dell'interfaccia della riga di comando (Bash, terminale, prompt dei comandi).</span><span class="sxs-lookup"><span data-stu-id="f11f3-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="f11f3-110">Per informazioni dettagliate sull'uso dell'estensione, eseguire **azure help vm extension set** .</span><span class="sxs-lookup"><span data-stu-id="f11f3-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="f11f3-111">Con l’interfaccia della riga di comando di Azure è possibile eseguire le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="f11f3-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="f11f3-112">Reimpostare la password</span><span class="sxs-lookup"><span data-stu-id="f11f3-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="f11f3-113">Reimpostare la chiave SSH</span><span class="sxs-lookup"><span data-stu-id="f11f3-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="f11f3-114">Reimpostare la password e la chiave SSH</span><span class="sxs-lookup"><span data-stu-id="f11f3-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="f11f3-115">Creare un nuovo account utente sudo</span><span class="sxs-lookup"><span data-stu-id="f11f3-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="f11f3-116">Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="f11f3-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="f11f3-117">Eliminare un utente</span><span class="sxs-lookup"><span data-stu-id="f11f3-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="f11f3-118">Visualizzare lo stato dell'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="f11f3-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="f11f3-119">Verificare la coerenza dei dischi aggiunti</span><span class="sxs-lookup"><span data-stu-id="f11f3-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="f11f3-120">Ripristinare i dischi aggiunti nella VM Linux</span><span class="sxs-lookup"><span data-stu-id="f11f3-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="f11f3-121">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f11f3-121">Prerequisites</span></span>
<span data-ttu-id="f11f3-122">Sarà necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f11f3-122">You will need to do the following:</span></span>

* <span data-ttu-id="f11f3-123">Sarà necessario [installare l'interfaccia della riga di comando di Azure](../../../cli-install-nodejs.md) e [connettersi alla proprio sottoscrizione](../../../xplat-cli-connect.md) per usare le risorse di Azure associate al proprio account.</span><span class="sxs-lookup"><span data-stu-id="f11f3-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="f11f3-124">Impostare la modalità corretta per il modello di distribuzione classico digitando quanto segue al prompt dei comandi:</span><span class="sxs-lookup"><span data-stu-id="f11f3-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="f11f3-125">Procurarsi una nuova password o un set di chiavi SSH, se si desidera reimpostare l'una o l'altro.</span><span class="sxs-lookup"><span data-stu-id="f11f3-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="f11f3-126">Queste non saranno necessarie se si vuole reimpostare la configurazione di SSH.</span><span class="sxs-lookup"><span data-stu-id="f11f3-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <span data-ttu-id="f11f3-127"><a name="pwresetcli"></a>Reimpostare la password</span><span class="sxs-lookup"><span data-stu-id="f11f3-127"><a name="pwresetcli"></a>Reset the password</span></span>
1. <span data-ttu-id="f11f3-128">Creare un file denominato PrivateConf.json nel computer locale con queste righe.</span><span class="sxs-lookup"><span data-stu-id="f11f3-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="f11f3-129">Sostituire **myUserName** e  **myP@ssW0rd**  con il proprio nome utente e password e impostare la data di scadenza.</span><span class="sxs-lookup"><span data-stu-id="f11f3-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="f11f3-130">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <span data-ttu-id="f11f3-131"><a name="sshkeyresetcli"></a>Reimpostare la chiave SSH</span><span class="sxs-lookup"><span data-stu-id="f11f3-131"><a name="sshkeyresetcli"></a>Reset the SSH key</span></span>
1. <span data-ttu-id="f11f3-132">Creare un file denominato PrivateConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="f11f3-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="f11f3-133">Sostituire i valori **myUserName** e **mySSHKey** con le proprie informazioni.</span><span class="sxs-lookup"><span data-stu-id="f11f3-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="f11f3-134">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <span data-ttu-id="f11f3-135"><a name="resetbothcli"></a>Reimpostare sia la password sia la chiave SSH</span><span class="sxs-lookup"><span data-stu-id="f11f3-135"><a name="resetbothcli"></a>Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="f11f3-136">Creare un file denominato PrivateConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="f11f3-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="f11f3-137">Sostituire i valori **myUserName**, **mySSHKey** e **myP@ssW0rd** con le proprie informazioni.</span><span class="sxs-lookup"><span data-stu-id="f11f3-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="f11f3-138">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="f11f3-139"><a name="createnewsudocli"></a>Creare un nuovo account utente sudo</span><span class="sxs-lookup"><span data-stu-id="f11f3-139"><a name="createnewsudocli"></a>Create a new sudo user account</span></span>

<span data-ttu-id="f11f3-140">Se si dimentica il nome utente, è possibile usare VMAccess per crearne uno nuovo con privilegi sudo.</span><span class="sxs-lookup"><span data-stu-id="f11f3-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="f11f3-141">In questo caso, il nome utente e la password esistenti non verranno modificati.</span><span class="sxs-lookup"><span data-stu-id="f11f3-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="f11f3-142">Per creare un nuovo utente sudo con accesso tramite password, usare lo script in [Reimpostare la password](#pwresetcli) e specificare il nuovo nome utente.</span><span class="sxs-lookup"><span data-stu-id="f11f3-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="f11f3-143">Per creare un nuovo utente sudo con accesso tramite chiave SSH, usare lo script in [Reimpostare la chiave SSH](#sshkeyresetcli) e specificare il nuovo nome utente.</span><span class="sxs-lookup"><span data-stu-id="f11f3-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="f11f3-144">È inoltre possibile usare [Reimpostare la password e la chiave SSH](#resetbothcli) per creare un nuovo utente con accesso tramite password e chiave SSH.</span><span class="sxs-lookup"><span data-stu-id="f11f3-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <span data-ttu-id="f11f3-145"><a name="sshconfigresetcli"></a>Reimpostare la configurazione SSH</span><span class="sxs-lookup"><span data-stu-id="f11f3-145"><a name="sshconfigresetcli"></a>Reset the SSH configuration</span></span>
<span data-ttu-id="f11f3-146">Se la configurazione SSH è in uno stato indesiderato, si potrebbe perdere anche l'accesso alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f11f3-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="f11f3-147">È possibile usare l'estensione VMAccess per reimpostare la configurazione allo stato predefinito.</span><span class="sxs-lookup"><span data-stu-id="f11f3-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="f11f3-148">A tale scopo, è sufficiente impostare la chiave "reset_ssh" su "True".</span><span class="sxs-lookup"><span data-stu-id="f11f3-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="f11f3-149">L'estensione riavvia il server SSH, apre la porta SSH nella VM e ripristina la configurazione SSH predefinita.</span><span class="sxs-lookup"><span data-stu-id="f11f3-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="f11f3-150">L'account utente (nome, password o chiavi SSH) non verrà modificato.</span><span class="sxs-lookup"><span data-stu-id="f11f3-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="f11f3-151">Il file di configurazione SSH che viene reimpostato si trova in /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="f11f3-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="f11f3-152">Creare un file denominato PrivateConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="f11f3-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="f11f3-153">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="f11f3-154"><a name="deletecli"></a>Eliminare un utente</span><span class="sxs-lookup"><span data-stu-id="f11f3-154"><a name="deletecli"></a>Delete a user</span></span>
<span data-ttu-id="f11f3-155">Se si desidera eliminare un account utente senza accedere alla macchina virtuale direttamente, è possibile usare questo script.</span><span class="sxs-lookup"><span data-stu-id="f11f3-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="f11f3-156">Creare un file denominato PrivateConf.json con questo contenuto, sostituendo il nome utente da rimuovere in **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="f11f3-157">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <span data-ttu-id="f11f3-158"><a name="statuscli"></a>Visualizzare lo stato dell'estensione VMAccess</span><span class="sxs-lookup"><span data-stu-id="f11f3-158"><a name="statuscli"></a>Display the status of the VMAccess extension</span></span>
<span data-ttu-id="f11f3-159">Per visualizzare lo stato dell'estensione VMAccess, eseguire questo comando.</span><span class="sxs-lookup"><span data-stu-id="f11f3-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <span data-ttu-id="f11f3-160"><a name='checkdisk'></a>Verificare la coerenza dei dischi aggiunti</span><span class="sxs-lookup"><span data-stu-id="f11f3-160"><a name='checkdisk'></a>Check consistency of added disks</span></span>
<span data-ttu-id="f11f3-161">Per eseguire fsck su tutti i dischi nella macchina virtuale Linux, è necessario eseguire le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="f11f3-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="f11f3-162">Creare un file denominato PublicConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="f11f3-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="f11f3-163">Il controllo del disco accetta un valore booleano che indica se controllare o meno i dischi collegati alla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f11f3-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="f11f3-164">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <span data-ttu-id="f11f3-165"><a name='repairdisk'></a>Riparare i dischi</span><span class="sxs-lookup"><span data-stu-id="f11f3-165"><a name='repairdisk'></a>Repair disks</span></span>
<span data-ttu-id="f11f3-166">Per ripristinare i dischi che presentano problemi di montaggio o errori di configurazione di montaggio, usare l'estensione VMAccess per reimpostare la configurazione di montaggio nella macchina virtuale Linux.</span><span class="sxs-lookup"><span data-stu-id="f11f3-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="f11f3-167">Sostituire il nome del disco in **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="f11f3-168">Creare un file denominato PublicConf.json con questo contenuto.</span><span class="sxs-lookup"><span data-stu-id="f11f3-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="f11f3-169">Eseguire questo comando, sostituendo il nome della macchina virtuale in **myVM**.</span><span class="sxs-lookup"><span data-stu-id="f11f3-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="f11f3-170">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f11f3-170">Next steps</span></span>
* <span data-ttu-id="f11f3-171">Se per reimpostare la password o la chiave SSH, correggere la configurazione SSH e verificare la coerenza dei dischi si vogliono usare cmdlet Azure PowerShell o modelli di Azure Resource Manager, vedere la [documentazione dell'estensione VMAccess in GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="f11f3-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="f11f3-172">Per reimpostare la password o la chiave SSH di una VM Linux distribuita con il modello di distribuzione classica è anche possibile usare il [portale di Azure](https://portal.azure.com) .</span><span class="sxs-lookup"><span data-stu-id="f11f3-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="f11f3-173">Non è attualmente possibile usare il portale per eseguire queste operazioni per una VM Linux distribuita con il modello di distribuzione Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="f11f3-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="f11f3-174">Per altre informazioni sull'uso di estensioni VM per macchine virtuali di Azure vedere [Informazioni sulle estensioni e sulle funzionalità delle macchine virtuali](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f11f3-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

