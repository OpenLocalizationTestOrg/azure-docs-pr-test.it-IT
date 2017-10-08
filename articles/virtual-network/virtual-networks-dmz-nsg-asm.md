---
title: 'aaaAzure esempio DMZ: compilare una semplice rete Perimetrale con NSGs | Documenti Microsoft'
description: Creare una rete perimetrale con gruppi di sicurezza di rete
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: f8622b1d-c07d-4ea6-b41c-4ae98d998fff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: 32a40a8dc7539c4c7293988e6c36e5e32ef11045
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Esempio 1: creare una semplice rete perimetrale usando un NSG con PowerShell classico
[Restituire la pagina sicurezza limite Best Practices toohello][HOME]

> [!div class="op_single_selector"]
> * [Modello di Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classica: PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Questo esempio descrive come creare una rete perimetrale primitiva con quattro server Windows e gruppi di sicurezza di rete. In questo esempio viene descritto ciascun hello rilevanti PowerShell comandi tooprovide una comprensione più approfondita di ogni passaggio. È inoltre disponibile un Scenario di traffico sezione tooprovide un'analisi approfondita dettagliate come traffico procede attraverso i livelli di difesa hello hello rete Perimetrale. Infine, nella sezione dei riferimenti hello è codice completo hello e istruzione toobuild questo ambiente tootest e sperimentare vari scenari. 

![Rete perimetrale in ingresso con gruppo di sicurezza di rete][1]

## <a name="environment-description"></a>Descrizione dell'ambiente
In questo esempio una sottoscrizione contiene hello seguenti risorse:

* Due servizi cloud, "FrontEnd001" e "BackEnd001"
* Una rete virtuale, "CorpNetwork", con due subnet, "FrontEnd" e "BackEnd"
* Un gruppo di sicurezza di rete che viene applicato tooboth subnet
* Un server Windows che rappresenta un server Web applicazioni ("IIS01").
* Due server Windows che rappresentano i server applicazioni back-end ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01")

Nella sezione dei riferimenti, hello è uno script di PowerShell che consente di creare la maggior parte dell'ambiente hello descritta in questo esempio. Macchine virtuali hello di compilazione e le reti virtuali, anche se vengono eseguite dallo script di esempio hello, non sono descritti in dettaglio in questo documento. 

ambiente di hello toobuild;

1. Salvare file xml configurazione rete hello inclusi nella sezione dei riferimenti hello (aggiornata con i nomi, la posizione e scenario hello dato toomatch di indirizzi IP)
2. Le variabili utente di aggiornamento hello nello script di hello script toomatch hello ambiente hello è toobe eseguite (sottoscrizioni, nomi di servizio e così via)
3. Eseguire script hello in PowerShell

>[!Note]
>area hello indicato nel file di configurazione xml di hello rete deve corrispondere a area Hello indicato nell'hello script di PowerShell.
>
>

Una volta script hello viene eseguito correttamente ulteriori passaggi facoltativi possono essere adottate, nella sezione dei riferimenti hello sono due script tooset hello web server e il server di app con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.

Hello sezioni seguenti forniscono una descrizione dettagliata dei gruppi di sicurezza di rete e il relativo funzionamento per questo esempio, illustrando le righe di chiave hello dello script di PowerShell.

## <a name="network-security-groups-nsg"></a>Gruppi di sicurezza di rete (NGS)
Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono caricate sei regole. 

> [!TIP]
> In genere, si deve creare regole "Consenti" specifiche prima e quindi hello ultima più generico "Deny" regole. Hello assegnata la priorità determina quali regole vengono valutate per prime. Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole. Possono essere applicate regole di gruppo in hello nella direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).
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

Una regola in uscita predefinito che consente il traffico in uscita toohello internet. Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita. toolock verso il basso il traffico in entrambe le direzioni, Routing definito dall'utente è obbligatorio e viene esaminata in "Esempio 3" in hello [pagina migliori procedure consigliate di sicurezza limite][HOME].

Ogni regola viene discusso in maggior dettaglio come indicato di seguito (**nota**: qualsiasi elemento nell'elenco a partire dal simbolo del dollaro seguito hello (ad esempio: $NSGName) è una variabile definita dall'utente da uno script di hello nella sezione di riferimento hello di questo documento):

