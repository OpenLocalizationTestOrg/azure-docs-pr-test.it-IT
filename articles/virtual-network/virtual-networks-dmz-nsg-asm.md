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
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-classic-powershell"></a><span data-ttu-id="88190-103">Esempio 1: creare una semplice rete perimetrale usando un NSG con PowerShell classico</span><span class="sxs-lookup"><span data-stu-id="88190-103">Example 1 – Build a simple DMZ using NSGs with classic PowerShell</span></span>
<span data-ttu-id="88190-104">[Restituire la pagina sicurezza limite Best Practices toohello][HOME]</span><span class="sxs-lookup"><span data-stu-id="88190-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="88190-105">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="88190-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="88190-106">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="88190-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="88190-107">Questo esempio descrive come creare una rete perimetrale primitiva con quattro server Windows e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="88190-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="88190-108">In questo esempio viene descritto ciascun hello rilevanti PowerShell comandi tooprovide una comprensione più approfondita di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="88190-108">This example describes each of hello relevant PowerShell commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="88190-109">È inoltre disponibile un Scenario di traffico sezione tooprovide un'analisi approfondita dettagliate come traffico procede attraverso i livelli di difesa hello hello rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="88190-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="88190-110">Infine, nella sezione dei riferimenti hello è codice completo hello e istruzione toobuild questo ambiente tootest e sperimentare vari scenari.</span><span class="sxs-lookup"><span data-stu-id="88190-110">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="88190-111">![Rete perimetrale in ingresso con gruppo di sicurezza di rete][1]</span><span class="sxs-lookup"><span data-stu-id="88190-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="88190-112">Descrizione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="88190-112">Environment description</span></span>
<span data-ttu-id="88190-113">In questo esempio una sottoscrizione contiene hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="88190-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="88190-114">Due servizi cloud, "FrontEnd001" e "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="88190-114">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="88190-115">Una rete virtuale, "CorpNetwork", con due subnet, "FrontEnd" e "BackEnd"</span><span class="sxs-lookup"><span data-stu-id="88190-115">A Virtual Network, “CorpNetwork”, with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="88190-116">Un gruppo di sicurezza di rete che viene applicato tooboth subnet</span><span class="sxs-lookup"><span data-stu-id="88190-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="88190-117">Un server Windows che rappresenta un server Web applicazioni ("IIS01").</span><span class="sxs-lookup"><span data-stu-id="88190-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="88190-118">Due server Windows che rappresentano i server applicazioni back-end ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="88190-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="88190-119">Un server Windows che rappresenta un server DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="88190-119">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="88190-120">Nella sezione dei riferimenti, hello è uno script di PowerShell che consente di creare la maggior parte dell'ambiente hello descritta in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="88190-120">In hello references section, there is a PowerShell script that builds most of hello environment described in this example.</span></span> <span data-ttu-id="88190-121">Macchine virtuali hello di compilazione e le reti virtuali, anche se vengono eseguite dallo script di esempio hello, non sono descritti in dettaglio in questo documento.</span><span class="sxs-lookup"><span data-stu-id="88190-121">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span> 

<span data-ttu-id="88190-122">ambiente di hello toobuild;</span><span class="sxs-lookup"><span data-stu-id="88190-122">toobuild hello environment;</span></span>

1. <span data-ttu-id="88190-123">Salvare file xml configurazione rete hello inclusi nella sezione dei riferimenti hello (aggiornata con i nomi, la posizione e scenario hello dato toomatch di indirizzi IP)</span><span class="sxs-lookup"><span data-stu-id="88190-123">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="88190-124">Le variabili utente di aggiornamento hello nello script di hello script toomatch hello ambiente hello è toobe eseguite (sottoscrizioni, nomi di servizio e così via)</span><span class="sxs-lookup"><span data-stu-id="88190-124">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc.)</span></span>
3. <span data-ttu-id="88190-125">Eseguire script hello in PowerShell</span><span class="sxs-lookup"><span data-stu-id="88190-125">Execute hello script in PowerShell</span></span>

>[!Note]
><span data-ttu-id="88190-126">area hello indicato nel file di configurazione xml di hello rete deve corrispondere a area Hello indicato nell'hello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88190-126">hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>
>
>

