---
title: Directory Federation Services in Azure aaaActive | Documenti Microsoft
description: "In questo documento si apprenderà come toodeploy AD ADFS in Azure ad alta disponibilità."
keywords: Distribuire ADFS in azure, distribuire adfs di azure, azure adfs, ADFS di azure, la distribuzione di adfs, distribuzione di ADFS, adfs in azure, distribuire adfs in azure, distribuire ADFS in azure, azure ad FS, introduzione tooAD ADFS, Azure, ADFS in Azure iaas, ADFS, spostare tooazure adfs
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2c39271f7569b9ce395dce2f53f5ba5a4897b132
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Distribuzione di Active Directory Federation Services in Azure
AD FS offre funzionalità di federazione delle identità e Single Sign-On (SSO) Web protette e semplificate. Federazione con Azure AD o Office 365 consente agli utenti tooauthenticate locale utilizzando le credenziali e accedere a tutte le risorse nel cloud. Di conseguenza, diventa importante toohave una disponibilità elevata ADFS infrastruttura tooensure accedere tooresources sia in locale e nel cloud hello. Distribuzione di ADFS in Azure consente di ottenere la disponibilità elevata hello obbligatoria con un impegno minimo.
Distribuire AD FS in Azure offre diverse vantaggi. Di seguito ne sono elencati alcuni.

* **Disponibilità elevata** -con la potenza di hello Azure set di disponibilità, assicurarsi di un'infrastruttura a disponibilità elevata.
* **Facile tooScale** – necessarie prestazioni più elevate? Eseguire facilmente la migrazione di macchine potente toomore da pochi clic in Azure
* **Ridondanza geografica tra** : con Azure geografica ridondanza, si può essere certi che l'infrastruttura sia a disponibilità elevata, tutto il mondo hello
* **Facile tooManage** – con opzioni di gestione semplificata elevata nel portale di Azure, la gestione dell'infrastruttura è molto semplice e senza problemi 

## <a name="design-principles"></a>Principi di progettazione
![Progettazione della distribuzione](./media/active-directory-aadconnect-azure-adfs/deployment.png)

diagramma di Hello sopra riportato mostra hello consigliato toostart topologia di base distribuzione dell'infrastruttura di ADFS in Azure. principi di Hello dietro hello vari componenti della topologia hello sono elencati di seguito:

* **Controller di dominio/server AD FS**: se il numero di utenti è inferiore a 1.000, è sufficiente installare il ruolo AD FS nei controller di dominio. Se non si desidera che qualsiasi impatto sulle prestazioni nei controller di dominio hello o se sono presenti più di 1.000 utenti, quindi distribuire ADFS in server separati.
* **Server WAP** : è necessario toodeploy Server Proxy applicazione Web, in modo che gli utenti possono raggiungere hello ADFS quando non sono nella rete aziendale hello anche.
* **Rete Perimetrale**: Server Proxy applicazione Web hello verranno inseriti nella rete Perimetrale hello e non è consentito l'accesso solo TCP/443 tra hello DMZ e subnet interna hello.
* **Bilanciamento del carico**: tooensure un'elevata disponibilità dei server ADFS e Proxy applicazione Web, si consiglia di utilizzare un servizio di bilanciamento del carico interno per i server ADFS e bilanciamento del carico di Azure per i server Proxy applicazione Web.
* **Set di disponibilità**: distribuzione di ADFS tooprovide ridondanza tooyour Active Directory, si consiglia di raggruppare due o più macchine virtuali in un Set di disponibilità per carichi di lavoro simili. Questa configurazione assicura che durante un evento di manutenzione pianificata o non pianificata sia disponibile almeno una macchina virtuale.
* **Gli account di archiviazione**: è consigliabile toohave due account di archiviazione. Con un singolo account di archiviazione può causare toocreation di un singolo punto di errore e può causare hello distribuzione toobecome disponibile in uno scenario improbabile in cui account di archiviazione hello diventa inattivo. Con due account di archiviazione è possibile associare un account di archiviazione per ogni linea di guasto.
* **Separazione delle reti**: i server proxy applicazione Web verranno distribuiti in una rete perimetrale separata. È possibile suddividere una rete virtuale in due subnet e quindi distribuire il server Proxy applicazione Web hello in una subnet isolato. È possibile semplicemente configurare hello le impostazioni gruppo di sicurezza di rete per ogni subnet e consentire solo necessaria comunicazione tra due subnet hello. Altri dettagli sono riportati di seguito per i singoli scenari di distribuzione.