1. Un gruppo di sicurezza di rete devono essere compilato regole hello toohold:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. prima regola di Hello in questo esempio consente il traffico DNS tra tutti i server DNS di toohello reti interne nella subnet back-end hello. regola di Hello include alcuni parametri importanti:
   
   * "Type" indica in quale direzione del flusso di traffico verrà applicata questa regola. direzione Hello è dal punto di vista di hello di subnet hello o macchina virtuale (in base a cui è associato questo gruppo). Pertanto se il tipo è "Inbound" e traffico sta entrando in subnet hello, verrà applicata la regola hello e traffico lasciando subnet hello potrebbe non essere interessato da questa regola.
   * "Priority" imposta hello l'ordine in cui viene valutato un flusso di traffico. Hello hello numero hello superiore hello priorità inferiore. Quando il flusso di traffico specifico tooa si applica una regola, non vengono elaborate ulteriori regole. Pertanto se una regola con priorità 1 consente il traffico e una regola con priorità 2 impedisca il traffico, entrambe le regole si applicano tootraffic quindi sia possibile usare il traffico hello tooflow (poiché la regola 1 ha una priorità più alta da cui ha effetto e non altre regole sono state applicate).
   * "Action" indica se il traffico a cui si applica la regola viene bloccato o consentito.

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. Questa regola consente di tooflow il traffico RDP da hello internet toohello la porta RDP in qualsiasi server in hello associato subnet. La regola usa due tipi speciali di prefissi per l'indirizzo: "VIRTUAL_NETWORK" e "INTERNET", Questi tag sono un tooaddress facilmente una categoria di dimensioni maggiore di prefissi di indirizzo.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Questa regola consente di server web in ingresso internet traffico toohit hello. Questa regola non modifica il comportamento di routing hello. regola di Hello consente solo il traffico destinato IIS01 toopass. Pertanto se il traffico proveniente da Internet hello disponesse di server web hello come destinazione di questa regola consente e arrestare l'elaborazione di altre regole. (Regola hello priorità 140 tutte le altre traffico in ingresso internet è bloccato). Se si sta elaborando solo il traffico HTTP, questa regola può essere ulteriormente limitato tooonly Consenti destinazione la porta 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Questa regola consente il traffico toopass dal server IIS01 hello toohello AppVM01 server, una regola successiva blocca tutto il traffico tooBackend altri server front-end. tooimprove questa regola, se la porta hello è noto che deve essere aggiunti. Ad esempio, se il server IIS hello sta impegnando solo SQL Server in AppVM01, hello intervallo di porte di destinazione deve essere modificato da "*" (Any) too1433 (porta SQL Buongiorno) consentendo in tal modo una superficie di attacco in ingresso più piccola in AppVM01 deve hello web applicazione dovesse essere compromessa.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Questa regola impedisce il traffico da hello internet tooany server hello rete. Con regole di hello priorità 110 e 120, effetto hello è tooallow solo internet traffico toohello firewall in entrata e le porte RDP nel server e blocca tutto il resto. Questa regola è "alternativo" regola tooblock tutti i flussi imprevisti.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $VNetName VNet from hello Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. regola finale Hello impedisca il traffico dalla subnet di back-end toohello subnet front-end hello. Poiché questa regola è una regola sola in ingresso, è consentito traffico inverso (da hello back-end toohello front-end).

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate hello $FESubnet subnet from hello $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Scenari di traffico
#### <a name="allowed-internet-tooweb-server"></a>(*Consentito*) server tooweb Internet
1. Un utente Internet richiede una pagina HTTP a FrontEnd001.CloudApp.Net (servizio cloud per Internet)
2. Traffico del servizio passa attraverso un endpoint aperto sulla porta 80 verso IIS01 cloud (server web hello)
3. La subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
   3. Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto
4. Traffico raggiunge l'indirizzo IP interno del server web hello IIS01 (10.0.1.5)
5. Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello
6. Iis01 richiede SQL Server hello su AppVM01 per informazioni
7. Non essendoci regole in uscita sulla subnet front-end, il traffico è consentito
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
13. Poiché non esistono regole in uscita nella subnet front-end hello hello risposta è consentita e hello internet viene visualizzata una pagina web hello richiesta.

#### <a name="allowed-rdp-toobackend"></a>(*Consentito*) toobackend RDP
1. Amministratore del server su internet richiede tooAppVM01 sessione RDP in BackEnd001.CloudApp.Net:xxxxx dove xxxxx è il numero di porta hello assegnato in modo casuale per RDP tooAppVM01 (porta hello assegnato è reperibile nel portale di Azure hello o tramite PowerShell)
2. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
3. Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.
4. La sessione RDP è abilitata.
5. AppVM01 richiede la password e nome utente hello

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

#### <a name="denied-web-toobackend-server"></a>(*Negato*) server toobackend Web
1. Un utente internet tenta tooaccess un file in AppVM01 tramite hello BackEnd001.CloudApp.Net servizio
2. Poiché non sono presenti endpoint aperto per la condivisione file, il traffico non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Negato*) Ricerca DNS Web sul server DNS
1. Un utente internet tenta toolook di un record DNS interno nella DNS01 tramite hello BackEnd001.CloudApp.Net servizio
2. Poiché non sono presenti endpoint aperto per DNS, il traffico non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello
3. Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico (Nota: la regola 1 (DNS) potrebbero non applicarsi per due motivi, primo indirizzo di origine hello è hello internet, questa regola si applica solo a toohello anche rete locale virtuale come hello di origine Questa regola è una regola di assenso, in modo che non sarebbe mai negare il traffico)

