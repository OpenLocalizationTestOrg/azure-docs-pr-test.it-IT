---
title: 'Esempio: aaaDMZ applicazioni tooprotect una rete Perimetrale con un Firewall e NSGs | Documenti Microsoft'
description: Creare una rete perimetrale con un firewall e gruppi di sicurezza di rete
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: c78491c7-54ac-4469-851c-b35bfed0f528
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: 18f116dc3897567bff14a509ae8c13f449182bfb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-2--build-a-dmz-tooprotect-applications-with-a-firewall-and-nsgs"></a>Esempio 2 – applicazioni tooprotect una rete Perimetrale con un Firewall e NSGs
[Restituire la pagina sicurezza limite Best Practices toohello][HOME]

Questo esempio illustra come creare una rete perimetrale con un firewall, quattro server Windows e gruppi di sicurezza di rete. Ogni tooprovide comandi rilevanti hello in modo dettagliato anche una comprensione più approfondita di ogni passaggio. È inoltre disponibile un Scenario di traffico sezione tooprovide un'analisi approfondita dettagliate come traffico procede attraverso i livelli di difesa hello hello rete Perimetrale. Infine, nella sezione dei riferimenti hello è codice completo hello e istruzione toobuild questo ambiente tootest e sperimentare vari scenari. 

![Rete Perimetrale in ingresso con NVA e gruppo][1]

## <a name="environment-description"></a>Descrizione dell'ambiente
In questo esempio è associata una sottoscrizione che contiene la seguente sintassi hello:

* Due servizi cloud, "FrontEnd001" e "BackEnd001"
* Una rete virtuale, "CorpNetwork", con due subnet: "FrontEnd" e "BackEnd"
* Un unico gruppo di sicurezza di rete che viene applicato tooboth subnet
* Un accessorio virtuale di rete, in questo esempio un Firewall, NextGen Barracuda connesso subnet front-end toohello
* Un server Windows che rappresenta un server Web applicazioni ("IIS01").
* Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01")

> [!NOTE]
> Sebbene questo esempio viene utilizzato un NextGen Firewall Barracuda, molti dei diversi dispositivi virtuali di rete può essere usati per questo esempio hello.
> 
> 

Nella sezione dei riferimenti hello sotto è uno script di PowerShell che compilerà la maggior parte dell'ambiente hello descritto in precedenza. Macchine virtuali hello di compilazione e le reti virtuali, anche se vengono eseguite dallo script di esempio hello, non sono descritti in dettaglio in questo documento.

ambiente di hello toobuild:

1. Salvare file xml configurazione rete hello inclusi nella sezione dei riferimenti hello (aggiornata con i nomi, la posizione e scenario hello dato toomatch di indirizzi IP)
2. Le variabili utente di aggiornamento hello nello script di hello script toomatch hello ambiente hello è toobe eseguite (sottoscrizioni, nomi di servizio e così via)
3. Eseguire script hello in PowerShell

**Nota**: area hello indicato nell'hello script di PowerShell deve corrispondere area hello indicato nel file xml di configurazione rete hello.

Una volta hello script viene eseguito correttamente può essere prelevato hello post-script come segue:

1. Impostare le regole firewall hello, questa attività viene descritta in hello sezione seguente: le regole del Firewall.
2. Facoltativamente, nella sezione dei riferimenti hello sono due script tooset hello web server e il server di app con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.

la sezione successiva di Hello spiega la maggior parte delle hello script istruzioni relativo tooNetwork gruppi di sicurezza.

## <a name="network-security-groups-nsg"></a>Gruppi di sicurezza di rete (NGS)
Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono poi caricate sei regole. 

> [!TIP]
> In genere, si deve creare regole "Consenti" specifiche prima e quindi hello ultima più generico "Deny" regole. Hello assegnata la priorità determina quali regole vengono valutate per prime. Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole. Possono essere applicate regole di gruppo in hello nella direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).
> 
> 

