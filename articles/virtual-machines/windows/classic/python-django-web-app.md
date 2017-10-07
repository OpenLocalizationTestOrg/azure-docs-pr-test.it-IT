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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>App Web Hello World Django in una macchina virtuale Windows Server

> [!IMPORTANT] 
> Azure offre due diversi modelli di distribuzione per la creazione e utilizzo delle risorse: [Gestione risorse di Azure e hello modello di distribuzione classica](../../../resource-manager-deployment-model.md). In questo articolo viene descritto il modello di distribuzione classica hello. È consigliabile che più nuove distribuzioni di usare il modello di gestione risorse hello.

In questa esercitazione illustra come toohost un sito Web basato su Django in Windows Server in macchine virtuali di Azure. Nell'esercitazione di hello, non si presuppone alcuna esperienza precedente con Azure. Dopo aver esercitazione hello, è possibile avere un'applicazione basata su Django backup e in esecuzione nel cloud hello.

È possibile passare agli argomenti seguenti:

* Consente di impostare un Django di toohost macchina virtuale di Azure. Sebbene in questa esercitazione viene illustrato come toodo per **Windows Server**, è possibile eseguire hello uguali per una VM Linux ospitati in Azure.
* Creare una nuova applicazione Django in Windows.

Hello esercitazione vengono illustrate le modalità di applicazione web toobuild una base di Hello World. un'applicazione Hello è ospitata in una macchina virtuale di Azure.

Hello seguente schermata mostra un'applicazione hello completata:

![Una finestra del browser visualizza una pagina di hello hello world in Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Creare e configurare un toohost macchina virtuale di Azure Django

1. vedere toocreate macchina virtuale di Azure con la distribuzione di Windows Server 2012 R2 Datacenter, hello [creare una macchina virtuale Windows in esecuzione in Azure portal hello](tutorial.md).
2. Impostare traffico sulla porta 80 toodirect Azure hello web tooport 80 nella macchina virtuale hello:
   
   1. In hello portale di Azure, passare toohello dashboard e selezionare la macchina virtuale appena creata.
   2. Far clic su **Endpoint** e selezionare **Aggiungi**.

     ![Aggiungere un endpoint](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. In hello **aggiungere endpoint** pagina per **nome**, immettere **HTTP**. Impostare le porte TCP pubbliche e private hello troppo**80**.

     ![Immettere il nome e impostare le porte pubblica e privata](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Fare clic su **OK**.
     
3. Nel dashboard di hello, selezionare la macchina virtuale. toouse Remote Desktop Protocol (RDP) tooremotely Accedi toohello creata la macchina virtuale di Azure, fare clic su **Connetti**.  

> [!IMPORTANT] 
> Hello attenendosi alle istruzioni si presuppone che l'utente eseguito nella macchina virtuale toohello correttamente. Si presuppone inoltre che si emette comandi nella macchina virtuale hello e non presenti nel computer locale.

## <a id="setup"></a>Installare Python, Django e WFastCGI
> [!NOTE]
> toodownload utilizzando Internet Explorer, potrebbe essere tooconfigure Internet Explorer **configurazione sicurezza avanzata** impostazioni. toodo, fare clic su **avviare** > **strumenti di amministrazione** > **Server Manager** > **diServerlocale**. Fare clic su **Configurazione sicurezza avanzata IE** e quindi **disattivare** l'opzione.

1. Installare versioni più recenti di hello di Python 2.7 o 3.4 Python da [python.org][python.org].
2. Installare i pacchetti hello wfastcgi e django, uso di pip.
   
    Per Python 2.7, utilizzare hello comando seguente:
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Per Python 3.4, utilizzare hello comando seguente:
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Installare IIS con FastCGI
* Installare Internet Information Services (IIS) con il supporto FastCGI. L'operazione potrebbe richiedere diversi minuti tooexecute.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Creare una nuova applicazione Django
1. In C:\inetpub\wwwroot, un nuovo progetto, Django toocreate immettere hello comando seguente:
   
   Per Python 2.7, utilizzare hello comando seguente:
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Per Python 3.4, utilizzare hello comando seguente:
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![risultato di Hello del comando New-AzureService hello](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Hello `django-admin` comando consente di generare una struttura di base per i siti Web basati su Django:
   
   * `helloworld\manage.py` consente di avviare e arrestare l'hosting del sito Web basato su Django.
   * `helloworld\helloworld\settings.py` contiene le impostazioni di Django per l'applicazione.
   * `helloworld\helloworld\urls.py`dispone di codice di mapping hello tra ogni URL e la relativa visualizzazione.
3. Nella directory C:\inetpub\wwwroot\helloworld\helloworld hello, creare un nuovo file denominato views.py. Questo file contiene una visualizzazione hello che esegue il rendering hello "hello world" pagina. Nell'editor di codice, immettere hello seguenti comandi:
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Sostituire il contenuto di hello del file urls.py hello con hello seguenti comandi:
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Configurare IIS
1. Nel file ApplicationHost. config globale hello, sbloccare la sezione dei gestori hello.  In questo modo il gestore di Web. config file toouse hello Python. Aggiungere questo comando:
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Attivare WFastCGI. Consente di aggiungere un file dell'applicazione toohello globale applicationHost. config, che fa riferimento tooyour interprete eseguibile e hello wfastcgi.py script Python.
   
    In Python 2.7:
   
        C:\python27\scripts\wfastcgi-enable
   
    In Python 3.4:
   
        C:\python34\scripts\wfastcgi-enable
3. Creare un file web.config in C:\inetpub\wwwroot\helloworld. valore di hello Hello `scriptProcessor` attributo deve corrispondere l'output di hello dalla hello passaggio precedente. Per ulteriori informazioni sull'impostazione di wfastcgi hello, vedere [pypi wfastcgi][wfastcgi].
   
   In Python 2.7:
   
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
   
   In Python 3.4:
   
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
4. Aggiornare il percorso di hello di hello IIS sito Web toopoint toohello Django cartella progetto predefinita:
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Caricare la pagina Web hello nel browser.

![Una finestra del browser visualizza una pagina di hello hello world in Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Arrestare la macchina virtuale di Azure
Una volta terminato con questa esercitazione, si consiglia di spegnere o rimuovere una macchina virtuale di Azure creata per l'esercitazione hello hello. Ciò consente di liberare risorse per altre esercitazioni ed evitare di incorrere in costi di utilizzo di Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
