---
title: Proteggere un server Web con i certificati SSL in Azure | Microsoft Docs
description: Informazioni su come proteggere il server Web NGINX con i certificati SSL in una macchina virtuale Linux in Azure
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
ms.openlocfilehash: 181be35aeb61020db3abaeba22aa882848923c31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="secure-a-web-server-with-ssl-certificates-on-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="f906a-103">Proteggere un server Web con i certificati SSL in una macchina virtuale Linux in Azure</span><span class="sxs-lookup"><span data-stu-id="f906a-103">Secure a web server with SSL certificates on a Linux virtual machine in Azure</span></span>
<span data-ttu-id="f906a-104">Per proteggere i server Web, si può usare un certificato Secure Sockets Layer (SSL) per crittografare il traffico Web.</span><span class="sxs-lookup"><span data-stu-id="f906a-104">To secure web servers, a Secure Sockets Later (SSL) certificate can be used to encrypt web traffic.</span></span> <span data-ttu-id="f906a-105">Questi certificati SSL possono essere archiviati in Azure Key Vault e consentono distribuzioni sicure dei certificati nelle macchine virtuali Linux in Azure.</span><span class="sxs-lookup"><span data-stu-id="f906a-105">These SSL certificates can be stored in Azure Key Vault, and allow secure deployments of certificates to Linux virtual machines (VMs) in Azure.</span></span> <span data-ttu-id="f906a-106">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="f906a-106">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f906a-107">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f906a-107">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="f906a-108">Generare o caricare un certificato in Key Vault</span><span class="sxs-lookup"><span data-stu-id="f906a-108">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="f906a-109">Creare una macchina virtuale e installare il server Web NGINX</span><span class="sxs-lookup"><span data-stu-id="f906a-109">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="f906a-110">Inserire il certificato nella macchina virtuale e configurare NGINX con un'associazione SSL</span><span class="sxs-lookup"><span data-stu-id="f906a-110">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f906a-111">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f906a-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="f906a-112">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="f906a-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="f906a-113">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f906a-113">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>  


## <a name="overview"></a><span data-ttu-id="f906a-114">Panoramica</span><span class="sxs-lookup"><span data-stu-id="f906a-114">Overview</span></span>
<span data-ttu-id="f906a-115">Azure Key Vault consente di proteggere chiavi di crittografia, chiavi private, certificati e password.</span><span class="sxs-lookup"><span data-stu-id="f906a-115">Azure Key Vault safeguards cryptographic keys and secrets, such certificates or passwords.</span></span> <span data-ttu-id="f906a-116">Key Vault semplifica il processo di gestione dei certificati e consente di mantenere il controllo delle chiavi che accedono a tali certificati.</span><span class="sxs-lookup"><span data-stu-id="f906a-116">Key Vault helps streamline the certificate management process and enables you to maintain control of keys that access those certificates.</span></span> <span data-ttu-id="f906a-117">È possibile creare un certificato autofirmato in Key Vault o caricarne uno esistente, un certificato attendibile di cui si è già proprietari.</span><span class="sxs-lookup"><span data-stu-id="f906a-117">You can create a self-signed certificate inside Key Vault, or upload an existing, trusted certificate that you already own.</span></span>

<span data-ttu-id="f906a-118">Invece di usare un'immagine di macchina virtuale personalizzata che include certificati incorporati, si inseriscono i certificati in una macchina virtuale in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="f906a-118">Rather than using a custom VM image that includes certificates baked-in, you inject certificates into a running VM.</span></span> <span data-ttu-id="f906a-119">Questo processo assicura che, durante la distribuzione, in un server Web vengano installati i certificati più aggiornati.</span><span class="sxs-lookup"><span data-stu-id="f906a-119">This process ensures that the most up-to-date certificates are installed on a web server during deployment.</span></span> <span data-ttu-id="f906a-120">Se si rinnova o sostituisce un certificato, non è necessario creare anche una nuova immagine di macchina virtuale personalizzata.</span><span class="sxs-lookup"><span data-stu-id="f906a-120">If you renew or replace a certificate, you don't also have to create a new custom VM image.</span></span> <span data-ttu-id="f906a-121">I certificati più recenti vengono automaticamente inseriti quando si creano macchine virtuali aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="f906a-121">The latest certificates are automatically injected as you create additional VMs.</span></span> <span data-ttu-id="f906a-122">Durante l'intero processo, i certificati non lasciano mai la piattaforma Azure e non vengono mai esposti in uno script, in una cronologia della riga di comando o in un modello.</span><span class="sxs-lookup"><span data-stu-id="f906a-122">During the whole process, the certificates never leave the Azure platform or are exposed in a script, command-line history, or template.</span></span>