In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:

1. Il traffico DNS interno (porta 53) è consentito.
2. È consentito il traffico RDP (porta 3389) da hello Internet tooany VM
3. È consentito il traffico HTTP (porta 80) da hello Internet toohello NVA (firewall)
4. È consentito qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1
5. Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (entrambi subnet)
6. Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello subnet front-end hello negato

Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso dal server web toohello Internet hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata, ma poiché la regola 3 ha una priorità più alta solo esso viene applicato e regola 5 sarebbe non entrano in gioco. In questo modo la richiesta HTTP hello sia possibile usare toohello firewall. Se il traffico stesso cercava server DNS01 di hello tooreach, regola 5 (Nega) sarebbe hello prima tooapply hello il traffico e non sarebbe consentito toopass toohello server. Regola 6 (Nega) blocchi hello subnet front-end dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4), consente di proteggere rete back-end hello nel caso in cui un'utente malintenzionato compromette hello applicazione web sul front-end hello autore dell'attacco hello avrebbe accesso limitato toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).

Una regola in uscita predefinito che consente il traffico in uscita toohello internet. Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita. toolock verso il basso il traffico in entrambe le direzioni, Routing definito dall'utente è obbligatorio, questo viene esaminato in un esempio di diversi che è possibile trovare in hello [documento limite di sicurezza principale][HOME].

Hello sopra descritto NSG le regole sono molto simili toohello NSG in [esempio 1: creare una rete Perimetrale semplice con NSGs][Example1]. Esaminare hello NSG descrizione in tale documento per ogni regola di gruppo e gli attributi di un'analisi approfondita.

## <a name="firewall-rules"></a>Regole del firewall
Un client di gestione sarà necessario toobe installato su un firewall di hello toomanage PC e creare configurazioni di hello necessarie. Vedere fornitore documentazione fornita dal firewall (o altri NVA) hello in modo toomanage hello dispositivo. resto Hello di questa sezione descrivono la configurazione hello di firewall hello stesso, tramite il client Gestione fornitori hello (ossia, non hello portale di Azure o PowerShell).

Istruzioni per il download di client e connessione toohello Barracuda utilizzato in questo esempio sono disponibili qui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)

Regole di inoltro sul firewall hello, saranno necessario toobe creato. Poiché in questo esempio viene distribuito solo il traffico in entrata toohello firewall internet, quindi toohello web server, è necessario solo un inoltro regola NAT. In hello Barracuda NextGen Firewall utilizzato in hello in questo esempio regola sarebbe un NAT di destinazione della regola toopass ("ora legale NAT") il traffico.

seguente hello toocreate regola (o verificare le regole predefinite esistente), a partire dal dashboard di hello Barracuda NG amministratore client, passare scheda Configurazione toohello, hello configurazione operativa sezione selezionare il set di regole. Chiamata di una griglia, "Main regole" mostrerà hello regole attive e disattivate il firewall hello esistente. In hello angolo superiore destro di questa griglia è una piccola verde "+" fare clic su questo toocreate una nuova regola (Nota: il firewall può essere "bloccato" per le modifiche, se viene visualizzato un pulsante contrassegnato come "Blocco" e toocreate Impossibile o modificare le regole, fare clic su questo pulsante troppo "sbloccare" hello set di regole e consentire la modifica). Se si desidera tooedit una regola esistente, selezionare la regola, fare doppio clic su e scegliere Modifica regola.

Creare una nuova regola e specificare un nome, ad esempio "WebTraffic". 

icona della regola NAT destinazione Hello è simile al seguente: ![icona NAT di destinazione][2]

regola di Hello stessa avrà un aspetto simile al seguente:

![Regola del firewall][3]

