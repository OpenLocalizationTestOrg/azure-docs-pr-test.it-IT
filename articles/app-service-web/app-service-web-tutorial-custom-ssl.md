---
title: aaaBind SSL personalizzato esistente certificato App Web tooAzure | Documenti Microsoft
description: Informazioni tootoobind un'applicazione web di tooyour di certificati SSL personalizzati, back-end dell'app mobile o app per le API in Azure App Service.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 5d5bf588-b0bb-4c6d-8840-1b609cfb5750
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 06/23/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3503ba9f96c8ea8d18451e8bf9a9b441797ef44d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="bind-an-existing-custom-ssl-certificate-tooazure-web-apps"></a>Associare un esistente personalizzato SSL certificato tooAzure App Web

Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. Questa esercitazione viene illustrato come toobind un SSL personalizzato certificato che si è acquistato da un'autorità di certificazione troppo[App Web di Azure](app-service-web-overview.md). Al termine, sarà in grado di tooaccess app web in endpoint HTTPS hello del dominio DNS personalizzato.

![App Web con certificato SSL personalizzato](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

In questa esercitazione si apprenderà come:

> [!div class="checklist"]
> * Aggiornare il piano tariffario dell'app
> * Associare il tooApp di certificato SSL del servizio personalizzato
> * Imporre HTTPS per l'app
> * Automatizzare l'associazione dei certificati SSL con gli script

> [!NOTE]
> Se è necessario un certificato SSL personalizzato tooget, è possibile ottenere uno nel portale di Azure hello direttamente e associarlo tooyour web app. Seguire hello [esercitazione i certificati di servizio App](web-sites-purchase-ssl-web-site.md).

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

- [Creare un'app del Servizio app](/azure/app-service/)
- [Eseguire il mapping di un'app web tooyour di nome DNS personalizzata](app-service-web-tutorial-custom-domain.md)
- Acquisire un certificato SSL da un'autorità di certificazione attendibile

<a name="requirements"></a>

### <a name="requirements-for-your-ssl-certificate"></a>Requisiti per il certificato SSL

toouse un certificato nel servizio App, il certificato di hello deve soddisfare hello tutti i requisiti seguenti:

* Deve essere firmato da un'autorità di certificazione attendibile
* Deve essere esportato come file PFX protetto da password
* Deve contenere una chiave privata costituita da almeno 2048 bit
* Contiene tutti i certificati intermedi nella catena di certificati hello

> [!NOTE]
> Sebbene non siano descritti in questo articolo, i **certificati di crittografia a curva ellittica (ECC)** possono essere usati con il servizio app. Funziona con un'autorità di certificazione in certificati ECC toocreate passaggi esatti di hello.

## <a name="prepare-your-web-app"></a>Preparare l'app Web

toobind un SSL personalizzato certificato tooyour app web, il [piano di servizio App](https://azure.microsoft.com/pricing/details/app-service/) deve essere in hello **base**, **Standard**, o **Premium** livello. In questo passaggio assicurarsi che l'app web è in hello supportata piano tariffario.

### <a name="log-in-tooazure"></a>Accedi tooAzure

Aprire hello [portale di Azure](https://portal.azure.com).

### <a name="navigate-tooyour-web-app"></a>Passare tooyour web app

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web.

![Selezionare l'app Web](./media/app-service-web-tutorial-custom-ssl/select-app.png)

Atterraggio nella pagina di gestione di hello dell'app web.  

### <a name="check-hello-pricing-tier"></a>Controllo hello piano tariffario

Nella finestra di navigazione a sinistra di hello della pagina web app, scorrere toohello **impostazioni** sezione e selezionare **scalabilità verticale (piano di servizio App)**.

![Menu di scalabilità verticale](./media/app-service-web-tutorial-custom-ssl/scale-up-menu.png)

Controllare toomake assicurarsi che l'app web non hello **libero** o **Shared** livello. Il livello corrente dell'app Web è evidenziato da una casella blu scuro.

![Controllare il piano tariffario](./media/app-service-web-tutorial-custom-ssl/check-pricing-tier.png)

SSL personalizzato non è supportato in hello **libero** o **Shared** livello. Se è necessario tooscale backup, seguire i passaggi di hello nella sezione successiva hello. In alternativa, chiudere hello **scegliere il piano tariffario** pagina e andare troppo[caricare e associare il certificato SSL](#upload).

### <a name="scale-up-your-app-service-plan"></a>Passare a un piano di servizio app superiore

Selezionare una delle hello **base**, **Standard**, o **Premium** livelli.

Fare clic su **Seleziona**.

![Scegliere un piano tariffario](./media/app-service-web-tutorial-custom-ssl/choose-pricing-tier.png)

Quando viene visualizzata hello previa notifica, l'operazione di ridimensionamento hello è stata completata.

![Notifica di passaggio al livello superiore](./media/app-service-web-tutorial-custom-ssl/scale-notification.png)

<a name="upload"></a>

## <a name="bind-your-ssl-certificate"></a>Associare il certificato SSL

Si sono pronti tooupload app web tooyour certificato SSL.

### <a name="merge-intermediate-certificates"></a>Unire i certificati intermedi

Se un'autorità di certificazione consente più certificati nella catena di certificati hello, sono necessari i certificati di hello toomerge in ordine. 

toodo questa operazione, aprire ogni certificato ricevuto in un editor di testo. 

Creare un file di certificato unite hello, denominato _mergedcertificate.crt_. In un editor di testo, copiare il contenuto di hello di ogni certificato in questo file. ordine di Hello certificati dovrebbe essere simile hello seguente modello:

```
-----BEGIN CERTIFICATE-----
<your Base64 encoded SSL certificate>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 1>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded intermediate certificate 2>
-----END CERTIFICATE-----

-----BEGIN CERTIFICATE-----
<Base64 encoded root certificate>
-----END CERTIFICATE-----
```

### <a name="export-certificate-toopfx"></a>Esporta certificato tooPFX

Esportare il certificato SSL unito con la chiave privata hello generata con la richiesta di certificato.

Se è stato usato OpenSSL per generare la richiesta del certificato, è stato creato un file di chiave privata. tooexport tooPFX il certificato, eseguire hello comando seguente. Sostituire i segnaposto hello  _&lt;file di chiave privata >_ e  _&lt;file di certificato unito >_.

```
openssl pkcs12 -export -out myserver.pfx -inkey <private-key-file> -in <merged-certificate-file>  
```

Quando richiesto, definire una password di esportazione. Utilizzare questa password quando si carica il SSL certificato tooApp servizio in un secondo momento.

Se si utilizza IIS o _Certreq.exe_ toogenerate la richiesta di certificato, installa hello certificato tooyour computer locale, quindi [esportare hello certificato tooPFX](https://technet.microsoft.com/library/cc754329(v=ws.11).aspx).

### <a name="upload-your-ssl-certificate"></a>Caricare il certificato SSL

tooupload il certificato SSL, fare clic su **i certificati SSL** nel riquadro di spostamento dell'app web sinistro hello.

Fare clic su **Carica certificato**.

In **File del certificato PFX** selezionare il file PFX. In **password certificato**, digitare la password hello creato durante l'esportazione dei file PFX hello.

Fare clic su **Carica**.

![Caricamento del certificato](./media/app-service-web-tutorial-custom-ssl/upload-certificate.png)

Quando l'App completato il caricamento del certificato, viene visualizzata in hello **i certificati SSL** pagina.

![Certificato caricato](./media/app-service-web-tutorial-custom-ssl/certificate-uploaded.png)

### <a name="bind-your-ssl-certificate"></a>Associare il certificato SSL

In hello **associazioni SSL** fare clic su **aggiungere un'associazione**.

In hello **aggiungere un Binding SSL** pagina, usare hello elenchi a discesa tooselect hello dominio nome toosecure e toouse certificato hello.

> [!NOTE]
> Se è stato caricato il certificato ma non i nomi di dominio hello in hello **Hostname** elenco a discesa, provare ad aggiornare la pagina di browser hello.
>
>

In **SSL tipo**, selezionare se toouse  **[indicazione nome Server (SNI)](http://en.wikipedia.org/wiki/Server_Name_Indication)**  o basata su IP SSL.

- **SSL basato su SNI**: è possibile aggiungere più associazioni SSL basate su SNI. Questa opzione consente a più toosecure di certificati SSL più domini in hello stesso indirizzo IP. La maggior parte dei browser moderni (tra cui Internet Explorer, Chrome, Firefox e Opera) supporta SNI. Per altre informazioni sul supporto dei browser, vedere [Indicazione nome server](http://wikipedia.org/wiki/Server_Name_Indication).
- **SSL basato su IP**: è possibile aggiungere una sola associazione SSL basata su IP. Questa opzione consente un solo toosecure di certificato SSL di un indirizzo IP pubblico dedicato. toosecure più domini, è necessario proteggere tali tutti con hello stesso certificato SSL. Si tratta hello opzione tradizionale per l'associazione SSL.

Fare clic su **Aggiungi l'associazione**.

![Associare un certificato SSL](./media/app-service-web-tutorial-custom-ssl/bind-certificate.png)

Quando l'App completato il caricamento del certificato, viene visualizzata in hello **associazioni SSL** sezioni.

![Certificato associato tooweb app](./media/app-service-web-tutorial-custom-ssl/certificate-bound.png)

## <a name="remap-a-record-for-ip-ssl"></a>Eseguire nuovamente il mapping di un record A per IP SSL

Se non si utilizza SSL basato su IP nell'app web, ignorare troppo[Test HTTPS per il dominio personalizzato](#test).

Per impostazione predefinita, l'app Web usa un indirizzo IP pubblico condiviso. Quando si associa un certificato con SSL basato su IP, il servizio app crea un nuovo indirizzo IP dedicato per l'app Web.

Se è stato eseguito il mapping di un'app web di un record tooyour, aggiornare il Registro di sistema di dominio con questo indirizzo IP dedicato, nuovo.

App web **dominio personalizzato** pagina viene aggiornata con l'indirizzo IP dedicato, nuova di hello. [Copiare questo indirizzo IP](app-service-web-tutorial-custom-domain.md#info), quindi [rimappatura hello un record](app-service-web-tutorial-custom-domain.md#map-an-a-record) toothis nuovo indirizzo IP.

<a name="test"></a>

## <a name="test-https"></a>Testare HTTPS

Tutto ciò che ha lasciato toodo ora è toomake assicurarsi che HTTPS funzioni per il dominio personalizzato. In diversi browser, passare troppo`https://<your.custom.domain>` toosee che fornisca l'app web.

![Spostamento del portale tooAzure app](./media/app-service-web-tutorial-custom-ssl/app-with-custom-ssl.png)

> [!NOTE]
> Se l'app Web visualizza errori di convalida del certificato, è probabile che si stia usando un certificato autofirmato.
>
> Se non è questo caso di hello, potrebbe trovarsi i certificati intermedi quando si esporta il file PFX del certificato toohello.

<a name="bkmk_enforce"></a>

## <a name="enforce-https"></a>Applicare HTTPS

Il Servizio app *non* impone l'uso del protocollo HTTPS, pertanto gli utenti possono continuare ad accedere all'app Web usando il protocollo HTTP. tooenforce HTTPS per l'app web, definire una regola di riscrittura in hello _Web. config_ file per l'applicazione web. Servizio App utilizza questo file, indipendentemente dal framework del linguaggio hello dell'app web.

> [!NOTE]
> Il reindirizzamento delle richieste è specifico per ogni linguaggio. ASP.NET MVC è possibile utilizzare hello [RequireHttps](http://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) filtro anziché una regola di riscrittura hello in _Web. config_.

Gli sviluppatori .NET dovrebbero avere familiarità con questo file. È in una directory radice della soluzione hello.

Se invece si sviluppa con PHP, Node.js, Python o Java, è possibile che questo file sia già stato generato da Microsoft nel Servizio app.

Connettere l'endpoint FTP dell'app web tooyour seguendo le istruzioni di hello in [distribuire il servizio App utilizzando FTP/S di tooAzure app](app-service-deploy-ftp.md).

Questo file sarà disponibile in _/home/site/wwwroot_. In caso contrario, creare un _Web. config_ file in questa cartella con hello XML seguente:

```xml   
<?xml version="1.0" encoding="UTF-8"?>
<configuration>
  <system.webServer>
    <rewrite>
      <rules>
        <!-- BEGIN rule ELEMENT FOR HTTPS REDIRECT -->
        <rule name="Force HTTPS" enabled="true">
          <match url="(.*)" ignoreCase="false" />
          <conditions>
            <add input="{HTTPS}" pattern="off" />
          </conditions>
          <action type="Redirect" url="https://{HTTP_HOST}/{R:1}" appendQueryString="true" redirectType="Permanent" />
        </rule>
        <!-- END rule ELEMENT FOR HTTPS REDIRECT -->
      </rules>
    </rewrite>
  </system.webServer>
</configuration>
```

Per un oggetto esistente _Web. config_ file, copiare l'intero hello `<rule>` elemento nel _Web. config_del `configuration/system.webServer/rewrite/rules` elemento. Se sono presenti altri `<rule>` gli elementi del _Web. config_, sul posto hello copiato `<rule>` elemento prima hello altri `<rule>` elementi.

Questa regola restituisce il protocollo HTTPS toohello un HTTP 301 (reindirizzamento permanente) ogni volta che l'utente hello rende un'app di web tooyour richiesta HTTP. Ad esempio, viene reindirizzato dal `http://contoso.com` troppo`https://contoso.com`.

Per ulteriori informazioni sul modulo IIS URL Rewrite hello, vedere hello [URL Rewrite](http://www.iis.net/downloads/microsoft/url-rewrite) documentazione.

## <a name="enforce-https-for-web-apps-on-linux"></a>Imporre l'uso di HTTPS per le app Web in Linux

Poiché il servizio app in Linux *non* impone l'uso di HTTPS, gli utenti possono continuare ad accedere all'app Web usando HTTP. tooenforce HTTPS per l'app web, definire una regola di riscrittura in hello _. htaccess_ file per l'applicazione web. 

Connettere l'endpoint FTP dell'app web tooyour seguendo le istruzioni di hello in [distribuire il servizio App utilizzando FTP/S di tooAzure app](app-service-deploy-ftp.md).

In _/home/site/wwwroot_, creare un _. htaccess_ file con hello seguente codice:

```
RewriteEngine On
RewriteCond %{HTTP:X-ARR-SSL} ^$
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
```

Questa regola restituisce il protocollo HTTPS toohello un HTTP 301 (reindirizzamento permanente) ogni volta che l'utente hello rende un'app di web tooyour richiesta HTTP. Ad esempio, viene reindirizzato dal `http://contoso.com` troppo`https://contoso.com`.

## <a name="automate-with-scripts"></a>Automatizzazione con gli script

È possibile automatizzare le associazioni SSL per l'app web con gli script, utilizzando hello [CLI di Azure](/cli/azure/install-azure-cli) o [Azure PowerShell](/powershell/azure/overview).

### <a name="azure-cli"></a>Interfaccia della riga di comando di Azure

Hello comando seguente carica un file PFX esportato e ottiene l'identificazione personale hello.

```bash
thumbprint=$(az appservice web config ssl upload \
    --name <app_name> \
    --resource-group <resource_group_name> \
    --certificate-file <path_to_PFX_file> \
    --certificate-password <PFX_password> \
    --query thumbprint \
    --output tsv)
```

Hello seguente comando aggiunge un'associazione SSL basata su SNI, con identificazione personale hello dal comando precedente hello.

```bash
az appservice web config ssl bind \
    --name <app_name> \
    --resource-group <resource_group_name>
    --certificate-thumbprint $thumbprint \
    --ssl-type SNI \
```

### <a name="azure-powershell"></a>Azure PowerShell

Hello comando seguente carica un file PFX esportato e aggiunge un'associazione basata su SNI SSL.

```PowerShell
New-AzureRmWebAppSSLBinding `
    -WebAppName <app_name> `
    -ResourceGroupName <resource_group_name> `
    -Name <dns_name> `
    -CertificateFilePath <path_to_PFX_file> `
    -CertificatePassword <PFX_password> `
    -SslState SniEnabled
```

## <a name="next-steps"></a>Passaggi successivi

In questa esercitazione si è appreso come:

> [!div class="checklist"]
> * Aggiornare il piano tariffario dell'app
> * Associare il tooApp di certificato SSL del servizio personalizzato
> * Imporre HTTPS per l'app
> * Automatizzare l'associazione dei certificati SSL con gli script

Spostare toolearn esercitazione successiva toohello come toouse rete CDN di Azure.

> [!div class="nextstepaction"]
> [Aggiungere un tooan rete CDN (Content Delivery) servizio App di Azure](app-service-web-tutorial-content-delivery-network.md)
