---
title: 'aaaAzure esempio DMZ: compilare una semplice rete Perimetrale con NSGs | Documenti Microsoft'
description: Creare una rete perimetrale con gruppi di sicurezza di rete
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 11c5c6026da30fbc9c5e585f5c16e2d411d6fd80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a>Esempio 1: Creare una rete perimetrale semplice usando gruppi di sicurezza di rete con un modello di Azure Resource Manager
[Restituire la pagina sicurezza limite Best Practices toohello][HOME]

> [!div class="op_single_selector"]
> * [Modello di Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classica: PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Questo esempio descrive come creare una rete perimetrale primitiva con quattro server Windows e gruppi di sicurezza di rete. In questo esempio viene descritto ciascun hello modello pertinenti sezioni tooprovide una comprensione più approfondita di ogni passaggio. È inoltre disponibile un tooprovide sezione Scenario traffico dettagliate approfondimenti sulla modalità di prosecuzione di traffico tramite i livelli di difesa hello DMZ hello. Infine, nella sezione dei riferimenti hello è toobuild di codice e le istruzioni modello completa hello questo ambiente tootest e sperimentare vari scenari. 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

![Rete perimetrale in ingresso con gruppo di sicurezza di rete][1]

## <a name="environment-description"></a>Descrizione dell'ambiente
In questo esempio una sottoscrizione contiene hello seguenti risorse:

* Un unico gruppo di risorse
* Una rete virtuale con due subnet: front-end e back-end
* Un gruppo di sicurezza di rete che viene applicato tooboth subnet
* Un server Windows che rappresenta un server Web applicazioni ("IIS01").
* Due server Windows che rappresentano i server applicazioni back-end ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01")
* Un indirizzo IP pubblico associato hello applicazione web server

Nella sezione dei riferimenti, hello è un modello di gestione risorse di Azure tooan collegamento che consente di creare ambiente hello descritta in questo esempio. Macchine virtuali hello di compilazione e le reti virtuali, anche se l'operazione eseguita dal modello di esempio hello, non sono descritti in dettaglio in questo documento. 

**toobuild questo ambiente** (istruzioni dettagliate sono nella sezione dei riferimenti hello di questo documento);

1. Distribuire hello modello di gestione risorse di Azure in: [modelli di avvio rapido di Azure][Template]
2. Installare l'applicazione di esempio hello in: [Script dell'applicazione di esempio][SampleApp]

>[!NOTE]
>server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella." Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end. In alternativa è possibile associare un indirizzo IP alla scheda di interfaccia di rete di ogni server per semplificare la connessione tramite RDP.
> 
>

Hello sezioni seguenti forniscono una descrizione dettagliata di hello il gruppo di sicurezza di rete e il funzionamento di questo esempio, illustrando le righe di chiave di hello il modello di gestione risorse di Azure.

## <a name="network-security-groups-nsg"></a>Gruppi di sicurezza di rete (NGS)
Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono caricate sei regole. 

>[!TIP]
>In genere, si deve creare regole "Consenti" specifiche prima e quindi hello ultima più generico "Deny" regole. Hello assegnata la priorità determina quali regole vengono valutate per prime. Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole. Possono essere applicate regole di gruppo in hello nella direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).
>
>

In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:

1. Il traffico DNS interno (porta 53) è consentito.
2. È consentito il traffico RDP (porta 3389) da hello Internet tooany VM
3. È consentito il traffico HTTP (porta 80) dal server di tooweb Internet hello (IIS01)
4. È consentito qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1
5. Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (entrambi subnet)
6. Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello subnet front-end hello negato

Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso dal server web toohello Internet hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata, ma poiché la regola 3 ha una priorità più alta solo esso viene applicato e regola 5 sarebbe non entrano in gioco. Richiesta HTTP hello sarebbe è pertanto a server web toohello. Se il traffico stesso cercava server DNS01 di hello tooreach, regola 5 (Nega) sarebbe hello prima tooapply hello il traffico e non sarebbe consentito toopass toohello server. Regola 6 (Nega) Blocca subnet front-end hello dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4), il set di regole protegge rete back-end hello nel caso in cui un'utente malintenzionato compromette hello applicazione web sul front-end hello autore dell'attacco hello sarebbe non dispongono di accesso toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).

Una regola in uscita predefinito che consente il traffico in uscita toohello internet. Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita. tooapply tootraffic criteri di sicurezza in entrambe le direzioni, Routing definito dall'utente è obbligatorio e viene esaminata in "Esempio 3" in hello [pagina migliori procedure consigliate di sicurezza limite][HOME].

