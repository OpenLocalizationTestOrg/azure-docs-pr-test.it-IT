---
title: 'Esempio: aaaDMZ compilare tooProtect una rete Perimetrale reti con un Firewall, UDR e NSG | Documenti Microsoft'
description: Creare una rete perimetrale con un firewall, routing definito dall'utente e un gruppo di sicurezza di rete
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: dc01ccfb-27b0-4887-8f0b-2792f770ffff
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/01/2016
ms.author: jonor;sivae
ms.openlocfilehash: cc121f9cd5fe3c3e9ac2c70fbb7d982a80bb345d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="example-3--build-a-dmz-tooprotect-networks-with-a-firewall-udr-and-nsg"></a><span data-ttu-id="255ba-103">Esempio 3: compilazione tooProtect una rete Perimetrale reti con un Firewall, UDR e NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-103">Example 3 – Build a DMZ tooProtect Networks with a Firewall, UDR, and NSG</span></span>
<span data-ttu-id="255ba-104">[Restituire la pagina sicurezza limite Best Practices toohello][HOME]</span><span class="sxs-lookup"><span data-stu-id="255ba-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="255ba-105">Questo esempio illustra come creare una rete perimetrale con un firewall, quattro server Windows, routing definito dall'utente, inoltro IP e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="255ba-105">This example will create a DMZ with a firewall, four windows servers, User Defined Routing, IP Forwarding, and Network Security Groups.</span></span> <span data-ttu-id="255ba-106">Ogni tooprovide comandi rilevanti hello in modo dettagliato anche una comprensione più approfondita di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="255ba-106">It will also walk through each of hello relevant commands tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="255ba-107">È inoltre disponibile un Scenario di traffico sezione tooprovide un'analisi approfondita dettagliate come traffico procede attraverso i livelli di difesa hello hello rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="255ba-107">There is also a Traffic Scenario section tooprovide an in-depth step-by-step how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="255ba-108">Infine, nella sezione dei riferimenti hello è codice completo hello e istruzione toobuild questo ambiente tootest e sperimentare vari scenari.</span><span class="sxs-lookup"><span data-stu-id="255ba-108">Finally, in hello references section is hello complete code and instruction toobuild this environment tootest and experiment with various scenarios.</span></span> 

<span data-ttu-id="255ba-109">![Rete perimetrale bidirezionale con appliance virtuale di rete, gruppo di sicurezza di rete e routing definito dall'utente][1]</span><span class="sxs-lookup"><span data-stu-id="255ba-109">![Bi-directional DMZ with NVA, NSG, and UDR][1]</span></span>

## <a name="environment-setup"></a><span data-ttu-id="255ba-110">Configurazione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="255ba-110">Environment Setup</span></span>
<span data-ttu-id="255ba-111">In questo esempio è associata una sottoscrizione che contiene la seguente sintassi hello:</span><span class="sxs-lookup"><span data-stu-id="255ba-111">In this example there is a subscription that contains hello following:</span></span>

* <span data-ttu-id="255ba-112">Tre servizi cloud, "SecSvc001", "FrontEnd001" e "BackEnd001".</span><span class="sxs-lookup"><span data-stu-id="255ba-112">Three cloud services: “SecSvc001”, “FrontEnd001”, and “BackEnd001”</span></span>
* <span data-ttu-id="255ba-113">Una rete virtuale, "CorpNetwork", con tre subnet: "SecNet", "FrontEnd" e "BackEnd"</span><span class="sxs-lookup"><span data-stu-id="255ba-113">A Virtual Network “CorpNetwork”, with three subnets: “SecNet”, “FrontEnd”, and “BackEnd”</span></span>
* <span data-ttu-id="255ba-114">Un accessorio virtuale di rete, in questo esempio un firewall, connesso toohello SecNet subnet</span><span class="sxs-lookup"><span data-stu-id="255ba-114">A network virtual appliance, in this example a firewall, connected toohello SecNet subnet</span></span>
* <span data-ttu-id="255ba-115">Un server Windows che rappresenta un server Web applicazioni ("IIS01").</span><span class="sxs-lookup"><span data-stu-id="255ba-115">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="255ba-116">Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="255ba-116">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="255ba-117">Un server Windows che rappresenta un server DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="255ba-117">A Windows server that represents a DNS server (“DNS01”)</span></span>

<span data-ttu-id="255ba-118">Nella sezione dei riferimenti hello sotto è uno script di PowerShell che compilerà la maggior parte dell'ambiente hello descritto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="255ba-118">In hello references section below there is a PowerShell script that will build most of hello environment described above.</span></span> <span data-ttu-id="255ba-119">Macchine virtuali hello di compilazione e le reti virtuali, anche se vengono eseguite dallo script di esempio hello, non sono descritti in dettaglio in questo documento.</span><span class="sxs-lookup"><span data-stu-id="255ba-119">Building hello VMs and Virtual Networks, although are done by hello example script, are not described in detail in this document.</span></span>

<span data-ttu-id="255ba-120">ambiente di hello toobuild:</span><span class="sxs-lookup"><span data-stu-id="255ba-120">toobuild hello environment:</span></span>

1. <span data-ttu-id="255ba-121">Salvare file xml configurazione rete hello inclusi nella sezione dei riferimenti hello (aggiornata con i nomi, la posizione e scenario hello dato toomatch di indirizzi IP)</span><span class="sxs-lookup"><span data-stu-id="255ba-121">Save hello network config xml file included in hello references section (updated with names, location, and IP addresses toomatch hello given scenario)</span></span>
2. <span data-ttu-id="255ba-122">Le variabili utente di aggiornamento hello nello script di hello script toomatch hello ambiente hello è toobe eseguite (sottoscrizioni, nomi di servizio e così via)</span><span class="sxs-lookup"><span data-stu-id="255ba-122">Update hello user variables in hello script toomatch hello environment hello script is toobe run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="255ba-123">Eseguire script hello in PowerShell</span><span class="sxs-lookup"><span data-stu-id="255ba-123">Execute hello script in PowerShell</span></span>

<span data-ttu-id="255ba-124">**Nota**: area hello indicato nell'hello script di PowerShell deve corrispondere area hello indicato nel file xml di configurazione rete hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-124">**Note**: hello region signified in hello PowerShell script must match hello region signified in hello network configuration xml file.</span></span>

<span data-ttu-id="255ba-125">Una volta hello script viene eseguito correttamente può essere prelevato hello post-script come segue:</span><span class="sxs-lookup"><span data-stu-id="255ba-125">Once hello script runs successfully hello following post-script steps may be taken:</span></span>

1. <span data-ttu-id="255ba-126">Impostare le regole firewall hello, questa attività viene descritta in hello sezione seguente: descrizione della regola Firewall.</span><span class="sxs-lookup"><span data-stu-id="255ba-126">Set up hello firewall rules, this is covered in hello section below titled: Firewall Rule Description.</span></span>
2. <span data-ttu-id="255ba-127">Facoltativamente, nella sezione dei riferimenti hello sono due script tooset hello web server e il server di app con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="255ba-127">Optionally in hello references section are two scripts tooset up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span>

<span data-ttu-id="255ba-128">Una volta hello script viene eseguito correttamente le regole del firewall hello saranno necessario toobe completato, questo aspetto è illustrato nella sezione hello: regole del Firewall.</span><span class="sxs-lookup"><span data-stu-id="255ba-128">Once hello script runs successfully hello firewall rules will need toobe completed, this is covered in hello section titled: Firewall Rules.</span></span>

## <a name="user-defined-routing-udr"></a><span data-ttu-id="255ba-129">Routing definito dall'utente</span><span class="sxs-lookup"><span data-stu-id="255ba-129">User Defined Routing (UDR)</span></span>
<span data-ttu-id="255ba-130">Per impostazione predefinita, hello seguendo le route di sistema è definito come:</span><span class="sxs-lookup"><span data-stu-id="255ba-130">By default, hello following system routes are defined as:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.0.0/16}     VNETLocal                            Active   Default    
         {0.0.0.0/0}       Internet                             Active   Default    
         {10.0.0.0/8}      Null                                 Active   Default    
         {100.64.0.0/10}   Null                                 Active   Default    
         {172.16.0.0/12}   Null                                 Active   Default    
         {192.168.0.0/16}  Null                                 Active   Default

<span data-ttu-id="255ba-131">Hello VNETLocal è sempre prefissi di indirizzo hello definito di hello rete virtuale per tale rete specifico (ad esempio passerà da ' tooVNet di rete virtuale a seconda della modalità di definizione di ogni rete virtuale di specifiche).</span><span class="sxs-lookup"><span data-stu-id="255ba-131">hello VNETLocal is always hello defined address prefix(es) of hello VNet for that specific network (ie it will change from VNet tooVNet depending on how each specific VNet is defined).</span></span> <span data-ttu-id="255ba-132">route sistema rimanenti Hello sono statiche e predefiniti come illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="255ba-132">hello remaining system routes are static and default as above.</span></span>

<span data-ttu-id="255ba-133">Per priorità, le route vengono elaborate tramite il metodo di corrispondenza di prefisso più lunga (LPM) hello, pertanto hello più specifico route nella tabella di hello sarebbe applicare tooa indirizzo di destinazione specificato.</span><span class="sxs-lookup"><span data-stu-id="255ba-133">As for priority, routes are processed via hello Longest Prefix Match (LPM) method, thus hello most specific route in hello table would apply tooa given destination address.</span></span>

<span data-ttu-id="255ba-134">Pertanto, verrà indirizzato attraverso destinazione tooits di rete virtuale hello a causa di route 10.0.0.0/16 toohello traffico (ad esempio toohello DNS01 server 10.0.2.4) per la rete locale hello (10.0.0.0/16).</span><span class="sxs-lookup"><span data-stu-id="255ba-134">Therefore, traffic (for example toohello DNS01 server, 10.0.2.4) intended for hello local network (10.0.0.0/16) would be routed across hello VNet tooits destination due toohello 10.0.0.0/16 route.</span></span> <span data-ttu-id="255ba-135">In altre parole, per 10.0.2.4, hello 10.0.0.0/16 route è una route più specifico hello, anche se 0.0.0.0/0 e hello 10.0.0.0/8 inoltre possibile applicare, ma poiché sono meno specifici non influiscono sul traffico.</span><span class="sxs-lookup"><span data-stu-id="255ba-135">In other words, for 10.0.2.4, hello 10.0.0.0/16 route is hello most specific route, even though hello 10.0.0.0/8 and 0.0.0.0/0 also could apply, but since they are less specific they don’t affect this traffic.</span></span> <span data-ttu-id="255ba-136">Pertanto hello traffico too10.0.2.4 avrebbe un hop successivo della rete locale virtuale hello e indirizzare semplicemente toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="255ba-136">Thus hello traffic too10.0.2.4 would have a next hop of hello local VNet and simply route toohello destination.</span></span>

<span data-ttu-id="255ba-137">Se il traffico è stato creato, ad esempio 10.1.1.1, non applica route 10.0.0.0/16 hello, ma 10.0.0.0/8 hello sarebbe hello più specifico e il traffico hello sarebbe eliminato ("black holed") poiché l'hop successivo hello è Null.</span><span class="sxs-lookup"><span data-stu-id="255ba-137">If traffic was intended for 10.1.1.1 for example, hello 10.0.0.0/16 route wouldn’t apply, but hello 10.0.0.0/8 would be hello most specific, and this hello traffic would be dropped (“black holed”) since hello next hop is Null.</span></span> 

<span data-ttu-id="255ba-138">Se destinazione hello non è stato applicato tooany di prefissi Null hello o prefissi VNETLocal hello, quindi è necessario seguire hello meno specifico routing, 0.0.0.0/0 e indirizzato toohello Internet come hop successivo hello e pertanto il bordo di internet di Azure.</span><span class="sxs-lookup"><span data-stu-id="255ba-138">If hello destination didn’t apply tooany of hello Null prefixes or hello VNETLocal prefixes, then it would follow hello least specific route, 0.0.0.0/0 and be routed out toohello Internet as hello next hop and thus out Azure’s internet edge.</span></span>

<span data-ttu-id="255ba-139">Se sono presenti due prefissi identici nella tabella di route hello, hello Ecco ordine hello di preferenza in base all'attributo di "origine" hello route:</span><span class="sxs-lookup"><span data-stu-id="255ba-139">If there are two identical prefixes in hello route table, hello following is hello order of preference based on hello routes “source” attribute:</span></span>

1. <span data-ttu-id="255ba-140">"VirtualAppliance" = una tabella di Route definite dall'utente aggiunti manualmente toohello</span><span class="sxs-lookup"><span data-stu-id="255ba-140">"VirtualAppliance" = A User Defined Route manually added toohello table</span></span>
2. <span data-ttu-id="255ba-141">"VPNGateway" = una Route Dynamic BGP (se usato con le reti ibride), aggiunto da un protocollo di rete dinamiche, queste route potrebbero cambiare nel tempo come protocollo dinamica hello riflette automaticamente le modifiche apportate nella rete il peering</span><span class="sxs-lookup"><span data-stu-id="255ba-141">“VPNGateway” = A Dynamic Route (BGP when used with hybrid networks), added by a dynamic network protocol, these routes may change over time as hello dynamic protocol automatically reflects changes in peered network</span></span>
3. <span data-ttu-id="255ba-142">"Default" = hello sistema route, hello voci statiche hello e di rete virtuale locale, come illustrato nella tabella di route hello precedente.</span><span class="sxs-lookup"><span data-stu-id="255ba-142">“Default” = hello System Routes, hello local VNet and hello static entries as shown in hello route table above.</span></span>

> [!NOTE]
> <span data-ttu-id="255ba-143">È ora possibile usare l'utente definito Routing (UDR) con ExpressRoute e i gateway VPN tooforce in uscita e appliance virtuale di rete indirizzato tooa toobe (NVA) il traffico in ingresso tra più sedi locali.</span><span class="sxs-lookup"><span data-stu-id="255ba-143">You can now use User Defined Routing (UDR) with ExpressRoute and VPN Gateways tooforce outbound and inbound cross-premises traffic toobe routed tooa network virtual appliance (NVA).</span></span>
> 
> 

#### <a name="creating-hello-local-routes"></a><span data-ttu-id="255ba-144">Creazione di hello route locali</span><span class="sxs-lookup"><span data-stu-id="255ba-144">Creating hello local routes</span></span>
<span data-ttu-id="255ba-145">In questo esempio, sono necessarie due tabelle di routing, uno per le subnet front-end e back-end di hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-145">In this example, two routing tables are needed, one each for hello Frontend and Backend subnets.</span></span> <span data-ttu-id="255ba-146">Ogni tabella viene caricato con routing statico appropriato per hello subnet specificato.</span><span class="sxs-lookup"><span data-stu-id="255ba-146">Each table is loaded with static routes appropriate for hello given subnet.</span></span> <span data-ttu-id="255ba-147">A scopo di hello di questo esempio, ogni tabella dispone di tre delle route:</span><span class="sxs-lookup"><span data-stu-id="255ba-147">For hello purpose of this example, each table has three routes:</span></span>

1. <span data-ttu-id="255ba-148">Traffico della subnet locale senza Hop successivo definito tooallow subnet locale il traffico toobypass hello firewall</span><span class="sxs-lookup"><span data-stu-id="255ba-148">Local subnet traffic with no Next Hop defined tooallow local subnet traffic toobypass hello firewall</span></span>
2. <span data-ttu-id="255ba-149">Traffico di rete virtuale con un Hop successivo definito come firewall, si esegue l'override regola predefinita hello che consente di direttamente tooroute il traffico di rete virtuale locale</span><span class="sxs-lookup"><span data-stu-id="255ba-149">Virtual Network traffic with a Next Hop defined as firewall, this overrides hello default rule that allows local VNet traffic tooroute directly</span></span>
3. <span data-ttu-id="255ba-150">Il traffico rimanente tutti (0 o 0) con un Hop successivo è definito come hello firewall</span><span class="sxs-lookup"><span data-stu-id="255ba-150">All remaining traffic (0/0) with a Next Hop defined as hello firewall</span></span>

<span data-ttu-id="255ba-151">Una volta create le tabelle di routing hello sono subnet tootheir associato.</span><span class="sxs-lookup"><span data-stu-id="255ba-151">Once hello routing tables are created they are bound tootheir subnets.</span></span> <span data-ttu-id="255ba-152">Per la tabella routing subnet front-end hello, dopo aver creato e associato subnet toohello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="255ba-152">For hello Frontend subnet routing table, once created and bound toohello subnet should look like this:</span></span>

        Effective routes : 
         Address Prefix    Next hop type    Next hop IP address Status   Source     
         --------------    -------------    ------------------- ------   ------     
         {10.0.1.0/24}     VNETLocal                            Active 
         {10.0.0.0/16}     VirtualAppliance 10.0.0.4            Active    
         {0.0.0.0/0}       VirtualAppliance 10.0.0.4            Active


<span data-ttu-id="255ba-153">Per questo esempio, comandi vengono utilizzati toobuild tabella di route hello hello seguenti, aggiungere una route definita dall'utente e quindi associare subnet tooa tabella route di hello (nota; tutti gli elementi sotto a partire da un segno di dollaro (ad esempio: $BESubnet) sono variabili definite dall'utente da uno script di hello in Hello sezione di riferimento di questo documento):</span><span class="sxs-lookup"><span data-stu-id="255ba-153">For this example, hello following commands are used toobuild hello route table, add a user defined route, and then bind hello route table tooa subnet (Note; any items below beginning with a dollar sign (e.g.: $BESubnet) are user defined variables from hello script in hello reference section of this document):</span></span>

