---
title: App Web Django in una macchina virtuale Windows Server in Azure | Microsoft Docs
description: Informazioni su come ospitare un sito Web basato su Django in Azure usando una macchina virtuale Windows Server 2012 R2 Datacenter con il modello di distribuzione classica.
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
ms.openlocfilehash: 283a296fb39863c2801be1093cc4f56904786abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="a6313-103">App Web Hello World Django in una macchina virtuale Windows Server</span><span class="sxs-lookup"><span data-stu-id="a6313-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="a6313-104">Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Azure Resource Manager e il modello di distribuzione classica](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="a6313-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and the classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="a6313-105">Questo articolo illustra il modello di distribuzione classica.</span><span class="sxs-lookup"><span data-stu-id="a6313-105">This article describes the classic deployment model.</span></span> <span data-ttu-id="a6313-106">Per le distribuzioni più recenti si consiglia di usare il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="a6313-106">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="a6313-107">In questa esercitazione viene illustrato come ospitare un sito Web basato su Django in Windows Server nelle macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6313-107">This tutorial shows you how to host a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="a6313-108">Nell'esercitazione si presuppone che l'utente non abbia mai usato Azure.</span><span class="sxs-lookup"><span data-stu-id="a6313-108">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="a6313-109">Al termine dell'esercitazione, si disporrà di un'applicazione basata su Django in esecuzione nel cloud.</span><span class="sxs-lookup"><span data-stu-id="a6313-109">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="a6313-110">È possibile passare agli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6313-110">Learn how to:</span></span>

* <span data-ttu-id="a6313-111">Configurare una macchina virtuale di Azure per l'hosting di Django.</span><span class="sxs-lookup"><span data-stu-id="a6313-111">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="a6313-112">Sebbene nell'esercitazione la procedura venga illustrata in **Windows Server**, è possibile eseguirla anche con una macchina virtuale Linux ospitata in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6313-112">Although this tutorial explains how to do this for **Windows Server**, you can do the same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="a6313-113">Creare una nuova applicazione Django in Windows.</span><span class="sxs-lookup"><span data-stu-id="a6313-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="a6313-114">Nell'esercitazione viene illustrato come compilare una semplice applicazione Web Hello World,</span><span class="sxs-lookup"><span data-stu-id="a6313-114">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="a6313-115">ospitata in una macchina virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6313-115">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="a6313-116">In questo screenshot viene visualizzata l'applicazione completata:</span><span class="sxs-lookup"><span data-stu-id="a6313-116">The following screenshot shows the completed application:</span></span>