Ogni regola viene illustrata in dettaglio nel modo seguente:

1. Una risorsa del gruppo di sicurezza di rete deve essere stata creata un'istanza toohold hello regole:

    ```JSON
    "resources": [
      {
        "apiVersion": "2015-05-01-preview",
        "type": "Microsoft.Network/networkSecurityGroups",
        "name": "[variables('NSGName')]",
        "location": "[resourceGroup().location]",
        "properties": { }
      }
    ]
    ``` 

2. prima regola di Hello in questo esempio consente il traffico DNS tra tutti i server DNS di toohello reti interne nella subnet back-end hello. regola di Hello include alcuni parametri importanti:
  * Questi tag sono identificatori forniti dal sistema che consentono di tooaddress un modo semplice una categoria di dimensioni maggiore di prefissi di indirizzo "destinationAddressPrefix" - regole di possono utilizzare un tipo speciale di prefisso dell'indirizzo denominato "Tag predefinito". Questa regola utilizza hello Tag predefinito "Internet" toosignify qualche indirizzo di fuori di hello rete virtuale. Altre etichette di prefisso sono VirtualNetwork e AzureLoadBalancer.
  * "Direction" indica la direzione del flusso di traffico a cui verrà applicata questa regola direzione Hello è dal punto di vista di hello di subnet hello o macchina virtuale (in base a cui è associato questo gruppo). In questo modo se direzione è "Inbound" e il traffico sta entrando in subnet hello, verrà applicata la regola hello e traffico lasciando subnet hello potrebbe non essere interessato da questa regola.
  * "Priority" imposta hello l'ordine in cui viene valutato un flusso di traffico. Hello hello numero hello superiore hello priorità inferiore. Quando il flusso di traffico specifico tooa si applica una regola, non vengono elaborate ulteriori regole. Pertanto se una regola con priorità 1 consente il traffico e una regola con priorità 2 impedisca il traffico, entrambe le regole si applicano tootraffic quindi sia possibile usare il traffico hello tooflow (poiché la regola 1 ha una priorità più alta da cui ha effetto e non altre regole sono state applicate).
  * "Access" indica se il traffico a cui si applica la regola viene bloccato ("Deny") o consentito ("Allow").

    ```JSON
    "properties": {
    "securityRules": [
      {
        "name": "enable_dns_rule",
        "properties": {
          "description": "Enable Internal DNS",
          "protocol": "*",
          "sourcePortRange": "*",
          "destinationPortRange": "53",
          "sourceAddressPrefix": "VirtualNetwork",
          "destinationAddressPrefix": "10.0.2.4",
          "access": "Allow",
          "priority": 100,
          "direction": "Inbound"
        }
      },
    ```

3. Questa regola consente di tooflow il traffico RDP da hello internet toohello la porta RDP in qualsiasi server in hello associato subnet. 

    ```JSON
    {
      "name": "enable_rdp_rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "*",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 110,
        "direction": "Inbound"
      }
    },
    ```

4. Questa regola consente di server web in ingresso internet traffico toohit hello. Questa regola non modifica il comportamento di routing hello. regola di Hello consente solo il traffico destinato IIS01 toopass. Pertanto se il traffico proveniente da Internet hello disponesse di server web hello come destinazione di questa regola consente e arrestare l'elaborazione di altre regole. (Regola hello priorità 140 tutte le altre traffico in ingresso internet è bloccato). Se si sta elaborando solo il traffico HTTP, questa regola può essere ulteriormente limitato tooonly Consenti destinazione la porta 80.

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet too[variables('VM01Name')]",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "10.0.1.5",
        "access": "Allow",
        "priority": 120,
        "direction": "Inbound"
        }
      },
    ```

5. Questa regola consente il traffico toopass dal server IIS01 hello toohello AppVM01 server, una regola successiva blocca tutto il traffico tooBackend altri server front-end. tooimprove questa regola, se la porta hello è noto che deve essere aggiunti. Ad esempio, se il server IIS hello sta impegnando solo SQL Server in AppVM01, hello intervallo di porte di destinazione deve essere modificato da "*" (Any) too1433 (porta SQL Buongiorno) consentendo in tal modo una superficie di attacco in ingresso più piccola in AppVM01 deve hello web applicazione dovesse essere compromessa.

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] too[variables('VM02Name')]",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "10.0.1.5",
        "destinationAddressPrefix": "10.0.2.5",
        "access": "Allow",
        "priority": 130,
        "direction": "Inbound"
      }
    },
     ```

