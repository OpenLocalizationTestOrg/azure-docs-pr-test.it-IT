---
title: "distribuzione di ADFS aaaHigh disponibilità geografici tra Active Directory in Azure con Azure Traffic Manager | Documenti Microsoft"
description: "In questo documento si apprenderà come toodeploy AD ADFS in Azure ad alta disponibilità."
keywords: "ADFS con gestione traffico di Azure, adfs con Azure Traffic Manager, geografica, Data Center multi, centri dati geografici, Data Center geografico di più, distribuire ADFS in azure, distribuire adfs di azure, azure adfs, ADFS di azure, la distribuzione di adfs, distribuire ADFS, adfs in azure, distribuire adfs in azure, distribuire ADFS in azure, azure ad FS, introduzione tooAD ADFS, Azure, ADFS in Azure iaas, ADFS, sposta tooazure adfs"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Distribuzione di AD FS a disponibilità elevata tra aree geografiche in Azure con Gestione traffico di Azure
[Distribuzione di ADFS in Azure](active-directory-aadconnect-azure-adfs.md) fornisce istruzioni dettagliate toohow è possibile distribuire un'infrastruttura ADFS semplice per l'organizzazione in Azure. In questo articolo viene descritta la procedura successiva hello toocreate un cross-geografica distribuzione di ADFS in Azure tramite [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md). Traffic Manager di Azure consente di creare un geograficamente distribuito un'elevata disponibilità e l'infrastruttura di ADFS ad alte prestazioni per l'organizzazione, rendendo l'uso dell'intervallo di metodi di routing deve toosuit disponibili diversi dall'infrastruttura di hello.

Un'infrastruttura AD FS tra aree geografiche a disponibilità elevata offre i vantaggi seguenti:

* **Eliminazione di un punto singolo di errore:** con funzionalità di failover di Traffic Manager di Azure, è possibile ottenere un'infrastruttura di ADFS a disponibilità elevata, anche quando uno dei centri dati hello in una parte del mondo hello diventa inattivo
* **Prestazioni migliorate:** è possibile utilizzare hello suggerito distribuzione in questo articolo di tooprovide un'infrastruttura di ADFS ad alte prestazioni che consente agli utenti di eseguire l'autenticazione a più velocemente. 

