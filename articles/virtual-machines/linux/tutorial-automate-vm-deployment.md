---
title: Personalizzare una macchina virtuale Linux al primo avvio in Azure | Microsoft Docs
description: Informazioni su come usare cloud-init e Key Vault per personalizzare le macchine virtuali Linux al primo avvio in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: 6adf4e43aa80c28c6f5f8d8a071966323ba85723
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-customize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="9d92e-103">Personalizzare una macchina virtuale al primo avvio</span><span class="sxs-lookup"><span data-stu-id="9d92e-103">How to customize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="9d92e-104">In un'esercitazione precedente si è appreso come eseguire una connessione SSH a una macchina virtuale (VM) e come installare manualmente NGINX.</span><span class="sxs-lookup"><span data-stu-id="9d92e-104">In a previous tutorial, you learned how to SSH to a virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="9d92e-105">Per creare macchine virtuali in modo rapido e coerente, di norma è consigliabile una qualche forma di automazione.</span><span class="sxs-lookup"><span data-stu-id="9d92e-105">To create VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="9d92e-106">Un approccio comune per personalizzare una macchina virtuale al primo avvio consiste nell'usare [cloud-init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="9d92e-106">A common approach to customize a VM on first boot is to use [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="9d92e-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="9d92e-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d92e-108">Creare un file di configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="9d92e-109">Creare una macchina virtuale che usa un file cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="9d92e-110">Visualizzare un'esecuzione dell'app Node.js dopo aver creato la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9d92e-110">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="9d92e-111">Usare Key Vault per archiviare in modo sicuro i certificati</span><span class="sxs-lookup"><span data-stu-id="9d92e-111">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="9d92e-112">Automatizzare le distribuzioni sicure di NGINX con cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9d92e-113">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="9d92e-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9d92e-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="9d92e-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="9d92e-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9d92e-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="9d92e-116">Panoramica di cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-116">Cloud-init overview</span></span>
<span data-ttu-id="9d92e-117">[Cloud-init](https://cloudinit.readthedocs.io) è un approccio diffuso per personalizzare una macchina virtuale Linux al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="9d92e-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="9d92e-118">Cloud-init consente di installare pacchetti e scrivere file o configurare utenti e impostazioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="9d92e-118">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="9d92e-119">Quando cloud-init viene eseguito durante il processo di avvio iniziale non vi sono altri passaggi o agenti necessari per applicare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="9d92e-119">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="9d92e-120">Cloud-init funziona anche fra distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="9d92e-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="9d92e-121">Ad esempio, non si usa **apt-get install** o **yum install** per installare un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="9d92e-121">For example, you don't use **apt-get install** or **yum install** to install a package.</span></span> <span data-ttu-id="9d92e-122">In alternativa, è possibile definire un elenco di pacchetti da installare.</span><span class="sxs-lookup"><span data-stu-id="9d92e-122">Instead you can define a list of packages to install.</span></span> <span data-ttu-id="9d92e-123">Cloud-init userà automaticamente lo strumento di gestione del pacchetto nativo per la distribuzione selezionata.</span><span class="sxs-lookup"><span data-stu-id="9d92e-123">Cloud-init automatically uses the native package management tool for the distro you select.</span></span>

<span data-ttu-id="9d92e-124">Microsoft collabora con i partner per promuovere l'inclusione e il funzionamento di cloud-init con le immagini da essi fornite per Azure.</span><span class="sxs-lookup"><span data-stu-id="9d92e-124">We are working with our partners to get cloud-init included and working in the images that they provide to Azure.</span></span> <span data-ttu-id="9d92e-125">La tabella seguente illustra l'attuale disponibilità di cloud-init nelle immagini della piattaforma Azure:</span><span class="sxs-lookup"><span data-stu-id="9d92e-125">The following table outlines the current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="9d92e-126">Alias</span><span class="sxs-lookup"><span data-stu-id="9d92e-126">Alias</span></span> | <span data-ttu-id="9d92e-127">Autore</span><span class="sxs-lookup"><span data-stu-id="9d92e-127">Publisher</span></span> | <span data-ttu-id="9d92e-128">Offerta</span><span class="sxs-lookup"><span data-stu-id="9d92e-128">Offer</span></span> | <span data-ttu-id="9d92e-129">SKU</span><span class="sxs-lookup"><span data-stu-id="9d92e-129">SKU</span></span> | <span data-ttu-id="9d92e-130">Versione</span><span class="sxs-lookup"><span data-stu-id="9d92e-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="9d92e-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="9d92e-131">UbuntuLTS</span></span> |<span data-ttu-id="9d92e-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="9d92e-132">Canonical</span></span> |<span data-ttu-id="9d92e-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9d92e-133">UbuntuServer</span></span> |<span data-ttu-id="9d92e-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="9d92e-134">16.04-LTS</span></span> |<span data-ttu-id="9d92e-135">più recenti</span><span class="sxs-lookup"><span data-stu-id="9d92e-135">latest</span></span> |
| <span data-ttu-id="9d92e-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="9d92e-136">UbuntuLTS</span></span> |<span data-ttu-id="9d92e-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="9d92e-137">Canonical</span></span> |<span data-ttu-id="9d92e-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="9d92e-138">UbuntuServer</span></span> |<span data-ttu-id="9d92e-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="9d92e-139">14.04.5-LTS</span></span> |<span data-ttu-id="9d92e-140">più recenti</span><span class="sxs-lookup"><span data-stu-id="9d92e-140">latest</span></span> |
| <span data-ttu-id="9d92e-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9d92e-141">CoreOS</span></span> |<span data-ttu-id="9d92e-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9d92e-142">CoreOS</span></span> |<span data-ttu-id="9d92e-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="9d92e-143">CoreOS</span></span> |<span data-ttu-id="9d92e-144">Stabile</span><span class="sxs-lookup"><span data-stu-id="9d92e-144">Stable</span></span> |<span data-ttu-id="9d92e-145">più recenti</span><span class="sxs-lookup"><span data-stu-id="9d92e-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="9d92e-146">Creare un file di configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-146">Create cloud-init config file</span></span>
<span data-ttu-id="9d92e-147">Per visualizzare cloud-init in azione, creare una macchina virtuale, installare NGINX ed eseguire una semplice app Node.js "Hello World".</span><span class="sxs-lookup"><span data-stu-id="9d92e-147">To see cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="9d92e-148">La configurazione cloud-init seguente installa i pacchetti necessari, crea un'applicazione Node.js, quindi inizializza e avvia l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="9d92e-148">The following cloud-init configuration installs the required packages, creates a Node.js app, then initialize and starts the app.</span></span>

<span data-ttu-id="9d92e-149">Nella shell corrente creare un file denominato *cloud-init.txt* e incollare la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="9d92e-149">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="9d92e-150">Ad esempio, creare il file in Cloud Shell anziché nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="9d92e-150">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="9d92e-151">È possibile usare qualsiasi editor.</span><span class="sxs-lookup"><span data-stu-id="9d92e-151">You can use any editor you wish.</span></span> <span data-ttu-id="9d92e-152">Immettere `sensible-editor cloud-init.txt` per creare il file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="9d92e-152">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="9d92e-153">Assicurarsi che l'intero file cloud-init venga copiato correttamente, in particolare la prima riga:</span><span class="sxs-lookup"><span data-stu-id="9d92e-153">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

<span data-ttu-id="9d92e-154">Per altre informazioni sulle opzioni di configurazione di cloud-init, vedere gli [esempi di configurazione di cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="9d92e-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="9d92e-155">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9d92e-155">Create virtual machine</span></span>
<span data-ttu-id="9d92e-156">Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="9d92e-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="9d92e-157">Nell'esempio seguente viene creato un gruppo di risorse denominato *myResourceGroupAutomate* nella posizione *eastus*:</span><span class="sxs-lookup"><span data-stu-id="9d92e-157">The following example creates a resource group named *myResourceGroupAutomate* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="9d92e-158">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9d92e-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9d92e-159">Usare il parametro `--custom-data` per specificare il file di configurazione di cloud-init.</span><span class="sxs-lookup"><span data-stu-id="9d92e-159">Use the `--custom-data` parameter to pass in your cloud-init config file.</span></span> <span data-ttu-id="9d92e-160">Se il file è stato salvato all'esterno della directory di lavoro corrente, specificare il percorso completo della configurazione *cloud-init.txt* .</span><span class="sxs-lookup"><span data-stu-id="9d92e-160">Provide the full path to the *cloud-init.txt* config if you saved the file outside of your present working directory.</span></span> <span data-ttu-id="9d92e-161">L'esempio seguente crea una macchina virtuale denominata *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="9d92e-161">The following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="9d92e-162">Per creare la macchina virtuale, installare i pacchetti e avviare l'applicazione sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9d92e-162">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="9d92e-163">Sono presenti attività in background la cui esecuzione continua dopo che l'interfaccia della riga di comando di Azure è tornata al prompt.</span><span class="sxs-lookup"><span data-stu-id="9d92e-163">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="9d92e-164">Potrebbe trascorrere ancora qualche minuto prima che sia possibile accedere all'app.</span><span class="sxs-lookup"><span data-stu-id="9d92e-164">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="9d92e-165">Dopo aver creato la macchina virtuale, prendere nota del `publicIpAddress` visualizzato dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d92e-165">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="9d92e-166">Questo indirizzo viene usato per accedere all'app Node.js tramite un Web browser.</span><span class="sxs-lookup"><span data-stu-id="9d92e-166">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="9d92e-167">Per consentire al traffico Web di raggiungere la macchina virtuale, aprire la porta 80 da Internet con il comando [az vm open_port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="9d92e-167">To allow web traffic to reach your VM, open port 80 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="9d92e-168">Testare l'app Web</span><span class="sxs-lookup"><span data-stu-id="9d92e-168">Test web app</span></span>
<span data-ttu-id="9d92e-169">È ora possibile aprire un Web browser e immettere *http://<publicIpAddress>* nella barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="9d92e-169">Now you can open a web browser and enter *http://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="9d92e-170">Fornire il proprio indirizzo IP pubblico dal processo di creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d92e-170">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="9d92e-171">L'app Node.js viene visualizzata come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9d92e-171">Your Node.js app is displayed as in the following example:</span></span>

![Visualizzare il sito NGINX in esecuzione](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="9d92e-173">Inserire certificati da Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d92e-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="9d92e-174">Questa sezione facoltativa illustra come archiviare in modo protetto i certificati in Azure Key Vault e inserirli durante la distribuzione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d92e-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during the VM deployment.</span></span> <span data-ttu-id="9d92e-175">Anziché usare un'immagine personalizzata che includa i certificati integrati, questo processo assicura che i certificati aggiornati vengano inseriti in una macchina virtuale al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="9d92e-175">Rather than using a custom image that includes the certificates baked-in, this process ensures that the most up-to-date certificates are injected to a VM on first boot.</span></span> <span data-ttu-id="9d92e-176">Durante il processo, il certificato non lascia mai la piattaforma Azure e non viene mai esposto in uno script, in una cronologia della riga di comando o in un modello.</span><span class="sxs-lookup"><span data-stu-id="9d92e-176">During the process, the certificate never leaves the Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="9d92e-177">Azure Key Vault consente di proteggere chiavi crittografiche e segreti, come certificati e password.</span><span class="sxs-lookup"><span data-stu-id="9d92e-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="9d92e-178">Key Vault semplifica il processo di gestione delle chiavi e consente di mantenere il controllo delle chiavi che accedono ai dati e li crittografano.</span><span class="sxs-lookup"><span data-stu-id="9d92e-178">Key Vault helps streamline the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="9d92e-179">Questo scenario introduce alcuni concetti chiave di Key Vault per creare e usare un certificato, sebbene non rappresenti una panoramica esaustiva sull'uso di Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9d92e-179">This scenario introduces some Key Vault concepts to create and use a certificate, though is not an exhaustive overview on how to use Key Vault.</span></span>

<span data-ttu-id="9d92e-180">I passaggi seguenti mostrano come sia possibile:</span><span class="sxs-lookup"><span data-stu-id="9d92e-180">The following steps show how you can:</span></span>

- <span data-ttu-id="9d92e-181">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d92e-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="9d92e-182">Generare o caricare un certificato in Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d92e-182">Generate or upload a certificate to the Key Vault</span></span>
- <span data-ttu-id="9d92e-183">Creare una chiave privata dal certificato da inserire in una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9d92e-183">Create a secret from the certificate to inject in to a VM</span></span>
- <span data-ttu-id="9d92e-184">Creare una macchina virtuale e inserire il certificato</span><span class="sxs-lookup"><span data-stu-id="9d92e-184">Create a VM and inject the certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="9d92e-185">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d92e-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="9d92e-186">Innanzitutto, creare un Key Vault con il comando [az keyvault create](/cli/azure/keyvault#create) e abilitarlo all'uso quando si distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d92e-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="9d92e-187">Ogni Key Vault deve avere un nome univoco in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="9d92e-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="9d92e-188">Nell'esempio seguente sostituire *mykeyvault* con il nome univoco del proprio Key Vault:</span><span class="sxs-lookup"><span data-stu-id="9d92e-188">Replace *mykeyvault* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="9d92e-189">Generare certificati e archiviarli in Key Vault</span><span class="sxs-lookup"><span data-stu-id="9d92e-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="9d92e-190">Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="9d92e-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="9d92e-191">Per questa esercitazione, l'esempio seguente illustra come sia possibile generare un certificato autofirmato con il comando [az keyvault certificate create](/cli/azure/keyvault/certificate#create) che usi i criteri dei certificati predefiniti:</span><span class="sxs-lookup"><span data-stu-id="9d92e-191">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="9d92e-192">Preparare i certificati per l'uso con macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="9d92e-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="9d92e-193">Per usare il certificato durante il processo di creazione della macchina virtuale, ottenere l'ID del certificato con il comando [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="9d92e-193">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="9d92e-194">La macchina virtuale richiede che il certificato abbia un formato specifico per inserirlo all'avvio, quindi è necessario convertire il certificato con [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="9d92e-194">The VM needs the certificate in a certain format to inject it on boot, so convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="9d92e-195">L'esempio seguente assegna l'output di questi comandi a delle variabili per semplificarne l'uso nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="9d92e-195">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="9d92e-196">Creare una configurazione cloud-init per proteggere NGINX</span><span class="sxs-lookup"><span data-stu-id="9d92e-196">Create cloud-init config to secure NGINX</span></span>
<span data-ttu-id="9d92e-197">Quando si crea una macchina virtuale, certificati e chiavi vengono archiviati nella directory */var/lib/waagent/* protetta.</span><span class="sxs-lookup"><span data-stu-id="9d92e-197">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="9d92e-198">Per automatizzare l'aggiunta del certificato alla macchina virtuale e la configurazione di NGINX, è possibile usare una configurazione di cloud-init aggiornata dall'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="9d92e-198">To automate adding the certificate to the VM and configuring NGINX, you can use an updated cloud-init config from the previous example.</span></span>

<span data-ttu-id="9d92e-199">Creare un file denominato *cloud-init-secured.txt* e incollare la configurazione seguente.</span><span class="sxs-lookup"><span data-stu-id="9d92e-199">Create a file named *cloud-init-secured.txt* and paste the following configuration.</span></span> <span data-ttu-id="9d92e-200">Anche in questo caso, se si usa Cloud Shell, creare il file di configurazione cloud-init in questa posizione e non nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="9d92e-200">Again, if you use the Cloud Shell, create the cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="9d92e-201">Usare `sensible-editor cloud-init-secured.txt` per creare il file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="9d92e-201">Use `sensible-editor cloud-init-secured.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="9d92e-202">Assicurarsi che l'intero file cloud-init venga copiato correttamente, in particolare la prima riga:</span><span class="sxs-lookup"><span data-stu-id="9d92e-202">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-secure-vm"></a><span data-ttu-id="9d92e-203">Creare una macchina virtuale protetta</span><span class="sxs-lookup"><span data-stu-id="9d92e-203">Create secure VM</span></span>
<span data-ttu-id="9d92e-204">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="9d92e-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="9d92e-205">I dati del certificato sono inseriti da Key Vault con il parametro `--secrets`.</span><span class="sxs-lookup"><span data-stu-id="9d92e-205">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="9d92e-206">Come nell'esempio precedente, si seleziona anche la configurazione cloud-init con il parametro `--custom-data`:</span><span class="sxs-lookup"><span data-stu-id="9d92e-206">As in the previous example, you also pass in the cloud-init config with the `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-secured.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="9d92e-207">Per creare la macchina virtuale, installare i pacchetti e avviare l'applicazione sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="9d92e-207">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="9d92e-208">Sono presenti attività in background la cui esecuzione continua dopo che l'interfaccia della riga di comando di Azure è tornata al prompt.</span><span class="sxs-lookup"><span data-stu-id="9d92e-208">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="9d92e-209">Potrebbe trascorrere ancora qualche minuto prima che sia possibile accedere all'app.</span><span class="sxs-lookup"><span data-stu-id="9d92e-209">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="9d92e-210">Dopo aver creato la macchina virtuale, prendere nota del `publicIpAddress` visualizzato dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="9d92e-210">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="9d92e-211">Questo indirizzo viene usato per accedere all'app Node.js tramite un Web browser.</span><span class="sxs-lookup"><span data-stu-id="9d92e-211">This address is used to access the Node.js app via a web browser.</span></span>

<span data-ttu-id="9d92e-212">Per consentire al traffico Web protetto di raggiungere la macchina virtuale, aprire la porta 443 da Internet con il comando [az vm open-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="9d92e-212">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="9d92e-213">Testare l'applicazione Web protetta</span><span class="sxs-lookup"><span data-stu-id="9d92e-213">Test secure web app</span></span>
<span data-ttu-id="9d92e-214">È ora possibile aprire un Web browser e immettere *https://<publicIpAddress>* nella barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="9d92e-214">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="9d92e-215">Fornire il proprio indirizzo IP pubblico dal processo di creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="9d92e-215">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="9d92e-216">Se è stato usato un certificato autofirmato, accettare l'avviso di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="9d92e-216">Accept the security warning if you used a self-signed certificate:</span></span>

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="9d92e-218">Il sito protetto NGINX e la app Node.js sono visualizzati come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="9d92e-218">Your secured NGINX site and Node.js app is then displayed as in the following example:</span></span>

![Visualizzare il sito protetto NGINX in esecuzione](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="9d92e-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9d92e-220">Next steps</span></span>
<span data-ttu-id="9d92e-221">In questa esercitazione vengono configurate macchine virtuali al primo avvio con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="9d92e-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="9d92e-222">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="9d92e-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9d92e-223">Creare un file di configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="9d92e-224">Creare una macchina virtuale che usa un file cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="9d92e-225">Visualizzare un'esecuzione dell'app Node.js dopo aver creato la macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="9d92e-225">View a running Node.js app after the VM is created</span></span>
> * <span data-ttu-id="9d92e-226">Usare Key Vault per archiviare in modo sicuro i certificati</span><span class="sxs-lookup"><span data-stu-id="9d92e-226">Use Key Vault to securely store certificates</span></span>
> * <span data-ttu-id="9d92e-227">Automatizzare le distribuzioni sicure di NGINX con cloud-init</span><span class="sxs-lookup"><span data-stu-id="9d92e-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="9d92e-228">Passare all'esercitazione successiva per imparare a creare immagini di macchine virtuali personalizzate.</span><span class="sxs-lookup"><span data-stu-id="9d92e-228">Advance to the next tutorial to learn how to create custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9d92e-229">Creare un'immagine di VM personalizzata</span><span class="sxs-lookup"><span data-stu-id="9d92e-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
