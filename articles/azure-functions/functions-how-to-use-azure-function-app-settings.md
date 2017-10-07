---
title: le impostazioni dell'App di Azure funzione aaaConfigure | Documenti Microsoft
description: Informazioni su come tooconfigure Azure funzionare le impostazioni dell'app.
services: 
documentationcenter: .net
author: rachelappel
manager: erikre
editor: 
ms.assetid: 81eb04f8-9a27-45bb-bf24-9ab6c30d205c
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: dotnet
ms.devlang: na
ms.topic: article
ms.date: 04/23/2017
ms.author: glenga
ms.openlocfilehash: 539e203ac449061ef3ceae5e93df3bdbb326e43b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-a-function-app-in-hello-azure-portal"></a>Come un'app di funzione nel portale di Azure hello toomanage 

Nelle funzioni di Azure, un'app di funzione fornisce il contesto di esecuzione hello per le singole funzioni. I comportamenti di app di funzione applicano funzioni di tooall ospitate da un'app di funzione specificata. Questo argomento viene descritto come tooconfigure e gestire le app di funzione in hello portale di Azure.

toobegin, andare toohello [portale di Azure](http://portal.azure.com) ed eseguire l'accesso tooyour account Azure. Nella barra di ricerca hello nella parte superiore di hello del portale hello, digitare il nome di hello dell'app in funzione e selezionarlo dall'elenco di hello. Dopo aver selezionato l'app di funzione, viene visualizzato hello pagina seguente:

![Panoramica della funzione app nel portale di Azure hello](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-main.png)

## <a name="manage-app-service-settings"></a>Scheda delle impostazioni dell'app per le funzioni

![Panoramica della funzione app nel portale di Azure hello.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-settings-tab.png)

Hello **impostazioni** scheda è dove è possibile aggiornare versione del runtime funzioni hello usato dall'app (funzione). È inoltre possibile gestire hello host chiavi utilizzate toorestrict HTTP tooall funzioni di accesso ospitate da app di funzione hello.

Funzioni supporta sia i piani di hosting a consumo che i piani di hosting del servizio app. Per ulteriori informazioni, vedere [piano di servizio corretto scegliere hello per le funzioni di Azure](functions-scale.md). Per una migliore prevedibilità nel piano di consumo hello, funzioni consente di limitare l'utilizzo di piattaforma impostando una quota di utilizzo giornaliero, in secondi di gigabyte. Una volta raggiunto quota di utilizzo giornaliero hello, app di funzione hello è stato arrestato. Un'app di funzione arrestata in seguito a raggiungere hello spesa quota può essere riattivata da hello stabilire hello quotidianamente spesa quota stesso contesto. Vedere hello [funzioni Azure pagina dei prezzi](http://azure.microsoft.com/pricing/details/functions/) per i dettagli sulla fatturazione.   

## <a name="platform-features-tab"></a>Scheda delle funzionalità della piattaforma

![Scheda delle funzionalità della piattaforma per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/azure-function-app-features-tab.png)

Funzione App eseguite in e vengono mantenute, dalla piattaforma Azure App Service hello. Di conseguenza, le app di funzione hanno accesso toomost funzionalità hello di piattaforma di hosting web di base di Azure. Hello **funzionalità della piattaforma** scheda è dove è possibile accedere hello molte funzionalità della piattaforma di servizio App che è possibile utilizzare nelle app di funzione hello. 

> [!NOTE]
> Non tutte le funzionalità di servizio App sono disponibili quando si esegue un'app di funzione nel piano di hosting consumo hello.

rest Hello di questo argomento è incentrato su hello seguenti caratteristiche di servizio App in hello portale di Azure che sono utili per le funzioni:

+ [Editor del servizio app](#editor)
+ [Impostazioni dell'applicazione](#settings) 
+ [Console](#console)
+ [Strumenti avanzati (Kudu)](#kudu)
+ [Opzioni di distribuzione](#deployment)
+ [CORS](#cors)
+ [Autenticazione](#auth)
+ [Definizione dell'API](#swagger)

Per ulteriori informazioni su come toowork con le impostazioni di servizio App, vedere [configurare le impostazioni di Azure App Service](../app-service-web/web-sites-configure.md).

### <a name="editor"></a>Editor del servizio app

| | |
|-|-|
| ![Editor del servizio app per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/function-app-appsvc-editor.png)  | Hello editor di servizio App è un editor avanzato nel portale, che è possibile utilizzare i file di configurazione JSON toomodify e file di codice simili. Quando si sceglie questa opzione, viene aperta una scheda separata del browser con un editor di base. Questo consente toointegrate con codice di debug, esecuzione e repository Git hello e modificare le impostazioni dell'app di funzione. Questo editor fornisce un ambiente di sviluppo avanzato per le funzioni confrontato con pannello app di funzione predefinita hello.    |

![Hello editor di servizio App](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-appservice-editor.png)

### <a name="settings"></a>Impostazioni dell'applicazione

| | |
|-|-|
| ![Impostazioni delle applicazioni per l'app per le funzioni.](./media/functions-how-to-use-azure-function-app-settings/function-app-application-settings.png) | Servizio App Hello **le impostazioni dell'applicazione** pannello è possibile configurare e gestire le versioni di framework, il debug remoto, le impostazioni dell'app e le stringhe di connessione. Quando l'app per le funzioni si integra con altri servizi di terze parti e di Azure, qui è possibile modificare tali impostazioni. |

![Configurare le impostazioni dell'applicazione](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-settings.png)

### <a name="console"></a>Console

| | |
|-|-|
| ![Console di app di funzione in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-console.png) | console di Hello nel portale è uno strumento ideale per sviluppatori quando si preferisce toointeract con l'app di funzione dalla riga di comando hello. I comandi comuni includono la creazione e lo spostamento di file e directory, nonché l'esecuzione di script e file batch. |

![Console dell'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-console.png)

### <a name="kudu"></a>Strumenti avanzati (Kudu)

| | |
|-|-|
| ![Funzione app Kudu in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-advanced-tools.png) | Hello strumenti avanzati per il servizio App (noto anche come Kudu) forniscono accesso tooadvanced le funzionalità amministrative dell'app in funzione. Dalla Kudu è possibile gestire informazioni di sistema, impostazioni dell'app, variabili di ambiente, estensioni del sito, intestazioni HTTP e variabili del server. È anche possibile avviare **Kudu** esplorando toohello endpoint di Gestione controllo servizi per l'app di funzione, ad esempio`https://<myfunctionapp>.scm.azurewebsites.net/` |

![Configurare Kudu](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-kudu.png)


### <a name="a-namedeploymentdeployment-options"></a><a name="deployment">Opzioni di distribuzione

| | |
|-|-|
| ![Opzioni di distribuzione di app di funzione in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-deployment-source.png) | Funzioni consente di sviluppare il codice della funzione sul computer locale. È quindi possibile caricare il tooAzure di progetto app di funzione locale. Inoltre tootraditional di caricamento tramite FTP, le funzioni consentono di distribuire un'applicazione di funzione con soluzioni di integrazione continua comuni, come GitHub, Visual Studio Team Services, Dropbox, Bitbucket e altri. Per altre informazioni, vedere [Distribuzione continua per Funzioni di Azure](functions-continuous-deployment.md). tooupload manualmente tramite FTP o Git locale, è anche necessario [configurare le credenziali di distribuzione](functions-continuous-deployment.md#credentials). |


### <a name="cors"></a>CORS

| | |
|-|-|
| ![Funzione app CORS in hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-cors.png) | esecuzione di codice dannoso tooprevent nei servizi, i blocchi di servizio App chiama tooyour funzione app da origini esterne. Funzioni supporta risorse multiorigine (CORS) toolet si definisce un "elenco" di consentite le origini da cui le funzioni possono accettare richieste remote di condivisione.  |

![Configurare CORS per l'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-cors.png)

### <a name="auth"></a>Autenticazione

| | |
|-|-|
| ![Autenticazione dell'app nel portale di Azure hello (funzione)](./media/functions-how-to-use-azure-function-app-settings/function-app-authentication.png) | Quando le funzioni utilizzano un trigger HTTP, è possibile richiedere chiamate toofirst essere autenticato. Servizio app supporta l'autenticazione di Azure Active Directory e consente di accedere ai provider social, quali Facebook, Microsoft e Twitter. Per informazioni dettagliate sulla configurazione di specifici provider di autenticazione, vedere [Autenticazione e autorizzazione nel servizio app di Azure](../app-service/app-service-authentication-overview.md). |

![Configurare l'autenticazione per un'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-authentication.png)


### <a name="swagger"></a>Definizione dell'API

| | |
|-|-|
| ![Funzione app API swagger di definizione di hello portale di Azure](./media/functions-how-to-use-azure-function-app-settings/function-app-api-definition.png) | Funzioni supporta Swagger tooallow client toomore utilizzare facilmente le funzioni di attivazione HTTP. Per altre informazioni sulla creazione di definizioni API con Swagger, visitare [Introduzione alle app per le API, ad ASP.NET e a Swagger in Azure](../app-service-api/app-service-api-dotnet-get-started.md). Inoltre, è possibile utilizzare funzioni proxy toodefine una superficie API singola per più funzioni. Per altre informazioni, vedere [Uso di proxy in Funzioni di Azure](functions-proxies.md). |

![Configurare l'API per l'app per le funzioni](./media/functions-how-to-use-azure-function-app-settings/configure-function-app-apidef.png)



## <a name="next-steps"></a>Passaggi successivi

+ [Configurare le impostazioni del servizio app di Azure](../app-service-web/web-sites-configure.md)
+ [Distribuzione continua per Funzioni di Azure](functions-continuous-deployment.md)