![Finestra del browser con la pagina hello world visualizzata in Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="a6313-118">Creare e configurare una macchina virtuale di Azure per l'hosting di Django</span><span class="sxs-lookup"><span data-stu-id="a6313-118">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="a6313-119">Per creare una macchina virtuale di Azure con la distribuzione di Windows Server 2012 R2 Datacenter, vedere [Creare una macchina virtuale con Windows nel portale di Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a6313-119">To create an Azure virtual machine with the Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="a6313-120">Impostare Azure in modo da dirigere il traffico della porta 80 proveniente dal Web alla porta 80 della macchina virtuale:</span><span class="sxs-lookup"><span data-stu-id="a6313-120">Set Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   1. <span data-ttu-id="a6313-121">Nel portale di Azure passare al dashboard e selezionare la macchina virtuale appena creata.</span><span class="sxs-lookup"><span data-stu-id="a6313-121">In the Azure portal, go to the dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="a6313-122">Far clic su **Endpoint** e selezionare **Aggiungi**.</span><span class="sxs-lookup"><span data-stu-id="a6313-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Aggiungere un endpoint](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="a6313-124">Nella pagina **Aggiungi endpoint** immettere **HTTP** nel campo **Nome**.</span><span class="sxs-lookup"><span data-stu-id="a6313-124">On the **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="a6313-125">Impostare le porte TCP pubblica e privata su **80**.</span><span class="sxs-lookup"><span data-stu-id="a6313-125">Set the public and private TCP ports to **80**.</span></span>

     ![Immettere il nome e impostare le porte pubblica e privata](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="a6313-127">Fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="a6313-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="a6313-128">Nel dashboard selezionare la VM.</span><span class="sxs-lookup"><span data-stu-id="a6313-128">In the dashboard, select your VM.</span></span> <span data-ttu-id="a6313-129">Per usare Remote Desktop Protocol (RDP) per accedere in modalità remota alla macchina virtuale di Azure appena creata, fare clic su **Connetti**.</span><span class="sxs-lookup"><span data-stu-id="a6313-129">To use Remote Desktop Protocol (RDP) to remotely sign in to the newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="a6313-130">Per le istruzioni seguenti, si suppone che l'accesso alla macchina virtuale sia stato eseguito correttamente</span><span class="sxs-lookup"><span data-stu-id="a6313-130">The following instructions assume that you signed in to the virtual machine correctly.</span></span> <span data-ttu-id="a6313-131">e che i comandi vengano inviati dalla macchina virtuale e non dal computer locale.</span><span class="sxs-lookup"><span data-stu-id="a6313-131">They also assume that you are issuing commands in the virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="a6313-132"><a id="setup"> </a>Installare Python, Django e WFastCGI</span><span class="sxs-lookup"><span data-stu-id="a6313-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="a6313-133">Per il download tramite Internet Explorer potrebbe essere necessario configurarne le impostazioni di **Sicurezza avanzata**.</span><span class="sxs-lookup"><span data-stu-id="a6313-133">To download by using Internet Explorer, you might have to configure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="a6313-134">A tale scopo, fare clic su **Start** > **Strumenti di amministrazione** > **Server Manager** > **Server locale**.</span><span class="sxs-lookup"><span data-stu-id="a6313-134">To do this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="a6313-135">Fare clic su **Configurazione sicurezza avanzata IE** e quindi **disattivare** l'opzione.</span><span class="sxs-lookup"><span data-stu-id="a6313-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="a6313-136">Installare le versioni più recenti di Python 2.7 o Python 3.4 da [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="a6313-136">Install the latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="a6313-137">Installare i pacchetti wfastcgi e django usando pip.</span><span class="sxs-lookup"><span data-stu-id="a6313-137">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="a6313-138">Per Python 2.7, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a6313-138">For Python 2.7, use the following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="a6313-139">Per Python 3.4, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a6313-139">For Python 3.4, use the following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="a6313-140">Installare IIS con FastCGI</span><span class="sxs-lookup"><span data-stu-id="a6313-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="a6313-141">Installare Internet Information Services (IIS) con il supporto FastCGI.</span><span class="sxs-lookup"><span data-stu-id="a6313-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="a6313-142">L'esecuzione può richiedere alcuni minuti.</span><span class="sxs-lookup"><span data-stu-id="a6313-142">This might take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="a6313-143">Creare una nuova applicazione Django</span><span class="sxs-lookup"><span data-stu-id="a6313-143">Create a new Django application</span></span>
1. <span data-ttu-id="a6313-144">Per creare un nuovo progetto Django, immettere in C:\inetpub\wwwroot il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a6313-144">In C:\inetpub\wwwroot, to create a new Django project, enter the following command:</span></span>
   
   <span data-ttu-id="a6313-145">Per Python 2.7, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a6313-145">For Python 2.7, use the following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="a6313-146">Per Python 3.4, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a6313-146">For Python 3.4, use the following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Risultato del comando New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="a6313-148">Il comando `django-admin` genera una struttura di base per i siti Web basati su Django:</span><span class="sxs-lookup"><span data-stu-id="a6313-148">The `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="a6313-149">`helloworld\manage.py` consente di avviare e arrestare l'hosting del sito Web basato su Django.</span><span class="sxs-lookup"><span data-stu-id="a6313-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="a6313-150">`helloworld\helloworld\settings.py` contiene le impostazioni di Django per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="a6313-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="a6313-151">`helloworld\helloworld\urls.py` contiene il codice di mapping tra ogni URL e la relativa visualizzazione.</span><span class="sxs-lookup"><span data-stu-id="a6313-151">`helloworld\helloworld\urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="a6313-152">Creare un nuovo file denominato views.py nella directory C:\inetpub\wwwroot\helloworld\helloworld.</span><span class="sxs-lookup"><span data-stu-id="a6313-152">In the C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="a6313-153">Questo file conterrà la visualizzazione del rendering della pagina "hello world".</span><span class="sxs-lookup"><span data-stu-id="a6313-153">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="a6313-154">Nell'editor del codice immettere i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6313-154">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="a6313-155">Sostituire il contenuto del file urls.py con i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a6313-155">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="a6313-156">Configurare IIS</span><span class="sxs-lookup"><span data-stu-id="a6313-156">Set up IIS</span></span>
1. <span data-ttu-id="a6313-157">Nel file applicationhost.config globale sbloccare la sezione dei gestori.</span><span class="sxs-lookup"><span data-stu-id="a6313-157">In the global applicationhost.config file, unlock the handlers section.</span></span>  <span data-ttu-id="a6313-158">In questo modo si consentirà al file web.config di usare il gestore Python.</span><span class="sxs-lookup"><span data-stu-id="a6313-158">This allows your web.config file to use the Python handler.</span></span> <span data-ttu-id="a6313-159">Aggiungere questo comando:</span><span class="sxs-lookup"><span data-stu-id="a6313-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="a6313-160">Attivare WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="a6313-160">Activate WFastCGI.</span></span> <span data-ttu-id="a6313-161">In questo modo si aggiungerà un'applicazione al file applicationhost.config globale che fa riferimento all'eseguibile dell'interprete Python e allo script wfastcgi.py.</span><span class="sxs-lookup"><span data-stu-id="a6313-161">This adds an application to the global applicationhost.config file, which refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="a6313-162">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="a6313-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="a6313-163">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="a6313-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="a6313-164">Creare un file web.config in C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="a6313-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="a6313-165">Il valore dell'attributo `scriptProcessor` deve corrispondere all'output del passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="a6313-165">The value of the `scriptProcessor` attribute should match the output from the preceding step.</span></span> <span data-ttu-id="a6313-166">Per altre informazioni sull'impostazione di wfastcgi, vedere [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="a6313-166">For more information about the wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="a6313-167">In Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="a6313-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="a6313-168">In Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="a6313-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="a6313-169">Aggiornare la posizione del sito Web predefinito IIS in modo che punti alla cartella del progetto Django:</span><span class="sxs-lookup"><span data-stu-id="a6313-169">Update the location of the IIS default website to point to the Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="a6313-170">Caricare la pagina Web nel browser.</span><span class="sxs-lookup"><span data-stu-id="a6313-170">Load the webpage in your browser.</span></span>

![Finestra del browser con la pagina hello world visualizzata in Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="a6313-172">Arrestare la macchina virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="a6313-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="a6313-173">Al termine dell'esercitazione è consigliabile arrestare o rimuovere la macchina virtuale di Azure creata per l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="a6313-173">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="a6313-174">Ciò consente di liberare risorse per altre esercitazioni ed evitare di incorrere in costi di utilizzo di Azure.</span><span class="sxs-lookup"><span data-stu-id="a6313-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