Qui qualsiasi indirizzo in ingresso che riscontri hello Firewall tooreach HTTP (porta 80 o 443 per HTTPS) durante il tentativo verrà inviato hello interfaccia "IP locale DHCP1" e toohello reindirizzato il Server Web con indirizzo IP del 10.0.1.5 hello del Firewall. Poiché hello traffico in ingresso sulla porta 80 e server web di toohello corso sulla porta 80 è necessario apportare alcuna modifica porta. Tuttavia, hello elenco destinazione avrebbe potuto essere 10.0.1.5:8080 se il Server Web resta in attesa su una porta 8080 in questo modo la traduzione hello in ingresso porta 80 in hello firewall tooinbound porta 8080 hello web server.

Un metodo di connessione devono anche essere indicato, per hello regola di destinazione da Internet, hello "SNAT dinamici" è più appropriato. 

Anche se è stata creata una sola regola, è importante impostarne la priorità correttamente. Se nella griglia hello di tutte le regole firewall hello che è la nuova regola nella parte inferiore di hello (sotto regola "BLOCKALL" hello) non verrà mai entrano in gioco. Verificare la regola hello appena creato per il traffico web sia superiore regola BLOCKALL hello.

Dopo aver creata la regola hello, deve essere inserito toohello firewall e quindi attivato, se ciò non avviene regola hello modifica non avrà alcun effetto. il processo di attivazione e push Hello è descritto nella sezione successiva hello.

## <a name="rule-activation"></a>Attivazione delle regole
Con hello ruleset modificato tooadd questa regola, hello ruleset deve essere caricato toohello firewall e attivato.

![Attivazione delle regole firewall][4]

Nell'angolo superiore destra hello del client di gestione di hello sono un cluster di pulsanti. Fare clic su hello "inviare modifiche" pulsante toosend hello modificato regole toohello firewall, quindi fare clic sul pulsante "Attiva" hello.

Con l'attivazione del set di regole firewall hello hello è stata completata la compilazione di ambiente di esempio. Facoltativamente, gli script di compilazione post hello in hello sezione può essere riferimenti esegue tooadd un'applicazione toothis ambiente tootest hello scenari di traffico seguenti.

> [!IMPORTANT]
> È toorealize critico che non verrà raggiunto di direttamente server web hello. Quando un browser richiede una pagina HTTP da FrontEnd001.CloudApp.Net, passa di endpoint (porta 80) HTTP hello questo firewall toohello traffico non hello web server. Hello firewall, quindi in base a regole toohello creato in precedenza, NAT che richiedono toohello Server Web.
> 
> 

## <a name="traffic-scenarios"></a>Scenari di traffico
#### <a name="allowed-web-tooweb-server-through-firewall"></a>(Consentito) TooWeb Web Server con Firewall
1. L'utente Internet richiede una pagina HTTP a FrontEnd001.CloudApp.Net (servizio cloud per Internet).
2. Traffico passa del servizio cloud tramite endpoint aperto sull'interfaccia locale di toofirewall la porta 80 in 10.0.1.4:80
3. La subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
   3. Applicare NSG regola 3 (tooFirewall Internet), il traffico è l'elaborazione della regola consentita, arresto
4. Traffico raggiunge l'indirizzo IP interno del firewall hello (10.0.1.4)
5. Regola di inoltro di firewall vedere questa operazione è traffico sulla porta 80, lo reindirizza il server web toohello IIS01
6. Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello
7. Iis01 richiede SQL Server hello su AppVM01 per informazioni
8. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
9. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
   3. GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola
   4. Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto
10. AppVM01 riceve hello Query SQL e risponde
11. Poiché esistono non è consentito alcun regole in uscita su hello risposta hello subnet di back-end
12. La subnet front-end inizia l'elaborazione delle regole in ingresso:
    1. Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile
    2. regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.
