---
title: aaaConfiguring un Firewall applicazione Web (WAF) per l'ambiente del servizio App
description: Informazioni su come un'applicazione web tooconfigure firewall davanti l'ambiente del servizio App.
services: app-service\web
documentationcenter: 
author: naziml
manager: erikre
editor: jimbe
ms.assetid: a2101291-83ba-4169-98a2-2c0ed9a65e8d
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: naziml
ms.openlocfilehash: 0fcf62aea871751c9d4f294d2d24df2186fc0e7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-a-web-application-firewall-waf-for-app-service-environment"></a>Configurazione di un Web application firewall (WAF) per l'ambiente del servizio app
## <a name="overview"></a>Panoramica
Firewall applicazione come hello Web [WAF Barracuda per Azure](https://www.barracuda.com/programs/azure) disponibile su hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/barracudanetworks/waf-byol/) consente di proteggere le applicazioni web controllando tooblock traffico web in ingresso SQL attacchi injection, Cross-Site Scripting, caricamenti di malware & applicazione DDoS e altri attacchi. Inoltre analizza le risposte hello dai server back-end web hello per la prevenzione della perdita di dati (DLP). In combinazione con l'isolamento di hello e scalabilità aggiuntive fornite per gli ambienti del servizio App, ciò offre un ambiente ideale toohost aziendali critici applicazioni che richiedono le richieste dannose toowithstand e traffico elevato.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)] 

## <a name="setup"></a>Configurazione
Per questo documento che verrà configurato l'ambiente del servizio App dietro più carico bilanciato le istanze di WAF Barracuda in modo che solo il traffico da WAF hello può raggiungere hello ambiente del servizio App e non sarà accessibile dalla rete Perimetrale hello. Si disporrà di Traffic Manager di Azure davanti il saldo di tooload Barracuda WAF istanze tra data center di Azure e le aree. Un diagramma di alto livello del programma di installazione di hello avrà un aspetto simile a quello riportato di seguito.

![Architettura][Architecture] 

> Nota: con introduzione hello di [ILB supporto per l'ambiente del servizio App](app-service-environment-with-internal-load-balancer.md), è possibile configurare toobe hello ASE accessibile dalla rete Perimetrale hello ed essere solo la rete privata toohello disponibili. 
> 
> 

## <a name="configuring-your-app-service-environment"></a>Configurazione dell'ambiente del servizio app
un ambiente del servizio App tooconfigure vedere troppo[documentazione](app-service-web-how-to-create-an-app-service-environment.md) oggetto hello. Dopo aver creato un ambiente del servizio App, è possibile creare [App Web](app-service-web-overview.md), [App per le API](../app-service-api/app-service-api-apps-why-best-platform.md) e [App per dispositivi mobili](../app-service-mobile/app-service-mobile-value-prop.md) in questo ambiente che sarà possibile proteggere dietro WAF hello è configurare la sezione successiva di hello.

## <a name="configuring-your-barracuda-waf-cloud-service"></a>Configurazione del servizio Cloud Barracuda WAF
Sul sito Barracuda è disponibile un [articolo dettagliato](https://campus.barracuda.com/product/webapplicationfirewall/article/WAF/DeployWAFInAzure) sulla distribuzione del firewall WAF in una macchina virtuale in Azure. Ma poiché si desidera la ridondanza e non introduce un singolo punto di errore, si desidera che toodeploy almeno 2 WAF istanza macchine virtuali in hello nello stesso servizio Cloud quando queste istruzioni.

### <a name="adding-endpoints-toocloud-service"></a>Aggiunta di tooCloud endpoint servizio
Dopo aver 2 o VM WAF altre istanze nel servizio Cloud, è possibile utilizzare hello [portale di Azure](https://portal.azure.com/) tooadd endpoint HTTP e HTTPS utilizzate dall'applicazione, come illustrato nell'immagine di hello riportata di seguito.

![Configurare l'endpoint][ConfigureEndpoint]

Se le applicazioni utilizzano altri endpoint, assicurarsi anche tali elenco toothis tooadd che. 

### <a name="configuring-barracuda-waf-through-its-management-portal"></a>Configurazione di Barracuda WAF tramite il relativo portale di gestione
Barracuda WAF usa la porta TCP 8000 per la configurazione tramite il proprio portale di gestione. Poiché vi sono più istanze di macchine virtuali WAF hello occorre toorepeat hello questa procedura per ogni istanza di macchina virtuale. 

> Nota: Termine con configurazione WAF, rimuovere endpoint TCP/8000 hello da tutti i tookeep di macchine virtuali WAF il WAF sicura.
> 
> 

Aggiungere hello Gestione endpoint come illustrato nell'immagine di hello sotto tooconfigure WAF il dispositivo Barracuda.

![Aggiungere l'endpoint di gestione][AddManagementEndpoint]

Utilizzare un endpoint di gestione toohello toobrowse browser sul servizio Cloud. Se il servizio Cloud viene chiamato test.cloudapp.net, è necessario accedere a questo endpoint esplorando toohttp://test.cloudapp.net:8000. Si noterà una pagina di accesso come il seguente che è possibile accedere utilizzando le credenziali specificate in fase di installazione di hello WAF VM.

![Pagina di accesso gestione][ManagementLoginPage]

Una volta accesso si dovrebbe essere visualizzato un dashboard come hello uno nell'immagine di hello seguito presenterà le statistiche di base sulla protezione WAF hello.

![Dashboard di gestione][ManagementDashboard]

Facendo clic sulla scheda Servizi hello consente di configurare il WAF per i servizi che protegge. Per altri dettagli sulla configurazione di Barracuda WAF, è possibile consultare la [relativa documentazione](https://techlib.barracuda.com/waf/getstarted1). Nell'esempio hello sotto un'App Web di Azure gestisce il traffico su HTTP e HTTPS è stata configurata.

![Aggiunta di servizi di gestione][ManagementAddServices]

> Nota: A seconda di come vengono configurate le applicazioni e le funzionalità sono usate nell'ambiente del servizio App, sarà necessario tooforward traffico per le porte TCP diverso da 80 e 443, ad esempio, se il programma di installazione di IP SSL per un'App Web. Per un elenco delle porte di rete utilizzata in ambienti di servizio App, fare riferimento troppo[documentazione di controllare il traffico in ingresso](app-service-app-service-environment-control-inbound-traffic.md) sezione porte di rete.
> 
> 

## <a name="configuring-microsoft-azure-traffic-manager-optional"></a>Configurazione di Gestione traffico di Microsoft Azure (FACOLTATIVO)
Se l'applicazione è disponibile in più aree, quindi è opportuno bilanciare tooload loro dietro [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). toodo è quindi possibile aggiungere un endpoint in hello [portale di Azure classico](https://manage.azure.com) utilizzando nome del servizio Cloud hello per le WAF nel profilo di Traffic Manager hello, come illustrato nell'immagine di hello riportata di seguito. 

![Endpoint di Gestione traffico][TrafficManagerEndpoint]

Se l'applicazione richiede l'autenticazione, assicurarsi di che disporre di alcune risorse che non richiedono alcuna autenticazione per tooping gestione traffico per la disponibilità dell'applicazione hello. È possibile configurare l'URL di hello nella sezione Configurazione hello in hello [portale di Azure classico](https://manage.azure.com) come illustrato di seguito.

![Configurare Gestione traffico][ConfigureTrafficManager]

ping di Traffic Manager tooforward hello dall'applicazione tooyour WAF, è necessario traduzioni del sito Web toosetup sull'applicazione Barracuda WAF tooforward traffico tooyour come illustrato nel seguente esempio hello.

![Website Translations][WebsiteTranslations]

## <a name="securing-traffic-tooapp-service-environment-using-network-security-groups-nsg"></a>Proteggere il traffico tooApp servizio ambiente con sicurezza gruppi (rete)
Seguire hello [documentazione di controllare il traffico in ingresso](app-service-app-service-environment-control-inbound-traffic.md) per ulteriori informazioni sulla limitazione del traffico tooyour ambiente del servizio App da hello WAF solo utilizzando l'indirizzo VIP hello del servizio Cloud. Ecco un comando di Powershell di esempio per eseguire questa attività per la porta TCP 80.

    Get-AzureNetworkSecurityGroup -Name "RestrictWestUSAppAccess" | Set-AzureNetworkSecurityRule -Name "ALLOW HTTP Barracuda" -Type Inbound -Priority 201 -Action Allow -SourceAddressPrefix '191.0.0.1'  -SourcePortRange '*' -DestinationAddressPrefix '*' -DestinationPortRange '80' -Protocol TCP

Sostituire hello SourceAddressPrefix con indirizzo di IP virtuale (VIP) del servizio Cloud del WAF hello.

> Nota: hello VIP del servizio Cloud verrà modificato se si elimina e ricrea hello servizio Cloud. Verificare che tooupdate hello indirizzo nel gruppo di risorse di rete hello dopo l'installazione. 
> 
> 

<!-- IMAGES -->
[Architecture]: ./media/app-service-app-service-environment-web-application-firewall/Architecture.png
[ConfigureEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureEndpoint.png
[AddManagementEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/AddManagementEndpoint.png
[ManagementAddServices]: ./media/app-service-app-service-environment-web-application-firewall/ManagementAddServices.png
[ManagementDashboard]: ./media/app-service-app-service-environment-web-application-firewall/ManagementDashboard.png
[ManagementLoginPage]: ./media/app-service-app-service-environment-web-application-firewall/ManagementLoginPage.png
[TrafficManagerEndpoint]: ./media/app-service-app-service-environment-web-application-firewall/TrafficManagerEndpoint.png
[ConfigureTrafficManager]: ./media/app-service-app-service-environment-web-application-firewall/ConfigureTrafficManager.png
[WebsiteTranslations]: ./media/app-service-app-service-environment-web-application-firewall/WebsiteTranslations.png
