---
title: App Web Python con Django in una macchina virtuale Linux di Azure | Microsoft Docs
description: Informazioni su come ospitare un'app Web basata su Django in Azure usando una macchina virtuale Linux.
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 6e2ab8c7da7496d0e2b567a4bdc9341adcf01552
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="4189a-103">App Web Hello World Django in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="4189a-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4189a-104">Windows</span><span class="sxs-lookup"><span data-stu-id="4189a-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="4189a-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="4189a-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="4189a-106">In questa esercitazione viene illustrato come ospitare un sito Web basato su Django in Linux nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="4189a-106">This tutorial shows you how to host a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="4189a-107">Nell'esercitazione si presuppone che l'utente non abbia mai usato Azure.</span><span class="sxs-lookup"><span data-stu-id="4189a-107">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="4189a-108">Al termine dell'esercitazione, si disporrà di un'applicazione basata su Django in esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="4189a-108">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="4189a-109">È possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4189a-109">Learn how to:</span></span>

* <span data-ttu-id="4189a-110">Configurare una macchina virtuale di Azure per l'hosting di Django.</span><span class="sxs-lookup"><span data-stu-id="4189a-110">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="4189a-111">Sebbene nell'esercitazione la procedura venga illustrata in **Linux**, è possibile eseguirla anche con una macchina virtuale Windows Server ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="4189a-111">Although this tutorial explains how to do this for **Linux**, you can do the same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="4189a-112">Creare una nuova applicazione Django in Linux.</span><span class="sxs-lookup"><span data-stu-id="4189a-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="4189a-113">Nell'esercitazione viene illustrato come compilare una semplice applicazione Web Hello World,</span><span class="sxs-lookup"><span data-stu-id="4189a-113">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="4189a-114">ospitata in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4189a-114">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="4189a-115">In questo screenshot viene visualizzata l'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="4189a-115">The following screenshot shows the completed application:</span></span>