13. server IIS Hello riceve risposta SQL hello e completa di risposta HTTP hello e invia toohello richiedente
14. Poiché si tratta di una sessione NAT dal firewall hello, destinazione risposta hello è (inizialmente) per hello Firewall
15. firewall Hello riceve hello risposta dal Server Web hello e inoltra toohello indietro utente Internet
16. Poiché esistono non è consentito alcun regole in uscita su hello risposta hello di subnet front-end e hello utente Internet riceve hello web pagina richiesta.

#### <a name="allowed-rdp-toobackend"></a>(Consentito) TooBackend RDP
1. Amministratore del server su internet richiede tooAppVM01 sessione RDP in BackEnd001.CloudApp.Net:xxxxx dove xxxxx è il numero di porta hello assegnato in modo casuale per RDP tooAppVM01 (porta hello assegnato è reperibile nel portale di Azure hello o tramite PowerShell)
2. Poiché hello che firewall è in ascolto solo hello indirizzo FrontEnd001.CloudApp.Net, non è coinvolta con questo flusso di traffico
3. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
4. Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.
5. La sessione RDP è abilitata.
6. AppVM01 richiede il nome utente e la password.

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a>(Consentito) Ricerca DNS del server Web sul server DNS
1. Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.
2. Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01
3. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
4. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   1. Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
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

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(Consentito) Il server Web richiede l'accesso a un file su AppVM01
1. IIS01 richiede un file su AppVM01.
2. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
3. subnet di back-end Hello inizia l'elaborazione della regola in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
   3. GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola
   4. Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto
4. AppVM01 riceve la richiesta di hello e risponde con il file (presupponendo che l'accesso è autorizzato)
5. Poiché esistono non è consentito alcun regole in uscita su hello risposta hello subnet di back-end
6. La subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile
   2. regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.
7. server IIS Hello riceve file hello

#### <a name="denied-web-direct-tooweb-server"></a>(Negato) TooWeb diretto Web Server
Poiché hello Server Web, IIS01 e hello Firewall sono in hello nello stesso servizio Cloud condividono hello stesso indirizzo IP pubblico. In questo modo sarebbe possibile indirizzare tutto il traffico HTTP toohello firewall. Mentre la richiesta hello viene fornita correttamente, non è possibile associarla direttamente toohello Server Web, viene passato, come previsto, tramite hello del Firewall prima di tutto. Vedere hello primo Scenario in questa sezione per il flusso del traffico hello.

#### <a name="denied-web-toobackend-server"></a>(Negato) TooBackend Web Server
1. Utente Internet tenta di un file in AppVM01 tramite hello servizio BackEnd001.CloudApp.Net tooaccess
2. Poiché non sono presenti endpoint aperto per la condivisione file, questo non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico

#### <a name="denied-web-dns-lookup-on-dns-server"></a>(Negato) Ricerca DNS Web sul server DNS
1. Utente Internet tenta un record DNS interno nella DNS01 tramite hello servizio BackEnd001.CloudApp.Net toolookup
2. Poiché non sono presenti endpoint aperto per DNS, questo non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico (Nota: la regola 1 (DNS) potrebbero non applicarsi per due motivi, primo indirizzo di origine hello è hello internet, questa regola si applica solo a toohello anche rete locale virtuale come hello di origine si tratta di una regola di assenso, non potrebbe negare il traffico mai)

#### <a name="denied-web-toosql-access-through-firewall"></a>(Negato) Accesso tooSQL Web tramite Firewall
1. L'utente Internet richiede dati SQL a FrontEnd001.CloudApp.Net (servizio cloud per Internet).
2. Poiché non sono presenti endpoint aperto per SQL, questo non raggiungerebbe hello servizio Cloud e non raggiunga firewall hello
3. Se gli endpoint sono stati aperti per qualche motivo, subnet front-end hello inizia l'elaborazione della regola in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
   3. Applicare la regola gruppo 2 (tooFirewall Internet), il traffico è l'elaborazione della regola consentita, arresto
4. Traffico raggiunge l'indirizzo IP interno del firewall hello (10.0.1.4)
5. Firewall non dispone di alcuna regola di inoltro per SQL ed Elimina hello traffico

## <a name="conclusion"></a>Conclusioni
Questo è un modo relativamente semplice di protezione delle applicazioni con un firewall e l'isolamento di subnet di back-end hello dal traffico in ingresso.

Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].

