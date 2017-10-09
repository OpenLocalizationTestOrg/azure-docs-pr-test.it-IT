---
title: aaaDeployment domande frequenti per App web di Azure | Documenti Microsoft
description: "Ottenere risposte toofrequently domande frequenti sulla distribuzione per funzionalità di App Web hello di servizio App di Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 566e1d7028e678f9679200f436118d27dfb07079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deployment-faqs-for-web-apps-in-azure"></a>Domande frequenti sulla distribuzione per app Web in Azure

In questo articolo ha toofrequently risposte domande frequenti (FAQ) sui problemi di distribuzione per hello [funzionalità App Web di Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="i-am-just-getting-started-with-app-service-web-apps-how-do-i-publish-my-code"></a>Quando si iniziano a usare le app Web del servizio app, come si pubblica il codice?

Di seguito sono riportate alcune opzioni per la pubblicazione del codice dell'app Web:

*   Eseguire la distribuzione usando Visual Studio. Se si dispone di soluzione di Visual Studio hello, il progetto di applicazione web hello e quindi scegliere **pubblica**.
*   Eseguire la distribuzione usando un client FTP. Nel portale di Azure hello, hello download profilo per l'app web hello di pubblicazione che si desidera toodeploy il codice. Caricare quindi too\site\wwwroot file hello utilizzando hello stesso pubblicare le credenziali del profilo FTP.

Per ulteriori informazioni, vedere [distribuire il servizio di tooApp app](web-sites-deploy.md).

## <a name="i-see-an-error-message-when-i-try-toodeploy-from-visual-studio-how-do-i-resolve-this"></a>Quando cerca di toodeploy da Visual Studio, viene visualizzato un messaggio di errore. Come posso risolvere il problema?

Se si segue messaggio hello, si potrebbe utilizzando una versione precedente di hello SDK: "Errore durante la distribuzione per la risorsa 'YourResourceName' nel gruppo di risorse 'YourResourceGroup': MissingRegistrationForLocation: sottoscrizione hello non è registrata per Hello tipo di risorsa 'componenti' percorso hello "Central US". Ripetere la registrazione per questo provider nel percorso di ordine toohave accesso toothis." 

tooresolve questo errore, l'aggiornamento toohello [SDK più recente](https://azure.microsoft.com/downloads/). Se viene visualizzato questo messaggio e si dispone di hello SDK più recente, inviare una richiesta di supporto.

## <a name="how-do-i-deploy-an-aspnet-application-from-visual-studio-tooapp-service"></a>Come distribuire un'applicazione ASP.NET da Visual Studio tooApp servizio?
<a id="deployasp"></a>

esercitazione Hello [creare la prima app web ASP.NET in Azure in cinque minuti](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-get-started/) viene illustrato come toodeploy ASP.NET web applicazione tooa web app nel servizio App con Visual Studio 2015.

## <a name="what-are-hello-different-types-of-deployment-credentials"></a>Quali sono hello diversi tipi di credenziali di distribuzione?

Il servizio app supporta due tipi di credenziali per la distribuzione Git locale e la distribuzione FTP/S. Per ulteriori informazioni su come tooconfigure le credenziali di distribuzione, vedere [configurare le credenziali di distribuzione per il servizio App](app-service-deployment-credentials.md).

## <a name="what-is-hello-file-or-directory-structure-of-my-app-service-web-app"></a>Che cos'è una struttura di file o directory hello della mia app web di servizio App?

Per informazioni sulla struttura di file hello della propria applicazione di servizio App, vedere [struttura di File in Azure](https://github.com/projectkudu/kudu/wiki/File-structure-on-azure).

## <a name="how-do-i-resolve-ftp-error-550---there-is-not-enough-space-on-hello-disk-when-i-try-tooftp-my-files"></a>Come risolvere "Errore di FTP 550 - non è sufficiente spazio su disco hello" quando si tenta tooFTP file?

Se viene visualizzato questo messaggio, è probabile che siano in esecuzione in una quota del disco nel piano di servizio hello per le app web. Potrebbe essere necessario tooscale backup tooa livello di servizio superiore in base alle proprie esigenze di spazio su disco. Per altre informazioni sui piani tariffari e i limiti delle risorse, vedere il [piano tariffario del servizio app](https://azure.microsoft.com/pricing/details/app-service/).

## <a name="how-do-i-set-up-continuous-deployment-for-my-app-service-web-app"></a>Come si configura la distribuzione continua dell'app Web del servizio app?

È possibile impostare la distribuzione continua da diverse risorse, tra cui Visual Studio Team Services, OneDrive, GitHub, Bitbucket, Dropbox e altri repository Git. Queste opzioni sono disponibili nel portale di hello. [La distribuzione continua tooApp servizio](app-service-continuous-deployment.md) è un'utile esercitazione che illustra come tooset la distribuzione continua.

## <a name="how-do-i-troubleshoot-issues-with-continuous-deployment-from-github-and-bitbucket"></a>Come si risolvono i problemi con la distribuzione continua da GitHub e Bitbucket?

Per informazioni sull'analisi dei problemi con la distribuzione continua da GitHub o Bitbucket, vedere [Investigating continuous deployment](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment) (Analisi della distribuzione continua).

## <a name="i-cant-ftp-toomy-site-and-publish-my-code-how-do-i-resolve-this"></a>Impossibile toomy sito FTP e pubblicare il codice utente. Come posso risolvere il problema?

problemi di tooresolve FTP:

1. Verificare che si immettono le credenziali e il nome host corretto hello. Per informazioni dettagliate sui diversi tipi di credenziali e toouse, vedere [le credenziali di distribuzione](https://github.com/projectkudu/kudu/wiki/Deployment-credentials).
2. Verificare che le porte FTP hello non sono bloccate da un firewall. porte Hello devono avere le seguenti impostazioni:
    * Porta di connessione di controllo FTP: 21
    * Porta di connessione dati FTP: 989, 10001-10300

## <a name="how-do-i-publish-my-code-tooapp-service"></a>Come pubblicare il servizio di tooApp di codice

Guida introduttiva di Azure Hello è progettato toohelp si distribuisce l'app tramite stack distribuzione hello e metodo di propria scelta. Ciao toouse Guide rapide, hello portale di Azure andare troppo**impostazioni** > **della distribuzione di applicazioni**.

## <a name="why-does-my-app-sometimes-restart-after-deployment-tooapp-service"></a>Perché mia app talvolta e riavviare tooApp distribuzione servizio?

toolearn sulle circostanze hello in cui una distribuzione dell'applicazione potrebbe comportare un riavvio, vedere [distribuzione e problemi di runtime](https://github.com/projectkudu/kudu/wiki/Deployment-vs-runtime-issues#deployments-and-web-app-restarts"). Come descritto nella sezione articolo hello, servizio App distribuisce cartella wwwroot toohello. Non riavvia mai direttamente l'app.

## <a name="how-do-i-integrate-visual-studio-team-services-code-with-app-service"></a>Come si integra il codice di Visual Studio Team Services con il servizio app?

Sono disponibili due opzioni per l'uso della distribuzione continua con Visual Studio Team Services:

*   Usare un progetto Git. Utilizzando le opzioni di distribuzione hello per repository si connettono tramite servizio App.
*   Usare un progetto di controllo della versione di Team Foundation. Distribuzione tramite l'agente di compilazione hello per servizio App.

La distribuzione continua di codice per entrambe le opzioni dipende dai flussi di lavoro di sviluppo esistenti e dalle procedure di archiviazione. Per altre informazioni, vedere questi articoli: 

*   [Implementare la distribuzione continua del tooan app sito Web di Azure](https://www.visualstudio.com/docs/release/examples/azure/azure-web-apps-from-build-and-release-hubs)
*   [Configurare un account di Visual Studio Team Services in modo è possibile distribuire l'app web tooa](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App)

## <a name="how-do-i-use-ftp-or-ftps-toodeploy-my-app-tooapp-service"></a>Come si utilizza FTP o FTPS toodeploy my tooApp app servizio?

Per informazioni sull'utilizzo di FTP o FTPS toodeploy il tooApp app web del servizio, vedere [distribuire il servizio di tooApp app tramite FTP/S](app-service-deploy-ftp.md).