## <a name="create-an-azure-key-vault"></a><span data-ttu-id="f906a-123">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f906a-123">Create an Azure Key Vault</span></span>
<span data-ttu-id="f906a-124">Per poter creare un insieme di credenziali delle chiavi e i certificati, è prima necessario creare un gruppo di risorse con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="f906a-124">Before you can create a Key Vault and certificates, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="f906a-125">L'esempio seguente crea un gruppo di risorse denominato *myResourceGroupSecureWeb* nella località *eastus*:</span><span class="sxs-lookup"><span data-stu-id="f906a-125">The following example creates a resource group named *myResourceGroupSecureWeb* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupSecureWeb --location eastus
```

<span data-ttu-id="f906a-126">Creare quindi un insieme di credenziali delle chiavi con il comando [az keyvault create](/cli/azure/keyvault#create) e abilitarlo all'uso quando si distribuisce una macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f906a-126">Next, create a Key Vault with [az keyvault create](/cli/azure/keyvault#create) and enable it for use when you deploy a VM.</span></span> <span data-ttu-id="f906a-127">Ogni Key Vault deve avere un nome univoco in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="f906a-127">Each Key Vault requires a unique name, and should be all lower case.</span></span> <span data-ttu-id="f906a-128">Nell'esempio seguente sostituire *<mykeyvault>* con il nome univoco del proprio Key Vault:</span><span class="sxs-lookup"><span data-stu-id="f906a-128">Replace *<mykeyvault>* in the following example with your own unique Key Vault name:</span></span>

```azurecli-interactive 
keyvault_name=<mykeyvault>
az keyvault create \
    --resource-group myResourceGroupSecureWeb \
    --name $keyvault_name \
    --enabled-for-deployment
```

## <a name="generate-a-certificate-and-store-in-key-vault"></a><span data-ttu-id="f906a-129">Generare un certificato e archiviarlo in Key Vault</span><span class="sxs-lookup"><span data-stu-id="f906a-129">Generate a certificate and store in Key Vault</span></span>
<span data-ttu-id="f906a-130">Per la produzione è necessario importare un certificato valido firmato da un provider attendibile con il comando [az keyvault certificate import](/cli/azure/certificate#import).</span><span class="sxs-lookup"><span data-stu-id="f906a-130">For production use, you should import a valid certificate signed by trusted provider with [az keyvault certificate import](/cli/azure/certificate#import).</span></span> <span data-ttu-id="f906a-131">Per questa esercitazione, l'esempio seguente illustra come sia possibile generare un certificato autofirmato con il comando [az keyvault certificate create](/cli/azure/certificate#create) che usi i criteri dei certificati predefiniti:</span><span class="sxs-lookup"><span data-stu-id="f906a-131">For this tutorial, the following example shows how you can generate a self-signed certificate with [az keyvault certificate create](/cli/azure/certificate#create) that uses the default certificate policy:</span></span>

```azurecli-interactive 
az keyvault certificate create \
    --vault-name $keyvault_name \
    --name mycert \
    --policy "$(az keyvault certificate get-default-policy)"
```

### <a name="prepare-a-certificate-for-use-with-a-vm"></a><span data-ttu-id="f906a-132">Preparare un certificato per l'uso con una macchina virtuale</span><span class="sxs-lookup"><span data-stu-id="f906a-132">Prepare a certificate for use with a VM</span></span>
<span data-ttu-id="f906a-133">Per usare il certificato durante il processo di creazione della macchina virtuale, ottenere l'ID del certificato con il comando [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span><span class="sxs-lookup"><span data-stu-id="f906a-133">To use the certificate during the VM create process, obtain the ID of your certificate with [az keyvault secret list-versions](/cli/azure/keyvault/secret#list-versions).</span></span> <span data-ttu-id="f906a-134">Convertire il certificato con il comando [az vm format-secret](/cli/azure/vm#format-secret).</span><span class="sxs-lookup"><span data-stu-id="f906a-134">Convert the certificate with [az vm format-secret](/cli/azure/vm#format-secret).</span></span> <span data-ttu-id="f906a-135">L'esempio seguente assegna l'output di questi comandi a delle variabili per semplificarne l'uso nei passaggi successivi:</span><span class="sxs-lookup"><span data-stu-id="f906a-135">The following example assigns the output of these commands to variables for ease of use in the next steps:</span></span>

```azurecli-interactive 
secret=$(az keyvault secret list-versions \
          --vault-name $keyvault_name \
          --name mycert \
          --query "[?attributes.enabled].id" --output tsv)
