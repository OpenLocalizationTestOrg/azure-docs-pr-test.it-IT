---
title: un server web con SSL certificati in Azure aaaSecure | Documenti Microsoft
description: Informazioni su come certificati del server web di toosecure hello NGINX con SSL in una VM Linux in Azure
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
ms.date: 07/17/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: d3a62d77ac05c9aa2a44356b7c8e44cb485b81aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="a4783-103">Proteggere un server Web con i certificati SSL in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="a4783-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="a4783-104">server web toosecure, un certificato in un secondo momento SSL (Secure Sockets) può essere utilizzato il traffico web tooencrypt.</span><span class="sxs-lookup"><span data-stu-id="a4783-104">toosecure web servers, a Secure Sockets Later (SSL) certificate can be used tooencrypt web traffic.</span></span> <span data-ttu-id="a4783-105">Questi certificati SSL possono essere archiviati nell'insieme di credenziali chiave di Azure e consentono le distribuzioni sicure di certificati tooLinux le macchine virtuali (VM) in Azure.</span><span class="sxs-lookup"><span data-stu-id="a4783-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates tooLinux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="a4783-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="a4783-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4783-107">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4783-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="a4783-108">Generare o caricare un insieme di credenziali chiave di toohello certificato</span><span class="sxs-lookup"><span data-stu-id="a4783-108">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="a4783-109">Creare una macchina virtuale e installare il server web NGINX di hello</span><span class="sxs-lookup"><span data-stu-id="a4783-109">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="a4783-110">Inserire il certificato di hello nella VM hello e configura NGINX con un binding SSL</span><span class="sxs-lookup"><span data-stu-id="a4783-110">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a4783-111">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="a4783-111">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a4783-112">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="a4783-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="a4783-113">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a4783-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="a4783-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="a4783-114">Overview</span></span>
<span data-ttu-id="a4783-115">Azure Key Vault consente di proteggere chiavi di crittografia, chiavi private, certificati e password.</span><span class="sxs-lookup"><span data-stu-id="a4783-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="a4783-116">Insieme di credenziali chiave consente di ottimizzare processo di gestione dei certificati hello e consente il controllo toomaintain delle chiavi che accedono a tali certificati.</span><span class="sxs-lookup"><span data-stu-id="a4783-116">Key Vault helps streamline hello certificate management process and enables you toomaintain control of keys that access those certificates.</span></span> <span data-ttu-id="a4783-117">È possibile creare un certificato autofirmato in Key Vault o caricarne uno esistente, un certificato attendibile di cui si è già proprietari.</span><span class="sxs-lookup"><span data-stu-id="a4783-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="a4783-118">Invece di usare un'immagine di macchina virtuale personalizzata che include certificati incorporati, si inseriscono i certificati in una macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="a4783-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="a4783-119">Questo processo assicura che i certificati più aggiornati di hello siano installati in un server web durante la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="a4783-119">This process ensures that hello most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="a4783-120">Se si rinnovare o sostituire un certificato, non è inoltre necessario toocreate una nuova immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="a4783-120">If you renew or replace a certificate, you don't also have toocreate a new custom VM image.</span></span> <span data-ttu-id="a4783-121">i certificati più recenti di Hello vengono inseriti automaticamente durante la creazione di macchine virtuali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="a4783-121">hello latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="a4783-122">Durante l'intero processo hello, i certificati di hello mai lasciare hello piattaforma Azure o vengono esposti in uno script, una cronologia della riga di comando o un modello.</span><span class="sxs-lookup"><span data-stu-id="a4783-122">During hello whole process, hello certificates never leave hello Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="a4783-123">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4783-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="a4783-124">Per poter creare un insieme di credenziali delle chiavi e i certificati, è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="a4783-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="a4783-125">esempio Hello crea un gruppo di risorse denominato *myResourceGroupSecureWeb* in hello *eastus* percorso:</span><span class="sxs-lookup"><span data-stu-id="a4783-125">hello following example creates a resource group named *myResourceGroupSecureWeb* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="a4783-126">Creare quindi un insieme di credenziali delle chiavi con il comando [az keyvault create](/cli/azure/keyvault#create) e abilitarlo all'uso quando si distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4783-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="a4783-127">Ogni Key Vault deve avere un nome univoco in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="a4783-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="a4783-128">Sostituire  *<mykeyvault>*  in hello esempio con il proprio nome univoco di insieme di credenziali chiave seguente:</span><span class="sxs-lookup"><span data-stu-id="a4783-128">Replace *<mykeyvault>* in hello following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="a4783-129">Generare un certificato e archiviarlo in Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4783-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="a4783-130">Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="a4783-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="a4783-131">Per questa esercitazione, hello esempio seguente viene illustrato come è possibile generare un certificato autofirmato con [certificato keyvault az creare](/cli/azure/certificate#create) che utilizza criteri di certificato predefiniti hello:</span><span class="sxs-lookup"><span data-stu-id="a4783-131">For this tutorial, hello following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses hello default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="a4783-132">Preparare un certificato per l'uso con una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="a4783-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="a4783-133">certificato di hello toouse durante hello VM creare il processo, ottenere l'ID di hello del certificato con [az keyvault elenco-versioni del segreto](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="a4783-133">toouse hello certificate during hello VM create process, obtain hello ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="a4783-134">Convertire certificato hello con [az vm segreto formato](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="a4783-134">Convert hello certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="a4783-135">Hello di esempio seguente assegna l'output di hello di toovariables questi comandi per facilitare l'utilizzo in hello passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="a4783-135">hello following example assigns hello output of these commands toovariables for ease of use in hello next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-toosecure-nginx"></a><span data-ttu-id="a4783-136">Creare un toosecure configurazione cloud init NGINX</span><span class="sxs-lookup"><span data-stu-id="a4783-136">Create a cloud-init config toosecure NGINX</span></span>
<span data-ttu-id="a4783-137">[Cloud init](https://cloudinit.readthedocs.io) è una VM Linux toocustomize un approccio ampiamente usato all'avvio per hello prima volta.</span><span class="sxs-lookup"><span data-stu-id="a4783-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach toocustomize a Linux VM as it boots for hello first time.</span></span> <span data-ttu-id="a4783-138">È possibile utilizzare pacchetti tooinstall cloud init e scrittura dei file, o gli utenti tooconfigure e sicurezza.</span><span class="sxs-lookup"><span data-stu-id="a4783-138">You can use cloud-init tooinstall packages and write files, or tooconfigure users and security.</span></span> <span data-ttu-id="a4783-139">Come cloud-inizializzazione viene eseguita durante il processo di avvio iniziale hello, non sono ulteriori passaggi o la configurazione obbligatoria tooapply gli agenti.</span><span class="sxs-lookup"><span data-stu-id="a4783-139">As cloud-init runs during hello initial boot process, there are no additional steps or required agents tooapply your configuration.</span></span>

<span data-ttu-id="a4783-140">Quando si crea una macchina virtuale, i certificati e chiavi vengono archiviate in hello protetto *var/lib/waagent/* directory.</span><span class="sxs-lookup"><span data-stu-id="a4783-140">When you create a VM, certificates and keys are stored in hello protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="a4783-141">aggiunta di tooautomate hello toohello certificato VM e configurazione hello del server web, utilizzare cloud init.</span><span class="sxs-lookup"><span data-stu-id="a4783-141">tooautomate adding hello certificate toohello VM and configuring hello web server, use cloud-init.</span></span> <span data-ttu-id="a4783-142">In questo esempio è di installare e configurare i server web NGINX di hello.</span><span class="sxs-lookup"><span data-stu-id="a4783-142">In this example, we install and configure hello NGINX web server.</span></span> <span data-ttu-id="a4783-143">È possibile utilizzare hello stesso processo tooinstall e configurare Apache.</span><span class="sxs-lookup"><span data-stu-id="a4783-143">You can use hello same process tooinstall and configure Apache.</span></span> 

<span data-ttu-id="a4783-144">Creare un file denominato *cloud-init-web-server.txt* e Incolla hello seguente configurazione:</span><span class="sxs-lookup"><span data-stu-id="a4783-144">Create a file named *cloud-init-web-server.txt* and paste hello following configuration:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 443 ssl;
        ssl_certificate /etc/nginx/ssl/mycert.cert;
        ssl_certificate_key /etc/nginx/ssl/mycert.prv;
      }
runcmd:
  - secretsname=$(find /var/lib/waagent/ -name "*.prv" | cut -c -57)
  - mkdir /etc/nginx/ssl
  - cp $secretsname.crt /etc/nginx/ssl/mycert.cert
  - cp $secretsname.prv /etc/nginx/ssl/mycert.prv
  - service nginx restart
```

### <a name="create-a-secure-vm"></a><span data-ttu-id="a4783-145">Creare una macchina virtuale sicura</span><span class="sxs-lookup"><span data-stu-id="a4783-145">Create a secure VM</span></span>
<span data-ttu-id="a4783-146">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a4783-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a4783-147">dati del certificato Hello viene inseriti dall'insieme di credenziali chiave con hello `--secrets` parametro.</span><span class="sxs-lookup"><span data-stu-id="a4783-147">hello certificate data is injected from Key Vault with hello `--secrets` parameter.</span></span> <span data-ttu-id="a4783-148">Passare in configurazione cloud init hello con hello `--custom-data` parametro:</span><span class="sxs-lookup"><span data-stu-id="a4783-148">You pass in hello cloud-init config with hello `--custom-data` parameter:</span></span>

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init-web-server.txt \
    --secrets "$vm_secret"
```

<span data-ttu-id="a4783-149">Sono necessari alcuni minuti per hello VM toobe creato, tooinstall pacchetti hello e toostart app hello.</span><span class="sxs-lookup"><span data-stu-id="a4783-149">It takes a few minutes for hello VM toobe created, hello packages tooinstall, and hello app toostart.</span></span> <span data-ttu-id="a4783-150">Dopo aver creato hello VM, prendere nota di hello `publicIpAddress` visualizzato da hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="a4783-150">When hello VM has been created, take note of hello `publicIpAddress` displayed by hello Azure CLI.</span></span> <span data-ttu-id="a4783-151">Questo indirizzo viene utilizzato tooaccess del sito in un web browser.</span><span class="sxs-lookup"><span data-stu-id="a4783-151">This address is used tooaccess your site in a web browser.</span></span>

<span data-ttu-id="a4783-152">tooallow secure tooreach traffico web la macchina virtuale, aprire la porta 443 da hello Internet con [az vm open-porta](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="a4783-152">tooallow secure web traffic tooreach your VM, open port 443 from hello Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-hello-secure-web-app"></a><span data-ttu-id="a4783-153">App web in modo sicuro hello di test</span><span class="sxs-lookup"><span data-stu-id="a4783-153">Test hello secure web app</span></span>
<span data-ttu-id="a4783-154">È ora possibile aprire un web browser e immettere *https://<publicIpAddress>*  nella barra degli indirizzi hello.</span><span class="sxs-lookup"><span data-stu-id="a4783-154">Now you can open a web browser and enter *https://<publicIpAddress>* in hello address bar.</span></span> <span data-ttu-id="a4783-155">Fornire la propria pubblico indirizzo IP da hello VM creare il processo.</span><span class="sxs-lookup"><span data-stu-id="a4783-155">Provide your own public IP address from hello VM create process.</span></span> <span data-ttu-id="a4783-156">Se è stato utilizzato un certificato autofirmato, è necessario accettare l'avviso di sicurezza hello:</span><span class="sxs-lookup"><span data-stu-id="a4783-156">Accept hello security warning if you used a self-signed certificate:</span></span>

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="a4783-158">Il sito NGINX protetto viene quindi visualizzato come hello di esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="a4783-158">Your secured NGINX site is then displayed as in hello following example:</span></span>

![Visualizzare il sito protetto NGINX in esecuzione](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="a4783-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a4783-160">Next steps</span></span>

<span data-ttu-id="a4783-161">In questa esercitazione si è protetto un server Web NGINX con un certificato SSL archiviato in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="a4783-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="a4783-162">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="a4783-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a4783-163">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="a4783-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="a4783-164">Generare o caricare un insieme di credenziali chiave di toohello certificato</span><span class="sxs-lookup"><span data-stu-id="a4783-164">Generate or upload a certificate toohello Key Vault</span></span>
> * <span data-ttu-id="a4783-165">Creare una macchina virtuale e installare il server web NGINX di hello</span><span class="sxs-lookup"><span data-stu-id="a4783-165">Create a VM and install hello NGINX web server</span></span>
> * <span data-ttu-id="a4783-166">Inserire il certificato di hello nella VM hello e configura NGINX con un binding SSL</span><span class="sxs-lookup"><span data-stu-id="a4783-166">Inject hello certificate into hello VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="a4783-167">Seguire questo toosee di collegamento incorporati gli esempi di script di macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="a4783-167">Follow this link toosee pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a4783-168">Esempi di script delle macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="a4783-168">Windows virtual machine script samples</span></span>](./cli-samples.md)