<span data-ttu-id="88190-127">Una volta script hello viene eseguito correttamente ulteriori passaggi facoltativi possono essere adottate, nella sezione dei riferimenti hello sono due script tooset hello web server e il server di app con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="88190-127">Once hello script runs successfully additional optional steps may be taken, in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="88190-128">Hello sezioni seguenti forniscono una descrizione dettagliata dei gruppi di sicurezza di rete e il relativo funzionamento per questo esempio, illustrando le righe di chiave hello dello script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88190-128">hello following sections provide a detailed description of Network Security Groups and how they function for this example by walking through key lines of hello PowerShell script.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="88190-129">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="88190-129">Network Security Groups (NSG)</span></span>
<span data-ttu-id="88190-130">Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono caricate sei regole.</span><span class="sxs-lookup"><span data-stu-id="88190-130">For this example, an NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="88190-131">In genere, si deve creare regole "Consenti" specifiche prima e quindi hello ultima più generico "Deny" regole.</span><span class="sxs-lookup"><span data-stu-id="88190-131">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="88190-132">Hello assegnata la priorità determina quali regole vengono valutate per prime.</span><span class="sxs-lookup"><span data-stu-id="88190-132">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="88190-133">Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole.</span><span class="sxs-lookup"><span data-stu-id="88190-133">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="88190-134">Possono essere applicate regole di gruppo in hello nella direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).</span><span class="sxs-lookup"><span data-stu-id="88190-134">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
> 
> 

<span data-ttu-id="88190-135">In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-135">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="88190-136">Il traffico DNS interno (porta 53) è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-136">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="88190-137">È consentito il traffico RDP (porta 3389) da hello Internet tooany VM</span><span class="sxs-lookup"><span data-stu-id="88190-137">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="88190-138">È consentito il traffico HTTP (porta 80) dal server di tooweb Internet hello (IIS01)</span><span class="sxs-lookup"><span data-stu-id="88190-138">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="88190-139">È consentito qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1</span><span class="sxs-lookup"><span data-stu-id="88190-139">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="88190-140">Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (entrambi subnet)</span><span class="sxs-lookup"><span data-stu-id="88190-140">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="88190-141">Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello subnet front-end hello negato</span><span class="sxs-lookup"><span data-stu-id="88190-141">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="88190-142">Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso dal server web toohello Internet hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata, ma poiché la regola 3 ha una priorità più alta solo esso viene applicato e regola 5 sarebbe non entrano in gioco.</span><span class="sxs-lookup"><span data-stu-id="88190-142">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="88190-143">Richiesta HTTP hello sarebbe è pertanto a server web toohello.</span><span class="sxs-lookup"><span data-stu-id="88190-143">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="88190-144">Se il traffico stesso cercava server DNS01 di hello tooreach, regola 5 (Nega) sarebbe hello prima tooapply hello il traffico e non sarebbe consentito toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="88190-144">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="88190-145">Regola 6 (Nega) Blocca subnet front-end hello dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4), il set di regole protegge rete back-end hello nel caso in cui un'utente malintenzionato compromette hello applicazione web sul front-end hello autore dell'attacco hello sarebbe non dispongono di accesso toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).</span><span class="sxs-lookup"><span data-stu-id="88190-145">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="88190-146">Una regola in uscita predefinito che consente il traffico in uscita toohello internet.</span><span class="sxs-lookup"><span data-stu-id="88190-146">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="88190-147">Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="88190-147">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="88190-148">toolock verso il basso il traffico in entrambe le direzioni, Routing definito dall'utente è obbligatorio e viene esaminata in "Esempio 3" in hello [pagina migliori procedure consigliate di sicurezza limite][HOME].</span><span class="sxs-lookup"><span data-stu-id="88190-148">toolock down traffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="88190-149">Ogni regola viene discusso in maggior dettaglio come indicato di seguito (**nota**: qualsiasi elemento nell'elenco a partire dal simbolo del dollaro seguito hello (ad esempio: $NSGName) è una variabile definita dall'utente da uno script di hello nella sezione di riferimento hello di questo documento):</span><span class="sxs-lookup"><span data-stu-id="88190-149">Each rule is discussed in more detail as follows (**Note**: any item in hello following list beginning with a dollar sign (for example: $NSGName) is a user-defined variable from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="88190-150">Un gruppo di sicurezza di rete devono essere compilato regole hello toohold:</span><span class="sxs-lookup"><span data-stu-id="88190-150">First a Network Security Group must be built toohold hello rules:</span></span>

    ```PowerShell
    New-AzureNetworkSecurityGroup -Name $NSGName `
        -Location $DeploymentLocation `
        -Label "Security group for $VNetName subnets in $DeploymentLocation"
    ```

