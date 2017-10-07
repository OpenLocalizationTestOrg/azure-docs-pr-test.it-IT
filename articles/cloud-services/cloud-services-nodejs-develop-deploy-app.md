---
title: Guida introduttiva di aaaNode.js | Documenti Microsoft
description: Informazioni su come toocreate Node.js una semplice applicazione web e distribuirla come servizio cloud di Azure tooan.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a>Compilare e distribuire un tooan applicazione Node.js servizio Cloud di Azure

Questa esercitazione viene illustrato come toocreate Node.js una semplice applicazione in esecuzione in un servizio Cloud di Azure. Servizi cloud sono blocchi predefiniti di hello delle applicazioni cloud scalabili in Azure. Consentono la separazione di hello e la gestione indipendente e scalabilità orizzontale di componenti front-end e back-end dell'applicazione.  Servizi cloud offre una potente macchina virtuale dedicata per ospitare ogni ruolo in modo affidabile.

Per ulteriori informazioni sui servizi Cloud e le modalità di confronto tooAzure siti Web e macchine virtuali, vedere [confronto siti Web di Azure, servizi Cloud e macchine virtuali].

> [!TIP]
> Ricerca toobuild un semplice sito Web? Se lo scenario prevede un semplice sito Web front-end, è possibile [usare un'app Web leggera]. Come si espande l'app web e i requisiti cambiano, è possibile aggiornare facilmente tooa servizio Cloud.

Questa esercitazione consente di creare una semplice applicazione Web ospitata in un ruolo Web. Verrà usare tootest emulatore di calcolo hello l'applicazione localmente, quindi distribuirlo utilizzando gli strumenti da riga di comando di PowerShell.

un'applicazione Hello è una semplice applicazione "hello world":

![Un web browser visualizzazione pagina web di Hello World hello][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a>Prerequisiti
> [!NOTE]
> Questa esercitazione usa Azure PowerShell, che richiede Windows.

* Installare e configurare [Azure PowerShell].
* Scaricare e installare hello [Azure SDK per .NET 2.7]. In hello installare il programma di installazione, selezionare:
  * MicrosoftAzureAuthoringTools
  * MicrosoftAzureComputeEmulator

## <a name="create-an-azure-cloud-service-project"></a>Creare un progetto di Servizi cloud di Azure
Eseguire hello seguenti attività toocreate un nuovo progetto di servizio Cloud di Azure, insieme a base scaffolding Node.js:

1. Eseguire **Windows PowerShell** come amministratore, da hello **Menu Start** o **schermata Start**, cercare **Windows PowerShell**.
2. [La connessione PowerShell] tooyour sottoscrizione.
3. Immettere hello progetto di hello toocreate toocreate cmdlet PowerShell seguente:

        New-AzureServiceProject helloworld

    ![risultato di Hello del comando helloworld hello New-AzureService][hello result of hello New-AzureService helloworld command]

    Hello **New AzureServiceProject** cmdlet genera una struttura di base per la pubblicazione di un tooa applicazione Node.js servizio Cloud. Contiene i file di configurazione necessari per la pubblicazione tooAzure. cmdlet di Hello cambia anche directory toohello di directory di lavoro per il servizio di hello.

    cmdlet di Hello crea hello i seguenti file:

   * **ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** e **ServiceDefinition.csdef** sono file specifici di Azure, necessari per la pubblicazione dell'applicazione. Per altre informazioni, vedere [Creazione di un servizio ospitato per Azure].
   * **Deploymentsettings**: archivia le impostazioni locali utilizzate da hello i cmdlet di distribuzione di Azure PowerShell.
4. Immettere hello successivo comando tooadd un nuovo ruolo web:

       Add-AzureNodeWebRole

   ![output di Hello del comando Add-AzureNodeWebRole hello][hello output of hello Add-AzureNodeWebRole command]

   Hello **Add-AzureNodeWebRole** cmdlet crea un'applicazione Node.js di base. Viene inoltre modificata hello **con estensione csfg** e **csdef** tooadd voci di configurazione per il nuovo ruolo di hello dei file.

   > [!NOTE]
   > Se non si specifica un nome di ruolo, viene usato un nome predefinito. È possibile fornire un nome come primo parametro del cmdlet hello:`Add-AzureNodeWebRole MyRole`

app Node.js Hello è definito nel file hello **server.js**, che si trova nella directory di hello per ruolo web hello (**WebRole1** per impostazione predefinita). Ecco il codice hello:

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

Questo codice è essenzialmente hello stesso hello "Hello World" di esempio in hello [nodejs.org] sito Web, ad eccezione del fatto che utilizza il numero di porta hello assegnato dall'ambiente cloud hello.

## <a name="deploy-hello-application-tooazure"></a>Distribuire tooAzure applicazione hello

> [!NOTE]
> toocomplete questa esercitazione, è necessario un account di Azure. È possibile [attivare i benefici della sottoscrizione MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) o [iscriversi per un account gratuito](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="download-hello-azure-publishing-settings"></a>Scaricare hello Azure impostazioni di pubblicazione
toodeploy tooAzure l'applicazione, è necessario prima scaricare hello pubblicazione le impostazioni per la sottoscrizione di Azure.

1. Eseguire hello cmdlet di Azure PowerShell seguente:

       Get-AzurePublishSettingsFile

   Verrà utilizzato il browser toonavigate toohello pagina di download delle impostazioni di pubblicazione. Potrebbe essere richiesta toolog con un Account Microsoft. In questo caso, utilizzare account hello associati alla sottoscrizione di Azure.

   Percorso file di hello scaricato profilo tooa consentono di accedere facilmente di salvataggio.
2. Eseguire riportata di seguito cmdlet tooimport hello scaricato profilo di pubblicazione:

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > Dopo l'importazione di hello le impostazioni di pubblicazione, provare a eliminare hello scaricato il file con estensione publishsettings, perché contiene informazioni che possono consentire a un utente tooaccess l'account.

### <a name="publish-hello-application"></a>Pubblicare un'applicazione hello
toopublish, eseguire hello seguenti comandi:

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* **-ServiceName** specifica hello nome per la distribuzione di hello. Deve essere un nome univoco, in caso contrario hello pubblicare processo avrà esito negativo. Hello **Get-Date** comando puntine su una stringa di data/ora che è necessario rendere univoca con nome hello.
* **-Location** specifica datacenter hello che verrà ospitata in un'applicazione hello. un elenco dei centri dati disponibili, utilizzare hello toosee **Get AzureLocation** cmdlet.
* **-Avviare** apre una finestra del browser e passa il servizio ospitato toohello dopo la distribuzione è stata completata.

Dopo la pubblicazione riesce, verrà visualizzato di seguito toohello simile risposta:

![output di Hello di hello comando Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> Può richiedere alcuni minuti per toodeploy applicazione hello e diventano disponibile durante la pubblicazione iniziale.

Una volta completata la distribuzione di hello, una finestra del browser verrà aperto e passare servizio cloud toohello.

![Una finestra del browser pagina hello hello world; URL di Hello indica pagina hello è ospitato in Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

L'applicazione è in esecuzione su Azure.

Hello **pubblica AzureServiceProject** cmdlet esegue hello alla procedura seguente:

1. Crea un pacchetto toodeploy. pacchetto di Hello contiene tutti i file hello nella cartella dell'applicazione.
2. Crea un nuovo **account di archiviazione** nel caso non ne esista uno. Hello account di archiviazione di Azure è pacchetto dell'applicazione hello toostore utilizzato durante la distribuzione. È possibile eliminare l'account di archiviazione di hello in modo sicuro al termine dell'operazione di distribuzione.
3. Crea un nuovo **servizio cloud** nel caso in cui non ne esista già uno. Oggetto **servizio cloud** hello contenitore in cui è ospitata l'applicazione quando è tooAzure distribuito. Per altre informazioni, vedere [Creazione di un servizio ospitato per Azure].
4. Pubblica tooAzure pacchetto di distribuzione hello.

## <a name="stopping-and-deleting-your-application"></a>Arrestare ed eliminare l'applicazione
Dopo aver distribuito l'applicazione, è opportuno toodisable in modo è possibile evitare i costi aggiuntivi. Azure addebita le istanze del ruolo Web al consumo, in base all'utilizzo di tempo del server su base oraria. Ora del server viene utilizzata una volta distribuita l'applicazione, anche se le istanze di hello non sono in esecuzione e sono in stato arrestato hello.

1. Nella finestra di Windows PowerShell hello, arrestare la distribuzione del servizio hello creata nella sezione precedente di hello con hello seguente cmdlet:

       Stop-AzureService

   L'arresto del servizio hello potrebbe richiedere alcuni minuti. Quando il servizio hello viene arrestato, viene visualizzato un messaggio che indica che è stato arrestato.

   ![stato di Hello del comando Stop-AzureService hello][hello status of hello Stop-AzureService command]
2. servizio di hello toodelete, hello chiamata seguente cmdlet:

       Remove-AzureService

   Quando richiesto, immettere **Y** servizio hello toodelete.

   Eliminazione del servizio hello potrebbe richiedere alcuni minuti. Dopo aver eliminato il servizio hello viene visualizzato un messaggio che indica che il servizio di hello è stato eliminato.

   ![stato di Hello del comando Remove-AzureService hello][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > Eliminazione del servizio di hello non comporta l'eliminazione account di archiviazione hello creato quando il servizio di hello inizialmente è stato pubblicato e si continuerà toobe fatturato per l'archiviazione utilizzata. Se nessun altro elemento utilizza archiviazione hello, è opportuno toodelete è.

## <a name="next-steps"></a>Passaggi successivi
Per ulteriori informazioni, vedere hello [Centro per sviluppatori di Node.js].

<!-- URL List -->

[confronto siti Web di Azure, servizi Cloud e macchine virtuali]: ../app-service-web/choose-web-site-cloud-service-vm.md
[usare un'app Web leggera]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Azure SDK per .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[La connessione PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Creazione di un servizio ospitato per Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Centro per sviluppatori di Node.js]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
