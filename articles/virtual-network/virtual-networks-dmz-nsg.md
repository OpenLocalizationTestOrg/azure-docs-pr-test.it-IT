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
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="08949-103">Esempio 1: Creare una rete perimetrale semplice usando gruppi di sicurezza di rete con un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08949-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="08949-104">[Restituire la pagina sicurezza limite Best Practices toohello][HOME]</span><span class="sxs-lookup"><span data-stu-id="08949-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="08949-105">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08949-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="08949-106">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="08949-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="08949-107">Questo esempio descrive come creare una rete perimetrale primitiva con quattro server Windows e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="08949-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="08949-108">In questo esempio viene descritto ciascun hello modello pertinenti sezioni tooprovide una comprensione più approfondita di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="08949-108">This example describes each of hello relevant template sections tooprovide a deeper understanding of each step.</span></span> <span data-ttu-id="08949-109">È inoltre disponibile un tooprovide sezione Scenario traffico dettagliate approfondimenti sulla modalità di prosecuzione di traffico tramite i livelli di difesa hello DMZ hello.</span><span class="sxs-lookup"><span data-stu-id="08949-109">There is also a Traffic Scenario section tooprovide an in-depth step-by-step look at how traffic proceeds through hello layers of defense in hello DMZ.</span></span> <span data-ttu-id="08949-110">Infine, nella sezione dei riferimenti hello è toobuild di codice e le istruzioni modello completa hello questo ambiente tootest e sperimentare vari scenari.</span><span class="sxs-lookup"><span data-stu-id="08949-110">Finally, in hello references section is hello complete template code and instructions toobuild this environment tootest and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="08949-111">![Rete perimetrale in ingresso con gruppo di sicurezza di rete][1]</span><span class="sxs-lookup"><span data-stu-id="08949-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="08949-112">Descrizione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="08949-112">Environment description</span></span>
<span data-ttu-id="08949-113">In questo esempio una sottoscrizione contiene hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="08949-113">In this example a subscription contains hello following resources:</span></span>

* <span data-ttu-id="08949-114">Un unico gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="08949-114">A single resource group</span></span>
* <span data-ttu-id="08949-115">Una rete virtuale con due subnet: front-end e back-end</span><span class="sxs-lookup"><span data-stu-id="08949-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="08949-116">Un gruppo di sicurezza di rete che viene applicato tooboth subnet</span><span class="sxs-lookup"><span data-stu-id="08949-116">A Network Security Group that is applied tooboth subnets</span></span>
* <span data-ttu-id="08949-117">Un server Windows che rappresenta un server Web applicazioni ("IIS01").</span><span class="sxs-lookup"><span data-stu-id="08949-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="08949-118">Due server Windows che rappresentano i server applicazioni back-end ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="08949-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="08949-119">Un server Windows che rappresenta un server DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="08949-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="08949-120">Un indirizzo IP pubblico associato hello applicazione web server</span><span class="sxs-lookup"><span data-stu-id="08949-120">A public IP address associated with hello application web server</span></span>

<span data-ttu-id="08949-121">Nella sezione dei riferimenti, hello è un modello di gestione risorse di Azure tooan collegamento che consente di creare ambiente hello descritta in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="08949-121">In hello references section, there is a link tooan Azure Resource Manager template that builds hello environment described in this example.</span></span> <span data-ttu-id="08949-122">Macchine virtuali hello di compilazione e le reti virtuali, anche se l'operazione eseguita dal modello di esempio hello, non sono descritti in dettaglio in questo documento.</span><span class="sxs-lookup"><span data-stu-id="08949-122">Building hello VMs and Virtual Networks, although done by hello example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="08949-123">**toobuild questo ambiente** (istruzioni dettagliate sono nella sezione dei riferimenti hello di questo documento);</span><span class="sxs-lookup"><span data-stu-id="08949-123">**toobuild this environment** (detailed instructions are in hello references section of this document);</span></span>