2. <span data-ttu-id="88190-151">prima regola di Hello in questo esempio consente il traffico DNS tra tutti i server DNS di toohello reti interne nella subnet back-end hello.</span><span class="sxs-lookup"><span data-stu-id="88190-151">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="88190-152">regola di Hello include alcuni parametri importanti:</span><span class="sxs-lookup"><span data-stu-id="88190-152">hello rule has some important parameters:</span></span>
   
   * <span data-ttu-id="88190-153">"Type" indica in quale direzione del flusso di traffico verrà applicata questa regola.</span><span class="sxs-lookup"><span data-stu-id="88190-153">“Type” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="88190-154">direzione Hello è dal punto di vista di hello di subnet hello o macchina virtuale (in base a cui è associato questo gruppo).</span><span class="sxs-lookup"><span data-stu-id="88190-154">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="88190-155">Pertanto se il tipo è "Inbound" e traffico sta entrando in subnet hello, verrà applicata la regola hello e traffico lasciando subnet hello potrebbe non essere interessato da questa regola.</span><span class="sxs-lookup"><span data-stu-id="88190-155">Thus if Type is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
   * <span data-ttu-id="88190-156">"Priority" imposta hello l'ordine in cui viene valutato un flusso di traffico.</span><span class="sxs-lookup"><span data-stu-id="88190-156">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="88190-157">Hello hello numero hello superiore hello priorità inferiore.</span><span class="sxs-lookup"><span data-stu-id="88190-157">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="88190-158">Quando il flusso di traffico specifico tooa si applica una regola, non vengono elaborate ulteriori regole.</span><span class="sxs-lookup"><span data-stu-id="88190-158">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="88190-159">Pertanto se una regola con priorità 1 consente il traffico e una regola con priorità 2 impedisca il traffico, entrambe le regole si applicano tootraffic quindi sia possibile usare il traffico hello tooflow (poiché la regola 1 ha una priorità più alta da cui ha effetto e non altre regole sono state applicate).</span><span class="sxs-lookup"><span data-stu-id="88190-159">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
   * <span data-ttu-id="88190-160">"Action" indica se il traffico a cui si applica la regola viene bloccato o consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-160">“Action” signifies if traffic affected by this rule is blocked or allowed.</span></span>

    ```PowerShell    
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" `
        -Type Inbound -Priority 100 -Action Allow `
        -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[4] `
        -DestinationPortRange '53' `
        -Protocol *
    ```

