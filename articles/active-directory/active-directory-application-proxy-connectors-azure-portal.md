---
title: le applicazioni aaaPublishing su reti separate e percorsi con gruppi di connettori proxy di App di Azure AD | Documenti Microsoft
description: Include informazioni su come toocreate e gestire gruppi di connettori Proxy di applicazione di Azure AD.
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: H1Hack27Feb2017; it-pro
ms.openlocfilehash: 8c9a84b365eab28eaaeb343d4d1e2e6990537fec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="publish-applications-on-separate-networks-and-locations-using-connector-groups"></a>Pubblicare applicazioni in reti e posizioni separate tramite i gruppi di connettori
> [!div class="op_single_selector"]
> * [Portale di Azure](active-directory-application-proxy-connectors-azure-portal.md)
> * [portale di Azure classico](active-directory-application-proxy-connectors.md)
>

Il proxy di applicazione di Azure AD viene usato per un numero crescente di scenari e applicazioni dei clienti. Per questo motivo, il proxy di applicazione è stato reso ancora più flessibile grazie all'abilitazione di altre topologie. È possibile creare gruppi di connettori Proxy di applicazione in modo che è possibile assegnare connettori specifici tooserve specifiche applicazioni. Questa funzionalità offre ulteriori toooptimize di controllo e le modalità la distribuzione di Proxy di applicazione. 

Ogni connettore Proxy dell'applicazione viene assegnato il gruppo di connettori tooa. Tutti hello connettori appartenenti toohello stesso gruppo di connettori fungono da un'unità separata per la disponibilità elevata e bilanciamento del carico. Tutti i connettori appartengano il gruppo di connettori tooa. Se non si creano i gruppi, tutti i connettori vengono inclusi in un gruppo predefinito. L'amministratore può creare nuovi gruppi e assegnare toothem connettori nel portale di Azure hello. 

Tutte le applicazioni vengono assegnate tooa gruppo di connettori. Se non è possibile creare gruppi, tutte le applicazioni vengono assegnate gruppo predefinito tooa. Tuttavia, se i connettori per organizzare in gruppi, è possibile impostare ogni toowork applicazione con un gruppo di connettori specifici. In questo caso, solo i connettori di hello in tale gruppo hanno un'applicazione hello su richiesta. Questa funzionalità è utile se le applicazioni sono ospitate in posizioni diverse. È possibile creare gruppi di connettori in base alla posizione, in modo che le applicazioni sono sempre servite dai connettori che sono fisicamente Chiudi toothem.

>[!TIP] 
>Se si dispone di una distribuzione di Proxy dell'applicazione di grandi dimensioni, non assegnare qualsiasi gruppo di applicazioni toohello predefinito connettore. In questo modo, nuovi connettori non ricevano traffico in tempo reale fino a quando non si assegnarli gruppo connettore active tooan. Questa configurazione consente inoltre connettori tooput in modalità inattiva spostandoli gruppo predefinito toohello indietro, in modo che sia possibile eseguire la manutenzione senza conseguenze per gli utenti.

## <a name="prerequisites"></a>Prerequisiti
toogroup connettori correnti, si dispone di toomake che si [installato più connettori](active-directory-application-proxy-enable.md). Quando si installa un nuovo connettore, viene automaticamente aggiunto hello **predefinito** gruppo di connettori.

## <a name="create-connector-groups"></a>Creare gruppi di connettori
Utilizzare questi passaggi toocreate tutti i gruppi di connettori che si desidera. 

