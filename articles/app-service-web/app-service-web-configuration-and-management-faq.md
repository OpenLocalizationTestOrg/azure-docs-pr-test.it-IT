---
title: aaaConfiguration domande frequenti per App web di Azure | Documenti Microsoft
description: "Ottenere risposte toofrequently domande frequenti sui problemi di gestione e configurazione per la funzionalità di App Web hello di servizio App di Azure."
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
ms.openlocfilehash: 5aa405582813291a4aaf144d2f821ecb20a5edcb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configuration-and-management-faqs-for-web-apps-in-azure"></a>Domande frequenti sulla configurazione e sulla gestione per App Web di Azure

In questo articolo ha toofrequently risposte domande frequenti (FAQ) sui problemi di configurazione e gestione per hello [funzionalità App Web di Azure App Service](https://azure.microsoft.com/services/app-service/web/).

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="are-there-limitations-i-should-be-aware-of-if-i-want-toomove-app-service-resources"></a>Esistono limitazioni, che consigliabile tenere in considerazione se desidero che le risorse del servizio App toomove?

Se si intende toomove servizio App risorse tooa nuovo gruppo di risorse o di sottoscrizione, esistono alcune limitazioni toobe conoscere. Per altre informazioni, vedere [Limitazioni del servizio app](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="how-do-i-use-a-custom-domain-name-for-my-web-app"></a>Come si utilizza un nome di dominio personalizzato per un'app Web?

Per le risposte toocommon domande sull'utilizzo di un nome di dominio personalizzato con l'app web di Azure, vedere il video di sette minuti [aggiungere un nome di dominio personalizzato](https://channel9.msdn.com/blogs/Azure-App-Service-Self-Help/Add-a-Custom-Domain-Name). Hello video offre una procedura dettagliata relativa tooadd un nome di dominio personalizzato. Viene descritto come toouse il proprio URL anziché hello *. azurewebsites.net URL con l'applicazione di servizio App web. È inoltre possibile visualizzare una descrizione dettagliata di [come nome di dominio personalizzato toomap](web-sites-custom-domain-name.md).


## <a name="how-do-i-purchase-a-new-custom-domain-for-my-web-app"></a>Come si acquista un nuovo dominio personalizzato per un'app Web?

toolearn toopurchase e configurare un dominio personalizzato per l'app web di servizio App, vedere [acquistare e configurare un nome di dominio personalizzato nel servizio App](custom-dns-web-site-buydomains-web-app.md).


## <a name="how-do-i-upload-and-configure-an-existing-ssl-certificate-for-my-web-app"></a>Come si carica e si configura un certificato SSL esistente per un'app Web?

toolearn tooupload e configurare un certificato SSL personalizzato esistente, vedere [associare un' personalizzato SSL certificato tooan Azure web app esistente](app-service-web-tutorial-custom-ssl.md#upload).


## <a name="how-do-i-purchase-and-configure-a-new-ssl-certificate-in-azure-for-my-web-app"></a>Come si acquista e si configura un nuovo certificato SSL certificate in Azure per un'app Web?

toolearn toopurchase e configurare un certificato SSL per l'app web di servizio App, vedere [aggiungere un tooyour certificato SSL del servizio App app](web-sites-purchase-ssl-web-site.md).


## <a name="how-do-i-move-application-insights-resources"></a>Come si spostano le risorse di Application Insights?

Attualmente, Azure Application Insights non supporta l'operazione di spostamento hello. Se il gruppo di risorse originale include una risorsa di Application Insights, non è possibile spostare tale risorsa. Se si include la risorsa di Application Insights hello quando si tenta di un'applicazione di servizio App toomove, hello intera spostare l'operazione ha esito negativo. Tuttavia, Application Insights e servizio App di piano non è necessario toobe in hello hello correttamente app hello per hello app toofunction stesso gruppo di risorse.

Per altre informazioni, vedere [Limitazioni del servizio app](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations).

## <a name="where-can-i-find-a-guidance-checklist-and-learn-more-about-resource-move-operations"></a>Dove è possibile trovare un elenco di controllo del materiale sussidiario e altre informazioni sulle operazioni di spostamento delle risorse?

[Limitazioni del servizio app](../azure-resource-manager/resource-group-move-resources.md#app-service-limitations) viene illustrato come toomove risorse tooeither una nuova sottoscrizione o tooa nuova risorsa gruppo hello stessa sottoscrizione. È possibile ottenere informazioni sull'elenco di controllo spostamento risorse hello, informazioni su servizi che supportano l'operazione di spostamento hello e altre informazioni sulle limitazioni del servizio App e altri argomenti.

## <a name="how-do-i-set-hello-server-time-zone-for-my-web-app"></a>Configurazione di hello fuso orario del server per l'applicazione web

tooset hello server fuso orario per l'app web:

1. Nel portale di Azure nella sottoscrizione al servizio App hello passare toohello **le impostazioni dell'applicazione** menu.
2. In **Impostazioni app**, aggiungere questa impostazione:
    * Key = WEBSITE_TIME_ZONE
    * Valore = *hello fuso orario desiderato*
3. Selezionare **Salva**.

## <a name="why-do-my-continuous-webjobs-sometimes-fail"></a>Perché i processi Web continui talvolta hanno esito negativo?

Per impostazione predefinita, le app Web vengono scaricate se restano inattive per un determinato periodo di tempo. Ciò consente di risparmiare risorse di sistema hello. Nei piani Basic e Standard, è possibile attivare hello **Always On** impostazione tookeep hello web app caricato tutto il tempo hello. Se l'app web è in esecuzione processi Web continui, è necessario attivare **Always On**, o hello processi Web potrebbe non essere eseguito in modo affidabile. Per altre informazioni, vedere [Creare un processo Web con esecuzione continua](web-sites-create-web-jobs.md#CreateContinuous).

## <a name="how-do-i-get-hello-outbound-ip-address-for-my-web-app"></a>Come ottenere l'indirizzo IP hello in uscita per la mia applicazione web

elenco di hello tooget di indirizzi IP in uscita per l'app web:

1. Nel portale di Azure, nel pannello app web, hello passare toohello **proprietà** menu.
2. Cercare **indirizzi ip in uscita**.

viene visualizzato l'elenco di Hello di indirizzi IP in uscita.

Se il sito Web è ospitato nell'ambiente del servizio App per PowerApps, toolearn come tooget l'indirizzo IP in uscita, vedere [gli indirizzi di rete in uscita](app-service-app-service-environment-network-architecture-overview.md#outbound-network-addresses).

## <a name="how-do-i-get-a-reserved-or-dedicated-inbound-ip-address-for-my-web-app"></a>Come si ottiene un indirizzo IP in ingresso dedicato o riservato per un'app Web?

tooset di un indirizzo IP dedicato o riservato per le chiamate in ingresso tooyour sito Web di app di Azure, installare e configurare un certificato SSL basato su IP.

Si noti che una dedicata toouse o indirizzo IP riservato per le chiamate in ingresso, il piano di servizio App deve essere in un piano di servizio di base o versione successiva.

## <a name="can-i-export-my-app-service-certificate-toouse-outside-azure-such-as-for-a-website-hosted-elsewhere"></a>È possibile esportare il toouse del certificato di servizio App all'esterno di Azure, ad esempio per un sito Web ospitato in un' posizione? 

I certificati del servizio app sono considerati risorse di Azure. Non sono previsti toouse all'esterno di servizi di Azure. È possibile esportarli toouse all'esterno di Azure. Per altre informazioni, vedere [Domande frequenti per i certificati del servizio app e i domini personalizzati](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).

## <a name="can-i-export-my-app-service-certificate-toouse-with-other-azure-cloud-services"></a>È possibile esportare il toouse del certificato di servizio App con altri servizi cloud di Azure?

portale Hello offre un'esperienza di primaria importanza per la distribuzione di un certificato di servizio App tramite applicazioni di servizio tooApp insieme credenziali chiavi Azure. Tuttavia, è stato ricevuto le richieste dai clienti toouse questi certificati all'esterno di hello piattaforma del servizio App, ad esempio, con macchine virtuali di Azure. toolearn come certificato di toocreate una copia locale PFX del servizio App è possibile utilizzare il certificato di hello con altre risorse di Azure, vedere [creare una copia di file PFX locale di un certificato di servizio App](https://blogs.msdn.microsoft.com/appserviceteam/2017/02/24/creating-a-local-pfx-copy-of-app-service-certificate/).

Per altre informazioni, vedere [Domande frequenti per i certificati del servizio app e i domini personalizzati](https://social.msdn.microsoft.com/Forums/azure/f3e6faeb-5ed4-435a-adaa-987d5db43b80/faq-on-app-service-certificates-and-custom-domains?forum=windowsazurewebsitespreview).


## <a name="why-do-i-see-hello-message-partially-succeeded-when-i-try-tooback-up-my-web-app"></a>Perché viene visualizzato il messaggio hello "Parzialmente riuscita" quando si tenta di tooback backup dell'app web?

Una causa comune di errori di backup è che alcuni file sono in uso da un'applicazione hello. File in uso vengono bloccati durante l'esecuzione di backup hello. Ciò impedisce che ne venga eseguito il backup ed è possibile che venga visualizzato lo stato "Parzialmente completato". È potenzialmente possibile impedire questo accada escludendo i file del processo di backup hello. È possibile scegliere tooback backup solo quelli necessari. Per ulteriori informazioni, vedere [appena hello parti importanti del sito con App web di Azure Backup](http://www.zainrizvi.io/2015/06/05/creating-partial-backups-of-your-site-with-azure-web-apps/).

## <a name="how-do-i-remove-a-header-from-hello-http-response"></a>Come rimuovere un'intestazione di risposta HTTP hello?

aggiornamento delle intestazioni di hello tooremove da hello risposta HTTP, file Web. config del sito. Per altre informazioni, vedere [Rimuovere intestazioni del server standard nei siti Web di Azure](https://azure.microsoft.com/blog/removing-standard-server-headers-on-windows-azure-web-sites/).

## <a name="is-app-service-compliant-with-pci-standard-30-and-31"></a>Il servizio app è conforme con lo standard PCI 3.0 e 3.1?

Funzionalità di App Web hello di servizio App di Azure è attualmente in conformità con la versione PCI Data Security Standard (DSS) 3.0 livello 1. La versione 3.1 di PCI DSS fa parte del piano d'azione. La pianificazione è già in corso per la modalità in cui verrà eseguita adozione di standard più recente di hello.

Il certificato PCI DSS versione 3.1 richiede la disabilitazione di Transport Layer Security (TLS) 1.0. Attualmente, la disabilitazione di TLS 1.0 non è un'opzione per la maggior parte dei piani del servizio app. Tuttavia, se si utilizza l'ambiente del servizio App o si sono disposti toomigrate il tooApp del carico di lavoro dell'ambiente del servizio, è possibile ottenere maggiore controllo del proprio ambiente. A tal fine, occorre disabilitare TLS 1.0 contattando il supporto tecnico di Azure. In hello prossimo futuro, contiamo toomake toousers di accessibili queste impostazioni.

Per altre informazioni, vedere [Conformità dell'app web del servizio app di Microsoft Azure con lo standard PCI 3.0 e 3.1](https://support.microsoft.com/help/3124528).

## <a name="how-do-i-use-hello-staging-environment-and-deployment-slots"></a>Utilizzo di hello ambiente e gli slot di distribuzione di gestione temporanea

Nei piani Standard e di servizio App Premium, quando si distribuisce il tooApp app web del servizio, è possibile distribuire uno slot di distribuzione separata tooa anziché toohello slot di produzione predefinito. Gli slot di distribuzione sono App Web live con i propri nomi host. Elementi di contenuto e la configurazione di app Web possono essere scambiati tra i due slot di distribuzione, compreso hello slot di produzione.

Per altre informazioni sull'utilizzo degli slot di distribuzione, vedere [Configurare un ambiente di gestione temporanea nel servizio app](web-sites-staged-publishing.md).

## <a name="how-do-i-access-and-review-webjob-logs"></a>Come si accede e come si esaminano i log dei processi Web?

tooreview registra processo Web:

1. Accedi tooyour [sito Web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).
2. Selezionare hello processo Web.
3. Seleziona hello **attiva/disattiva Output** pulsante.
4. file di output di hello toodownload, seleziona hello **scaricare** collegamento.
5. Per le singole esecuzioni, selezionare **Singolo richiamo**.
6. Seleziona hello **attiva/disattiva Output** pulsante.
7. Collegamento di download selezionare hello.

## <a name="im-trying-toouse-hybrid-connections-with-sql-server-why-do-i-see-hello-message-systemoverflowexception-arithmetic-operation-resulted-in-an-overflow"></a>Si sta tentando di connessioni ibride toouse con SQL Server. Perché viene visualizzato il messaggio hello "System. OverflowException: operazione aritmetica ha causato un overflow"?

Se si utilizzano le connessioni ibride tooaccess SQL Server, un aggiornamento di Microsoft .NET 10 maggio 2016, potrebbe toofail connessioni. È possibile che venga visualizzato questo messaggio:

```
Exception: System.Data.Entity.Core.EntityException: hello underlying provider failed on Open. —> System.OverflowException: Arithmetic operation resulted in an overflow. or (64 bit Web app) System.OverflowException: Array dimensions exceeded supported range, at System.Data.SqlClient.TdsParser.ConsumePreLoginHandshake
```

### <a name="resolution"></a>Risoluzione

Stiamo lavorando tooupdate toofix Hybrid Connection Manager questo problema. Per soluzioni alternative, vedere [Errore di Connessioni ibride con SQL Server: System.OverflowException: Overflow di un'operazione aritmetica](https://blogs.msdn.microsoft.com/waws/2016/05/17/hybrid-connection-error-with-sql-server-system-overflowexception-arithmetic-operation-resulted-in-an-overflow/).

## <a name="how-do-i-add-or-edit-a-url-rewrite-rule"></a>Come si aggiunge o si modifica una regola di riscrittura di URL?

tooadd o modifica una regola di riscrittura URL:

1. Configurare Gestione Internet Information Services (IIS) in modo che si connette tooyour App del servizio web app. toolearn tooconnect servizio tooApp Gestione IIS, vedere [amministrazione remota di siti Web di Azure tramite Gestione IIS](https://azure.microsoft.com/blog/remote-administration-of-windows-azure-websites-using-iis-manager/).
2. In Gestione IIS, aggiungere o modificare una regola di riscrittura di URL. toolearn come tooadd o modificare un URL rewrite regola, vedere [crea regole di riscrittura URL hello riscrivere modulo](https://www.iis.net/learn/extensions/url-rewrite-module/creating-rewrite-rules-for-the-url-rewrite-module).

## <a name="how-do-i-control-inbound-traffic-tooapp-service"></a>Come controllare il traffico in entrata tooApp servizio?

A livello di sito hello, sono disponibili due opzioni per controllare il traffico in entrata tooApp servizio:

* Attivare le restrizioni di IP dinamico. toolearn tooturn su restrizioni IP dinamici, vedere [restrizioni IP e di dominio per siti Web di Azure](https://azure.microsoft.com/blog/ip-and-domain-restrictions-for-windows-azure-web-sites/).
* Attivare la protezione di modulo. toolearn tooturn nel modulo di protezione, vedere [ModSecurity firewall di applicazione web in siti Web di Azure](https://azure.microsoft.com/blog/modsecurity-for-azure-websites/).

Se si utilizza l'ambiente del servizio app, è possibile utilizzare il [firewall Barracuda](https://azure.microsoft.com/blog/configuring-barracuda-web-application-firewall-for-azure-app-service-environment/).

## <a name="how-do-i-block-ports-in-an-app-service-web-app"></a>Come è possibile bloccare le porte in un'app Web del servizio Web?

In hello servizio App condiviso ambiente tenant, non è possibile tooblock specifiche porte a causa di natura hello dell'infrastruttura di hello. Inoltre, le porte TCP 4016, 4018 e 4020 potrebbero essere aperte per il debug remoto di Visual Studio.

Nell'ambiente del servizio app, si ha il controllo totale sul traffico in ingresso e in uscita. È possibile utilizzare gruppi di sicurezza di rete toorestrict o blocco porte specifiche. Per altre informazioni sull'ambiente del servizio app, vedere [Introduzione all'ambiente del servizio app](https://azure.microsoft.com/blog/introducing-app-service-environment/).

## <a name="how-do-i-capture-an-f12-trace"></a>Come si acquisisce una traccia F12?

È possibile acquisire una traccia F12 in due modi:

* Traccia HTTP F12
* Output di console F12

### <a name="f12-http-trace"></a>Traccia HTTP F12

1. In Internet Explorer, passare il sito Web tooyour. È importante toosign prima si hello passaggi successivi. In caso contrario, hello F12 traccia acquisisce i dati sensibili Accedi.
2. Premere F12.
3. Verificare che hello **rete** scheda sia selezionata e quindi selezionare hello verde **riprodurre** pulsante.
4. Hello passaggi per riprodurre il problema di hello.
5. Seleziona hello rosso **arrestare** pulsante.
6. Seleziona hello **salvare** pulsante (icona del disco) e salvare file HAR hello (in Internet Explorer e bordo) *o* file HAR hello e quindi scegliere **Salva come HAR con contenuto** ( in Chrome).

### <a name="f12-console-output"></a>Output di console F12

1. Seleziona hello **Console** scheda.
2. Per ogni scheda che contiene più di zero elementi, selezionare la scheda hello (**errore**, **avviso**, o **informazioni**). Se non è selezionata la scheda hello, l'icona della scheda hello è grigio o in nero quando allontanando il cursore di hello.
3. Nell'area dei messaggi hello del riquadro hello e quindi scegliere **copiare tutti**.
4. Ciao Incolla il testo copiato in un file e quindi salvare il file hello.

un file HAR tooview, è possibile utilizzare hello [Visualizzatore HAR](http://www.softwareishard.com/har/viewer/).

## <a name="why-do-i-get-an-error-when-i-try-tooconnect-an-app-service-web-app-tooa-virtual-network-that-is-connected-tooexpressroute"></a>Perché viene visualizzato un errore quando si tenta di tooconnect un servizio App web app tooa rete virtuale connessa tooExpressRoute?

Se si tenta una Azure web app tooa rete virtuale connessa tooAzure ExpressRoute tooconnect, l'esito negativo. Hello seguente messaggio: "Gateway non è un gateway VPN".

Attualmente, è possibile avere point-to-site VPN connessioni tooa rete virtuale connessa tooExpressRoute. Una VPN point-to-site ed ExpressRoute non può coesistere per hello stessa rete virtuale. Per altre informazioni, vedere [Limiti e limitazioni delle connessioni ExpressRoute e VPN da sito a sito](../expressroute/expressroute-howto-coexist-classic.md#limits-and-limitations).

## <a name="how-do-i-connect-an-app-service-web-app-tooa-virtual-network-that-has-a-static-routing-policy-based-gateway"></a>Come si connette una servizio App web app tooa rete virtuale con un gateway (basata su criteri) con routing statico?

Attualmente, non è supportata la connessione a una servizio App web app tooa rete virtuale con un gateway (basata su criteri) con routing statico. Se la rete virtuale di destinazione esiste già, deve avere point-to-site VPN attivata con un gateway con routing dinamico, prima di poter essere app tooan connesso. Se il gateway è impostato toostatic routing, è possibile attivare una VPN point-to-site. 

Per altre informazioni, vedere [Integrare un'app in una rete virtuale di Azure](web-sites-integrate-with-vnet.md#getting-started).

## <a name="in-my-app-service-environment-why-can-i-create-only-one-app-service-plan-even-though-i-have-two-workers-available"></a>Nell'ambiente del servizio app, perché è possibile creare solo un piano di servizio app anche se sono disponibili due ruoli di lavoro?

tolleranza di errore tooprovide, ambiente del servizio App richiede che ogni pool di lavoro almeno una risorsa di calcolo. risorse di calcolo aggiuntive Hello non possono essere assegnata un carico di lavoro.

Per ulteriori informazioni, vedere [come un ambiente del servizio App toocreate](app-service-web-how-to-create-an-app-service-environment.md).

## <a name="why-do-i-see-timeouts-when-i-try-toocreate-an-app-service-environment"></a>Per vedere i timeout quando si tenta di toocreate un ambiente del servizio App?

Talvolta, la creazione di un ambiente del servizio app ha esito negativo. In tal caso, vedrai il seguente errore nel log attività hello hello:
```
ResourceID: /subscriptions/{SubscriptionID}/resourceGroups/Default-Networking/providers/Microsoft.Web/hostingEnvironments/{ASEname}
Error:{"error":{"code":"ResourceDeploymentFailure","message":"hello resource provision operation did not complete within hello allowed timeout period.”}}
```

tooresolve, assicurarsi che nessuno dei hello seguenti condizioni sono vere:
* subnet Hello è troppo piccolo.
* subnet Hello non è vuoto.
* ExpressRoute impedisce i requisiti di connettività di rete hello di un ambiente del servizio App.
* I requisiti di connettività di rete hello di un ambiente del servizio App impedisce a un gruppo di sicurezza di rete non valido.
* Il tunneling forzato è attivato.

Per altre informazioni, vedere [Problemi più frequenti quando si distribuisce o si crea un nuovo ambiente del servizio app di Azure](https://blogs.msdn.microsoft.com/waws/2016/05/13/most-frequent-issues-when-deploying-creating-a-new-azure-app-service-environment-ase/).

## <a name="why-cant-i-delete-my-app-service-plan"></a>Perché non è possibile eliminare il piano del servizio app?

Se le app di servizio App sono associate a hello piano di servizio App, è possibile eliminare un piano di servizio App. Prima di eliminare un piano di servizio App, rimuovere tutte le applicazioni di servizio App associate hello piano di servizio App.

## <a name="how-do-i-schedule-a-webjob"></a>Come è possibile pianificare un processo Web?

Per creare un processo Web pianificato, utilizzare le espressioni Cron:

1. Creare un file settings.job.
2. In questo file JSON, includere una proprietà di pianificazione tramite un'espressione Cron: 
    ```
    { "schedule": "{second}
    {minute} {hour} {day}
    {month} {day of hello week}" }
    ```

Per altre informazioni sui processi Web pianificati, vedere [Creare un processo Web pianificato utilizzando un'espressione Cron](web-sites-create-web-jobs.md#CreateScheduledCRON).

## <a name="how-do-i-perform-penetration-testing-for-my-app-service-app"></a>Come si esegue il test di penetrazione per l'app del servizio app?

test di penetrazione tooperform, [inviare una richiesta](https://security-forms.azure.com/penetration-testing/terms).

## <a name="how-do-i-configure-a-custom-domain-name-for-an-app-service-web-app-that-uses-traffic-manager"></a>Come si configura un nome di dominio personalizzato per un app We del servizio app che utilizza Gestione traffico?

toolearn toouse un nome di dominio personalizzato con un'applicazione di servizio App che Usa gestione traffico di Azure per il bilanciamento del carico, vedere [configurare un nome di dominio personalizzato per un'app web di Azure con gestione traffico](web-sites-traffic-manager-custom-domain-name.md).

## <a name="my-app-service-certificate-is-flagged-for-fraud-how-do-i-resolve-this"></a>Il certificato del servizio app è contrassegnato per illecito. Come posso risolvere il problema?

Durante la verifica del dominio hello un acquisto di certificati di servizio App, si potrebbe vedere hello seguente messaggio:

"Il certificato è stato segnalato per una potenziale frode. richiesta di Hello è attualmente in fase di revisione. Se il certificato di hello diventa utilizzabile entro 24 ore, contattare il supporto tecnico di Azure."

Come messaggio hello indicato, il processo di verifica illecito può richiedere too24 ore toocomplete. Durante questo periodo, si procederà messaggio hello toosee.

Se il certificato di servizio App continua tooshow questo messaggio dopo 24 ore, eseguire lo script di PowerShell seguente hello. hello contatti di script Hello [provider certificate](https://www.godaddy.com/) direttamente il problema di hello tooresolve.

```
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId <subId>
$actionProperties = @{
    "Name"= "<Customer Email Address>"
    };
Invoke-AzureRmResourceAction -ResourceGroupName "<App Service Certificate Resource Group Name>" -ResourceType Microsoft.CertificateRegistration/certificateOrders -ResourceName "<App Service Certificate Resource Name>" -Action resendRequestEmails -Parameters $actionProperties -ApiVersion 2015-08-01 -Force   
```

## <a name="how-do-authentication-and-authorization-work-in-app-service"></a>Come funzionano autenticazione e autorizzazione nel servizio app?

Per la documentazione dettagliata sull'autenticazione e l'autorizzazione nel servizio app, vedere [Sicurezza del servizio app](../app-service/app-service-security-readme.md). documentazione di Hello presenta anche informazioni sulla configurazione di servizio App toouse vari identificare accessi provider:
* [Azure Active Directory](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md)
* [Facebook](../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md)
* [Google](../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md)
* [Account Microsoft](../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md)
* [Twitter](../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md)

## <a name="how-do-i-redirect-hello-default-azurewebsitesnet-domain-toomy-azure-web-apps-custom-domain"></a>Modalità reindirizzamento predefinito hello *. dominio personalizzato dell'app di azurewebsites.net dominio toomy web di Azure?

Quando si crea un nuovo sito Web tramite le applicazioni Web in Azure, valore predefinito è *sitename*. dominio azurewebsites.net assegnato sito tooyour. Se si aggiunge un sito di tooyour nome host personalizzato e non desidera che gli utenti toobe in grado di tooaccess predefinito *. dominio azurewebsites.net, è possibile reindirizzare l'URL predefinito hello. toolearn come tooredirect tutto il traffico da predefinito dominio tooyour dominio personalizzato del sito Web, vedere [reindirizzamento hello predefinito dominio tooyour dominio personalizzato in App web di Azure](http://www.zainrizvi.io/2016/04/07/block-default-azure-websites-domain/).

## <a name="how-do-i-determine-which-version-of-net-version-is-installed-in-app-service"></a>Come si determina la versione di .NET installata nel servizio app?

Hello più rapido modo toofind hello versione di Microsoft .NET è installato nel servizio App è tramite console Kudu hello. È possibile accedere console Kudu hello dal portale hello o utilizzando hello URL dell'applicazione di servizio App. Per istruzioni dettagliate, vedere [verifica della versione di .NET installata hello nel servizio App](https://blogs.msdn.microsoft.com/waws/2016/11/02/how-to-determine-the-installed-net-version-in-azure-app-services/).

## <a name="why-isnt-autoscale-working-as-expected"></a>Perché la scalabilità automatica non funziona come previsto?

Se non è stato ridimensionato scalabilità automatica di Azure in o scalare orizzontalmente l'istanza di hello web app come previsto, potrebbe essere in esecuzione in uno scenario in cui è intenzionalmente scegliere non tooscale tooavoid un ciclo infinito di scadenza troppo "instabile". Ciò si verifica in genere quando non è un margine sufficiente tra i limiti di scalabilità orizzontale e scalabilità in hello. toolearn tooavoid "instabile" e tooread su altre procedure consigliate di scalabilità automatica, vedere [le procedure consigliate di scalabilità automatica](../monitoring-and-diagnostics/insights-autoscale-best-practices.md#autoscale-best-practices).

## <a name="why-does-autoscale-sometimes-scale-only-partially"></a>Perché la scalabilità automatica talvolta viene applicata solo parzialmente?

La scalabilità automatica si attiva quando le metriche superano i limiti preconfigurati. In alcuni casi, è possibile notare che la capacità di hello è solo parzialmente riempita confrontati toowhat previsto. Questa situazione può verificarsi quando non sono disponibili numerosi hello istanze desiderate. In questo scenario, scalabilità automatica parzialmente riempie con numero di istanze disponibili hello. Scalabilità automatica viene quindi eseguita hello ribilanciamento logica tooget maggiore capacità. Alloca hello rimanenti istanze. Ciò potrebbe richiedere alcuni minuti.

Se il numero di hello previsto di istanze non viene visualizzato dopo pochi minuti, è possibile che la ricarica parziale hello è stato sufficiente metriche hello toobring all'interno dei limiti di hello. In alternativa, potrebbero avere progressive scalabilità automatica perché ha raggiunto un limite inferiore metriche hello.

Se nessuna di queste condizioni si applicano e hello problema persiste, inviare una richiesta di supporto.

## <a name="how-do-i-turn-on-http-compression-for-my-content"></a>Come si attiva la compressione HTTP per il contenuto?

tooturn sulla compressione sia per i tipi di contenuto statici e dinamici, aggiungere hello codice toohello a livello di applicazione Web. config seguente:

```
<system.webServer>
<urlCompression doStaticCompression="true" doDynamicCompression="true" />
< /system.webServer>
```

È inoltre possibile specificare dinamico specifico hello e i tipi MIME statici che si desidera toocompress. Per ulteriori informazioni, vedere la domanda di forum risposta tooa in [httpCompression impostazioni in un sito Web Azure semplice](https://social.msdn.microsoft.com/Forums/azure/890b6d25-f7dd-4272-8970-da7798bcf25d/httpcompression-settings-on-a-simple-azure-website?forum=windowsazurewebsitespreview).

## <a name="how-do-i-migrate-from-an-on-premises-environment-tooapp-service"></a>Come la migrazione da un tooApp ambiente locale del servizio?

siti toomigrate da Linux e Windows web server tooApp servizio, è possibile utilizzare Azure App Service Migration Assistant. strumento di migrazione Hello crea App web e i database in Azure in base alle esigenze e quindi pubblica hello contenuti. Per altre informazioni, vedere [Azure App Service Migration Assistant](https://www.movemetothecloud.net/).