3. <span data-ttu-id="88190-161">Questa regola consente di tooflow il traffico RDP da hello internet toohello la porta RDP in qualsiasi server in hello associato subnet.</span><span class="sxs-lookup"><span data-stu-id="88190-161">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> <span data-ttu-id="88190-162">La regola usa due tipi speciali di prefissi per l'indirizzo: "VIRTUAL_NETWORK" e "INTERNET",</span><span class="sxs-lookup"><span data-stu-id="88190-162">This rule uses two special types of address prefixes; “VIRTUAL_NETWORK” and “INTERNET.”</span></span> <span data-ttu-id="88190-163">Questi tag sono un tooaddress facilmente una categoria di dimensioni maggiore di prefissi di indirizzo.</span><span class="sxs-lookup"><span data-stu-id="88190-163">These tags are an easy way tooaddress a larger category of address prefixes.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable RDP too$VNetName VNet" `
         -Type Inbound -Priority 110 -Action Allow `
         -SourceAddressPrefix INTERNET -SourcePortRange '*' `
         -DestinationAddressPrefix VIRTUAL_NETWORK `
         -DestinationPortRange '3389' `
         -Protocol *
    ```

4. <span data-ttu-id="88190-164">Questa regola consente di server web in ingresso internet traffico toohit hello.</span><span class="sxs-lookup"><span data-stu-id="88190-164">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="88190-165">Questa regola non modifica il comportamento di routing hello.</span><span class="sxs-lookup"><span data-stu-id="88190-165">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="88190-166">regola di Hello consente solo il traffico destinato IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="88190-166">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="88190-167">Pertanto se il traffico proveniente da Internet hello disponesse di server web hello come destinazione di questa regola consente e arrestare l'elaborazione di altre regole.</span><span class="sxs-lookup"><span data-stu-id="88190-167">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="88190-168">(Regola hello priorità 140 tutte le altre traffico in ingresso internet è bloccato).</span><span class="sxs-lookup"><span data-stu-id="88190-168">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="88190-169">Se si sta elaborando solo il traffico HTTP, questa regola può essere ulteriormente limitato tooonly Consenti destinazione la porta 80.</span><span class="sxs-lookup"><span data-stu-id="88190-169">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
         Set-AzureNetworkSecurityRule -Name "Enable Internet too$VMName[0]" `
         -Type Inbound -Priority 120 -Action Allow `
         -SourceAddressPrefix Internet -SourcePortRange '*' `
         -DestinationAddressPrefix $VMIP[0] `
         -DestinationPortRange '*' `
         -Protocol *
    ```

5. <span data-ttu-id="88190-170">Questa regola consente il traffico toopass dal server IIS01 hello toohello AppVM01 server, una regola successiva blocca tutto il traffico tooBackend altri server front-end.</span><span class="sxs-lookup"><span data-stu-id="88190-170">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="88190-171">tooimprove questa regola, se la porta hello è noto che deve essere aggiunti.</span><span class="sxs-lookup"><span data-stu-id="88190-171">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="88190-172">Ad esempio, se il server IIS hello sta impegnando solo SQL Server in AppVM01, hello intervallo di porte di destinazione deve essere modificato da "*" (Any) too1433 (porta SQL Buongiorno) consentendo in tal modo una superficie di attacco in ingresso più piccola in AppVM01 deve hello web applicazione dovesse essere compromessa.</span><span class="sxs-lookup"><span data-stu-id="88190-172">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

    ```PowerShell
    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Enable $VMName[1] too$VMName[2]" `
        -Type Inbound -Priority 130 -Action Allow `
        -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
        -DestinationAddressPrefix $VMIP[2] `
        -DestinationPortRange '*' `
        -Protocol *
    ```