## <a name="references"></a>Riferimenti
### <a name="main-script-and-network-config"></a>Script principale e configurazione di rete
Salvare uno Script completo di hello in un file di script di PowerShell. Salvare hello configurazione di rete in un file denominato "NetworkConf2.xml".
Modificare le variabili definite dall'utente di hello in base alle esigenze. Eseguire script hello, quindi seguire istruzioni di programma di installazione di un regola Firewall di hello precedente.

#### <a name="full-script"></a>Script completo
Questo script verrà, in base alle variabili definite dall'utente hello:

1. Connettersi tooan sottoscrizione di Azure
2. Creare un nuovo account di archiviazione.
3. Creare una nuova rete virtuale e due subnet, come definito nel file di configurazione di rete hello
4. Creare 4 macchine virtuali di Windows Server.
5. Configurare il gruppo di sicurezza di rete eseguendo queste operazioni:
   * Creazione di un gruppo di sicurezza di rete
   * Inserimento delle regole.
   * Subnet appropriata toohello associazione hello NSG

Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.

> [!IMPORTANT]
> Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi. Solo i messaggi di errore formattati in rosso possono indicare un problema.
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and Network Security Groups in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Two new cloud services
       - Two Subnets (FrontEnd and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet (plus hello NVA on hello FrontEnd subnet)
       - Three Servers on hello BackEnd Subnet
       - Network Security Groups tooallow/deny traffic patterns as declared

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Security requirements are different for each use case and can be addressed in a
      myriad of ways. Please be sure that any sensitive data or applications are behind
      hello appropriate layer(s) of protection. This script serves as an example of some
      of hello techniques that can be used, but should not be used for all scenarios. You
      are responsible tooassess your security needs and hello appropriate protections
      needed, and then effectively implement those protections.

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       myFirewall - 10.0.1.4
       IIS01      - 10.0.1.5

      BackEnd Service (BackEnd subnet 10.0.2.0/24)
       DNS01      - 10.0.2.4
       AppVM01    - 10.0.2.5
       AppVM02    - 10.0.2.6

    #>

    # Fixed Variables
        $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password toobe used for all VMs"
        $VMName = @()
        $ServiceName = @()
        $VMFamily = @()
        $img = @()
        $size = @()
        $SubnetName = @()
        $VMIP = @()

    # User Defined Global Variables
      # These should be changes tooreflect your subscription and services
      # Invalid options will fail in hello validation section

      # Subscription Access Details
        $subID = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"

      # VM Account, Location, and Storage Details
        $LocalAdmin = "theAdmin"
        $DeploymentLocation = "Central US"
        $StorageAccountName = "vmstore02"

      # Service Details
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure proper NSG Rule creation later in this script:
        #       - hello Web Server must be VM 1
        #       - hello AppVM1 Server must be VM 2
        #       - hello DNS server must be VM 4
        #
        #       Otherwise hello NSG rules in hello last section of this
        #       script will need toobe changed toomatch hello modified
        #       VM array numbers ($i) so hello NSG Rule IP addresses
        #       are aligned toohello associated VM IP addresses.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - hello First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - hello Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - hello DNS Server
          $VMName += "DNS01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.4"

    # ----------------------------- #
    # No User Defined Varibles or   #
    # Configuration past this point #
    # ----------------------------- #

      # Get your Azure accounts
        Add-AzureAccount
        Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
        Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

      # Create Storage Account
        If (Test-AzureName -Storage -Name $StorageAccountName) { 
            Write-Host "Fatal Error: This storage account name is already in use, please pick a diffrent name." -ForegroundColor Red
            Return}
        Else {Write-Host "Creating Storage Account" -ForegroundColor Cyan 
              New-AzureStorageAccount -Location $DeploymentLocation -StorageAccountName $StorageAccountName}

      # Update Subscription Pointer tooNew Storage Account
        Write-Host "Updating Subscription Pointer tooNew Storage Account" -ForegroundColor Cyan 
        Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

    # Validation
    $FatalError = $false

    If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
         Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
         $FatalError = $true}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $BackEndService) { 
        Write-Host "hello BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello BackEndService service name is valid for use." -ForegroundColor Green}

    If (-Not (Test-Path $NetworkConfigFile)) { 
        Write-Host 'hello network config file was not found, please update hello $NetworkConfigFile variable toopoint toohello network config xml file.' -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation varible is correct and hello netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see hello above messages for more information." -ForegroundColor Red
        Return}
    Else { Write-Host "Validation passed, now building hello environment." -ForegroundColor Green}

    # Create VNET
        Write-Host "Creating VNET" -ForegroundColor Cyan 
        Set-AzureVNetConfig -ConfigurationPath $NetworkConfigFile -ErrorAction Stop

    # Create Services
        Write-Host "Creating Services" -ForegroundColor Cyan
        New-AzureService -Location $DeploymentLocation -ServiceName $FrontEndService -ErrorAction Stop
        New-AzureService -Location $DeploymentLocation -ServiceName $BackEndService -ErrorAction Stop

    # Build VMs
        $i=0
        $VMName | Foreach {
            Write-Host "Building $($VMName[$i])" -ForegroundColor Cyan
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all hello EndPoints we'll need once we're up and running
                # Note: Web traffic goes through hello firewall, so we'll need tooset up a HTTP endpoint.
                #       Also, hello firewall will be redirecting web traffic tooa new IP and Port in a
                #       forwarding rule, so hello HTTP endpoint here will have hello same public and local
                #       port and hello firewall will do hello NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                    # Note: A Remote Desktop endpoint is automatically created when each VM is created.
                }
            $i++
        }

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) too$($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 140 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
            -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
            -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
            -Protocol *

        # Assign hello NSG toohello Subnets
            Write-Host "Binding hello NSG tooboth subnets" -ForegroundColor Cyan
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
            Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

    # Optional Post-script Manual Configuration
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on hello IIS Server)
      # Install Backend resource (Run Post-Build Script on hello AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a>File di configurazione di rete
