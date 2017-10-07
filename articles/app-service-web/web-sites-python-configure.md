---
title: aaaConfiguring Python con App Web di servizio App di Azure
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
ms.openlocfilehash: 00d49fb01491e9adb4b6fededfb95669a8dbd485
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-python-with-azure-app-service-web-apps"></a><span data-ttu-id="ac830-103">Configurazione di Python con App Web del servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="ac830-103">Configuring Python with Azure App Service Web Apps</span></span>
<span data-ttu-id="ac830-104">Questa esercitazione descrive le opzioni per la creazione e la configurazione di un'applicazione Python di base conforme all'interfaccia WSGI (Web Server Gateway Interface) in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="ac830-104">This tutorial describes options for authoring and configuring a basic Web Server Gateway Interface (WSGI) compliant Python application on [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="ac830-105">Descrive le funzionalità aggiuntive della distribuzione Git, ad esempio l'ambiente virtuale e l'installazione del pacchetto con requirements.txt.</span><span class="sxs-lookup"><span data-stu-id="ac830-105">It describes additional features of Git deployment, such as virtual environment and package installation using requirements.txt.</span></span>

## <a name="bottle-django-or-flask"></a><span data-ttu-id="ac830-106">Bottle, Django o Flask?</span><span class="sxs-lookup"><span data-stu-id="ac830-106">Bottle, Django or Flask?</span></span>
<span data-ttu-id="ac830-107">Hello Azure Marketplace contiene modelli per il framework di bottiglia, Django e pallone hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-107">hello Azure Marketplace contains templates for hello Bottle, Django and Flask frameworks.</span></span> <span data-ttu-id="ac830-108">Se si sviluppa la prima app web in Azure App Service o non si ha familiarità con Git, è consigliabile adottare una di queste esercitazioni, che includono istruzioni dettagliate per la creazione di un'applicazione dalla raccolta di hello tramite distribuzione Git da Windows o Mac:</span><span class="sxs-lookup"><span data-stu-id="ac830-108">If you are developing your first web app in Azure App Service, or you are not familiar with Git, we recommend that you follow one of these tutorials, which include step-by-step instructions for building a working application from hello gallery using Git deployment from Windows or Mac:</span></span>

* [<span data-ttu-id="ac830-109">Creazione di app Web con Bottle</span><span class="sxs-lookup"><span data-stu-id="ac830-109">Creating web apps with Bottle</span></span>](web-sites-python-create-deploy-bottle-app.md)
* [<span data-ttu-id="ac830-110">Creazione di app Web con Django</span><span class="sxs-lookup"><span data-stu-id="ac830-110">Creating web apps with Django</span></span>](web-sites-python-create-deploy-django-app.md)
* [<span data-ttu-id="ac830-111">Creazione di app Web con Flask</span><span class="sxs-lookup"><span data-stu-id="ac830-111">Creating web apps with Flask</span></span>](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a><span data-ttu-id="ac830-112">Creazione di un'app Web nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="ac830-112">Web app creation on Azure Portal</span></span>
<span data-ttu-id="ac830-113">In questa esercitazione si presuppone un esistente Azure sottoscrizione e accesso toohello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ac830-113">This tutorial assumes an existing Azure subscription and access toohello Azure Portal.</span></span>

<span data-ttu-id="ac830-114">Se non si dispone di un'app web esistente, è possibile crearne uno da hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ac830-114">If you do not have an existing web app, you can create one from hello [Azure Portal](https://portal.azure.com).</span></span>  <span data-ttu-id="ac830-115">Fare clic sul pulsante nuova di hello nell'angolo superiore sinistro di hello, quindi fare clic su **Web e dispositivi mobili** > **app Web**.</span><span class="sxs-lookup"><span data-stu-id="ac830-115">Click hello NEW button in hello top left corner, then click **Web + Mobile** > **Web app**.</span></span>

## <a name="git-publishing"></a><span data-ttu-id="ac830-116">Pubblicazione Git</span><span class="sxs-lookup"><span data-stu-id="ac830-116">Git Publishing</span></span>
<span data-ttu-id="ac830-117">Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ac830-117">Configure Git publishing for your newly created web app by following hello instructions at [Local Git Deployment tooAzure App Service](app-service-deploy-local-git.md).</span></span> <span data-ttu-id="ac830-118">Questa esercitazione viene utilizzato toocreate Git, gestire e pubblicare il nostro tooAzure app web di Python servizio App.</span><span class="sxs-lookup"><span data-stu-id="ac830-118">This tutorial uses Git toocreate, manage, and publish our Python web app tooAzure App Service.</span></span>

<span data-ttu-id="ac830-119">Dopo aver configurato la pubblicazione Git, verrà creato un repository che verrà associato all'app Web.</span><span class="sxs-lookup"><span data-stu-id="ac830-119">Once Git publishing is set up, a Git repository will be created and associated with your web app.</span></span> <span data-ttu-id="ac830-120">URL del repository Hello verrà visualizzata e può essere ormai dati toopush utilizzata dal cloud di hello sviluppo locale ambiente toohello.</span><span class="sxs-lookup"><span data-stu-id="ac830-120">hello repository's URL will be displayed and can henceforth be used toopush data from hello local development environment toohello cloud.</span></span> <span data-ttu-id="ac830-121">applicazioni toopublish tramite Git, verificare che viene installato anche un client Git e le istruzioni riportate hello fornito toopush del servizio App tooAzure di web app contenuto.</span><span class="sxs-lookup"><span data-stu-id="ac830-121">toopublish applications via Git, make sure a Git client is also installed and use hello instructions provided toopush your web app content tooAzure App Service.</span></span>

## <a name="application-overview"></a><span data-ttu-id="ac830-122">Informazioni generali sull'applicazione</span><span class="sxs-lookup"><span data-stu-id="ac830-122">Application Overview</span></span>
<span data-ttu-id="ac830-123">Nelle sezioni successive di hello, viene creato i seguenti file hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-123">In hello next sections, hello following files are created.</span></span> <span data-ttu-id="ac830-124">Essi devono essere posizionati nella directory radice del repository Git hello hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-124">They should be placed in hello root of hello Git repository.</span></span>

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a><span data-ttu-id="ac830-125">Gestore WSGI</span><span class="sxs-lookup"><span data-stu-id="ac830-125">WSGI Handler</span></span>
<span data-ttu-id="ac830-126">WSGI è uno standard di Python descritto da [PEP 3333](http://www.python.org/dev/peps/pep-3333/) che definisce un'interfaccia tra i server web hello e Python.</span><span class="sxs-lookup"><span data-stu-id="ac830-126">WSGI is a Python standard described by [PEP 3333](http://www.python.org/dev/peps/pep-3333/) defining an interface between hello web server and Python.</span></span> <span data-ttu-id="ac830-127">Oggi i più comuni framework Web Python usano l'interfaccia WSGI.</span><span class="sxs-lookup"><span data-stu-id="ac830-127">It provides a standardized interface for writing various web applications and frameworks using Python.</span></span> <span data-ttu-id="ac830-128">App Web del servizio app di Azure offre assistenza per qualsiasi framework.</span><span class="sxs-lookup"><span data-stu-id="ac830-128">Popular Python web frameworks today use WSGI.</span></span> <span data-ttu-id="ac830-129">Azure offre App del servizio Web App che è il supporto per alcun Framework; Inoltre, gli utenti avanzati possono anche creare i propri come gestore personalizzato hello segue le linee guida specifiche WSGI di hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-129">Azure App Service Web Apps gives you support for any such frameworks; in addition, advanced users can even author their own as long as hello custom handler follows hello WSGI specification guidelines.</span></span>

<span data-ttu-id="ac830-130">Di seguito è riportato un esempio di un `app.py` che definisce un gestore personalizzato:</span><span class="sxs-lookup"><span data-stu-id="ac830-130">Here's an example of an `app.py` that defines a custom handler:</span></span>

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

<span data-ttu-id="ac830-131">È possibile eseguire l'applicazione localmente con `python app.py`, quindi selezionare troppo`http://localhost:5555` nel web browser.</span><span class="sxs-lookup"><span data-stu-id="ac830-131">You can run this application locally with `python app.py`, then browse too`http://localhost:5555` in your web browser.</span></span>

## <a name="virtual-environment"></a><span data-ttu-id="ac830-132">Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="ac830-132">Virtual Environment</span></span>
<span data-ttu-id="ac830-133">Anche se l'applicazione di esempio hello precedente non necessita di tutti i pacchetti esterni, è probabile che l'applicazione richiederà alcuni.</span><span class="sxs-lookup"><span data-stu-id="ac830-133">Although hello example app above doesn't require any external packages, it is likely that your application will require some.</span></span>

<span data-ttu-id="ac830-134">toohelp gestire le dipendenze di pacchetto esterno, la distribuzione Git Azure supporta la creazione di hello degli ambienti virtuali.</span><span class="sxs-lookup"><span data-stu-id="ac830-134">toohelp manage external package dependencies, Azure Git deployment supports hello creation of virtual environments.</span></span>

<span data-ttu-id="ac830-135">Quando Azure rileva un requirements.txt nella directory radice del repository hello hello, viene creato automaticamente un ambiente virtuale denominato `env`.</span><span class="sxs-lookup"><span data-stu-id="ac830-135">When Azure detects a requirements.txt in hello root of hello repository, it automatically creates a virtual environment named `env`.</span></span> <span data-ttu-id="ac830-136">Ciò si verifica solo nella prima distribuzione hello o durante qualsiasi distribuzione dopo hello runtime di Python selezionato è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="ac830-136">This only occurs on hello first deployment, or during any deployment after hello selected Python runtime has changed.</span></span>

<span data-ttu-id="ac830-137">Potrebbe essere necessario toocreate un ambiente virtuale in locale per lo sviluppo, ma non includerlo nel repository Git.</span><span class="sxs-lookup"><span data-stu-id="ac830-137">You will probably want toocreate a virtual environment locally for development, but don't include it in your Git repository.</span></span>

## <a name="package-management"></a><span data-ttu-id="ac830-138">Gestione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ac830-138">Package Management</span></span>
<span data-ttu-id="ac830-139">I pacchetti elencati in requirements.txt verranno installati automaticamente in ambiente virtuale di hello uso di pip.</span><span class="sxs-lookup"><span data-stu-id="ac830-139">Packages listed in requirements.txt will be installed automatically in hello virtual environment using pip.</span></span> <span data-ttu-id="ac830-140">Ciò avviene in ogni distribuzione, tuttavia pip non eseguirà l'installazione se un pacchetto è già installato.</span><span class="sxs-lookup"><span data-stu-id="ac830-140">This happens on every deployment, but pip will skip installation if a package is already installed.</span></span>

<span data-ttu-id="ac830-141">Esempio `requirements.txt`:</span><span class="sxs-lookup"><span data-stu-id="ac830-141">Example `requirements.txt`:</span></span>

    azure==0.8.4


## <a name="python-version"></a><span data-ttu-id="ac830-142">Versione di Python</span><span class="sxs-lookup"><span data-stu-id="ac830-142">Python Version</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

<span data-ttu-id="ac830-143">Esempio `runtime.txt`:</span><span class="sxs-lookup"><span data-stu-id="ac830-143">Example `runtime.txt`:</span></span>

    python-2.7


## <a name="webconfig"></a><span data-ttu-id="ac830-144">Web.config</span><span class="sxs-lookup"><span data-stu-id="ac830-144">Web.config</span></span>
<span data-ttu-id="ac830-145">È necessario toocreate un toospecify file Web. config come server hello deve gestire le richieste.</span><span class="sxs-lookup"><span data-stu-id="ac830-145">You'll need toocreate a web.config file toospecify how hello server should handle requests.</span></span>

<span data-ttu-id="ac830-146">Si noti che se si dispone di un file web.x.y.config nel repository, in cui x. y corrisponde hello selezionato runtime di Python, quindi Azure copierà automaticamente i file appropriati di hello come Web. config.</span><span class="sxs-lookup"><span data-stu-id="ac830-146">Note that if you have a web.x.y.config file in your repository, where x.y matches hello selected Python runtime, then Azure will automatically copy hello appropriate file as web.config.</span></span>

<span data-ttu-id="ac830-147">Hello negli esempi seguenti di Web. config si basano su uno script proxy ambiente virtuale, descritto nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-147">hello following web.config examples rely on a virtual environment proxy script, which is described in hello next section.</span></span>  <span data-ttu-id="ac830-148">E funzionano con il gestore WSGI hello utilizzato nell'esempio hello `app.py` sopra.</span><span class="sxs-lookup"><span data-stu-id="ac830-148">They work with hello WSGI handler used in hello example `app.py` above.</span></span>

<span data-ttu-id="ac830-149">`web.config` di esempio per Python 2.7:</span><span class="sxs-lookup"><span data-stu-id="ac830-149">Example `web.config` for Python 2.7:</span></span>

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


<span data-ttu-id="ac830-150">`web.config` di esempio per Python 3.4:</span><span class="sxs-lookup"><span data-stu-id="ac830-150">Example `web.config` for Python 3.4:</span></span>

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


<span data-ttu-id="ac830-151">Verranno gestiti file statici dal server web hello direttamente, senza passare attraverso il codice Python, per migliorare le prestazioni.</span><span class="sxs-lookup"><span data-stu-id="ac830-151">Static files will be handled by hello web server directly, without going through Python code, for improved performance.</span></span>

<span data-ttu-id="ac830-152">In hello esempi sopra riportati, deve corrispondere a percorso hello nell'URL hello percorso hello dei file statici di hello su disco.</span><span class="sxs-lookup"><span data-stu-id="ac830-152">In hello above examples, hello location of hello static files on disk should match hello location in hello URL.</span></span> <span data-ttu-id="ac830-153">Ciò significa che una richiesta per `http://pythonapp.azurewebsites.net/static/site.css` verrà utilizzato il file hello sul disco in `\static\site.css`.</span><span class="sxs-lookup"><span data-stu-id="ac830-153">This means that a request for `http://pythonapp.azurewebsites.net/static/site.css` will serve hello file on disk at `\static\site.css`.</span></span>

<span data-ttu-id="ac830-154">`WSGI_ALT_VIRTUALENV_HANDLER`è possibile specificare il gestore WSGI hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-154">`WSGI_ALT_VIRTUALENV_HANDLER` is where you specify hello WSGI handler.</span></span> <span data-ttu-id="ac830-155">In hello sopra esempi, ha `app.wsgi_app` perché il gestore di hello è una funzione denominata `wsgi_app` in `app.py` nella cartella radice hello.</span><span class="sxs-lookup"><span data-stu-id="ac830-155">In hello above examples, it's `app.wsgi_app` because hello handler is a function named `wsgi_app` in `app.py` in hello root folder.</span></span>

<span data-ttu-id="ac830-156">`PYTHONPATH`può essere personalizzato, ma se si installano tutte le dipendenze in ambiente virtuale hello specificandoli in requirements.txt, non deve essere toochange è.</span><span class="sxs-lookup"><span data-stu-id="ac830-156">`PYTHONPATH` can be customized, but if you install all your dependencies in hello virtual environment by specifying them in requirements.txt, you shouldn't need toochange it.</span></span>

## <a name="virtual-environment-proxy"></a><span data-ttu-id="ac830-157">Proxy dell'ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="ac830-157">Virtual Environment Proxy</span></span>
<span data-ttu-id="ac830-158">Hello lo script seguente è gestore WSGI di hello tooretrieve usato, attivare hello virtuali ambiente e registrare gli errori.</span><span class="sxs-lookup"><span data-stu-id="ac830-158">hello following script is used tooretrieve hello WSGI handler, activate hello virtual environment and log errors.</span></span> <span data-ttu-id="ac830-159">È progettato toobe generico e usati senza modifiche.</span><span class="sxs-lookup"><span data-stu-id="ac830-159">It is designed toobe generic and used without modifications.</span></span>

<span data-ttu-id="ac830-160">Contenuto di `ptvs_virtualenv_proxy.py`:</span><span class="sxs-lookup"><span data-stu-id="ac830-160">Contents of `ptvs_virtualenv_proxy.py`:</span></span>

     # ############################################################################
     #
     # Copyright (c) Microsoft Corporation. 
     #
     # This source code is subject tooterms and conditions of hello Apache License, Version 2.0. A 
     # copy of hello license can be found in hello License.html file at hello root of this distribution. If 
     # you cannot locate hello Apache License, Version 2.0, please send an email too
     # vspython@microsoft.com. By using this source code in any fashion, you are agreeing toobe bound 
     # by hello terms of hello Apache License, Version 2.0.
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
        """Logs fatal errors tooa log file if WSGI_LOG env var is defined"""
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


## <a name="customize-git-deployment"></a><span data-ttu-id="ac830-161">Personalizzare la distribuzione Git</span><span class="sxs-lookup"><span data-stu-id="ac830-161">Customize Git deployment</span></span>
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a><span data-ttu-id="ac830-162">Risoluzione dei problemi - Installazione dei pacchetti</span><span class="sxs-lookup"><span data-stu-id="ac830-162">Troubleshooting - Package Installation</span></span>
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a><span data-ttu-id="ac830-163">Risoluzione dei problemi - Ambiente virtuale</span><span class="sxs-lookup"><span data-stu-id="ac830-163">Troubleshooting - Virtual Environment</span></span>
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a><span data-ttu-id="ac830-164">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ac830-164">Next steps</span></span>
<span data-ttu-id="ac830-165">Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).</span><span class="sxs-lookup"><span data-stu-id="ac830-165">For more information, see hello [Python Developer Center](/develop/python/).</span></span>

> [!NOTE]
> <span data-ttu-id="ac830-166">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="ac830-166">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="ac830-167">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="ac830-167">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="ac830-168">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="ac830-168">What's changed</span></span>
* <span data-ttu-id="ac830-169">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="ac830-169">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