6. <span data-ttu-id="88190-173">Questa regola impedisce il traffico da hello internet tooany server hello rete.</span><span class="sxs-lookup"><span data-stu-id="88190-173">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="88190-174">Con regole di hello priorità 110 e 120, effetto hello è tooallow solo internet traffico toohello firewall in entrata e le porte RDP nel server e blocca tutto il resto.</span><span class="sxs-lookup"><span data-stu-id="88190-174">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="88190-175">Questa regola è "alternativo" regola tooblock tutti i flussi imprevisti.</span><span class="sxs-lookup"><span data-stu-id="88190-175">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>
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
7. <span data-ttu-id="88190-176">regola finale Hello impedisca il traffico dalla subnet di back-end toohello subnet front-end hello.</span><span class="sxs-lookup"><span data-stu-id="88190-176">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="88190-177">Poiché questa regola è una regola sola in ingresso, è consentito traffico inverso (da hello back-end toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="88190-177">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

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

## <a name="traffic-scenarios"></a><span data-ttu-id="88190-178">Scenari di traffico</span><span class="sxs-lookup"><span data-stu-id="88190-178">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="88190-179">(*Consentito*) server tooweb Internet</span><span class="sxs-lookup"><span data-stu-id="88190-179">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="88190-180">Un utente Internet richiede una pagina HTTP a FrontEnd001.CloudApp.Net (servizio cloud per Internet)</span><span class="sxs-lookup"><span data-stu-id="88190-180">An internet user requests an HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="88190-181">Traffico del servizio passa attraverso un endpoint aperto sulla porta 80 verso IIS01 cloud (server web hello)</span><span class="sxs-lookup"><span data-stu-id="88190-181">Cloud service passes traffic through open endpoint on port 80 towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="88190-182">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-182">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88190-183">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-183">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88190-184">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-184">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88190-185">Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="88190-185">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88190-186">Traffico raggiunge l'indirizzo IP interno del server web hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="88190-186">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="88190-187">Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello</span><span class="sxs-lookup"><span data-stu-id="88190-187">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="88190-188">Iis01 richiede SQL Server hello su AppVM01 per informazioni</span><span class="sxs-lookup"><span data-stu-id="88190-188">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="88190-189">Non essendoci regole in uscita sulla subnet front-end, il traffico è consentito</span><span class="sxs-lookup"><span data-stu-id="88190-189">Since there are no outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="88190-190">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-190">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88190-191">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-191">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88190-192">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-192">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88190-193">GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-193">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="88190-194">Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="88190-194">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="88190-195">AppVM01 riceve hello Query SQL e risponde</span><span class="sxs-lookup"><span data-stu-id="88190-195">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="88190-196">Poiché non esistono regole in uscita nella subnet back-end hello, risposta hello è consentito</span><span class="sxs-lookup"><span data-stu-id="88190-196">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="88190-197">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-197">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="88190-198">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="88190-198">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="88190-199">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-199">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="88190-200">server IIS Hello riceve risposta SQL hello e completa di risposta HTTP hello e invia toohello richiedente</span><span class="sxs-lookup"><span data-stu-id="88190-200">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requestor</span></span>
13. <span data-ttu-id="88190-201">Poiché non esistono regole in uscita nella subnet front-end hello hello risposta è consentita e hello internet viene visualizzata una pagina web hello richiesta.</span><span class="sxs-lookup"><span data-stu-id="88190-201">Since there are no outbound rules on hello Frontend subnet hello response is allowed, and hello internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-toobackend"></a><span data-ttu-id="88190-202">(*Consentito*) toobackend RDP</span><span class="sxs-lookup"><span data-stu-id="88190-202">(*Allowed*) RDP toobackend</span></span>
1. <span data-ttu-id="88190-203">Amministratore del server su internet richiede tooAppVM01 sessione RDP in BackEnd001.CloudApp.Net:xxxxx dove xxxxx è il numero di porta hello assegnato in modo casuale per RDP tooAppVM01 (porta hello assegnato è reperibile nel portale di Azure hello o tramite PowerShell)</span><span class="sxs-lookup"><span data-stu-id="88190-203">Server Admin on internet requests RDP session tooAppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is hello randomly assigned port number for RDP tooAppVM01 (hello assigned port can be found on hello Azure portal or via PowerShell)</span></span>
2. <span data-ttu-id="88190-204">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-204">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88190-205">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-205">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88190-206">Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="88190-206">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
3. <span data-ttu-id="88190-207">Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-207">With no outbound rules, default rules apply and return traffic is allowed</span></span>
4. <span data-ttu-id="88190-208">La sessione RDP è abilitata.</span><span class="sxs-lookup"><span data-stu-id="88190-208">RDP session is enabled</span></span>
5. <span data-ttu-id="88190-209">AppVM01 richiede la password e nome utente hello</span><span class="sxs-lookup"><span data-stu-id="88190-209">AppVM01 prompts for hello user name and password</span></span>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="88190-210">(*Consentito*) Ricerca DNS del server Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="88190-210">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="88190-211">Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.</span><span class="sxs-lookup"><span data-stu-id="88190-211">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="88190-212">Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01</span><span class="sxs-lookup"><span data-stu-id="88190-212">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="88190-213">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-213">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="88190-214">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-214">Backend subnet begins inbound rule processing:</span></span>
   * <span data-ttu-id="88190-215">Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="88190-215">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="88190-216">Server DNS riceve una richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="88190-216">DNS server receives hello request</span></span>
6. <span data-ttu-id="88190-217">Server DNS non dispone di indirizzo hello memorizzati nella cache e richiede un server radice DNS su hello internet</span><span class="sxs-lookup"><span data-stu-id="88190-217">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="88190-218">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-218">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="88190-219">Server DNS Internet risponde, poiché questa sessione è stata avviata internamente, la risposta hello è consentita</span><span class="sxs-lookup"><span data-stu-id="88190-219">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="88190-220">Server DNS memorizza nella cache la risposta hello e risponde toohello richiesta iniziale indietro tooIIS01</span><span class="sxs-lookup"><span data-stu-id="88190-220">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="88190-221">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-221">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="88190-222">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-222">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="88190-223">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="88190-223">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="88190-224">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito</span><span class="sxs-lookup"><span data-stu-id="88190-224">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="88190-225">Iis01 riceve risposta hello da DNS01</span><span class="sxs-lookup"><span data-stu-id="88190-225">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="88190-226">(*Consentito*) Il server Web richiede l'accesso a un file in AppVM01</span><span class="sxs-lookup"><span data-stu-id="88190-226">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="88190-227">IIS01 richiede un file in AppVM01.</span><span class="sxs-lookup"><span data-stu-id="88190-227">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="88190-228">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-228">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="88190-229">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-229">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88190-230">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-230">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88190-231">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-231">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88190-232">GRUPPO regola 3 (tooIIS01 Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-232">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="88190-233">Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="88190-233">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88190-234">AppVM01 riceve la richiesta di hello e risponde con il file (presupponendo che l'accesso è autorizzato)</span><span class="sxs-lookup"><span data-stu-id="88190-234">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="88190-235">Poiché non esistono regole in uscita nella subnet back-end hello, risposta hello è consentito</span><span class="sxs-lookup"><span data-stu-id="88190-235">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="88190-236">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-236">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88190-237">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="88190-237">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
   2. <span data-ttu-id="88190-238">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="88190-238">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="88190-239">server IIS Hello riceve file hello</span><span class="sxs-lookup"><span data-stu-id="88190-239">hello IIS server receives hello file</span></span>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="88190-240">(*Negato*) server toobackend Web</span><span class="sxs-lookup"><span data-stu-id="88190-240">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="88190-241">Un utente internet tenta tooaccess un file in AppVM01 tramite hello BackEnd001.CloudApp.Net servizio</span><span class="sxs-lookup"><span data-stu-id="88190-241">An internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="88190-242">Poiché non sono presenti endpoint aperto per la condivisione file, il traffico non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="88190-242">Since there are no endpoints open for file share, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="88190-243">Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico</span><span class="sxs-lookup"><span data-stu-id="88190-243">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="88190-244">(*Negato*) Ricerca DNS Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="88190-244">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="88190-245">Un utente internet tenta toolook di un record DNS interno nella DNS01 tramite hello BackEnd001.CloudApp.Net servizio</span><span class="sxs-lookup"><span data-stu-id="88190-245">An internet user tries toolook up an internal DNS record on DNS01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="88190-246">Poiché non sono presenti endpoint aperto per DNS, il traffico non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="88190-246">Since there are no endpoints open for DNS, this traffic would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="88190-247">Se gli endpoint hello erano aperti per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico (Nota: la regola 1 (DNS) potrebbero non applicarsi per due motivi, primo indirizzo di origine hello è hello internet, questa regola si applica solo a toohello anche rete locale virtuale come hello di origine Questa regola è una regola di assenso, in modo che non sarebbe mai negare il traffico)</span><span class="sxs-lookup"><span data-stu-id="88190-247">If hello endpoints were open for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first hello source address is hello internet, this rule only applies toohello local VNet as hello source, also this rule is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-toosql-access-through-firewall"></a><span data-ttu-id="88190-248">(*Negato*) Web tooSQL accesso tramite firewall</span><span class="sxs-lookup"><span data-stu-id="88190-248">(*Denied*) Web tooSQL access through firewall</span></span>
1. <span data-ttu-id="88190-249">Un utente Internet richiede dati SQL a FrontEnd001.CloudApp.Net (servizio cloud per Internet)</span><span class="sxs-lookup"><span data-stu-id="88190-249">An internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="88190-250">Poiché non sono presenti endpoint aperto per SQL, il traffico non raggiungerebbe hello servizio Cloud e non raggiunga firewall hello</span><span class="sxs-lookup"><span data-stu-id="88190-250">Since there are no endpoints open for SQL, this traffic would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="88190-251">Se gli endpoint sono stati aperti per qualche motivo, subnet front-end hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="88190-251">If endpoints were open for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="88190-252">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-252">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="88190-253">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="88190-253">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="88190-254">Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="88190-254">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="88190-255">Traffico raggiunge l'indirizzo IP interno di hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="88190-255">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="88190-256">Non è in ascolto sulla porta 1433, che non è più richiesta toohello risposta iis01</span><span class="sxs-lookup"><span data-stu-id="88190-256">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="88190-257">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="88190-257">Conclusion</span></span>
<span data-ttu-id="88190-258">Questo esempio è un modo semplice e relativamente semplice isolare subnet back-end hello dal traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="88190-258">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="88190-259">Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].</span><span class="sxs-lookup"><span data-stu-id="88190-259">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="88190-260">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="88190-260">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="88190-261">Script principale e configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="88190-261">Main script and network config</span></span>
<span data-ttu-id="88190-262">Salvare uno Script completo di hello in un file di script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="88190-262">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="88190-263">Salvare hello configurazione di rete in un file denominato "NetworkConf1.xml".</span><span class="sxs-lookup"><span data-stu-id="88190-263">Save hello Network Config into a file named “NetworkConf1.xml.”</span></span>
<span data-ttu-id="88190-264">Modificare le variabili definite dall'utente hello come script hello necessari e vengono eseguiti.</span><span class="sxs-lookup"><span data-stu-id="88190-264">Modify hello user-defined variables as needed and run hello script.</span></span>

#### <a name="full-script"></a><span data-ttu-id="88190-265">Script completo</span><span class="sxs-lookup"><span data-stu-id="88190-265">Full script</span></span>
<span data-ttu-id="88190-266">Questo script verrà, in base alle variabili definite dall'utente hello;</span><span class="sxs-lookup"><span data-stu-id="88190-266">This script will, based on hello user-defined variables;</span></span>

1. <span data-ttu-id="88190-267">Connettersi tooan sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="88190-267">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="88190-268">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="88190-268">Create a storage account</span></span>
3. <span data-ttu-id="88190-269">Creare una rete virtuale e due subnet, come definito nel file di configurazione di rete hello</span><span class="sxs-lookup"><span data-stu-id="88190-269">Create a VNet and two subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="88190-270">Compilare quattro macchine virtuali Windows Server</span><span class="sxs-lookup"><span data-stu-id="88190-270">Build four windows server VMs</span></span>
5. <span data-ttu-id="88190-271">Configurare il gruppo di sicurezza di rete eseguendo queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="88190-271">Configure NSG including:</span></span>
   * <span data-ttu-id="88190-272">Creazione di un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="88190-272">Creating an NSG</span></span>
   * <span data-ttu-id="88190-273">Inserimento delle regole.</span><span class="sxs-lookup"><span data-stu-id="88190-273">Populating it with rules</span></span>
   * <span data-ttu-id="88190-274">Subnet appropriata toohello associazione hello NSG</span><span class="sxs-lookup"><span data-stu-id="88190-274">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="88190-275">Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="88190-275">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88190-276">Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi.</span><span class="sxs-lookup"><span data-stu-id="88190-276">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="88190-277">Solo i messaggi di errore formattati in rosso possono indicare un problema.</span><span class="sxs-lookup"><span data-stu-id="88190-277">Only error messages in red are cause for concern.</span></span>
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

#### <a name="network-config-file"></a><span data-ttu-id="88190-278">File di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="88190-278">Network config file</span></span>
<span data-ttu-id="88190-279">Salvare il file xml con posizione aggiornata e aggiungere la variabile toohello $NetworkConfigFile hello link toothis file hello script precedente.</span><span class="sxs-lookup"><span data-stu-id="88190-279">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello preceding script.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="88190-280">Script di applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="88190-280">Sample application scripts</span></span>
<span data-ttu-id="88190-281">Se si desidera tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="88190-281">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="88190-282">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="88190-282">Next steps</span></span>
* <span data-ttu-id="88190-283">Aggiornare e salvare il file XML</span><span class="sxs-lookup"><span data-stu-id="88190-283">Update and save XML file</span></span>
* <span data-ttu-id="88190-284">Eseguire hello PowerShell script toobuild hello ambiente</span><span class="sxs-lookup"><span data-stu-id="88190-284">Run hello PowerShell script toobuild hello environment</span></span>
* <span data-ttu-id="88190-285">Installare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="88190-285">Install hello sample application</span></span>
* <span data-ttu-id="88190-286">Testare diversi flussi di traffico attraverso la rete perimetrale</span><span class="sxs-lookup"><span data-stu-id="88190-286">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-asm/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md