1. <span data-ttu-id="255ba-154">È necessario creare prima tabella di routing base hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-154">First hello base routing table must be created.</span></span> <span data-ttu-id="255ba-155">Questo frammento viene illustrato creare hello hello tabella per la subnet di back-end hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-155">This snippet shows hello creation of hello table for hello Backend subnet.</span></span> <span data-ttu-id="255ba-156">Nello script hello, per la subnet front-end hello viene creata anche una tabella corrispondente.</span><span class="sxs-lookup"><span data-stu-id="255ba-156">In hello script, a corresponding table is also created for hello Frontend subnet.</span></span>
   
     <span data-ttu-id="255ba-157">New-AzureRouteTable -Name $BERouteTableName \`</span><span class="sxs-lookup"><span data-stu-id="255ba-157">New-AzureRouteTable -Name $BERouteTableName \`</span></span>
   
         -Location $DeploymentLocation `
         -Label "Route table for $BESubnet subnet"
2. <span data-ttu-id="255ba-158">Una volta creata la tabella di route hello, è possibile aggiungere route definite dall'utente specifici.</span><span class="sxs-lookup"><span data-stu-id="255ba-158">Once hello route table is created, specific user defined routes can be added.</span></span> <span data-ttu-id="255ba-159">In questo frammento, (0.0.0.0/0) di tutto il traffico verrà instradato tramite dell'appliance virtuale hello (una variabile, $VMIP [0], viene utilizzato toopass in hello l'indirizzo IP assegnato al momento dell'appliance virtuale hello creato in precedenza in script hello).</span><span class="sxs-lookup"><span data-stu-id="255ba-159">In this snipped, all traffic (0.0.0.0/0) will be routed through hello virtual appliance (a variable, $VMIP[0], is used toopass in hello IP address assigned when hello virtual appliance was created earlier in hello script).</span></span> <span data-ttu-id="255ba-160">Nello script hello, viene anche creata una regola corrispondente nella tabella di hello front-end.</span><span class="sxs-lookup"><span data-stu-id="255ba-160">In hello script, a corresponding rule is also created in hello Frontend table.</span></span>
   
     <span data-ttu-id="255ba-161">Get-AzureRouteTable $BERouteTableName | \`</span><span class="sxs-lookup"><span data-stu-id="255ba-161">Get-AzureRouteTable $BERouteTableName | \`</span></span>
   
         Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
         -NextHopType VirtualAppliance `
         -NextHopIpAddress $VMIP[0]
3. <span data-ttu-id="255ba-162">Hello sopra la voce di route sostituiranno route di hello predefinita "0.0.0.0/0", ma regola 10.0.0.0/16 predefinita di hello ancora esistente che consente il traffico all'interno di hello rete virtuale tooroute direttamente toohello destinazione e non toohello dispositivo di rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="255ba-162">hello above route entry will override hello default "0.0.0.0/0" route, but hello default 10.0.0.0/16 rule still existing which would allow traffic within hello VNet tooroute directly toohello destination and not toohello Network Virtual Appliance.</span></span> <span data-ttu-id="255ba-163">toocorrect che questa regola di seguire hello comportamento deve essere aggiunto.</span><span class="sxs-lookup"><span data-stu-id="255ba-163">toocorrect this behavior hello follow rule must be added.</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
4. <span data-ttu-id="255ba-164">A questo punto è un toobe scelta effettuata.</span><span class="sxs-lookup"><span data-stu-id="255ba-164">At this point there is a choice toobe made.</span></span> <span data-ttu-id="255ba-165">Con hello sopra due route tutto il traffico verrà instradato toohello firewall per la valutazione, anche il traffico all'interno di una singola subnet.</span><span class="sxs-lookup"><span data-stu-id="255ba-165">With hello above two routes all traffic will route toohello firewall for assessment, even traffic within a single subnet.</span></span> <span data-ttu-id="255ba-166">Questo è preferibile, ma tooallow il traffico all'interno di un tooroute subnet locale senza coinvolgere firewall hello è possibile aggiungere una regola di terza, molto specifica.</span><span class="sxs-lookup"><span data-stu-id="255ba-166">This may be desired, however tooallow traffic within a subnet tooroute locally without involvement from hello firewall a third, very specific rule can be added.</span></span> <span data-ttu-id="255ba-167">Questa route stati che qualsiasi indirizzo destine per la subnet locale hello sufficiente route sono direttamente (NextHopType = VNETLocal).</span><span class="sxs-lookup"><span data-stu-id="255ba-167">This route states that any address destine for hello local subnet can just route there directly (NextHopType = VNETLocal).</span></span>
   
        Get-AzureRouteTable $BERouteTableName | `
            Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
5. <span data-ttu-id="255ba-168">Infine, con hello tabella di routing creati e popolati con una route definite dall'utente, hello tabella deve essere in ora subnet tooa associato.</span><span class="sxs-lookup"><span data-stu-id="255ba-168">Finally, with hello routing table created and populated with a user defined routes, hello table must now be bound tooa subnet.</span></span> <span data-ttu-id="255ba-169">Nello script hello, tabella di route hello front-end è anche associato toohello subnet front-end.</span><span class="sxs-lookup"><span data-stu-id="255ba-169">In hello script, hello front end route table is also bound toohello Frontend subnet.</span></span> <span data-ttu-id="255ba-170">Ecco uno script di associazione hello per subnet back-end hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-170">Here is hello binding script for hello back end subnet.</span></span>
   
     <span data-ttu-id="255ba-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span><span class="sxs-lookup"><span data-stu-id="255ba-171">Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName \`</span></span>
   
        -SubnetName $BESubnet `
        -RouteTableName $BERouteTableName

## <a name="ip-forwarding"></a><span data-ttu-id="255ba-172">Inoltro IP</span><span class="sxs-lookup"><span data-stu-id="255ba-172">IP Forwarding</span></span>
<span data-ttu-id="255ba-173">TooUDR una funzionalità complementare, è l'inoltro IP.</span><span class="sxs-lookup"><span data-stu-id="255ba-173">A companion feature tooUDR, is IP Forwarding.</span></span> <span data-ttu-id="255ba-174">Si tratta di un'impostazione in un dispositivo virtuale che consente il traffico tooreceive non specificamente indirizzati toohello dispositivo e quindi inoltrare tale destinazione finale tooits di traffico.</span><span class="sxs-lookup"><span data-stu-id="255ba-174">This is a setting on a Virtual Appliance that allows it tooreceive traffic not specifically addressed toohello appliance and then forward that traffic tooits ultimate destination.</span></span>

<span data-ttu-id="255ba-175">Ad esempio, se il traffico da AppVM01 server DNS01 toohello richiesta, UDR invierebbe questo firewall toohello.</span><span class="sxs-lookup"><span data-stu-id="255ba-175">As an example, if traffic from AppVM01 makes a request toohello DNS01 server, UDR would route this toohello firewall.</span></span> <span data-ttu-id="255ba-176">Con attivato l'inoltro IP, il traffico di hello per destinazione DNS01 hello (10.0.2.4) verrà accettato dal dispositivo hello (10.0.0.4) e quindi inoltrato da destinazione finale tooits (10.0.2.4).</span><span class="sxs-lookup"><span data-stu-id="255ba-176">With IP Forwarding enabled, hello traffic for hello DNS01 destination (10.0.2.4) will be accepted by hello appliance (10.0.0.4) and then forwarded tooits ultimate destination (10.0.2.4).</span></span> <span data-ttu-id="255ba-177">Senza l'inoltro IP attivato hello Firewall, il traffico verrebbe non accettato dal dispositivo hello anche se la tabella di route hello dispone di firewall hello come hop successivo hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-177">Without IP Forwarding enabled on hello Firewall, traffic would not be accepted by hello appliance even though hello route table has hello firewall as hello next hop.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="255ba-178">È critico tooremember tooenable l'inoltro IP in combinazione con il Routing definito dall'utente.</span><span class="sxs-lookup"><span data-stu-id="255ba-178">It’s critical tooremember tooenable IP Forwarding in conjunction with User Defined Routing.</span></span>
> 
> 

<span data-ttu-id="255ba-179">La configurazione dell'inoltro IP è costituita da un singolo comando e può essere eseguita al momento della creazione della macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="255ba-179">Setting up IP Forwarding is a single command and can be done at VM creation time.</span></span> <span data-ttu-id="255ba-180">In hello flusso di questo frammento di codice di esempio hello verso la fine hello dello script hello è raggruppato con comandi UDR hello:</span><span class="sxs-lookup"><span data-stu-id="255ba-180">For hello flow of this example hello code snippet is towards hello end of hello script and grouped with hello UDR commands:</span></span>

1. <span data-ttu-id="255ba-181">Chiamare l'istanza di VM hello del dispositivo virtuale, hello in questo caso i firewall e attivare l'inoltro IP (nota; qualsiasi elemento in rosso a partire da un segno di dollaro (ad esempio: $VMName[0]) è una variabile definita dall'utente da uno script di hello nella sezione di riferimento hello di questo documento.</span><span class="sxs-lookup"><span data-stu-id="255ba-181">Call hello VM instance that is your virtual appliance, hello firewall in this case, and enable IP Forwarding (Note; any item in red beginning with a dollar sign (e.g.: $VMName[0]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="255ba-182">Hello zero tra parentesi quadre, [0] rappresenta hello prima VM nella matrice hello di macchine virtuali, per toowork di script di esempio hello senza alcuna modifica, hello prima macchina virtuale (VM 0) deve essere hello firewall):</span><span class="sxs-lookup"><span data-stu-id="255ba-182">hello zero in brackets, [0], represents hello first VM in hello array of VMs, for hello example script toowork without modification, hello first VM (VM 0) must be hello firewall):</span></span>
   
     <span data-ttu-id="255ba-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span><span class="sxs-lookup"><span data-stu-id="255ba-183">Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] | \`</span></span>
   
        Set-AzureIPForwarding -Enable

## <a name="network-security-groups-nsg"></a><span data-ttu-id="255ba-184">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="255ba-184">Network Security Groups (NSG)</span></span>
<span data-ttu-id="255ba-185">In questo esempio viene creato un gruppo di sicurezza di rete, in cui viene poi caricata una singola regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-185">In this example, a NSG group is built and then loaded with a single rule.</span></span> <span data-ttu-id="255ba-186">Questo gruppo viene quindi associato solo toohello front-end e back-end nelle subnet (non hello SecNet).</span><span class="sxs-lookup"><span data-stu-id="255ba-186">This group is then bound only toohello Frontend and Backend subnets (not hello SecNet).</span></span> <span data-ttu-id="255ba-187">Viene compilato in modo dichiarativo hello seguente regola:</span><span class="sxs-lookup"><span data-stu-id="255ba-187">Declaratively hello following rule is being built:</span></span>

1. <span data-ttu-id="255ba-188">Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (tutte le subnet)</span><span class="sxs-lookup"><span data-stu-id="255ba-188">Any traffic (all ports) from hello Internet toohello entire VNet (all subnets) is Denied</span></span>

<span data-ttu-id="255ba-189">Anche se in questo esempio vengono usati i gruppi di sicurezza di rete, lo scopo principale consiste nel creare un secondo livello di difesa contro errori di configurazione manuale.</span><span class="sxs-lookup"><span data-stu-id="255ba-189">Although NSGs are used in this example, it’s main purpose is as a secondary layer of defense against manual misconfiguration.</span></span> <span data-ttu-id="255ba-190">Vogliamo tooblock traffico tutto in ingresso da hello tooeither tramite internet hello front-end o subnet di back-end, il traffico solo flusso tramite firewall toohello di subnet SecNet hello (e quindi, se appropriata in toohello front-end o back-end subnet).</span><span class="sxs-lookup"><span data-stu-id="255ba-190">We want tooblock all inbound traffic from hello internet tooeither hello Frontend or Backend subnets, traffic should only flow through hello SecNet subnet toohello firewall (and then if appropriate on toohello Frontend or Backend subnets).</span></span> <span data-ttu-id="255ba-191">Inoltre, con regole UDR hello sul posto, tutto il traffico che in hello subnet front-end o back-end sarebbe indirizzato out toohello firewall (grazie tooUDR).</span><span class="sxs-lookup"><span data-stu-id="255ba-191">Plus, with hello UDR rules in place, any traffic that did make it into hello Frontend or Backend subnets would be directed out toohello firewall (thanks tooUDR).</span></span> <span data-ttu-id="255ba-192">firewall Hello verrà visualizzato come un flusso asimmetrico e riduzione in caso di traffico in uscita hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-192">hello firewall would see this as an asymmetric flow and would drop hello outbound traffic.</span></span> <span data-ttu-id="255ba-193">In questo modo sono disponibili tre livelli di hello protezione sicurezza front-end e back-end subnet; 1) senza aprire gli endpoint in hello FrontEnd001 e servizi cloud BackEnd001, 2) NSGs negare il traffico da Internet, firewall hello 3) eliminazione traffico asimmetrico di hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-193">Thus there are three layers of security protecting hello Frontend and Backend subnets; 1) no open endpoints on hello FrontEnd001 and BackEnd001 cloud services, 2) NSGs denying traffic from hello Internet, 3) hello firewall dropping asymmetric traffic.</span></span>

<span data-ttu-id="255ba-194">Un punto di interesse riguardanti hello il gruppo di sicurezza di rete in questo esempio è che contenga una sola regola, illustrata di seguito, ovvero toodeny internet traffico toohello intera rete virtuale che comprende subnet sicurezza hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-194">One interesting point regarding hello Network Security Group in this example is that it contains only one rule, shown below, which is toodeny internet traffic toohello entire virtual network which would include hello Security subnet.</span></span> 

    Get-AzureNetworkSecurityGroup -Name $NSGName | `
        Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet `
        from hello Internet" `
        -Type Inbound -Priority 100 -Action Deny `
        -SourceAddressPrefix INTERNET -SourcePortRange '*' `
        -DestinationAddressPrefix VIRTUAL_NETWORK `
        -DestinationPortRange '*' `
        -Protocol *

