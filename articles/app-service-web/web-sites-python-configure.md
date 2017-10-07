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
# <a name="configuring-python-with-azure-app-service-web-apps"></a>Configurazione di Python con App Web del servizio app di Azure
Questa esercitazione descrive le opzioni per la creazione e la configurazione di un'applicazione Python di base conforme all'interfaccia WSGI (Web Server Gateway Interface) in [App Web del servizio app di Azure](http://go.microsoft.com/fwlink/?LinkId=529714).

Descrive le funzionalità aggiuntive della distribuzione Git, ad esempio l'ambiente virtuale e l'installazione del pacchetto con requirements.txt.

## <a name="bottle-django-or-flask"></a>Bottle, Django o Flask?
Hello Azure Marketplace contiene modelli per il framework di bottiglia, Django e pallone hello. Se si sviluppa la prima app web in Azure App Service o non si ha familiarità con Git, è consigliabile adottare una di queste esercitazioni, che includono istruzioni dettagliate per la creazione di un'applicazione dalla raccolta di hello tramite distribuzione Git da Windows o Mac:

* [Creazione di app Web con Bottle](web-sites-python-create-deploy-bottle-app.md)
* [Creazione di app Web con Django](web-sites-python-create-deploy-django-app.md)
* [Creazione di app Web con Flask](web-sites-python-create-deploy-flask-app.md)

## <a name="web-app-creation-on-azure-portal"></a>Creazione di un'app Web nel portale di Azure
In questa esercitazione si presuppone un esistente Azure sottoscrizione e accesso toohello portale di Azure.

Se non si dispone di un'app web esistente, è possibile crearne uno da hello [portale Azure](https://portal.azure.com).  Fare clic sul pulsante nuova di hello nell'angolo superiore sinistro di hello, quindi fare clic su **Web e dispositivi mobili** > **app Web**.

## <a name="git-publishing"></a>Pubblicazione Git
Configurare la pubblicazione Git per l'app web appena creato seguendo le istruzioni di hello in [tooAzure distribuzione Git locale del servizio App](app-service-deploy-local-git.md). Questa esercitazione viene utilizzato toocreate Git, gestire e pubblicare il nostro tooAzure app web di Python servizio App.

Dopo aver configurato la pubblicazione Git, verrà creato un repository che verrà associato all'app Web. URL del repository Hello verrà visualizzata e può essere ormai dati toopush utilizzata dal cloud di hello sviluppo locale ambiente toohello. applicazioni toopublish tramite Git, verificare che viene installato anche un client Git e le istruzioni riportate hello fornito toopush del servizio App tooAzure di web app contenuto.

## <a name="application-overview"></a>Informazioni generali sull'applicazione
Nelle sezioni successive di hello, viene creato i seguenti file hello. Essi devono essere posizionati nella directory radice del repository Git hello hello.

    app.py
    requirements.txt
    runtime.txt
    web.config
    ptvs_virtualenv_proxy.py


## <a name="wsgi-handler"></a>Gestore WSGI
WSGI è uno standard di Python descritto da [PEP 3333](http://www.python.org/dev/peps/pep-3333/) che definisce un'interfaccia tra i server web hello e Python. Oggi i più comuni framework Web Python usano l'interfaccia WSGI. App Web del servizio app di Azure offre assistenza per qualsiasi framework. Azure offre App del servizio Web App che è il supporto per alcun Framework; Inoltre, gli utenti avanzati possono anche creare i propri come gestore personalizzato hello segue le linee guida specifiche WSGI di hello.

Di seguito è riportato un esempio di un `app.py` che definisce un gestore personalizzato:

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

È possibile eseguire l'applicazione localmente con `python app.py`, quindi selezionare troppo`http://localhost:5555` nel web browser.

## <a name="virtual-environment"></a>Ambiente virtuale
Anche se l'applicazione di esempio hello precedente non necessita di tutti i pacchetti esterni, è probabile che l'applicazione richiederà alcuni.

toohelp gestire le dipendenze di pacchetto esterno, la distribuzione Git Azure supporta la creazione di hello degli ambienti virtuali.

Quando Azure rileva un requirements.txt nella directory radice del repository hello hello, viene creato automaticamente un ambiente virtuale denominato `env`. Ciò si verifica solo nella prima distribuzione hello o durante qualsiasi distribuzione dopo hello runtime di Python selezionato è stato modificato.

Potrebbe essere necessario toocreate un ambiente virtuale in locale per lo sviluppo, ma non includerlo nel repository Git.

## <a name="package-management"></a>Gestione dei pacchetti
I pacchetti elencati in requirements.txt verranno installati automaticamente in ambiente virtuale di hello uso di pip. Ciò avviene in ogni distribuzione, tuttavia pip non eseguirà l'installazione se un pacchetto è già installato.

Esempio `requirements.txt`:

    azure==0.8.4


## <a name="python-version"></a>Versione di Python
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-runtime.md)]

