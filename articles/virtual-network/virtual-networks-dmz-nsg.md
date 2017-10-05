---
title: 'Esempio di rete perimetrale di Azure: Creare una rete perimetrale semplice con gruppi di sicurezza di rete | Microsoft Docs'
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
ms.openlocfilehash: ec29e6b250f927a3a4a94ffdf83d6c7c0e325722
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="example-1--build-a-simple-dmz-using-nsgs-with-an-azure-resource-manager-template"></a><span data-ttu-id="5d9ed-103">Esempio 1: Creare una rete perimetrale semplice usando gruppi di sicurezza di rete con un modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5d9ed-103">Example 1 – Build a simple DMZ using NSGs with an Azure Resource Manager template</span></span>
<span data-ttu-id="5d9ed-104">[Tornare alla pagina relativa alle procedure consigliate sui limiti di sicurezza][HOME]</span><span class="sxs-lookup"><span data-stu-id="5d9ed-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="5d9ed-105">Modello di Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5d9ed-105">Resource Manager Template</span></span>](virtual-networks-dmz-nsg.md)
> * [<span data-ttu-id="5d9ed-106">Classica: PowerShell</span><span class="sxs-lookup"><span data-stu-id="5d9ed-106">Classic - PowerShell</span></span>](virtual-networks-dmz-nsg-asm.md)
> 
>

<span data-ttu-id="5d9ed-107">Questo esempio descrive come creare una rete perimetrale primitiva con quattro server Windows e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-107">This example creates a primitive DMZ with four Windows servers and Network Security Groups.</span></span> <span data-ttu-id="5d9ed-108">Per comprendere in modo approfondito ogni passaggio, questo esempio descrive tutte le sezioni del modello pertinenti.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-108">This example describes each of the relevant template sections to provide a deeper understanding of each step.</span></span> <span data-ttu-id="5d9ed-109">È disponibile anche una sezione sugli scenari di traffico con istruzioni dettagliate sul percorso seguito dal traffico attraverso i livelli di difesa della rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-109">There is also a Traffic Scenario section to provide an in-depth step-by-step look at how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="5d9ed-110">La sezione Riferimenti, infine, include le istruzioni e il codice del modello completi per creare l'ambiente per testare e sperimentare vari scenari.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-110">Finally, in the references section is the complete template code and instructions to build this environment to test and experiment with various scenarios.</span></span> 

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)] 