<span data-ttu-id="255ba-195">Tuttavia, poiché hello è solo di gruppo associata toohello front-end e back-end subnet, hello regola non è elaborata sul traffico in ingresso toohello subnet di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="255ba-195">However, since hello NSG is only bound toohello Frontend and Backend subnets, hello rule isn’t processed on traffic inbound toohello Security subnet.</span></span> <span data-ttu-id="255ba-196">Di conseguenza, anche se regola gruppo hello è indicato alcun indirizzo di tooany il traffico Internet nella rete virtuale, hello perché non è mai stata NSG hello associato subnet sicurezza toohello traffico verrà instradato toohello subnet di sicurezza.</span><span class="sxs-lookup"><span data-stu-id="255ba-196">As a result, even though hello NSG rule says no Internet traffic tooany address on hello VNet, because hello NSG was never bound toohello Security subnet, traffic will flow toohello Security subnet.</span></span>

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $FESubnet -VirtualNetworkName $VNetName

    Set-AzureNetworkSecurityGroupToSubnet -Name $NSGName `
        -SubnetName $BESubnet -VirtualNetworkName $VNetName

## <a name="firewall-rules"></a><span data-ttu-id="255ba-197">Regole del firewall</span><span class="sxs-lookup"><span data-stu-id="255ba-197">Firewall Rules</span></span>
<span data-ttu-id="255ba-198">Regole di inoltro sul firewall hello, saranno necessario toobe creato.</span><span class="sxs-lookup"><span data-stu-id="255ba-198">On hello firewall, forwarding rules will need toobe created.</span></span> <span data-ttu-id="255ba-199">Poiché firewall hello è traffico di blocco o inoltro tutto in ingresso, uscita e all'interno della rete virtuale sono necessarie numerose regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="255ba-199">Since hello firewall is blocking or forwarding all inbound, outbound, and intra-VNet traffic many firewall rules are needed.</span></span> <span data-ttu-id="255ba-200">Inoltre, tutto il traffico in ingresso verrà raggiunto l'indirizzo IP pubblico del servizio di sicurezza hello (su porte diverse), toobe elaborati dal firewall hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-200">Also, all inbound traffic will hit hello Security Service public IP address (on different ports), toobe processed by hello firewall.</span></span> <span data-ttu-id="255ba-201">Consiglia di flussi logici di hello toodiagram prima di configurare le subnet hello e variazioni tooavoid di regole firewall in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="255ba-201">A best practice is toodiagram hello logical flows before setting up hello subnets and firewall rules tooavoid rework later.</span></span> <span data-ttu-id="255ba-202">Hello nella figura seguente è una vista logica hello regole del firewall per questo esempio:</span><span class="sxs-lookup"><span data-stu-id="255ba-202">hello following figure is a logical view of hello firewall rules for this example:</span></span>

<span data-ttu-id="255ba-203">![Vista logica di hello regole del Firewall][2]</span><span class="sxs-lookup"><span data-stu-id="255ba-203">![Logical View of hello Firewall Rules][2]</span></span>

> [!NOTE]
> <span data-ttu-id="255ba-204">In base a hello che Appliance virtuale di rete utilizzato, porte di gestione di hello possono variare.</span><span class="sxs-lookup"><span data-stu-id="255ba-204">Based on hello Network Virtual Appliance used, hello management ports will vary.</span></span> <span data-ttu-id="255ba-205">In questo esempio si fa riferimento a Barracuda NextGen Firewall, che usa le porte 22, 801 e 807.</span><span class="sxs-lookup"><span data-stu-id="255ba-205">In this example a Barracuda NextGen Firewall is referenced which uses ports 22, 801, and 807.</span></span> <span data-ttu-id="255ba-206">Consultare hello accessorio fornitore documentazione toofind hello esatta porte utilizzate per la gestione dei dispositivi hello in uso.</span><span class="sxs-lookup"><span data-stu-id="255ba-206">Please consult hello appliance vendor documentation toofind hello exact ports used for management of hello device being used.</span></span>
> 
> 

### <a name="logical-rule-description"></a><span data-ttu-id="255ba-207">Descrizione della regola logica</span><span class="sxs-lookup"><span data-stu-id="255ba-207">Logical Rule Description</span></span>
<span data-ttu-id="255ba-208">Nel diagramma logico hello sopra, subnet sicurezza hello non viene visualizzato perché firewall hello è l'unica risorsa di hello subnet e questo diagramma verrà visualizzati le regole del firewall hello e come essi logicamente consentire o negare i flussi di traffico e non hello indirizzato percorso effettivo.</span><span class="sxs-lookup"><span data-stu-id="255ba-208">In hello logical diagram above, hello security subnet is not shown since hello firewall is hello only resource on that subnet, and this diagram is showing hello firewall rules and how they logically allow or deny traffic flows and not hello actual routed path.</span></span> <span data-ttu-id="255ba-209">Inoltre, due ottetti dell'indirizzo IP locale hello per facilitarne la lettura dell'ultima porte hello selezionate per il traffico RDP hello sono porte nell'intervallo superiore (8014 – 8026) e sono stati selezionati toosomewhat allinearlo hello (ad esempio indirizzo del server locale 10.0.1.4 è associato porta esterna 8014), tuttavia possibile utilizzare qualsiasi porta superiore non in conflitto.</span><span class="sxs-lookup"><span data-stu-id="255ba-209">Also, hello external ports selected for hello RDP traffic are higher ranged ports (8014 – 8026) and were selected toosomewhat align with hello last two octets of hello local IP address for easier readability (e.g. local server address 10.0.1.4 is associated with external port 8014), however any higher non-conflicting ports could be used.</span></span>

<span data-ttu-id="255ba-210">Per questo esempio sono necessari 7 tipi di regole, ovvero:</span><span class="sxs-lookup"><span data-stu-id="255ba-210">For this example, we need 7 types of rules, these rule types are described as follows:</span></span>

* <span data-ttu-id="255ba-211">Regole esterne (per il traffico in ingresso):</span><span class="sxs-lookup"><span data-stu-id="255ba-211">External Rules (for inbound traffic):</span></span>
  1. <span data-ttu-id="255ba-212">Regola Del firewall Management: Questa regola di reindirizzamento App consente porte di gestione del traffico toopass toohello dell'appliance virtuale di rete hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-212">Firewall Management Rule: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance.</span></span>
  2. <span data-ttu-id="255ba-213">Le regole di RDP (per ogni server di windows): queste quattro regole (uno per ogni server) consente la gestione di hello singoli server tramite RDP.</span><span class="sxs-lookup"><span data-stu-id="255ba-213">RDP Rules (for each windows server): These four rules (one for each server) will allow management of hello individual servers via RDP.</span></span> <span data-ttu-id="255ba-214">Questo potrebbe anche essere inserito in una regola a seconda delle funzionalità di hello di hello dispositivo di rete virtuale in uso.</span><span class="sxs-lookup"><span data-stu-id="255ba-214">This could also be bundled into one rule depending on hello capabilities of hello Network Virtual Appliance being used.</span></span>
  3. <span data-ttu-id="255ba-215">Regole del traffico di applicazione: Esistono due regole del traffico dell'applicazione hello prima per il traffico web front-end di hello e hello secondo per il traffico di back-end hello (ad esempio server toodata livello web).</span><span class="sxs-lookup"><span data-stu-id="255ba-215">Application Traffic Rules: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="255ba-216">configurazione di Hello di queste regole dipenderà dall'architettura di rete hello (in cui vengono collocati i server) e flussi di traffico (il tipo di traffico hello direzione flussi e le porte utilizzate).</span><span class="sxs-lookup"><span data-stu-id="255ba-216">hello configuration of these rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
     * <span data-ttu-id="255ba-217">prima regola Hello consentirà hello effettivo traffico tooreach hello applicazione server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="255ba-217">hello first rule will allow hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="255ba-218">Mentre hello altre regole consentono per la sicurezza, gestione, e così via, le regole di applicazione sono tooaccess utenti o servizi esterni quali consentire applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-218">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="255ba-219">Per questo esempio, non esiste un singolo server web sulla porta 80, pertanto una singola applicazione regola del firewall reindirizzerà il traffico in entrata toohello IP esterno, indirizzo IP interno di toohello web server.</span><span class="sxs-lookup"><span data-stu-id="255ba-219">For this example, there is a single web server on port 80, thus a single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span> <span data-ttu-id="255ba-220">Hello reindirizzato sessione traffico potrebbe essere stato NAT toohello interno del server.</span><span class="sxs-lookup"><span data-stu-id="255ba-220">hello redirected traffic session would be NAT’d toohello internal server.</span></span>
     * <span data-ttu-id="255ba-221">seconda regola del traffico di applicazione è Hello hello tootalk toohello AppVM01 server di back-end regola tooallow hello Server Web (ma non AppVM02) tramite qualsiasi porta.</span><span class="sxs-lookup"><span data-stu-id="255ba-221">hello second Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via any port.</span></span>
* <span data-ttu-id="255ba-222">Regole interne (per il traffico tra reti virtuali)</span><span class="sxs-lookup"><span data-stu-id="255ba-222">Internal Rules (for intra-VNet traffic)</span></span>
  1. <span data-ttu-id="255ba-223">Regola di tooInternet in uscita: questa regola consentirà il traffico da qualsiasi rete toopass toohello selezionato reti.</span><span class="sxs-lookup"><span data-stu-id="255ba-223">Outbound tooInternet Rule: This rule will allow traffic from any network toopass toohello selected networks.</span></span> <span data-ttu-id="255ba-224">Questa regola è in genere una regola predefinita già installati nel firewall hello, ma in uno stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="255ba-224">This rule is usually a default rule already on hello firewall, but in a disabled state.</span></span> <span data-ttu-id="255ba-225">È consigliabile abilitarla per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="255ba-225">This rule should be enabled for this example.</span></span>
  2. <span data-ttu-id="255ba-226">Regola DNS: Questa regola consente solo DNS (porta 53) traffico toopass toohello server DNS.</span><span class="sxs-lookup"><span data-stu-id="255ba-226">DNS Rule: This rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="255ba-227">Per questo ambiente che maggior parte del traffico da hello front-end toohello back-end è bloccata, questa regola consente DNS in modo specifico da una qualsiasi subnet locale.</span><span class="sxs-lookup"><span data-stu-id="255ba-227">For this environment most traffic from hello Frontend toohello Backend is blocked, this rule specifically allows DNS from any local subnet.</span></span>
  3. <span data-ttu-id="255ba-228">Subnet tooSubnet regola: questa regola è tooallow qualsiasi server in back hello terminare server tooany tooconnect di subnet nella subnet front-end hello (ma non hello inversa).</span><span class="sxs-lookup"><span data-stu-id="255ba-228">Subnet tooSubnet Rule: This rule is tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet (but not hello reverse).</span></span>
* <span data-ttu-id="255ba-229">Regola alternativo (per il traffico che non soddisfa uno qualsiasi dei hello precedente):</span><span class="sxs-lookup"><span data-stu-id="255ba-229">Fail-safe Rule (for traffic that doesn’t meet any of hello above):</span></span>
  1. <span data-ttu-id="255ba-230">Nega tutte le regole di traffico: Questo deve essere sempre regola finale di hello (in termini di priorità) e di conseguenza un traffico flussi avrà esito negativo toomatch qualsiasi hello precedenti regole che verranno eliminati da questa regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-230">Deny All Traffic Rule: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="255ba-231">Questa è una regola predefinita ed è solitamente attivata, quindi non sono in genere necessarie modifiche.</span><span class="sxs-lookup"><span data-stu-id="255ba-231">This is a default rule and usually activated, no modifications are generally needed.</span></span>

> [!TIP]
> <span data-ttu-id="255ba-232">Regola di traffico applicazione secondo hello, qualsiasi porta è consentita per semplice di questo esempio, in un hello uno scenario reale più specifici intervalli di porte e indirizzi devono essere utilizzato tooreduce superficie di attacco hello di questa regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-232">On hello second application traffic rule, any port is allowed for easy of this example, in a real scenario hello most specific port and address ranges should be used tooreduce hello attack surface of this rule.</span></span>
> 
> 

<br />

> [!IMPORTANT]
> <span data-ttu-id="255ba-233">Una volta tutte hello sopra le regole vengono create, è importante priorità hello tooreview del traffico di tooensure ogni regola verrà consentita o negata in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="255ba-233">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="255ba-234">Per questo esempio, le regole di hello sono in ordine di priorità.</span><span class="sxs-lookup"><span data-stu-id="255ba-234">For this example, hello rules are in priority order.</span></span> <span data-ttu-id="255ba-235">È facile toobe bloccati dal firewall hello a causa di regole ordinate toomis.</span><span class="sxs-lookup"><span data-stu-id="255ba-235">It's easy toobe locked out of hello firewall due toomis-ordered rules.</span></span> <span data-ttu-id="255ba-236">Come minimo, verificare che Gestione hello per firewall hello stesso sia sempre assoluto regola priorità più alta hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-236">At a minimum, ensure hello management for hello firewall itself is always hello absolute highest priority rule.</span></span>
> 
> 

### <a name="rule-prerequisites"></a><span data-ttu-id="255ba-237">Prerequisiti delle regole</span><span class="sxs-lookup"><span data-stu-id="255ba-237">Rule Prerequisites</span></span>
<span data-ttu-id="255ba-238">Uno dei prerequisiti per i firewall di hello hello macchina virtuale in esecuzione sono endpoint pubblici.</span><span class="sxs-lookup"><span data-stu-id="255ba-238">One prerequisite for hello Virtual Machine running hello firewall are public endpoints.</span></span> <span data-ttu-id="255ba-239">Per il traffico di hello firewall tooprocess endpoint pubblici appropriato hello deve essere aperto.</span><span class="sxs-lookup"><span data-stu-id="255ba-239">For hello firewall tooprocess traffic hello appropriate public endpoints must be open.</span></span> <span data-ttu-id="255ba-240">Esistono tre tipi di traffico in questo esempio; 1) Gestione traffico toocontrol hello firewall e le regole del firewall, server di windows hello toocontrol il traffico RDP 2) e il traffico di 3) dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="255ba-240">There are three types of traffic in this example; 1) Management traffic toocontrol hello firewall and firewall rules, 2) RDP traffic toocontrol hello windows servers, and 3) Application Traffic.</span></span> <span data-ttu-id="255ba-241">Questi includono hello tre colonne di tipi di traffico in hello superiore metà della vista logica delle regole del firewall hello sopra.</span><span class="sxs-lookup"><span data-stu-id="255ba-241">These are hello three columns of traffic types in hello upper half of logical view of hello firewall rules above.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="255ba-242">Una chiave takeway qui è tooremember che **tutti** proverrà il traffico attraverso il firewall hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-242">A key takeway here is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="255ba-243">Così tooremote desktop toohello IIS01 server, anche se è in servizio di Cloud Front-End hello e sulla subnet Front-End hello, tooaccess dobbiamo tooRDP toohello firewall sul server porta 8014 e attendere la richiesta RDP hello firewall tooroute hello internamente la porta RDP IIS01 toohello.</span><span class="sxs-lookup"><span data-stu-id="255ba-243">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="255ba-244">Hello "Connetti" del portale di Azure pulsante non funzionerà poiché non esiste alcun diretto tooIIS01 percorso RDP (per quanto possibile vedere portale hello).</span><span class="sxs-lookup"><span data-stu-id="255ba-244">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="255ba-245">Ciò significa che tutte le connessioni da hello internet sarà toohello servizio di sicurezza e una porta, ad esempio secscv001.cloudapp.net:xxxx (Buongiorno riferimento diagramma per il mapping di porta esterna e indirizzo IP interno e porta hello).</span><span class="sxs-lookup"><span data-stu-id="255ba-245">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx (reference hello above diagram for hello mapping of External Port and Internal IP and Port).</span></span>
> 
> 

<span data-ttu-id="255ba-246">Un endpoint può essere aperto sia in fase di creazione della macchina virtuale di hello o post-compilazione come viene eseguita in uno script di esempio hello e illustrato di seguito in questo frammento di codice (nota; qualsiasi elemento che inizia con un segno di dollaro (ad esempio: $VMName[$i]) è una variabile definita dall'utente da uno script di hello in hello referen sezione di stima di cardinalità di questo documento.</span><span class="sxs-lookup"><span data-stu-id="255ba-246">An endpoint can be opened either at hello time of VM creation or post build as is done in hello example script and shown below in this code snippet (Note; any item beginning with a dollar sign (e.g.: $VMName[$i]) is a user defined variable from hello script in hello reference section of this document.</span></span> <span data-ttu-id="255ba-247">Hello "$i" tra parentesi quadre, [$i], rappresenta il numero di matrice hello di una macchina virtuale specifica in una matrice di macchine virtuali):</span><span class="sxs-lookup"><span data-stu-id="255ba-247">hello “$i” in brackets, [$i], represents hello array number of a specific VM in an array of VMs):</span></span>

    Add-AzureEndpoint -Name "HTTP" -Protocol tcp -PublicPort 80 -LocalPort 80 `
        -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | `
        Update-AzureVM

<span data-ttu-id="255ba-248">Anche se non è chiaramente indicato qui di scadenza toohello utilizzo di variabili, ma gli endpoint sono **solo** aperto su hello servizio Cloud di protezione.</span><span class="sxs-lookup"><span data-stu-id="255ba-248">Although not clearly shown here due toohello use of variables, but endpoints are **only** opened on hello Security Cloud Service.</span></span> <span data-ttu-id="255ba-249">Si tratta di tooensure che tutto il traffico in ingresso viene gestito (indirizzati NAT aveva eliminate) da firewall hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-249">This is tooensure that all inbound traffic is handled (routed, NAT'd, dropped) by hello firewall.</span></span>

<span data-ttu-id="255ba-250">Un client di gestione sarà necessario toobe installato su un firewall di hello toomanage PC e creare configurazioni di hello necessarie.</span><span class="sxs-lookup"><span data-stu-id="255ba-250">A management client will need toobe installed on a PC toomanage hello firewall and create hello configurations needed.</span></span> <span data-ttu-id="255ba-251">Vedere fornitore documentazione fornita dal firewall (o altri NVA) hello in modo toomanage hello dispositivo.</span><span class="sxs-lookup"><span data-stu-id="255ba-251">See hello documentation from your firewall (or other NVA) vendor on how toomanage hello device.</span></span> <span data-ttu-id="255ba-252">resto Hello di questa sezione e la sezione successiva di hello, la creazione delle regole Firewall, descriverà configurazione hello del firewall hello stesso, tramite il client Gestione fornitori hello (ossia, non hello portale di Azure o PowerShell).</span><span class="sxs-lookup"><span data-stu-id="255ba-252">hello remainder of this section and hello next section, Firewall Rules Creation, will describe hello configuration of hello firewall itself, through hello vendors management client (i.e. not hello Azure portal or PowerShell).</span></span>

<span data-ttu-id="255ba-253">Istruzioni per il download di client e connessione toohello Barracuda utilizzato in questo esempio sono disponibili qui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="255ba-253">Instructions for client download and connecting toohello Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="255ba-254">Una volta effettuato l'accesso nel firewall hello ma prima di creare regole del firewall, sono disponibili due classi di oggetti dei prerequisiti che possono semplificare la Creazione regole di hello; Oggetti di rete e del servizio.</span><span class="sxs-lookup"><span data-stu-id="255ba-254">Once logged onto hello firewall but before creating firewall rules, there are two prerequisite object classes that can make creating hello rules easier; Network & Service objects.</span></span>

<span data-ttu-id="255ba-255">Per questo esempio, tre gli oggetti di rete denominata devono essere definito (uno per la subnet front-end hello e subnet di back-end hello, anche un oggetto di rete per l'indirizzo IP di hello del server DNS hello).</span><span class="sxs-lookup"><span data-stu-id="255ba-255">For this example, three named network objects should be defined (one for hello Frontend subnet and hello Backend subnet, also a network object for hello IP address of hello DNS server).</span></span> <span data-ttu-id="255ba-256">toocreate rete denominata. a partire dal dashboard di hello Barracuda NG amministratore client, passare scheda Configurazione toohello, nella sezione di configurazione Operational hello fare clic su set di regole, fare clic su "Reti" nel menu di hello oggetti Firewall, quindi fare clic su Nuovo dal menu Modifica reti hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-256">toocreate a named network; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Networks” under hello Firewall Objects menu, then click New in hello Edit Networks menu.</span></span> <span data-ttu-id="255ba-257">oggetto di rete Hello è ora possibile creare, mediante l'aggiunta di hello nome e un prefisso di hello:</span><span class="sxs-lookup"><span data-stu-id="255ba-257">hello network object can now be created, by adding hello name and hello prefix:</span></span>

<span data-ttu-id="255ba-258">![Creare un oggetto di rete di front-end][3]</span><span class="sxs-lookup"><span data-stu-id="255ba-258">![Create a FrontEnd Network Object][3]</span></span>

<span data-ttu-id="255ba-259">Verrà creata una rete per la subnet front-end hello denominata, deve creare un oggetto simile per la subnet di back-end hello anche.</span><span class="sxs-lookup"><span data-stu-id="255ba-259">This will create a named network for hello FrontEnd subnet, a similar object should be created for hello BackEnd subnet as well.</span></span> <span data-ttu-id="255ba-260">Subnet hello ora possibile fare riferimento più facilmente in base al nome regole di firewall hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-260">Now hello subnets can be more easily referenced by name in hello firewall rules.</span></span>

<span data-ttu-id="255ba-261">Per l'oggetto Server DNS hello:</span><span class="sxs-lookup"><span data-stu-id="255ba-261">For hello DNS Server Object:</span></span>

<span data-ttu-id="255ba-262">![Creare un oggetto server DNS][4]</span><span class="sxs-lookup"><span data-stu-id="255ba-262">![Create a DNS Server Object][4]</span></span>

<span data-ttu-id="255ba-263">Questo riferimento di indirizzo IP singolo verrà utilizzato in una regola DNS in un secondo momento nel documento di hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-263">This single IP address reference will be utilized in a DNS rule later in hello document.</span></span>

<span data-ttu-id="255ba-264">gli oggetti, prerequisiti secondo Hello sono oggetti di servizi.</span><span class="sxs-lookup"><span data-stu-id="255ba-264">hello second prerequisite objects are Services objects.</span></span> <span data-ttu-id="255ba-265">Questi rappresenteranno porte di connessione RDP hello per ogni server.</span><span class="sxs-lookup"><span data-stu-id="255ba-265">These will represent hello RDP connection ports for each server.</span></span> <span data-ttu-id="255ba-266">Poiché l'oggetto servizio RDP esistente hello è la porta RDP predefinito toohello associato, 3389, nuovi servizi possono essere creati tooallow traffico da porte esterne hello (8014 8026).</span><span class="sxs-lookup"><span data-stu-id="255ba-266">Since hello existing RDP service object is bound toohello default RDP port, 3389, new Services can be created tooallow traffic from hello external ports (8014-8026).</span></span> <span data-ttu-id="255ba-267">le nuove porte di Hello anche possibile aggiungere servizio RDP esistente toohello, ma per la dimostrazione, è possibile creare una singola regola per ogni server.</span><span class="sxs-lookup"><span data-stu-id="255ba-267">hello new ports could also be added toohello existing RDP service, but for ease of demonstration, an individual rule for each server can be created.</span></span> <span data-ttu-id="255ba-268">toocreate una nuova regola RDP per un server. a partire dal dashboard di client dispositivo Barracuda NG Admin hello, passare scheda Configurazione toohello, in configurazione operativa hello sezione Ruleset, quindi fare clic su "Servizi" nel menu di oggetti di Firewall, scorrere verso il basso l'elenco di hello servizi hello scegliere hello Servizio "RDP".</span><span class="sxs-lookup"><span data-stu-id="255ba-268">toocreate a new RDP rule for a server; starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset, then click “Services” under hello Firewall Objects menu, scroll down hello list of services and select hello “RDP” service.</span></span> <span data-ttu-id="255ba-269">Ora è disponibile un oggetto servizio RDP-Copy1 che può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="255ba-269">Right-click and select copy, then right-click and select Paste.</span></span> <span data-ttu-id="255ba-270">Fare clic con il pulsante destro del mouse su RDP-Copy1 e scegliere Edit.</span><span class="sxs-lookup"><span data-stu-id="255ba-270">There is now a RDP-Copy1 Service Object that can be edited.</span></span> <span data-ttu-id="255ba-271">Fare doppio clic su RDP Copy1 e selezionare Modifica, hello Modifica oggetto servizio si aprirà la finestra come illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="255ba-271">Right-click RDP-Copy1 and select Edit, hello Edit Service Object window will pop up as shown here:</span></span>

<span data-ttu-id="255ba-272">![Copiare la regola RDP predefinita][5]</span><span class="sxs-lookup"><span data-stu-id="255ba-272">![Copy of Default RDP Rule][5]</span></span>

<span data-ttu-id="255ba-273">i valori Hello possono quindi essere modificato toorepresent hello servizio RDP per un server specifico.</span><span class="sxs-lookup"><span data-stu-id="255ba-273">hello values can then be edited toorepresent hello RDP service for a specific server.</span></span> <span data-ttu-id="255ba-274">Per hello AppVM01 sopra predefinito regola RDP deve essere modificato tooreflect un nuovo nome del servizio, descrizione, e la porta RDP esterno utilizzato in hello diagramma nella figura 8 (Nota: hello porte vengono modificate da hello predefinito RDP è 3389 porta esterna toohello che viene usata per questo server specifico, nel caso di hello di porta esterna di AppVM01 hello è 8025) hello servizio modificato è illustrato di seguito:</span><span class="sxs-lookup"><span data-stu-id="255ba-274">For AppVM01 hello above default RDP rule should be modified tooreflect a new Service Name, Description, and external RDP Port used in hello Figure 8 diagram (Note: hello ports are changed from hello RDP default of 3389 toohello external port being used for this specific server, in hello case of AppVM01 hello external Port is 8025) hello modified service is shown below:</span></span>

<span data-ttu-id="255ba-275">![Regola AppVM01][6]</span><span class="sxs-lookup"><span data-stu-id="255ba-275">![AppVM01 Rule][6]</span></span>

<span data-ttu-id="255ba-276">Questo processo deve essere ripetuto toocreate servizi RDP per hello rimanenti server. AppVM02 DNS01 e IIS01.</span><span class="sxs-lookup"><span data-stu-id="255ba-276">This process must be repeated toocreate RDP Services for hello remaining servers; AppVM02, DNS01, and IIS01.</span></span> <span data-ttu-id="255ba-277">Creazione Hello di questi servizi consentirà la creazione di regole hello più semplice e più ovvio nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-277">hello creation of these Services will make hello Rule creation simpler and more obvious in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="255ba-278">Un servizio RDP per hello Firewall non è necessaria per due motivi. firewall 1) prima di hello VM è un'immagine di basati su Linux in modo che verrebbe utilizzato SSH sulla porta 22 per la gestione delle macchine Virtuali anziché RDP e 2) la porta 22 e due altre porte di gestione sono consentiti nella regola gestione primo hello descritto di seguito tooallow per la connettività di gestione.</span><span class="sxs-lookup"><span data-stu-id="255ba-278">An RDP service for hello Firewall is not needed for two reasons; 1) first hello firewall VM is a Linux based image so SSH would be used on port 22 for VM management instead of RDP, and 2) port 22, and two other management ports are allowed in hello first management rule described below tooallow for management connectivity.</span></span>
> 
> 

### <a name="firewall-rules-creation"></a><span data-ttu-id="255ba-279">Creazione di regole del firewall</span><span class="sxs-lookup"><span data-stu-id="255ba-279">Firewall Rules Creation</span></span>
<span data-ttu-id="255ba-280">In questo esempio si usano tre tipi di regole del firewall ognuna con icone distinte:</span><span class="sxs-lookup"><span data-stu-id="255ba-280">There are three types of firewall rules used in this example, they all have distinct icons:</span></span>

<span data-ttu-id="255ba-281">regola di reindirizzare l'applicazione Hello: ![icona di reindirizzamento dell'applicazione][7]</span><span class="sxs-lookup"><span data-stu-id="255ba-281">hello Application Redirect rule: ![Application Redirect Icon][7]</span></span>

<span data-ttu-id="255ba-282">la regola NAT di destinazione di Hello: ![icona NAT di destinazione][8]</span><span class="sxs-lookup"><span data-stu-id="255ba-282">hello Destination NAT rule: ![Destination NAT Icon][8]</span></span>

<span data-ttu-id="255ba-283">regola di Pass Hello: ![passare icona][9]</span><span class="sxs-lookup"><span data-stu-id="255ba-283">hello Pass rule: ![Pass Icon][9]</span></span>

<span data-ttu-id="255ba-284">Ulteriori informazioni su queste regole sono reperibile nel sito web di Barracuda hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-284">More information on these rules can be found at hello Barracuda web site.</span></span>

<span data-ttu-id="255ba-285">toocreate hello seguendo regole (o verificare le regole predefinite esistente), a partire dal dashboard di hello Barracuda NG amministratore client, passare scheda Configurazione toohello, hello configurazione operativa sezione selezionare il set di regole.</span><span class="sxs-lookup"><span data-stu-id="255ba-285">toocreate hello following rules (or verify existing default rules), starting from hello Barracuda NG Admin client dashboard, navigate toohello configuration tab, in hello Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="255ba-286">Chiamata di una griglia, "Main regole" mostrerà hello esistente regole attive e disattivate il firewall.</span><span class="sxs-lookup"><span data-stu-id="255ba-286">A grid called, “Main Rules” will show hello existing active and deactivated rules on this firewall.</span></span> <span data-ttu-id="255ba-287">In hello angolo superiore destro di questa griglia è una piccola verde "+" fare clic su questo toocreate una nuova regola (Nota: il firewall può essere "bloccato" per le modifiche, se viene visualizzato un pulsante contrassegnato come "Lock" e si toocreate Impossibile o modificare le regole, fare clic su questo pulsante troppo "sbloccare" hello se regola t e consentire la modifica).</span><span class="sxs-lookup"><span data-stu-id="255ba-287">In hello upper right corner of this grid is a small, green “+” button, click this toocreate a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable toocreate or edit rules, click this button too“unlock” hello rule set and allow editing).</span></span> <span data-ttu-id="255ba-288">Se si desidera tooedit una regola esistente, selezionare la regola, fare doppio clic su e scegliere Modifica regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-288">If you wish tooedit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="255ba-289">Una volta le regole vengono create e/o modificate, devono essere inseriti toohello firewall e quindi attivato, se ciò non avviene regola hello le modifiche apportate verranno rese effettive.</span><span class="sxs-lookup"><span data-stu-id="255ba-289">Once your rules are created and/or modified, they must be pushed toohello firewall and then activated, if this is not done hello rule changes will not take effect.</span></span> <span data-ttu-id="255ba-290">il processo di attivazione e push Hello è descritta di seguito le descrizioni delle regole di hello dettagli.</span><span class="sxs-lookup"><span data-stu-id="255ba-290">hello push and activation process is described below hello details rule descriptions.</span></span>

<span data-ttu-id="255ba-291">specifiche di Hello del toocomplete ogni regola richiesta in questo esempio sono descritti di seguito:</span><span class="sxs-lookup"><span data-stu-id="255ba-291">hello specifics of each rule required toocomplete this example are described as follows:</span></span>

* <span data-ttu-id="255ba-292">**Regola di gestione del firewall**: regole di reindirizzamento di questa App consente il traffico toopass toohello di porte di gestione del dispositivo di rete virtuale hello, in questo esempio un NextGen Firewall Barracuda.</span><span class="sxs-lookup"><span data-stu-id="255ba-292">**Firewall Management Rule**: This App Redirect rule allows traffic toopass toohello management ports of hello network virtual appliance, in this example a Barracuda NextGen Firewall.</span></span> <span data-ttu-id="255ba-293">porte di gestione di Hello siano 801, 807 e, facoltativamente, 22.</span><span class="sxs-lookup"><span data-stu-id="255ba-293">hello management ports are 801, 807 and optionally 22.</span></span> <span data-ttu-id="255ba-294">le porte interne ed esterne Hello sono hello stesso (ad esempio alcuna conversione porta).</span><span class="sxs-lookup"><span data-stu-id="255ba-294">hello external and internal ports are hello same (i.e. no port translation).</span></span> <span data-ttu-id="255ba-295">Questa regola, SETUP-MGMT-ACCESS, è una regola predefinita e abilitata per impostazione predefinita in Barracuda NextGen Firewall versione 6.1.</span><span class="sxs-lookup"><span data-stu-id="255ba-295">This rule, SETUP-MGMT-ACCESS, is a default rule and enabled by default (in Barracuda NextGen Firewall version 6.1).</span></span>
  
    <span data-ttu-id="255ba-296">![Regola di gestione del firewall][10]</span><span class="sxs-lookup"><span data-stu-id="255ba-296">![Firewall Management Rule][10]</span></span>

> [!TIP]
> <span data-ttu-id="255ba-297">Hello spazio degli indirizzi di origine nella regola è qualsiasi, se hello intervalli di indirizzi IP di gestione sono note, riducendo l'ambito consentirebbe di ridurre anche porte di gestione toohello superficie di attacco hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-297">hello source address space in this rule is Any, if hello management IP address ranges are known, reducing this scope would also reduce hello attack surface toohello management ports.</span></span>
> 
> 

* <span data-ttu-id="255ba-298">**Le regole di RDP**: le regole NAT destinazione questi consente la gestione di hello singoli server tramite RDP.</span><span class="sxs-lookup"><span data-stu-id="255ba-298">**RDP Rules**:  These Destination NAT rules will allow management of hello individual servers via RDP.</span></span>
  <span data-ttu-id="255ba-299">Esistono quattro campi critici necessari toocreate questa regola:</span><span class="sxs-lookup"><span data-stu-id="255ba-299">There are four critical fields needed toocreate this rule:</span></span>
  
  1. <span data-ttu-id="255ba-300">Origine: tooallow RDP da qualsiasi luogo e riferimento hello "Any" viene utilizzato nel campo di origine hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-300">Source – tooallow RDP from anywhere, hello reference “Any” is used in hello Source field.</span></span>
  2. <span data-ttu-id="255ba-301">Servizio-utilizzare l'oggetto servizio appropriato creato in precedenza, in questo caso "AppVM01 RDP" hello, porte esterne hello reindirizzare toohello server l'indirizzo IP locale e tooport 3386 (porta RDP hello predefinita).</span><span class="sxs-lookup"><span data-stu-id="255ba-301">Service – use hello appropriate Service Object created earlier, in this case “AppVM01 RDP”, hello external ports redirect toohello servers local IP address and tooport 3386 (hello default RDP port).</span></span> <span data-ttu-id="255ba-302">Questa regola specifica è per tooAppVM01 accesso RDP.</span><span class="sxs-lookup"><span data-stu-id="255ba-302">This specific rule is for RDP access tooAppVM01.</span></span>
  3. <span data-ttu-id="255ba-303">Destinazione: deve essere hello *locale porta nel firewall hello*, "DCHP 1 IP locale" o eth0 se utilizza indirizzi IP statici.</span><span class="sxs-lookup"><span data-stu-id="255ba-303">Destination – should be hello *local port on hello firewall*, “DCHP 1 Local IP” or eth0 if using static IPs.</span></span> <span data-ttu-id="255ba-304">numero ordinale di Hello (scheda eth1 eth0, e così via) potrebbe essere diverso se il dispositivo di rete dispone di più interfacce locale.</span><span class="sxs-lookup"><span data-stu-id="255ba-304">hello ordinal number (eth0, eth1, etc) may be different if your network appliance has multiple local interfaces.</span></span> <span data-ttu-id="255ba-305">Si tratta di hello porta firewall hello vengono inviati da (potrebbero essere hello stesso come porta di ricezione hello), destinazione indirizzato effettiva hello è nel campo destinazione elenco hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-305">This is hello port hello firewall is sending out from (may be hello same as hello receiving port), hello actual routed destination is in hello Target List field.</span></span>
  4. <span data-ttu-id="255ba-306">Reindirizzamento: in questa sezione viene appliance virtuale hello in tooultimately reindirizzare il traffico.</span><span class="sxs-lookup"><span data-stu-id="255ba-306">Redirection – this section tells hello virtual appliance where tooultimately redirect this traffic.</span></span> <span data-ttu-id="255ba-307">reindirizzamento più semplice di Hello è tooplace hello IP e porta (facoltativa) nel campo destinazione elenco hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-307">hello simplest redirection is tooplace hello IP and Port (optional) in hello Target List field.</span></span> <span data-ttu-id="255ba-308">Se nessuna porta è la porta di destinazione hello utilizzato nella richiesta in ingresso hello sarà utilizzato (ovvero nessuna conversione), se una porta è definita una porta di hello saranno anche NAT insieme hello IP indirizzo Net. MSMQ.</span><span class="sxs-lookup"><span data-stu-id="255ba-308">If no port is used hello destination port on hello inbound request will be used (ie no translation), if a port is designated hello port will also be NAT’d along with hello IP address.</span></span>
     
     <span data-ttu-id="255ba-309">![Regola firewall RDP][11]</span><span class="sxs-lookup"><span data-stu-id="255ba-309">![Firewall RDP Rule][11]</span></span>
     
     <span data-ttu-id="255ba-310">Un totale di quattro regole RDP necessario toobe creato:</span><span class="sxs-lookup"><span data-stu-id="255ba-310">A total of four RDP rules will need toobe created:</span></span> 
     
     | <span data-ttu-id="255ba-311">Nome regola</span><span class="sxs-lookup"><span data-stu-id="255ba-311">Rule Name</span></span> | <span data-ttu-id="255ba-312">Server</span><span class="sxs-lookup"><span data-stu-id="255ba-312">Server</span></span> | <span data-ttu-id="255ba-313">Service</span><span class="sxs-lookup"><span data-stu-id="255ba-313">Service</span></span> | <span data-ttu-id="255ba-314">Target List</span><span class="sxs-lookup"><span data-stu-id="255ba-314">Target List</span></span> |
     | --- | --- | --- | --- |
     | <span data-ttu-id="255ba-315">RDP-to-IIS01</span><span class="sxs-lookup"><span data-stu-id="255ba-315">RDP-to-IIS01</span></span> |<span data-ttu-id="255ba-316">IIS01</span><span class="sxs-lookup"><span data-stu-id="255ba-316">IIS01</span></span> |<span data-ttu-id="255ba-317">IIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-317">IIS01 RDP</span></span> |<span data-ttu-id="255ba-318">10.0.1.4:3389</span><span class="sxs-lookup"><span data-stu-id="255ba-318">10.0.1.4:3389</span></span> |
     | <span data-ttu-id="255ba-319">RDP-to-DNS01</span><span class="sxs-lookup"><span data-stu-id="255ba-319">RDP-to-DNS01</span></span> |<span data-ttu-id="255ba-320">DNS01</span><span class="sxs-lookup"><span data-stu-id="255ba-320">DNS01</span></span> |<span data-ttu-id="255ba-321">DNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-321">DNS01 RDP</span></span> |<span data-ttu-id="255ba-322">10.0.2.4:3389</span><span class="sxs-lookup"><span data-stu-id="255ba-322">10.0.2.4:3389</span></span> |
     | <span data-ttu-id="255ba-323">RDP-to-AppVM01</span><span class="sxs-lookup"><span data-stu-id="255ba-323">RDP-to-AppVM01</span></span> |<span data-ttu-id="255ba-324">AppVM01</span><span class="sxs-lookup"><span data-stu-id="255ba-324">AppVM01</span></span> |<span data-ttu-id="255ba-325">AppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-325">AppVM01 RDP</span></span> |<span data-ttu-id="255ba-326">10.0.2.5:3389</span><span class="sxs-lookup"><span data-stu-id="255ba-326">10.0.2.5:3389</span></span> |
     | <span data-ttu-id="255ba-327">RDP-to-AppVM02</span><span class="sxs-lookup"><span data-stu-id="255ba-327">RDP-to-AppVM02</span></span> |<span data-ttu-id="255ba-328">AppVM02</span><span class="sxs-lookup"><span data-stu-id="255ba-328">AppVM02</span></span> |<span data-ttu-id="255ba-329">AppVm02 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-329">AppVm02 RDP</span></span> |<span data-ttu-id="255ba-330">10.0.2.6:3389</span><span class="sxs-lookup"><span data-stu-id="255ba-330">10.0.2.6:3389</span></span> |

> [!TIP]
> <span data-ttu-id="255ba-331">In quanto l'ambito hello di hello origine e i campi servizio riduce la superficie di attacco hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-331">Narrowing down hello scope of hello Source and Service fields will reduce hello attack surface.</span></span> <span data-ttu-id="255ba-332">ambito più limitato Hello che consentirà la funzionalità deve essere utilizzato.</span><span class="sxs-lookup"><span data-stu-id="255ba-332">hello most limited scope that will allow functionality should be used.</span></span>
> 
> 

* <span data-ttu-id="255ba-333">**Regole del traffico di applicazione**: sono presenti due regole del traffico di applicazione, hello prima per il traffico web front-end di hello e hello secondo per il traffico di back-end hello (ad esempio server toodata livello web).</span><span class="sxs-lookup"><span data-stu-id="255ba-333">**Application Traffic Rules**: There are two Application Traffic Rules, hello first for hello front end web traffic, and hello second for hello back end traffic (eg web server toodata tier).</span></span> <span data-ttu-id="255ba-334">Queste regole dipenderà dall'architettura di rete hello (in cui vengono collocati i server) e flussi di traffico (il tipo di traffico hello direzione flussi e le porte utilizzate).</span><span class="sxs-lookup"><span data-stu-id="255ba-334">These rules will depend on hello network architecture (where your servers are placed) and traffic flows (which direction hello traffic flows, and which ports are used).</span></span>
  
    <span data-ttu-id="255ba-335">Innanzitutto descritto è regola di hello front-end per il traffico web:</span><span class="sxs-lookup"><span data-stu-id="255ba-335">First discussed is hello front end rule for web traffic:</span></span>
  
    <span data-ttu-id="255ba-336">![Regola firewall Web][12]</span><span class="sxs-lookup"><span data-stu-id="255ba-336">![Firewall Web Rule][12]</span></span>
  
    <span data-ttu-id="255ba-337">Questa regola NAT di destinazione consente hello effettivo traffico tooreach hello applicazione server applicazioni.</span><span class="sxs-lookup"><span data-stu-id="255ba-337">This Destination NAT rule allows hello actual application traffic tooreach hello application server.</span></span> <span data-ttu-id="255ba-338">Mentre hello altre regole consentono per la sicurezza, gestione, e così via, le regole di applicazione sono tooaccess utenti o servizi esterni quali consentire applicazioni hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-338">While hello other rules allow for security, management, etc., Application Rules are what allow external users or services tooaccess hello application(s).</span></span> <span data-ttu-id="255ba-339">Per questo esempio, non esiste un singolo server web sulla porta 80, pertanto hello singola applicazione regola del firewall reindirizzerà il traffico in entrata toohello IP esterno, indirizzo IP interno di toohello web server.</span><span class="sxs-lookup"><span data-stu-id="255ba-339">For this example, there is a single web server on port 80, thus hello single firewall application rule will redirect inbound traffic toohello external IP, toohello web servers internal IP address.</span></span>
  
    <span data-ttu-id="255ba-340">**Nota**: che non sono disponibili porte assegnate nel campo destinazione elenco hello, pertanto hello in ingresso porta 80 (o 443 per hello servizio selezionato) da utilizzare nel reindirizzamento hello del server web hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-340">**Note**: that there is no port assigned in hello Target List field, thus hello inbound port 80 (or 443 for hello Service selected) will be used in hello redirection of hello web server.</span></span> <span data-ttu-id="255ba-341">Se il server web hello è in ascolto su una porta diversa, ad esempio 8080, campo elenco destinazione hello potrebbe essere tooallow too10.0.1.4:8080 aggiornato per il reindirizzamento delle porte hello anche.</span><span class="sxs-lookup"><span data-stu-id="255ba-341">If hello web server is listening on a different port, for example port 8080, hello Target List field could be updated too10.0.1.4:8080 tooallow for hello Port redirection as well.</span></span>
  
    <span data-ttu-id="255ba-342">Regola del traffico di applicazione successivo è Hello hello tootalk toohello AppVM01 server di back-end regola tooallow hello Server Web (ma non AppVM02) tramite qualsiasi servizio:</span><span class="sxs-lookup"><span data-stu-id="255ba-342">hello next Application Traffic Rule is hello back end rule tooallow hello Web Server tootalk toohello AppVM01 server (but not AppVM02) via Any service:</span></span>
  
    <span data-ttu-id="255ba-343">![Regola firewall AppVM01][13]</span><span class="sxs-lookup"><span data-stu-id="255ba-343">![Firewall AppVM01 Rule][13]</span></span>
  
    <span data-ttu-id="255ba-344">Questa regola di Pass consente a qualsiasi server IIS su hello tooreach di subnet front-end hello AppVM01 (indirizzo IP 10.0.2.5) su qualsiasi porta, utilizzando i dati di tooaccess protocollo richiesti dall'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-344">This Pass rule allows any IIS server on hello Frontend subnet tooreach hello AppVM01 (IP Address 10.0.2.5) on Any port, using any Protocol tooaccess data needed by hello web application.</span></span>
  
    <span data-ttu-id="255ba-345">In questa schermata un "\<esplicita dest\>" viene usato in hello destinazione campo toosignify 10.0.2.5 come destinazione di hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-345">In this screen shot an "\<explicit-dest\>" is used in hello Destination field toosignify 10.0.2.5 as hello destination.</span></span> <span data-ttu-id="255ba-346">Può essere denominato esplicita come illustrato o un oggetto di rete (come avveniva in prerequisiti hello per il server DNS hello).</span><span class="sxs-lookup"><span data-stu-id="255ba-346">This could be either explicit as shown or a named Network Object (as was done in hello prerequisites for hello DNS server).</span></span> <span data-ttu-id="255ba-347">Si tratta di amministratore toohello di firewall hello verrà utilizzato il metodo toowhich.</span><span class="sxs-lookup"><span data-stu-id="255ba-347">This is up toohello administrator of hello firewall as toowhich method will be used.</span></span> <span data-ttu-id="255ba-348">tooadd 10.0.2.5 come un Explict Desitnation, fare doppio clic sulla riga vuota prima di hello in \<esplicita dest\> e immettere l'indirizzo hello nella finestra di hello che viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="255ba-348">tooadd 10.0.2.5 as an Explict Desitnation, double-click on hello first blank row under \<explicit-dest\> and enter hello address in hello window that pops up.</span></span>
  
    <span data-ttu-id="255ba-349">Con questa regola passare, non è necessario alcun NAT poiché si tratta di traffico interno, pertanto hello metodo di connessione può essere impostata troppo "SNAT n".</span><span class="sxs-lookup"><span data-stu-id="255ba-349">With this Pass Rule, no NAT is needed since this is internal traffic, so hello Connection Method can be set too"No SNAT".</span></span>
  
    <span data-ttu-id="255ba-350">**Nota**: rete di origine hello in questa regola è qualsiasi risorsa nella subnet front-end hello, se è solo uno, o noto il numero specifico di server web, un oggetto di rete le risorse potrebbero essere creati toobe più toothose esatti indirizzi IP specifici anziché intera subnet front-end di Hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-350">**Note**: hello Source network in this rule is any resource on hello FrontEnd subnet, if there will only be one, or a known specific number of web servers, a Network Object resource could be created toobe more specific toothose exact IP addresses instead of hello entire Frontend subnet.</span></span>

> [!TIP]
> <span data-ttu-id="255ba-351">Questa regola utilizza il servizio di hello "Any" toomake hello toosetup più semplice applicazione di esempio e utilizzare, sarà inoltre ICMPv4 (ping) in una singola regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-351">This rule uses hello service “Any” toomake hello sample application easier toosetup and use, this will also allow ICMPv4 (ping) in a single rule.</span></span> <span data-ttu-id="255ba-352">Questa non è comunque una procedura consigliata.</span><span class="sxs-lookup"><span data-stu-id="255ba-352">However, this is not a recommended practice.</span></span> <span data-ttu-id="255ba-353">Hello porte e protocolli ("servizi") devono essere minimo possibile toohello ristretto che consente di superficie di attacco hello tooreduce operazione applicazione oltre questo limite.</span><span class="sxs-lookup"><span data-stu-id="255ba-353">hello ports and protocols (“Services”) should be narrowed toohello minimum possible that allows application operation tooreduce hello attack surface across this boundary.</span></span>
> 
> 

<br />

> [!TIP]
> <span data-ttu-id="255ba-354">Anche se questa regola Mostra un riferimento esplicito dest in uso, un approccio coerente deve essere utilizzato in tutta la configurazione del firewall hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-354">Although this rule shows an explicit-dest reference being used, a consistent approach should be used throughout hello firewall configuration.</span></span> <span data-ttu-id="255ba-355">È consigliabile che hello denominato oggetto di rete utilizzabile in tutto per semplificare la leggibilità e facilità di supporto.</span><span class="sxs-lookup"><span data-stu-id="255ba-355">It is recommended that hello named Network Object be used throughout for easier readability and supportability.</span></span> <span data-ttu-id="255ba-356">Hello esplicita-dest è qui usato da solo tooshow un metodo alternativo di riferimento e non è in genere consigliabile (soprattutto per le configurazioni complesse).</span><span class="sxs-lookup"><span data-stu-id="255ba-356">hello explicit-dest is used here only tooshow an alternative reference method and is not generally recommended (especially for complex configurations).</span></span>
> 
> 

* <span data-ttu-id="255ba-357">**In uscita tooInternet regola**: passare a questa regola consentirà il traffico da qualsiasi destinazione reti di origine rete toopass toohello selezionato.</span><span class="sxs-lookup"><span data-stu-id="255ba-357">**Outbound tooInternet Rule**: This Pass rule will allow traffic from any Source network toopass toohello selected Destination networks.</span></span> <span data-ttu-id="255ba-358">Questa regola è una regola predefinita in genere già firewall Barracuda NextGen hello, ma è in uno stato disabilitato.</span><span class="sxs-lookup"><span data-stu-id="255ba-358">This rule is a default rule usually already on hello Barracuda NextGen firewall, but is in a disabled state.</span></span> <span data-ttu-id="255ba-359">Facendo clic su questa regola può accedere a hello comando di attivare la regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-359">Right-clicking on this rule can access hello Activate Rule command.</span></span> <span data-ttu-id="255ba-360">regola di Hello illustrato di seguito è stato modificato tooadd hello due subnet locali che sono state create come riferimenti nella sezione dei prerequisiti di hello di questo attributo di origine documento toohello di questa regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-360">hello rule shown here has been modified tooadd hello two local subnets that were created as references in hello prerequisite section of this document toohello Source attribute of this rule.</span></span>
  
    <span data-ttu-id="255ba-361">![Regola firewall in uscita][14]</span><span class="sxs-lookup"><span data-stu-id="255ba-361">![Firewall Outbound Rule][14]</span></span>
* <span data-ttu-id="255ba-362">**Regola DNS**: passare a questa regola consente solo DNS (porta 53) traffico toopass toohello server DNS.</span><span class="sxs-lookup"><span data-stu-id="255ba-362">**DNS Rule**: This Pass rule allows only DNS (port 53) traffic toopass toohello DNS server.</span></span> <span data-ttu-id="255ba-363">Per questo ambiente che maggior parte del traffico da hello front-end toohello back-end è bloccata, questa regola consente in particolare DNS.</span><span class="sxs-lookup"><span data-stu-id="255ba-363">For this environment most traffic from hello FrontEnd toohello BackEnd is blocked, this rule specifically allows DNS.</span></span>
  
    <span data-ttu-id="255ba-364">![Regola firewall DNS][15]</span><span class="sxs-lookup"><span data-stu-id="255ba-364">![Firewall DNS Rule][15]</span></span>
  
    <span data-ttu-id="255ba-365">**Nota**: In questa schermata è incluso hello ripresa metodo di connessione.</span><span class="sxs-lookup"><span data-stu-id="255ba-365">**Note**: In this screen shot hello Connection Method is included.</span></span> <span data-ttu-id="255ba-366">Poiché questa regola per il traffico indirizzo IP toointernal IP interno, non è necessario alcun NATing, questo hello metodo di connessione è troppo "SNAT No" per questa regola di sessione.</span><span class="sxs-lookup"><span data-stu-id="255ba-366">Because this rule is for internal IP toointernal IP address traffic, no NATing is required, this hello Connection Method is set too“No SNAT” for this Pass rule.</span></span>
* <span data-ttu-id="255ba-367">**Subnet tooSubnet regola**: passare a questa regola è una regola predefinita che è stata attivata e tooallow modificato qualsiasi server nel nuovo hello finiscono con server di subnet tooconnect tooany hello subnet front-end.</span><span class="sxs-lookup"><span data-stu-id="255ba-367">**Subnet tooSubnet Rule**: This Pass rule is a default rule that has been activated and modified tooallow any server on hello back end subnet tooconnect tooany server on hello front end subnet.</span></span> <span data-ttu-id="255ba-368">Questa regola è interno tutti traffico pertanto hello metodo di connessione può essere impostata tooNo SNAT.</span><span class="sxs-lookup"><span data-stu-id="255ba-368">This rule is all internal traffic so hello Connection Method can be set tooNo SNAT.</span></span>
  
    <span data-ttu-id="255ba-369">![Regola firewall Intra-VNet][16]</span><span class="sxs-lookup"><span data-stu-id="255ba-369">![Firewall Intra-VNet Rule][16]</span></span>
  
    <span data-ttu-id="255ba-370">**Nota**: hello bidirezionale casella di controllo non è selezionata (non è selezionata nella maggior parte delle regole), questo aspetto è fondamentale per la regola in quanto rende questa regola "unidirezionale", una connessione può essere avviata dalla rete di front-end toohello subnet back-end hello, ma non hello inversa.</span><span class="sxs-lookup"><span data-stu-id="255ba-370">**Note**: hello Bi-directional checkbox is not checked (nor is it checked in most rules), this is significant for this rule in that it makes this rule “one directional”, a connection can be initiated from hello back end subnet toohello front end network, but not hello reverse.</span></span> <span data-ttu-id="255ba-371">Se la casella di controllo viene selezionata, la regola consente il traffico bidirezionale, che in base al diagramma logico in questo articolo non è auspicabile.</span><span class="sxs-lookup"><span data-stu-id="255ba-371">If that checkbox was checked, this rule would enable bi-directional traffic, which from our logical diagram is not desired.</span></span>
* <span data-ttu-id="255ba-372">**Negare tutte le regole di traffico**: deve sempre essere regola finale di hello (in termini di priorità) e un traffico flussi toomatch ha esito negativo di una delle regole precedenti hello pertanto verranno eliminato da questa regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-372">**Deny All Traffic Rule**: This should always be hello final rule (in terms of priority), and as such if a traffic flows fails toomatch any of hello preceding rules it will be dropped by this rule.</span></span> <span data-ttu-id="255ba-373">Questa è una regola predefinita ed è solitamente attivata, quindi non sono in genere necessarie modifiche.</span><span class="sxs-lookup"><span data-stu-id="255ba-373">This is a default rule and usually activated, no modifications are generally needed.</span></span> 
  
    <span data-ttu-id="255ba-374">![Regola firewall Deny][17]</span><span class="sxs-lookup"><span data-stu-id="255ba-374">![Firewall Deny Rule][17]</span></span>

> [!IMPORTANT]
> <span data-ttu-id="255ba-375">Una volta tutte hello sopra le regole vengono create, è importante priorità hello tooreview del traffico di tooensure ogni regola verrà consentita o negata in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="255ba-375">Once all of hello above rules are created, it’s important tooreview hello priority of each rule tooensure traffic will be allowed or denied as desired.</span></span> <span data-ttu-id="255ba-376">Per questo esempio, le regole di hello sono in ordine di hello che vengano visualizzati nella griglia principale di regole in hello Barracuda Client di gestione di inoltro hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-376">For this example, hello rules are in hello order they should appear in hello Main Grid of forwarding rules in hello Barracuda Management Client.</span></span>
> 
> 

## <a name="rule-activation"></a><span data-ttu-id="255ba-377">Attivazione delle regole</span><span class="sxs-lookup"><span data-stu-id="255ba-377">Rule Activation</span></span>
<span data-ttu-id="255ba-378">Con hello ruleset modificato toohello specifica del diagramma logica hello, hello ruleset deve essere caricato toohello firewall e quindi attivato.</span><span class="sxs-lookup"><span data-stu-id="255ba-378">With hello ruleset modified toohello specification of hello logic diagram, hello ruleset must be uploaded toohello firewall and then activated.</span></span>

<span data-ttu-id="255ba-379">![Attivazione delle regole firewall][18]</span><span class="sxs-lookup"><span data-stu-id="255ba-379">![Firewall Rule Activation][18]</span></span>

<span data-ttu-id="255ba-380">Nell'angolo superiore destra hello del client di gestione di hello sono un cluster di pulsanti.</span><span class="sxs-lookup"><span data-stu-id="255ba-380">In hello upper right hand corner of hello management client are a cluster of buttons.</span></span> <span data-ttu-id="255ba-381">Fare clic su hello "inviare modifiche" pulsante toosend hello modificato regole toohello firewall, quindi fare clic sul pulsante "Attiva" hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-381">Click hello “Send Changes” button toosend hello modified rules toohello firewall, then click hello “Activate” button.</span></span>

<span data-ttu-id="255ba-382">Con l'attivazione del set di regole firewall hello hello è stata completata la compilazione di ambiente di esempio.</span><span class="sxs-lookup"><span data-stu-id="255ba-382">With hello activation of hello firewall ruleset this example environment build is complete.</span></span>

## <a name="traffic-scenarios"></a><span data-ttu-id="255ba-383">Scenari di traffico</span><span class="sxs-lookup"><span data-stu-id="255ba-383">Traffic Scenarios</span></span>
> [!IMPORTANT]
> <span data-ttu-id="255ba-384">Una chiave takeway è tooremember che **tutti** proverrà il traffico attraverso il firewall hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-384">A key takeway is tooremember that **all** traffic will come through hello firewall.</span></span> <span data-ttu-id="255ba-385">Così tooremote desktop toohello IIS01 server, anche se è in servizio di Cloud Front-End hello e sulla subnet Front-End hello, tooaccess dobbiamo tooRDP toohello firewall sul server porta 8014 e attendere la richiesta RDP hello firewall tooroute hello internamente la porta RDP IIS01 toohello.</span><span class="sxs-lookup"><span data-stu-id="255ba-385">So tooremote desktop toohello IIS01 server, even though it's in hello Front End Cloud Service and on hello Front End subnet, tooaccess this server we will need tooRDP toohello firewall on port 8014, and then allow hello firewall tooroute hello RDP request internally toohello IIS01 RDP Port.</span></span> <span data-ttu-id="255ba-386">Hello "Connetti" del portale di Azure pulsante non funzionerà poiché non esiste alcun diretto tooIIS01 percorso RDP (per quanto possibile vedere portale hello).</span><span class="sxs-lookup"><span data-stu-id="255ba-386">hello Azure portal's "Connect" button won't work because there is no direct RDP path tooIIS01 (as far as hello portal can see).</span></span> <span data-ttu-id="255ba-387">Ciò significa che tutte le connessioni da hello internet sarà toohello servizio di sicurezza e una porta, ad esempio secscv001.cloudapp.net:xxxx.</span><span class="sxs-lookup"><span data-stu-id="255ba-387">This means all connections from hello internet will be toohello Security Service and a Port, e.g. secscv001.cloudapp.net:xxxx.</span></span>
> 
> 

<span data-ttu-id="255ba-388">Per questi scenari, hello segue le regole del firewall deve essere disponibili:</span><span class="sxs-lookup"><span data-stu-id="255ba-388">For these scenarios, hello following firewall rules should be in place:</span></span>

1. <span data-ttu-id="255ba-389">Firewall Management</span><span class="sxs-lookup"><span data-stu-id="255ba-389">Firewall Management</span></span>
2. <span data-ttu-id="255ba-390">TooIIS01 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-390">RDP tooIIS01</span></span>
3. <span data-ttu-id="255ba-391">TooDNS01 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-391">RDP tooDNS01</span></span>
4. <span data-ttu-id="255ba-392">TooAppVM01 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-392">RDP tooAppVM01</span></span>
5. <span data-ttu-id="255ba-393">TooAppVM02 RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-393">RDP tooAppVM02</span></span>
6. <span data-ttu-id="255ba-394">Toohello traffico App Web</span><span class="sxs-lookup"><span data-stu-id="255ba-394">App Traffic toohello Web</span></span>
7. <span data-ttu-id="255ba-395">Traffico App tooAppVM01</span><span class="sxs-lookup"><span data-stu-id="255ba-395">App Traffic tooAppVM01</span></span>
8. <span data-ttu-id="255ba-396">In uscita toohello Internet</span><span class="sxs-lookup"><span data-stu-id="255ba-396">Outbound toohello Internet</span></span>
9. <span data-ttu-id="255ba-397">TooDNS01 front-end</span><span class="sxs-lookup"><span data-stu-id="255ba-397">Frontend tooDNS01</span></span>
10. <span data-ttu-id="255ba-398">Traffico tra più Subnet (solo fine toofront back-end)</span><span class="sxs-lookup"><span data-stu-id="255ba-398">Intra-Subnet Traffic (back end toofront end only)</span></span>
11. <span data-ttu-id="255ba-399">Deny All</span><span class="sxs-lookup"><span data-stu-id="255ba-399">Deny All</span></span>

<span data-ttu-id="255ba-400">set di regole firewall effettivo Hello avrà probabilmente molte altre regole toothese aggiunta, le regole di hello qualsiasi dato firewall disporrà di numeri di priorità diversi rispetto a quelli elencati di seguito hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-400">hello actual firewall ruleset will most likely have many other rules in addition toothese, hello rules on any given firewall will also have different priority numbers than hello ones listed here.</span></span> <span data-ttu-id="255ba-401">Questo elenco e dei numeri sono tooprovide pertinenza solo queste undici regole e la priorità relativa di hello tra loro.</span><span class="sxs-lookup"><span data-stu-id="255ba-401">This list and associated numbers are tooprovide relevance between just these eleven rules and hello relative priority amongst them.</span></span> <span data-ttu-id="255ba-402">In altre parole; firewall effettivo hello, hello "RDP tooIIS01" potrebbe essere regola numero 5, ma come è di sotto di regole "Gestione Firewall" hello e versioni successive regola "RDP tooDNS01" hello che allineamento con l'intenzione di hello dell'elenco.</span><span class="sxs-lookup"><span data-stu-id="255ba-402">In other words; on hello actual firewall, hello “RDP tooIIS01” may be rule number 5, but as long as it’s below hello “Firewall Management” rule and above hello “RDP tooDNS01” rule it would align with hello intention of this list.</span></span> <span data-ttu-id="255ba-403">supporta anche l'elenco Hello nell'hello brevità; consentendo scenari seguenti ad esempio "Regole firewall 9 (DNS)".</span><span class="sxs-lookup"><span data-stu-id="255ba-403">hello list will also aid in hello below scenarios allowing brevity; e.g. “FW Rule 9 (DNS)”.</span></span> <span data-ttu-id="255ba-404">Per ragioni di brevità, hello quattro regole RDP sarà collettivamente chiamati anche "hello regole RDP" quando hello traffico risulta tooRDP non correlati.</span><span class="sxs-lookup"><span data-stu-id="255ba-404">Also for brevity, hello four RDP rules will be collectively called, “hello RDP rules” when hello traffic scenario is unrelated tooRDP.</span></span>

<span data-ttu-id="255ba-405">Ricordare anche che sono gruppi di sicurezza di rete sul posto per il traffico internet in entrata su hello front-end e back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="255ba-405">Also recall that Network Security Groups are in-place for inbound internet traffic on hello Frontend and Backend subnets.</span></span>

#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="255ba-406">(Consentito) Internet tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="255ba-406">(Allowed) Internet tooWeb Server</span></span>
1. <span data-ttu-id="255ba-407">L'utente Internet richiede una pagina HTTP a SecSvc001.CloudApp.Net (servizio cloud per Internet).</span><span class="sxs-lookup"><span data-stu-id="255ba-407">Internet user requests HTTP page from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="255ba-408">Traffico passa del servizio cloud tramite endpoint aperto interfaccia toofirewall porta 80 del 10.0.0.4:80</span><span class="sxs-lookup"><span data-stu-id="255ba-408">Cloud service passes traffic through open endpoint on port 80 toofirewall interface on 10.0.0.4:80</span></span>
3. <span data-ttu-id="255ba-409">Nessun gruppo assegnato tooSecurity subnet, pertanto le regole di sistema NSG consentono traffico toofirewall</span><span class="sxs-lookup"><span data-stu-id="255ba-409">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="255ba-410">Traffico raggiunge l'indirizzo IP interno del firewall hello (10.0.1.4)</span><span class="sxs-lookup"><span data-stu-id="255ba-410">Traffic hits internal IP address of hello firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="255ba-411">Il firewall inizia l'elaborazione delle regole:</span><span class="sxs-lookup"><span data-stu-id="255ba-411">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="255ba-412">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-412">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-413">Regole FW 2-5 (regole di RDP) non si applicano, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-413">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="255ba-414">FW regola 6 (App: Web) viene applicato, il traffico è consentito, firewall NAT è too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="255ba-414">FW Rule 6 (App: Web) does apply, traffic is allowed, firewall NATs it too10.0.1.4 (IIS01)</span></span>
6. <span data-ttu-id="255ba-415">subnet front-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-415">hello Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="255ba-416">NSG regola 1 (blocco Internet) non è valida (il traffico è stato NAT usasse firewall hello, indirizzo di origine hello è ora pertanto firewall hello nella subnet sicurezza hello e visibili subnet front-end hello traffico "local" toobe di gruppo ed è pertanto consentita), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-416">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Frontend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="255ba-417">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-417">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="255ba-418">Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello</span><span class="sxs-lookup"><span data-stu-id="255ba-418">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
8. <span data-ttu-id="255ba-419">Iis01 tenta tooinitiates un tooAppVM01 sessione FTP nella subnet back-end</span><span class="sxs-lookup"><span data-stu-id="255ba-419">IIS01 attempts tooinitiates an FTP session tooAppVM01 on Backend subnet</span></span>
9. <span data-ttu-id="255ba-420">route UDR Hello nella subnet front-end rende hop successivo di hello firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-420">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
10. <span data-ttu-id="255ba-421">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="255ba-421">No outbound rules on Frontend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="255ba-422">Il firewall inizia l'elaborazione delle regole:</span><span class="sxs-lookup"><span data-stu-id="255ba-422">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="255ba-423">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-423">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="255ba-424">Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-424">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="255ba-425">FW regola 6 (App: Web) non si applicano, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-425">FW Rule 6 (App: Web) doesn’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="255ba-426">Regola FW 7 (App: back-end) viene applicato, è consentito il traffico, firewall inoltra il traffico too10.0.2.5 (AppVM01)</span><span class="sxs-lookup"><span data-stu-id="255ba-426">FW Rule 7 (App: Backend) does apply, traffic is allowed, firewall forwards traffic too10.0.2.5 (AppVM01)</span></span>
12. <span data-ttu-id="255ba-427">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-427">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="255ba-428">Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-428">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="255ba-429">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-429">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
13. <span data-ttu-id="255ba-430">AppVM01 riceve la richiesta di hello e avvia la sessione hello e risponde</span><span class="sxs-lookup"><span data-stu-id="255ba-430">AppVM01 receives hello request and initiates hello session and responds</span></span>
14. <span data-ttu-id="255ba-431">route UDR Hello nella subnet back-end rende hop successivo di hello firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-431">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
15. <span data-ttu-id="255ba-432">Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello subnet di back-end</span><span class="sxs-lookup"><span data-stu-id="255ba-432">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
16. <span data-ttu-id="255ba-433">Poiché questo restituisce il traffico su un firewall hello sessione stabilita passa server web di hello risposta toohello indietro (IIS01)</span><span class="sxs-lookup"><span data-stu-id="255ba-433">Because this is returning traffic on an established session hello firewall passes hello response back toohello web server (IIS01)</span></span>
17. <span data-ttu-id="255ba-434">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-434">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="255ba-435">Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-435">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="255ba-436">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-436">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
18. <span data-ttu-id="255ba-437">server IIS Hello riceve risposta hello, completa la transazione hello con AppVM01 e quindi completa compilazione hello risposta HTTP, la risposta HTTP viene inviata toohello richiedente</span><span class="sxs-lookup"><span data-stu-id="255ba-437">hello IIS server receives hello response, completes hello transaction with AppVM01, and then completes building hello HTTP response, this HTTP response is sent toohello requestor</span></span>
19. <span data-ttu-id="255ba-438">Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello di subnet front-end</span><span class="sxs-lookup"><span data-stu-id="255ba-438">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
20. <span data-ttu-id="255ba-439">Poiché si tratta di hello risposta tooan stabilita la sessione NAT è accettata dal firewall hello e Hello HTTP risposta riscontri hello firewall</span><span class="sxs-lookup"><span data-stu-id="255ba-439">hello HTTP response hits hello firewall, and because this is hello response tooan established NAT session is accepted by hello firewall</span></span>
21. <span data-ttu-id="255ba-440">firewall Hello Reindirizza quindi hello risposta back toohello utente Internet</span><span class="sxs-lookup"><span data-stu-id="255ba-440">hello firewall then redirects hello response back toohello Internet User</span></span>
22. <span data-ttu-id="255ba-441">Poiché non esistono regole in uscita di gruppo o hop UDR in subnet front-end hello è consentita una risposta hello e hello utente Internet riceve hello web pagina richiesta.</span><span class="sxs-lookup"><span data-stu-id="255ba-441">Since there are no outbound NSG rules or UDR hops on hello Frontend subnet hello response is allowed, and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-internet-rdp-toobackend"></a><span data-ttu-id="255ba-442">(Consentito) TooBackend Internet RDP</span><span class="sxs-lookup"><span data-stu-id="255ba-442">(Allowed) Internet RDP tooBackend</span></span>
1. <span data-ttu-id="255ba-443">Amministratore del server su internet richiede tooAppVM01 sessione RDP tramite SecSvc001.CloudApp.Net:8025, dove 8025 è numero di porta hello assegnati all'utente per la regola del firewall "RDP tooAppVM01" hello</span><span class="sxs-lookup"><span data-stu-id="255ba-443">Server Admin on internet requests RDP session tooAppVM01 via SecSvc001.CloudApp.Net:8025, where 8025 is hello user assigned port number for hello “RDP tooAppVM01” firewall rule</span></span>
2. <span data-ttu-id="255ba-444">servizio cloud Hello passa il traffico attraverso endpoint aperto hello porta 8025 toofirewall interfaccia 10.0.0.4:8025</span><span class="sxs-lookup"><span data-stu-id="255ba-444">hello cloud service passes traffic through hello open endpoint on port 8025 toofirewall interface on 10.0.0.4:8025</span></span>
3. <span data-ttu-id="255ba-445">Nessun gruppo assegnato tooSecurity subnet, pertanto le regole di sistema NSG consentono traffico toofirewall</span><span class="sxs-lookup"><span data-stu-id="255ba-445">No NSG assigned tooSecurity subnet, so system NSG rules allow traffic toofirewall</span></span>
4. <span data-ttu-id="255ba-446">Il firewall inizia l'elaborazione delle regole:</span><span class="sxs-lookup"><span data-stu-id="255ba-446">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="255ba-447">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-447">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-448">Non si applica la regola 2 FW (RDP IIS), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-448">FW Rule 2 (RDP IIS) doesn’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="255ba-449">Regola di FW 3 (DNS01 RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-449">FW Rule 3 (RDP DNS01) doesn’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="255ba-450">Applicare la regola FW 4 (AppVM01 RDP), è consentito il traffico, firewall NAT è too10.0.2.5:3386 (porta RDP in AppVM01)</span><span class="sxs-lookup"><span data-stu-id="255ba-450">FW Rule 4 (RDP AppVM01) does apply, traffic is allowed, firewall NATs it too10.0.2.5:3386 (RDP port on AppVM01)</span></span>
5. <span data-ttu-id="255ba-451">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-451">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="255ba-452">NSG regola 1 (blocco Internet) non è valida (il traffico è stato NAT usasse firewall hello, indirizzo di origine hello è ora pertanto firewall hello nella subnet sicurezza hello e visualizzati in base alla subnet di back-end hello traffico "local" toobe di gruppo ed è pertanto consentita), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-452">NSG Rule 1 (Block Internet) doesn’t apply (this traffic was NAT’d by hello firewall, thus hello source address is now hello firewall which is on hello Security subnet and seen by hello Backend subnet NSG toobe “local” traffic and is thus allowed), move toonext rule</span></span>
   2. <span data-ttu-id="255ba-453">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-453">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="255ba-454">AppVM01 è in ascolto del traffico RDP e risponde.</span><span class="sxs-lookup"><span data-stu-id="255ba-454">AppVM01 is listening for RDP traffic and responds</span></span>
7. <span data-ttu-id="255ba-455">Senza regole del gruppo di sicurezza di rete in uscita sono applicabili le regole predefinite e il traffico restituito è consentito.</span><span class="sxs-lookup"><span data-stu-id="255ba-455">With no outbound NSG rules, default rules apply and return traffic is allowed</span></span>
8. <span data-ttu-id="255ba-456">Le route UDR il traffico in uscita toohello firewall come hop successivo hello</span><span class="sxs-lookup"><span data-stu-id="255ba-456">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
9. <span data-ttu-id="255ba-457">Poiché questo è restituzione di traffico in un firewall hello sessione stabilita passa utente internet di hello risposta toohello indietro</span><span class="sxs-lookup"><span data-stu-id="255ba-457">Because this is returning traffic on an established session hello firewall passes hello response back toohello internet user</span></span>
10. <span data-ttu-id="255ba-458">La sessione RDP è abilitata.</span><span class="sxs-lookup"><span data-stu-id="255ba-458">RDP session is enabled</span></span>
11. <span data-ttu-id="255ba-459">AppVM01 richiede il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="255ba-459">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="255ba-460">(Consentito) Ricerca DNS del server Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="255ba-460">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="255ba-461">Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.</span><span class="sxs-lookup"><span data-stu-id="255ba-461">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="255ba-462">Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01</span><span class="sxs-lookup"><span data-stu-id="255ba-462">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="255ba-463">Le route UDR il traffico in uscita toohello firewall come hop successivo hello</span><span class="sxs-lookup"><span data-stu-id="255ba-463">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
4. <span data-ttu-id="255ba-464">Nessuna regola di gruppo in uscita è subnet front-end toohello associato, è consentito il traffico</span><span class="sxs-lookup"><span data-stu-id="255ba-464">No outbound NSG rules are bound toohello Frontend subnet, traffic is allowed</span></span>
5. <span data-ttu-id="255ba-465">Il firewall inizia l'elaborazione delle regole:</span><span class="sxs-lookup"><span data-stu-id="255ba-465">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="255ba-466">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-466">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-467">Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-467">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="255ba-468">Non applicare, spostare toonext regola FW regole 6 e 7 (regole di App)</span><span class="sxs-lookup"><span data-stu-id="255ba-468">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="255ba-469">FW regola 8 (tooInternet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-469">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="255ba-470">Applicare FW regola 9 (DNS), è consentito il traffico, firewall inoltra il traffico too10.0.2.4 (DNS01)</span><span class="sxs-lookup"><span data-stu-id="255ba-470">FW Rule 9 (DNS) does apply, traffic is allowed, firewall forwards traffic too10.0.2.4 (DNS01)</span></span>
6. <span data-ttu-id="255ba-471">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-471">hello Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="255ba-472">Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-472">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-473">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-473">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
7. <span data-ttu-id="255ba-474">Server DNS riceve una richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="255ba-474">DNS server receives hello request</span></span>
8. <span data-ttu-id="255ba-475">Server DNS non dispone di indirizzo hello memorizzati nella cache e richiede un server radice DNS su hello internet</span><span class="sxs-lookup"><span data-stu-id="255ba-475">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
9. <span data-ttu-id="255ba-476">Le route UDR il traffico in uscita toohello firewall come hop successivo hello</span><span class="sxs-lookup"><span data-stu-id="255ba-476">UDR routes outbound traffic toohello firewall as hello next hop</span></span>
10. <span data-ttu-id="255ba-477">Non sono impostate regole del gruppo di sicurezza di rete in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="255ba-477">No outbound NSG rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="255ba-478">Il firewall inizia l'elaborazione delle regole:</span><span class="sxs-lookup"><span data-stu-id="255ba-478">Firewall begins rule processing:</span></span>
    1. <span data-ttu-id="255ba-479">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-479">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="255ba-480">Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-480">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
    3. <span data-ttu-id="255ba-481">Non applicare, spostare toonext regola FW regole 6 e 7 (regole di App)</span><span class="sxs-lookup"><span data-stu-id="255ba-481">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
    4. <span data-ttu-id="255ba-482">Applicare FW regola 8 (tooInternet) è consentito il traffico, sessione SNAT tooroot di server DNS su Internet hello</span><span class="sxs-lookup"><span data-stu-id="255ba-482">FW Rule 8 (tooInternet) does apply, traffic is allowed, session is SNAT out tooroot DNS server on hello Internet</span></span>
12. <span data-ttu-id="255ba-483">Server DNS Internet risponde, poiché questa sessione è stata avviata dal firewall hello, risposta hello è accettata dal firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-483">Internet DNS server responds, since this session was initiated from hello firewall, hello response is accepted by hello firewall</span></span>
13. <span data-ttu-id="255ba-484">Poiché si tratta di una sessione stabilita, firewall hello inoltra hello risposta toohello avvio server, DNS01</span><span class="sxs-lookup"><span data-stu-id="255ba-484">As this is an established session, hello firewall forwards hello response toohello initiating server, DNS01</span></span>
14. <span data-ttu-id="255ba-485">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-485">hello Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="255ba-486">Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-486">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="255ba-487">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-487">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
15. <span data-ttu-id="255ba-488">server DNS Hello riceve e memorizza nella cache la risposta hello e risponde quindi toohello richiesta iniziale indietro tooIIS01</span><span class="sxs-lookup"><span data-stu-id="255ba-488">hello DNS server receives and caches hello response, and then responds toohello initial request back tooIIS01</span></span>
16. <span data-ttu-id="255ba-489">route UDR Hello nella subnet back-end rende hop successivo di hello firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-489">hello UDR route on backend subnet makes hello firewall hello next hop</span></span>
17. <span data-ttu-id="255ba-490">Nessuna regola di gruppo in uscita presenti nella subnet back-end hello, è consentito il traffico</span><span class="sxs-lookup"><span data-stu-id="255ba-490">No outbound NSG rules exist on hello Backend subnet, traffic is allowed</span></span>
18. <span data-ttu-id="255ba-491">Si tratta di una sessione stabilita firewall hello, risposta hello viene inoltrato dal server IIS di hello firewall toohello indietro</span><span class="sxs-lookup"><span data-stu-id="255ba-491">This is an established session on hello firewall, hello response is forwarded by hello firewall back toohello IIS server</span></span>
19. <span data-ttu-id="255ba-492">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-492">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="255ba-493">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="255ba-493">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
    2. <span data-ttu-id="255ba-494">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito</span><span class="sxs-lookup"><span data-stu-id="255ba-494">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
20. <span data-ttu-id="255ba-495">Iis01 riceve risposta hello da DNS01</span><span class="sxs-lookup"><span data-stu-id="255ba-495">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-backend-server-toofrontend-server"></a><span data-ttu-id="255ba-496">(Consentito) Server di back-end server tooFrontend</span><span class="sxs-lookup"><span data-stu-id="255ba-496">(Allowed) Backend server tooFrontend server</span></span>
1. <span data-ttu-id="255ba-497">Un amministratore connesso tooAppVM02 tramite RDP richiede un file direttamente dal server IIS01 hello tramite Esplora file</span><span class="sxs-lookup"><span data-stu-id="255ba-497">An administrator logged on tooAppVM02 via RDP requests a file directly from hello IIS01 server via windows file explorer</span></span>
2. <span data-ttu-id="255ba-498">route UDR Hello nella subnet back-end rende hop successivo di hello firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-498">hello UDR route on Backend subnet makes hello firewall hello next hop</span></span>
3. <span data-ttu-id="255ba-499">Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello subnet di back-end</span><span class="sxs-lookup"><span data-stu-id="255ba-499">Since there are no outbound NSG rules on hello Backend subnet hello response is allowed</span></span>
4. <span data-ttu-id="255ba-500">Il firewall inizia l'elaborazione delle regole:</span><span class="sxs-lookup"><span data-stu-id="255ba-500">Firewall begins rule processing:</span></span>
   1. <span data-ttu-id="255ba-501">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-501">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-502">Non applicare FW regola 2-5 (regole di RDP), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-502">FW Rule 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="255ba-503">Non applicare, spostare toonext regola FW regole 6 e 7 (regole di App)</span><span class="sxs-lookup"><span data-stu-id="255ba-503">FW Rules 6 & 7 (App Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="255ba-504">FW regola 8 (tooInternet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-504">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="255ba-505">Non applicare FW regola 9 (DNS), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-505">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="255ba-506">Applicare FW regola 10 (Intra-Subnet), è consentito il traffico, firewall passa traffico too10.0.1.4 (IIS01)</span><span class="sxs-lookup"><span data-stu-id="255ba-506">FW Rule 10 (Intra-Subnet) does apply, traffic is allowed, firewall passes traffic too10.0.1.4 (IIS01)</span></span>
5. <span data-ttu-id="255ba-507">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-507">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="255ba-508">Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-508">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-509">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-509">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
6. <span data-ttu-id="255ba-510">Supponendo che l'autorizzazione e autenticazione appropriate, IIS01 accetta hello richiesta e risposta</span><span class="sxs-lookup"><span data-stu-id="255ba-510">Assuming proper authentication and authorization, IIS01 accepts hello request and responds</span></span>
7. <span data-ttu-id="255ba-511">route UDR Hello nella subnet front-end rende hop successivo di hello firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-511">hello UDR route on Frontend subnet makes hello firewall hello next hop</span></span>
8. <span data-ttu-id="255ba-512">Poiché esistono non è consentita alcuna regola di gruppo in uscita su hello risposta hello di subnet front-end</span><span class="sxs-lookup"><span data-stu-id="255ba-512">Since there are no outbound NSG rules on hello Frontend subnet hello response is allowed</span></span>
9. <span data-ttu-id="255ba-513">Poiché si tratta di una sessione esistente in firewall hello è consentita la risposta e firewall hello restituisce hello risposta tooAppVM02</span><span class="sxs-lookup"><span data-stu-id="255ba-513">As this is an existing session on hello firewall this response is allowed and hello firewall returns hello response tooAppVM02</span></span>
10. <span data-ttu-id="255ba-514">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="255ba-514">Backend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="255ba-515">Regola di gruppo 1 (blocco Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-515">NSG Rule 1 (Block Internet) doesn’t apply, move toonext rule</span></span>
    2. <span data-ttu-id="255ba-516">GRUPPO regole predefinite per consentire il traffico toosubnet subnet, è consentito il traffico, arrestare l'elaborazione della regola NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-516">Default NSG Rules allow subnet toosubnet traffic, traffic is allowed, stop NSG rule processing</span></span>
11. <span data-ttu-id="255ba-517">AppVM02 riceve risposta hello</span><span class="sxs-lookup"><span data-stu-id="255ba-517">AppVM02 receives hello response</span></span>

#### <a name="denied-internet-direct-tooweb-server"></a><span data-ttu-id="255ba-518">(Negato) Internet diretta tooWeb Server</span><span class="sxs-lookup"><span data-stu-id="255ba-518">(Denied) Internet direct tooWeb Server</span></span>
1. <span data-ttu-id="255ba-519">Utente Internet tenta tooaccess hello server web, IIS01, tramite hello FrontEnd001.CloudApp.Net servizio</span><span class="sxs-lookup"><span data-stu-id="255ba-519">Internet user tries tooaccess hello web server, IIS01, through hello FrontEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="255ba-520">Poiché non sono presenti endpoint aperto per il traffico HTTP, questa non passa attraverso hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="255ba-520">Since there are no endpoints open for HTTP traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="255ba-521">Se gli endpoint hello erano aperti per qualche motivo, hello NSG (blocco Internet) in subnet front-end hello bloccano il traffico</span><span class="sxs-lookup"><span data-stu-id="255ba-521">If hello endpoints were open for some reason, hello NSG (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="255ba-522">Infine, route UDR subnet front-end di hello viene inviato il traffico in uscita dal firewall toohello IIS01 come hop successivo hello e firewall hello sarebbe vedere questo traffico asimmetrica e rilasciare la risposta in uscita hello pertanto esistono almeno tre livelli indipendenti difesa tra hello internet e IIS01 tramite il servizio cloud, impedendo l'accesso non autorizzato o non appropriato.</span><span class="sxs-lookup"><span data-stu-id="255ba-522">Finally, hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and IIS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toobackend-server"></a><span data-ttu-id="255ba-523">(Negato) Internet tooBackend Server</span><span class="sxs-lookup"><span data-stu-id="255ba-523">(Denied) Internet tooBackend Server</span></span>
1. <span data-ttu-id="255ba-524">Utente Internet tenta di un file in AppVM01 tramite hello servizio BackEnd001.CloudApp.Net tooaccess</span><span class="sxs-lookup"><span data-stu-id="255ba-524">Internet user tries tooaccess a file on AppVM01 through hello BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="255ba-525">Poiché non sono presenti endpoint aperto per la condivisione file, questo non raggiungerebbe hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="255ba-525">Since there are no endpoints open for file share, this would not pass hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="255ba-526">Se gli endpoint hello erano aperti per qualche motivo, blocca il traffico hello NSG (blocco Internet)</span><span class="sxs-lookup"><span data-stu-id="255ba-526">If hello endpoints were open for some reason, hello NSG (Block Internet) would block this traffic</span></span>
4. <span data-ttu-id="255ba-527">Infine, route UDR hello viene inviato il traffico in uscita dal firewall toohello AppVM01 come hop successivo hello e firewall hello sarebbe vedere questo traffico asimmetrica e rilasciare la risposta in uscita hello pertanto esistono almeno tre livelli indipendenti di difesa tra Hello internet e AppVM01 tramite il servizio cloud, impedendo l'accesso non autorizzato o non appropriato.</span><span class="sxs-lookup"><span data-stu-id="255ba-527">Finally, hello UDR route would send any outbound traffic from AppVM01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and AppVM01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-frontend-server-toobackend-server"></a><span data-ttu-id="255ba-528">(Negato) TooBackend server front-end Server</span><span class="sxs-lookup"><span data-stu-id="255ba-528">(Denied) Frontend server tooBackend Server</span></span>
1. <span data-ttu-id="255ba-529">Si supponga IIS01 compromesso e sia in esecuzione Server subnet back-end di hello tooscan durante il tentativo di codice dannoso.</span><span class="sxs-lookup"><span data-stu-id="255ba-529">Assume IIS01 was compromised and is running malicious code trying tooscan hello Backend subnet servers.</span></span>
2. <span data-ttu-id="255ba-530">route UDR subnet front-end di Hello invierebbe tutto il traffico in uscita dal firewall toohello IIS01 come hop successivo hello.</span><span class="sxs-lookup"><span data-stu-id="255ba-530">hello Frontend subnet UDR route would send any outbound traffic from IIS01 toohello firewall as hello next hop.</span></span> <span data-ttu-id="255ba-531">Non è un elemento che può essere modificato da hello compromesso macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="255ba-531">This is not something that can be altered by hello compromised VM.</span></span>
3. <span data-ttu-id="255ba-532">firewall Hello potrebbe elaborare il traffico di hello, se è stata richiesta hello tooAppVM01 o toohello DNS server per le ricerche DNS che il traffico potrebbe potenzialmente essere consentito dal firewall hello (scadenza tooFW regole 7 e 9).</span><span class="sxs-lookup"><span data-stu-id="255ba-532">hello firewall would process hello traffic, if hello request was tooAppVM01, or toohello DNS server for DNS lookups that traffic could potentially be allowed by hello firewall (due tooFW Rules 7 and 9).</span></span> <span data-ttu-id="255ba-533">Tutto il resto del traffico verrebbe bloccato dalla regola firewall 11 (Deny All).</span><span class="sxs-lookup"><span data-stu-id="255ba-533">All other traffic would be blocked by FW Rule 11 (Deny All).</span></span>
4. <span data-ttu-id="255ba-534">Se avanzate di rilevamento minacce è stato abilitato il firewall hello (non illustrata in questo documento, vedere la documentazione del fornitore hello per dispositivo di rete specifica minaccia funzionalità avanzate), anche il traffico che sarebbe necessario consentire hello base di regole di inoltro illustrati in questo documento può contribuire a evitare traffico hello contenuti firme note o modelli che una regola avanzata minaccia di flag.</span><span class="sxs-lookup"><span data-stu-id="255ba-534">If advanced threat detection was enabled on hello firewall (which is not covered in this document, see hello vendor documentation for your specific network appliance advanced threat capabilities), even traffic that would be allowed by hello basic forwarding rules discussed in this document could be prevented if hello traffic contained known signatures or patterns that flag an advanced threat rule.</span></span>

#### <a name="denied-internet-dns-lookup-on-dns-server"></a><span data-ttu-id="255ba-535">(Negato) Ricerca DNS Internet sul server DNS</span><span class="sxs-lookup"><span data-stu-id="255ba-535">(Denied) Internet DNS lookup on DNS server</span></span>
1. <span data-ttu-id="255ba-536">Utente Internet tenta un record DNS interno nella DNS01 tramite servizio BackEnd001.CloudApp.Net toolookup</span><span class="sxs-lookup"><span data-stu-id="255ba-536">Internet user tries toolookup an internal DNS record on DNS01 through BackEnd001.CloudApp.Net service</span></span> 
2. <span data-ttu-id="255ba-537">Poiché non sono presenti endpoint aperto per il traffico DNS, questo non passa attraverso hello servizio Cloud e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="255ba-537">Since there are no endpoints open for DNS traffic, this would not pass through hello Cloud Service and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="255ba-538">Se gli endpoint hello erano aperti per qualche motivo, regola di gruppo hello (blocco Internet) in subnet front-end hello bloccano il traffico</span><span class="sxs-lookup"><span data-stu-id="255ba-538">If hello endpoints were open for some reason, hello NSG rule (Block Internet) on hello Frontend subnet would block this traffic</span></span>
4. <span data-ttu-id="255ba-539">Infine, route UDR subnet back-end di hello viene inviato il traffico in uscita dal firewall toohello DNS01 come hop successivo hello e firewall hello sarebbe vedere questo traffico asimmetrica e rilasciare la risposta in uscita hello pertanto esistono almeno tre livelli indipendenti difesa tra hello internet e DNS01 tramite il servizio cloud, impedendo l'accesso non autorizzato o non appropriato.</span><span class="sxs-lookup"><span data-stu-id="255ba-539">Finally, hello Backend subnet UDR route would send any outbound traffic from DNS01 toohello firewall as hello next hop, and hello firewall would see this as asymmetric traffic and drop hello outbound response Thus there are at least three independent layers of defense between hello internet and DNS01 via its cloud service preventing unauthorized/inappropriate access.</span></span>

#### <a name="denied-internet-toosql-access-through-firewall"></a><span data-ttu-id="255ba-540">(Negato) Accesso a Internet tooSQL tramite Firewall</span><span class="sxs-lookup"><span data-stu-id="255ba-540">(Denied) Internet tooSQL access through Firewall</span></span>
1. <span data-ttu-id="255ba-541">L'utente Internet richiede dati SQL a SecSvc001.CloudApp.Net (servizio cloud per Internet).</span><span class="sxs-lookup"><span data-stu-id="255ba-541">Internet user requests SQL data from SecSvc001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="255ba-542">Poiché non sono presenti endpoint aperto per SQL, questo non raggiungerebbe hello servizio Cloud e non raggiunga firewall hello</span><span class="sxs-lookup"><span data-stu-id="255ba-542">Since there are no endpoints open for SQL, this would not pass hello Cloud Service and wouldn’t reach hello firewall</span></span>
3. <span data-ttu-id="255ba-543">Se gli endpoint SQL sono stati aperti per qualche motivo, il firewall hello inizierebbe l'elaborazione della regola:</span><span class="sxs-lookup"><span data-stu-id="255ba-543">If SQL endpoints were open for some reason, hello firewall would begin rule processing:</span></span>
   1. <span data-ttu-id="255ba-544">FW regola 1 (FW Mgmt) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-544">FW Rule 1 (FW Mgmt) doesn’t apply, move toonext rule</span></span>
   2. <span data-ttu-id="255ba-545">Regole FW 2-5 (regole di RDP) non si applicano, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-545">FW Rules 2 - 5 (RDP Rules) don’t apply, move toonext rule</span></span>
   3. <span data-ttu-id="255ba-546">Non applicare, spostare toonext regola FW regola 6 e 7 (regole di applicazione)</span><span class="sxs-lookup"><span data-stu-id="255ba-546">FW Rule 6 & 7 (Application Rules) don’t apply, move toonext rule</span></span>
   4. <span data-ttu-id="255ba-547">FW regola 8 (tooInternet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-547">FW Rule 8 (tooInternet) doesn’t apply, move toonext rule</span></span>
   5. <span data-ttu-id="255ba-548">Non applicare FW regola 9 (DNS), spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-548">FW Rule 9 (DNS) doesn’t apply, move toonext rule</span></span>
   6. <span data-ttu-id="255ba-549">FW regola 10 (Intra-Subnet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="255ba-549">FW Rule 10 (Intra-Subnet) doesn’t apply, move toonext rule</span></span>
   7. <span data-ttu-id="255ba-550">Regole firewall 11 (Deny All) applicabile, il traffico viene bloccato, l'elaborazione della regola si arresta.</span><span class="sxs-lookup"><span data-stu-id="255ba-550">FW Rule 11 (Deny All) does apply, traffic is blocked, stop rule processing</span></span>

## <a name="references"></a><span data-ttu-id="255ba-551">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="255ba-551">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="255ba-552">Script principale e configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="255ba-552">Main Script and Network Config</span></span>
<span data-ttu-id="255ba-553">Salvare uno Script completo di hello in un file di script di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="255ba-553">Save hello Full Script in a PowerShell script file.</span></span> <span data-ttu-id="255ba-554">Salvare hello configurazione di rete in un file denominato "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="255ba-554">Save hello Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="255ba-555">Modificare le variabili definite dall'utente di hello in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="255ba-555">Modify hello user defined variables as needed.</span></span> <span data-ttu-id="255ba-556">Eseguire script hello, quindi seguire istruzioni di programma di installazione di un regola Firewall di hello precedente.</span><span class="sxs-lookup"><span data-stu-id="255ba-556">Run hello script, then follow hello Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="255ba-557">Script completo</span><span class="sxs-lookup"><span data-stu-id="255ba-557">Full Script</span></span>
<span data-ttu-id="255ba-558">Questo script verrà, in base alle variabili definite dall'utente hello:</span><span class="sxs-lookup"><span data-stu-id="255ba-558">This script will, based on hello user defined variables:</span></span>

1. <span data-ttu-id="255ba-559">Connettersi tooan sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="255ba-559">Connect tooan Azure subscription</span></span>
2. <span data-ttu-id="255ba-560">Creare un nuovo account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="255ba-560">Create a new storage account</span></span>
3. <span data-ttu-id="255ba-561">Creare una nuova rete virtuale e tre le subnet, come definito nel file di configurazione di rete hello</span><span class="sxs-lookup"><span data-stu-id="255ba-561">Create a new VNet and three subnets as defined in hello Network Config file</span></span>
4. <span data-ttu-id="255ba-562">Compilare cinque macchine virtuali, 1 firewall e 4 VM Windows Server.</span><span class="sxs-lookup"><span data-stu-id="255ba-562">Build five virtual machines; 1 firewall and 4 windows server VMs</span></span>
5. <span data-ttu-id="255ba-563">Configurare il routing definito dall'utente, incluse le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="255ba-563">Configure UDR including:</span></span>
   1. <span data-ttu-id="255ba-564">Creazione di due nuove tabelle di route.</span><span class="sxs-lookup"><span data-stu-id="255ba-564">Creating two new route tables</span></span>
   2. <span data-ttu-id="255ba-565">Aggiungere le route toohello tabelle</span><span class="sxs-lookup"><span data-stu-id="255ba-565">Add routes toohello tables</span></span>
   3. <span data-ttu-id="255ba-566">Associare subnet tooappropriate tabelle</span><span class="sxs-lookup"><span data-stu-id="255ba-566">Bind tables tooappropriate subnets</span></span>
6. <span data-ttu-id="255ba-567">Attivare l'inoltro IP hello NVA</span><span class="sxs-lookup"><span data-stu-id="255ba-567">Enable IP Forwarding on hello NVA</span></span>
7. <span data-ttu-id="255ba-568">Configurare il gruppo di sicurezza di rete, incluse le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="255ba-568">Configure NSG including:</span></span>
   1. <span data-ttu-id="255ba-569">Creazione di un gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="255ba-569">Creating a NSG</span></span>
   2. <span data-ttu-id="255ba-570">Aggiunta di una regola.</span><span class="sxs-lookup"><span data-stu-id="255ba-570">Adding a rule</span></span>
   3. <span data-ttu-id="255ba-571">Subnet appropriata toohello associazione hello NSG</span><span class="sxs-lookup"><span data-stu-id="255ba-571">Binding hello NSG toohello appropriate subnets</span></span>

<span data-ttu-id="255ba-572">Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="255ba-572">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="255ba-573">Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi.</span><span class="sxs-lookup"><span data-stu-id="255ba-573">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="255ba-574">Solo i messaggi di errore formattati in rosso possono indicare un problema.</span><span class="sxs-lookup"><span data-stu-id="255ba-574">Only error messages in red are cause for concern.</span></span>
> 
> 

    <# 
     .SYNOPSIS
      Example of DMZ and User Defined Routing in an isolated network (Azure only, no hybrid connections)

     .DESCRIPTION
      This script will build out a sample DMZ setup containing:
       - A default storage account for VM disks
       - Three new cloud services
       - Three Subnets (SecNet, FrontEnd, and BackEnd subnets)
       - A Network Virtual Appliance (NVA), in this case a Barracuda NextGen Firewall
       - One server on hello FrontEnd Subnet
       - Three Servers on hello BackEnd Subnet
       - IP Forwading from hello FireWall out toohello internet
       - User Defined Routing FrontEnd and BackEnd Subnets toohello NVA

      Before running script, ensure hello network configuration file is created in
      hello directory referenced by $NetworkConfigFile variable (or update the
      variable tooreflect hello path and file name of hello config file being used).

     .Notes
      Everyone's security requirements are different and can be addressed in a myriad of ways.
      Please be sure that any sensitive data or applications are behind hello appropriate
      layer(s) of protection. This script serves as an example of some of hello techniques
      that can be used, but should not be used for all scenarios. You are responsible to
      assess your security needs and hello appropriate protections needed, and then effectively
      implement those protections.

      Security Service (SecNet subnet 10.0.0.0/24)
       myFirewall - 10.0.0.4

      FrontEnd Service (FrontEnd subnet 10.0.1.0/24)
       IIS01      - 10.0.1.4

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
        $SecureService = "SecSvc001"
        $FrontEndService = "FrontEnd001"
        $BackEndService = "BackEnd001"

      # Network Details
        $VNetName = "CorpNetwork"
        $VNetPrefix = "10.0.0.0/16"
        $SecNet = "SecNet"
        $FESubnet = "FrontEnd"
        $FEPrefix = "10.0.1.0/24"
        $BESubnet = "BackEnd"
        $BEPrefix = "10.0.2.0/24"
        $NetworkConfigFile = "C:\Scripts\NetworkConf3.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # UDR Details
        $FERouteTableName = "FrontEndSubnetRouteTable"
        $BERouteTableName = "BackEndSubnetRouteTable"

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: tooensure UDR and IP forwarding is setup
        # properly this script requires VM 0 be hello NVA.

        # VM 0 - hello Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $SecureService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $SecNet
          $VMIP += "10.0.0.4"

        # VM 1 - hello Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

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

    If (Test-AzureName -Service -Name $SecureService) { 
        Write-Host "hello SecureService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use." -ForegroundColor Green}

    If (Test-AzureName -Service -Name $FrontEndService) { 
        Write-Host "hello FrontEndService service name is already in use, please pick a different service name." -ForegroundColor Yellow
        $FatalError = $true}
    Else { Write-Host "hello FrontEndService service name is valid for use" -ForegroundColor Green}

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
        New-AzureService -Location $DeploymentLocation -ServiceName $SecureService -ErrorAction Stop
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
                # Note: All traffic goes through hello firewall, so we'll need tooset up all ports here.
                #       Also, hello firewall will be redirecting traffic tooa new IP and Port in a forwarding
                #       rule, so all of these endpoint have hello same public and local port and hello firewall
                #       will do hello mapping, NATing, and/or redirection as declared in hello firewall rules.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPWeb"    -Protocol tcp -PublicPort 8014 -LocalPort 8014 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp1"   -Protocol tcp -PublicPort 8025 -LocalPort 8025 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPApp2"   -Protocol tcp -PublicPort 8026 -LocalPort 8026 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "RDPDNS01"  -Protocol tcp -PublicPort 8024 -LocalPort 8024 -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when hello appliance is created.
                }
            Else
                {
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Windows -AdminUsername $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    Set-AzureVMMicrosoftAntimalwareExtension -AntimalwareConfiguration '{"AntimalwareEnabled" : true}' | `
                    Remove-AzureEndpoint -Name "RemoteDesktop" | `
                    Remove-AzureEndpoint -Name "PowerShell" | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                }
            $i++
        }

    # Configure UDR and IP Forwarding
        Write-Host "Configuring UDR" -ForegroundColor Cyan

      # Create hello Route Tables
        Write-Host "Creating hello Route Tables" -ForegroundColor Cyan 
        New-AzureRouteTable -Name $BERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $BESubnet subnet"
        New-AzureRouteTable -Name $FERouteTableName `
            -Location $DeploymentLocation `
            -Label "Route table for $FESubnet subnet"

      # Add Routes tooRoute Tables
        Write-Host "Adding Routes toohello Route Tables" -ForegroundColor Cyan 
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $BERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $BEPrefix `
            -NextHopType VNETLocal
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "All traffic tooFW" -AddressPrefix 0.0.0.0/0 `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Internal traffic tooFW" -AddressPrefix $VNetPrefix `
            -NextHopType VirtualAppliance `
            -NextHopIpAddress $VMIP[0]
        Get-AzureRouteTable $FERouteTableName `
            |Set-AzureRoute -RouteName "Allow Intra-Subnet Traffic" -AddressPrefix $FEPrefix `
            -NextHopType VNETLocal

      # Assoicate hello Route Tables with hello Subnets
        Write-Host "Binding Route Tables toohello Subnets" -ForegroundColor Cyan 
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $BESubnet `
            -RouteTableName $BERouteTableName
        Set-AzureSubnetRouteTable -VirtualNetworkName $VNetName `
            -SubnetName $FESubnet `
            -RouteTableName $FERouteTableName

     # Enable IP Forwarding on hello Virtual Appliance
        Get-AzureVM -Name $VMName[0] -ServiceName $ServiceName[0] `
            |Set-AzureIPForwarding -Enable

    # Configure NSG
        Write-Host "Configuring hello Network Security Group (NSG)" -ForegroundColor Cyan

      # Build hello NSG
        Write-Host "Building hello NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rule
        Write-Host "Writing rules into hello NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Isolate hello $VNetName VNet from hello Internet" -Type Inbound -Priority 100 -Action Deny `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '*' `
            -Protocol *

      # Assign hello NSG tootwo Subnets
        # hello NSG is *not* bound toohello Security Subnet. hello result
        # is that internet traffic flows only toohello Security subnet
        # since hello NSG bound toohello Frontend and Backback subnets
        # will Deny internet traffic toothose subnets.
        Write-Host "Binding hello NSG tootwo subnets" -ForegroundColor Cyan
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


#### <a name="network-config-file"></a><span data-ttu-id="255ba-575">File di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="255ba-575">Network Config File</span></span>
<span data-ttu-id="255ba-576">Salvare il file xml con posizione aggiornata e aggiungere hello collegamento toothis file toohello $NetworkConfigFile variabile nello script hello precedente.</span><span class="sxs-lookup"><span data-stu-id="255ba-576">Save this xml file with updated location and add hello link toothis file toohello $NetworkConfigFile variable in hello script above.</span></span>

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
              <Subnet name="SecNet">
                <AddressPrefix>10.0.0.0/24</AddressPrefix>
              </Subnet>
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

#### <a name="sample-application-scripts"></a><span data-ttu-id="255ba-577">Script di applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="255ba-577">Sample Application Scripts</span></span>
<span data-ttu-id="255ba-578">Se si desidera tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="255ba-578">If you wish tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3design.png "Rete perimetrale bidirezionale con appliance virtuale di rete, gruppo di sicurezza di rete e routing definito dall'utente"
[2]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/example3firewalllogical.png "Vista logica di hello regole del Firewall"
[3]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectfrontend.png "Creare un oggetto di rete front-end"
[4]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectdns.png "Creare un oggetto server DNS"
[5]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpa.png "Copiare la regola RDP predefinita"
[6]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/createnetworkobjectrdpb.png "Regola AppVM01"
[7]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconapplicationredirect.png "Icona di reindirizzamento dell'applicazione"
[8]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/icondestinationnat.png "Icona di Destination NAT"
[9]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/iconpass.png "Icona di passaggio"
[10]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulefirewall.png "Regola di gestione del firewall"
[11]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/rulerdp.png "Regola firewall RDP"
[12]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleweb.png "Regola firewall Web"
[13]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleappvm01.png "Regola firewall AppVM01"
[14]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleoutbound.png "Regola firewall in uscita"
[15]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledns.png "Regola firewall DNS"
[16]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruleintravnet.png "Regola firewall Intra-VNet"
[17]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/ruledeny.png "Regola firewall Deny"
[18]: ./media/virtual-networks-dmz-nsg-fw-udr-asm/firewallruleactivate.png "Attivazione delle regole firewall"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