## <a name="steps-toodeploy-ad-fs-in-azure"></a>Passaggi toodeploy ADFS in Azure
i passaggi di Hello indicati in questa sezione struttura hello Guida toodeploy hello seguente rappresentate infrastruttura ADFS in Azure.

### <a name="1-deploying-hello-network"></a>1. Distribuzione di rete hello
Come indicato in precedenza, è possibile creare due subnet in una singola rete virtuale oppure creare due reti virtuali completamente diverse. Questo articolo è incentrato sulla distribuzione di una singola rete virtuale e sulla relativa divisione in due subnet. Questo è un approccio più semplice, come un gateway di rete virtuale tooVNet richiederebbe due reti virtuali separate per le comunicazioni.

**1.1 Creare una rete virtuale**

![Creare una rete virtuale](./media/active-directory-aadconnect-azure-adfs/deploynetwork1.png)

In hello portale di Azure, selezionare rete virtuale ed è possibile distribuire la rete virtuale hello e una subnet immediatamente con un solo clic. Subnet INT è definita ed è ora pronto per le macchine virtuali toobe aggiunto.
passaggio successivo Hello è tooadd un'altra subnet toohello la rete, ad esempio hello DMZ subnet. toocreate hello subnet di rete Perimetrale, è sufficiente

* Selezionare la rete hello appena creato.
* Nelle proprietà hello selezionare subnet
* Nella fare clic su Pannello di subnet hello in hello pulsante Aggiungi
* Fornire hello subnet nome e indirizzo spazio informazioni toocreate hello subnet

![Subnet](./media/active-directory-aadconnect-azure-adfs/deploynetwork2.png)

![Subnet DMZ](./media/active-directory-aadconnect-azure-adfs/deploynetwork3.png)

**1.2. La creazione di gruppi di sicurezza di rete hello**

Un rete gruppo di sicurezza () contiene un elenco di regole di elenco di controllo di accesso (ACL) che consentono o negano il traffico di rete tooyour istanze di macchina virtuale in una rete virtuale. I gruppi di sicurezza di rete possono essere associati a subnet o singole istanze VM in una subnet. Quando un gruppo è associata a una subnet, regole ACL hello si applicano le istanze VM hello tooall nella subnet.
A scopo di hello di questa Guida, si creerà due NSGs: uno per una rete interna e una rete Perimetrale. denominati rispettivamente NSG_INT e NSG_DMZ.

![Creare un gruppo di sicurezza di rete](./media/active-directory-aadconnect-azure-adfs/creatensg1.png)

Dopo aver hello che gruppo viene creato, saranno presenti regole in uscita in ingresso e 0, 0. Dopo aver installato e funzionante ruoli hello nei rispettivi server di hello, quindi hello regole in entrata e in uscita possono essere reso secondo livello toohello desiderato di sicurezza.

![Inizializzare il gruppo di sicurezza di rete](./media/active-directory-aadconnect-azure-adfs/nsgint1.png)

Dopo aver creato hello NSGs, associare subnet NSG_INT INT e NSG_DMZ con subnet rete Perimetrale. Di seguito è riportato uno screenshot di esempio:

![Configurazione dei gruppi di sicurezza di rete](./media/active-directory-aadconnect-azure-adfs/nsgconfigure1.png)

* Fare clic su Pannello di hello tooopen subnet per subnet
* Selezionare hello subnet tooassociate con hello NSG 

Dopo la configurazione, il pannello hello per le subnet dovrebbe essere simile di sotto:

![Subnet dopo la configurazione dei gruppi di sicurezza di rete](./media/active-directory-aadconnect-azure-adfs/nsgconfigure2.png)

**1.3. Creare una connessione locale tooon**

È necessario un connessione tooon sedi in ordine toodeploy hello controller di dominio (DC) in azure. Azure offre vari tooconnect opzioni di connettività del tooyour infrastruttura on-premise infrastruttura di Azure.

* Da punto a sito
* Da sito a sito di rete virtuale
* ExpressRoute

È consigliabile toouse ExpressRoute. ExpressRoute consente di creare connessioni private tra i data center di Azure e l'infrastruttura disponibile localmente o in un ambiente con percorso condiviso. Le connessioni ExpressRoute non sfruttano hello rete Internet pubblica. Offrono ulteriori affidabilità, velocità più elevate, minori latenze e una maggiore sicurezza rispetto alle connessioni tramite hello Internet.
Sebbene sia consigliabile toouse ExpressRoute, è possibile scegliere qualsiasi metodo di connessione più adatto per l'organizzazione. informazioni su ExpressRoute e hello toolearn varie opzioni di connettività con ExpressRoute, leggere [Panoramica tecnica su ExpressRoute](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Creare gli account di archiviazione
La disponibilità elevata di ordine toomaintain ed evitare una dipendenza da un singolo account di archiviazione, è possibile creare due account di archiviazione. Dividere macchine hello in ogni set di disponibilità in due gruppi e quindi assegnare ogni gruppo di un account di archiviazione separata.