6. Questa regola impedisce il traffico da hello internet tooany server hello rete. Con regole di hello priorità 110 e 120, effetto hello è tooallow solo internet traffico toohello firewall in entrata e le porte RDP nel server e blocca tutto il resto. Questa regola è "alternativo" regola tooblock tutti i flussi imprevisti.

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate hello [variables('VNetName')] VNet from hello Internet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "VirtualNetwork",
        "access": "Deny",
        "priority": 140,
        "direction": "Inbound"
      }
    },
     ```

7. regola finale Hello impedisca il traffico dalla subnet di back-end toohello subnet front-end hello. Poiché questa regola è una regola sola in ingresso, è consentito traffico inverso (da hello back-end toohello front-end).

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate hello [variables('Subnet1Name')] subnet from hello [variables('Subnet2Name')] subnet",
        "protocol": "*",
        "sourcePortRange": "*",
        "destinationPortRange": "*",
        "sourceAddressPrefix": "[variables('Subnet1Prefix')]",
        "destinationAddressPrefix": "[variables('Subnet2Prefix')]",
        "access": "Deny",
        "priority": 150,
        "direction": "Inbound"
      }
    }
    ```

## <a name="traffic-scenarios"></a>Scenari di traffico
#### <a name="allowed-internet-tooweb-server"></a>(*Consentito*) server tooweb Internet
1. Un utente internet richiede una pagina HTTP da indirizzo IP pubblico hello di hello che NIC associato hello IIS01 NIC
2. indirizzo IP pubblico Hello passa toohello il traffico tra reti virtuali verso IIS01 (server web hello)
3. La subnet front-end inizia l'elaborazione delle regole in ingresso:
  1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
  2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
  3. Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto
4. Traffico raggiunge l'indirizzo IP interno del server web hello IIS01 (10.0.1.5)
5. Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello
6. Iis01 richiede SQL Server hello su AppVM01 per informazioni
7. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
8. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
  1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
  2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
  3. GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola
  4. Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto
9. AppVM01 riceve hello Query SQL e risponde
10. Poiché non esistono regole in uscita nella subnet back-end hello, risposta hello è consentito
11. La subnet front-end inizia l'elaborazione delle regole in ingresso:
  1. Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile
  2. regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.
12. server IIS Hello riceve risposta SQL hello e completa di risposta HTTP hello e invia toohello richiedente
13. Poiché non esistono regole in uscita nella subnet front-end hello, risposta hello è consentito e hello utente Internet riceve hello web pagina richiesta.

#### <a name="allowed-rdp-tooiis-server"></a>(*Consentito*) server tooIIS RDP
1. Un amministratore del Server su internet richiede un tooIIS01 sessione RDP in indirizzo IP pubblico hello di hello che NIC associato hello NIC IIS01 (questo indirizzo IP pubblico è disponibile tramite hello portale o PowerShell)
2. indirizzo IP pubblico Hello passa toohello il traffico tra reti virtuali verso IIS01 (server web hello)
3. La subnet front-end inizia l'elaborazione delle regole in ingresso:
  1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
  2. Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
4. Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.
5. La sessione RDP è abilitata.
6. Iis01 chiesta la password e il nome utente hello

>[!NOTE]
>server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella." Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Consentito*) Ricerca DNS del server Web sul server DNS
1. Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.
2. Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01
3. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
4. La subnet back-end inizia l'elaborazione delle regole in ingresso:
  * Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
5. Server DNS riceve una richiesta di hello
6. Server DNS non dispone di indirizzo hello memorizzati nella cache e richiede un server radice DNS su hello internet
7. Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.
8. Server DNS Internet risponde, poiché questa sessione è stata avviata internamente, la risposta hello è consentita
9. Server DNS memorizza nella cache la risposta hello e risponde toohello richiesta iniziale indietro tooIIS01
10. Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.
11. La subnet front-end inizia l'elaborazione delle regole in ingresso:
  1. Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile
  2. regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito
12. Iis01 riceve risposta hello da DNS01

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Consentito*) Il server Web richiede l'accesso a un file in AppVM01
1. IIS01 richiede un file in AppVM01.
2. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
3. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
  1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
  2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
  3. GRUPPO regola 3 (tooIIS01 Internet) non è applicabile, spostare toonext regola
  4. Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto
