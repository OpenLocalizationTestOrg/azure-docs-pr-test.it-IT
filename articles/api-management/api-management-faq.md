---
title: domande frequenti su gestione API aaaAzure | Documenti Microsoft
description: Informazioni su hello risponde alle domande toocommon, modelli e procedure consigliate in Gestione API di Azure.
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 9e7cdf1b881a4dfed4bd2cfd7fbb4994f48b5f79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-api-management-faqs"></a>Domande frequenti su Gestione API di Azure
Ottenere hello risposte toocommon domande, i modelli e procedure consigliate per gestione API di Azure.

## <a name="contact-us"></a>Contatti
* [Come posso fare team di gestione API di Microsoft Azure hello domande?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question)


## <a name="frequently-asked-questions"></a>Domande frequenti
* [Che cosa significa se una funzionalità è in anteprima?](#what-does-it-mean-when-a-feature-is-in-preview)
* [Come è possibile proteggere la connessione hello tra il gateway di gestione API hello e i servizi back-end?](#how-can-i-secure-the-connection-between-the-api-management-gateway-and-my-back-end-services)
* [Come è possibile copiare l'istanza servizio Gestione API istanza tooa nuovo?](#how-do-i-copy-my-api-management-service-instance-to-a-new-instance)
* [È possibile gestire l'istanza di Gestione API a livello di codice?](#can-i-manage-my-api-management-instance-programmatically)
* [Come è possibile aggiungere un gruppo di amministratori toohello utente?](#how-do-i-add-a-user-to-the-administrators-group)
* [Perché è criteri hello che desidera tooadd disponibile in editor Criteri di hello?](#why-is-the-policy-that-i-want-to-add-unavailable-in-the-policy-editor)
* [Come si usa il controllo delle versioni API in Gestione API?](#how-do-i-use-api-versioning-in-api-management)
* [Come si configurano più ambienti in una sola API?](#how-do-i-set-up-multiple-environments-in-a-single-api)
* [È possibile usare SOAP con Gestione API?](#can-i-use-soap-with-api-management)
* [È una costante di indirizzo IP di hello API Gestione gateway? Può essere usato nelle regole del firewall?](#is-the-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules)
* [È possibile configurare un server di autorizzazione OAuth 2.0 con la sicurezza AD FS?](#can-i-configure-an-oauth-20-authorization-server-with-adfs-security)
* [Il metodo di routing utilizza Gestione API in aree geografiche di distribuzioni toomultiple?](#what-routing-method-does-api-management-use-in-deployments-to-multiple-geographic-locations)
* [È possibile utilizzare un toocreate di modello un'istanza del servizio Gestione API di gestione risorse di Azure?](#can-i-use-an-azure-resource-manager-template-to-create-an-api-management-service-instance)
* [È possibile usare un certificato SSL autofirmato per un back-end?](#can-i-use-a-self-signed-ssl-certificate-for-a-back-end)
* [Motivo per cui ottenere un errore di autenticazione quando si tenta di tooclone un repository GIT?](#why-do-i-get-an-authentication-failure-when-i-try-to-clone-a-git-repository)
* [Gestione API funziona con ExpressRoute?](#does-api-management-work-with-azure-expressroute)
* [Perché è necessaria una subnet dedicata nelle reti virtuali di Resource Manager quando Gestione API viene distribuita in tali reti?](#why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them)
* [Che cos'è la dimensione della subnet minimo hello necessaria quando si distribuisce gestione API in una rete virtuale?](#what-is-the-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet)
* [È possibile spostare un servizio di gestione API da una sottoscrizione tooanother?](#can-i-move-an-api-management-service-from-one-subscription-to-another)
* [Esistono restrizioni o problemi noti relativi all'importazione di questa API?](#are-there-restrictions-on-or-known-issues-with-importing-my-api)

### <a name="how-can-i-ask-hello-microsoft-azure-api-management-team-a-question"></a>Come posso fare team di gestione API di Microsoft Azure hello domande?
È possibile contattare Microsoft in uno dei modi seguenti:

* Pubblicare le domande sul [forum MSDN di Gestione API](https://social.msdn.microsoft.com/forums/azure/home?forum=azureapimgmt).
* Inviare un messaggio di posta elettronica troppo<mailto:apimgmt@microsoft.com>.
* Inviare una richiesta di funzionalità hello [forum sul feedback Azure su](https://feedback.azure.com/forums/248703-api-management).

### <a name="what-does-it-mean-when-a-feature-is-in-preview"></a>Che cosa significa se una funzionalità è in anteprima?
Quando una funzionalità è in anteprima, significa che si sta attivamente ricerca commenti e suggerimenti su come funzionalità hello è alle proprie esigenze. Una funzionalità di anteprima è completa, ma è possibile che ci accerteremo un'interruzione di modifica di commenti e suggerimenti toocustomer di risposta. È consigliabile non far dipendere l'ambiente di produzione da una funzionalità in anteprima. Se si dispone di eventuali commenti e suggerimenti sulle funzionalità di anteprima, Saremmo lieti di sapere tramite una delle opzioni di contatto hello in [come è possibile fare team di gestione API di Microsoft Azure hello domande?](#how-can-i-ask-the-microsoft-azure-api-management-team-a-question).

### <a name="how-can-i-secure-hello-connection-between-hello-api-management-gateway-and-my-back-end-services"></a>Come è possibile proteggere la connessione hello tra il gateway di gestione API hello e i servizi back-end?
Si dispone di numerose opzioni hello di toosecure di connessione tra il gateway di gestione API hello e i servizi back-end. È possibile:

* Usare l'autenticazione HTTP di base. Per altre informazioni, vedere [Configurare le impostazioni API](api-management-howto-create-apis.md#configure-api-settings).
* Utilizzare l'autenticazione reciproca di SSL, come descritto in [come toosecure back-end servizi utilizzando l'autenticazione del certificato client in Gestione API di Azure](api-management-howto-mutual-certificates.md).
* Usare gli elenchi di IP consentiti nel servizio back-end. Se si dispone di un'istanza di gestione API di livello Standard o Premium, indirizzo IP di hello del gateway hello rimane costante. È possibile impostare il tooallow whitelist questo indirizzo IP. È possibile ottenere l'indirizzo IP hello dell'istanza di gestione API in hello Dashboard nel portale di Azure hello.
* Connettere il tooan di istanza di gestione API la rete virtuale di Azure.

### <a name="how-do-i-copy-my-api-management-service-instance-tooa-new-instance"></a>Come è possibile copiare l'istanza servizio Gestione API istanza tooa nuovo?
Se si desidera toocopy un'istanza nuova di istanza tooa gestione API sono disponibili diverse opzioni. È possibile:

* Utilizzare hello backup e ripristino funzione nell'API di gestione. Per ulteriori informazioni, vedere [come tooimplement il ripristino di emergenza tramite servizio di backup e ripristino configurazione di gestione API di Azure](api-management-howto-disaster-recovery-backup-restore.md).
* Creare la propria copia di backup e ripristino di funzionalità mediante hello [API REST gestione API](https://msdn.microsoft.com/library/azure/dn776326.aspx). Utilizzare toosave API REST hello e ripristinare le entità hello dall'istanza di servizio hello che si desidera.
* Scaricare la configurazione del servizio hello tramite Git e quindi caricarla tooa nuova istanza. Per ulteriori informazioni, vedere [come toosave e configurare la configurazione del servizio Gestione API tramite Git](api-management-configuration-repository-git.md).

### <a name="can-i-manage-my-api-management-instance-programmatically"></a>È possibile gestire l'istanza di Gestione API a livello di codice?
Sì, è possibile gestire Gestione API a livello di codice usando:

* Hello [API REST gestione API](https://msdn.microsoft.com/library/azure/dn776326.aspx).
* Hello [SDK libreria Gestione servizi di Microsoft Azure ApiManagement](http://aka.ms/apimsdk).
* Hello [distribuzione del servizio](https://msdn.microsoft.com/library/mt619282.aspx) e [gestione dei servizi](https://msdn.microsoft.com/library/mt613507.aspx) i cmdlet di PowerShell.

### <a name="how-do-i-add-a-user-toohello-administrators-group"></a>Come è possibile aggiungere un gruppo di amministratori toohello utente?
Ecco come è possibile aggiungere un gruppo di amministratori toohello utente:

1. Accedi toohello [portale di Azure](https://portal.azure.com).
2. Passare a gruppo di risorse toohello con l'istanza di gestione API hello da tooupdate.
3. In Gestione API, assegnare hello **Api gestione collaboratore** utente toohello ruolo.

Ora hello appena aggiunto per i collaboratori possono usare Azure PowerShell [cmdlet](https://msdn.microsoft.com/library/mt613507.aspx). Ecco come toosign in come amministratore:

1. Hello utilizzare `Login-AzureRmAccount` toosign cmdlet in.
2. Impostare hello contesto toohello sottoscrizione con il servizio hello utilizzando `Set-AzureRmContext -SubscriptionID <subscriptionGUID>`.
3. Ottenere un l'URL Single Sign-On usando `Get-AzureRmApiManagementSsoToken -ResourceGroupName <rgName> -Name <serviceName>`.
4. Utilizzare hello URL tooaccess hello del portale di amministrazione.

### <a name="why-is-hello-policy-that-i-want-tooadd-unavailable-in-hello-policy-editor"></a>Perché è criteri hello che desidera tooadd disponibile in editor Criteri di hello?
Se criteri hello desiderati tooadd viene visualizzato in grigio o ombreggiata in editor Criteri di hello, assicurarsi di essere nell'ambito corretto hello criteri hello. Ogni istruzione dei criteri è progettata per toouse in ambiti specifici e sezioni del criterio. sezioni del criterio tooreview hello e gli ambiti per i criteri, vedere Utilizzo di criteri di hello sezione [criteri di gestione API](https://msdn.microsoft.com/library/azure/dn894080.aspx).

### <a name="how-do-i-use-api-versioning-in-api-management"></a>Come si usa il controllo delle versioni API in Gestione API?
Si dispone di controllo delle versioni di alcune opzioni toouse API in Gestione API:

* In Gestione API, è possibile configurare versioni diverse di API toorepresent. Ad esempio, se esistono due API diverse, MyAPIv1 e MyAPIv2, Uno sviluppatore può scegliere toouse richiede la versione di hello hello developer.
* È anche possibile configurare l'API con un URL del servizio che non include un segmento di versione, ad esempio https://my.api. Configurare quindi un segmento di versione nel modello di [URL di riscrittura](https://msdn.microsoft.com/library/azure/dn894083.aspx#RewriteURL) di ogni operazione. Ad esempio, è possibile avere un'operazione con un [modello di URL](api-management-howto-add-operations.md#url-template) denominato /resource e un modello di [URL di riscrittura](api-management-howto-add-operations.md#rewrite-url-template) denominato /v1/Resource. È possibile modificare valore del segmento versione hello separatamente per ogni operazione.
* Se si desidera tookeep un segmento di versione "default" nell'URL di servizio hello dell'API, in operazioni selezionate, imposta un criterio che utilizza hello [impostare servizio back-end](https://msdn.microsoft.com/library/azure/dn894083.aspx#SetBackendService) del percorso della richiesta di back-end criteri toochange hello.

### <a name="how-do-i-set-up-multiple-environments-in-a-single-api"></a>Come si configurano più ambienti in una sola API?
tooset più ambienti, ad esempio, un ambiente di test e un ambiente di produzione, in una singola API sono disponibili due opzioni. È possibile:

* Le API di diversi host su hello stesso tenant.
* Host hello stesse API tenant diversi.

### <a name="can-i-use-soap-with-api-management"></a>È possibile usare SOAP con Gestione API?
Ora è disponibile il supporto per il [pass-through SOAP](http://blogs.msdn.microsoft.com/apimanagement/2016/10/13/soap-pass-through/). Gli amministratori possono importare hello WSDL del servizio di SOAP e gestione API di Azure creerà un front-end SOAP. Per i servizi SOAP sono disponibili la documentazione del portale per sviluppatori, la console di test, i criteri e l'analisi.

### <a name="is-hello-api-management-gateway-ip-address-constant-can-i-use-it-in-firewall-rules"></a>È una costante di indirizzo IP di hello API Gestione gateway? Può essere usato nelle regole del firewall?
Livelli Standard e Premium hello indirizzo IP pubblico (VIP) di hello del tenant di gestione API hello è statico per la durata di hello del tenant di hello, con alcune eccezioni. modifiche all'indirizzo IP Hello in queste circostanze:

* servizio Hello viene eliminata e quindi ricreato.
* sottoscrizione al servizio Hello è [sospeso](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) o [avvisato](https://github.com/Azure/azure-resource-manager-rpc/blob/master/v1.0/subscription-lifecycle-api-reference.md#subscription-states) (ad esempio, per nonpayment) e quindi riavviato.
* Per aggiungere o rimuovere rete virtuale di Azure (è possibile utilizzare la rete virtuale solo hello Developer e livello Premium).

Per le distribuzioni con più aree, le modifiche all'indirizzo internazionali hello se area hello è liberata e quindi reimpostato (è possibile utilizzare più aree distribuzione solo al livello Premium hello).

Ai tenant nel piano Premium configurati per la distribuzione in più aree viene assegnato un indirizzo IP pubblico per ogni area.

Nella pagina tenant hello hello portale di Azure, è possibile ottenere l'indirizzo IP (o gli indirizzi, in una distribuzione con più aree).

### <a name="can-i-configure-an-oauth-20-authorization-server-with-ad-fs-security"></a>È possibile configurare un server di autorizzazione OAuth 2.0 con la sicurezza AD FS?
toolearn tooconfigure un server di autorizzazione OAuth 2.0 con la sicurezza di Active Directory Federation Services (ADFS), vedere [utilizzando ADFS in Gestione API](https://phvbaars.wordpress.com/2016/02/06/using-adfs-in-api-management/).

### <a name="what-routing-method-does-api-management-use-in-deployments-toomultiple-geographic-locations"></a>Il metodo di routing utilizza Gestione API in aree geografiche di distribuzioni toomultiple?
Gestione API utilizza hello [metodo di routing del traffico prestazioni](../traffic-manager/traffic-manager-routing-methods.md#priority) in aree geografiche toomultiple di distribuzioni. Il traffico in ingresso viene indirizzato toohello gateway di API più vicino. Se un'area è offline, il traffico in ingresso è gateway più vicino successivo toohello automaticamente indirizzato. Altre informazioni sui metodi di routing sono disponibili in [Metodi di routing di Gestione traffico](../traffic-manager/traffic-manager-routing-methods.md).

### <a name="can-i-use-an-azure-resource-manager-template-toocreate-an-api-management-service-instance"></a>È possibile utilizzare un toocreate di modello un'istanza del servizio Gestione API di gestione risorse di Azure?
Sì. Vedere hello [servizio Gestione API di Azure](http://aka.ms/apimtemplate) modelli di avvio rapido.

### <a name="can-i-use-a-self-signed-ssl-certificate-for-a-back-end"></a>È possibile usare un certificato SSL autofirmato per un back-end?
Sì. Ecco come toouse un autofirmato SSL Secure Sockets Layer () del certificato per un back-end:

1. Creare un'entità di [back-end](https://msdn.microsoft.com/library/azure/dn935030.aspx) usando Gestione API.
2. Set hello **skipCertificateChainValidation** proprietà troppo**true**.
3. Se non si desidera più certificati autofirmati tooallow, eliminare l'entità Backend hello o impostare hello **skipCertificateChainValidation** proprietà troppo**false**.

### <a name="why-do-i-get-an-authentication-failure-when-i-try-tooclone-a-git-repository"></a>Motivo per cui ottenere un errore di autenticazione quando si tenta di tooclone un repository Git?
Se si utilizza Gestione credenziali Git o se si sta cercando un repository Git tooclone tramite Visual Studio, è possibile eseguire in un problema noto con la finestra di dialogo credenziali di Windows hello. la finestra di dialogo Hello limita i caratteri too127 lunghezza della password e tronca la password di hello generati da Microsoft. Microsoft sta lavorando con una riduzione delle password hello. Per il momento, utilizzare Git Bash tooclone il repository Git.

### <a name="does-api-management-work-with-azure-expressroute"></a>Gestione API funziona con ExpressRoute?
Sì. Gestione API funziona con ExpressRoute.

### <a name="why-do-we-require-a-dedicated-subnet-in-resource-manager-style-vnets-when-api-management-is-deployed-into-them"></a>Perché è necessaria una subnet dedicata nelle reti virtuali di Resource Manager quando Gestione API viene distribuita in tali reti?
requisito di Hello subnet dedicata per la gestione API deriva dal fatto hello, che è stato progettato su modello di distribuzione classica (V1 PAAS layer). Mentre è possibile distribuire in una VNET Gestione risorse (livello 2), esistono toothat conseguenze. Hello modello di distribuzione classica in Azure non è strettamente accoppiato al modello di gestione risorse di hello e pertanto se si crea una risorsa nel livello V2, livello V1 hello non riportarlo e problemi possono verificarsi, ad esempio Gestione API tentativo toouse un indirizzo IP che è già allocato tooa NIC (incorporato in V2).
informazioni sulla differenza dei modelli classico e Gestione risorse di Azure vedere troppo toolearn[differenza nei modelli di distribuzione](../azure-resource-manager/resource-manager-deployment-model.md).

### <a name="what-is-hello-minimum-subnet-size-needed-when-deploying-api-management-into-a-vnet"></a>Che cos'è la dimensione della subnet minimo hello necessaria quando si distribuisce gestione API in una rete virtuale?
la dimensione della subnet minimo Hello necessari toodeploy API di gestione è [/29](../virtual-network/virtual-networks-faq.md#configuration), ovvero la dimensione della subnet minimo hello che supporta Azure.

### <a name="can-i-move-an-api-management-service-from-one-subscription-tooanother"></a>È possibile spostare un servizio di gestione API da una sottoscrizione tooanother?
Sì. toolearn, vedere [spostare le risorse tooa nuovo gruppo di risorse o sottoscrizione](../azure-resource-manager/resource-group-move-resources.md).

### <a name="are-there-restrictions-on-or-known-issues-with-importing-my-api"></a>Esistono restrizioni o problemi noti relativi all'importazione di questa API?
[Problemi noti e limitazioni](api-management-api-import-restrictions.md) per i formati Open API (Swagger), WSDL e WADL.
