---
title: aaaDeploy LEMP in una macchina virtuale di Linux in Azure | Documenti Microsoft
description: Esercitazione - stack LEMP hello di installazione in una VM Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a><span data-ttu-id="6bb7b-103">Installare un server Web LEMP in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="6bb7b-103">Install a LEMP web server on an Azure VM</span></span>
<span data-ttu-id="6bb7b-104">In questo articolo illustra come un NGINX toodeploy web server, MySQL e PHP (stack LEMP hello) in una VM Ubuntu in Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-104">This article walks you through how toodeploy an NGINX web server, MySQL, and PHP (hello LEMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="6bb7b-105">stack LEMP Hello è un'alternativa toohello diffuso [stack LAMP](tutorial-lamp-stack.md), che è anche possibile installare in Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-105">hello LEMP stack is an alternative toohello popular [LAMP stack](tutorial-lamp-stack.md), which you can also install in Azure.</span></span> <span data-ttu-id="6bb7b-106">server LEMP toosee hello in azione, è facoltativamente possibile installare e configurare un sito WordPress.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-106">toosee hello LEMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="6bb7b-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bb7b-108">Creare una VM Ubuntu (Buongiorno "L" nello stack LEMP hello)</span><span class="sxs-lookup"><span data-stu-id="6bb7b-108">Create an Ubuntu VM (hello 'L' in hello LEMP stack)</span></span>
> * <span data-ttu-id="6bb7b-109">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="6bb7b-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="6bb7b-110">Installare NGINX, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="6bb7b-110">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="6bb7b-111">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="6bb7b-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="6bb7b-112">Installa WordPress sul server LEMP hello</span><span class="sxs-lookup"><span data-stu-id="6bb7b-112">Install WordPress on hello LEMP server</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6bb7b-113">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="6bb7b-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6bb7b-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6bb7b-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a><span data-ttu-id="6bb7b-116">Installare NGINX, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="6bb7b-116">Install NGINX, MySQL, and PHP</span></span>

<span data-ttu-id="6bb7b-117">Eseguire le seguenti origini di comando tooupdate Ubuntu pacchetto hello e installare NGINX, MySQL e PHP.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-117">Run hello following command tooupdate Ubuntu package sources and install NGINX, MySQL, and PHP.</span></span> 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

<span data-ttu-id="6bb7b-118">Sono pacchetti hello tooinstall richiesta e altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-118">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="6bb7b-119">Quando richiesto, è possibile impostare una password radice per MySQL e toocontinue [INVIO].</span><span class="sxs-lookup"><span data-stu-id="6bb7b-119">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="6bb7b-120">Seguire hello prompt rimanenti.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-120">Follow hello remaining prompts.</span></span> <span data-ttu-id="6bb7b-121">Questo processo installa hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-121">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Pagina della password radice per MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="6bb7b-123">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="6bb7b-123">Verify installation and configuration</span></span>


### <a name="nginx"></a><span data-ttu-id="6bb7b-124">NGINX</span><span class="sxs-lookup"><span data-stu-id="6bb7b-124">NGINX</span></span>

<span data-ttu-id="6bb7b-125">Controllare la versione di hello di NGINX con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-125">Check hello version of NGINX with hello following command:</span></span>
```bash
nginx -v
```

<span data-ttu-id="6bb7b-126">Con NGINX installato e la porta 80 aprire tooyour VM, server web hello è ora possibile accedere da hello internet.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-126">With NGINX installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="6bb7b-127">pagina iniziale NGINX hello tooview, aprire un web browser e immettere l'indirizzo IP pubblico hello di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-127">tooview hello NGINX welcome page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="6bb7b-128">Utilizzare l'indirizzo IP pubblico hello utilizzato tooSSH toohello VM:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-128">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Pagina NGINX predefinita][3]


### <a name="mysql"></a><span data-ttu-id="6bb7b-130">MySQL</span><span class="sxs-lookup"><span data-stu-id="6bb7b-130">MySQL</span></span>

<span data-ttu-id="6bb7b-131">Controllare la versione di hello di MySQL con hello comando seguente (si noti il capitale hello `V` parametro):</span><span class="sxs-lookup"><span data-stu-id="6bb7b-131">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="6bb7b-132">Si consiglia di eseguire script toohelp hello sicuro al termine dell'installazione di MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-132">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="6bb7b-133">Immettere la password radice MySQL e configurare le impostazioni di sicurezza hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-133">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="6bb7b-134">Se si desidera toocreate un database MySQL, gli utenti di aggiungere o modificare le impostazioni di configurazione, account di accesso tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-134">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="6bb7b-135">Al termine, uscire dal prompt dei comandi mysql hello immettendo `\q`.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-135">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="6bb7b-136">PHP</span><span class="sxs-lookup"><span data-stu-id="6bb7b-136">PHP</span></span>

