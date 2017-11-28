---
title: aaaDeploy LAMP in una macchina virtuale di Linux in Azure | Documenti Microsoft
description: Esercitazione - stack LAMP hello di installazione in una VM Linux in Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6c12603a-e391-4d3e-acce-442dd7ebb2fe
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: a3d0ecb3277f15bd0a2fdc0d85b738a760e68865
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="812e1-103">Installare un server Web LAMP in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="812e1-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="812e1-104">In questo articolo illustra come toodeploy un Apache web server, MySQL e PHP (stack LAMP hello) in una VM Ubuntu in Azure.</span><span class="sxs-lookup"><span data-stu-id="812e1-104">This article walks you through how toodeploy an Apache web server, MySQL, and PHP (hello LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="812e1-105">Se si preferisce server web NGINX di hello, vedere hello [stack LEMP](tutorial-lemp-stack.md) esercitazione.</span><span class="sxs-lookup"><span data-stu-id="812e1-105">If you prefer hello NGINX web server, see hello [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="812e1-106">server di luce toosee hello in azione, è facoltativamente possibile installare e configurare un sito WordPress.</span><span class="sxs-lookup"><span data-stu-id="812e1-106">toosee hello LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="812e1-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="812e1-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="812e1-108">Creare una VM Ubuntu (Buongiorno "L" nello stack LAMP hello)</span><span class="sxs-lookup"><span data-stu-id="812e1-108">Create an Ubuntu VM (hello 'L' in hello LAMP stack)</span></span>
> * <span data-ttu-id="812e1-109">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="812e1-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="812e1-110">Installare Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="812e1-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="812e1-111">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="812e1-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="812e1-112">Installa WordPress nel server di luce hello</span><span class="sxs-lookup"><span data-stu-id="812e1-112">Install WordPress on hello LAMP server</span></span>