## <a name="design-principles"></a>Principi di progettazione
![Progettazione complessiva](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

principi di progettazione di base Hello saranno uguali a quelli elencati in principi di progettazione nell'articolo hello distribuzione di ADFS in Azure. diagramma di Hello precedente mostra una semplice estensione dell'area geografica tooanother distribuzione di base di hello. Ecco alcuni tooconsider punti quando si estende l'area geografica toonew di distribuzione

* **Rete virtuale:** è necessario creare una nuova rete virtuale nella regione geografica hello desiderato infrastruttura ADFS toodeploy AD altri. Nel diagramma hello precedente vengono visualizzati tra reti VIRTUALI Geo1 e rete virtuale Geo2 come hello due reti virtuali in ogni area geografica.
* **Controller di dominio e server AD FS in una nuova rete virtuale geografiche:** toodeploy i controller di dominio nella nuova area geografica di hello è consigliabile che i server ADFS hello nella nuova area hello toocontact un controller di dominio in un'altra misura rete di stoccaggio toocomplete un'autenticazione e migliorando in tal modo le prestazioni di hello.
* **Account di archiviazione:** gli account di archiviazione sono associati a un'area. Poiché si distribuiscono macchine in una nuova area geografica, sarà necessario toocreate nuovi account di archiviazione toobe utilizzata nell'area di hello.  
* **Gruppi di sicurezza di rete:** come gli account di archiviazione, i gruppi di sicurezza di rete creati in un'area non possono essere usati in un'altra area geografica. Pertanto, sarà necessario toocreate nuova rete sicurezza gruppi simili toothose nella prima area geografica di hello per INT e DMZ subnet nella nuova area geografica di hello.
* **Le etichette di DNS per gli indirizzi IP pubblici:** Traffic Manager di Azure può fare riferimento a tooendpoints solo tramite le etichette DNS. Pertanto, sono necessari toocreate DNS etichette per gli indirizzi IP pubblici degli hello esterno bilanciamenti del carico.
* **Gestione traffico di Azure:** Traffic Manager di Microsoft Azure consente la distribuzione di hello toocontrol utente traffico tooyour di endpoint del servizio in esecuzione in diversi Data Center di tutto il mondo hello. Traffic Manager di Azure opera a livello DNS hello. Usa DNS risposte toodirect dell'utente finale traffico distributed tooglobally endpoint. I client quindi connettersi direttamente toothose endpoint. Con diverse opzioni di routine di prestazioni, Weighted e priorità, è possibile scegliere facilmente di instradamento hello più adattato alle esigenze dell'organizzazione. 
* **V-net tooV net connettività tra due aree:** toohave connettività tra reti virtuali hello non è necessario se stesso. Poiché ogni rete virtuale dispone di accesso toodomain controller e dispone di server AD FS e WAP in sé, possono lavorare senza qualsiasi connessione tra reti virtuali di hello in aree diverse. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Passaggi toointegrate Traffic Manager di Azure
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Distribuzione di ADFS nella nuova area geografica di hello
Seguire i passaggi di hello e linee guida fornite in [distribuzione di ADFS in Azure](active-directory-aadconnect-azure-adfs.md) toodeploy hello stessa topologia nella nuova area geografica di hello.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Etichette DNS per gli indirizzi IP pubblici di hello bilanciamenti del carico con connessione Internet (pubblica)
Come indicato in precedenza, hello Azure Traffic Manager può fare riferimento solo le etichette tooDNS come endpoint e pertanto è importante toocreate etichette DNS per gli indirizzi IP pubblici degli hello esterno bilanciamenti del carico. Seguente schermata mostra come è possibile configurare l'etichetta DNS per l'indirizzo IP pubblico hello. 

![Etichetta DNS](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Distribuzione di Gestione traffico di Azure
Eseguire operazioni di hello seguenti toocreate un profilo di gestione traffico. Per ulteriori informazioni, è anche possibile fare riferimento troppo[gestire un profilo di Traffic Manager di Azure](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Creare un profilo di Gestione traffico:** assegnare un nome univoco al profilo di Gestione traffico. Questo nome di profilo hello fa parte del nome DNS hello e funge da un prefisso per l'etichetta del nome di dominio gestione traffico hello. nome Hello / too.trafficmanager.net toocreate un'etichetta DNS viene aggiunto il prefisso per il profilo di gestione. Hello schermata riportata di seguito viene illustrato come gestione traffico hello prefisso DNS viene impostata come mysts e l'etichetta DNS risulta sarà mysts.trafficmanager.net. 
   
    ![Creazione del profilo di Gestione traffico](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Metodo di routing del traffico:** in Gestione traffico sono disponibili tre opzioni di routing del traffico:
   
   * Priorità 
   * Prestazioni
   * Ponderato
     
     **Prestazioni** hello consiglia di infrastruttura di opzione tooachieve ad alte AD FS. È tuttavia possibile scegliere il metodo di routing più adatto alle proprie esigenze di distribuzione. funzionalità di Hello AD FS non è interessata dall'opzione di routing hello selezionato. Per altre informazioni, vedere [Metodi di routing del traffico di Gestione traffico](../traffic-manager/traffic-manager-routing-methods.md) . In hello schermata di esempio sopra riportato è possibile vedere hello **prestazioni** metodo selezionato.
3. **Configurare gli endpoint:** nella pagina di gestione traffico hello, fare clic sull'endpoint, quindi scegliere Aggiungi. Verrà aperto un'Aggiungi endpoint pagina simile toohello schermata riportata di seguito
   
   ![Configurare gli endpoint](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Per i diversi input hello, attenersi alla linea guida hello riportato di seguito:
   
   **Tipo:** selezionare l'endpoint di Azure, come abbiamo verrà verso tooan Azure indirizzo IP pubblico.
   
   **Nome:** creare un nome che si desidera tooassociate con endpoint hello. Questo non è un nome DNS hello e non è rilevante per i record DNS.
   
   **Tipo di risorsa di destinazione:** indirizzo IP pubblico selezionare come proprietà di toothis valore hello. 
   
   **Risorsa di destinazione:** questa query fornirà toochoose un'opzione da etichette DNS diverse hello è disponibile nella sottoscrizione. Scegliere hello che DNS etichetta endpoint toohello corrispondente che si sta configurando.
   
   Aggiungere endpoint per ogni area geografica che si desideri hello Azure Traffic Manager tooroute il traffico.
   Per ulteriori informazioni e procedure dettagliate su come tooadd / configurare gli endpoint in Gestione traffico, consultare troppo[aggiungere, disabilitare, abilitare o eliminare endpoint](../traffic-manager/traffic-manager-endpoints.md)
4. **Configurare il probe:** nella pagina di gestione traffico hello, fare clic su configurazione. Nella pagina di configurazione hello, è necessario toochange hello monitoraggio impostazioni tooprobe alla porta HTTP 80 e percorso relativo /adfs/probe
   
    ![Configurare il probe](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Verificare che lo stato di hello degli endpoint hello sia ONLINE una volta completata la configurazione hello**. Se tutti gli endpoint sono in stato 'danneggiato', gestione traffico di Azure eseguirà un migliore traffico hello tooroute tentativo presupponendo che hello diagnostica non è corretta e che tutti gli endpoint sono raggiungibili.
   > 
   > 
5. **Modifica di record DNS per gestione traffico di Azure:** il servizio federativo deve essere un nome DNS di Azure Traffic Manager di toohello CNAME. Creare un record CNAME hello record DNS pubblici in modo da chi sta tentando di servizio federativo di hello tooreach raggiunga effettivamente hello Azure Traffic Manager.
   
    Ad esempio, toopoint hello federation service fs.fabidentity.com toohello Traffic Manager, sarà necessario tooupdate il hello toobe record di risorse DNS seguenti:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Routing hello e AD FS sign-in di test
### <a name="routing-test"></a>Test di routing
Un test di base per il routing hello sarebbe tootry ping hello federazione nome DNS del servizio da un computer in ogni area geografica. In base al metodo di routing hello scelto, endpoint hello che effettivamente ping verranno riflesse nella visualizzazione di ping hello. Ad esempio, se si seleziona prestazioni hello routing, quindi l'endpoint di hello più vicino al toohello area del client hello verrà raggiunto. Di seguito è snapshot hello di due ping dai computer client di area geografica diversa due, uno in area asiatico e uno negli Stati Uniti occidentali. 

![Test di routing](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Test dell'accesso ad AD FS
tootest modo più semplice di Hello AD FS è la pagina IdpInitiatedSignon.aspx hello. In ordine toobe in grado di toodo che, è necessario tooenable hello IdpInitiatedSignOn sulle proprietà hello AD FS. Eseguire operazioni di hello seguenti tooverify il programma di installazione di ADFS

1. Esecuzione hello di sotto di cmdlet nel server di hello AD FS, tramite PowerShell, tooset è tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true
2. Da qualsiasi computer esterno accedere a https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Verrà visualizzata la pagina hello ADFS come il seguente:
   
    ![Test AD FS - richiesta di autenticazione](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    Dopo l'accesso verrà visualizzato un messaggio di completamento dell'operazione come il seguente:
   
    ![Test AD FS - autenticazione completata](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Collegamenti correlati
* [Distribuzione di AD FS in Azure](active-directory-aadconnect-azure-adfs.md)
* [Gestione traffico di Azure](../traffic-manager/traffic-manager-overview.md)
* [Metodi di routing di Gestione traffico+](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Passaggi successivi
* [Gestire un profilo di Gestione traffico di Azure](../traffic-manager/traffic-manager-manage-profiles.md)
* [Aggiungere, disabilitare, abilitare o eliminare gli endpoint](../traffic-manager/traffic-manager-endpoints.md) 