1. <span data-ttu-id="08949-124">Distribuire hello modello di gestione risorse di Azure in: [modelli di avvio rapido di Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="08949-124">Deploy hello Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="08949-125">Installare l'applicazione di esempio hello in: [Script dell'applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="08949-125">Install hello sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="08949-126">server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella."</span><span class="sxs-lookup"><span data-stu-id="08949-126">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="08949-127">Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="08949-127">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span> <span data-ttu-id="08949-128">In alternativa è possibile associare un indirizzo IP alla scheda di interfaccia di rete di ogni server per semplificare la connessione tramite RDP.</span><span class="sxs-lookup"><span data-stu-id="08949-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="08949-129">Hello sezioni seguenti forniscono una descrizione dettagliata di hello il gruppo di sicurezza di rete e il funzionamento di questo esempio, illustrando le righe di chiave di hello il modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="08949-129">hello following sections provide a detailed description of hello Network Security Group and how it functions for this example by walking through key lines of hello Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="08949-130">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="08949-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="08949-131">Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono caricate sei regole.</span><span class="sxs-lookup"><span data-stu-id="08949-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="08949-132">In genere, si deve creare regole "Consenti" specifiche prima e quindi hello ultima più generico "Deny" regole.</span><span class="sxs-lookup"><span data-stu-id="08949-132">Generally speaking, you should create your specific “Allow” rules first and then hello more generic “Deny” rules last.</span></span> <span data-ttu-id="08949-133">Hello assegnata la priorità determina quali regole vengono valutate per prime.</span><span class="sxs-lookup"><span data-stu-id="08949-133">hello assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="08949-134">Una volta traffico trovato tooapply tooa specifica regola, non vengono valutate altre regole.</span><span class="sxs-lookup"><span data-stu-id="08949-134">Once traffic is found tooapply tooa specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="08949-135">Possono essere applicate regole di gruppo in hello nella direzione in ingresso o in uscita (dalla prospettiva di hello della subnet hello).</span><span class="sxs-lookup"><span data-stu-id="08949-135">NSG rules can apply in either in hello inbound or outbound direction (from hello perspective of hello subnet).</span></span>
>
>

<span data-ttu-id="08949-136">In modo dichiarativo, hello segue le regole è compilato per il traffico in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-136">Declaratively, hello following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="08949-137">Il traffico DNS interno (porta 53) è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="08949-138">È consentito il traffico RDP (porta 3389) da hello Internet tooany VM</span><span class="sxs-lookup"><span data-stu-id="08949-138">RDP traffic (port 3389) from hello Internet tooany VM is allowed</span></span>
3. <span data-ttu-id="08949-139">È consentito il traffico HTTP (porta 80) dal server di tooweb Internet hello (IIS01)</span><span class="sxs-lookup"><span data-stu-id="08949-139">HTTP traffic (port 80) from hello Internet tooweb server (IIS01) is allowed</span></span>
4. <span data-ttu-id="08949-140">È consentito qualsiasi tipo di traffico (tutte le porte) da IIS01 tooAppVM1</span><span class="sxs-lookup"><span data-stu-id="08949-140">Any traffic (all ports) from IIS01 tooAppVM1 is allowed</span></span>
5. <span data-ttu-id="08949-141">Qualsiasi tipo di traffico (tutte le porte) da hello Internet toohello viene negato l'intera rete virtuale (entrambi subnet)</span><span class="sxs-lookup"><span data-stu-id="08949-141">Any traffic (all ports) from hello Internet toohello entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="08949-142">Qualsiasi tipo di traffico (tutte le porte) dalla subnet di back-end toohello subnet front-end hello negato</span><span class="sxs-lookup"><span data-stu-id="08949-142">Any traffic (all ports) from hello Frontend subnet toohello Backend subnet is Denied</span></span>

<span data-ttu-id="08949-143">Con queste subnet associata tooeach regole, se una richiesta HTTP in ingresso dal server web toohello Internet hello entrambi regole 3 (Consenti) e 5 (Nega) verrà applicata, ma poiché la regola 3 ha una priorità più alta solo esso viene applicato e regola 5 sarebbe non entrano in gioco.</span><span class="sxs-lookup"><span data-stu-id="08949-143">With these rules bound tooeach subnet, if an HTTP request was inbound from hello Internet toohello web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="08949-144">Richiesta HTTP hello sarebbe è pertanto a server web toohello.</span><span class="sxs-lookup"><span data-stu-id="08949-144">Thus hello HTTP request would be allowed toohello web server.</span></span> <span data-ttu-id="08949-145">Se il traffico stesso cercava server DNS01 di hello tooreach, regola 5 (Nega) sarebbe hello prima tooapply hello il traffico e non sarebbe consentito toopass toohello server.</span><span class="sxs-lookup"><span data-stu-id="08949-145">If that same traffic was trying tooreach hello DNS01 server, rule 5 (Deny) would be hello first tooapply and hello traffic would not be allowed toopass toohello server.</span></span> <span data-ttu-id="08949-146">Regola 6 (Nega) Blocca subnet front-end hello dalla conversazione toohello subnet di back-end (ad eccezione di traffico consentito nelle regole 1 e 4), il set di regole protegge rete back-end hello nel caso in cui un'utente malintenzionato compromette hello applicazione web sul front-end hello autore dell'attacco hello sarebbe non dispongono di accesso toohello back-end "protetto" rete (solo tooresources esposte nel server AppVM01 hello).</span><span class="sxs-lookup"><span data-stu-id="08949-146">Rule 6 (Deny) blocks hello Frontend subnet from talking toohello Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects hello Backend network in case an attacker compromises hello web application on hello Frontend, hello attacker would have limited access toohello Backend “protected” network (only tooresources exposed on hello AppVM01 server).</span></span>

<span data-ttu-id="08949-147">Una regola in uscita predefinito che consente il traffico in uscita toohello internet.</span><span class="sxs-lookup"><span data-stu-id="08949-147">There is a default outbound rule that allows traffic out toohello internet.</span></span> <span data-ttu-id="08949-148">Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="08949-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="08949-149">tooapply tootraffic criteri di sicurezza in entrambe le direzioni, Routing definito dall'utente è obbligatorio e viene esaminata in "Esempio 3" in hello [pagina migliori procedure consigliate di sicurezza limite][HOME].</span><span class="sxs-lookup"><span data-stu-id="08949-149">tooapply security policy tootraffic in both directions, User Defined Routing is required and is explored in “Example 3” on hello [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="08949-150">Ogni regola viene illustrata in dettaglio nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="08949-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="08949-151">Una risorsa del gruppo di sicurezza di rete deve essere stata creata un'istanza toohold hello regole:</span><span class="sxs-lookup"><span data-stu-id="08949-151">A Network Security Group resource must be instantiated toohold hello rules:</span></span>

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

2. <span data-ttu-id="08949-152">prima regola di Hello in questo esempio consente il traffico DNS tra tutti i server DNS di toohello reti interne nella subnet back-end hello.</span><span class="sxs-lookup"><span data-stu-id="08949-152">hello first rule in this example allows DNS traffic between all internal networks toohello DNS server on hello backend subnet.</span></span> <span data-ttu-id="08949-153">regola di Hello include alcuni parametri importanti:</span><span class="sxs-lookup"><span data-stu-id="08949-153">hello rule has some important parameters:</span></span>
  * <span data-ttu-id="08949-154">Questi tag sono identificatori forniti dal sistema che consentono di tooaddress un modo semplice una categoria di dimensioni maggiore di prefissi di indirizzo "destinationAddressPrefix" - regole di possono utilizzare un tipo speciale di prefisso dell'indirizzo denominato "Tag predefinito".</span><span class="sxs-lookup"><span data-stu-id="08949-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way tooaddress a larger category of address prefixes.</span></span> <span data-ttu-id="08949-155">Questa regola utilizza hello Tag predefinito "Internet" toosignify qualche indirizzo di fuori di hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="08949-155">This rule uses hello Default Tag “Internet” toosignify any address outside of hello VNet.</span></span> <span data-ttu-id="08949-156">Altre etichette di prefisso sono VirtualNetwork e AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="08949-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="08949-157">"Direction" indica la direzione del flusso di traffico a cui verrà applicata questa regola</span><span class="sxs-lookup"><span data-stu-id="08949-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="08949-158">direzione Hello è dal punto di vista di hello di subnet hello o macchina virtuale (in base a cui è associato questo gruppo).</span><span class="sxs-lookup"><span data-stu-id="08949-158">hello direction is from hello perspective of hello subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="08949-159">In questo modo se direzione è "Inbound" e il traffico sta entrando in subnet hello, verrà applicata la regola hello e traffico lasciando subnet hello potrebbe non essere interessato da questa regola.</span><span class="sxs-lookup"><span data-stu-id="08949-159">Thus if Direction is “Inbound” and traffic is entering hello subnet, hello rule would apply and traffic leaving hello subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="08949-160">"Priority" imposta hello l'ordine in cui viene valutato un flusso di traffico.</span><span class="sxs-lookup"><span data-stu-id="08949-160">“Priority” sets hello order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="08949-161">Hello hello numero hello superiore hello priorità inferiore.</span><span class="sxs-lookup"><span data-stu-id="08949-161">hello lower hello number hello higher hello priority.</span></span> <span data-ttu-id="08949-162">Quando il flusso di traffico specifico tooa si applica una regola, non vengono elaborate ulteriori regole.</span><span class="sxs-lookup"><span data-stu-id="08949-162">When a rule applies tooa specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="08949-163">Pertanto se una regola con priorità 1 consente il traffico e una regola con priorità 2 impedisca il traffico, entrambe le regole si applicano tootraffic quindi sia possibile usare il traffico hello tooflow (poiché la regola 1 ha una priorità più alta da cui ha effetto e non altre regole sono state applicate).</span><span class="sxs-lookup"><span data-stu-id="08949-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply tootraffic then hello traffic would be allowed tooflow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="08949-164">"Access" indica se il traffico a cui si applica la regola viene bloccato ("Deny") o consentito ("Allow").</span><span class="sxs-lookup"><span data-stu-id="08949-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

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

3. <span data-ttu-id="08949-165">Questa regola consente di tooflow il traffico RDP da hello internet toohello la porta RDP in qualsiasi server in hello associato subnet.</span><span class="sxs-lookup"><span data-stu-id="08949-165">This rule allows RDP traffic tooflow from hello internet toohello RDP port on any server on hello bound subnet.</span></span> 

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

4. <span data-ttu-id="08949-166">Questa regola consente di server web in ingresso internet traffico toohit hello.</span><span class="sxs-lookup"><span data-stu-id="08949-166">This rule allows inbound internet traffic toohit hello web server.</span></span> <span data-ttu-id="08949-167">Questa regola non modifica il comportamento di routing hello.</span><span class="sxs-lookup"><span data-stu-id="08949-167">This rule does not change hello routing behavior.</span></span> <span data-ttu-id="08949-168">regola di Hello consente solo il traffico destinato IIS01 toopass.</span><span class="sxs-lookup"><span data-stu-id="08949-168">hello rule only allows traffic destined for IIS01 toopass.</span></span> <span data-ttu-id="08949-169">Pertanto se il traffico proveniente da Internet hello disponesse di server web hello come destinazione di questa regola consente e arrestare l'elaborazione di altre regole.</span><span class="sxs-lookup"><span data-stu-id="08949-169">Thus if traffic from hello Internet had hello web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="08949-170">(Regola hello priorità 140 tutte le altre traffico in ingresso internet è bloccato).</span><span class="sxs-lookup"><span data-stu-id="08949-170">(In hello rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="08949-171">Se si sta elaborando solo il traffico HTTP, questa regola può essere ulteriormente limitato tooonly Consenti destinazione la porta 80.</span><span class="sxs-lookup"><span data-stu-id="08949-171">If you're only processing HTTP traffic, this rule could be further restricted tooonly allow Destination Port 80.</span></span>

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

5. <span data-ttu-id="08949-172">Questa regola consente il traffico toopass dal server IIS01 hello toohello AppVM01 server, una regola successiva blocca tutto il traffico tooBackend altri server front-end.</span><span class="sxs-lookup"><span data-stu-id="08949-172">This rule allows traffic toopass from hello IIS01 server toohello AppVM01 server, a later rule blocks all other Frontend tooBackend traffic.</span></span> <span data-ttu-id="08949-173">tooimprove questa regola, se la porta hello è noto che deve essere aggiunti.</span><span class="sxs-lookup"><span data-stu-id="08949-173">tooimprove this rule, if hello port is known that should be added.</span></span> <span data-ttu-id="08949-174">Ad esempio, se il server IIS hello sta impegnando solo SQL Server in AppVM01, hello intervallo di porte di destinazione deve essere modificato da "*" (Any) too1433 (porta SQL Buongiorno) consentendo in tal modo una superficie di attacco in ingresso più piccola in AppVM01 deve hello web applicazione dovesse essere compromessa.</span><span class="sxs-lookup"><span data-stu-id="08949-174">For example, if hello IIS server is hitting only SQL Server on AppVM01, hello Destination Port Range should be changed from “*” (Any) too1433 (hello SQL port) thus allowing a smaller inbound attack surface on AppVM01 should hello web application ever be compromised.</span></span>

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

6. <span data-ttu-id="08949-175">Questa regola impedisce il traffico da hello internet tooany server hello rete.</span><span class="sxs-lookup"><span data-stu-id="08949-175">This rule denies traffic from hello internet tooany servers on hello network.</span></span> <span data-ttu-id="08949-176">Con regole di hello priorità 110 e 120, effetto hello è tooallow solo internet traffico toohello firewall in entrata e le porte RDP nel server e blocca tutto il resto.</span><span class="sxs-lookup"><span data-stu-id="08949-176">With hello rules at priority 110 and 120, hello effect is tooallow only inbound internet traffic toohello firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="08949-177">Questa regola è "alternativo" regola tooblock tutti i flussi imprevisti.</span><span class="sxs-lookup"><span data-stu-id="08949-177">This rule is a "fail-safe" rule tooblock all unexpected flows.</span></span>

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

7. <span data-ttu-id="08949-178">regola finale Hello impedisca il traffico dalla subnet di back-end toohello subnet front-end hello.</span><span class="sxs-lookup"><span data-stu-id="08949-178">hello final rule denies traffic from hello Frontend subnet toohello Backend subnet.</span></span> <span data-ttu-id="08949-179">Poiché questa regola è una regola sola in ingresso, è consentito traffico inverso (da hello back-end toohello front-end).</span><span class="sxs-lookup"><span data-stu-id="08949-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from hello Backend toohello Frontend).</span></span>

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

## <a name="traffic-scenarios"></a><span data-ttu-id="08949-180">Scenari di traffico</span><span class="sxs-lookup"><span data-stu-id="08949-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-tooweb-server"></a><span data-ttu-id="08949-181">(*Consentito*) server tooweb Internet</span><span class="sxs-lookup"><span data-stu-id="08949-181">(*Allowed*) Internet tooweb server</span></span>
1. <span data-ttu-id="08949-182">Un utente internet richiede una pagina HTTP da indirizzo IP pubblico hello di hello che NIC associato hello IIS01 NIC</span><span class="sxs-lookup"><span data-stu-id="08949-182">An internet user requests an HTTP page from hello public IP address of hello NIC associated with hello IIS01 NIC</span></span>
2. <span data-ttu-id="08949-183">indirizzo IP pubblico Hello passa toohello il traffico tra reti virtuali verso IIS01 (server web hello)</span><span class="sxs-lookup"><span data-stu-id="08949-183">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="08949-184">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-185">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-185">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="08949-186">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-186">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="08949-187">Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="08949-187">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="08949-188">Traffico raggiunge l'indirizzo IP interno del server web hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="08949-188">Traffic hits internal IP address of hello web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="08949-189">Iis01 è in ascolto per il traffico web, riceve la richiesta e avvia l'elaborazione richiesta hello</span><span class="sxs-lookup"><span data-stu-id="08949-189">IIS01 is listening for web traffic, receives this request and starts processing hello request</span></span>
6. <span data-ttu-id="08949-190">Iis01 richiede SQL Server hello su AppVM01 per informazioni</span><span class="sxs-lookup"><span data-stu-id="08949-190">IIS01 asks hello SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="08949-191">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="08949-192">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-192">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-193">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-193">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="08949-194">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-194">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="08949-195">GRUPPO regola 3 (tooFirewall Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-195">NSG Rule 3 (Internet tooFirewall) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="08949-196">Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="08949-196">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="08949-197">AppVM01 riceve hello Query SQL e risponde</span><span class="sxs-lookup"><span data-stu-id="08949-197">AppVM01 receives hello SQL Query and responds</span></span>
10. <span data-ttu-id="08949-198">Poiché non esistono regole in uscita nella subnet back-end hello, risposta hello è consentito</span><span class="sxs-lookup"><span data-stu-id="08949-198">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
11. <span data-ttu-id="08949-199">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-200">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="08949-200">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="08949-201">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-201">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
12. <span data-ttu-id="08949-202">server IIS Hello riceve risposta SQL hello e completa di risposta HTTP hello e invia toohello richiedente</span><span class="sxs-lookup"><span data-stu-id="08949-202">hello IIS server receives hello SQL response and completes hello HTTP response and sends toohello requester</span></span>
13. <span data-ttu-id="08949-203">Poiché non esistono regole in uscita nella subnet front-end hello, risposta hello è consentito e hello utente Internet riceve hello web pagina richiesta.</span><span class="sxs-lookup"><span data-stu-id="08949-203">Since there are no outbound rules on hello Frontend subnet, hello response is allowed and hello Internet User receives hello web page requested.</span></span>

#### <a name="allowed-rdp-tooiis-server"></a><span data-ttu-id="08949-204">(*Consentito*) server tooIIS RDP</span><span class="sxs-lookup"><span data-stu-id="08949-204">(*Allowed*) RDP tooIIS server</span></span>
1. <span data-ttu-id="08949-205">Un amministratore del Server su internet richiede un tooIIS01 sessione RDP in indirizzo IP pubblico hello di hello che NIC associato hello NIC IIS01 (questo indirizzo IP pubblico è disponibile tramite hello portale o PowerShell)</span><span class="sxs-lookup"><span data-stu-id="08949-205">A Server Admin on internet requests an RDP session tooIIS01 on hello public IP address of hello NIC associated with hello IIS01 NIC (this public IP address can be found via hello Portal or PowerShell)</span></span>
2. <span data-ttu-id="08949-206">indirizzo IP pubblico Hello passa toohello il traffico tra reti virtuali verso IIS01 (server web hello)</span><span class="sxs-lookup"><span data-stu-id="08949-206">hello Public IP address passes traffic toohello VNet towards IIS01 (hello web server)</span></span>
3. <span data-ttu-id="08949-207">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-208">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-208">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="08949-209">Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="08949-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="08949-210">Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="08949-211">La sessione RDP è abilitata.</span><span class="sxs-lookup"><span data-stu-id="08949-211">RDP session is enabled</span></span>
6. <span data-ttu-id="08949-212">Iis01 chiesta la password e il nome utente hello</span><span class="sxs-lookup"><span data-stu-id="08949-212">IIS01 prompts for hello user name and password</span></span>

>[!NOTE]
><span data-ttu-id="08949-213">server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella."</span><span class="sxs-lookup"><span data-stu-id="08949-213">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="08949-214">Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="08949-214">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="08949-215">(*Consentito*) Ricerca DNS del server Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="08949-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="08949-216">Web Server, IIS01, necessita di un feed di dati in www.data.gov, ma è necessario tooresolve hello indirizzo.</span><span class="sxs-lookup"><span data-stu-id="08949-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs tooresolve hello address.</span></span>
2. <span data-ttu-id="08949-217">Hello configurazione di rete per gli elenchi di rete virtuale hello DNS01 (10.0.2.4 nella subnet back-end hello) come server DNS primario hello, IIS01 invia hello DNS richiesta tooDNS01</span><span class="sxs-lookup"><span data-stu-id="08949-217">hello network configuration for hello VNet lists DNS01 (10.0.2.4 on hello Backend subnet) as hello primary DNS server, IIS01 sends hello DNS request tooDNS01</span></span>
3. <span data-ttu-id="08949-218">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="08949-219">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="08949-220">Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="08949-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="08949-221">Server DNS riceve una richiesta di hello</span><span class="sxs-lookup"><span data-stu-id="08949-221">DNS server receives hello request</span></span>
6. <span data-ttu-id="08949-222">Server DNS non dispone di indirizzo hello memorizzati nella cache e richiede un server radice DNS su hello internet</span><span class="sxs-lookup"><span data-stu-id="08949-222">DNS server doesn’t have hello address cached and asks a root DNS server on hello internet</span></span>
7. <span data-ttu-id="08949-223">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="08949-224">Server DNS Internet risponde, poiché questa sessione è stata avviata internamente, la risposta hello è consentita</span><span class="sxs-lookup"><span data-stu-id="08949-224">Internet DNS server responds, since this session was initiated internally, hello response is allowed</span></span>
9. <span data-ttu-id="08949-225">Server DNS memorizza nella cache la risposta hello e risponde toohello richiesta iniziale indietro tooIIS01</span><span class="sxs-lookup"><span data-stu-id="08949-225">DNS server caches hello response, and responds toohello initial request back tooIIS01</span></span>
10. <span data-ttu-id="08949-226">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="08949-227">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-228">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="08949-228">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="08949-229">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito</span><span class="sxs-lookup"><span data-stu-id="08949-229">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed</span></span>
12. <span data-ttu-id="08949-230">Iis01 riceve risposta hello da DNS01</span><span class="sxs-lookup"><span data-stu-id="08949-230">IIS01 receives hello response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="08949-231">(*Consentito*) Il server Web richiede l'accesso a un file in AppVM01</span><span class="sxs-lookup"><span data-stu-id="08949-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="08949-232">IIS01 richiede un file in AppVM01.</span><span class="sxs-lookup"><span data-stu-id="08949-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="08949-233">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="08949-234">subnet di back-end Hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-234">hello Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-235">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-235">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="08949-236">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-236">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="08949-237">GRUPPO regola 3 (tooIIS01 Internet) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-237">NSG Rule 3 (Internet tooIIS01) doesn’t apply, move toonext rule</span></span>
  4. <span data-ttu-id="08949-238">Applicare la regola gruppo 4 (IIS01 tooAppVM01), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="08949-238">NSG Rule 4 (IIS01 tooAppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="08949-239">AppVM01 riceve la richiesta di hello e risponde con il file (presupponendo che l'accesso è autorizzato)</span><span class="sxs-lookup"><span data-stu-id="08949-239">AppVM01 receives hello request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="08949-240">Poiché non esistono regole in uscita nella subnet back-end hello, risposta hello è consentito</span><span class="sxs-lookup"><span data-stu-id="08949-240">Since there are no outbound rules on hello Backend subnet, hello response is allowed</span></span>
6. <span data-ttu-id="08949-241">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-242">Nessuna regola di gruppo che si applica tooInbound traffico dalla subnet front-end toohello di subnet back-end di hello, pertanto nessuna delle regole NSG hello applicabile</span><span class="sxs-lookup"><span data-stu-id="08949-242">There is no NSG rule that applies tooInbound traffic from hello Backend subnet toohello Frontend subnet, so none of hello NSG rules apply</span></span>
  2. <span data-ttu-id="08949-243">regola di sistema predefinito Hello consenta il traffico tra subnet consente il traffico in modo hello traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="08949-243">hello default system rule allowing traffic between subnets would allow this traffic so hello traffic is allowed.</span></span>
7. <span data-ttu-id="08949-244">server IIS Hello riceve file hello</span><span class="sxs-lookup"><span data-stu-id="08949-244">hello IIS server receives hello file</span></span>

#### <a name="denied-rdp-toobackend"></a><span data-ttu-id="08949-245">(*Negato*) toobackend RDP</span><span class="sxs-lookup"><span data-stu-id="08949-245">(*Denied*) RDP toobackend</span></span>
1. <span data-ttu-id="08949-246">Un utente internet tenta tooRDP tooserver AppVM01</span><span class="sxs-lookup"><span data-stu-id="08949-246">An internet user tries tooRDP tooserver AppVM01</span></span>
2. <span data-ttu-id="08949-247">Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="08949-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="08949-248">Se tuttavia per qualunque motivo è stato abilitato un indirizzo IP pubblico, la regola del gruppo di sicurezza di rete 2 (RDP) consentirà questo traffico.</span><span class="sxs-lookup"><span data-stu-id="08949-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="08949-249">server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella."</span><span class="sxs-lookup"><span data-stu-id="08949-249">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="08949-250">Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="08949-250">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

#### <a name="denied-web-toobackend-server"></a><span data-ttu-id="08949-251">(*Negato*) server toobackend Web</span><span class="sxs-lookup"><span data-stu-id="08949-251">(*Denied*) Web toobackend server</span></span>
1. <span data-ttu-id="08949-252">Un utente internet tenta un file in AppVM01 tooaccess</span><span class="sxs-lookup"><span data-stu-id="08949-252">An internet user tries tooaccess a file on AppVM01</span></span>
2. <span data-ttu-id="08949-253">Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="08949-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="08949-254">Se un indirizzo IP pubblico è stato abilitato per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico</span><span class="sxs-lookup"><span data-stu-id="08949-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="08949-255">(*Negato*) Ricerca DNS Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="08949-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="08949-256">Un utente internet tenta toolook di un record DNS interno nella DNS01</span><span class="sxs-lookup"><span data-stu-id="08949-256">An internet user tries toolook up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="08949-257">Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="08949-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="08949-258">Se un indirizzo IP pubblico è stato abilitato per qualche motivo, la regola gruppo 5 (Internet tooVNet) bloccano il traffico (Nota: che regola 1 (DNS) potrebbero non applicarsi perché hello richiede l'indirizzo di origine è hello internet e regola 1 si applica solo a toohello rete locale virtuale come origine di hello)</span><span class="sxs-lookup"><span data-stu-id="08949-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet tooVNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because hello requests source address is hello internet and Rule 1 only applies toohello local VNet as hello source)</span></span>

#### <a name="denied-sql-access-on-hello-web-server"></a><span data-ttu-id="08949-259">(*Negato*) l'accesso a SQL Server web hello</span><span class="sxs-lookup"><span data-stu-id="08949-259">(*Denied*) SQL access on hello web server</span></span>
1. <span data-ttu-id="08949-260">Un utente su Internet richiede dati SQL da IIS01</span><span class="sxs-lookup"><span data-stu-id="08949-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="08949-261">Poiché non sono indirizzi IP pubblici associati a questa scheda di rete server, il traffico mai immettere hello rete virtuale e non raggiunga il server di hello</span><span class="sxs-lookup"><span data-stu-id="08949-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter hello VNet and wouldn’t reach hello server</span></span>
3. <span data-ttu-id="08949-262">Se un indirizzo IP pubblico è stato abilitato per qualche motivo, subnet front-end hello inizia l'elaborazione della regola in ingresso:</span><span class="sxs-lookup"><span data-stu-id="08949-262">If a Public IP address was enabled for some reason, hello Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="08949-263">GRUPPO regola 1 (DNS) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-263">NSG Rule 1 (DNS) doesn’t apply, move toonext rule</span></span>
  2. <span data-ttu-id="08949-264">GRUPPO regola 2 (RDP) non è applicabile, spostare toonext regola</span><span class="sxs-lookup"><span data-stu-id="08949-264">NSG Rule 2 (RDP) doesn’t apply, move toonext rule</span></span>
  3. <span data-ttu-id="08949-265">Applicare NSG regola 3 (tooIIS01 Internet), il traffico è l'elaborazione della regola consentita, arresto</span><span class="sxs-lookup"><span data-stu-id="08949-265">NSG Rule 3 (Internet tooIIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="08949-266">Traffico raggiunge l'indirizzo IP interno di hello IIS01 (10.0.1.5)</span><span class="sxs-lookup"><span data-stu-id="08949-266">Traffic hits internal IP address of hello IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="08949-267">Non è in ascolto sulla porta 1433, che non è più richiesta toohello risposta iis01</span><span class="sxs-lookup"><span data-stu-id="08949-267">IIS01 isn't listening on port 1433, so no response toohello request</span></span>

## <a name="conclusion"></a><span data-ttu-id="08949-268">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="08949-268">Conclusion</span></span>
<span data-ttu-id="08949-269">Questo esempio è un modo semplice e relativamente semplice isolare subnet back-end hello dal traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="08949-269">This example is a relatively simple and straight forward way of isolating hello back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="08949-270">Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].</span><span class="sxs-lookup"><span data-stu-id="08949-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="08949-271">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="08949-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="08949-272">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08949-272">Azure Resource Manager template</span></span>
<span data-ttu-id="08949-273">In questo esempio viene utilizzato un modello di gestione risorse di Azure predefinito in un repository GitHub gestito da Microsoft e aprire toohello community.</span><span class="sxs-lookup"><span data-stu-id="08949-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open toohello community.</span></span> <span data-ttu-id="08949-274">Questo modello può essere distribuito direttamente da GitHub, o scaricati e modificati toofit le proprie esigenze.</span><span class="sxs-lookup"><span data-stu-id="08949-274">This template can be deployed straight out of GitHub, or downloaded and modified toofit your needs.</span></span> 

<span data-ttu-id="08949-275">modello principale Hello è nel file hello denominato "azuredeploy.json".</span><span class="sxs-lookup"><span data-stu-id="08949-275">hello main template is in hello file named "azuredeploy.json."</span></span> <span data-ttu-id="08949-276">Questo modello può essere inviato tramite PowerShell o CLI (con file associato "azuredeploy.parameters.json" hello) toodeploy questo modello.</span><span class="sxs-lookup"><span data-stu-id="08949-276">This template can be submitted via PowerShell or CLI (with hello associated "azuredeploy.parameters.json" file) toodeploy this template.</span></span> <span data-ttu-id="08949-277">È possibile individuare hello più semplice consiste nel toouse hello pulsante "Distribuisci tooAzure" nella pagina README.md hello in GitHub.</span><span class="sxs-lookup"><span data-stu-id="08949-277">I find hello easiest way is toouse hello "Deploy tooAzure" button on hello README.md page at GitHub.</span></span>

<span data-ttu-id="08949-278">modello di hello toodeploy che si basa questo esempio da GitHub e hello portale di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="08949-278">toodeploy hello template that builds this example from GitHub and hello Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="08949-279">Da un browser, passare toohello [modello][Template]</span><span class="sxs-lookup"><span data-stu-id="08949-279">From a browser, navigate toohello [Template][Template]</span></span>
2. <span data-ttu-id="08949-280">Fare clic su pulsante "Distribuisci tooAzure" hello (o toosee di pulsante "Visualizza" hello una rappresentazione grafica del modello)</span><span class="sxs-lookup"><span data-stu-id="08949-280">Click hello "Deploy tooAzure" button (or hello "Visualize" button toosee a graphical representation of this template)</span></span>
3. <span data-ttu-id="08949-281">Immettere hello Account di archiviazione, nome utente e Password nel Pannello di hello parametri, quindi fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="08949-281">Enter hello Storage Account, User Name, and Password in hello Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="08949-282">Creare un gruppo di risorse per questa distribuzione. È possibile usarne uno esistente, ma è consigliabile creare una nuova istanza per risultati ottimali.</span><span class="sxs-lookup"><span data-stu-id="08949-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="08949-283">Se necessario, modificare le impostazioni di sottoscrizione e posizione hello per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="08949-283">If necessary, change hello Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="08949-284">Fare clic su **esaminare le note legali**, leggere le condizioni di hello e fare clic su **acquisto** tooagree.</span><span class="sxs-lookup"><span data-stu-id="08949-284">Click **Review legal terms**, read hello terms, and click **Purchase** tooagree.</span></span>
8. <span data-ttu-id="08949-285">Fare clic su **crea** distribuzione hello toobegin del modello.</span><span class="sxs-lookup"><span data-stu-id="08949-285">Click **Create** toobegin hello deployment of this template.</span></span>
9. <span data-ttu-id="08949-286">Al termine della distribuzione hello correttamente, è possibile passare toohello che gruppo di risorse creato per le risorse di hello toosee questa distribuzione configurata all'interno.</span><span class="sxs-lookup"><span data-stu-id="08949-286">Once hello deployment finishes successfully, navigate toohello Resource Group created for this deployment toosee hello resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="08949-287">Questo modello consente RDP toohello IIS01 solo server (ricerca hello, indirizzo IP pubblico per IIS01 su hello portale).</span><span class="sxs-lookup"><span data-stu-id="08949-287">This template enables RDP toohello IIS01 server only (find hello Public IP for IIS01 on hello Portal).</span></span> <span data-ttu-id="08949-288">server di back-end tooany tooRDP in questo caso, il server IIS hello viene utilizzato come una "salto casella."</span><span class="sxs-lookup"><span data-stu-id="08949-288">tooRDP tooany back-end servers in this instance, hello IIS server is used as a "jump box."</span></span> <span data-ttu-id="08949-289">Primo server IIS toohello RDP e quindi dal server di hello IIS Server RDP toohello back-end.</span><span class="sxs-lookup"><span data-stu-id="08949-289">First RDP toohello IIS server and then from hello IIS Server RDP toohello back-end server.</span></span>
>
>

<span data-ttu-id="08949-290">tooremove questa distribuzione, hello di eliminazione gruppo di risorse e tutte le risorse figlio saranno eliminate.</span><span class="sxs-lookup"><span data-stu-id="08949-290">tooremove this deployment, delete hello Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="08949-291">Script di applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="08949-291">Sample application scripts</span></span>
<span data-ttu-id="08949-292">Una volta modello hello viene eseguito correttamente, è possibile impostare server web hello e server di applicazioni con un tooallow di applicazione web semplice test con questa configurazione di rete Perimetrale.</span><span class="sxs-lookup"><span data-stu-id="08949-292">Once hello template runs successfully, you can set up hello web server and app server with a simple web application tooallow testing with this DMZ configuration.</span></span> <span data-ttu-id="08949-293">tooinstall un'applicazione di esempio per questo e altri esempi di rete Perimetrale, ne è stato fornito al collegamento hello: [Script dell'applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="08949-293">tooinstall a sample application for this, and other DMZ Examples, one has been provided at hello following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="08949-294">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="08949-294">Next steps</span></span>

* <span data-ttu-id="08949-295">Distribuire questo esempio</span><span class="sxs-lookup"><span data-stu-id="08949-295">Deploy this example</span></span>
* <span data-ttu-id="08949-296">Compilare l'applicazione di esempio hello</span><span class="sxs-lookup"><span data-stu-id="08949-296">Build hello sample application</span></span>
* <span data-ttu-id="08949-297">Testare diversi flussi di traffico attraverso la rete perimetrale</span><span class="sxs-lookup"><span data-stu-id="08949-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md