![Creare gli account di archiviazione](./media/active-directory-aadconnect-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Creare set di disponibilità
Per ogni ruolo (controller di dominio/AD FS e WAP), creare set di disponibilità che conterrà 2 macchine ogni a hello minimo. Sarà così possibile ottenere una disponibilità più elevata per ogni ruolo. Mentre il set di disponibilità di hello creazione, è essenziale toodecide successivo hello:

* **Domini di errore**: hello di macchine virtuali nella stessa condivisione di dominio di errore hello stessa alimentazione e switch di rete fisica. È consigliabile usare almeno 2 domini di errore. valore predefinito di Hello è 3 e che è possibile lasciarla invariata per hello scopo della distribuzione
* **Domini di aggiornamento**: macchine appartenenti toohello nello stesso dominio di aggiornamento vengono riavviate insieme durante un aggiornamento. Si desidera toohave minimo 2 di domini di aggiornamento. valore predefinito di Hello è 5 ed è possibile lasciarla invariata per hello scopo della distribuzione

![Set di disponibilità](./media/active-directory-aadconnect-azure-adfs/availabilityset1.png)

Creare set di disponibilità seguenti hello

| Set di disponibilità | Ruolo | Domini di errore | Domini di aggiornamento |
|:---:|:---:|:---:|:--- |
| contosodcset |Controller di dominio/AD FS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Distribuire le macchine virtuali
passaggio successivo Hello è toodeploy le macchine virtuali che ospiteranno hello ruoli diversi all'interno dell'infrastruttura. In ogni set di disponibilità è consigliato un minimo di due computer. Creare quattro macchine virtuali per la distribuzione di base hello.

| Machine | Ruolo | Subnet | Set di disponibilità | Account di archiviazione | Indirizzo IP |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |Controller di dominio/AD FS |INT |contosodcset |contososac1 |Static |
| contosodc2 |Controller di dominio/AD FS |INT |contosodcset |contososac2 |Static |
| contosowap1 |WAP |Rete perimetrale |contosowapset |contososac1 |Static |
| contosowap2 |WAP |Rete perimetrale |contosowapset |contososac2 |Static |

Come è possibile osservare, non sono stati specificati gruppi di sicurezza di rete. In questo modo azure consente di utilizzare gruppo a livello di subnet hello. Quindi, è possibile controllare il traffico di rete di computer utilizzando hello che NSG singoli associato non subnet hello oppure oggetto NIC hello. Per altre informazioni, vedere [Che cos'è un gruppo di sicurezza di rete](https://aka.ms/Azure/NSG).
Indirizzo IP statico è consigliato se si sta gestendo hello DNS. È possibile usare DNS di Azure e invece hello i record DNS per il dominio, fare riferimento toohello nuove macchine da loro FQDN di Azure.
Il riquadro di macchina virtuale dovrebbe essere simile di sotto, dopo aver completata la distribuzione di hello:

![Macchine virtuali distribuite](./media/active-directory-aadconnect-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-hello-domain-controller--ad-fs-servers"></a>5. Configurazione dei controller di dominio hello / server AD FS
 In ordine tooauthenticate qualsiasi richiesta in ingresso, ADFS sarà necessario controller di dominio toocontact hello. toosave hello costose di andata e ritorno da controller di dominio di Azure tooon locale per l'autenticazione, è consigliabile toodeploy una replica del controller di dominio hello in Azure. In ordine tooattain a disponibilità elevata è consigliabile toocreate un gruppo di disponibilità di almeno 2 controller di dominio.

| Controller di dominio | Ruolo | Account di archiviazione |
|:---:|:---:|:---:|
| contosodc1 |Replica |contososac1 |
| contosodc2 |Replica |contososac2 |

* Promuovere i due server hello come controller di dominio di replica con DNS
* Configurare i server di hello ADFS installando il ruolo di hello AD FS con server manager di hello.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Distribuire il servizio di bilanciamento del carico interno
**6.1. Creare hello bilanciamento del carico interno**

toodeploy un bilanciamento del carico interno, selezionare i bilanciamenti del carico in hello portale di Azure e fare clic su Aggiungi (+).

> [!NOTE]
> Se non viene visualizzato **bilanciamenti del carico** nel menu, fare clic su **Sfoglia** in hello inferiore sinistro del portale hello e scorrere fino a visualizzare **bilanciamenti del carico**.  Quindi fare clic su tooadd stella gialla hello è tooyour menu. A questo punto selezionare hello nuova icona tooopen hello pannello toobegin configurazione di bilanciamento carico di bilanciamento del carico hello.
> 
> 

![Visualizzazione di Servizi di bilanciamento del carico](./media/active-directory-aadconnect-azure-adfs/browseloadbalancer.png)

* **Nome**: assegnare bilanciamento del carico di toohello qualsiasi nome appropriato
* **Schema**: poiché il bilanciamento del carico verrà inserito davanti al server hello AD FS e per le connessioni di rete interna solo, selezionare "Interno"
* **Rete virtuale**: scegliere hello rete virtuale in cui si intende distribuire ADFS
* **Subnet**: scegliere una subnet interna di hello qui
* **Assegnazione di indirizzi IP**: statici

![Servizio di bilanciamento del carico interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment1.png)

Dopo aver fatto clic creare hello bilanciamento del carico interno viene distribuito, verrà visualizzato nell'elenco di hello di servizi di bilanciamento del carico:

![Servizi di bilanciamento del carico dopo la distribuzione del servizio di bilanciamento del carico interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment2.png)

Passaggio successivo è tooconfigure pool back-end hello e un probe di hello back-end.

**6.2. Configurare il pool back-end del servizio di bilanciamento del carico interno**

Seleziona hello appena creato ILB nel Pannello di hello bilanciamenti del carico. Verrà aperto il pannello di impostazioni hello. 

1. Selezionare il pool back-end dal pannello impostazioni hello
2. In hello aggiungere riquadro pool back-end, fare clic sulla macchina virtuale
3. Verrà visualizzato un pannello in cui è possibile scegliere un set di disponibilità
4. Scegliere il set di disponibilità hello AD FS

![Configurare il pool back-end del servizio di bilanciamento del carico interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment3.png)

**6.3. Configurare il probe**

Nel pannello impostazioni di bilanciamento del carico interno hello selezionare probe.

1. Fare clic su Aggiungi
2. Specificare i dettagli del probe a. **Nome**: nome del probe b. **Protocollo**: TCP c. **Porta**: 443 (HTTPS) d. **Intervallo**: 5 (valore predefinito): si tratta di intervallo hello in corrispondenza del quale verrà probe macchine hello in pool back-end hello e di bilanciamento del carico interno. **Limite di soglia non integra**: 2 (predefinito val ue): si tratta di hello soglia degli errori di probe consecutivi dopo cui bilanciamento del carico interno verrà dichiarato una macchina in hello back-end del pool non risponde e interrompere l'invio del traffico tooit.

![Configurare il probe del servizio di bilanciamento del carico interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment4.png)

**6.4. Creare le regole di bilanciamento del carico**

Ordine tooeffectively saldo hello del traffico, hello bilanciamento del carico interno deve essere configurato con regole di bilanciamento del carico. In ordine toocreate una regola di bilanciamento del carico, 

1. Selezionare una regola dal pannello impostazioni hello di hello ILB di bilanciamento del carico
2. Fare clic su Aggiungi nel hello pannello regole di bilanciamento del carico
3. In hello Aggiungi pannello regola bilanciamento di carico una. **Nome**: specificare un nome per la regola hello b. **Protocollo**: selezionare TCP c. **Porta**: 443 d. **Porta back-end**: 443 e. **Pool back-end**: selezionare il pool di hello creato per AD FS hello cluster f precedenti. **Probe**: probe hello selezionare creato in precedenza per i server ADFS

![Configurare le regole di bilanciamento del servizio di bilanciamento del carico interno](./media/active-directory-aadconnect-azure-adfs/ilbdeployment5.png)

**6.5. Aggiornare il DNS con il servizio di bilanciamento del carico interno**

Passare i server DNS tooyour e creare un record CNAME per hello bilanciamento del carico interno. Hello CNAME deve essere per servizio federativo hello con indirizzo IP hello verso toohello l'indirizzo IP del bilanciamento del carico interno hello. Ad esempio se hello indirizzo DIP di bilanciamento del carico interno è 10.3.0.8 e il servizio federativo hello installato è fs.contoso.com, quindi creare un record CNAME per fs.contoso.com verso too10.3.0.8.
Ciò garantisce che tutte le comunicazioni relative fs.contoso.com finire in hello bilanciamento del carico interno e sono indirizzati in modo appropriato.

### <a name="7-configuring-hello-web-application-proxy-server"></a>7. Configurazione dei server Proxy applicazione Web hello
**7.1. Configurazione dei server di hello Proxy applicazione Web Server tooreach AD FS**

In ordine tooensure che i server Proxy applicazione Web sono server di hello ADFS in grado di tooreach dietro hello ILB, creare un record in hello %systemroot%\system32\drivers\etc\hosts per hello bilanciamento del carico interno. Si noti che il nome distinto (DN) hello devono essere nome del servizio federativo hello, ad esempio fs.contoso.com. E voce hello dell'indirizzo IP deve essere quello di indirizzo IP del ILB hello (10.3.0.8 come esempio hello).

**7.2. Installare il ruolo di Proxy applicazione Web hello**

Dopo avere verificato che i server Proxy applicazione Web sono server di hello ADFS in grado di tooreach dietro bilanciamento del carico interno, è possibile installare successivamente il server di Proxy applicazione Web hello. Server Proxy applicazione Web non essere toohello aggiunti a un dominio. Installare ruoli del Proxy applicazione Web hello in due server Proxy applicazione Web di hello selezionando il ruolo di accesso remoto hello. gestione di server Hello consentirà di installazione di toocomplete hello WAP.
Per ulteriori informazioni su come leggere toodeploy WAP, [installare e configurare i Server Proxy applicazione Web hello](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-hello-internet-facing-public-load-balancer"></a>8.  Distribuzione di hello bilanciamento del carico Internet affiancate (pubblico)
**8.1.  Creare il servizio di bilanciamento del carico con connessione Internet (pubblico)**

Nel portale di Azure hello, selezionare servizi di bilanciamento del carico e quindi fare clic su Aggiungi. Nel pannello del servizio di bilanciamento carico di hello crea, immettere le seguenti informazioni hello

1. **Nome**: nome del servizio di bilanciamento del carico hello
2. **Schema**: Pubblico. Questa opzione indica ad Azure che il servizio di bilanciamento del carico dovrà avere un indirizzo pubblico.
3. **Indirizzo IP**: creare un nuovo indirizzo IP (dinamico)

![Servizio di bilanciamento del carico con connessione Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment1.png)

Dopo la distribuzione, bilanciamento del carico hello verrà visualizzato nell'elenco di sistemi di bilanciamento carico di hello.

![Elenco dei servizi di bilanciamento del carico](./media/active-directory-aadconnect-azure-adfs/elbdeployment2.png)

**8.2. Assegnare un indirizzo IP pubblico di toohello in etichetta DNS**

Fare clic sulla voce di servizio di bilanciamento carico di hello appena creato nella hello toobring pannello bilanciamento di carico pannello hello per la configurazione di. Seguire sotto l'etichetta DNS hello tooconfigure passaggi per l'IP pubblico hello:

1. Fare clic sull'indirizzo IP pubblico hello. Verrà aperto il pannello hello per indirizzo IP pubblico hello e le relative impostazioni
2. Fare clic su Configurazione
3. Specificare un'etichetta DNS, Che diventerà etichetta DNS pubblico hello che è possibile accedere da qualsiasi posizione, ad esempio contosofs.westus.cloudapp.azure.com. È possibile aggiungere una voce in hello DNS esterno per il servizio federativo hello (ad esempio fs.contoso.com) che risolve l'etichetta di hello esterna DNS toohello bilanciamento del carico (contosofs.westus.cloudapp.azure.com).

![Configurare il servizio di bilanciamento del carico con connessione Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment3.png) 

![Configurare il servizio di bilanciamento del carico con connessione Internet (DNS)](./media/active-directory-aadconnect-azure-adfs/elbdeployment4.png)

**8.3. Configurare il pool back-end per il servizio di bilanciamento del carico con connessione Internet (pubblico)** 

Seguire hello stessi passaggi come servizio di bilanciamento del carico interno hello Creazione pool back-end di hello tooconfigure per Internet affiancate (pubblico) bilanciamento del carico come disponibilità hello impostare per i server WAP di hello. ad esempio contosowapset.

![Configurare il pool back-end del servizio di bilanciamento del carico con connessione Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment5.png)

**8.4. Configurare il probe**

Seguire hello stessi passaggi come configurazione hello carico interno tooconfigure hello probe di bilanciamento per il pool di back-end hello del server WAP.

![Configurare il probe del servizio di bilanciamento del carico con connessione Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment6.png)

**8.5. Creare regole di bilanciamento del carico**

Attenersi alla stessa procedura come esempio di bilanciamento del carico di bilanciamento del carico interno tooconfigure hello regola per TCP 443 hello.

![Configurare le regole di bilanciamento del servizio di bilanciamento del carico con connessione Internet](./media/active-directory-aadconnect-azure-adfs/elbdeployment7.png)

### <a name="9-securing-hello-network"></a>9. La protezione di rete hello
**9.1. Protezione di subnet interna hello**

In generale, è necessario hello seguendo regole tooefficiently secure subnet interna (in ordine di hello come indicato di seguito)

| Regola | Descrizione | Flusso |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Consentire le comunicazioni HTTPS hello dalla rete Perimetrale |In ingresso |
| DenyInternetOutbound |Nessun toointernet di accesso |In uscita |

![Regole di accesso interno (in ingresso)](./media/active-directory-aadconnect-azure-adfs/nsg_int.png)

[commento]: <> (![regole di accesso interno (in ingresso)](./media/active-directory-aadconnect-azure-adfs/nsgintinbound.png)) [commento]: <> (![regole di accesso interno (in uscita)](./media/active-directory-aadconnect-azure-adfs/nsgintoutbound.png))

**9.2. Protezione di subnet di rete Perimetrale hello**

| Regola | Descrizione | Flusso |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |Consenti HTTPS da internet toohello rete Perimetrale |In ingresso |
| DenyInternetOutbound |Un valore diverso da toointernet HTTPS è bloccato |In uscita |

![Regole di accesso esterno (in ingresso)](./media/active-directory-aadconnect-azure-adfs/nsg_dmz.png)

[commento]: <> (![regole di accesso esterno (in ingresso)](./media/active-directory-aadconnect-azure-adfs/nsgdmzinbound.png)) [commento]: <> (![regole di accesso esterno (in uscita)](./media/active-directory-aadconnect-azure-adfs/nsgdmzoutbound.png))

> [!NOTE]
> Se è necessaria l'autenticazione del certificato utente client (autenticazione clientTLS con i certificati utente X509), AD FS richiede l'abilitazione della porta TCP 49443 per l'accesso in ingresso.
> 
> 

### <a name="10-test-hello-ad-fs-sign-in"></a>10. Hello AD FS sign-in di test
Hello più semplice è tootest che ADFS è la pagina IdpInitiatedSignon.aspx hello. In ordine toobe in grado di toodo che, è necessario tooenable hello IdpInitiatedSignOn sulle proprietà hello AD FS. Eseguire operazioni di hello seguenti tooverify il programma di installazione di ADFS

1. Esecuzione hello di sotto di cmdlet nel server di hello AD FS, tramite PowerShell, tooset è tooenabled.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Da qualsiasi computer esterno accedere a https://adfs.thecloudadvocate.com/adfs/ls/IdpInitiatedSignon.aspx  
3. Verrà visualizzata la pagina hello ADFS come il seguente:

![Pagina di accesso di test](./media/active-directory-aadconnect-azure-adfs/test1.png)

Dopo l'accesso, verrà visualizzato un messaggio di completamento dell'operazione come illustrato di seguito:

![Completamento test](./media/active-directory-aadconnect-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Modello per la distribuzione di AD FS in Azure
modello Hello consente di distribuire una configurazione 6 macchina, 2 per i controller di dominio, AD FS e WAP.

[Modello di distribuzione di AD FS in Azure](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Durante la distribuzione di questo modello, è possibile usare una rete virtuale esistente o crearne una nuova. Hello vari parametri disponibili per la personalizzazione della distribuzione hello sono elencati di seguito con descrizione hello dell'utilizzo del parametro hello hello processo di distribuzione. 

| . | Description |
|:--- |:--- |
| Percorso |Hello area toodeploy hello risorse in, ad esempio Stati Uniti orientali. |
| StorageAccountType |tipo di Hello di hello Account di archiviazione creato |
| VirtualNetworkUsage |Indica se verrà creata una nuova rete virtuale o ne verrà usata una esistente |
| VirtualNetworkName |nome Hello di hello tooCreate di rete virtuale, obbligatorio all'utilizzo della rete virtuale nuova o esistente |
| VirtualNetworkResourceGroupName |Specifica il nome di hello hello del gruppo di risorse in cui risiede la rete virtuale esistente di hello. Quando si utilizza una rete virtuale esistente, questa diventa un parametro obbligatorio per consentire la distribuzione di hello trovare hello ID di rete virtuale esistente hello |
| VirtualNetworkAddressRange |intervallo di indirizzi di hello Hello nuova rete virtuale, obbligatorio se la creazione di una nuova rete virtuale |
| InternalSubnetName |nome Hello di subnet interna hello, obbligatoria in entrambe le opzioni di utilizzo della rete virtuale (nuove o esistente) |
| InternalSubnetAddressRange |intervallo di indirizzi Hello di subnet interna hello, che contiene hello i controller di dominio e ad FS server, obbligatorio se la creazione di una nuova rete virtuale. |
| DMZSubnetAddressRange |intervallo di indirizzi Hello della subnet di rete perimetrale hello, che contiene hello Windows application server proxy, obbligatorio se la creazione di una nuova rete virtuale. |
| DMZSubnetName |nome Hello di subnet interna hello, obbligatoria in entrambe le opzioni di utilizzo della rete virtuale (nuove o esistente). |
| ADDC01NICIPAddress |indirizzo IP interno Hello di hello primo Controller di dominio, questo indirizzo IP verrà assegnato in modo statico toohello controller di dominio e deve essere un indirizzo ip valido all'interno di subnet interna hello |
| ADDC02NICIPAddress |indirizzo IP interno Hello di hello secondo Controller di dominio, questo indirizzo IP verrà assegnato in modo statico toohello controller di dominio e deve essere un indirizzo ip valido all'interno di subnet interna hello |
| ADFS01NICIPAddress |indirizzo IP interno Hello del server ADFS prima hello, questo indirizzo IP verrà assegnato in modo statico server ADFS toohello e deve essere un indirizzo ip valido all'interno di subnet interna hello |
| ADFS02NICIPAddress |indirizzo IP interno Hello del server ADFS secondo hello, questo indirizzo IP verrà assegnato in modo statico server ADFS toohello e deve essere un indirizzo ip valido all'interno di subnet interna hello |
| WAP01NICIPAddress |indirizzo IP interno Hello del primo server WAP di hello, questo indirizzo IP verrà assegnato in modo statico server WAP toohello e deve essere un indirizzo ip valido all'interno di subnet di rete Perimetrale hello |
| WAP02NICIPAddress |indirizzo IP interno Hello del secondo server WAP di hello, questo indirizzo IP verrà assegnato in modo statico server WAP toohello e deve essere un indirizzo ip valido all'interno di subnet di rete Perimetrale hello |
| ADFSLoadBalancerPrivateIPAddress |bilanciamento del carico indirizzo IP interno Hello di hello ADFS, questo indirizzo IP verrà assegnato in modo statico toohello servizio di bilanciamento del carico e deve essere un indirizzo ip valido all'interno di subnet interna hello |
| ADDCVMNamePrefix |Il prefisso del nome della macchina virtuale per i controller di dominio |
| ADFSVMNamePrefix |Il prefisso del nome della macchina virtuale per i server AD FS |
| WAPVMNamePrefix |Il prefisso del nome della macchina virtuale per i server WAP |
| ADDCVMSize |dimensioni delle macchine virtuali Hello di hello i controller di dominio |
| ADFSVMSize |dimensioni delle macchine virtuali Hello del server ADFS hello |
| WAPVMSize |dimensioni delle macchine virtuali Hello del server WAP hello |
| AdminUserName |nome Hello di hello amministratore locale di macchine virtuali hello |
| AdminPassword |password account amministratore locale hello delle macchine virtuali hello Hello |

## <a name="additional-resources"></a>Risorse aggiuntive
* [Set di disponibilità](https://aka.ms/Azure/Availability) 
* [Servizio di bilanciamento del carico di Azure](https://aka.ms/Azure/ILB)
* [Servizio di bilanciamento del carico interno](https://aka.ms/Azure/ILB/Internal)
* [Servizio di bilanciamento del carico con connessione Internet](https://aka.ms/Azure/ILB/Internet)
* [Account di archiviazione](https://aka.ms/Azure/Storage)
* [Reti virtuali di Azure](https://aka.ms/Azure/VNet)
* [Collegamenti relativi ad AD FS e proxy applicazione Web](http://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Passaggi successivi
* [Integrazione delle identità locali con Azure Active Directory](active-directory-aadconnect.md)
* [Configurazione e gestione di AD FS con Azure AD Connect](active-directory-aadconnectfed-whatis.md)
* [Distribuzione di AD FS a disponibilità elevata tra aree geografiche in Azure con Gestione traffico di Azure](../active-directory-adfs-in-azure-with-azure-traffic-manager.md)