vm_secret=$(az vm format-secret --secret "$secret")
```

### <a name="create-a-cloud-init-config-to-secure-nginx"></a><span data-ttu-id="f906a-136">Creare una configurazione cloud-init per proteggere NGINX</span><span class="sxs-lookup"><span data-stu-id="f906a-136">Create a cloud-init config to secure NGINX</span></span>
<span data-ttu-id="f906a-137">[Cloud-init](https://cloudinit.readthedocs.io) è un approccio diffuso per personalizzare una macchina virtuale Linux al primo avvio.</span><span class="sxs-lookup"><span data-stu-id="f906a-137">[Cloud-init](https://cloudinit.readthedocs.io) is a widely used approach to customize a Linux VM as it boots for the first time.</span></span> <span data-ttu-id="f906a-138">Cloud-init consente di installare pacchetti e scrivere file o configurare utenti e impostazioni di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="f906a-138">You can use cloud-init to install packages and write files, or to configure users and security.</span></span> <span data-ttu-id="f906a-139">Quando cloud-init viene eseguito durante il processo di avvio iniziale non vi sono altri passaggi o agenti necessari per applicare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="f906a-139">As cloud-init runs during the initial boot process, there are no additional steps or required agents to apply your configuration.</span></span>

<span data-ttu-id="f906a-140">Quando si crea una macchina virtuale, certificati e chiavi vengono archiviati nella directory */var/lib/waagent/* protetta.</span><span class="sxs-lookup"><span data-stu-id="f906a-140">When you create a VM, certificates and keys are stored in the protected */var/lib/waagent/* directory.</span></span> <span data-ttu-id="f906a-141">Per automatizzare l'aggiunta del certificato alla macchina virtuale e la configurazione del server Web, usare cloud-init.</span><span class="sxs-lookup"><span data-stu-id="f906a-141">To automate adding the certificate to the VM and configuring the web server, use cloud-init.</span></span> <span data-ttu-id="f906a-142">In questo esempio viene installato e configurato il server Web NGINX.</span><span class="sxs-lookup"><span data-stu-id="f906a-142">In this example, we install and configure the NGINX web server.</span></span> <span data-ttu-id="f906a-143">È possibile usare lo stesso processo per installare e configurare Apache.</span><span class="sxs-lookup"><span data-stu-id="f906a-143">You can use the same process to install and configure Apache.</span></span> 

<span data-ttu-id="f906a-144">Creare un file denominato *cloud-init-web-server.txt* e incollare la configurazione seguente:</span><span class="sxs-lookup"><span data-stu-id="f906a-144">Create a file named *cloud-init-web-server.txt* and paste the following configuration:</span></span>

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

### <a name="create-a-secure-vm"></a><span data-ttu-id="f906a-145">Creare una macchina virtuale sicura</span><span class="sxs-lookup"><span data-stu-id="f906a-145">Create a secure VM</span></span>
<span data-ttu-id="f906a-146">Creare quindi una macchina virtuale con il comando [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="f906a-146">Now create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="f906a-147">I dati del certificato sono inseriti da Key Vault con il parametro `--secrets`.</span><span class="sxs-lookup"><span data-stu-id="f906a-147">The certificate data is injected from Key Vault with the `--secrets` parameter.</span></span> <span data-ttu-id="f906a-148">Passare la configurazione cloud-init con il parametro `--custom-data`:</span><span class="sxs-lookup"><span data-stu-id="f906a-148">You pass in the cloud-init config with the `--custom-data` parameter:</span></span>

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

<span data-ttu-id="f906a-149">Per creare la macchina virtuale, installare i pacchetti e avviare l'applicazione sono necessari alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="f906a-149">It takes a few minutes for the VM to be created, the packages to install, and the app to start.</span></span> <span data-ttu-id="f906a-150">Dopo aver creato la macchina virtuale, prendere nota del `publicIpAddress` visualizzato dall'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="f906a-150">When the VM has been created, take note of the `publicIpAddress` displayed by the Azure CLI.</span></span> <span data-ttu-id="f906a-151">Questo indirizzo viene usato per accedere al sito in un Web browser.</span><span class="sxs-lookup"><span data-stu-id="f906a-151">This address is used to access your site in a web browser.</span></span>

<span data-ttu-id="f906a-152">Per consentire al traffico Web protetto di raggiungere la macchina virtuale, aprire la porta 443 da Internet con il comando [az vm open-port](/cli/azure/vm#open-port):</span><span class="sxs-lookup"><span data-stu-id="f906a-152">To allow secure web traffic to reach your VM, open port 443 from the Internet with [az vm open-port](/cli/azure/vm#open-port):</span></span>

```azurecli-interactive 
az vm open-port \
    --resource-group myResourceGroupSecureWeb \
    --name myVM \
    --port 443
