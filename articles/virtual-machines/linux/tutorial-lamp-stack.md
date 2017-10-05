---
title: Distribuire LAMP in una macchina virtuale Linux in Azure | Microsoft Docs
description: 'Esercitazione: installare lo stack LAMP in una macchina virtuale Linux in Azure'
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
ms.openlocfilehash: 9148ac9646e4e1cfeff8f20c096e390499437e78
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="install-a-lamp-web-server-on-an-azure-vm"></a><span data-ttu-id="9fba0-103">Installare un server Web LAMP in una macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="9fba0-103">Install a LAMP web server on an Azure VM</span></span>
<span data-ttu-id="9fba0-104">Questo articolo illustra come distribuire un server Web Apache, MySQL e PHP (lo stack LAMP) in una VM Ubuntu in Azure.</span><span class="sxs-lookup"><span data-stu-id="9fba0-104">This article walks you through how to deploy an Apache web server, MySQL, and PHP (the LAMP stack) on an Ubuntu VM in Azure.</span></span> <span data-ttu-id="9fba0-105">Se si preferisce il server Web NGINX, vedere l'esercitazione [LEMP stack](tutorial-lemp-stack.md) (Stack LEMP).</span><span class="sxs-lookup"><span data-stu-id="9fba0-105">If you prefer the NGINX web server, see the [LEMP stack](tutorial-lemp-stack.md) tutorial.</span></span> <span data-ttu-id="9fba0-106">Per verificare il funzionamento del server LAMP, è facoltativamente possibile installare e configurare un sito WordPress.</span><span class="sxs-lookup"><span data-stu-id="9fba0-106">To see the LAMP server in action, you can optionally install and configure a WordPress site.</span></span> <span data-ttu-id="9fba0-107">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="9fba0-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9fba0-108">Creare una VM Ubuntu ("L" nello stack LAMP)</span><span class="sxs-lookup"><span data-stu-id="9fba0-108">Create an Ubuntu VM (the 'L' in the LAMP stack)</span></span>
> * <span data-ttu-id="9fba0-109">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="9fba0-109">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="9fba0-110">Installare Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="9fba0-110">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="9fba0-111">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="9fba0-111">Verify installation and configuration</span></span>
> * <span data-ttu-id="9fba0-112">Installare WordPress nel server LAMP</span><span class="sxs-lookup"><span data-stu-id="9fba0-112">Install WordPress on the LAMP server</span></span>