<span data-ttu-id="812e1-113">Per ulteriori informazioni su stack LAMP hello, incluse le raccomandazioni per un ambiente di produzione, vedere hello [Ubuntu documentazione](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="812e1-113">For more on hello LAMP stack, including recommendations for a production environment, see hello [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="812e1-114">Se si sceglie tooinstall e utilizza hello CLI in locale, questa esercitazione, è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="812e1-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="812e1-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="812e1-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="812e1-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="812e1-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="812e1-117">Installare Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="812e1-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="812e1-118">Eseguire le seguenti origini di comando tooupdate Ubuntu pacchetto hello e installare Apache, MySQL e PHP.</span><span class="sxs-lookup"><span data-stu-id="812e1-118">Run hello following command tooupdate Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="812e1-119">Si noti hello punto di inserimento (^) alla fine di hello del comando hello.</span><span class="sxs-lookup"><span data-stu-id="812e1-119">Note hello caret (^) at hello end of hello command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="812e1-120">Sono pacchetti hello tooinstall richiesta e altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="812e1-120">You are prompted tooinstall hello packages and other dependencies.</span></span> <span data-ttu-id="812e1-121">Quando richiesto, è possibile impostare una password radice per MySQL e toocontinue [INVIO].</span><span class="sxs-lookup"><span data-stu-id="812e1-121">When prompted, set a root password for MySQL, and then [Enter] toocontinue.</span></span> <span data-ttu-id="812e1-122">Seguire hello prompt rimanenti.</span><span class="sxs-lookup"><span data-stu-id="812e1-122">Follow hello remaining prompts.</span></span> <span data-ttu-id="812e1-123">Questo processo installa hello minimo richiesto PHP necessite estensioni toouse PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="812e1-123">This process installs hello minimum required PHP extensions needed toouse PHP with MySQL.</span></span> 

![Pagina della password radice per MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="812e1-125">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="812e1-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="812e1-126">Apache</span><span class="sxs-lookup"><span data-stu-id="812e1-126">Apache</span></span>

<span data-ttu-id="812e1-127">Controllare la versione di hello di Apache con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="812e1-127">Check hello version of Apache with hello following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="812e1-128">In quest'ultimo installato e la porta 80 aprire tooyour VM, server web hello è ora possibile accedere da hello internet.</span><span class="sxs-lookup"><span data-stu-id="812e1-128">With Apache installed, and port 80 open tooyour VM, hello web server can now be accessed from hello internet.</span></span> <span data-ttu-id="812e1-129">Ciao tooview Apache2 Ubuntu predefinito pagina, aprire un web browser e immettere l'indirizzo IP pubblico hello di hello macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="812e1-129">tooview hello Apache2 Ubuntu Default Page, open a web browser, and enter hello public IP address of hello VM.</span></span> <span data-ttu-id="812e1-130">Utilizzare l'indirizzo IP pubblico hello utilizzato tooSSH toohello VM:</span><span class="sxs-lookup"><span data-stu-id="812e1-130">Use hello public IP address you used tooSSH toohello VM:</span></span>

![Pagina predefinita di Apache][3]


### <a name="mysql"></a><span data-ttu-id="812e1-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="812e1-132">MySQL</span></span>

<span data-ttu-id="812e1-133">Controllare la versione di hello di MySQL con hello comando seguente (si noti il capitale hello `V` parametro):</span><span class="sxs-lookup"><span data-stu-id="812e1-133">Check hello version of MySQL with hello following command (note hello capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="812e1-134">Si consiglia di eseguire script toohelp hello sicuro al termine dell'installazione di MySQL hello:</span><span class="sxs-lookup"><span data-stu-id="812e1-134">We recommend running hello following script toohelp secure hello installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="812e1-135">Immettere la password radice MySQL e configurare le impostazioni di sicurezza hello per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="812e1-135">Enter your MySQL root password, and configure hello security settings for your environment.</span></span>

<span data-ttu-id="812e1-136">Se si desidera toocreate un database MySQL, gli utenti di aggiungere o modificare le impostazioni di configurazione, account di accesso tooMySQL:</span><span class="sxs-lookup"><span data-stu-id="812e1-136">If you want toocreate a MySQL database, add users, or change configuration settings, login tooMySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="812e1-137">Al termine, uscire dal prompt dei comandi mysql hello immettendo `\q`.</span><span class="sxs-lookup"><span data-stu-id="812e1-137">When done, exit hello mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="812e1-138">PHP</span><span class="sxs-lookup"><span data-stu-id="812e1-138">PHP</span></span>

<span data-ttu-id="812e1-139">Controllare la versione di hello di PHP con hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="812e1-139">Check hello version of PHP with hello following command:</span></span>

```bash
php -v
```

<span data-ttu-id="812e1-140">Se si desidera tootest ulteriormente, creare un rapido tooview pagina informazioni PHP in un browser.</span><span class="sxs-lookup"><span data-stu-id="812e1-140">If you want tootest further, create a quick PHP info page tooview in a browser.</span></span> <span data-ttu-id="812e1-141">Hello comando seguente crea una pagina di informazioni di hello PHP:</span><span class="sxs-lookup"><span data-stu-id="812e1-141">hello following command creates hello PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="812e1-142">Ora è possibile controllare pagina delle info PHP hello che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="812e1-142">Now you can check hello PHP info page you created.</span></span> <span data-ttu-id="812e1-143">Aprire un browser e andare troppo`http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="812e1-143">Open a browser and go too`http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="812e1-144">Sostituire l'indirizzo IP pubblico hello della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="812e1-144">Substitute hello public IP address of your VM.</span></span> <span data-ttu-id="812e1-145">Dovrebbe essere simile toothis immagine.</span><span class="sxs-lookup"><span data-stu-id="812e1-145">It should look similar toothis image.</span></span>

![Pagina di informazioni di PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="812e1-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="812e1-147">Next steps</span></span>

<span data-ttu-id="812e1-148">In questa esercitazione si è distribuito un server LAMP in Azure.</span><span class="sxs-lookup"><span data-stu-id="812e1-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="812e1-149">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="812e1-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="812e1-150">Creare una VM Ubuntu</span><span class="sxs-lookup"><span data-stu-id="812e1-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="812e1-151">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="812e1-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="812e1-152">Installare Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="812e1-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="812e1-153">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="812e1-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="812e1-154">Installa WordPress nel server di luce hello</span><span class="sxs-lookup"><span data-stu-id="812e1-154">Install WordPress on hello LAMP server</span></span>

<span data-ttu-id="812e1-155">Spostare toolearn esercitazione successiva toohello come server web toosecure con certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="812e1-155">Advance toohello next tutorial toolearn how toosecure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="812e1-156">Secure web server with SSL (Proteggere il server Web con SSL)</span><span class="sxs-lookup"><span data-stu-id="812e1-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png