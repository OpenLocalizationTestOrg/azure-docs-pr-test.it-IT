---
title: aaaOptions per eseguire la migrazione da Azure RemoteApp | Documenti Microsoft
description: Informazioni sulle opzioni di hello per eseguire la migrazione da Azure RemoteApp.
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>Opzioni per la migrazione da Azure RemoteApp
> [!IMPORTANT]
> Azure RemoteApp verrà sospeso a partire dal 31 agosto 2017. Hello lettura [annuncio](https://go.microsoft.com/fwlink/?linkid=821148) per informazioni dettagliate.


Se è stata interrotta con RemoteApp di Azure a causa di hello [annuncio del ritiro](https://go.microsoft.com/fwlink/?linkid=821148) o perché è stata completata la valutazione, è necessario toomigrate di fuori di servizio app di Azure RemoteApp tooanother. La migrazione può essere effettuata in due modi: con una distribuzione autogestita (spesso denominata Infrastructure as a Service [IaaS]) o tramite un'offerta completamente gestita (spesso denominata Platform as a Service oppure Software as a Service [PaaS/SaaS]). 

L'approccio IaaS self-service consiste in una distribuzione "fai da te" gestita dall'utente e di sua proprietà, direttamente distribuita su macchine virtuali (VM) o sistemi fisici. In altri hello terminare, l'offerta più simili a Azure RemoteApp - un partner fornisce un livello di servizio all'inizio di una soluzione di comunicazione remota che gestisce operativo un PaaS/SaaS completamente gestito e la manutenzione, quando il computer, come cliente hello, eseguire alcune app e l'immagine di gestione.

[Visualizzare hello Azure RemoteApp webinar sulle opzioni di migrazione](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp), o di lettura in per altre informazioni (con esempi di hello diversa opzioni di hosting).

## <a name="self-managed-iaas-solutions"></a>Soluzioni autogestite (IaaS)
### <a name="rds-on-iaas"></a>**RDS su IaaS**
È possibile implementare una distribuzione di Servizi Desktop remoto (in Windows Server) basata su una sessione nativa tramite RemoteApp o desktop locali oppure in un ambiente ospitato (come le VM di Azure). Le distribuzioni di Servizi Desktop remoto su IaaS sono particolarmente indicate per i clienti che le conoscono già e che possiedono le necessarie competenze tecniche in merito. 

> [!NOTE]
> È necessario un contratto multilicenza con Software Assurance (SA) per toouse licenze accesso client di servizi desktop remoto questa opzione di distribuzione.

Distribuire Servizi Desktop remoto nelle VM di Azure è più semplice che mai se si usano i modelli di distribuzione e applicazione delle patch (leggere una [panoramica](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/) e quindi [accedere ai modelli](https://aka.ms/rdautomation)). È possibile ottenere hello stesse funzionalità di scalabilità elastica con risorse del modello di distribuzione classico di Azure (non le risorse di un modello di risorse di Azure) all'interno di Azure RemoteApp con hello [script di scalabilità automatica](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76), anche se esistono più elementi le personalizzazioni e le configurazioni. Quando si distribuisce Servizi Desktop remoto in macchine virtuali di Azure, il supporto viene fornito tramite [Azure supporta](https://azure.microsoft.com/support/plans/), hello stesso personale di supporto tecnico è supportata con Azure RemoteApp. È possibile ottenere stime dei costi in base all'utilizzo esistente contattando [supporto Azure](https://azure.microsoft.com/support/plans/), calcoli può essere eseguita manualmente o utilizzando un appena toobe rilasciato calcolatore dei costi.  Inoltre, con le macchine virtuali serie N (attualmente in anteprima privata) è possibile aggiungere vGPU - lieti di ricevere informazioni sull'aggiunta di vGPU e su come troppo[sfruttare i miglioramenti di servizi desktop remoto in Windows Server 2016](https://myignite.microsoft.com/videos/2794) nella sessione il nostro Ignite.   

Sono disponibili le guide alla distribuzione dettagliata per [Windows Server 2012 R2](http://aka.ms/rdsonazure) e [Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist con la distribuzione. Estrarre hello [blog di Desktop remoto](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services) per notizie più recenti di hello.

### <a name="citrix-on-iaas"></a>**Citrix in IaaS**
Una distribuzione Citrix nativa di XenApp o XenDesktop in base alla sessione può essere effettuata in locale o in un ambiente ospitato (ad esempio, nelle VM di Azure). 

Estrarre hello Guida dettagliata alla distribuzione, [Citrix XA 7.6 in Azure](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx), per ulteriori informazioni. Sono inoltre disponibili altre informazioni su [Citrix in Azure](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx), con in più il calcolatore dei prezzi. È anche possibile trovare un [contatto Citrix](http://citrix.com/English/contact/index.asp) toodiscuss le opzioni.

## <a name="fully-managed-paassaas-offerings"></a>Offerte completamente gestite (PaaS/SaaS)

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (rilasciato nell'aprile 2017)
Disponibili su hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials), Citrix informazioni Essentials è hello nuova applicazione virtualizzazione servizio, la combinazione di risparmio energia hello e flessibilità di hello piattaforma Cloud Citrix con hello semplice prescrittivo, e visione all'uso di Microsoft Azure RemoteApp. 

I clienti di Azure RemoteApp esistenti possono [registrarsi per una prova gratuita](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/).  Nota: solo il servizio utente Citrix è gratuito, verranno addebitati i costi di calcolo e archiviazione di Azure

Altre informazioni:
- [Eseguire la migrazione da Azure RemoteApp tooCitrix informazioni Essentials](remoteapp-migrate-citrix.md)
- [Citrix e Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html)
- [Presentazione di Citrix XenApp Essentials](https://www.youtube.com/watch?v=91Z7CCfQ-9k).  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Servizio Citrix Cloud XenApp e servizio XenDesktop 

[Servizio informazioni Cloud di Citrix e XenDesktop Service](https://www.citrix.com/products/citrix-cloud/services.html) sia hello la soluzione migliore per il recapito di hello di sia le applicazioni e desktop, più avanzate di gestione e funzionalità di monitoraggio. 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (nome della piattaforma: MyCloudIT)
[MyCloudIT](https://mycloudit.com) è una piattaforma di automazione per toosimplify le aziende IT, ottimizzare e scalare migrazione hello e recapito di desktop remoto, le applicazioni remote e infrastruttura hello Cloud di Microsoft Azure. 

piattaforma MyCloudIT Hello riduce il tempo di distribuzione del 95%, Azure costo del 30% e sposta l'intera infrastruttura IT di propri clienti nel cloud hello nel giro di qualche pressioni di tasti. Partner possono ora gestire i clienti da un dashboard globale, gli utenti finali di servizio in tutto il mondo hello come mai prima e aumento delle dimensioni dei ricavi senza aggiungere un ulteriore sovraccarico o formazione di Azure completa.  

> Sede principale: Dallas (Texas)
> 
> Regione operativa: tutto il mondo
> 
> Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Provider di servizi cloud Microsoft: sì
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe
> 
> Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, Vicepresidente dell'area Business Development
> 
> Telefono: 972-218-0741
>   
> E-mail: [brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Frame

Le organizzazioni IT dell'organizzazione e per enti pubblici, provider di servizi gestiti e principali fornitori di software scegliere toocreate Frame e gestire le aree di lavoro nel cloud hello protette, definita dal software. Da organizzazioni di piccole dimensioni toolarge, Frame rende estremamente semplice toolet utenti accedere alle applicazioni di Windows in qualsiasi browser da qualsiasi dispositivo. Hello Frame piattaforma include tutto ciò che un amministratore deve toodeploy di applicazioni cloud hello inclusi hello dell'infrastruttura di Azure e licenze di servizi desktop remoto (riportare il proprio account Azure e licenze è facoltativo). 

Altre informazioni su [Frame in Azure](https://www.fra.me/ara). 

> Località primaria: San Mateo, CA, USA
>
> Regione operativa: tutto il mondo
>
> Partner Microsoft: Sì
> 
> Telefono: 1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu offre una semplice soluzione online per l'area di lavoro che esegue applicazioni legacy, SaaS e documenti da un browser html5. Di conseguenza rende disponibili tutte le applicazioni in modo sicuro in qualsiasi tipo di dispositivo. Per i servizi SaaS è disponibile un'ampia gamma di opzioni Single Sign-On. Inoltre è possibile integrare profondamente diversi file system (cloud) nell'area di lavoro. Mobilità toofull successiva, RTF online dell'area di lavoro dell'Awingu fornirà una sicurezza ottimale con controlli granulari (ad esempio il download/caricamento), informazioni complete sull'utilizzo di controllo, multi-Factor Authentication (ad esempio Azure MFA), la registrazione di sessioni e altro ancora. Awingu consente in modo predefinito la condivisione dei documenti e delle sessioni di applicazione per una collaborazione ottimizzata e sicura.
La soluzione Awingu è multi-tenant, multi-AD e open API. È utilizzata da piccole e grandi aziende, provider di servizi cloud e [ISV](http://www.isv2saas.com). Questi clienti apprezzano particolarmente hello semplice di utilizzo, per semplificare l'installazione e a basso costo totale di proprietà.

È Awingu All-in-One [disponibile in Azure Marketplace hello](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm) con 2 utenti simultanei incorporati. Sono disponibili licenze aggiuntive tramite un'[ampia gamma di distributori e rivenditori](http://www.awingu.com/reseller).

Altre informazioni, vedere [Awingu su come alternativa tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/).


> Sede principale: Belgio
> 
> Aree operative: EMEA, America del Nord e Brasile
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe 
> 
> **Globale**:
> 
> Arnaud Marlière, CMO
> 
> E-mail: [arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> Telefono: +1 646 583 3025
> 
> **Sede centrale in Belgio**:
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> E-mail: [info@awingu.com](mailto:info@awingu.com) 
> 
> Telefono: +32 9 296 40 11
> 
> **USA**:
> 
> 7 floor, Ave 1177 di hello Americas,
> 
> New York, NY 10036
> 
> E-mail: [info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Provider di servizi ospitati Microsoft
I partner di hosting offrono in genere completamente gestito ospitato desktop di Windows hello di servizio dell'applicazione, che può includere la gestione delle risorse di Azure, sistemi operativi, applicazioni e supporto tecnico con i partner di hello di licenze contratti Microsoft e altri fornitori di software insieme in un contratto di licenza di Provider di servizi tooallow rivendita di licenza di accesso sottoscrittore (SAL). Hello seguito vengono fornite informazioni dettagliate e informazioni di contatto per alcune delle hosting hello specializzate nell'assistenza ai clienti con la migrazione di Azure RemoteApp. Estrarre [elenco corrente di hello del provider di servizi ospitati](http://aka.ms/rdsonazurecertified) ha completato l'hello in IaaS apprendimento percorso e la valutazione di servizi desktop remoto.  

### <a name="citrix-service-provider-program"></a>Programma Citrix Service Provider
Programma di Provider del servizio Citrix Hello rende più semplice per semplicità di hello toodeliver provider del servizio di virtuale cloud computing tooSMBs, l'offerta di servizi di hello che vogliono in un modello semplice e pagamento a consumo. I provider di servizi Citrix crescita SPLA di Microsoft ed espandere gli investimenti di piattaforma di servizi desktop remoto con qualsiasi dispositivo, accesso remoto via Internet, hello più ampio supporto dell'applicazione, un'esperienza, maggiore sicurezza e aumentare la scalabilità. A loro volta, gli stessi provider di servizi Citrix possono attrarre più sottoscrittori, aumentare la soddisfazione dei clienti e ridurre i costi operativi. [Leggere altre informazioni](http://www.citrix.com/products/service-providers.html) o [cercare un partner](https://www.citrix.com/buy/partnerlocator.html).

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com) è progettato per offrire soluzioni desktop ospitate, recapito completo desktop e applicazioni di ISV esperienze basate su tecnologia tooa globale client Microsoft base da Azure e i propri Data Center.

> Sede principale: Londra; Singapore; Houston (Texas)
> 
> Regione operativa: tutto il mondo
> 
> Stato partner: Gold
> 
> Provider di servizi cloud Microsoft: sì
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe
> 
> Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](http://www.acuutech.com/ara-migration/)
> 
> **Regno Unito**:
>   
> 5/6 York House, Langston Road,
>   
> Loughton, Essex IG10 3TQ
>   
> Telefono: +44 (0) 20 8502 2155
> 
> **Singapore**:
>   
> 100 Cecil Street, #09-02, 
>   
> Hello 069532 globo, Singapore
> 
> Telefono: +65 6709 4933
>   
> **America del Nord**:
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, TX 77098
>   
> Telefono: +1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en) è progettato per gli ISV transizione toohello Cloud e ISV' ricerca toooptimize le impostazioni di cloud corrente. ASPEX offre un'ampia gamma di servizi gestiti, DevOps e di consulenza.  

> Sede principale: Anversa
> 
> Regione operativa: Europa occidentale
> 
> Stato partner: [Silver](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Provider di servizi cloud Microsoft: sì
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe
> 
> Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](https://www.aspex.be/en/azure-remote-apps)
> 
> Telefono: +3232202198
> 
> E-mail: [info@aspex.be](mailto:info@aspex.be)
> 
> Web: [http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/) consente di aziende, amministrazioni locali, organismi non governativi, sanitari con il viaggio verso un modo efficiente di lavoro in hello Cloud Microsoft. Produttività e sicurezza in qualsiasi luogo, con qualsiasi dispositivo e a basso costo IT. Caase.com è un vero specialista di Microsoft Office365, Azure, Enterprise Mobility e Sicurezza e Windows. Grazie alla consulenza, ai servizi di migrazione, ai programmi di adozione, alla formazione, alla gestione e al supporto di Microsoft, Caase.com crea una piattaforma sicura e ottimizzata per la collaborazione per i dipendenti, i partner e i fornitori dei clienti.
Caase.com è mastermind hello di hello Azure remoto dell'area di lavoro (area di lavoro per dispositivi mobili) e hello digitale all'area di lavoro (Social Intranet). Entrambe le soluzioni – eseguite con l'adozione di – sono foundation hello che consente agli utenti di hello di queste soluzioni di analisi di più piacevole, efficace e di hello nella loro toohello route Cloud Microsoft.
Per la traduzione in olandese e un filmato di supporto visitare questa pagina: http://caase.com/over-ons/

> Area di operatività: con sede in Olanda e portata globale
> 
> Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Provider di servizi cloud Microsoft: sì
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe
> 
> Soluzioni per la migrazione di Azure RemoteApp: sì, [altre informazioni](http://caase.com/diensten/microsoft-azure/).
> 
> 
> Paesi Bassi:
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> Telefono: +31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Nerdio per Azure](http://getnerdio.com/nfa/) è una piattaforma di automazione IT che offre provisioning estremamente semplice, gestione e ottimizzazione di ambienti IT completati hello cloud Microsoft. Consente di configurare desktop virtuali, applicazioni remote e server in un paio di ore; Amministrare l'ambiente hello in tre clic o meno con il portale di amministrazione di Nerdio. Utilizzare intelligente il ridimensionamento automatico e salvare 40% di too60 nelle risorse IaaS di Azure.

> Sede principale: area di Chicago, IL Sede operativa: a livello globale Stato del partner: [Oro](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1) Provider del servizio cloud di Microsoft: sì
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe
> 
> Soluzioni per la migrazione di Azure RemoteApp: sì
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> USA
> 
> (844) 4NERDIO ext. 6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) offre un portfolio Microsoft Dynamics completo (NAV, AX, GP, SL, CRM) con cloud privato e pubblico (Azure).

> Località primaria: Paesi Bassi
> 
> Area operativa: tutto il mondo
> 
> Stato partner: [Gold](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Provider di servizi cloud Microsoft: sì
> 
> Offerta di soluzioni desktop e RemoteApp basate sulla sessione: sì, entrambe
> 
> **EMEA**:
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> Hello (Paesi Bassi)
> 
> Telefono: +31 20 547 8060 
> 
>  **Americhe**:
> 
> 171 Saxony Road, Suite 105
> 
> Encinitas, CA 92024
> 
> San Diego
> 
> Stati Uniti
> 
> Telefono: +1 858 385 8900 
> 
> **APAC**:
> 
> 105 Cecil Street
>    
> \#11-08, hello ottagono
> 
> Singapore 069534
> 
> Singapore
>   
> Telefono - Singapore: +65 6222 6591
> 
> Telefono - Australia: +61 2 8310 5568 
>    
> Telefono - Nuova Zelanda: +64 4 488 0321
> 
## <a name="need-more-help"></a>Ulteriore assistenza
Per farsi aiutare nella scelta o se si hanno altre domande, Utilizzare uno dei seguenti metodi tooget Guida hello. 

1. Scrivere un'e-mail all'indirizzo [arainfo@microsoft.com](mailto:arainfo@microsoft.com).
2. Contattare il [supporto tecnico di Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). Aprire un [caso di supporto su Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade).
3. Contattare il [team di vendita locale](https://azure.microsoft.com/overview/sales-number/).