Salvare il file xml con posizione aggiornata e aggiungere hello collegamento toothis file toohello $NetworkConfigFile variabile nello script hello precedente.

    <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
      <VirtualNetworkConfiguration>
        <Dns>
          <DnsServers>
            <DnsServer name="DNS01" IPAddress="10.0.2.4" />
            <DnsServer name="Level3" IPAddress="209.244.0.3" />
          </DnsServers>
        </Dns>
        <VirtualNetworkSites>
          <VirtualNetworkSite name="CorpNetwork" Location="Central US">
            <AddressSpace>
              <AddressPrefix>10.0.0.0/16</AddressPrefix>
            </AddressSpace>
            <Subnets>
              <Subnet name="FrontEnd">
                <AddressPrefix>10.0.1.0/24</AddressPrefix>
              </Subnet>
              <Subnet name="BackEnd">
                <AddressPrefix>10.0.2.0/24</AddressPrefix>
              </Subnet>
            </Subnets>
            <DnsServersRef>
              <DnsServerRef name="DNS01" />
              <DnsServerRef name="Level3" />
            </DnsServersRef>
          </VirtualNetworkSite>
        </VirtualNetworkSites>
      </VirtualNetworkConfiguration>
    </NetworkConfiguration>

#### <a name="sample-application-scripts"></a>Script di applicazione di esempio
Se si desidera tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"
[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icona di Destination NAT"
[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regola del firewall"
[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Attivazione delle regole firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