```


### <a name="test-the-secure-web-app"></a><span data-ttu-id="f906a-153">Testare l'applicazione Web protetta</span><span class="sxs-lookup"><span data-stu-id="f906a-153">Test the secure web app</span></span>
<span data-ttu-id="f906a-154">È ora possibile aprire un Web browser e immettere *https://<publicIpAddress>* nella barra degli indirizzi.</span><span class="sxs-lookup"><span data-stu-id="f906a-154">Now you can open a web browser and enter *https://<publicIpAddress>* in the address bar.</span></span> <span data-ttu-id="f906a-155">Fornire il proprio indirizzo IP pubblico dal processo di creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="f906a-155">Provide your own public IP address from the VM create process.</span></span> <span data-ttu-id="f906a-156">Se è stato usato un certificato autofirmato, accettare l'avviso di sicurezza:</span><span class="sxs-lookup"><span data-stu-id="f906a-156">Accept the security warning if you used a self-signed certificate:</span></span>

![Accettare l'avviso di sicurezza del Web browser](./media/tutorial-secure-web-server/browser-warning.png)

<span data-ttu-id="f906a-158">Il sito NGINX protetto viene quindi visualizzato come illustrato nell'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="f906a-158">Your secured NGINX site is then displayed as in the following example:</span></span>

![Visualizzare il sito protetto NGINX in esecuzione](./media/tutorial-secure-web-server/secured-nginx.png)


## <a name="next-steps"></a><span data-ttu-id="f906a-160">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f906a-160">Next steps</span></span>

<span data-ttu-id="f906a-161">In questa esercitazione si è protetto un server Web NGINX con un certificato SSL archiviato in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f906a-161">In this tutorial, you secured an NGINX web server with an SSL certificate stored in Azure Key Vault.</span></span> <span data-ttu-id="f906a-162">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="f906a-162">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f906a-163">Creare un Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="f906a-163">Create an Azure Key Vault</span></span>
> * <span data-ttu-id="f906a-164">Generare o caricare un certificato in Key Vault</span><span class="sxs-lookup"><span data-stu-id="f906a-164">Generate or upload a certificate to the Key Vault</span></span>
> * <span data-ttu-id="f906a-165">Creare una macchina virtuale e installare il server Web NGINX</span><span class="sxs-lookup"><span data-stu-id="f906a-165">Create a VM and install the NGINX web server</span></span>
> * <span data-ttu-id="f906a-166">Inserire il certificato nella macchina virtuale e configurare NGINX con un'associazione SSL</span><span class="sxs-lookup"><span data-stu-id="f906a-166">Inject the certificate into the VM and configure NGINX with an SSL binding</span></span>

<span data-ttu-id="f906a-167">Seguire questo collegamento per vedere esempi di script predefiniti delle macchine virtuali.</span><span class="sxs-lookup"><span data-stu-id="f906a-167">Follow this link to see pre-built virtual machine script samples.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f906a-168">Esempi di script delle macchine virtuali Windows</span><span class="sxs-lookup"><span data-stu-id="f906a-168">Windows virtual machine script samples</span></span>](./cli-samples.md)