1. Accedi toohello [portale di Azure](https://portal.azure.com).
1. Selezionare **Azure Active Directory** > **Applicazioni aziendali** > **Proxy dell'applicazione**.
2. Selezionare **Nuovo gruppo di connettori**. viene visualizzato il pannello di nuovo gruppo di connettori Hello.

   ![Selezionare il nuovo gruppo di connettori](./media/active-directory-application-proxy-connectors-azure-portal/new-group.png)

3. Assegnare un nome del nuovo gruppo di connettore, quindi utilizzare tooselect di menu a discesa hello cui appartengono i connettori di questo gruppo.
4. Selezionare **Salva**.

## <a name="assign-applications-tooyour-connector-groups"></a>Assegnare gruppi di connettori tooyour le applicazioni
Usare questi passaggi per ogni applicazione pubblicata con il proxy di applicazione. È possibile assegnare un gruppo di applicazioni tooa connettore quando prima pubblicazione o ogni volta che desidera, è possibile utilizzare l'assegnazione hello toochange questi passaggi.   

1. Dal dashboard di gestione di hello per le directory, selezionare **applicazioni aziendali** > **tutte le applicazioni** > hello applicazione del gruppo di connettori tooa tooassign >  **Proxy dell'applicazione**.
2. Hello utilizzare **connettore gruppo** gruppo hello tooselect menu a discesa desiderato toouse applicazione hello.
3. Selezionare **salvare** modifica hello tooapply.

## <a name="use-cases-for-connector-groups"></a>Casi d'uso per gruppi di connettori 

I gruppi di connettori sono utili in varie situazioni, ad esempio:

### <a name="sites-with-multiple-interconnected-datacenters"></a>Siti con più data center interconnessi

Molte organizzazioni hanno diversi data center interconnessi. In questo caso, si desidera tookeep come quantità di traffico in Data Center di hello possibile poiché i collegamenti tra Data Center sono lente e costoso. È possibile distribuire i connettori in ogni Data Center tooserve solo hello le applicazioni che risiedono all'interno di hello datacenter. Questo approccio riduce al minimo i collegamenti tra Data Center e offre un'esperienza completamente trasparente agli utenti di tooyour.

### <a name="applications-installed-on-isolated-networks"></a>Applicazioni installate in reti isolate

Le applicazioni possono essere ospitate in reti che non fanno parte della rete aziendale principale hello. È possibile utilizzare i connettori di connettore gruppi tooinstall dedicato nella rete di toohello reti isolate tooalso isolare le applicazioni. Questo accade in genere quando un fornitore di terze parti gestisce un'applicazione specifica per l'organizzazione. 

Gruppi di connettori consentono si tooinstall dedicato connettori per le reti a cui pubblicano solo determinate applicazioni, rendendo più semplice e più sicuro di gestione delle applicazioni toooutsource toothird fornitori.

### <a name="applications-installed-on-iaas"></a>Applicazioni installate in IaaS 

Per le applicazioni installate in IaaS per l'accesso cloud, i gruppi di connettori forniscono un servizio toosecure hello accesso tooall hello le applicazioni comuni. Gruppi di connettori non creare una dipendenza aggiuntiva nella rete aziendale, o frammento esperienza app hello. I connettori possono essere installati in ogni data center nel cloud e gestire solo le applicazioni che si trovano nella rete. È possibile installare i diversi connettori tooachieve la disponibilità elevata.

Richiedere ad esempio un'organizzazione che dispone di più macchine virtuali connesse a rete virtuale IaaS ospitate proprio tootheir. tooallow dipendenti toouse queste applicazioni, queste reti private sono connessi toohello rete aziendale tramite VPN site-to-site. Questa soluzione offre un'esperienza ottimale ai dipendenti a livello locale. Tuttavia, potrebbe non essere ideale per i dipendenti remoti, perché richiede l'accesso tooroute infrastruttura locale aggiuntivi, come è possibile visualizzare nel diagramma hello riportato di seguito:

![Rete IaaS di Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-iaas-network.png)
  
Con i gruppi di connettori Proxy di applicazione AD Azure, è possibile abilitare un comune servizio toosecure hello accesso tooall le applicazioni senza creare una dipendenza aggiuntiva nella rete aziendale:

![Più fornitori cloud IaaS per Azure AD](./media/application-proxy-publish-apps-separate-networks/application-proxy-multiple-cloud-vendors.png)

### <a name="multi-forest--different-connector-groups-for-each-forest"></a>Scenario a più foreste: gruppi di connettori diversi per ogni foresta

La maggior parte dei clienti che hanno distribuito il proxy di applicazione usa le funzionalità Single Sign-On (SSO) eseguendo la delega vincolata Kerberos (KCD). tooachieve questo macchine necessità toobe tooa aggiunti a un dominio del connettore hello che può delegare agli utenti di hello verso un'applicazione hello. La delega vincolata Kerberos supporta le funzionalità tra foreste. Tuttavia, per le aziende che hanno ambienti a più foreste distinti senza una relazione di trust tra di essi, è possibile usare un solo connettore per tutte le foreste. 

In questo caso, possono essere distribuiti connettori specifici per ogni foresta e applicazioni tooserve set che sono stati pubblicati tooserve hello solo gli utenti di tale foresta specifico. Ogni gruppo di connettori rappresenta una foresta diversa. Mentre tenant hello e la maggior parte dell'esperienza di hello unificata per tutte le foreste, gli utenti possono essere assegnati tootheir applicazioni di foresta usando gruppi di Azure AD.
 
### <a name="disaster-recovery-sites"></a>Siti di ripristino di emergenza

Sono disponibili due diversi approcci ai siti di ripristino di emergenza, a seconda della modalità di implementazione dei siti:

* Se il sito di ripristino di emergenza viene compilato in modalità attivo-attivo dove esattamente come sito principale hello ed è hello stessa rete e le impostazioni di Active Directory, è possibile creare i connettori di hello nel sito di ripristino di emergenza hello in hello allo stesso gruppo di connettore del sito principale hello. Consente di abilitare i failover toodetect di Azure AD a.
* Se il sito di ripristino di emergenza è separato dal sito principale hello, è possibile creare un gruppo di connettori diversi nel sito di ripristino di emergenza hello e 1) necessario alle applicazioni di backup oppure 2) manualmente deviare gruppo connettore toohello ripristino di emergenza hello esistente dell'applicazione in base alle esigenze.
 
