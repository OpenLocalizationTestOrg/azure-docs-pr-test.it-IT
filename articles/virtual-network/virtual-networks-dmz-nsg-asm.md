---
title: 'Esempio di rete perimetrale di Azure: Creare una rete perimetrale semplice con gruppi di sicurezza di rete | Microsoft Docs'
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
ms.openlocfilehash: ed172d552e1e4c9ee27c58abcd7ad2d98df21579
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/21/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a>Esempio 1: creare una semplice rete perimetrale usando un NSG con PowerShell classico
[Tornare alla pagina relativa alle procedure consigliate sui limiti di sicurezza][HOME]

> [!div class="op_single_selector"]
> * [Modello di Resource Manager](virtual-networks-dmz-nsg.md)
> * [Classica: PowerShell](virtual-networks-dmz-nsg-asm.md)
> 
>

Questo esempio descrive come creare una rete perimetrale primitiva con quattro server Windows e gruppi di sicurezza di rete. Questo esempio descrive tutti i comandi PowerShell pertinenti per un approfondimento di ogni passaggio. È disponibile anche una sezione sugli scenari di traffico con istruzioni dettagliate sul percorso seguito dal traffico attraverso i livelli di difesa della rete perimetrale. La sezione Riferimenti, infine, include tutto il codice e istruzioni complete per creare l'ambiente per testare e sperimentare vari scenari. 

![Rete perimetrale in ingresso con gruppo di sicurezza di rete][1]

## <a name="environment-description"></a>Descrizione dell'ambiente
Una sottoscrizione in questo esempio include le risorse seguenti:

* Due servizi cloud, "FrontEnd001" e "BackEnd001"
* Una rete virtuale, "CorpNetwork", con due subnet, "FrontEnd" e "BackEnd"
* Un gruppo di sicurezza di rete applicato a entrambe le subnet
* Un server Windows che rappresenta un server Web applicazioni ("IIS01")
* Due server Windows che rappresentano i server applicazioni back-end ("AppVM01", "AppVM02")
* Un server Windows che rappresenta un server DNS ("DNS01").

Nella sezione Riferimenti è disponibile uno script di PowerShell per creare la maggior parte dell'ambiente descritto in questo esempio. La creazione di macchine virtuali e reti virtuali, anche se eseguita dallo script di esempio, non è descritta in dettaglio in questo documento. 

Per creare l'ambiente, eseguire queste operazioni:

1. Salvare il file XML di configurazione di rete incluso nella sezione Riferimenti, aggiornandolo con i nomi, il percorso e gli indirizzi IP corrispondenti allo scenario specifico.
2. Aggiornare le variabili utente incluse nello script in modo che corrispondano all'ambiente in cui lo script verrà eseguito, ad esempio sottoscrizioni, nomi dei servizi e così via.
3. Eseguire lo script in PowerShell.

>[!Note]
>L'area indicata nello script di PowerShell deve corrispondere all'area indicata nel file XML di configurazione di rete.
>
>

Se l'esecuzione dello script viene completata correttamente, è possibile effettuare alcuni passaggi facoltativi. Nella sezione Riferimenti sono disponibili due script per configurare il server Web e il server applicazioni con una semplice applicazione Web per consentire l'esecuzione dei test con questa configurazione della rete perimetrale.

Le sezioni seguenti forniscono una descrizione dettagliata dei gruppi di sicurezza di rete e del relativo funzionamento per questo esempio spiegando le righe principali dello script di PowerShell.

## <a name="network-security-groups-nsg"></a>Gruppi di sicurezza di rete (NGS)
Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono caricate sei regole. 

> [!TIP]
> In genere, è consigliabile creare prima di tutto le regole specifiche di tipo "Consenti" e infine le regole di tipo "Nega" più generiche. La priorità assegnata determina quali regole vengono valutate per prime. Quando si rileva che al traffico è applicabile una determinata regola, non vengono valutate altre regole. Le regole del gruppo di sicurezza di rete possono essere applicate nella direzione in ingresso o in uscita, dal punto di vista della subnet.
> 
> 

A livello dichiarativo, per il traffico in ingresso vengono create le righe seguenti:

1. Il traffico DNS interno (porta 53) è consentito.
2. Il traffico RDP (porta 3389) da Internet a qualsiasi macchina virtuale è consentito.
3. Il traffico HTTP (porta 80) da Internet al server Web (IIS01) è consentito.
4. Tutto il traffico (tutte le porte) da IIS01 ad AppVM1 è consentito.
5. Tutto il traffico (tutte le porte) da Internet all'intera rete virtuale (entrambe le subnet) viene bloccato.
6. Tutto il traffico (tutte le porte) dalla subnet front-end alla subnet back-end viene bloccato.

