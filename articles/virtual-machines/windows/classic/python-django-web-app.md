---
title: app web aaaDjango in una macchina virtuale Azure di Windows Server | Documenti Microsoft
description: Informazioni su come toohost un sito Web basato su Django in Azure utilizzando una VM di Windows Server 2012 R2 Datacenter con il modello di distribuzione classica hello.
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="eb235-103">App Web Hello World Django in una macchina virtuale Windows Server</span><span class="sxs-lookup"><span data-stu-id="eb235-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="eb235-104">Azure offre due diversi modelli di distribuzione per la creazione e utilizzo delle risorse: [Gestione risorse di Azure e hello modello di distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="eb235-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="eb235-105">In questo articolo viene descritto il modello di distribuzione classica hello.</span><span class="sxs-lookup"><span data-stu-id="eb235-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="eb235-106">È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello.</span><span class="sxs-lookup"><span data-stu-id="eb235-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="eb235-107">In questa esercitazione illustra come toohost un sito Web basato su Django in Windows Server in macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb235-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="eb235-108">Nell'esercitazione di hello, non si presuppone alcuna esperienza precedente con Azure.</span><span class="sxs-lookup"><span data-stu-id="eb235-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="eb235-109">Dopo aver esercitazione hello, è possibile avere un'applicazione basata su Django backup e in esecuzione nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="eb235-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="eb235-110">È possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb235-110">Learn how to:</span></span>

* <span data-ttu-id="eb235-111">Consente di impostare un Django di toohost macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb235-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="eb235-112">Sebbene in questa esercitazione viene illustrato come toodo per **Windows Server**, è possibile eseguire hello uguali per una VM Linux ospitati in Azure.</span><span class="sxs-lookup"><span data-stu-id="eb235-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="eb235-113">Creare una nuova applicazione Django in Windows.</span><span class="sxs-lookup"><span data-stu-id="eb235-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="eb235-114">Hello esercitazione vengono illustrate le modalità di applicazione web toobuild una base di Hello World.</span><span class="sxs-lookup"><span data-stu-id="eb235-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="eb235-115">un'applicazione Hello è ospitata in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb235-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="eb235-116">Hello seguente schermata mostra un'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="eb235-116">hello following screenshot shows hello completed application:</span></span>