<span data-ttu-id="6bb7b-137">Controllare la versione di hello di PHP con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-137">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="6bb7b-138">Configurare hello toouse NGINX gestore di processi FastCGI PHP (PHP FPM).</span><span class="sxs-lookup"><span data-stu-id="6bb7b-138">Configure NGINX toouse hello PHP FastCGI Process Manager (PHP-FPM).</span></span> <span data-ttu-id="6bb7b-139">Eseguire i seguenti comandi tooback server NGINX originale hello bloccare il file di configurazione e quindi modificare il file originale di hello in un editor di propria scelta hello:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-139">Run hello following commands tooback up hello original NGINX server block config file and then edit hello original file in an editor of your choice:</span></span>

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

<span data-ttu-id="6bb7b-140">Nell'editor di hello, sostituire il contenuto di hello di `/etc/nginx/sites-available/default` con seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-140">In hello editor, replace hello contents of `/etc/nginx/sites-available/default` with hello following.</span></span> <span data-ttu-id="6bb7b-141">Vedere i commenti di hello per una descrizione delle impostazioni di hello.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-141">See hello comments for explanation of hello settings.</span></span> <span data-ttu-id="6bb7b-142">Sostituire l'indirizzo IP pubblico hello della macchina virtuale per *yourPublicIPAddress*, lasciando hello rimanenti impostazioni.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-142">Substitute hello public IP address of your VM for *yourPublicIPAddress*, and leave hello remaining settings.</span></span> <span data-ttu-id="6bb7b-143">Quindi salvare il file hello.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-143">Then save hello file.</span></span>

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

<span data-ttu-id="6bb7b-144">Controllare la configurazione di NGINX hello errori di sintassi:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-144">Check hello NGINX configuration for syntax errors:</span></span>

```bash
sudo nginx -t
```

<span data-ttu-id="6bb7b-145">Se la sintassi di hello è corretta, riavviare NGINX con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-145">If hello syntax is correct, restart NGINX with hello following command:</span></span>

```bash
sudo service nginx restart
```

<span data-ttu-id="6bb7b-146">Se si desidera tootest ulteriormente, creare un rapido tooview pagina informazioni PHP in un browser.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-146">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="6bb7b-147">Hello comando seguente crea una pagina di informazioni di hello PHP:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-147">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



<span data-ttu-id="6bb7b-148">Ora è possibile controllare pagina delle info PHP hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-148">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="6bb7b-149">Aprire un browser e andare troppo`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-149">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="6bb7b-150">Sostituire l'indirizzo IP pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-150">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="6bb7b-151">Dovrebbe essere simile toothis immagine.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-151">It should look similar toothis image.</span></span>

![Pagina di informazioni di PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a><span data-ttu-id="6bb7b-153">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6bb7b-153">Next steps</span></span>

<span data-ttu-id="6bb7b-154">In questa esercitazione si è distribuito un server LEMP in Azure.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-154">In this tutorial, you deployed a LEMP server in Azure.</span></span> <span data-ttu-id="6bb7b-155">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="6bb7b-155">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6bb7b-156">Creare una VM Ubuntu</span><span class="sxs-lookup"><span data-stu-id="6bb7b-156">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="6bb7b-157">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="6bb7b-157">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="6bb7b-158">Installare NGINX, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="6bb7b-158">Install NGINX, MySQL, and PHP</span></span>
> * <span data-ttu-id="6bb7b-159">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="6bb7b-159">Verify installation and configuration</span></span>
> * <span data-ttu-id="6bb7b-160">Installa WordPress nello stack LEMP hello</span><span class="sxs-lookup"><span data-stu-id="6bb7b-160">Install WordPress on hello LEMP stack</span></span>

<span data-ttu-id="6bb7b-161">Spostare toolearn esercitazione successiva toohello come server web toosecure con certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="6bb7b-161">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6bb7b-162">Secure web server with SSL (Proteggere il server Web con SSL)</span><span class="sxs-lookup"><span data-stu-id="6bb7b-162">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