<span data-ttu-id="9fba0-113">Per altre informazioni sullo stack LAMP, incluse le raccomandazioni per un ambiente di produzione, vedere la [documentazione di Ubuntu](https://help.ubuntu.com/community/ApacheMySQLPHP).</span><span class="sxs-lookup"><span data-stu-id="9fba0-113">For more on the LAMP stack, including recommendations for a production environment, see the [Ubuntu documentation](https://help.ubuntu.com/community/ApacheMySQLPHP).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9fba0-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questa esercitazione è necessario eseguire l'interfaccia della riga di comando di Azure versione 2.0.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="9fba0-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="9fba0-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="9fba0-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="9fba0-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="9fba0-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-apache-mysql-and-php"></a><span data-ttu-id="9fba0-117">Installare Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="9fba0-117">Install Apache, MySQL, and PHP</span></span>

<span data-ttu-id="9fba0-118">Usare il comando seguente per aggiornare le origini dei pacchetti Ubuntu e installare Apache, MySQL e PHP.</span><span class="sxs-lookup"><span data-stu-id="9fba0-118">Run the following command to update Ubuntu package sources and install Apache, MySQL, and PHP.</span></span> <span data-ttu-id="9fba0-119">Si noti l'accento circonflesso (^) alla fine del comando.</span><span class="sxs-lookup"><span data-stu-id="9fba0-119">Note the caret (^) at the end of the command.</span></span>


```bash
sudo apt update && sudo apt install lamp-server^
```



<span data-ttu-id="9fba0-120">Viene chiesto di installare i pacchetti e le altre dipendenze.</span><span class="sxs-lookup"><span data-stu-id="9fba0-120">You are prompted to install the packages and other dependencies.</span></span> <span data-ttu-id="9fba0-121">Quando viene richiesto, impostare una password radice per MySQL e quindi premere [INVIO] per continuare.</span><span class="sxs-lookup"><span data-stu-id="9fba0-121">When prompted, set a root password for MySQL, and then [Enter] to continue.</span></span> <span data-ttu-id="9fba0-122">Seguire i prompt rimanenti.</span><span class="sxs-lookup"><span data-stu-id="9fba0-122">Follow the remaining prompts.</span></span> <span data-ttu-id="9fba0-123">In questo modo vengono installate le estensioni PHP minime richieste per l'uso di PHP con MySQL.</span><span class="sxs-lookup"><span data-stu-id="9fba0-123">This process installs the minimum required PHP extensions needed to use PHP with MySQL.</span></span> 

![Pagina della password radice per MySQL][1]

## <a name="verify-installation-and-configuration"></a><span data-ttu-id="9fba0-125">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="9fba0-125">Verify installation and configuration</span></span>


### <a name="apache"></a><span data-ttu-id="9fba0-126">Apache</span><span class="sxs-lookup"><span data-stu-id="9fba0-126">Apache</span></span>

<span data-ttu-id="9fba0-127">Controllare la versione di Apache con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9fba0-127">Check the version of Apache with the following command:</span></span>
```bash
apache2 -v
```

<span data-ttu-id="9fba0-128">Con Apache installato e la porta 80 aperta per la macchina virtuale, è ora possibile accedere al server Web da Internet.</span><span class="sxs-lookup"><span data-stu-id="9fba0-128">With Apache installed, and port 80 open to your VM, the web server can now be accessed from the internet.</span></span> <span data-ttu-id="9fba0-129">Per visualizzare Apache2 Ubuntu Default Page (Pagina predefinita Apache2 Ubuntu), aprire un Web browser e immettere l'indirizzo IP pubblico della VM.</span><span class="sxs-lookup"><span data-stu-id="9fba0-129">To view the Apache2 Ubuntu Default Page, open a web browser, and enter the public IP address of the VM.</span></span> <span data-ttu-id="9fba0-130">Usare l'indirizzo IP pubblico usato per stabilire la connessione SSH alla VM:</span><span class="sxs-lookup"><span data-stu-id="9fba0-130">Use the public IP address you used to SSH to the VM:</span></span>

![Pagina predefinita di Apache][3]


### <a name="mysql"></a><span data-ttu-id="9fba0-132">MySQL</span><span class="sxs-lookup"><span data-stu-id="9fba0-132">MySQL</span></span>

<span data-ttu-id="9fba0-133">Controllare la versione di MySQL con il comando seguente. Si noti il parametro `V` in maiuscolo:</span><span class="sxs-lookup"><span data-stu-id="9fba0-133">Check the version of MySQL with the following command (note the capital `V` parameter):</span></span>

```bash
msql -V
```

<span data-ttu-id="9fba0-134">È consigliabile eseguire lo script seguente per proteggere l'installazione di MySQL:</span><span class="sxs-lookup"><span data-stu-id="9fba0-134">We recommend running the following script to help secure the installation of MySQL:</span></span>

```bash
mysql_secure_installation
```

<span data-ttu-id="9fba0-135">Immettere la password radice per MySQL e configurare le impostazioni di sicurezza per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="9fba0-135">Enter your MySQL root password, and configure the security settings for your environment.</span></span>

<span data-ttu-id="9fba0-136">Per creare un database MySQL, aggiungere utenti o modificare le impostazioni di configurazione, accedere a MySQL:</span><span class="sxs-lookup"><span data-stu-id="9fba0-136">If you want to create a MySQL database, add users, or change configuration settings, login to MySQL:</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="9fba0-137">Al termine, chiudere il prompt mysql digitando `\q`.</span><span class="sxs-lookup"><span data-stu-id="9fba0-137">When done, exit the mysql prompt by typing `\q`.</span></span>

### <a name="php"></a><span data-ttu-id="9fba0-138">PHP</span><span class="sxs-lookup"><span data-stu-id="9fba0-138">PHP</span></span>

<span data-ttu-id="9fba0-139">Controllare la versione di PHP con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="9fba0-139">Check the version of PHP with the following command:</span></span>

```bash
php -v
```

<span data-ttu-id="9fba0-140">Per eseguire altri test, creare rapidamente una pagina di informazioni PHP da visualizzare in un browser.</span><span class="sxs-lookup"><span data-stu-id="9fba0-140">If you want to test further, create a quick PHP info page to view in a browser.</span></span> <span data-ttu-id="9fba0-141">Il comando seguente crea la pagina di informazioni di PHP:</span><span class="sxs-lookup"><span data-stu-id="9fba0-141">The following command creates the PHP info page:</span></span>

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```

<span data-ttu-id="9fba0-142">Ora è possibile controllare la pagina di informazioni di PHP creata.</span><span class="sxs-lookup"><span data-stu-id="9fba0-142">Now you can check the PHP info page you created.</span></span> <span data-ttu-id="9fba0-143">Aprire un browser e passare a `http://yourPublicIPAddress/info.php`.</span><span class="sxs-lookup"><span data-stu-id="9fba0-143">Open a browser and go to `http://yourPublicIPAddress/info.php`.</span></span> <span data-ttu-id="9fba0-144">Sostituire l'indirizzo IP pubblico della VM.</span><span class="sxs-lookup"><span data-stu-id="9fba0-144">Substitute the public IP address of your VM.</span></span> <span data-ttu-id="9fba0-145">Dovrebbe avere un aspetto simile a questa immagine.</span><span class="sxs-lookup"><span data-stu-id="9fba0-145">It should look similar to this image.</span></span>

![Pagina di informazioni di PHP][2]

[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]


## <a name="next-steps"></a><span data-ttu-id="9fba0-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9fba0-147">Next steps</span></span>

<span data-ttu-id="9fba0-148">In questa esercitazione si è distribuito un server LAMP in Azure.</span><span class="sxs-lookup"><span data-stu-id="9fba0-148">In this tutorial, you deployed a LAMP server in Azure.</span></span> <span data-ttu-id="9fba0-149">Si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="9fba0-149">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9fba0-150">Creare una VM Ubuntu</span><span class="sxs-lookup"><span data-stu-id="9fba0-150">Create an Ubuntu VM</span></span>
> * <span data-ttu-id="9fba0-151">Aprire la porta 80 per il traffico Web</span><span class="sxs-lookup"><span data-stu-id="9fba0-151">Open port 80 for web traffic</span></span>
> * <span data-ttu-id="9fba0-152">Installare Apache, MySQL e PHP</span><span class="sxs-lookup"><span data-stu-id="9fba0-152">Install Apache, MySQL, and PHP</span></span>
> * <span data-ttu-id="9fba0-153">Verificare l'installazione e la configurazione</span><span class="sxs-lookup"><span data-stu-id="9fba0-153">Verify installation and configuration</span></span>
> * <span data-ttu-id="9fba0-154">Installare WordPress nel server LAMP</span><span class="sxs-lookup"><span data-stu-id="9fba0-154">Install WordPress on the LAMP server</span></span>

<span data-ttu-id="9fba0-155">Passare all'esercitazione successiva per apprendere come proteggere i server Web con i certificati SSL.</span><span class="sxs-lookup"><span data-stu-id="9fba0-155">Advance to the next tutorial to learn how to secure web servers with SSL certificates.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9fba0-156">Secure web server with SSL (Proteggere il server Web con SSL)</span><span class="sxs-lookup"><span data-stu-id="9fba0-156">Secure web server with SSL</span></span>](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lamp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lamp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lamp-stack/apachesuccesspage.png