Con queste regole associate a ogni subnet, se una richiesta HTTP proviene da Internet ed è diretta verso il server Web, le regole 3 (consenti) e 5 (nega) saranno applicabili, ma poiché la regola 3 ha una priorità maggiore, verrà applicata solo tale regola e la regola 5 non verrà presa in considerazione. La richiesta HTTP verrà quindi consentita sul server Web. Se lo stesso traffico prova a raggiungere il server DNS01, la regola 5 (nega) sarà la prima applicabile e il traffico non sarà autorizzato a passare al server. La regola 6 (nega) impedisce alla subnet front-end di comunicare con la subnet back-end, ad eccezione del traffico consentito nelle regole 1 e 4; questo set di regole protegge la rete back-end nel caso in cui un utente malintenzionato comprometta l'applicazione Web sul front-end. L'utente malintenzionato avrà infatti accesso limitato alla rete "protetta" back-end, ovvero solo alle risorse esposte nel server AppVM01.

Esiste una regola in uscita predefinita che consente il traffico in uscita verso Internet. Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita. Per bloccare il traffico in entrambe le direzioni, è obbligatorio il routing definito dall'utente, descritto nell'"Esempio 3" della [pagina relativa alle procedure consigliate sui limiti di sicurezza][HOME].

Nel seguito le singole regole vengono descritte in modo più dettagliato. **Nota**: nell'elenco seguente tutte le voci che iniziano con il simbolo del dollaro (ad esempio, $NSGName) sono variabili definite dall'utente incluse nello script riportato nella sezione Riferimenti di questo documento:

1. È necessario prima di tutto creare un gruppo di sicurezza di rete in cui inserire le regole:

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. La prima regola in questo esempio consente il traffico DNS fra tutte le reti interne e il server DNS nella subnet back-end. Nella regola sono inclusi alcuni parametri importanti:
   
   * "Type" indica in quale direzione del flusso di traffico verrà applicata questa regola. La direzione è dal punto di vista del subnet o della macchina virtuale, in base al punto in cui è associato questo gruppo di sicurezza di rete. Pertanto, se Type è impostato su "Inbound", la regola verrà applicata al traffico in ingresso nella subnet, ma non al traffico in uscita da essa.
   * "Priority" consente di impostare l'ordine in base al quale viene valutato un flusso di traffico. Più è basso il numero, maggiore sarà la priorità. Quando un flusso di traffico specifico è applicabile a una determinata regola, non vengono elaborate altre regole. Se quindi una regola con priorità 1 consente il traffico e una regola con priorità 2 lo blocca ed entrambe le regole sono applicabili, il passaggio del traffico viene consentito perché viene applicata la regola 1 con priorità più alta e non vengono considerate altre regole.
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

