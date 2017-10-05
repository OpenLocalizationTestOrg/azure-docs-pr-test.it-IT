---
title: Configurazione di Python con App Web del servizio app di Azure
description: Questa esercitazione descrive le opzioni per la creazione e la configurazione di un'applicazione Python di base conforme all'interfaccia WSGI (Web Server Gateway Interface) in App Web del servizio app di Azure.
services: app-service
documentationcenter: python
tags: python
author: huguesv
manager: erikre
editor: 
ms.assetid: fd00dc91-9935-4331-b955-4bd71e66d518
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 02/26/2016
ms.author: huvalo
ms.openlocfilehash: 9683a1af13eeff364d3c4714f0b791324fd82659
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="b6f6c-103">Configurazione di Python con App Web del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="b6f6c-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="b6f6c-104">Questa esercitazione descrive le opzioni per la creazione e la configurazione di un'applicazione Python di base conforme all'interfaccia WSGI (Web Server Gateway Interface) in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="b6f6c-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="b6f6c-105">Descrive le funzionalità aggiuntive della distribuzione Git, ad esempio l'ambiente virtuale e l'installazione del pacchetto con requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="b6f6c-106">Bottle, Django o Flask?</span><span class="sxs-lookup"><span data-stu-id="b6f6c-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="b6f6c-107">Azure Marketplace contiene modelli per i framework Bottle, Django e Flask.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-107">The Azure Marketplace contains templates for the Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="b6f6c-108">Se si sta sviluppando la prima app Web nel servizio app di Azure o non si ha familiarità con Git, è consigliabile seguire una delle esercitazioni seguenti, che includono istruzioni dettagliate per la creazione di un'applicazione funzionante dalla raccolta tramite la distribuzione Git da Windows o Mac:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from the gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="b6f6c-109">Creazione di app Web con Bottle</span><span class="sxs-lookup"><span data-stu-id="b6f6c-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="b6f6c-110">Creazione di app Web con Django</span><span class="sxs-lookup"><span data-stu-id="b6f6c-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="b6f6c-111">Creazione di app Web con Flask</span><span class="sxs-lookup"><span data-stu-id="b6f6c-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="b6f6c-112">Creazione di un'app Web nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b6f6c-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="b6f6c-113">Per seguire questa esercitazione è necessaria una sottoscrizione di Azure e l'accesso al portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-113">This tutorial assumes an existing Azure subscription and access to the Azure Portal.</span></span>

<span data-ttu-id="b6f6c-114">Se non si dispone di un'app Web esistente, è possibile crearne una dal [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b6f6c-114">If you do not have an existing web app, you can create one from the [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="b6f6c-115">Fare clic sul pulsante NUOVO nell'angolo superiore sinistro e quindi su **Web e dispositivi mobili** > **App Web**.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-115">Click the NEW button in the top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="b6f6c-116">Pubblicazione Git</span><span class="sxs-lookup"><span data-stu-id="b6f6c-116">Git Publishing</span></span>
<span data-ttu-id="b6f6c-117">Configurare la pubblicazione Git per l'app Web appena creata seguendo le istruzioni disponibili in [Distribuzione del repository Git locale nel servizio app di Azure](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="b6f6c-117">Configure Git publishing for your newly created web app by following the instructions at [Local Git Deployment to Azure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="b6f6c-118">Questa esercitazione usa Git per creare, gestire e pubblicare l'app Web Python nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-118">This tutorial uses Git to create, manage, and publish our Python web app to Azure App Service.</span></span>

