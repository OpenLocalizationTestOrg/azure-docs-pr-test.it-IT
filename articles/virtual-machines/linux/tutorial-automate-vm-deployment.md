---
title: aaaCustomize una VM Linux al primo avvio in Azure | Documenti Microsoft
description: Informazioni su come toouse cloud-init e hello macchine virtuali Linux di insieme di credenziali chiave toocustomze prima volta che eseguiranno l'avvio in Azure
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
ms.openlocfilehash: 280189723ac0205226f9c0068bd605da13249ace
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocustomize-a-linux-virtual-machine-on-first-boot"></a><span data-ttu-id="38d75-103">Come toocustomize una macchina virtuale Linux al primo avvio</span><span class="sxs-lookup"><span data-stu-id="38d75-103">How toocustomize a Linux virtual machine on first boot</span></span>
<span data-ttu-id="38d75-104">In un'esercitazione precedente, si è appreso come tooSSH tooa virtual machine (VM) e installare manualmente NGINX.</span><span class="sxs-lookup"><span data-stu-id="38d75-104">In a previous tutorial, you learned how tooSSH tooa virtual machine (VM) and manually install NGINX.</span></span> <span data-ttu-id="38d75-105">in genere desiderata toocreate macchine virtuali in modo rapido e coerenza, qualche forma di automazione.</span><span class="sxs-lookup"><span data-stu-id="38d75-105">toocreate VMs in a quick and consistent manner, some form of automation is typically desired.</span></span> <span data-ttu-id="38d75-106">Un comune toocustomize approccio una macchina virtuale al primo avvio viene toouse [cloud init](https://cloudinit.readthedocs.io).</span><span class="sxs-lookup"><span data-stu-id="38d75-106">A common approach toocustomize a VM on first boot is toouse [cloud-init](https://cloudinit.readthedocs.io).</span></span> <span data-ttu-id="38d75-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="38d75-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38d75-108">Creare un file di configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-108">Create a cloud-init config file</span></span>
> * <span data-ttu-id="38d75-109">Creare una macchina virtuale che usa un file cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-109">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="38d75-110">Visualizzare un'app Node.js in esecuzione dopo la creazione della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="38d75-110">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="38d75-111">Utilizzare l'archivio certificati di chiave dell'insieme di credenziali toosecurely</span><span class="sxs-lookup"><span data-stu-id="38d75-111">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="38d75-112">Automatizzare le distribuzioni sicure di NGINX con cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-112">Automate secure deployments of NGINX with cloud-init</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="38d75-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="38d75-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="38d75-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="38d75-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="38d75-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38d75-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  