![Finestra del browser con la pagina Hello World visualizzata in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="4189a-117">Creare e configurare una macchina virtuale di Azure per l'hosting di Django</span><span class="sxs-lookup"><span data-stu-id="4189a-117">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="4189a-118">Per creare una macchina virtuale di Azure con la distribuzione di Ubuntu Server 14.04 LTS, vedere [Creare una macchina virtuale Linux con il portale di Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4189a-118">To create an Azure virtual machine with the Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in the Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4189a-119">È anche possibile scegliere l'autenticazione della password invece di usare una chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="4189a-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="4189a-120">Per modificare il gruppo di sicurezza di rete per consentire il traffico HTTP in ingresso alla porta 80, vedere [Creare gruppi di sicurezza di rete mediante il portale di Azure](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="4189a-120">To edit the network security group to allow incoming HTTP traffic to port 80, see [Create network security groups in the Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="4189a-121">(Facoltativo) La nuova macchina virtuale non dispone di un nome di dominio completo (FQDN) per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="4189a-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="4189a-122">Per creare una macchina virtuale con un nome di dominio completo, vedere [Creare un nome di dominio completo nel portale di Azure per una macchina virtuale Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4189a-122">To create a VM with an FQDN, see [Create an FQDN in the Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="4189a-123">Questo passaggio non è necessario per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4189a-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="4189a-124"><a id="setup"> </a>Configurare l'ambiente di sviluppo</span><span class="sxs-lookup"><span data-stu-id="4189a-124"><a id="setup"> </a>Set up the development environment</span></span>
> [!NOTE]
> <span data-ttu-id="4189a-125">Se è necessario installare Python o si desidera usare le librerie client, vedere la [Guida all'installazione di Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="4189a-125">If you need to install Python or want to use the client libraries, see the [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="4189a-126">La macchina virtuale Ubuntu Linux include già Python 2.7, ma non Apache o Django.</span><span class="sxs-lookup"><span data-stu-id="4189a-126">The Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="4189a-127">Per connettersi alla macchina virtuale e installare Apache e Django, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="4189a-127">Complete the following steps to connect to your VM and install Apache and Django:</span></span>

1. <span data-ttu-id="4189a-128">Aprire una nuova finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="4189a-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="4189a-129">Per connettersi alla macchina virtuale di Azure, immettere il comando seguente.</span><span class="sxs-lookup"><span data-stu-id="4189a-129">To connect to the Azure VM, enter the following command.</span></span> <span data-ttu-id="4189a-130">Se non è stato creato un nome di dominio completo, è possibile connettersi usando l'indirizzo IP pubblico visualizzato nel riepilogo della macchina virtuale nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4189a-130">If you didn't create an FQDN, you can connect by using the public IP address that's displayed in the virtual machine summary in the Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="4189a-131">Per installare Django, immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4189a-131">To install Django, enter the following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="4189a-132">Per installare Apache con mod-wsgi, immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4189a-132">To install Apache with mod-wsgi, enter the following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="4189a-133">Creare una nuova app Django</span><span class="sxs-lookup"><span data-stu-id="4189a-133">Create a new Django app</span></span>
1. <span data-ttu-id="4189a-134">Per usare SSH per accedere alla macchina virtuale, aprire la finestra del terminale usata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="4189a-134">To use SSH to access your VM, open the Terminal window you used in the preceding section.</span></span>
2. <span data-ttu-id="4189a-135">Per creare un nuovo progetto Django, immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4189a-135">To create a new Django project, enter the following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="4189a-136">Lo script `django-admin.py` genera una struttura di base per i siti Web basati su Django:</span><span class="sxs-lookup"><span data-stu-id="4189a-136">The `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="4189a-137">`helloworld/manage.py` consente di avviare e arrestare l'hosting del sito Web basato su Django.</span><span class="sxs-lookup"><span data-stu-id="4189a-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="4189a-138">`helloworld/helloworld/settings.py` contiene le impostazioni di Django per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4189a-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="4189a-139">`helloworld/helloworld/urls.py` contiene il codice di mapping tra ogni URL e la relativa visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="4189a-139">`helloworld/helloworld/urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="4189a-140">Nella directory /var/www/helloworld/helloworld creare un nuovo file denominato views.py.</span><span class="sxs-lookup"><span data-stu-id="4189a-140">In the /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="4189a-141">Questo file conterrà la visualizzazione del rendering della pagina "hello world".</span><span class="sxs-lookup"><span data-stu-id="4189a-141">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="4189a-142">Nell'editor del codice immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4189a-142">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="4189a-143">Sostituire il contenuto del file urls.py con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="4189a-143">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="4189a-144">Configurare Apache</span><span class="sxs-lookup"><span data-stu-id="4189a-144">Set up Apache</span></span>
1. <span data-ttu-id="4189a-145">Creare un file di configurazione dell'host virtuale Apache nella cartella /etc/apache2/sites-available/helloworld.conf.</span><span class="sxs-lookup"><span data-stu-id="4189a-145">In the /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="4189a-146">Impostare il contenuto sui valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="4189a-146">Set the contents to the following values.</span></span> <span data-ttu-id="4189a-147">Sostituire *yourVmName* con il nome effettivo del computer in uso (ad esempio, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="4189a-147">Replace *yourVmName* with the actual name of the machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="4189a-148">Per attivare il sito, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4189a-148">To activate the site, use the following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="4189a-149">Per riavviare Apache, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="4189a-149">To restart Apache, use the following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="4189a-150">Caricare la pagina Web nel browser:</span><span class="sxs-lookup"><span data-stu-id="4189a-150">Load the webpage in your browser:</span></span>
   
   ![Finestra del browser con la pagina hello world visualizzata in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="4189a-152">Arrestare la macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="4189a-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="4189a-153">Al termine dell'esercitazione è consigliabile arrestare o rimuovere la macchina virtuale di Azure creata per l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="4189a-153">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="4189a-154">Ciò consente di liberare risorse per altre esercitazioni ed evitare di incorrere in costi di utilizzo di Azure.</span><span class="sxs-lookup"><span data-stu-id="4189a-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