<span data-ttu-id="b6f6c-119">Dopo aver configurato la pubblicazione Git, verrà creato un repository che verrà associato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="b6f6c-120">L'URL del repository verrà visualizzato e potrà pertanto essere usato per effettuare il push dei dati dall'ambiente di sviluppo locale al cloud.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-120">The repository's URL will be displayed and can henceforth be used to push data from the local development environment to the cloud.</span></span> <span data-ttu-id="b6f6c-121">Per pubblicare applicazioni tramite Git, assicurarsi che sia stato installato anche il client Git e attenersi alle istruzioni fornite per eseguire il push dei contenuti dell'app Web nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-121">To publish applications via Git, make sure a Git client is also installed and use the instructions provided to push your web app content to Azure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="b6f6c-122">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="b6f6c-122">Application Overview</span></span>
<span data-ttu-id="b6f6c-123">Nelle sezioni successive vengono creati i seguenti file.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-123">In the next sections, the following files are created.</span></span> <span data-ttu-id="b6f6c-124">Devono essere posizionati nella radice del repository Git.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-124">They should be placed in the root of the Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="b6f6c-125">Gestore WSGI</span><span class="sxs-lookup"><span data-stu-id="b6f6c-125">WSGI Handler</span></span>
<span data-ttu-id="b6f6c-126">WSGI è uno standard Python descritto da [PEP 3333](http://www.python.org/dev/peps/pep-3333/) che definisce un'interfaccia tra il server Web e Python che consente di scrivere varie applicazioni e framework Web tramite Python.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between the web server and Python.</span></span> <span data-ttu-id="b6f6c-127">Oggi i più comuni framework Web Python usano l'interfaccia WSGI.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="b6f6c-128">App Web del servizio app di Azure offre assistenza per qualsiasi framework.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="b6f6c-129">Inoltre, gli utenti avanzati possono anche creare il proprio framework a patto che il gestore personalizzato si attenga alle linee guida delle specifiche WSGI.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as the custom handler follows the WSGI specification guidelines.</span></span>

<span data-ttu-id="b6f6c-130">Di seguito è riportato un esempio di un `app.py` che definisce un gestore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

    def wsgi_app(environ, start_response):
        status = '200 OK'
        response_headers = [('Content-type', 'text/plain')]
        start_response(status, response_headers)
        response_body = 'Hello World'
        yield response_body.encode()

    if __name__ == '__main__':
        from wsgiref.simple_server import make_server

        httpd = make_server('localhost', 5555, wsgi_app)
        httpd.serve_forever()

<span data-ttu-id="b6f6c-131">È possibile eseguire l'applicazione localmente con `python app.py`, quindi passare a `http://localhost:5555` nel Web browser.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-131">You can run this application locally with `python app.py`, then browse to `http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="b6f6c-132">Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="b6f6c-132">Virtual Environment</span></span>
<span data-ttu-id="b6f6c-133">Sebbene l'app dell'esempio precedente non necessiti di pacchetti esterni, è probabile che l'applicazione creata ne richieda alcuni.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-133">Although the example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="b6f6c-134">Per gestire le dipendenze di pacchetti esterni, la distribuzione Git di Azure supporta la creazione di ambienti virtuali.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-134">To help manage external package dependencies, Azure Git deployment supports the creation of virtual environments.</span></span>

<span data-ttu-id="b6f6c-135">Quando Azure rileva un file requirements.txt nella radice del repository, crea automaticamente un ambiente virtuale denominato `env`.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-135">When Azure detects a requirements.txt in the root of the repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="b6f6c-136">Questo si verifica solo durante la prima distribuzione o durante una qualsiasi distribuzione dopo che è cambiato il runtime di Python selezionato.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-136">This only occurs on the first deployment, or during any deployment after the selected Python runtime has changed.</span></span>

<span data-ttu-id="b6f6c-137">È opportuno creare un ambiente virtuale locale per lo sviluppo, ma evitare di includerlo nel repository Git.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-137">You will probably want to create a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="b6f6c-138">Gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="b6f6c-138">Package Management</span></span>
<span data-ttu-id="b6f6c-139">I pacchetti elencati in requirements.txt verranno installati automaticamente nell'ambiente virtuale tramite pip.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-139">Packages listed in requirements.txt will be installed automatically in the virtual environment using pip.</span></span> <span data-ttu-id="b6f6c-140">Ciò avviene in ogni distribuzione, tuttavia pip non eseguirà l'installazione se un pacchetto è già installato.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="b6f6c-141">Esempio `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="b6f6c-142">Versione di Python</span><span class="sxs-lookup"><span data-stu-id="b6f6c-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="b6f6c-143">Esempio `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="b6f6c-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="b6f6c-144">Web.config</span></span>
<span data-ttu-id="b6f6c-145">È necessario creare un file web.config per specificare il modo in cui il server deve gestire le richieste.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-145">You'll need to create a web.config file to specify how the server should handle requests.</span></span>

<span data-ttu-id="b6f6c-146">Si noti che se nel repository si dispone di un file web.x.y.config, dove x.y corrisponde al runtime di Python selezionato, Azure copierà automaticamente il file appropriato come web.config.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-146">Note that if you have a web.x.y.config file in your repository, where x.y matches the selected Python runtime, then Azure will automatically copy the appropriate file as web.config.</span></span>

<span data-ttu-id="b6f6c-147">I seguenti esempi di file web.config si basano su uno script proxy dell'ambiente virtuale, descritto nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-147">The following web.config examples rely on a virtual environment proxy script, which is described in the next section.</span></span>  <span data-ttu-id="b6f6c-148">Funzionano con il gestore WSGI usato nell' `app.py` di esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-148">They work with the WSGI handler used in the example `app.py` above.</span></span>

<span data-ttu-id="b6f6c-149">`web.config` di esempio per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-149">Example `web.config` for Python 2.7:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\activate_this.py" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_virtualenv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python27\python.exe|D:\Python27\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite"
                      url="handler.fcgi/{R:1}"
                      appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="b6f6c-150">`web.config` di esempio per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-150">Example `web.config` for Python 3.4:</span></span>

    <?xml version="1.0"?>
    <configuration>
      <appSettings>
        <add key="WSGI_ALT_VIRTUALENV_HANDLER" value="app.wsgi_app" />
        <add key="WSGI_ALT_VIRTUALENV_ACTIVATE_THIS"
             value="D:\home\site\wwwroot\env\Scripts\python.exe" />
        <add key="WSGI_HANDLER"
             value="ptvs_virtualenv_proxy.get_venv_handler()" />
        <add key="PYTHONPATH" value="D:\home\site\wwwroot" />
      </appSettings>
      <system.web>
        <compilation debug="true" targetFramework="4.0" />
      </system.web>
      <system.webServer>
        <modules runAllManagedModulesForAllRequests="true" />
        <handlers>
          <remove name="Python27_via_FastCGI" />
          <remove name="Python34_via_FastCGI" />
          <add name="Python FastCGI"
               path="handler.fcgi"
               verb="*"
               modules="FastCgiModule"
               scriptProcessor="D:\Python34\python.exe|D:\Python34\Scripts\wfastcgi.py"
               resourceType="Unspecified"
               requireAccess="Script" />
        </handlers>
        <rewrite>
          <rules>
            <rule name="Static Files" stopProcessing="true">
              <conditions>
                <add input="true" pattern="false" />
              </conditions>
            </rule>
            <rule name="Configure Python" stopProcessing="true">
              <match url="(.*)" ignoreCase="false" />
              <conditions>
                <add input="{REQUEST_URI}" pattern="^/static/.*" ignoreCase="true" negate="true" />
              </conditions>
              <action type="Rewrite" url="handler.fcgi/{R:1}" appendQueryString="true" />
            </rule>
          </rules>
        </rewrite>
      </system.webServer>
    </configuration>


<span data-ttu-id="b6f6c-151">I file statici verranno gestiti direttamente dal server Web, senza passare per il codice Python, per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-151">Static files will be handled by the web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="b6f6c-152">Negli esempi precedenti il percorso dei file statici sul disco deve corrispondere al percorso nell'URL.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-152">In the above examples, the location of the static files on disk should match the location in the URL.</span></span> <span data-ttu-id="b6f6c-153">Ciò significa che una richiesta per `http://pythonapp.azurewebsites.net/static/site.css` servirà il file sul disco nel percorso `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve the file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="b6f6c-154">`WSGI_ALT_VIRTUALENV_HANDLER` viene specificato il gestore WSGI.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify the WSGI handler.</span></span> <span data-ttu-id="b6f6c-155">Negli esempi precedenti corrisponde a `app.wsgi_app` perché il gestore è una funzione denominata `wsgi_app` in `app.py` nella cartella radice.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-155">In the above examples, it's `app.wsgi_app` because the handler is a function named `wsgi_app` in `app.py` in the root folder.</span></span>

<span data-ttu-id="b6f6c-156">`PYTHONPATH` può essere personalizzato ma, se si installano tutte le dipendenze nell'ambiente virtuale specificandole in requirements.txt, non è necessario modificarlo.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-156">`PYTHONPATH` can be customized, but if you install all your dependencies in the virtual environment by specifying them in requirements.txt, you shouldn't need to change it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="b6f6c-157">Proxy dell'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="b6f6c-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="b6f6c-158">Il seguente script viene usato per recuperare il gestore WSGI, attivare l'ambiente virtuale e registrare gli errori.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-158">The following script is used to retrieve the WSGI handler, activate the virtual environment and log errors.</span></span> <span data-ttu-id="b6f6c-159">È progettato per essere generico e per essere usato senza doverlo modificare.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-159">It is designed to be generic and used without modifications.</span></span>

<span data-ttu-id="b6f6c-160">Contenuto di `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="b6f6c-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject to terms and conditions of the Apache License, Version 2.0. A 
     # copy of the license can be found in the License.html file at the root of this distribution. If 
     # you cannot locate the Apache License, Version 2.0, please send an email to 
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing to be bound 
     # by the terms of the Apache License, Version 2.0.
     #
     # You must not remove this notice, or any other, from this software.
     #
     # ###########################################################################

    import datetime
    import os
    import sys
    import traceback

    if sys.version_info[0] == 3:
        def to_str(value):
            return value.decode(sys.getfilesystemencoding())

        def execfile(path, global_dict):
            """Execute a file"""
            with open(path, 'r') as f:
                code = f.read()
            code = code.replace('\r\n', '\n') + '\n'
            exec(code, global_dict)
    else:
        def to_str(value):
            return value.encode(sys.getfilesystemencoding())

    def log(txt):
        """Logs fatal errors to a log file if WSGI_LOG env var is defined"""
        log_file = os.environ.get('WSGI_LOG')
        if log_file:
            f = open(log_file, 'a+')
            try:
                f.write('%s: %s' % (datetime.datetime.now(), txt))
            finally:
                f.close()

    ptvsd_secret = os.getenv('WSGI_PTVSD_SECRET')
    if ptvsd_secret:
        log('Enabling ptvsd ...\n')
        try:
            import ptvsd
            try:
                ptvsd.enable_attach(ptvsd_secret)
                log('ptvsd enabled.\n')
            except: 
                log('ptvsd.enable_attach failed\n')
        except ImportError:
            log('error importing ptvsd.\n')

    def get_wsgi_handler(handler_name):
        if not handler_name:
            raise Exception('WSGI_ALT_VIRTUALENV_HANDLER env var must be set')

        if not isinstance(handler_name, str):
            handler_name = to_str(handler_name)

        module_name, _, callable_name = handler_name.rpartition('.')
        should_call = callable_name.endswith('()')
        callable_name = callable_name[:-2] if should_call else callable_name
        name_list = [(callable_name, should_call)]
        handler = None
        last_tb = ''

        while module_name:
            try:
                handler = __import__(module_name, fromlist=[name_list[0][0]])
                last_tb = ''
                for name, should_call in name_list:
                    handler = getattr(handler, name)
                    if should_call:
                        handler = handler()
                break
            except ImportError:
                module_name, _, callable_name = module_name.rpartition('.')
                should_call = callable_name.endswith('()')
                callable_name = callable_name[:-2] if should_call else callable_name
                name_list.insert(0, (callable_name, should_call))
                handler = None
                last_tb = ': ' + traceback.format_exc()

        if handler is None:
            raise ValueError('"%s" could not be imported%s' % (handler_name, last_tb))

        return handler

    activate_this = os.getenv('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS')
    if not activate_this:
        raise Exception('WSGI_ALT_VIRTUALENV_ACTIVATE_THIS is not set')

    def get_virtualenv_handler():
        log('Activating virtualenv with %s\n' % activate_this)
        execfile(activate_this, dict(__file__=activate_this))

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler

    def get_venv_handler():
        log('Activating venv with executable at %s\n' % activate_this)
        import site
        sys.executable = activate_this
        old_sys_path, sys.path = sys.path, []

        site.main()

        sys.path.insert(0, '')
        for item in old_sys_path:
            if item not in sys.path:
                sys.path.append(item)

        log('Getting handler %s\n' % os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        handler = get_wsgi_handler(os.getenv('WSGI_ALT_VIRTUALENV_HANDLER'))
        log('Got handler: %r\n' % handler)
        return handler


## <a name="customize-git-deployment"></a><span data-ttu-id="b6f6c-161">Personalizzare la distribuzione Git</span><span class="sxs-lookup"><span data-stu-id="b6f6c-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="b6f6c-162">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="b6f6c-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="b6f6c-163">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="b6f6c-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="b6f6c-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b6f6c-164">Next steps</span></span>
<span data-ttu-id="b6f6c-165">Per ulteriori informazioni, vedere il [Centro per sviluppatori di Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="b6f6c-165">For more information, see the [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="b6f6c-166">Per iniziare a usare il servizio app di Azure prima di registrarsi per ottenere un account Azure, andare a [Prova il servizio app](https://azure.microsoft.com/try/app-service/), dove è possibile creare un'app Web iniziale temporanea nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-166">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b6f6c-167">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="b6f6c-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="b6f6c-168">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="b6f6c-168">What's changed</span></span>
* <span data-ttu-id="b6f6c-169">Per una guida relativa al passaggio da Siti Web al servizio app, vedere [Servizio app di Azure e impatto sui servizi di Azure esistenti](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b6f6c-169">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