4. AppVM01 riceve la richiesta di hello e risponde con il file (presupponendo che l'accesso è autorizzato)
5. Poiché non esistono regole in uscita nella subnet back-end hello, risposta hello è consentito
6. La subnet front-end inizia l'elaborazione delle regole in ingresso:
  1. Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile
  2. regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.
7. server IIS Hello riceve file hello

#### <a name="denied-rdp-toobackend"></a>(*Negato*) toobackend RDP
1. Un utente internet tenta tooRDP tooserver AppVM01
2. Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello
3. Se tuttavia per qualunque motivo è stato abilitato un indirizzo IP pubblico, la regola del gruppo di sicurezza di rete 2 (RDP) consentirà questo traffico.

>[!NOTE]
>server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella." Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.
>
>

#### <a name="denied-web-toobackend-server"></a>(*Negato*) server toobackend Web
1. Un utente internet tenta un file in AppVM01 tooaccess
2. Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello
3. Se un indirizzo IP pubblico è stato abilitato per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Negato*) Ricerca DNS Web sul server DNS
1. Un utente internet tenta toolook di un record DNS interno nella DNS01
2. Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello
3. Se un indirizzo IP pubblico è stato abilitato per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico (Nota: che regola 1 (DNS) potrebbero non applicarsi perché hello richiede l'indirizzo di origine è hello internet e regola 1 si applica solo a toohello rete locale virtuale come origine di hello)

#### <a name="denied-sql-access-on-hello-web-server"></a>(*Negato*) l'accesso a SQL Server web hello
1. Un utente su Internet richiede dati SQL da IIS01
2. Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello
3. Se un indirizzo IP pubblico è stato abilitato per qualche motivo, subnet front-end hello inizia l'elaborazione della regola in ingresso:
  1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
  2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
  3. Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto
4. Traffico raggiunge l'indirizzo IP interno di hello IIS01 (10.0.1.5)
5. Non è in ascolto sulla porta 1433, che non è più richiesta toohello risposta iis01

## <a name="conclusion"></a>Conclusioni
Questo esempio è un modo semplice e relativamente semplice isolare subnet back-end hello dal traffico in ingresso.

Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].

## <a name="references"></a>Riferimenti
### <a name="azure-resource-manager-template"></a>Modello di Azure Resource Manager
In questo esempio viene utilizzato un modello di gestione risorse di Azure predefinito in un repository GitHub gestito da Microsoft e aprire toohello community. Questo modello può essere distribuito direttamente da GitHub, o scaricati e modificati toofit le proprie esigenze. 

modello principale Hello è nel file hello denominato "azuredeploy.json". Questo modello può essere inviato tramite PowerShell o CLI (con file associato "azuredeploy.parameters.json" hello) toodeploy questo modello. È possibile individuare hello più semplice consiste nel toouse hello pulsante "Distribuisci tooAzure" nella pagina README.md hello in GitHub.

modello di hello toodeploy che si basa questo esempio da GitHub e hello portale di Azure, seguire questi passaggi:

1. Da un browser, passare toohello [modello][Template]
2. Fare clic su pulsante "Distribuisci tooAzure" hello (o toosee di pulsante "Visualizza" hello una rappresentazione grafica del modello)
3. Immettere hello Account di archiviazione, nome utente e Password nel Pannello di hello parametri, quindi fare clic su **OK**
5. Creare un gruppo di risorse per questa distribuzione. È possibile usarne uno esistente, ma è consigliabile creare una nuova istanza per risultati ottimali.
6. Se necessario, modificare le impostazioni di sottoscrizione e posizione hello per la rete virtuale.
7. Fare clic su **esaminare le note legali**, leggere le condizioni di hello e fare clic su **acquisto** tooagree.
8. Fare clic su **crea** distribuzione hello toobegin del modello.
9. Al termine della distribuzione hello correttamente, è possibile passare toohello che gruppo di risorse creato per le risorse di hello toosee questa distribuzione configurata all'interno.

>[!NOTE]
>Questo modello consente RDP toohello IIS01 solo server (ricerca hello, indirizzo IP pubblico per IIS01 su hello portale). server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella." Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.
>
>

tooremove questa distribuzione, hello di eliminazione gruppo di risorse e tutte le risorse figlio saranno eliminate.

#### <a name="sample-application-scripts"></a>Script di applicazione di esempio
Una volta modello hello viene eseguito correttamente, è possibile impostare server web hello e server di applicazioni con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale. tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]

## <a name="next-steps"></a>Passaggi successivi

* Distribuire questo esempio
* Compilare l'applicazione di esempio hello
* Testare diversi flussi di traffico attraverso la rete perimetrale

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md