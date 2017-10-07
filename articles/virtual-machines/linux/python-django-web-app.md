---
title: app web aaaPython con Django in una macchina virtuale Linux di Azure | Documenti Microsoft
description: Informazioni su come toohost a Django basato su web app in Azure utilizzando una VM Linux.
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
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="2c39a-103">App Web Hello World Django in una macchina virtuale Linux</span><span class="sxs-lookup"><span data-stu-id="2c39a-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="2c39a-104">Windows</span><span class="sxs-lookup"><span data-stu-id="2c39a-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="2c39a-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="2c39a-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="2c39a-106">In questa esercitazione illustra come toohost un sito Web basato su Django in Linux in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="2c39a-107">Nell'esercitazione di hello, non si presuppone alcuna esperienza precedente con Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="2c39a-108">Dopo aver esercitazione hello, è possibile avere un'applicazione basata su Django backup e in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="2c39a-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="2c39a-109">È possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="2c39a-109">Learn how to:</span></span>

* <span data-ttu-id="2c39a-110">Consente di impostare un Django di toohost macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="2c39a-111">Sebbene in questa esercitazione viene illustrato come toodo per **Linux**, è possibile eseguire hello uguali per una macchina virtuale di Windows Server ospitato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="2c39a-112">Creare una nuova applicazione Django in Linux.</span><span class="sxs-lookup"><span data-stu-id="2c39a-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="2c39a-113">Hello esercitazione vengono illustrate le modalità di applicazione web toobuild una base di Hello World.</span><span class="sxs-lookup"><span data-stu-id="2c39a-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="2c39a-114">un'applicazione Hello è ospitata in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="2c39a-115">Hello seguente schermata mostra un'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="2c39a-115">hello following screenshot shows hello completed application:</span></span>

![Una finestra del browser visualizza una pagina di Hello World hello in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="2c39a-117">Creare e configurare un toohost macchina virtuale di Azure Django</span><span class="sxs-lookup"><span data-stu-id="2c39a-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="2c39a-118">vedere toocreate macchina virtuale di Azure con distribuzione Ubuntu Server 14.04 LTS, hello [creare una macchina virtuale Linux nel portale di Azure hello](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c39a-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2c39a-119">È anche possibile scegliere l'autenticazione della password invece di usare una chiave pubblica SSH.</span><span class="sxs-lookup"><span data-stu-id="2c39a-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="2c39a-120">tooedit hello rete sicurezza gruppo tooallow in ingresso HTTP traffico tooport 80, vedere [creare gruppi di sicurezza di rete nel portale di Azure hello](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="2c39a-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="2c39a-121">(Facoltativo) La nuova macchina virtuale non dispone di un nome di dominio completo (FQDN) per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="2c39a-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="2c39a-122">toocreate una macchina virtuale con un nome di dominio completo, vedere [creare un nome di dominio completo in hello portale di Azure per una macchina virtuale Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="2c39a-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="2c39a-123">Questo passaggio non è necessario per completare questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2c39a-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="2c39a-124"><a id="setup"></a>Configurare un ambiente di sviluppo hello</span><span class="sxs-lookup"><span data-stu-id="2c39a-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="2c39a-125">Se è necessario tooinstall Python o le librerie client di hello toouse, vedere hello [Guida all'installazione di Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="2c39a-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="2c39a-126">Hello Ubuntu Linux VM include Python 2.7 preinstallati, ma non proviene con Apache o Django.</span><span class="sxs-lookup"><span data-stu-id="2c39a-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="2c39a-127">Completare i seguenti passaggi tooconnect tooyour VM hello e installare il pacchetto Apache e Django:</span><span class="sxs-lookup"><span data-stu-id="2c39a-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="2c39a-128">Aprire una nuova finestra del terminale.</span><span class="sxs-lookup"><span data-stu-id="2c39a-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="2c39a-129">tooconnect toohello macchina virtuale di Azure, immettere hello comando seguente.</span><span class="sxs-lookup"><span data-stu-id="2c39a-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="2c39a-130">Se non è stato creato un nome di dominio completo, è possibile connettersi utilizzando l'indirizzo IP pubblico hello che viene visualizzato nella macchina virtuale hello riepilogo in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="2c39a-131">tooinstall Django, immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2c39a-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="2c39a-132">tooinstall Apache con mod-wsgi, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2c39a-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="2c39a-133">Creare una nuova app Django</span><span class="sxs-lookup"><span data-stu-id="2c39a-133">Create a new Django app</span></span>
1. <span data-ttu-id="2c39a-134">tooaccess SSH toouse la macchina virtuale, la finestra Terminal aprire hello usato nella precedente sezione hello.</span><span class="sxs-lookup"><span data-stu-id="2c39a-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="2c39a-135">un nuovo progetto, Django toocreate immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2c39a-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="2c39a-136">Hello `django-admin.py` script genera una struttura di base per i siti Web basati su Django:</span><span class="sxs-lookup"><span data-stu-id="2c39a-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="2c39a-137">`helloworld/manage.py` consente di avviare e arrestare l'hosting del sito Web basato su Django.</span><span class="sxs-lookup"><span data-stu-id="2c39a-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="2c39a-138">`helloworld/helloworld/settings.py` contiene le impostazioni di Django per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2c39a-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="2c39a-139">`helloworld/helloworld/urls.py`dispone di codice di mapping hello tra ogni URL e la relativa visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="2c39a-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="2c39a-140">Nella directory /var/www/helloworld/helloworld hello, creare un nuovo file denominato views.py.</span><span class="sxs-lookup"><span data-stu-id="2c39a-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="2c39a-141">Questo file contiene una visualizzazione hello che esegue il rendering hello "hello world" pagina.</span><span class="sxs-lookup"><span data-stu-id="2c39a-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="2c39a-142">Nell'editor di codice, immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2c39a-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="2c39a-143">Sostituire il contenuto di hello del file urls.py hello con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="2c39a-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="2c39a-144">Configurare Apache</span><span class="sxs-lookup"><span data-stu-id="2c39a-144">Set up Apache</span></span>
1. <span data-ttu-id="2c39a-145">Nella cartella /etc/apache2/sites-available/helloworld.conf hello, creare un file di configurazione host virtuale Apache.</span><span class="sxs-lookup"><span data-stu-id="2c39a-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="2c39a-146">Impostare hello contenuto toohello i valori seguenti.</span><span class="sxs-lookup"><span data-stu-id="2c39a-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="2c39a-147">Sostituire *Nomevm* con nome effettivo del hello della macchina hello in uso (ad esempio, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="2c39a-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="2c39a-148">sito di hello tooactivate, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2c39a-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="2c39a-149">toorestart Apache, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2c39a-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="2c39a-150">Caricare la pagina Web hello nel browser:</span><span class="sxs-lookup"><span data-stu-id="2c39a-150">Load hello webpage in your browser:</span></span>
   
   ![Una finestra del browser visualizza una pagina di hello hello world in Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="2c39a-152">Arrestare la macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="2c39a-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="2c39a-153">Una volta terminato con questa esercitazione, si consiglia di spegnere o rimuovere una macchina virtuale di Azure creata per l'esercitazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="2c39a-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="2c39a-154">Ciò consente di liberare risorse per altre esercitazioni ed evitare di incorrere in costi di utilizzo di Azure.</span><span class="sxs-lookup"><span data-stu-id="2c39a-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