### <a name="serve-multiple-companies-from-a-single-tenant"></a>Gestire più aziende da un singolo tenant

Esistono molti modi diversi servizi per più società correlati a tooimplement un modello in cui un unico provider di servizi, distribuisce e gestisce AD Azure. Gruppi di connettori Guida salve separare connettori hello e le applicazioni in gruppi diversi. In primo luogo, è adatta per le piccole aziende, è toohave un singolo tenant di Azure AD, mentre le aziende hello hanno le proprie reti e il nome di dominio. Questo vale anche per scenari di fusione e acquisizione e situazioni in cui un singolo reparto IT gestisce diverse aziende per motivi legali o economici. 

## <a name="sample-configurations"></a>Configurazioni di esempio

Alcuni esempi che è possibile implementare, includono i seguenti gruppi di connettori hello.
 
### <a name="default-configuration--no-use-for-connector-groups"></a>Configurazione predefinita senza gruppi di connettori

Se non si usano gruppi di connettori, la configurazione ha un aspetto simile al seguente:

![Azure AD senza gruppi di connettori](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-1.png)
 
Questa configurazione è sufficiente per distribuzioni di piccole dimensioni e test. È adatta anche a organizzazioni con una topologia di rete flat.
 
### <a name="default-configuration-and-an-isolated-network"></a>Configurazione predefinita con una rete isolata

Questa configurazione è un'evoluzione del hello predefinito, in cui è un'app specifica che viene eseguito in una rete isolata, ad esempio la rete virtuale IaaS: 

![Azure AD senza gruppi di connettori](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-2.png)
 
### <a name="recommended-configuration--several-specific-groups-and-a-default-group-for-idle"></a>Configurazione consigliata con diversi gruppi specifici e un gruppo predefinito inattivo

configurazione consigliata per le organizzazioni di grandi e complesse Hello è toohave hello predefinito connettore gruppo come gruppo che non possa essere usata tutte le applicazioni e viene utilizzato per i connettori di inattività o appena installati. Tutte le applicazioni vengono gestite tramite gruppi di connettori personalizzati. In questo modo tutta la complessità hello degli scenari di hello descritto in precedenza.

Nel seguente esempio hello hello società dispone di due Data Center, A e B, con due connettori da ogni sito. In ognuno dei siti vengono eseguite applicazioni diverse. 

![Azure AD senza gruppi di connettori](./media/application-proxy-publish-apps-separate-networks/application-proxy-sample-config-3.png)
 
## <a name="next-steps"></a>Passaggi successivi

* [Comprendere i connettori del proxy applicazione di Azure AD](application-proxy-understand-connectors.md)
* [Abilitare l'accesso Single Sign-On](application-proxy-sso-overview.md)