<span data-ttu-id="5d9ed-111">![Rete perimetrale in ingresso con gruppo di sicurezza di rete][1]</span><span class="sxs-lookup"><span data-stu-id="5d9ed-111">![Inbound DMZ with NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="5d9ed-112">Descrizione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="5d9ed-112">Environment description</span></span>
<span data-ttu-id="5d9ed-113">Una sottoscrizione in questo esempio include le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-113">In this example a subscription contains the following resources:</span></span>

* <span data-ttu-id="5d9ed-114">Un unico gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5d9ed-114">A single resource group</span></span>
* <span data-ttu-id="5d9ed-115">Una rete virtuale con due subnet: front-end e back-end</span><span class="sxs-lookup"><span data-stu-id="5d9ed-115">A Virtual Network with two subnets; “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="5d9ed-116">Un gruppo di sicurezza di rete applicato a entrambe le subnet</span><span class="sxs-lookup"><span data-stu-id="5d9ed-116">A Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="5d9ed-117">Un server Windows che rappresenta un server Web applicazioni ("IIS01")</span><span class="sxs-lookup"><span data-stu-id="5d9ed-117">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="5d9ed-118">Due server Windows che rappresentano i server applicazioni back-end ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="5d9ed-118">Two windows servers that represent application back-end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="5d9ed-119">Un server Windows che rappresenta un server DNS ("DNS01")</span><span class="sxs-lookup"><span data-stu-id="5d9ed-119">A Windows server that represents a DNS server (“DNS01”)</span></span>
* <span data-ttu-id="5d9ed-120">Un indirizzo IP pubblico associato al server Web applicazioni</span><span class="sxs-lookup"><span data-stu-id="5d9ed-120">A public IP address associated with the application web server</span></span>

<span data-ttu-id="5d9ed-121">Un collegamento nella sezione Riferimenti a un modello di Azure Resource Manager compila l'ambiente descritto in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-121">In the references section, there is a link to an Azure Resource Manager template that builds the environment described in this example.</span></span> <span data-ttu-id="5d9ed-122">La creazione di VM e reti virtuali, anche se eseguita dal modello di esempio, non è descritta in dettaglio in questo documento.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-122">Building the VMs and Virtual Networks, although done by the example template, are not described in detail in this document.</span></span> 

<span data-ttu-id="5d9ed-123">**Per compilare questo ambiente**. Istruzioni dettagliate sono disponibili nella sezione Riferimenti di questo documento;</span><span class="sxs-lookup"><span data-stu-id="5d9ed-123">**To build this environment** (detailed instructions are in the references section of this document);</span></span>

1. <span data-ttu-id="5d9ed-124">Distribuire il modello di Azure Resource Manager in [Modelli di avvio rapido di Azure][Template]</span><span class="sxs-lookup"><span data-stu-id="5d9ed-124">Deploy the Azure Resource Manager Template at: [Azure Quickstart Templates][Template]</span></span>
2. <span data-ttu-id="5d9ed-125">Installare l'applicazione di esempio in: [Script di applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="5d9ed-125">Install the sample application at: [Sample Application Script][SampleApp]</span></span>

>[!NOTE]
><span data-ttu-id="5d9ed-126">Per eseguire la connessione tramite RDP ai server back-end in questa istanza, il server IIS viene usato come "jumpbox".</span><span class="sxs-lookup"><span data-stu-id="5d9ed-126">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="5d9ed-127">Eseguire prima la connessione tramite RDP al server IIS e, quindi, dal server IIS eseguire la connessione tramite RDP al server back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-127">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span> <span data-ttu-id="5d9ed-128">In alternativa è possibile associare un indirizzo IP alla scheda di interfaccia di rete di ogni server per semplificare la connessione tramite RDP.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-128">Alternately a Public IP can be associated with each server NIC for easier RDP.</span></span>
> 
>

<span data-ttu-id="5d9ed-129">Le sezioni seguenti descrivono in modo dettagliato il gruppo di sicurezza di rete e il relativo funzionamento per questo esempio spiegando le righe principali del modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-129">The following sections provide a detailed description of the Network Security Group and how it functions for this example by walking through key lines of the Azure Resource Manager Template.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="5d9ed-130">Gruppi di sicurezza di rete (NGS)</span><span class="sxs-lookup"><span data-stu-id="5d9ed-130">Network Security Groups (NSG)</span></span>
<span data-ttu-id="5d9ed-131">Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono caricate sei regole.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-131">For this example, an NSG group is built and then loaded with six rules.</span></span> 

>[!TIP]
><span data-ttu-id="5d9ed-132">In genere, è consigliabile creare prima di tutto le regole specifiche di tipo "Consenti" e infine le regole di tipo "Nega" più generiche.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-132">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="5d9ed-133">La priorità assegnata determina quali regole vengono valutate per prime.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-133">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="5d9ed-134">Quando si rileva che al traffico è applicabile una determinata regola, non vengono valutate altre regole.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-134">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="5d9ed-135">Le regole del gruppo di sicurezza di rete possono essere applicate nella direzione in ingresso o in uscita, dal punto di vista della subnet.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-135">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
>
>

<span data-ttu-id="5d9ed-136">A livello dichiarativo, per il traffico in ingresso vengono create le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-136">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="5d9ed-137">Il traffico DNS interno (porta 53) è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-137">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="5d9ed-138">Il traffico RDP (porta 3389) da Internet a qualsiasi macchina virtuale è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-138">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="5d9ed-139">Il traffico HTTP (porta 80) da Internet al server Web (IIS01) è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-139">HTTP traffic (port 80) from the Internet to web server (IIS01) is allowed</span></span>
4. <span data-ttu-id="5d9ed-140">Tutto il traffico (tutte le porte) da IIS01 ad AppVM1 è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-140">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="5d9ed-141">Tutto il traffico (tutte le porte) da Internet all'intera rete virtuale (entrambe le subnet) viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-141">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="5d9ed-142">Tutto il traffico (tutte le porte) dalla subnet front-end alla subnet back-end viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-142">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="5d9ed-143">Con queste regole associate a ogni subnet, se una richiesta HTTP proviene da Internet ed è diretta verso il server Web, le regole 3 (consenti) e 5 (nega) saranno applicabili, ma poiché la regola 3 ha una priorità maggiore, verrà applicata solo tale regola e la regola 5 non verrà presa in considerazione.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-143">With these rules bound to each subnet, if an HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="5d9ed-144">La richiesta HTTP verrà quindi consentita sul server Web.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-144">Thus the HTTP request would be allowed to the web server.</span></span> <span data-ttu-id="5d9ed-145">Se lo stesso traffico prova a raggiungere il server DNS01, la regola 5 (nega) sarà la prima applicabile e il traffico non sarà autorizzato a passare al server.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-145">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="5d9ed-146">La regola 6 (nega) impedisce alla subnet front-end di comunicare con la subnet back-end, ad eccezione del traffico consentito nelle regole 1 e 4; questo set di regole protegge la rete back-end nel caso in cui un utente malintenzionato comprometta l'applicazione Web sul front-end. L'utente malintenzionato avrà infatti accesso limitato alla rete "protetta" back-end, ovvero solo alle risorse esposte nel server AppVM01.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-146">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this rule-set protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="5d9ed-147">Esiste una regola in uscita predefinita che consente il traffico in uscita verso Internet.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-147">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="5d9ed-148">Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-148">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="5d9ed-149">Per applicare criteri di sicurezza al traffico in entrambe le direzioni, è obbligatorio il routing definito dall'utente, descritto nell'"Esempio 3" della [pagina relativa alle procedure consigliate sui limiti di sicurezza][HOME].</span><span class="sxs-lookup"><span data-stu-id="5d9ed-149">To apply security policy to traffic in both directions, User Defined Routing is required and is explored in “Example 3” on the [Security Boundary Best Practices Page][HOME].</span></span>

<span data-ttu-id="5d9ed-150">Ogni regola viene illustrata in dettaglio nel modo seguente:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-150">Each rule is discussed in more detail as follows:</span></span>

1. <span data-ttu-id="5d9ed-151">È necessario creare l'istanza della risorsa gruppo di sicurezza di rete per inserire le regole:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-151">A Network Security Group resource must be instantiated to hold the rules:</span></span>

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

2. <span data-ttu-id="5d9ed-152">La prima regola in questo esempio consente il traffico DNS fra tutte le reti interne al server DNS nella subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-152">The first rule in this example allows DNS traffic between all internal networks to the DNS server on the backend subnet.</span></span> <span data-ttu-id="5d9ed-153">Nella regola sono inclusi alcuni parametri importanti:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-153">The rule has some important parameters:</span></span>
  * <span data-ttu-id="5d9ed-154">Questi tag sono identificatori forniti dal sistema che consentono di gestire in modo semplice una categoria più ampia di prefissi di indirizzi; "destinationAddressPrefix": le regole possono usare un tipo speciale di prefisso denominato "Tag predefinito".</span><span class="sxs-lookup"><span data-stu-id="5d9ed-154">"destinationAddressPrefix" - Rules can use a special type of address prefix called a "Default Tag", these tags are system-provided identifiers that allow an easy way to address a larger category of address prefixes.</span></span> <span data-ttu-id="5d9ed-155">Questa regola usa il tag predefinito "Internet" per indicare qualsiasi indirizzo all'esterno della rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-155">This rule uses the Default Tag “Internet” to signify any address outside of the VNet.</span></span> <span data-ttu-id="5d9ed-156">Altre etichette di prefisso sono VirtualNetwork e AzureLoadBalancer.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-156">Other prefix labels are VirtualNetwork and AzureLoadBalancer.</span></span>
  * <span data-ttu-id="5d9ed-157">"Direction" indica la direzione del flusso di traffico a cui verrà applicata questa regola</span><span class="sxs-lookup"><span data-stu-id="5d9ed-157">“Direction” signifies in which direction of traffic flow this rule takes effect.</span></span> <span data-ttu-id="5d9ed-158">dal punto di vista della subnet o della macchina virtuale, a seconda della posizione a cui è associato il gruppo di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-158">The direction is from the perspective of the subnet or Virtual Machine (depending on where this NSG is bound).</span></span> <span data-ttu-id="5d9ed-159">Se Direction è impostato su "Inbound", la regola verrà applicata al traffico in ingresso nella subnet, ma non al traffico in uscita da essa.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-159">Thus if Direction is “Inbound” and traffic is entering the subnet, the rule would apply and traffic leaving the subnet would not be affected by this rule.</span></span>
  * <span data-ttu-id="5d9ed-160">"Priority" consente di impostare l'ordine in base al quale viene valutato un flusso di traffico.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-160">“Priority” sets the order in which a traffic flow is evaluated.</span></span> <span data-ttu-id="5d9ed-161">Più è basso il numero, maggiore sarà la priorità.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-161">The lower the number the higher the priority.</span></span> <span data-ttu-id="5d9ed-162">Quando un flusso di traffico specifico è applicabile a una determinata regola, non vengono elaborate altre regole.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-162">When a rule applies to a specific traffic flow, no further rules are processed.</span></span> <span data-ttu-id="5d9ed-163">Se quindi una regola con priorità 1 consente il traffico e una regola con priorità 2 lo blocca ed entrambe le regole sono applicabili, il passaggio del traffico viene consentito perché viene applicata la regola 1 con priorità più alta e non vengono considerate altre regole.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-163">Thus if a rule with priority 1 allows traffic, and a rule with priority 2 denies traffic, and both rules apply to traffic then the traffic would be allowed to flow (since rule 1 had a higher priority it took effect and no further rules were applied).</span></span>
  * <span data-ttu-id="5d9ed-164">"Access" indica se il traffico a cui si applica la regola viene bloccato ("Deny") o consentito ("Allow").</span><span class="sxs-lookup"><span data-stu-id="5d9ed-164">“Access” signifies if traffic affected by this rule is blocked ("Deny") or allowed ("Allow").</span></span>

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

3. <span data-ttu-id="5d9ed-165">Questa regola consente il flusso del traffico RDP da Internet alla porta RDP su qualsiasi server sulla subnet associata.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-165">This rule allows RDP traffic to flow from the internet to the RDP port on any server on the bound subnet.</span></span> 

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

4. <span data-ttu-id="5d9ed-166">Questa regola consente al traffico Internet in ingresso di raggiungere il server Web.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-166">This rule allows inbound internet traffic to hit the web server.</span></span> <span data-ttu-id="5d9ed-167">Il comportamento di routing rimane invariato,</span><span class="sxs-lookup"><span data-stu-id="5d9ed-167">This rule does not change the routing behavior.</span></span> <span data-ttu-id="5d9ed-168">ma il traffico destinato a IIS01 può transitare.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-168">The rule only allows traffic destined for IIS01 to pass.</span></span> <span data-ttu-id="5d9ed-169">Se quindi il traffico proveniente da Internet ha come destinazione il server Web, viene consentito e non vengono elaborate altre regole</span><span class="sxs-lookup"><span data-stu-id="5d9ed-169">Thus if traffic from the Internet had the web server as its destination this rule would allow it and stop processing further rules.</span></span> <span data-ttu-id="5d9ed-170">(nella regola con priorità 140 viene bloccato qualsiasi altro tipo di traffico Internet in ingresso).</span><span class="sxs-lookup"><span data-stu-id="5d9ed-170">(In the rule at priority 140 all other inbound internet traffic is blocked).</span></span> <span data-ttu-id="5d9ed-171">Se si elabora soltanto traffico HTTP, questa regola può essere limitata ulteriormente in modo da consentire esclusivamente la porta di destinazione 80.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-171">If you're only processing HTTP traffic, this rule could be further restricted to only allow Destination Port 80.</span></span>

    ```JSON
    {
      "name": "enable_web_rule",
      "properties": {
        "description": "Enable Internet to [variables('VM01Name')]",
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

5. <span data-ttu-id="5d9ed-172">Questa regola consente il passaggio del traffico dal server IIS01 al server AppVM01 e una regola successiva blocca tutto il resto del traffico dal front-end al back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-172">This rule allows traffic to pass from the IIS01 server to the AppVM01 server, a later rule blocks all other Frontend to Backend traffic.</span></span> <span data-ttu-id="5d9ed-173">Per migliorare la regola, è consigliabile aggiungere la porta, se è nota.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-173">To improve this rule, if the port is known that should be added.</span></span> <span data-ttu-id="5d9ed-174">Ad esempio, se il server IIS ha necessità di raggiungere solo SQL Server in AppVM01, l'impostazione dell'intervallo delle porte di destinazione (DestinationPortRange) deve essere modificata da "*" (qualsiasi) a 1433 (porta SQL), in modo da esporre una superficie di attacco più limitata in AppVM01 nel caso l'applicazione Web venisse compromessa.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-174">For example, if the IIS server is hitting only SQL Server on AppVM01, the Destination Port Range should be changed from “*” (Any) to 1433 (the SQL port) thus allowing a smaller inbound attack surface on AppVM01 should the web application ever be compromised.</span></span>

    ```JSON
    {
      "name": "enable_app_rule",
      "properties": {
        "description": "Enable [variables('VM01Name')] to [variables('VM02Name')]",
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

6. <span data-ttu-id="5d9ed-175">Questa regola blocca il traffico da Internet a qualsiasi server della rete.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-175">This rule denies traffic from the internet to any servers on the network.</span></span> <span data-ttu-id="5d9ed-176">Insieme alla regola con priorità 110 e 120, consente esclusivamente il traffico Internet in ingresso diretto al firewall e alle porte RDP sui server e blocca tutto il traffico restante.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-176">With the rules at priority 110 and 120, the effect is to allow only inbound internet traffic to the firewall and RDP ports on servers and blocks everything else.</span></span> <span data-ttu-id="5d9ed-177">Questa regola è di tipo fail-safe per bloccare tutti i flussi imprevisti.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-177">This rule is a "fail-safe" rule to block all unexpected flows.</span></span>

    ```JSON
    {
      "name": "deny_internet_rule",
      "properties": {
        "description": "Isolate the [variables('VNetName')] VNet from the Internet",
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

7. <span data-ttu-id="5d9ed-178">La regola finale blocca il traffico dalla subnet front-end alla subnet back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-178">The final rule denies traffic from the Frontend subnet to the Backend subnet.</span></span> <span data-ttu-id="5d9ed-179">Poiché si tratta di una regola solo di tipo Inbound, il traffico in direzione opposta è consentito (dal back-end al front-end).</span><span class="sxs-lookup"><span data-stu-id="5d9ed-179">Since this rule is an Inbound only rule, reverse traffic is allowed (from the Backend to the Frontend).</span></span>

    ```JSON
    {
      "name": "deny_frontend_rule",
      "properties": {
        "description": "Isolate the [variables('Subnet1Name')] subnet from the [variables('Subnet2Name')] subnet",
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

## <a name="traffic-scenarios"></a><span data-ttu-id="5d9ed-180">Scenari di traffico</span><span class="sxs-lookup"><span data-stu-id="5d9ed-180">Traffic scenarios</span></span>
#### <a name="allowed-internet-to-web-server"></a><span data-ttu-id="5d9ed-181">(*Consentito*) Da Internet al server Web</span><span class="sxs-lookup"><span data-stu-id="5d9ed-181">(*Allowed*) Internet to web server</span></span>
1. <span data-ttu-id="5d9ed-182">Un utente su Internet richiede una pagina HTTP dall'indirizzo IP pubblico della scheda di interfaccia di rete associata alla scheda di interfaccia di rete di IIS01</span><span class="sxs-lookup"><span data-stu-id="5d9ed-182">An internet user requests an HTTP page from the public IP address of the NIC associated with the IIS01 NIC</span></span>
2. <span data-ttu-id="5d9ed-183">L'indirizzo IP pubblico passa il traffico alla rete virtuale verso IIS01 (il server Web)</span><span class="sxs-lookup"><span data-stu-id="5d9ed-183">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="5d9ed-184">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-184">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-185">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-185">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="5d9ed-186">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-186">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="5d9ed-187">Regola gruppo di sicurezza di rete 3 (da Internet a IIS01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-187">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="5d9ed-188">Il traffico raggiunge l'indirizzo IP interno del server Web IIS01 (10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="5d9ed-188">Traffic hits internal IP address of the web server IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="5d9ed-189">IIS01 è in ascolto del traffico Web, riceve la richiesta e ne avvia l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-189">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
6. <span data-ttu-id="5d9ed-190">IIS01 chiede informazioni a SQL Server in AppVM01.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-190">IIS01 asks the SQL Server on AppVM01 for information</span></span>
7. <span data-ttu-id="5d9ed-191">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-191">No outbound rules on Frontend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="5d9ed-192">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-192">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-193">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="5d9ed-194">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="5d9ed-195">Regola gruppo di sicurezza di rete 3 (da Internet a firewall), non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-195">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="5d9ed-196">Regola gruppo di sicurezza di rete 4 (da IIS01 ad AppVM01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-196">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
9. <span data-ttu-id="5d9ed-197">AppVM01 riceve la query SQL e risponde.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-197">AppVM01 receives the SQL Query and responds</span></span>
10. <span data-ttu-id="5d9ed-198">Non essendoci regole in uscita sulla subnet back-end, la risposta è consentita</span><span class="sxs-lookup"><span data-stu-id="5d9ed-198">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
11. <span data-ttu-id="5d9ed-199">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-199">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-200">Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-200">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="5d9ed-201">La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-201">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
12. <span data-ttu-id="5d9ed-202">Il server IIS riceve la risposta SQL, completa la risposta HTTP e la invia al richiedente.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-202">The IIS server receives the SQL response and completes the HTTP response and sends to the requester</span></span>
13. <span data-ttu-id="5d9ed-203">Non essendoci regole in uscita sulla subnet front-end, la risposta è consentita e l'utente su Internet riceve la pagina Web richiesta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-203">Since there are no outbound rules on the Frontend subnet, the response is allowed and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-iis-server"></a><span data-ttu-id="5d9ed-204">(*Consentito*) Traffico RDP al server IIS</span><span class="sxs-lookup"><span data-stu-id="5d9ed-204">(*Allowed*) RDP to IIS server</span></span>
1. <span data-ttu-id="5d9ed-205">L'amministratore del server su Internet richiede una sessione RDP a IIS01 sull'indirizzo IP pubblico della scheda di interfaccia di rete associata alla scheda di interfaccia di rete di IIS01; questo indirizzo IP pubblico è disponibile tramite il portale o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-205">A Server Admin on internet requests an RDP session to IIS01 on the public IP address of the NIC associated with the IIS01 NIC (this public IP address can be found via the Portal or PowerShell)</span></span>
2. <span data-ttu-id="5d9ed-206">L'indirizzo IP pubblico passa il traffico alla rete virtuale verso IIS01 (il server Web)</span><span class="sxs-lookup"><span data-stu-id="5d9ed-206">The Public IP address passes traffic to the VNet towards IIS01 (the web server)</span></span>
3. <span data-ttu-id="5d9ed-207">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-207">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-208">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-208">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="5d9ed-209">Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-209">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="5d9ed-210">Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-210">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="5d9ed-211">La sessione RDP è abilitata.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-211">RDP session is enabled</span></span>
6. <span data-ttu-id="5d9ed-212">IIS01 richiede il nome utente e la password</span><span class="sxs-lookup"><span data-stu-id="5d9ed-212">IIS01 prompts for the user name and password</span></span>

>[!NOTE]
><span data-ttu-id="5d9ed-213">Per eseguire la connessione tramite RDP ai server back-end in questa istanza, il server IIS viene usato come "jumpbox".</span><span class="sxs-lookup"><span data-stu-id="5d9ed-213">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="5d9ed-214">Eseguire prima la connessione tramite RDP al server IIS e, quindi, dal server IIS eseguire la connessione tramite RDP al server back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-214">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="allowed-web-server-dns-look-up-on-dns-server"></a><span data-ttu-id="5d9ed-215">(*Consentito*) Ricerca DNS del server Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="5d9ed-215">(*Allowed*) Web server DNS look-up on DNS server</span></span>
1. <span data-ttu-id="5d9ed-216">Il server Web, IIS01, richiede un feed di dati all'indirizzo www.data.gov, ma deve risolvere l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-216">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="5d9ed-217">La configurazione di rete per la rete virtuale elenca DNS01 (10.0.2.4 nella subnet back-end) come server DNS primario, IIS01 invia la richiesta DNS a DNS01.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-217">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="5d9ed-218">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-218">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="5d9ed-219">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-219">Backend subnet begins inbound rule processing:</span></span>
  * <span data-ttu-id="5d9ed-220">Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-220">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="5d9ed-221">Il server DNS riceve la richiesta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-221">DNS server receives the request</span></span>
6. <span data-ttu-id="5d9ed-222">Il server DNS non ha l'indirizzo memorizzato nella cache e invia la richiesta a un server DNS radice su Internet.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-222">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="5d9ed-223">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-223">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="5d9ed-224">Il server DNS Internet risponde perché la sessione è stata avviata internamente, la risposta è consentita.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-224">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="5d9ed-225">Il server DNS memorizza la risposta nella cache e restituisce a IIS01 la risposta alla richiesta iniziale.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-225">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="5d9ed-226">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-226">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="5d9ed-227">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-227">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-228">Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-228">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="5d9ed-229">La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-229">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="5d9ed-230">IIS01 riceve la risposta da DNS01.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-230">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="5d9ed-231">(*Consentito*) Il server Web richiede l'accesso a un file in AppVM01</span><span class="sxs-lookup"><span data-stu-id="5d9ed-231">(*Allowed*) Web server access file on AppVM01</span></span>
1. <span data-ttu-id="5d9ed-232">IIS01 richiede un file in AppVM01.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-232">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="5d9ed-233">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-233">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="5d9ed-234">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-234">The Backend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-235">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-235">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="5d9ed-236">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-236">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="5d9ed-237">Regola gruppo di sicurezza di rete 3 (da Internet a IIS01) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-237">NSG Rule 3 (Internet to IIS01) doesn’t apply, move to next rule</span></span>
  4. <span data-ttu-id="5d9ed-238">Regola gruppo di sicurezza di rete 4 (da IIS01 ad AppVM01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-238">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="5d9ed-239">AppVM01 riceve la richiesta e risponde con il file (presupponendo che l'accesso sia autorizzato).</span><span class="sxs-lookup"><span data-stu-id="5d9ed-239">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="5d9ed-240">Non essendoci regole in uscita sulla subnet back-end, la risposta è consentita</span><span class="sxs-lookup"><span data-stu-id="5d9ed-240">Since there are no outbound rules on the Backend subnet, the response is allowed</span></span>
6. <span data-ttu-id="5d9ed-241">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-241">Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-242">Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-242">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
  2. <span data-ttu-id="5d9ed-243">La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-243">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="5d9ed-244">Il server IIS riceve il file.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-244">The IIS server receives the file</span></span>

#### <a name="denied-rdp-to-backend"></a><span data-ttu-id="5d9ed-245">(*Negato*) Traffico RDP al back-end</span><span class="sxs-lookup"><span data-stu-id="5d9ed-245">(*Denied*) RDP to backend</span></span>
1. <span data-ttu-id="5d9ed-246">Un utente su Internet tenta di eseguire la connessione tramite RDP al server AppVM01.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-246">An internet user tries to RDP to server AppVM01</span></span>
2. <span data-ttu-id="5d9ed-247">Non essendoci indirizzi IP pubblici associati alla scheda di interfaccia di rete dei server, il traffico non entra nella rete virtuale e non raggiunge il server.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-247">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="5d9ed-248">Se tuttavia per qualunque motivo è stato abilitato un indirizzo IP pubblico, la regola del gruppo di sicurezza di rete 2 (RDP) consentirà questo traffico.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-248">However if a Public IP address was enabled for some reason, NSG rule 2 (RDP) would allow this traffic</span></span>

>[!NOTE]
><span data-ttu-id="5d9ed-249">Per eseguire la connessione tramite RDP ai server back-end in questa istanza, il server IIS viene usato come "jumpbox".</span><span class="sxs-lookup"><span data-stu-id="5d9ed-249">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="5d9ed-250">Eseguire prima la connessione tramite RDP al server IIS e, quindi, dal server IIS eseguire la connessione tramite RDP al server back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-250">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="5d9ed-251">(*Negato*) Traffico Web al server back-end</span><span class="sxs-lookup"><span data-stu-id="5d9ed-251">(*Denied*) Web to backend server</span></span>
1. <span data-ttu-id="5d9ed-252">Un utente su Internet tenta di accedere a un file su AppVM01</span><span class="sxs-lookup"><span data-stu-id="5d9ed-252">An internet user tries to access a file on AppVM01</span></span>
2. <span data-ttu-id="5d9ed-253">Non essendoci indirizzi IP pubblici associati alla scheda di interfaccia di rete dei server, il traffico non entra nella rete virtuale e non raggiunge il server.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-253">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="5d9ed-254">Se per qualunque motivo è stato abilitato un indirizzo IP pubblico, la regola del gruppo di sicurezza di rete 5 (da Internet a rete virtuale) bloccherà questo traffico.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-254">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-look-up-on-dns-server"></a><span data-ttu-id="5d9ed-255">(*Negato*) Ricerca DNS Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="5d9ed-255">(*Denied*) Web DNS look-up on DNS server</span></span>
1. <span data-ttu-id="5d9ed-256">Un utente su Internet tenta di cercare un record DNS interno su DNS01</span><span class="sxs-lookup"><span data-stu-id="5d9ed-256">An internet user tries to look up an internal DNS record on DNS01</span></span>
2. <span data-ttu-id="5d9ed-257">Non essendoci indirizzi IP pubblici associati alla scheda di interfaccia di rete dei server, il traffico non entra nella rete virtuale e non raggiunge il server.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-257">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="5d9ed-258">Se per qualunque motivo è stato abilitato un indirizzo IP pubblico, la regola del gruppo di sicurezza di rete 5 (da Internet a rete virtuale) bloccherà il traffico. Nota: la regola 1 (DNS) potrebbe non essere applicabile perché l'indirizzo di origine della richieste è Internet e la regola 1 si applica solo alla rete locale virtuale come origine.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-258">If a Public IP address was enabled for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply because the requests source address is the internet and Rule 1 only applies to the local VNet as the source)</span></span>

#### <a name="denied-sql-access-on-the-web-server"></a><span data-ttu-id="5d9ed-259">(*Negato*) Accesso SQL nel server Web</span><span class="sxs-lookup"><span data-stu-id="5d9ed-259">(*Denied*) SQL access on the web server</span></span>
1. <span data-ttu-id="5d9ed-260">Un utente su Internet richiede dati SQL da IIS01</span><span class="sxs-lookup"><span data-stu-id="5d9ed-260">An internet user requests SQL data from IIS01</span></span>
2. <span data-ttu-id="5d9ed-261">Non essendoci indirizzi IP pubblici associati alla scheda di interfaccia di rete dei server, il traffico non entra nella rete virtuale e non raggiunge il server.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-261">Since there are no Public IP addresses associated with this servers NIC, this traffic would never enter the VNet and wouldn’t reach the server</span></span>
3. <span data-ttu-id="5d9ed-262">Se per qualunque motivo è stato abilitato un indirizzo IP pubblico, la subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-262">If a Public IP address was enabled for some reason, the Frontend subnet begins inbound rule processing:</span></span>
  1. <span data-ttu-id="5d9ed-263">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-263">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
  2. <span data-ttu-id="5d9ed-264">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-264">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
  3. <span data-ttu-id="5d9ed-265">Regola gruppo di sicurezza di rete 3 (da Internet a IIS01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-265">NSG Rule 3 (Internet to IIS01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="5d9ed-266">Il traffico raggiunge l'indirizzo IP interno di IIS01 (10.0.1.5).</span><span class="sxs-lookup"><span data-stu-id="5d9ed-266">Traffic hits internal IP address of the IIS01 (10.0.1.5)</span></span>
5. <span data-ttu-id="5d9ed-267">IIS01 non è in ascolto sulla porta 1433, pertanto la richiesta non ottiene risposta.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-267">IIS01 isn't listening on port 1433, so no response to the request</span></span>

## <a name="conclusion"></a><span data-ttu-id="5d9ed-268">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="5d9ed-268">Conclusion</span></span>
<span data-ttu-id="5d9ed-269">Questo esempio consente di isolare la subnet back-end dal traffico in ingresso in un modo relativamente semplice e diretto.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-269">This example is a relatively simple and straight forward way of isolating the back-end subnet from inbound traffic.</span></span>

<span data-ttu-id="5d9ed-270">Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].</span><span class="sxs-lookup"><span data-stu-id="5d9ed-270">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="5d9ed-271">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="5d9ed-271">References</span></span>
### <a name="azure-resource-manager-template"></a><span data-ttu-id="5d9ed-272">Modello di Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5d9ed-272">Azure Resource Manager template</span></span>
<span data-ttu-id="5d9ed-273">Questo esempio usa un modello di Azure Resource Manager predefinito in un repository GitHub gestito da Microsoft e lo rende disponibile alla community.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-273">This example uses a predefined Azure Resource Manager template in a GitHub repository maintained by Microsoft and open to the community.</span></span> <span data-ttu-id="5d9ed-274">Il modello può essere distribuito immediatamente da GitHub o scaricato e modificato in base alle specifiche esigenze.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-274">This template can be deployed straight out of GitHub, or downloaded and modified to fit your needs.</span></span> 

<span data-ttu-id="5d9ed-275">Il modello principale è presente nel file denominato "azuredeploy.json".</span><span class="sxs-lookup"><span data-stu-id="5d9ed-275">The main template is in the file named "azuredeploy.json."</span></span> <span data-ttu-id="5d9ed-276">Questo modello può essere inviato tramite PowerShell o l'interfaccia della riga di comando (con il file "azuredeploy.parameters.json associato") per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-276">This template can be submitted via PowerShell or CLI (with the associated "azuredeploy.parameters.json" file) to deploy this template.</span></span> <span data-ttu-id="5d9ed-277">Il modo più semplice è usare il pulsante "Deploy to Azure" nella pagina README.md in GitHub.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-277">I find the easiest way is to use the "Deploy to Azure" button on the README.md page at GitHub.</span></span>

<span data-ttu-id="5d9ed-278">Per distribuire il modello che usa questo esempio da GitHub e il portale di Azure, seguire questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="5d9ed-278">To deploy the template that builds this example from GitHub and the Azure portal, follow these steps:</span></span>

1. <span data-ttu-id="5d9ed-279">Da un browser passare a [Template][Template]</span><span class="sxs-lookup"><span data-stu-id="5d9ed-279">From a browser, navigate to the [Template][Template]</span></span>
2. <span data-ttu-id="5d9ed-280">Fare clic sul pulsante "Deploy to Azure" oppure su "View" per visualizzare una rappresentazione grafica del modello.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-280">Click the "Deploy to Azure" button (or the "Visualize" button to see a graphical representation of this template)</span></span>
3. <span data-ttu-id="5d9ed-281">Immettere l'account di archiviazione, il nome utente e la password nel pannello dei parametri, quindi fare clic su **OK**</span><span class="sxs-lookup"><span data-stu-id="5d9ed-281">Enter the Storage Account, User Name, and Password in the Parameters blade, then click **OK**</span></span>
5. <span data-ttu-id="5d9ed-282">Creare un gruppo di risorse per questa distribuzione. È possibile usarne uno esistente, ma è consigliabile creare una nuova istanza per risultati ottimali.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-282">Create a Resource Group for this deployment (You can use an existing one, but I recommend a new one for best results)</span></span>
6. <span data-ttu-id="5d9ed-283">Se necessario, modificare le impostazioni relative a Sottoscrizione e Località per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-283">If necessary, change the Subscription and Location settings for your VNet.</span></span>
7. <span data-ttu-id="5d9ed-284">Fare clic su **Rivedere le note legali**, leggere le condizioni e fare clic su **Acquista** per accettare.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-284">Click **Review legal terms**, read the terms, and click **Purchase** to agree.</span></span>
8. <span data-ttu-id="5d9ed-285">Fare clic su **Crea** per iniziare la distribuzione di questo modello.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-285">Click **Create** to begin the deployment of this template.</span></span>
9. <span data-ttu-id="5d9ed-286">Dopo il corretto completamento della distribuzione, passare al gruppo di risorse creato per questa distribuzione per esaminare le risorse configurate in esso.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-286">Once the deployment finishes successfully, navigate to the Resource Group created for this deployment to see the resources configured inside.</span></span>

>[!NOTE]
><span data-ttu-id="5d9ed-287">Questo modello consente di eseguire la connessione tramite RDP solo al server IIS01; l'indirizzo IP pubblico per IIS01 è reperibile nel portale.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-287">This template enables RDP to the IIS01 server only (find the Public IP for IIS01 on the Portal).</span></span> <span data-ttu-id="5d9ed-288">Per eseguire la connessione tramite RDP ai server back-end in questa istanza, il server IIS viene usato come "jumpbox".</span><span class="sxs-lookup"><span data-stu-id="5d9ed-288">To RDP to any back-end servers in this instance, the IIS server is used as a "jump box."</span></span> <span data-ttu-id="5d9ed-289">Eseguire prima la connessione tramite RDP al server IIS e, quindi, dal server IIS eseguire la connessione tramite RDP al server back-end.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-289">First RDP to the IIS server and then from the IIS Server RDP to the back-end server.</span></span>
>
>

<span data-ttu-id="5d9ed-290">Per rimuovere questa distribuzione, eliminare il gruppo di risorse; verranno eliminate anche tutte le risorse figlio.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-290">To remove this deployment, delete the Resource Group and all child resources will also be deleted.</span></span>

#### <a name="sample-application-scripts"></a><span data-ttu-id="5d9ed-291">Script di applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5d9ed-291">Sample application scripts</span></span>
<span data-ttu-id="5d9ed-292">Dopo la corretta esecuzione del modello è possibile configurare il server Web e il server applicazioni con un'applicazione Web di esempio per consentire l'esecuzione di test con questa configurazione della rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="5d9ed-292">Once the template runs successfully, you can set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span> <span data-ttu-id="5d9ed-293">Per installare un'applicazione di esempio per questo e altri esempi di rete perimetrale, è possibile trovarne una in [Script di applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="5d9ed-293">To install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d9ed-294">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5d9ed-294">Next steps</span></span>

* <span data-ttu-id="5d9ed-295">Distribuire questo esempio</span><span class="sxs-lookup"><span data-stu-id="5d9ed-295">Deploy this example</span></span>
* <span data-ttu-id="5d9ed-296">Compilare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="5d9ed-296">Build the sample application</span></span>
* <span data-ttu-id="5d9ed-297">Testare diversi flussi di traffico attraverso la rete perimetrale</span><span class="sxs-lookup"><span data-stu-id="5d9ed-297">Test different traffic flows through this DMZ</span></span>

<!--Image References-->
<span data-ttu-id="5d9ed-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"</span><span class="sxs-lookup"><span data-stu-id="5d9ed-298">[1]: ./media/virtual-networks-dmz-nsg-arm/example1design.png "Inbound DMZ with NSG"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[Template]: https://github.com/Azure/azure-quickstart-templates/tree/master/301-dmz-nsg
[SampleApp]: ./virtual-networks-sample-app.md