Esempio `runtime.txt`:

    python-2.7


## <a name="webconfig"></a>Web.config
È necessario toocreate un toospecify file Web. config come server hello deve gestire le richieste.

Si noti che se si dispone di un file web.x.y.config nel repository, in cui x. y corrisponde hello selezionato runtime di Python, quindi Azure copierà automaticamente i file appropriati di hello come Web. config.

Hello negli esempi seguenti di Web. config si basano su uno script proxy ambiente virtuale, descritto nella sezione successiva hello.  E funzionano con il gestore WSGI hello utilizzato nell'esempio hello `app.py` sopra.

`web.config` di esempio per Python 2.7:

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


`web.config` di esempio per Python 3.4:

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


Verranno gestiti file statici dal server web hello direttamente, senza passare attraverso il codice Python, per migliorare le prestazioni.

In hello esempi sopra riportati, deve corrispondere a percorso hello nell'URL hello percorso hello dei file statici di hello su disco. Ciò significa che una richiesta per `http://pythonapp.azurewebsites.net/static/site.css` verrà utilizzato il file hello sul disco in `\static\site.css`.

`WSGI_ALT_VIRTUALENV_HANDLER`è possibile specificare il gestore WSGI hello. In hello sopra esempi, ha `app.wsgi_app` perché il gestore di hello è una funzione denominata `wsgi_app` in `app.py` nella cartella radice hello.

`PYTHONPATH`può essere personalizzato, ma se si installano tutte le dipendenze in ambiente virtuale hello specificandoli in requirements.txt, non deve essere toochange è.

## <a name="virtual-environment-proxy"></a>Proxy dell'ambiente virtuale
Hello lo script seguente è gestore WSGI di hello tooretrieve usato, attivare hello virtuali ambiente e registrare gli errori. È progettato toobe generico e usati senza modifiche.

Contenuto di `ptvs_virtualenv_proxy.py`:

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


## <a name="customize-git-deployment"></a>Personalizzare la distribuzione Git
[!INCLUDE [web-sites-python-customizing-runtime](../../includes/web-sites-python-customizing-deployment.md)]

## <a name="troubleshooting---package-installation"></a>Risoluzione dei problemi - Installazione dei pacchetti
[!INCLUDE [web-sites-python-troubleshooting-package-installation](../../includes/web-sites-python-troubleshooting-package-installation.md)]

## <a name="troubleshooting---virtual-environment"></a>Risoluzione dei problemi - Ambiente virtuale
[!INCLUDE [web-sites-python-troubleshooting-virtual-environment](../../includes/web-sites-python-troubleshooting-virtual-environment.md)]

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro per sviluppatori Python](/develop/python/).

> [!NOTE]
> Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App. Non è necessario fornire una carta di credito né impegnarsi in alcun modo.
> 
> 

## <a name="whats-changed"></a>Modifiche apportate
* Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