#### <a name="denied-web-toosql-access-through-firewall"></a>(*Negato*) Web tooSQL accesso tramite firewall
1. Un utente Internet richiede dati SQL a FrontEnd001.CloudApp.Net (servizio cloud per Internet)
2. Poiché non sono presenti endpoint aperto per SQL, il traffico non raggiungerebbe hello servizio Cloud e non raggiunga firewall hello
3. Se gli endpoint sono stati aperti per qualche motivo, subnet front-end hello inizia l'elaborazione della regola in ingresso:
   1. GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola
   2. GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola
   3. Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto
4. Traffico raggiunge l'indirizzo IP interno di hello IIS01 (10.0.1.5)
5. Non è in ascolto sulla porta 1433, che non è più richiesta toohello risposta iis01

## <a name="conclusion"></a>Conclusioni
Questo esempio è un modo semplice e relativamente semplice isolare subnet back-end hello dal traffico in ingresso.

Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].

## <a name="references"></a>Riferimenti
### <a name="main-script-and-network-config"></a>Script principale e configurazione di rete
Salvare uno Script completo di hello in un file di script di PowerShell. Salvare hello configurazione di rete in un file denominato "NetworkConf1.xml".
Modificare le variabili definite dall'utente hello come script hello necessari e vengono eseguiti.

#### <a name="full-script"></a>Script completo
Questo script verrà, in base alle variabili definite dall'utente hello;

1. Connettersi tooan sottoscrizione di Azure
2. Creare un account di archiviazione
3. Creare una rete virtuale e due subnet, come definito nel file di configurazione di rete hello
4. Compilare quattro macchine virtuali Windows Server
5. Configurare il gruppo di sicurezza di rete eseguendo queste operazioni:
   * Creazione di un gruppo di sicurezza di rete
   * Inserimento delle regole.
   * Subnet appropriata toohello associazione hello NSG

Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.

> [!IMPORTANT]
> Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi. Solo i messaggi di errore formattati in rosso possono indicare un problema.
> 
>

```PowerShell
<# 
 .SYNOPSIS
  Example of Network Security Groups in an isolated network (Azure only, no hybrid connections)

 .DESCRIPTION
  This script will build out a sample DMZ setup containing:
   - A default storage account for VM disks
   - Two new cloud services
   - Two Subnets (FrontEnd and BackEnd subnets)
   - One server on hello FrontEnd Subnet
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

# User-Defined Global Variables
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
    $NetworkConfigFile = "C:\Scripts\NetworkConf1.xml"

  # VM Base Disk Image Details
    $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

  # NSG Details
    $NSGName = "MyVNetSG"

# User-Defined VM Specific Configuration
    # Note: tooensure proper NSG Rule creation later in this script:
    #       - hello Web Server must be VM 0
    #       - hello AppVM1 Server must be VM 1
    #       - hello DNS server must be VM 3
    #
    #       Otherwise hello NSG rules in hello last section of this
    #       script will need toobe changed toomatch hello modified
    #       VM array numbers ($i) so hello NSG Rule IP addresses
    #       are aligned toohello associated VM IP addresses.

    # VM 0 - hello Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - hello First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - hello Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - hello DNS Server
      $VMName += "DNS01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.4"

# ----------------------------- #
# No User-Defined Variables or  #
# Configuration past this point #
# ----------------------------- #    

  # Get your Azure accounts
    Add-AzureAccount
    Set-AzureSubscription –SubscriptionId $subID -ErrorAction Stop
    Select-AzureSubscription -SubscriptionId $subID -Current -ErrorAction Stop

  # Create Storage Account
    If (Test-AzureName -Storage -Name $StorageAccountName) { 
        Write-Host "Fatal Error: This storage account name is already in use, please pick a different name." -ForegroundColor Red
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
Else { Write-Host "hello network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'hello deployment location was not found in hello network config file, please check hello network config file tooensure hello $DeploymentLocation variable is correct and hello network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "hello deployment location was found in hello network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see hello above messages for more information." -ForegroundColor Red
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
        New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
            Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
            Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
            Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
            Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
            Remove-AzureEndpoint -Name "PowerShell" | `
            New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
            # Note: A Remote Desktop endpoint is automatically created when each VM is created.
        $i++
    }
    # Add HTTP Endpoint for IIS01
    Get-AzureVM -ServiceName $ServiceName[0] -Name $VMName[0] | Add-AzureEndpoint -Name HTTP -Protocol tcp -LocalPort 80 -PublicPort 80 | Update-AzureVM

# Configure NSG
    Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

  # Build hello NSG
    Write-Host "Building hello NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet too$($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) too$($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
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
  # Install Test Web App (Run Post-Build Script on hello IIS Server)
  # Install Backend resource (Run Post-Build Script on hello AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on hello IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on hello AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>File di configurazione di rete
Salvare il file xml con posizione aggiornata e aggiungere la variabile toohello $NetworkConfigFile hello link toothis file hello script precedente.

```XML
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
```

#### <a name="sample-application-scripts"></a>Script di applicazione di esempio
Se si desidera tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]

## <a name="next-steps"></a>Passaggi successivi
* Aggiornare e salvare il file XML
* Eseguire hello PowerShell script toobuild hello ambiente
* Installare l'applicazione di esempio hello
* Testare diversi flussi di traffico attraverso la rete perimetrale

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