3. Questa regola consente il flusso del traffico RDP da Internet alla porta RDP su qualsiasi server della subnet associata. La regola usa due tipi speciali di prefissi per l'indirizzo: "VIRTUAL_NETWORK" e "INTERNET", pertanto consente di gestire più facilmente una categoria più ampia di prefissi dell'indirizzo.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. Questa regola consente al traffico Internet in ingresso di raggiungere il server Web. Il comportamento di routing rimane invariato, ma il traffico destinato a IIS01 può transitare. Se quindi il traffico proveniente da Internet ha come destinazione il server Web, viene consentito e non vengono elaborate altre regole (nella regola con priorità 140 viene bloccato qualsiasi altro tipo di traffico Internet in ingresso). Se si elabora soltanto traffico HTTP, questa regola può essere limitata ulteriormente in modo da consentire esclusivamente la porta di destinazione 80.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet to $VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. Questa regola consente il passaggio del traffico dal server IIS01 al server AppVM01 e una regola successiva blocca tutto il resto del traffico dal front-end al back-end. Per migliorare la regola, è consigliabile aggiungere la porta, se è nota. Ad esempio, se il server IIS ha necessità di raggiungere solo SQL Server in AppVM01, l'impostazione dell'intervallo delle porte di destinazione (DestinationPortRange) deve essere modificata da "*" (qualsiasi) a 1433 (porta SQL), in modo da esporre una superficie di attacco più limitata in AppVM01 nel caso l'applicazione Web venisse compromessa.

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] to $VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. Questa regola blocca il traffico da Internet a qualsiasi server della rete. Insieme alla regola con priorità 110 e 120, consente esclusivamente il traffico Internet in ingresso diretto al firewall e alle porte RDP sui server e blocca tutto il traffico restante. Questa regola è di tipo fail-safe per bloccare tutti i flussi imprevisti.
    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $VNetName VNet from the Internet" `
        -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *
    ```
7. La regola finale blocca il traffico dalla subnet front-end alla subnet back-end. Poiché si tratta di una regola solo di tipo Inbound, il traffico in direzione opposta è consentito (dal back-end al front-end).

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule `
        -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" `
        -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix `
        -DestinationPortRange '*' `
        -Protocol * 
    ```

## <a name="traffic-scenarios"></a>Scenari di traffico
#### <a name="allowed-internet-to-web-server"></a>(*Consentito*) Da Internet a server Web
1. Un utente Internet richiede una pagina HTTP a FrontEnd001.CloudApp.Net (servizio cloud per Internet)
2. Il servizio cloud passa il traffico attraverso l'endpoint aperto sulla porta 80 a IIS01 (server Web).
3. La subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.
   2. Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.
   3. Regola gruppo di sicurezza di rete 3 (da Internet a IIS01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
4. Il traffico raggiunge l'indirizzo IP interno del server Web IIS01 (10.0.1.5).
5. IIS01 è in ascolto del traffico Web, riceve la richiesta e ne avvia l'elaborazione.
6. IIS01 chiede informazioni a SQL Server in AppVM01.
7. Non essendoci regole in uscita sulla subnet front-end, il traffico è consentito
8. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   1. Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.
   2. Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.
   3. Regola gruppo di sicurezza di rete 3 (da Internet a firewall), non applicabile, passa alla regola successiva.
   4. Regola gruppo di sicurezza di rete 4 (da IIS01 ad AppVM01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
9. AppVM01 riceve la query SQL e risponde.
10. Non essendoci regole in uscita sulla subnet back-end, la risposta è consentita
11. La subnet front-end inizia l'elaborazione delle regole in ingresso:
    1. Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.
    2. La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.
12. Il server IIS riceve la risposta SQL , completa la risposta HTTP e la invia al richiedente.
13. Non essendoci regole in uscita sulla subnet front-end, la risposta è consentita e l'utente Internet riceve la pagina Web richiesta.

#### <a name="allowed-rdp-to-backend"></a>(*Consentito*) Traffico RDP al back-end
1. L'amministratore del server su Internet richiede una sessione RDP ad AppVM01 su BackEnd001.CloudApp.Net:xxxxx, dove xxxxx è il numero di porta assegnato casualmente per RDP a AppVM01. Si può trovare la porta assegnata sul portale di Azure o tramite PowerShell
2. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   1. Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.
   2. Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
3. Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.
4. La sessione RDP è abilitata.
5. AppVM01 richiede il nome utente e la password

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a>(*Consentito*) Ricerca DNS del server Web sul server DNS
1. Il server Web, IIS01, richiede un feed di dati all'indirizzo www.data.gov, ma deve risolvere l'indirizzo.
2. La configurazione di rete per la rete virtuale elenca DNS01 (10.0.2.4 nella subnet back-end) come server DNS primario, IIS01 invia la richiesta DNS a DNS01.
3. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
4. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   * Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
5. Il server DNS riceve la richiesta.
6. Il server DNS non ha l'indirizzo memorizzato nella cache e invia la richiesta a un server DNS radice su Internet.
7. Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.
8. Il server DNS Internet risponde perché la sessione è stata avviata internamente, la risposta è consentita.
9. Il server DNS memorizza la risposta nella cache e restituisce a IIS01 la risposta alla richiesta iniziale.
10. Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.
11. La subnet front-end inizia l'elaborazione delle regole in ingresso:
    1. Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.
    2. La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.
12. IIS01 riceve la risposta da DNS01.

#### <a name="allowed-web-server-access-file-on-appvm01"></a>(*Consentito*) Il server Web richiede l'accesso a un file in AppVM01
1. IIS01 richiede un file in AppVM01.
2. Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.
3. La subnet back-end inizia l'elaborazione delle regole in ingresso:
   1. Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.
   2. Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.
   3. Regola gruppo di sicurezza di rete 3 (da Internet a IIS01) non applicabile, passa alla regola successiva.
   4. Regola gruppo di sicurezza di rete 4 (da IIS01 ad AppVM01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
4. AppVM01 riceve la richiesta e risponde con il file (presupponendo che l'accesso sia autorizzato).
5. Non essendoci regole in uscita sulla subnet back-end, la risposta è consentita
6. La subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.
   2. La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.
7. Il server IIS riceve il file.

#### <a name="denied-web-to-backend-server"></a>(*Negato*) Traffico Web al server back-end
1. Un utente Internet prova ad accedere a un file in AppVM01 tramite il servizio BackEnd001.CloudApp.Net
2. Non essendoci endpoint aperti per la condivisione file, il traffico non passa attraverso il servizio cloud e non raggiunge il server
3. In caso di apertura degli endpoint per qualunque motivo, la regola del gruppo di sicurezza di rete 5 (da Internet a rete virtuale) bloccherà questo traffico.

#### <a name="denied-web-dns-look-up-on-dns-server"></a>(*Negato*) Ricerca DNS Web sul server DNS
1. L'utente Internet prova a cercare un record DNS interno su DNS01 tramite il servizio BackEnd001.CloudApp.Net
2. Non essendoci endpoint aperti per DNS, il traffico non passa attraverso il servizio cloud e non raggiunge il server
3. In caso di apertura degli endpoint per qualunque motivo, la regola del gruppo di sicurezza di rete 5 (da Internet a rete virtuale) bloccherà questo traffico. Si noti che la regola 1 (DNS) non è applicabile per due motivi, prima di tutto l'indirizzo di origine è Internet e questa regola si applica solo quando l'origine è la rete virtuale locale, in secondo luogo questa è una regola di tipo Consenti e quindi non bloccherà mai il traffico

#### <a name="denied-web-to-sql-access-through-firewall"></a>(*Negato*) Accesso dal Web a SQL tramite il firewall
1. Un utente Internet richiede dati SQL a FrontEnd001.CloudApp.Net (servizio cloud per Internet)
2. Non essendoci endpoint aperti per SQL, il traffico non passa attraverso il servizio cloud e non raggiunge il firewall
3. Se gli endpoint sono aperti per qualunque motivo, la subnet front-end inizia l'elaborazione delle regole in ingresso:
   1. Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.
   2. Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.
   3. Regola gruppo di sicurezza di rete 3 (da Internet a IIS01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.
4. Il traffico raggiunge l'indirizzo IP interno di IIS01 (10.0.1.5).
5. IIS01 non è in ascolto sulla porta 1433, pertanto la richiesta non ottiene risposta.

## <a name="conclusion"></a>Conclusioni
Questo esempio consente di isolare la subnet back-end dal traffico in ingresso in un modo relativamente semplice e diretto.

Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].

## <a name="references"></a>Riferimenti
### <a name="main-script-and-network-config"></a>Script principale e configurazione di rete
Salvare lo script completo in un file script di PowerShell. Salvare la configurazione di rete in un file denominato "NetworkConf1.xml".
Modificare le variabili definite dall'utente secondo le esigenze ed eseguire lo script.

#### <a name="full-script"></a>Script completo
In base alle variabili definite dall'utente, lo script consente di:

1. Connettersi a una sottoscrizione di Azure
2. Creare un account di archiviazione
3. Creare una rete virtuale e due subnet, come definito nel file di configurazione di rete
4. Compilare quattro macchine virtuali Windows Server
5. Configurare il gruppo di sicurezza di rete, incluse le operazioni seguenti:
   * Creazione di un gruppo di sicurezza di rete
   * Inserimento delle regole.
   * Associazione del gruppo di sicurezza di rete alle subnet appropriate

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
   - One server on the FrontEnd Subnet
   - Three Servers on the BackEnd Subnet
   - Network Security Groups to allow/deny traffic patterns as declared

  Before running script, ensure the network configuration file is created in
  the directory referenced by $NetworkConfigFile variable (or update the
  variable to reflect the path and file name of the config file being used).

 .Notes
  Security requirements are different for each use case and can be addressed in a
  myriad of ways. Please be sure that any sensitive data or applications are behind
  the appropriate layer(s) of protection. This script serves as an example of some
  of the techniques that can be used, but should not be used for all scenarios. You
  are responsible to assess your security needs and the appropriate protections
  needed, and then effectively implement those protections.

  FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
   IIS01      - 10.0.1.5

  BackEnd Service (BackEnd subnet 10.0.2.0/24)
   DNS01      - 10.0.2.4
   AppVM01    - 10.0.2.5
   AppVM02    - 10.0.2.6

#>

# Fixed Variables
    $LocalAdminPwd = Read-Host -Prompt "Enter Local Admin Password to be used for all VMs"
    $VMName = @()
    $ServiceName = @()
    $VMFamily = @()
    $img = @()
    $size = @()
    $SubnetName = @()
    $VMIP = @()

# User-Defined Global Variables
  # These should be changes to reflect your subscription and services
  # Invalid options will fail in the validation section

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
    # Note: To ensure proper NSG Rule creation later in this script:
    #       - The Web Server must be VM 0
    #       - The AppVM1 Server must be VM 1
    #       - The DNS server must be VM 3
    #
    #       Otherwise the NSG rules in the last section of this
    #       script will need to be changed to match the modified
    #       VM array numbers ($i) so the NSG Rule IP addresses
    #       are aligned to the associated VM IP addresses.

    # VM 0 - The Web Server
      $VMName += "IIS01"
      $ServiceName += $FrontEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $FESubnet
      $VMIP += "10.0.1.5"

    # VM 1 - The First Application Server
      $VMName += "AppVM01"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.5"

    # VM 2 - The Second Application Server
      $VMName += "AppVM02"
      $ServiceName += $BackEndService
      $VMFamily += "Windows"
      $img += $SrvImg
      $size += "Standard_D3"
      $SubnetName += $BESubnet
      $VMIP += "10.0.2.6"

    # VM 3 - The DNS Server
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

  # Update Subscription Pointer to New Storage Account
    Write-Host "Updating Subscription Pointer to New Storage Account" -ForegroundColor Cyan 
    Set-AzureSubscription –SubscriptionId $subID -CurrentStorageAccountName $StorageAccountName -ErrorAction Stop

# Validation
$FatalError = $false

If (-Not (Get-AzureLocation | Where {$_.DisplayName -eq $DeploymentLocation})) {
     Write-Host "This Azure Location was not found or available for use" -ForegroundColor Yellow
     $FatalError = $true}

If (Test-AzureName -Service -Name $FrontEndService) { 
    Write-Host "The FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The FrontEndService service name is valid for use." -ForegroundColor Green}

If (Test-AzureName -Service -Name $BackEndService) { 
    Write-Host "The BackEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The BackEndService service name is valid for use." -ForegroundColor Green}

If (-Not (Test-Path $NetworkConfigFile)) { 
    Write-Host 'The network config file was not found, please update the $NetworkConfigFile variable to point to the network config xml file.' -ForegroundColor Yellow
    $FatalError = $true}
Else { Write-Host "The network configuration file was found" -ForegroundColor Green
        If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
            Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation variable is correct and the network config file matches.' -ForegroundColor Yellow
            $FatalError = $true}
        Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

If ($FatalError) {
    Write-Host "A fatal error has occurred, please see the above messages for more information." -ForegroundColor Red
    Return}
Else { Write-Host "Validation passed, now building the environment." -ForegroundColor Green}

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
    Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

  # Build the NSG
    Write-Host "Building the NSG" -ForegroundColor Cyan
    New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

  # Add NSG Rules
    Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[3] -DestinationPortRange '53' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
        -SourceAddressPrefix Internet -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[0]) to $($VMName[1])" -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[0] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[1] -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $VNetName VNet from the Internet" -Type Inbound -Priority 140 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
        -Protocol *

    Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate the $FESubnet subnet from the $BESubnet subnet" -Type Inbound -Priority 150 -Action Deny `
        -SourceAddressPrefix $FEPrefix -SourcePortRange '*' `
        -DestinationAddressPrefix $BEPrefix -DestinationPortRange '*' `
        -Protocol *

    # Assign the NSG to the Subnets
        Write-Host "Binding the NSG to both subnets" -ForegroundColor Cyan
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $FESubnet -VirtualNetworkName $VNetName
        Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName -SubnetName $BESubnet -VirtualNetworkName $VNetName

# Optional Post-script Manual Configuration
  # Install Test Web App (Run Post-Build Script on the IIS Server)
  # Install Backend resource (Run Post-Build Script on the AppVM01)
  Write-Host
  Write-Host "Build Complete!" -ForegroundColor Green
  Write-Host
  Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
  Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
  Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
  Write-Host
```

#### <a name="network-config-file"></a>File di configurazione di rete
Salvare questo file XML con il percorso aggiornato e aggiungere il collegamento a questo file nella variabile $NetworkConfigFile dello script precedente.

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
Se si vuole installare un'applicazione di esempio per questo e altri esempi di rete perimetrale, è possibile trovarne una in [Script di applicazione di esempio][SampleApp]

## <a name="next-steps"></a>Passaggi successivi
* Aggiornare e salvare il file XML
* Eseguire lo script di PowerShell per creare l'ambiente
* Installare l'applicazione di esempio
* Testare diversi flussi di traffico attraverso la rete perimetrale

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