## <a name="cloud-init-overview"></a><span data-ttu-id="38d75-116">Panoramica di cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-116">Cloud-init overview</span></span>
<span data-ttu-id="38d75-117">[Cloud init](https://cloudinit.readthedocs.io) è una VM Linux toocustomize un approccio ampiamente usato all'avvio per hello prima volta.</span><span class="sxs-lookup"><span data-stu-id="38d75-117">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="38d75-118">È possibile utilizzare pacchetti tooinstall cloud init e scrittura dei file, o gli utenti tooconfigure e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="38d75-118">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="38d75-119">Come cloud-inizializzazione viene eseguita durante il processo di avvio iniziale hello, non sono ulteriori passaggi o la configurazione obbligatoria tooapply gli agenti.</span><span class="sxs-lookup"><span data-stu-id="38d75-119">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="38d75-120">Cloud-init funziona anche fra distribuzioni.</span><span class="sxs-lookup"><span data-stu-id="38d75-120">Cloud-init also works across distributions.</span></span> <span data-ttu-id="38d75-121">Ad esempio, non si usa **installazione apt get** o **yum installare** tooinstall un pacchetto.</span><span class="sxs-lookup"><span data-stu-id="38d75-121">For example, you don't use **apt-get install** or **yum install** tooinstall a package.</span></span> <span data-ttu-id="38d75-122">In alternativa è possibile definire un elenco di pacchetti tooinstall.</span><span class="sxs-lookup"><span data-stu-id="38d75-122">Instead you can define a list of packages tooinstall.</span></span> <span data-ttu-id="38d75-123">Cloud init utilizza automaticamente lo strumento di gestione di hello pacchetto nativo per distribuzione hello selezionate.</span><span class="sxs-lookup"><span data-stu-id="38d75-123">Cloud-init automatically uses hello native package management tool for hello distro you select.</span></span>

<span data-ttu-id="38d75-124">È in uso di nostri partner tooget cloud-init inclusi e l'utilizzo delle immagini hello che forniscono tooAzure.</span><span class="sxs-lookup"><span data-stu-id="38d75-124">We are working with our partners tooget cloud-init included and working in hello images that they provide tooAzure.</span></span> <span data-ttu-id="38d75-125">Hello nella tabella seguente sono illustrati hello corrente cloud init disponibilità le immagini della piattaforma Azure:</span><span class="sxs-lookup"><span data-stu-id="38d75-125">hello following table outlines hello current cloud-init availability on Azure platform images:</span></span>

| <span data-ttu-id="38d75-126">Alias</span><span class="sxs-lookup"><span data-stu-id="38d75-126">Alias</span></span> | <span data-ttu-id="38d75-127">Autore</span><span class="sxs-lookup"><span data-stu-id="38d75-127">Publisher</span></span> | <span data-ttu-id="38d75-128">Offerta</span><span class="sxs-lookup"><span data-stu-id="38d75-128">Offer</span></span> | <span data-ttu-id="38d75-129">SKU</span><span class="sxs-lookup"><span data-stu-id="38d75-129">SKU</span></span> | <span data-ttu-id="38d75-130">Versione</span><span class="sxs-lookup"><span data-stu-id="38d75-130">Version</span></span> |
|:--- |:--- |:--- |:--- |:--- |:--- |
| <span data-ttu-id="38d75-131">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="38d75-131">UbuntuLTS</span></span> |<span data-ttu-id="38d75-132">Canonical</span><span class="sxs-lookup"><span data-stu-id="38d75-132">Canonical</span></span> |<span data-ttu-id="38d75-133">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="38d75-133">UbuntuServer</span></span> |<span data-ttu-id="38d75-134">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="38d75-134">16.04-LTS</span></span> |<span data-ttu-id="38d75-135">più recenti</span><span class="sxs-lookup"><span data-stu-id="38d75-135">latest</span></span> |
| <span data-ttu-id="38d75-136">UbuntuLTS</span><span class="sxs-lookup"><span data-stu-id="38d75-136">UbuntuLTS</span></span> |<span data-ttu-id="38d75-137">Canonical</span><span class="sxs-lookup"><span data-stu-id="38d75-137">Canonical</span></span> |<span data-ttu-id="38d75-138">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="38d75-138">UbuntuServer</span></span> |<span data-ttu-id="38d75-139">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="38d75-139">14.04.5-LTS</span></span> |<span data-ttu-id="38d75-140">più recenti</span><span class="sxs-lookup"><span data-stu-id="38d75-140">latest</span></span> |
| <span data-ttu-id="38d75-141">CoreOS</span><span class="sxs-lookup"><span data-stu-id="38d75-141">CoreOS</span></span> |<span data-ttu-id="38d75-142">CoreOS</span><span class="sxs-lookup"><span data-stu-id="38d75-142">CoreOS</span></span> |<span data-ttu-id="38d75-143">CoreOS</span><span class="sxs-lookup"><span data-stu-id="38d75-143">CoreOS</span></span> |<span data-ttu-id="38d75-144">Stabile</span><span class="sxs-lookup"><span data-stu-id="38d75-144">Stable</span></span> |<span data-ttu-id="38d75-145">più recenti</span><span class="sxs-lookup"><span data-stu-id="38d75-145">latest</span></span> |


## <a name="create-cloud-init-config-file"></a><span data-ttu-id="38d75-146">Creare un file di configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-146">Create cloud-init config file</span></span>
<span data-ttu-id="38d75-147">cloud toosee-init in azione, creare una macchina virtuale che installa NGINX ed esegue una semplice app Node.js 'Hello World'.</span><span class="sxs-lookup"><span data-stu-id="38d75-147">toosee cloud-init in action, create a VM that installs NGINX and runs a simple 'Hello World' Node.js app.</span></span> <span data-ttu-id="38d75-148">Hello seguente configurazione cloud init installa i pacchetti hello necessario, crea un'app Node.js, quindi inizializza e avvia l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-148">hello following cloud-init configuration installs hello required packages, creates a Node.js app, then initialize and starts hello app.</span></span>

<span data-ttu-id="38d75-149">Nella shell corrente, creare un file denominato *cloud init.txt* e Incolla hello seguente configurazione.</span><span class="sxs-lookup"><span data-stu-id="38d75-149">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="38d75-150">Ad esempio, creare file hello in hello Shell Cloud non presenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="38d75-150">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="38d75-151">È possibile usare qualsiasi editor.</span><span class="sxs-lookup"><span data-stu-id="38d75-151">You can use any editor you wish.</span></span> <span data-ttu-id="38d75-152">Immettere `sensible-editor cloud-init.txt` toocreate hello file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="38d75-152">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="38d75-153">Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:</span><span class="sxs-lookup"><span data-stu-id="38d75-153">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

<span data-ttu-id="38d75-154">Per altre informazioni sulle opzioni di configurazione di cloud-init, vedere gli [esempi di configurazione di cloud-init](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span><span class="sxs-lookup"><span data-stu-id="38d75-154">For more information about cloud-init configuration options, see [cloud-init config examples](https://cloudinit.readthedocs.io/en/latest/topics/examples.html).</span></span>

## <a name="create-virtual-machine"></a><span data-ttu-id="38d75-155">Crea macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="38d75-155">Create virtual machine</span></span>
<span data-ttu-id="38d75-156">Per poter creare una macchina virtuale è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="38d75-156">Before you can create a VM, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="38d75-157">esempio Hello crea un gruppo di risorse denominato *myResourceGroupAutomate* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="38d75-157">hello following example creates a resource group named *myResourceGroupAutomate* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupAutomate --location eastus
```

<span data-ttu-id="38d75-158">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="38d75-158">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="38d75-159">Hello utilizzare `--custom-data` toopass parametro nel file di configurazione cloud init.</span><span class="sxs-lookup"><span data-stu-id="38d75-159">Use hello `--custom-data` parameter toopass in your cloud-init config file.</span></span> <span data-ttu-id="38d75-160">Fornire hello percorso completo toohello *cloud init.txt* configurazione se è stato salvato il file hello all'esterno delle directory di lavoro attuale.</span><span class="sxs-lookup"><span data-stu-id="38d75-160">Provide hello full path toohello *cloud-init.txt* config if you saved hello file outside of your present working directory.</span></span> <span data-ttu-id="38d75-161">esempio Hello crea una macchina virtuale denominata *myAutomatedVM*:</span><span class="sxs-lookup"><span data-stu-id="38d75-161">hello following example creates a VM named *myAutomatedVM*:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupAutomate \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

<span data-ttu-id="38d75-162">Sono necessari alcuni minuti per hello VM toobe creato, tooinstall pacchetti hello e toostart app hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-162">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="38d75-163">Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="38d75-163">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="38d75-164">Potrebbe essere un altro paio di minuti prima di poter accedere app hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-164">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="38d75-165">Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="38d75-165">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="38d75-166">Questo indirizzo è utilizzato tooaccess hello Node.js app tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="38d75-166">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="38d75-167">tooallow web tooreach traffico la macchina virtuale, aprire la porta 80 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="38d75-167">tooallow web traffic tooreach your VM, open port 80 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroupAutomate --name myVM
```

## <a name="test-web-app"></a><span data-ttu-id="38d75-168">Testare l'app Web</span><span class="sxs-lookup"><span data-stu-id="38d75-168">Test web app</span></span>
<span data-ttu-id="38d75-169">È ora possibile aprire un web browser e immettere *http://<publicIpAddress>*  nella barra degli indirizzi hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-169">Now you can open a web browser and enter *http://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="38d75-170">Fornire la propria pubblico indirizzo IP da hello VM creare il processo.</span><span class="sxs-lookup"><span data-stu-id="38d75-170">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="38d75-171">App Node.js viene visualizzato come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="38d75-171">Your Node.js app is displayed as in hello following example:</span></span>

![Visualizzare il sito NGINX in esecuzione](./media/tutorial-automate-vm-deployment/nginx.png)


## <a name="inject-certificates-from-key-vault"></a><span data-ttu-id="38d75-173">Inserire certificati da Key Vault</span><span class="sxs-lookup"><span data-stu-id="38d75-173">Inject certificates from Key Vault</span></span>
<span data-ttu-id="38d75-174">Questa sezione facoltativa Mostra come è possibile in modo sicuro archiviare i certificati nell'insieme di credenziali chiave di Azure e li inserire durante la distribuzione di macchine Virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-174">This optional section shows how you can securely store certificates in Azure Key Vault and inject them during hello VM deployment.</span></span> <span data-ttu-id="38d75-175">Invece di usare un'immagine personalizzata che include i certificati di hello baked-in, questo processo assicura che i certificati più aggiornati di hello vengono inseriti tooa VM al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="38d75-175">Rather than using a custom image that includes hello certificates baked-in, this process ensures that hello most up-to-date certificates are injected tooa VM on first boot.</span></span> <span data-ttu-id="38d75-176">Durante il processo di hello mai certificato hello lascia hello piattaforma Azure o è esposto in uno script, una cronologia della riga di comando o un modello.</span><span class="sxs-lookup"><span data-stu-id="38d75-176">During hello process, hello certificate never leaves hello Azure platform or is exposed in a script, command-line history, or template.</span></span>

<span data-ttu-id="38d75-177">Azure Key Vault consente di proteggere chiavi crittografiche e segreti, come certificati e password.</span><span class="sxs-lookup"><span data-stu-id="38d75-177">Azure Key Vault safeguards cryptographic keys and secrets, such as certificates or passwords.</span></span> <span data-ttu-id="38d75-178">Insieme di credenziali chiave consente di semplificare il processo di gestione delle chiavi hello e consente il controllo toomaintain di chiavi per l'accesso e crittografare i dati.</span><span class="sxs-lookup"><span data-stu-id="38d75-178">Key Vault helps streamline hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="38d75-179">Questo scenario presenta alcuni toocreate concetti chiave dell'insieme di credenziali e utilizzare un certificato, anche se non viene fornita una panoramica completa sulla toouse insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="38d75-179">This scenario introduces some Key Vault concepts toocreate and use a certificate, though is not an exhaustive overview on how toouse Key Vault.</span></span>

<span data-ttu-id="38d75-180">Hello alla procedura seguente mostra come è possibile:</span><span class="sxs-lookup"><span data-stu-id="38d75-180">hello following steps show how you can:</span></span>

- <span data-ttu-id="38d75-181">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="38d75-181">Create an Azure Key Vault</span></span>
- <span data-ttu-id="38d75-182">Generare o caricare un insieme di credenziali chiave di toohello certificato</span><span class="sxs-lookup"><span data-stu-id="38d75-182">Generate or upload a certificate toohello Key Vault</span></span>
- <span data-ttu-id="38d75-183">Creare una chiave privata da tooinject certificato hello in tooa VM</span><span class="sxs-lookup"><span data-stu-id="38d75-183">Create a secret from hello certificate tooinject in tooa VM</span></span>
- <span data-ttu-id="38d75-184">Creare una macchina virtuale e inserire il certificato di hello</span><span class="sxs-lookup"><span data-stu-id="38d75-184">Create a VM and inject hello certificate</span></span>

### <a name="create-an-azure-key-vault"></a><span data-ttu-id="38d75-185">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="38d75-185">Create an Azure Key Vault</span></span>
<span data-ttu-id="38d75-186">Innanzitutto, creare un Key Vault con il comando [az keyvault create](/cli/azure/keyvault#create) e abilitarlo all'uso quando si distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="38d75-186">First, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="38d75-187">Ogni Key Vault deve avere un nome univoco in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="38d75-187">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="38d75-188">Sostituire *mykeyvault* in hello esempio con il proprio nome univoco di insieme di credenziali chiave seguente:</span><span class="sxs-lookup"><span data-stu-id="38d75-188">Replace *mykeyvault* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=mykeyvault
az keyvault create \
    --resource-group myResourceGroupAutomate \
    --name $keyvault_name \
    --enabled-for-deployment
```

### <a name="generate-certificate-and-store-in-key-vault"></a><span data-ttu-id="38d75-189">Generare certificati e archiviarli in Key Vault</span><span class="sxs-lookup"><span data-stu-id="38d75-189">Generate certificate and store in Key Vault</span></span>
<span data-ttu-id="38d75-190">Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="38d75-190">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/keyvault/certificate#import).</span></span> <span data-ttu-id="38d75-191">Per questa esercitazione, hello esempio seguente viene illustrato come è possibile generare un certificato autofirmato con [certificato keyvault az creare](/cli/azure/keyvault/certificate#create) che utilizza criteri di certificato predefiniti hello:</span><span class="sxs-lookup"><span data-stu-id="38d75-191">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/keyvault/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```


### <a name="prepare-certificate-for-use-with-vm"></a><span data-ttu-id="38d75-192">Preparare i certificati per l'uso con macchine virtuali</span><span class="sxs-lookup"><span data-stu-id="38d75-192">Prepare certificate for use with VM</span></span>
<span data-ttu-id="38d75-193">certificato di hello toouse durante hello VM creare il processo, ottenere l'ID di hello del certificato con [az keyvault elenco-versioni del segreto](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="38d75-193">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="38d75-194">Hello VM deve certificato hello in un determinato formato tooinject non all'avvio del sistema, quindi convertire certificato hello con [az vm segreto formato](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="38d75-194">hello VM needs hello certificate in a certain format tooinject it on boot, so convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="38d75-195">Hello di esempio seguente assegna l'output di hello di toovariables questi comandi per facilitare l'utilizzo in hello passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="38d75-195">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```


### <a name="create-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="38d75-196">Creare cloud init configurazione toosecure NGINX</span><span class="sxs-lookup"><span data-stu-id="38d75-196">Create cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="38d75-197">Quando si crea una macchina virtuale, i certificati e chiavi vengono archiviate in hello protetto *var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="38d75-197">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="38d75-198">tooautomate aggiunta hello certificato toohello macchina virtuale e la configurazione NGINX, è possibile utilizzare una configurazione cloud-init aggiornata dall'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-198">tooautomate adding hello certificate toohello VM and configuring NGINX, you can use an updated cloud-init config from hello previous example.</span></span>

<span data-ttu-id="38d75-199">Creare un file denominato *cloud-init-secured.txt* e Incolla hello seguente configurazione.</span><span class="sxs-lookup"><span data-stu-id="38d75-199">Create a file named *cloud-init-secured.txt* and paste hello following configuration.</span></span> <span data-ttu-id="38d75-200">Nuovamente, se si utilizza hello Shell Cloud, creare il file di configurazione cloud init hello non esiste e non nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="38d75-200">Again, if you use hello Cloud Shell, create hello cloud-init config file there and not on your local machine.</span></span> <span data-ttu-id="38d75-201">Utilizzare `sensible-editor cloud-init-secured.txt` toocreate hello file e visualizzare un elenco degli editor disponibili.</span><span class="sxs-lookup"><span data-stu-id="38d75-201">Use `sensible-editor cloud-init-secured.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="38d75-202">Assicurarsi che tale file intero cloud-init hello viene copiato correttamente, soprattutto hello prima riga:</span><span class="sxs-lookup"><span data-stu-id="38d75-202">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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

### <a name="create-secure-vm"></a><span data-ttu-id="38d75-203">Creare una macchina virtuale protetta</span><span class="sxs-lookup"><span data-stu-id="38d75-203">Create secure VM</span></span>
<span data-ttu-id="38d75-204">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="38d75-204">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="38d75-205">dati del certificato Hello viene inseriti dall'insieme di credenziali chiave con hello `--secrets` parametro.</span><span class="sxs-lookup"><span data-stu-id="38d75-205">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="38d75-206">Nell'esempio precedente hello, è anche passare nella configurazione cloud init hello con hello `--custom-data` parametro:</span><span class="sxs-lookup"><span data-stu-id="38d75-206">As in hello previous example, you also pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

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

<span data-ttu-id="38d75-207">Sono necessari alcuni minuti per hello VM toobe creato, tooinstall pacchetti hello e toostart app hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-207">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="38d75-208">Sono presenti attività in background che continuare toorun dopo hello CLI di Azure restituisce toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="38d75-208">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="38d75-209">Potrebbe essere un altro paio di minuti prima di poter accedere app hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-209">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="38d75-210">Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="38d75-210">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="38d75-211">Questo indirizzo è utilizzato tooaccess hello Node.js app tramite un web browser.</span><span class="sxs-lookup"><span data-stu-id="38d75-211">This address is used tooaccess hello Node.js app via a web browser.</span></span>

<span data-ttu-id="38d75-212">tooallow secure tooreach traffico web la macchina virtuale, aprire la porta 443 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="38d75-212">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupAutomate \
    --name myVMSecured \
    --port 443
```

### <a name="test-secure-web-app"></a><span data-ttu-id="38d75-213">Testare l'applicazione Web protetta</span><span class="sxs-lookup"><span data-stu-id="38d75-213">Test secure web app</span></span>
<span data-ttu-id="38d75-214">È ora possibile aprire un web browser e immettere *https://<publicIpAddress>*  nella barra degli indirizzi hello.</span><span class="sxs-lookup"><span data-stu-id="38d75-214">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="38d75-215">Fornire la propria pubblico indirizzo IP da hello VM creare il processo.</span><span class="sxs-lookup"><span data-stu-id="38d75-215">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="38d75-216">Se è stato utilizzato un certificato autofirmato, è necessario accettare l'avviso di sicurezza hello:</span><span class="sxs-lookup"><span data-stu-id="38d75-216">Accept hello security warning if you used a self-signed certificate:</span></span>

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-automate-vm-deployment/browser-warning.png)

<span data-ttu-id="38d75-218">Il sito NGINX e Node.js app viene quindi visualizzata come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="38d75-218">Your secured NGINX site and Node.js app is then displayed as in hello following example:</span></span>

![Visualizzare il sito protetto NGINX in esecuzione](./media/tutorial-automate-vm-deployment/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="38d75-220">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="38d75-220">Next steps</span></span>
<span data-ttu-id="38d75-221">In questa esercitazione vengono configurate macchine virtuali al primo avvio con cloud-init.</span><span class="sxs-lookup"><span data-stu-id="38d75-221">In this tutorial, you configured VMs on first boot with cloud-init.</span></span> <span data-ttu-id="38d75-222">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="38d75-222">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="38d75-223">Creare un file di configurazione cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-223">Create a cloud-init config file</span></span>
> * <span data-ttu-id="38d75-224">Creare una macchina virtuale che usa un file cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-224">Create a VM that uses a cloud-init file</span></span>
> * <span data-ttu-id="38d75-225">Visualizzare un'app Node.js in esecuzione dopo la creazione della macchina virtuale hello</span><span class="sxs-lookup"><span data-stu-id="38d75-225">View a running Node.js app after hello VM is created</span></span>
> * <span data-ttu-id="38d75-226">Utilizzare l'archivio certificati di chiave dell'insieme di credenziali toosecurely</span><span class="sxs-lookup"><span data-stu-id="38d75-226">Use Key Vault toosecurely store certificates</span></span>
> * <span data-ttu-id="38d75-227">Automatizzare le distribuzioni sicure di NGINX con cloud-init</span><span class="sxs-lookup"><span data-stu-id="38d75-227">Automate secure deployments of NGINX with cloud-init</span></span>

<span data-ttu-id="38d75-228">Spostare toolearn esercitazione successiva toohello come toocreate immagini di macchina virtuale personalizzate.</span><span class="sxs-lookup"><span data-stu-id="38d75-228">Advance toohello next tutorial toolearn how toocreate custom VM images.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38d75-229">Creare un'immagine di VM personalizzata</span><span class="sxs-lookup"><span data-stu-id="38d75-229">Create custom VM images</span></span>](./tutorial-custom-images.md)