![Una finestra del browser visualizza una pagina di hello hello world in Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="eb235-118">Creare e configurare un toohost macchina virtuale di Azure Django</span><span class="sxs-lookup"><span data-stu-id="eb235-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="eb235-119">vedere toocreate macchina virtuale di Azure con la distribuzione di Windows Server 2012 R2 Datacenter, hello [creare una macchina virtuale Windows in esecuzione in Azure portal hello](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="eb235-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="eb235-120">Impostare traffico sulla porta 80 toodirect Azure hello web tooport 80 nella macchina virtuale hello:</span><span class="sxs-lookup"><span data-stu-id="eb235-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="eb235-121">In hello portale di Azure, passare toohello dashboard e selezionare la macchina virtuale appena creata.</span><span class="sxs-lookup"><span data-stu-id="eb235-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="eb235-122">Far clic su **Endpoint** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="eb235-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Aggiungere un endpoint](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="eb235-124">In hello **aggiungere endpoint** pagina per **nome**, immettere **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="eb235-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="eb235-125">Impostare le porte TCP pubbliche e private hello troppo**80**.</span><span class="sxs-lookup"><span data-stu-id="eb235-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Immettere il nome e impostare le porte pubblica e privata](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="eb235-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb235-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="eb235-128">Nel dashboard di hello, selezionare la macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="eb235-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="eb235-129">toouse Remote Desktop Protocol (RDP) tooremotely Accedi toohello creata la macchina virtuale di Azure, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="eb235-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="eb235-130">Hello attenendosi alle istruzioni si presuppone che l'utente eseguito nella macchina virtuale toohello correttamente.</span><span class="sxs-lookup"><span data-stu-id="eb235-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="eb235-131">Si presuppone inoltre che si emette comandi nella macchina virtuale hello e non presenti nel computer locale.</span><span class="sxs-lookup"><span data-stu-id="eb235-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="eb235-132"><a id="setup"></a>Installare Python, Django e WFastCGI</span><span class="sxs-lookup"><span data-stu-id="eb235-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="eb235-133">toodownload utilizzando Internet Explorer, potrebbe essere tooconfigure Internet Explorer **configurazione sicurezza avanzata** impostazioni.</span><span class="sxs-lookup"><span data-stu-id="eb235-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="eb235-134">toodo, fare clic su **avviare** > **strumenti di amministrazione** > **Server Manager** > **diServerlocale**.</span><span class="sxs-lookup"><span data-stu-id="eb235-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="eb235-135">Fare clic su **Configurazione sicurezza avanzata IE** e quindi **disattivare** l'opzione.</span><span class="sxs-lookup"><span data-stu-id="eb235-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="eb235-136">Installare versioni più recenti di hello di Python 2.7 o 3.4 Python da [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="eb235-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="eb235-137">Installare i pacchetti hello wfastcgi e django, uso di pip.</span><span class="sxs-lookup"><span data-stu-id="eb235-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="eb235-138">Per Python 2.7, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb235-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="eb235-139">Per Python 3.4, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb235-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="eb235-140">Installare IIS con FastCGI</span><span class="sxs-lookup"><span data-stu-id="eb235-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="eb235-141">Installare Internet Information Services (IIS) con il supporto FastCGI.</span><span class="sxs-lookup"><span data-stu-id="eb235-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="eb235-142">L'operazione potrebbe richiedere diversi minuti tooexecute.</span><span class="sxs-lookup"><span data-stu-id="eb235-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="eb235-143">Creare una nuova applicazione Django</span><span class="sxs-lookup"><span data-stu-id="eb235-143">Create a new Django application</span></span>
1. <span data-ttu-id="eb235-144">In C:\inetpub\wwwroot, un nuovo progetto, Django toocreate immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb235-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="eb235-145">Per Python 2.7, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb235-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="eb235-146">Per Python 3.4, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eb235-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![risultato di Hello del comando New-AzureService hello](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="eb235-148">Hello `django-admin` comando consente di generare una struttura di base per i siti Web basati su Django:</span><span class="sxs-lookup"><span data-stu-id="eb235-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="eb235-149">`helloworld\manage.py` consente di avviare e arrestare l'hosting del sito Web basato su Django.</span><span class="sxs-lookup"><span data-stu-id="eb235-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="eb235-150">`helloworld\helloworld\settings.py` contiene le impostazioni di Django per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb235-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="eb235-151">`helloworld\helloworld\urls.py`dispone di codice di mapping hello tra ogni URL e la relativa visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="eb235-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="eb235-152">Nella directory C:\inetpub\wwwroot\helloworld\helloworld hello, creare un nuovo file denominato views.py.</span><span class="sxs-lookup"><span data-stu-id="eb235-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="eb235-153">Questo file contiene una visualizzazione hello che esegue il rendering hello "hello world" pagina.</span><span class="sxs-lookup"><span data-stu-id="eb235-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="eb235-154">Nell'editor di codice, immettere hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="eb235-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="eb235-155">Sostituire il contenuto di hello del file urls.py hello con hello seguenti comandi:</span><span class="sxs-lookup"><span data-stu-id="eb235-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="eb235-156">Configurare IIS</span><span class="sxs-lookup"><span data-stu-id="eb235-156">Set up IIS</span></span>
1. <span data-ttu-id="eb235-157">Nel file ApplicationHost. config globale hello, sbloccare la sezione dei gestori hello.</span><span class="sxs-lookup"><span data-stu-id="eb235-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="eb235-158">In questo modo il gestore di Web. config file toouse hello Python.</span><span class="sxs-lookup"><span data-stu-id="eb235-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="eb235-159">Aggiungere questo comando:</span><span class="sxs-lookup"><span data-stu-id="eb235-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="eb235-160">Attivare WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="eb235-160">Activate WFastCGI.</span></span> <span data-ttu-id="eb235-161">Consente di aggiungere un file dell'applicazione toohello globale applicationHost. config, che fa riferimento tooyour interprete eseguibile e hello wfastcgi.py script Python.</span><span class="sxs-lookup"><span data-stu-id="eb235-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="eb235-162">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="eb235-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="eb235-163">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="eb235-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="eb235-164">Creare un file web.config in C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="eb235-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="eb235-165">valore di hello Hello `scriptProcessor` attributo deve corrispondere l'output di hello dalla hello passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="eb235-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="eb235-166">Per ulteriori informazioni sull'impostazione di wfastcgi hello, vedere [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="eb235-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="eb235-167">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="eb235-167">In  Python 2.7:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   <span data-ttu-id="eb235-168">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="eb235-168">In  Python 3.4:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. <span data-ttu-id="eb235-169">Aggiornare il percorso di hello di hello IIS sito Web toopoint toohello Django cartella progetto predefinita:</span><span class="sxs-lookup"><span data-stu-id="eb235-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="eb235-170">Caricare la pagina Web hello nel browser.</span><span class="sxs-lookup"><span data-stu-id="eb235-170">Load hello webpage in your browser.</span></span>

![Una finestra del browser visualizza una pagina di hello hello world in Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="eb235-172">Arrestare la macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="eb235-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="eb235-173">Una volta terminato con questa esercitazione, si consiglia di spegnere o rimuovere una macchina virtuale di Azure creata per l'esercitazione hello hello.</span><span class="sxs-lookup"><span data-stu-id="eb235-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="eb235-174">Ciò consente di liberare risorse per altre esercitazioni ed evitare di incorrere in costi di utilizzo di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb235-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
