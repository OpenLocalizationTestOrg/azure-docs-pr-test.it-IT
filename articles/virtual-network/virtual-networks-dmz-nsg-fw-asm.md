---
title: 'Esempio di rete perimetrale: Creare una rete perimetrale per proteggere le applicazioni con un firewall e gruppi di sicurezza di rete | Documentazione Microsoft'
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
ms.openlocfilehash: cc0e8a3fa749eb2e6f65ef92c2d3cb404cfc8bc0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="example-2--build-a-dmz-to-protect-applications-with-a-firewall-and-nsgs"></a><span data-ttu-id="496b4-103">Esempio 2: Creare una rete perimetrale per proteggere le applicazioni con un firewall e gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="496b4-103">Example 2 – Build a DMZ to protect applications with a Firewall and NSGs</span></span>
<span data-ttu-id="496b4-104">[Tornare alla pagina relativa alle procedure consigliate sui limiti di sicurezza][HOME]</span><span class="sxs-lookup"><span data-stu-id="496b4-104">[Return to the Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="496b4-105">Questo esempio illustra come creare una rete perimetrale con un firewall, quattro server Windows e gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="496b4-105">This example will create a DMZ with a firewall, four windows servers, and Network Security Groups.</span></span> <span data-ttu-id="496b4-106">Illustra in dettaglio anche ogni comando rilevante per favorire una comprensione più approfondita di ogni passaggio.</span><span class="sxs-lookup"><span data-stu-id="496b4-106">It will also walk through each of the relevant commands to provide a deeper understanding of each step.</span></span> <span data-ttu-id="496b4-107">È disponibile anche una sezione sugli scenari di traffico con istruzioni dettagliate sul percorso seguito dal traffico attraverso i livelli di difesa della rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="496b4-107">There is also a Traffic Scenario section to provide an in-depth step-by-step how traffic proceeds through the layers of defense in the DMZ.</span></span> <span data-ttu-id="496b4-108">La sezione Riferimenti, infine, include tutto il codice e istruzioni complete per creare l'ambiente per testare e sperimentare vari scenari.</span><span class="sxs-lookup"><span data-stu-id="496b4-108">Finally, in the references section is the complete code and instruction to build this environment to test and experiment with various scenarios.</span></span> 

<span data-ttu-id="496b4-109">![Rete Perimetrale in ingresso con NVA e gruppo][1]</span><span class="sxs-lookup"><span data-stu-id="496b4-109">![Inbound DMZ with NVA and NSG][1]</span></span>

## <a name="environment-description"></a><span data-ttu-id="496b4-110">Descrizione dell'ambiente</span><span class="sxs-lookup"><span data-stu-id="496b4-110">Environment Description</span></span>
<span data-ttu-id="496b4-111">In questo esempio è presente una sottoscrizione che include gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="496b4-111">In this example there is a subscription that contains the following:</span></span>

* <span data-ttu-id="496b4-112">Due servizi cloud, "FrontEnd001" e "BackEnd001"</span><span class="sxs-lookup"><span data-stu-id="496b4-112">Two cloud services: “FrontEnd001” and “BackEnd001”</span></span>
* <span data-ttu-id="496b4-113">Una rete virtuale, "CorpNetwork", con due subnet: "FrontEnd" e "BackEnd"</span><span class="sxs-lookup"><span data-stu-id="496b4-113">A Virtual Network “CorpNetwork”, with two subnets: “FrontEnd” and “BackEnd”</span></span>
* <span data-ttu-id="496b4-114">Un singolo gruppo di sicurezza di rete applicato a entrambe le subnet.</span><span class="sxs-lookup"><span data-stu-id="496b4-114">A single Network Security Group that is applied to both subnets</span></span>
* <span data-ttu-id="496b4-115">Un dispositivo virtuale di rete, in questo esempio Barracuda NextGen Firewall, connesso alla subnet FrontEnd</span><span class="sxs-lookup"><span data-stu-id="496b4-115">A network virtual appliance, in this example a Barracuda NextGen Firewall, connected to the Frontend subnet</span></span>
* <span data-ttu-id="496b4-116">Un server Windows che rappresenta un server Web applicazioni ("IIS01").</span><span class="sxs-lookup"><span data-stu-id="496b4-116">A Windows Server that represents an application web server (“IIS01”)</span></span>
* <span data-ttu-id="496b4-117">Due server Windows che rappresentano server back-end applicazioni ("AppVM01", "AppVM02")</span><span class="sxs-lookup"><span data-stu-id="496b4-117">Two windows servers that represent application back end servers (“AppVM01”, “AppVM02”)</span></span>
* <span data-ttu-id="496b4-118">Un server Windows che rappresenta un server DNS ("DNS01").</span><span class="sxs-lookup"><span data-stu-id="496b4-118">A Windows server that represents a DNS server (“DNS01”)</span></span>

> [!NOTE]
> <span data-ttu-id="496b4-119">Anche se in questo esempio si usa Barracuda NextGen Firewall, possono essere usati molti altri dispositivi virtuali di rete.</span><span class="sxs-lookup"><span data-stu-id="496b4-119">Although this example uses a Barracuda NextGen Firewall, many of the different Network Virtual Appliances could be used for this example.</span></span>
> 
> 

<span data-ttu-id="496b4-120">Nella sezione Riferimenti alla fine dell'articolo è disponibile uno script di PowerShell per creare la maggior parte dell'ambiente descritto sopra.</span><span class="sxs-lookup"><span data-stu-id="496b4-120">In the references section below there is a PowerShell script that will build most of the environment described above.</span></span> <span data-ttu-id="496b4-121">La creazione di macchine virtuali e reti virtuali, anche se eseguita dallo script di esempio, non è descritta in dettaglio in questo documento.</span><span class="sxs-lookup"><span data-stu-id="496b4-121">Building the VMs and Virtual Networks, although are done by the example script, are not described in detail in this document.</span></span>

<span data-ttu-id="496b4-122">Per creare l'ambiente, eseguire queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="496b4-122">To build the environment:</span></span>

1. <span data-ttu-id="496b4-123">Salvare il file XML di configurazione di rete incluso nella sezione Riferimenti, aggiornandolo con i nomi, il percorso e gli indirizzi IP corrispondenti allo scenario specifico.</span><span class="sxs-lookup"><span data-stu-id="496b4-123">Save the network config xml file included in the references section (updated with names, location, and IP addresses to match the given scenario)</span></span>
2. <span data-ttu-id="496b4-124">Aggiornare le variabili utente incluse nello script in modo che corrispondano all'ambiente in cui lo script verrà eseguito, ad esempio sottoscrizioni, nomi dei servizi e così via.</span><span class="sxs-lookup"><span data-stu-id="496b4-124">Update the user variables in the script to match the environment the script is to be run against (subscriptions, service names, etc)</span></span>
3. <span data-ttu-id="496b4-125">Eseguire lo script in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="496b4-125">Execute the script in PowerShell</span></span>

<span data-ttu-id="496b4-126">**Nota**: l'area indicata nello script di PowerShell deve corrispondere all'area indicata nel file XML di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="496b4-126">**Note**: The region signified in the PowerShell script must match the region signified in the network configuration xml file.</span></span>

<span data-ttu-id="496b4-127">Dopo l'esecuzione corretta dello script, si potranno eseguire i passaggi successivi allo script seguenti:</span><span class="sxs-lookup"><span data-stu-id="496b4-127">Once the script runs successfully the following post-script steps may be taken:</span></span>

1. <span data-ttu-id="496b4-128">Configurare le regole del firewall illustrate nella sezione seguente intitolata Regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-128">Set up the firewall rules, this is covered in the section below titled: Firewall Rules.</span></span>
2. <span data-ttu-id="496b4-129">Facoltativamente, nella sezione Riferimenti sono disponibili due script per configurare il server Web e il server applicazioni per consentire l'esecuzione dei test con questa configurazione della rete perimetrale.</span><span class="sxs-lookup"><span data-stu-id="496b4-129">Optionally in the references section are two scripts to set up the web server and app server with a simple web application to allow testing with this DMZ configuration.</span></span>

<span data-ttu-id="496b4-130">La sezione successiva descrive la maggior parte delle istruzioni dello script relativamente ai gruppi di sicurezza di rete.</span><span class="sxs-lookup"><span data-stu-id="496b4-130">The next section explains most of the scripts statements relative to Network Security Groups.</span></span>

## <a name="network-security-groups-nsg"></a><span data-ttu-id="496b4-131">Gruppi di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="496b4-131">Network Security Groups (NSG)</span></span>
<span data-ttu-id="496b4-132">Per questo esempio viene creato un gruppo di sicurezza di rete, in cui vengono poi caricate sei regole.</span><span class="sxs-lookup"><span data-stu-id="496b4-132">For this example, a NSG group is built and then loaded with six rules.</span></span> 

> [!TIP]
> <span data-ttu-id="496b4-133">In genere, è consigliabile creare prima di tutto le regole specifiche di tipo "Consenti" e infine le regole di tipo "Nega" più generiche.</span><span class="sxs-lookup"><span data-stu-id="496b4-133">Generally speaking, you should create your specific “Allow” rules first and then the more generic “Deny” rules last.</span></span> <span data-ttu-id="496b4-134">La priorità assegnata determina quali regole vengono valutate per prime.</span><span class="sxs-lookup"><span data-stu-id="496b4-134">The assigned priority dictates which rules are evaluated first.</span></span> <span data-ttu-id="496b4-135">Quando si rileva che al traffico è applicabile una determinata regola, non vengono valutate altre regole.</span><span class="sxs-lookup"><span data-stu-id="496b4-135">Once traffic is found to apply to a specific rule, no further rules are evaluated.</span></span> <span data-ttu-id="496b4-136">Le regole del gruppo di sicurezza di rete possono essere applicate nella direzione in ingresso o in uscita, dal punto di vista della subnet.</span><span class="sxs-lookup"><span data-stu-id="496b4-136">NSG rules can apply in either in the inbound or outbound direction (from the perspective of the subnet).</span></span>
> 
> 

<span data-ttu-id="496b4-137">A livello dichiarativo, per il traffico in ingresso vengono create le righe seguenti:</span><span class="sxs-lookup"><span data-stu-id="496b4-137">Declaratively, the following rules are being built for inbound traffic:</span></span>

1. <span data-ttu-id="496b4-138">Il traffico DNS interno (porta 53) è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-138">Internal DNS traffic (port 53) is allowed</span></span>
2. <span data-ttu-id="496b4-139">Il traffico RDP (porta 3389) da Internet a qualsiasi VM è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-139">RDP traffic (port 3389) from the Internet to any VM is allowed</span></span>
3. <span data-ttu-id="496b4-140">Il traffico HTTP (porta 80) da Internet al dispositivo virtuale di rete (firewall) è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-140">HTTP traffic (port 80) from the Internet to the NVA (firewall) is allowed</span></span>
4. <span data-ttu-id="496b4-141">Tutto il traffico (tutte le porte) da IIS01 ad AppVM1 è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-141">Any traffic (all ports) from IIS01 to AppVM1 is allowed</span></span>
5. <span data-ttu-id="496b4-142">Tutto il traffico (tutte le porte) da Internet all'intera rete virtuale (entrambe le subnet) viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="496b4-142">Any traffic (all ports) from the Internet to the entire VNet (both subnets) is Denied</span></span>
6. <span data-ttu-id="496b4-143">Tutto il traffico (tutte le porte) dalla subnet front-end alla subnet back-end viene bloccato.</span><span class="sxs-lookup"><span data-stu-id="496b4-143">Any traffic (all ports) from the Frontend subnet to the Backend subnet is Denied</span></span>

<span data-ttu-id="496b4-144">Con queste regole associate a ogni subnet, se una richiesta HTTP proviene da Internet verso il server Web, le regole 3 (consenti) e 5 (nega) saranno applicabili, ma poiché la regola 3 ha una priorità maggiore, verrà applicata solo tale regola e la regola 5 non verrà presa in considerazione.</span><span class="sxs-lookup"><span data-stu-id="496b4-144">With these rules bound to each subnet, if a HTTP request was inbound from the Internet to the web server, both rules 3 (allow) and 5 (deny) would apply, but since rule 3 has a higher priority only it would apply and rule 5 would not come into play.</span></span> <span data-ttu-id="496b4-145">La richiesta HTTP verrà quindi consentita sul firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-145">Thus the HTTP request would be allowed to the firewall.</span></span> <span data-ttu-id="496b4-146">Se lo stesso traffico prova a raggiungere il server DNS01, la regola 5 (nega) sarà la prima applicabile e il traffico non sarà autorizzato a passare al server.</span><span class="sxs-lookup"><span data-stu-id="496b4-146">If that same traffic was trying to reach the DNS01 server, rule 5 (Deny) would be the first to apply and the traffic would not be allowed to pass to the server.</span></span> <span data-ttu-id="496b4-147">La regola 6 (nega) impedisce alla subnet front-end di comunicare con la subnet back-end (ad eccezione del traffico consentito nelle regole 1 e 4), proteggendo la rete back-end nel caso in cui un utente malintenzionato comprometta l'applicazione Web sul front-end. L'utente malintenzionato avrà infatti accesso limitato alla rete "protetta" back-end, ovvero solo alle risorse esposte nel server AppVM01.</span><span class="sxs-lookup"><span data-stu-id="496b4-147">Rule 6 (Deny) blocks the Frontend subnet from talking to the Backend subnet (except for allowed traffic in rules 1 and 4), this protects the Backend network in case an attacker compromises the web application on the Frontend, the attacker would have limited access to the Backend “protected” network (only to resources exposed on the AppVM01 server).</span></span>

<span data-ttu-id="496b4-148">Esiste una regola in uscita predefinita che consente il traffico in uscita verso Internet.</span><span class="sxs-lookup"><span data-stu-id="496b4-148">There is a default outbound rule that allows traffic out to the internet.</span></span> <span data-ttu-id="496b4-149">Per questo esempio si consente il traffico in uscita e non si modificano le regole in uscita.</span><span class="sxs-lookup"><span data-stu-id="496b4-149">For this example, we’re allowing outbound traffic and not modifying any outbound rules.</span></span> <span data-ttu-id="496b4-150">Per bloccare il traffico in entrambe le direzioni, è richiesto il routing definito dall'utente. Questo aspetto viene esaminato in un esempio diverso, disponibile nel [documento sui principali limiti della sicurezza][HOME].</span><span class="sxs-lookup"><span data-stu-id="496b4-150">To lock down traffic in both directions, User Defined Routing is required, this is explored in a different example that can found in the [main security boundary document][HOME].</span></span>

<span data-ttu-id="496b4-151">Le regole per i gruppi di sicurezza di rete illustrate sopra sono molto simili a quelle descritte nell'[Esempio 1: Creare una semplice rete perimetrale con gruppi di sicurezza di rete][Example1].</span><span class="sxs-lookup"><span data-stu-id="496b4-151">The above discussed NSG rules are very similar to the NSG rules in [Example 1 - Build a Simple DMZ with NSGs][Example1].</span></span> <span data-ttu-id="496b4-152">Vedere anche la descrizione relativa ai gruppi di sicurezza di rete in quel documento per un'analisi dettagliata della regola sui gruppi di sicurezza di rete e i relativi attributi.</span><span class="sxs-lookup"><span data-stu-id="496b4-152">Please review the NSG Description in that document for a detailed look at each NSG rule and it's attributes.</span></span>

## <a name="firewall-rules"></a><span data-ttu-id="496b4-153">Regole del firewall</span><span class="sxs-lookup"><span data-stu-id="496b4-153">Firewall Rules</span></span>
<span data-ttu-id="496b4-154">È necessario installare un client di gestione in un PC per controllare il firewall e creare le configurazioni necessarie.</span><span class="sxs-lookup"><span data-stu-id="496b4-154">A management client will need to be installed on a PC to manage the firewall and create the configurations needed.</span></span> <span data-ttu-id="496b4-155">Per informazioni sulla gestione del dispositivo, vedere la documentazione del fornitore del firewall o di un altro dispositivo virtuale di rete.</span><span class="sxs-lookup"><span data-stu-id="496b4-155">See the documentation from your firewall (or other NVA) vendor on how to manage the device.</span></span> <span data-ttu-id="496b4-156">Il resto di questa sezione descrive la configurazione del firewall stesso tramite il client di gestione dei fornitori, non del portale di Azure o di PowerShell.</span><span class="sxs-lookup"><span data-stu-id="496b4-156">The remainder of this section will describe the configuration of the firewall itself, through the vendors management client (i.e. not the Azure portal or PowerShell).</span></span>

<span data-ttu-id="496b4-157">Le istruzioni per scaricare il client e connettersi all'applicazione Barracuda usata in questo esempio sono disponibili qui: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span><span class="sxs-lookup"><span data-stu-id="496b4-157">Instructions for client download and connecting to the Barracuda used in this example can be found here: [Barracuda NG Admin](https://techlib.barracuda.com/NG61/NGAdmin)</span></span>

<span data-ttu-id="496b4-158">Sul firewall sarà necessario creare regole di inoltro.</span><span class="sxs-lookup"><span data-stu-id="496b4-158">On the firewall, forwarding rules will need to be created.</span></span> <span data-ttu-id="496b4-159">Poiché questo esempio indirizza solo il traffico Internet in ingresso verso il firewall e quindi verso il server Web, sarà necessaria solo una regola del processo NAT di inoltro.</span><span class="sxs-lookup"><span data-stu-id="496b4-159">Since this example only routes internet traffic in-bound to the firewall and then to the web server, only one forwarding NAT rule is needed.</span></span> <span data-ttu-id="496b4-160">Nel dispositivo Barracuda NextGen Firewall usato in questo esempio, per passare il traffico viene usata una regola Destination NAT ("Dst NAT").</span><span class="sxs-lookup"><span data-stu-id="496b4-160">On the Barracuda NextGen Firewall used in this example the rule would be a Destination NAT rule (“Dst NAT”) to pass this traffic.</span></span>

<span data-ttu-id="496b4-161">Per creare la regola seguente, o verificare le regole predefinite esistenti, dal dashboard del client Barracuda NG Admin passare alla scheda di configurazione, quindi nella sezione Operational Configuration fare clic su Ruleset.</span><span class="sxs-lookup"><span data-stu-id="496b4-161">To create the following rule (or verify existing default rules), starting from the Barracuda NG Admin client dashboard, navigate to the configuration tab, in the Operational Configuration section click Ruleset.</span></span> <span data-ttu-id="496b4-162">Una griglia denominata "Main Rules" mostrerà le regole esistenti attive e disattivate nel firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-162">A grid called, “Main Rules” will show the existing active and deactivated rules on the firewall.</span></span> <span data-ttu-id="496b4-163">Nell'angolo in alto a destra della griglia è presente un piccolo pulsante verde "+" sul quale occorre fare clic per creare una nuova regola. Notare che il firewall potrebbe essere "bloccato" per modifiche. Se è visualizzato un pulsante contrassegnato con "Lock" e non si riescono a creare o modificare regole, fare clic sul pulsante per "sbloccare" il set di regole e consentire la modifica.</span><span class="sxs-lookup"><span data-stu-id="496b4-163">In the upper right corner of this grid is a small, green “+” button, click this to create a new rule (Note: your firewall may be “locked” for changes, if you see a button marked “Lock” and you are unable to create or edit rules, click this button to “unlock” the ruleset and allow editing).</span></span> <span data-ttu-id="496b4-164">Se si vuole modificare una regola esistente, selezionarla, fare clic con il pulsante destro del mouse e scegliere Edit Rule.</span><span class="sxs-lookup"><span data-stu-id="496b4-164">If you wish to edit an existing rule, select that rule, right-click and select Edit Rule.</span></span>

<span data-ttu-id="496b4-165">Creare una nuova regola e specificare un nome, ad esempio "WebTraffic".</span><span class="sxs-lookup"><span data-stu-id="496b4-165">Create a new rule and provide a name, such as "WebTraffic".</span></span> 

<span data-ttu-id="496b4-166">Icona regola NAT di destinazione è simile al seguente: ![icona NAT di destinazione][2]</span><span class="sxs-lookup"><span data-stu-id="496b4-166">The Destination NAT rule icon looks like this: ![Destination NAT Icon][2]</span></span>

<span data-ttu-id="496b4-167">La regola stessa dovrebbe essere simile alla schermata seguente:</span><span class="sxs-lookup"><span data-stu-id="496b4-167">The rule itself would look something like this:</span></span>

<span data-ttu-id="496b4-168">![Regola del firewall][3]</span><span class="sxs-lookup"><span data-stu-id="496b4-168">![Firewall Rule][3]</span></span>

<span data-ttu-id="496b4-169">In questo caso, qualsiasi indirizzo di origine in ingresso che accede al firewall nel tentativo di raggiungere HTTP (porta 80 o 443 per HTTPS) verrà trasmesso all'interfaccia "DHCP1 Local IP" del firewall e reindirizzato al server Web con l'indirizzo IP 10.0.1.5.</span><span class="sxs-lookup"><span data-stu-id="496b4-169">Here any inbound address that hits the Firewall trying to reach HTTP (port 80 or 443 for HTTPS) will be sent out the Firewall’s “DHCP1 Local IP” interface and redirected to the Web Server with the IP Address of 10.0.1.5.</span></span> <span data-ttu-id="496b4-170">Poiché il traffico arriva sulla porta 80 e viene inoltrato al server Web sulla porta 80, non sono necessarie modifiche della porta.</span><span class="sxs-lookup"><span data-stu-id="496b4-170">Since the traffic is coming in on port 80 and going to the web server on port 80 no port change was needed.</span></span> <span data-ttu-id="496b4-171">Il campo Target List poteva tuttavia essere 10.0.1.5:8080 se il server Web fosse stato in ascolto sulla porta 8080, convertendo così la porta in ingresso 80 sul firewall nella porta in ingresso 8080 sul server Web.</span><span class="sxs-lookup"><span data-stu-id="496b4-171">However, the Target List could have been 10.0.1.5:8080 if our Web Server listened on port 8080 thus translating the inbound port 80 on the firewall to inbound port 8080 on the web server.</span></span>

<span data-ttu-id="496b4-172">È necessario definire un valore in Connection Method. Come regola di destinazione da Internet la più appropriata è "Dynamic SNAT".</span><span class="sxs-lookup"><span data-stu-id="496b4-172">A Connection Method should also be signified, for the Destination Rule from the Internet, "Dynamic SNAT" is most appropriate.</span></span> 

<span data-ttu-id="496b4-173">Anche se è stata creata una sola regola, è importante impostarne la priorità correttamente.</span><span class="sxs-lookup"><span data-stu-id="496b4-173">Although only one rule has been created it's important that its priority is set correctly.</span></span> <span data-ttu-id="496b4-174">Se nella griglia di tutte le regole sul firewall questa nuova regola si trova in basso, sotto la regola "BLOCKALL", non verrà mai applicata.</span><span class="sxs-lookup"><span data-stu-id="496b4-174">If in the grid of all rules on the firewall this new rule is on the bottom (below the "BLOCKALL" rule) it will never come into play.</span></span> <span data-ttu-id="496b4-175">Assicurarsi che la regola appena creata per il traffico Web si trovi sopra la regola BLOCKALL.</span><span class="sxs-lookup"><span data-stu-id="496b4-175">Ensure the newly created rule for web traffic is above the BLOCKALL rule.</span></span>

<span data-ttu-id="496b4-176">Una volta che la regola è stata creata, è necessario effettuarne il push al firewall e quindi attivarla. In caso contrario, la modifica della regola non sarà applicata.</span><span class="sxs-lookup"><span data-stu-id="496b4-176">Once the rule is created, it must be pushed to the firewall and then activated, if this is not done the rule change will not take effect.</span></span> <span data-ttu-id="496b4-177">Il processo di push e attivazione è descritto nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-177">The push and activation process is described in the next section.</span></span>

## <a name="rule-activation"></a><span data-ttu-id="496b4-178">Attivazione delle regole</span><span class="sxs-lookup"><span data-stu-id="496b4-178">Rule Activation</span></span>
<span data-ttu-id="496b4-179">Dopo aver modificato il set di regole per aggiungervi questa regola, è necessario caricarlo nel firewall e attivarlo.</span><span class="sxs-lookup"><span data-stu-id="496b4-179">With the ruleset modified to add this rule, the ruleset must be uploaded to the firewall and activated.</span></span>

<span data-ttu-id="496b4-180">![Attivazione delle regole firewall][4]</span><span class="sxs-lookup"><span data-stu-id="496b4-180">![Firewall Rule Activation][4]</span></span>

<span data-ttu-id="496b4-181">Nell'angolo in alto a destra del client di gestione è disponibile un gruppo di pulsanti.</span><span class="sxs-lookup"><span data-stu-id="496b4-181">In the upper right hand corner of the management client are a cluster of buttons.</span></span> <span data-ttu-id="496b4-182">Fare clic sul pulsante "Send Changes" per inviare le regole modificate al firewall, quindi fare clic sul pulsante "Activate".</span><span class="sxs-lookup"><span data-stu-id="496b4-182">Click the “Send Changes” button to send the modified rules to the firewall, then click the “Activate” button.</span></span>

<span data-ttu-id="496b4-183">Con l'attivazione del set di regole del firewall, la compilazione dell'ambiente di esempio è completata.</span><span class="sxs-lookup"><span data-stu-id="496b4-183">With the activation of the firewall ruleset this example environment build is complete.</span></span> <span data-ttu-id="496b4-184">Facoltativamente, è possibile eseguire gli script successivi alla compilazione disponibili nella sezione Riferimenti per aggiungere un'applicazione a questo ambiente e testare gli scenari di traffico seguenti.</span><span class="sxs-lookup"><span data-stu-id="496b4-184">Optionally, the post build scripts in the References section can be run to add an application to this environment to test the below traffic scenarios.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="496b4-185">È importante comprendere che non si raggiungerà il server Web direttamente.</span><span class="sxs-lookup"><span data-stu-id="496b4-185">It is critical to realize that you will not hit the web server directly.</span></span> <span data-ttu-id="496b4-186">Quando un browser richiede una pagina HTTP da FrontEnd001.CloudApp.Net, l'endpoint HTTP (porta 80) passa questo traffico al firewall, non al server Web.</span><span class="sxs-lookup"><span data-stu-id="496b4-186">When a browser requests an HTTP page from FrontEnd001.CloudApp.Net, the HTTP endpoint (port 80) passes this traffic to the firewall not the web server.</span></span> <span data-ttu-id="496b4-187">Il firewall inoltra quindi la richiesta tramite NAT al server Web, in base alla regola creata sopra.</span><span class="sxs-lookup"><span data-stu-id="496b4-187">The firewall then, according to the rule created above, NATs that request to the Web Server.</span></span>
> 
> 

## <a name="traffic-scenarios"></a><span data-ttu-id="496b4-188">Scenari di traffico</span><span class="sxs-lookup"><span data-stu-id="496b4-188">Traffic Scenarios</span></span>
#### <a name="allowed-web-to-web-server-through-firewall"></a><span data-ttu-id="496b4-189">(Consentito) Da Web a server Web tramite il firewall</span><span class="sxs-lookup"><span data-stu-id="496b4-189">(Allowed) Web to Web Server through Firewall</span></span>
1. <span data-ttu-id="496b4-190">L'utente Internet richiede una pagina HTTP a FrontEnd001.CloudApp.Net (servizio cloud per Internet).</span><span class="sxs-lookup"><span data-stu-id="496b4-190">Internet user requests HTTP page from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="496b4-191">Il servizio cloud passa il traffico attraverso l'endpoint aperto sulla porta 80 all'interfaccia locale del firewall su 10.0.1.4:80.</span><span class="sxs-lookup"><span data-stu-id="496b4-191">Cloud service passes traffic through open endpoint on port 80 to firewall local interface on 10.0.1.4:80</span></span>
3. <span data-ttu-id="496b4-192">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-192">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-193">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-193">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="496b4-194">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-194">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="496b4-195">Regola gruppo di sicurezza di rete 3 (da Internet a firewall) applicabile, il traffico è consentito, l'elaborazione della regola si arresta.</span><span class="sxs-lookup"><span data-stu-id="496b4-195">NSG Rule 3 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="496b4-196">Il traffico raggiunge l'indirizzo IP interno del firewall (10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="496b4-196">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="496b4-197">La regola di inoltro al firewall riconosce il traffico per la porta 80 e lo reindirizza al server Web IIS01.</span><span class="sxs-lookup"><span data-stu-id="496b4-197">Firewall forwarding rule see this is port 80 traffic, redirects it to the web server IIS01</span></span>
6. <span data-ttu-id="496b4-198">IIS01 è in ascolto del traffico Web, riceve la richiesta e ne avvia l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="496b4-198">IIS01 is listening for web traffic, receives this request and starts processing the request</span></span>
7. <span data-ttu-id="496b4-199">IIS01 chiede informazioni a SQL Server in AppVM01.</span><span class="sxs-lookup"><span data-stu-id="496b4-199">IIS01 asks the SQL Server on AppVM01 for information</span></span>
8. <span data-ttu-id="496b4-200">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-200">No outbound rules on Frontend subnet, traffic is allowed</span></span>
9. <span data-ttu-id="496b4-201">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-201">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-202">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-202">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="496b4-203">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-203">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="496b4-204">Regola gruppo di sicurezza di rete 3 (da Internet a firewall), non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-204">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="496b4-205">Regola gruppo di sicurezza di rete 4 (da IIS01 ad AppVM01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="496b4-205">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
10. <span data-ttu-id="496b4-206">AppVM01 riceve la query SQL e risponde.</span><span class="sxs-lookup"><span data-stu-id="496b4-206">AppVM01 receives the SQL Query and responds</span></span>
11. <span data-ttu-id="496b4-207">Non essendoci regole in uscita sulla subnet back-end, la risposta è consentita.</span><span class="sxs-lookup"><span data-stu-id="496b4-207">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
12. <span data-ttu-id="496b4-208">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-208">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="496b4-209">Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.</span><span class="sxs-lookup"><span data-stu-id="496b4-209">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="496b4-210">La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-210">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
13. <span data-ttu-id="496b4-211">Il server IIS riceve la risposta SQL, completa la risposta HTTP e la invia al richiedente.</span><span class="sxs-lookup"><span data-stu-id="496b4-211">The IIS server receives the SQL response and completes the HTTP response and sends to the requestor</span></span>
14. <span data-ttu-id="496b4-212">Essendo una sessione NAT dal firewall, la destinazione della risposta (inizialmente) è il firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-212">Since this is a NAT session from the firewall, the response destination (initially) is for the Firewall</span></span>
15. <span data-ttu-id="496b4-213">Il firewall riceve la risposta dal server Web e la restituisce all'utente Internet.</span><span class="sxs-lookup"><span data-stu-id="496b4-213">The firewall receives the response from the Web Server and forwards back to the Internet User</span></span>
16. <span data-ttu-id="496b4-214">Non essendoci regole in uscita sulla subnet front-end, la risposta è consentita e l'utente Internet riceve la pagina Web richiesta.</span><span class="sxs-lookup"><span data-stu-id="496b4-214">Since there are no outbound rules on the Frontend subnet the response is allowed, and the Internet User receives the web page requested.</span></span>

#### <a name="allowed-rdp-to-backend"></a><span data-ttu-id="496b4-215">(Consentito) Da RDP a back-end</span><span class="sxs-lookup"><span data-stu-id="496b4-215">(Allowed) RDP to Backend</span></span>
1. <span data-ttu-id="496b4-216">L'amministratore del server su Internet richiede una sessione RDP ad AppVM01 su BackEnd001.CloudApp.Net:xxxxx, dove xxxxx è il numero di porta assegnato casualmente per RDP a AppVM01. Si può trovare la porta assegnata sul portale di Azure o tramite PowerShell.</span><span class="sxs-lookup"><span data-stu-id="496b4-216">Server Admin on internet requests RDP session to AppVM01 on BackEnd001.CloudApp.Net:xxxxx where xxxxx is the randomly assigned port number for RDP to AppVM01 (the assigned port can be found on the Azure Portal or via PowerShell)</span></span>
2. <span data-ttu-id="496b4-217">Poiché il firewall è in ascolto solo dell'indirizzo FrontEnd001.CloudApp.Net, non è interessato da questo flusso di traffico.</span><span class="sxs-lookup"><span data-stu-id="496b4-217">Since the Firewall is only listening on the FrontEnd001.CloudApp.Net address, it is not involved with this traffic flow</span></span>
3. <span data-ttu-id="496b4-218">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-218">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-219">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-219">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="496b4-220">Regola gruppo di sicurezza di rete 2 (RDP) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="496b4-220">NSG Rule 2 (RDP) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="496b4-221">Senza regole in uscita, sono applicabili le regole predefinite e il traffico restituito è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-221">With no outbound rules, default rules apply and return traffic is allowed</span></span>
5. <span data-ttu-id="496b4-222">La sessione RDP è abilitata.</span><span class="sxs-lookup"><span data-stu-id="496b4-222">RDP session is enabled</span></span>
6. <span data-ttu-id="496b4-223">AppVM01 richiede il nome utente e la password.</span><span class="sxs-lookup"><span data-stu-id="496b4-223">AppVM01 prompts for user name password</span></span>

#### <a name="allowed-web-server-dns-lookup-on-dns-server"></a><span data-ttu-id="496b4-224">(Consentito) Ricerca DNS del server Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="496b4-224">(Allowed) Web Server DNS lookup on DNS server</span></span>
1. <span data-ttu-id="496b4-225">Il server Web, IIS01, richiede un feed di dati all'indirizzo www.data.gov, ma deve risolvere l'indirizzo.</span><span class="sxs-lookup"><span data-stu-id="496b4-225">Web Server, IIS01, needs a data feed at www.data.gov, but needs to resolve the address.</span></span>
2. <span data-ttu-id="496b4-226">La configurazione di rete per la rete virtuale elenca DNS01 (10.0.2.4 nella subnet back-end) come server DNS primario, IIS01 invia la richiesta DNS a DNS01.</span><span class="sxs-lookup"><span data-stu-id="496b4-226">The network configuration for the VNet lists DNS01 (10.0.2.4 on the Backend subnet) as the primary DNS server, IIS01 sends the DNS request to DNS01</span></span>
3. <span data-ttu-id="496b4-227">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-227">No outbound rules on Frontend subnet, traffic is allowed</span></span>
4. <span data-ttu-id="496b4-228">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-228">Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-229">Regola gruppo di sicurezza di rete 1 (DNS) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="496b4-229">NSG Rule 1 (DNS) does apply, traffic is allowed, stop rule processing</span></span>
5. <span data-ttu-id="496b4-230">Il server DNS riceve la richiesta.</span><span class="sxs-lookup"><span data-stu-id="496b4-230">DNS server receives the request</span></span>
6. <span data-ttu-id="496b4-231">Il server DNS non ha l'indirizzo memorizzato nella cache e invia la richiesta a un server DNS radice su Internet.</span><span class="sxs-lookup"><span data-stu-id="496b4-231">DNS server doesn’t have the address cached and asks a root DNS server on the internet</span></span>
7. <span data-ttu-id="496b4-232">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-232">No outbound rules on Backend subnet, traffic is allowed</span></span>
8. <span data-ttu-id="496b4-233">Il server DNS Internet risponde perché la sessione è stata avviata internamente, la risposta è consentita.</span><span class="sxs-lookup"><span data-stu-id="496b4-233">Internet DNS server responds, since this session was initiated internally, the response is allowed</span></span>
9. <span data-ttu-id="496b4-234">Il server DNS memorizza la risposta nella cache e restituisce a IIS01 la risposta alla richiesta iniziale.</span><span class="sxs-lookup"><span data-stu-id="496b4-234">DNS server caches the response, and responds to the initial request back to IIS01</span></span>
10. <span data-ttu-id="496b4-235">Non sono impostate regole in uscita sulla subnet back-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-235">No outbound rules on Backend subnet, traffic is allowed</span></span>
11. <span data-ttu-id="496b4-236">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-236">Frontend subnet begins inbound rule processing:</span></span>
    1. <span data-ttu-id="496b4-237">Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.</span><span class="sxs-lookup"><span data-stu-id="496b4-237">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
    2. <span data-ttu-id="496b4-238">La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-238">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed</span></span>
12. <span data-ttu-id="496b4-239">IIS01 riceve la risposta da DNS01.</span><span class="sxs-lookup"><span data-stu-id="496b4-239">IIS01 receives the response from DNS01</span></span>

#### <a name="allowed-web-server-access-file-on-appvm01"></a><span data-ttu-id="496b4-240">(Consentito) Il server Web richiede l'accesso a un file su AppVM01</span><span class="sxs-lookup"><span data-stu-id="496b4-240">(Allowed) Web Server access file on AppVM01</span></span>
1. <span data-ttu-id="496b4-241">IIS01 richiede un file su AppVM01.</span><span class="sxs-lookup"><span data-stu-id="496b4-241">IIS01 asks for a file on AppVM01</span></span>
2. <span data-ttu-id="496b4-242">Non sono impostate regole in uscita sulla subnet front-end, il traffico è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-242">No outbound rules on Frontend subnet, traffic is allowed</span></span>
3. <span data-ttu-id="496b4-243">La subnet back-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-243">The Backend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-244">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-244">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="496b4-245">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-245">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="496b4-246">Regola gruppo di sicurezza di rete 3 (da Internet a firewall), non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-246">NSG Rule 3 (Internet to Firewall) doesn’t apply, move to next rule</span></span>
   4. <span data-ttu-id="496b4-247">Regola gruppo di sicurezza di rete 4 (da IIS01 ad AppVM01) applicabile, il traffico è consentito, l'elaborazione delle regole si arresta.</span><span class="sxs-lookup"><span data-stu-id="496b4-247">NSG Rule 4 (IIS01 to AppVM01) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="496b4-248">AppVM01 riceve la richiesta e risponde con il file (presupponendo che l'accesso sia autorizzato).</span><span class="sxs-lookup"><span data-stu-id="496b4-248">AppVM01 receives the request and responds with file (assuming access is authorized)</span></span>
5. <span data-ttu-id="496b4-249">Non essendoci regole in uscita sulla subnet back-end, la risposta è consentita.</span><span class="sxs-lookup"><span data-stu-id="496b4-249">Since there are no outbound rules on the Backend subnet the response is allowed</span></span>
6. <span data-ttu-id="496b4-250">La subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-250">Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-251">Non sono presenti regole del gruppo di sicurezza di rete applicabili al traffico in ingresso dalla subnet back-end alla subnet front-end, quindi nessuna regola del gruppo di sicurezza di rete è applicabile.</span><span class="sxs-lookup"><span data-stu-id="496b4-251">There is no NSG rule that applies to Inbound traffic from the Backend subnet to the Frontend subnet, so none of the NSG rules apply</span></span>
   2. <span data-ttu-id="496b4-252">La regola di sistema predefinita che consente il traffico tra le subnet consentirebbe questo tipo di traffico, perciò è consentito.</span><span class="sxs-lookup"><span data-stu-id="496b4-252">The default system rule allowing traffic between subnets would allow this traffic so the traffic is allowed.</span></span>
7. <span data-ttu-id="496b4-253">Il server IIS riceve il file.</span><span class="sxs-lookup"><span data-stu-id="496b4-253">The IIS server receives the file</span></span>

#### <a name="denied-web-direct-to-web-server"></a><span data-ttu-id="496b4-254">(Negato) Traffico Web diretto al server Web</span><span class="sxs-lookup"><span data-stu-id="496b4-254">(Denied) Web direct to Web Server</span></span>
<span data-ttu-id="496b4-255">Poiché il server Web, IIS01, e il firewall si trovano nello stesso servizio cloud, condividono lo stesso indirizzo IP pubblico.</span><span class="sxs-lookup"><span data-stu-id="496b4-255">Since the Web Server, IIS01, and the Firewall are in the same Cloud Service they share the same public facing IP address.</span></span> <span data-ttu-id="496b4-256">Tutto il traffico HTTP verrà quindi indirizzato al firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-256">Thus any HTTP traffic would be directed to the firewall.</span></span> <span data-ttu-id="496b4-257">Anche se la richiesta viene servita correttamente, non può passare direttamente al server Web. Come progettato, passa prima attraverso il firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-257">While the request would be successfully served, it cannot go directly to the Web Server, it passed, as designed, through the Firewall first.</span></span> <span data-ttu-id="496b4-258">Per il flusso di traffico, vedere il primo scenario in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="496b4-258">See the first Scenario in this section for the traffic flow.</span></span>

#### <a name="denied-web-to-backend-server"></a><span data-ttu-id="496b4-259">(Negato) Traffico Web al server back-end</span><span class="sxs-lookup"><span data-stu-id="496b4-259">(Denied) Web to Backend Server</span></span>
1. <span data-ttu-id="496b4-260">L'utente Internet prova ad accedere a un file su AppVM01 tramite il servizio BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="496b4-260">Internet user tries to access a file on AppVM01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="496b4-261">Non essendoci endpoint aperti per la condivisione file, il traffico non passa attraverso il servizio cloud e non raggiunge il server.</span><span class="sxs-lookup"><span data-stu-id="496b4-261">Since there are no endpoints open for file share, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="496b4-262">In caso di apertura degli endpoint per qualunque motivo, la regola del gruppo di sicurezza di rete 5 (da Internet a rete virtuale) bloccherà questo traffico.</span><span class="sxs-lookup"><span data-stu-id="496b4-262">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic</span></span>

#### <a name="denied-web-dns-lookup-on-dns-server"></a><span data-ttu-id="496b4-263">(Negato) Ricerca DNS Web sul server DNS</span><span class="sxs-lookup"><span data-stu-id="496b4-263">(Denied) Web DNS lookup on DNS server</span></span>
1. <span data-ttu-id="496b4-264">L'utente Internet prova a cercare un record DNS interno su DNS01 tramite il servizio BackEnd001.CloudApp.Net.</span><span class="sxs-lookup"><span data-stu-id="496b4-264">Internet user tries to lookup an internal DNS record on DNS01 through the BackEnd001.CloudApp.Net service</span></span>
2. <span data-ttu-id="496b4-265">Non essendoci endpoint aperti per DNS, il traffico non passa attraverso il servizio cloud e non raggiunge il server.</span><span class="sxs-lookup"><span data-stu-id="496b4-265">Since there are no endpoints open for DNS, this would not pass the Cloud Service and wouldn’t reach the server</span></span>
3. <span data-ttu-id="496b4-266">In caso di apertura degli endpoint per qualunque motivo, la regola del gruppo di sicurezza di rete 5 (da Internet a rete virtuale) bloccherà questo traffico. Si noti che la regola 1 (DNS) non è applicabile per due motivi, prima di tutto l'indirizzo di origine è Internet e questa regola si applica solo quando l'origine è la rete virtuale locale, poi questa è una regola di tipo Consenti e quindi non bloccherà mai il traffico.</span><span class="sxs-lookup"><span data-stu-id="496b4-266">If the endpoints were open for some reason, NSG rule 5 (Internet to VNet) would block this traffic (Note: that Rule 1 (DNS) would not apply for two reasons, first the source address is the internet, this rule only applies to the local VNet as the source, also this is an Allow rule, so it would never deny traffic)</span></span>

#### <a name="denied-web-to-sql-access-through-firewall"></a><span data-ttu-id="496b4-267">(Negato) Accesso dal Web a SQL tramite il firewall</span><span class="sxs-lookup"><span data-stu-id="496b4-267">(Denied) Web to SQL access through Firewall</span></span>
1. <span data-ttu-id="496b4-268">L'utente Internet richiede dati SQL a FrontEnd001.CloudApp.Net (servizio cloud per Internet).</span><span class="sxs-lookup"><span data-stu-id="496b4-268">Internet user requests SQL data from FrontEnd001.CloudApp.Net (Internet Facing Cloud Service)</span></span>
2. <span data-ttu-id="496b4-269">Non essendoci endpoint aperti per SQL, il traffico non passa attraverso il servizio cloud e non raggiunge il firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-269">Since there are no endpoints open for SQL, this would not pass the Cloud Service and wouldn’t reach the firewall</span></span>
3. <span data-ttu-id="496b4-270">Se gli endpoint sono aperti per qualunque motivo, la subnet front-end inizia l'elaborazione delle regole in ingresso:</span><span class="sxs-lookup"><span data-stu-id="496b4-270">If endpoints were open for some reason, the Frontend subnet begins inbound rule processing:</span></span>
   1. <span data-ttu-id="496b4-271">Regola gruppo di sicurezza di rete 1 (DNS) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-271">NSG Rule 1 (DNS) doesn’t apply, move to next rule</span></span>
   2. <span data-ttu-id="496b4-272">Regola gruppo di sicurezza di rete 2 (RDP) non applicabile, passa alla regola successiva.</span><span class="sxs-lookup"><span data-stu-id="496b4-272">NSG Rule 2 (RDP) doesn’t apply, move to next rule</span></span>
   3. <span data-ttu-id="496b4-273">Regola gruppo di sicurezza di rete 2 (da Internet a firewall) applicabile, il traffico è consentito, l'elaborazione della regola si arresta.</span><span class="sxs-lookup"><span data-stu-id="496b4-273">NSG Rule 2 (Internet to Firewall) does apply, traffic is allowed, stop rule processing</span></span>
4. <span data-ttu-id="496b4-274">Il traffico raggiunge l'indirizzo IP interno del firewall (10.0.1.4).</span><span class="sxs-lookup"><span data-stu-id="496b4-274">Traffic hits internal IP address of the firewall (10.0.1.4)</span></span>
5. <span data-ttu-id="496b4-275">Il firewall non ha regole di inoltro per SQL ed elimina il traffico.</span><span class="sxs-lookup"><span data-stu-id="496b4-275">Firewall has no forwarding rules for SQL and drops the traffic</span></span>

## <a name="conclusion"></a><span data-ttu-id="496b4-276">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="496b4-276">Conclusion</span></span>
<span data-ttu-id="496b4-277">Questo è un modo relativamente semplice per proteggere l'applicazione con un firewall e isolare la subnet back-end dal traffico in ingresso.</span><span class="sxs-lookup"><span data-stu-id="496b4-277">This is a relatively straight forward way of protecting your application with a firewall and isolating the back end subnet from inbound traffic.</span></span>

<span data-ttu-id="496b4-278">Altri esempi e una panoramica dei limiti di sicurezza della rete sono disponibili [qui][HOME].</span><span class="sxs-lookup"><span data-stu-id="496b4-278">More examples and an overview of network security boundaries can be found [here][HOME].</span></span>

## <a name="references"></a><span data-ttu-id="496b4-279">Riferimenti</span><span class="sxs-lookup"><span data-stu-id="496b4-279">References</span></span>
### <a name="main-script-and-network-config"></a><span data-ttu-id="496b4-280">Script principale e configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="496b4-280">Main Script and Network Config</span></span>
<span data-ttu-id="496b4-281">Salvare lo script completo in un file di script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="496b4-281">Save the Full Script in a PowerShell script file.</span></span> <span data-ttu-id="496b4-282">Salvare la configurazione di rete in un file denominato "NetworkConf2.xml".</span><span class="sxs-lookup"><span data-stu-id="496b4-282">Save the Network Config into a file named “NetworkConf2.xml”.</span></span>
<span data-ttu-id="496b4-283">Modificare le variabili definite dall'utente secondo le esigenze.</span><span class="sxs-lookup"><span data-stu-id="496b4-283">Modify the user defined variables as needed.</span></span> <span data-ttu-id="496b4-284">Eseguire lo script, quindi seguire le istruzioni per la configurazione delle regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="496b4-284">Run the script, then follow the Firewall rule setup instruction above.</span></span>

#### <a name="full-script"></a><span data-ttu-id="496b4-285">Script completo</span><span class="sxs-lookup"><span data-stu-id="496b4-285">Full Script</span></span>
<span data-ttu-id="496b4-286">In base alle variabili definite dall'utente, lo script consente di:</span><span class="sxs-lookup"><span data-stu-id="496b4-286">This script will, based on the user defined variables:</span></span>

1. <span data-ttu-id="496b4-287">Connettersi a una sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="496b4-287">Connect to an Azure subscription</span></span>
2. <span data-ttu-id="496b4-288">Creare un nuovo account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="496b4-288">Create a new storage account</span></span>
3. <span data-ttu-id="496b4-289">Creare una nuova rete virtuale e due subnet, come definito nel file di configurazione di rete.</span><span class="sxs-lookup"><span data-stu-id="496b4-289">Create a new VNet and two subnets as defined in the Network Config file</span></span>
4. <span data-ttu-id="496b4-290">Creare 4 macchine virtuali di Windows Server.</span><span class="sxs-lookup"><span data-stu-id="496b4-290">Build 4 windows server VMs</span></span>
5. <span data-ttu-id="496b4-291">Configurare il gruppo di sicurezza di rete eseguendo queste operazioni:</span><span class="sxs-lookup"><span data-stu-id="496b4-291">Configure NSG including:</span></span>
   * <span data-ttu-id="496b4-292">Creazione di un gruppo di sicurezza di rete</span><span class="sxs-lookup"><span data-stu-id="496b4-292">Creating a NSG</span></span>
   * <span data-ttu-id="496b4-293">Inserimento delle regole.</span><span class="sxs-lookup"><span data-stu-id="496b4-293">Populating it with rules</span></span>
   * <span data-ttu-id="496b4-294">Associazione del gruppo di sicurezza di rete alle subnet appropriate</span><span class="sxs-lookup"><span data-stu-id="496b4-294">Binding the NSG to the appropriate subnets</span></span>

<span data-ttu-id="496b4-295">Questo script di PowerShell deve essere eseguito localmente in un server o un PC connesso a Internet.</span><span class="sxs-lookup"><span data-stu-id="496b4-295">This PowerShell script should be run locally on an internet connected PC or server.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="496b4-296">Quando si esegue lo script, in PowerShell potrebbero venire visualizzati avvisi o altri messaggi informativi.</span><span class="sxs-lookup"><span data-stu-id="496b4-296">When this script is run, there may be warnings or other informational messages that pop in PowerShell.</span></span> <span data-ttu-id="496b4-297">Solo i messaggi di errore formattati in rosso possono indicare un problema.</span><span class="sxs-lookup"><span data-stu-id="496b4-297">Only error messages in red are cause for concern.</span></span>
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
       - One server on the FrontEnd Subnet (plus the NVA on the FrontEnd subnet)
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
       myFirewall - 10.0.1.4
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

    # User Defined Global Variables
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
        $NetworkConfigFile = "C:\Scripts\NetworkConf2.xml"

      # VM Base Disk Image Details
        $SrvImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Windows Server 2012 R2 Datacenter'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}
        $FWImg = Get-AzureVMImage | Where {$_.ImageFamily -match 'Barracuda NextGen Firewall'} | sort PublishedDate -Descending | Select ImageName -First 1 | ForEach {$_.ImageName}

      # NSG Details
        $NSGName = "MyVNetSG"

    # User Defined VM Specific Config
        # Note: To ensure proper NSG Rule creation later in this script:
        #       - The Web Server must be VM 1
        #       - The AppVM1 Server must be VM 2
        #       - The DNS server must be VM 4
        #
        #       Otherwise the NSG rules in the last section of this
        #       script will need to be changed to match the modified
        #       VM array numbers ($i) so the NSG Rule IP addresses
        #       are aligned to the associated VM IP addresses.

        # VM 0 - The Network Virtual Appliance (NVA)
          $VMName += "myFirewall"
          $ServiceName += $FrontEndService
          $VMFamily += "Firewall"
          $img += $FWImg
          $size += "Small"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.4"

        # VM 1 - The Web Server
          $VMName += "IIS01"
          $ServiceName += $FrontEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $FESubnet
          $VMIP += "10.0.1.5"

        # VM 2 - The First Appliaction Server
          $VMName += "AppVM01"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.5"

        # VM 3 - The Second Appliaction Server
          $VMName += "AppVM02"
          $ServiceName += $BackEndService
          $VMFamily += "Windows"
          $img += $SrvImg
          $size += "Standard_D3"
          $SubnetName += $BESubnet
          $VMIP += "10.0.2.6"

        # VM 4 - The DNS Server
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
    Else { Write-Host "The network config file was found" -ForegroundColor Green
            If (-Not (Select-String -Pattern $DeploymentLocation -Path $NetworkConfigFile)) {
                Write-Host 'The deployment location was not found in the network config file, please check the network config file to ensure the $DeploymentLocation varible is correct and the netowrk config file matches.' -ForegroundColor Yellow
                $FatalError = $true}
            Else { Write-Host "The deployment location was found in the network config file." -ForegroundColor Green}}

    If ($FatalError) {
        Write-Host "A fatal error has occured, please see the above messages for more information." -ForegroundColor Red
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
            If ($VMFamily[$i] -eq "Firewall") 
                { 
                New-AzureVMConfig -Name $VMName[$i] -ImageName $img[$i] –InstanceSize $size[$i] | `
                    Add-AzureProvisioningConfig -Linux -LinuxUser $LocalAdmin -Password $LocalAdminPwd  | `
                    Set-AzureSubnet  –SubnetNames $SubnetName[$i] | `
                    Set-AzureStaticVNetIP -IPAddress $VMIP[$i] | `
                    New-AzureVM –ServiceName $ServiceName[$i] -VNetName $VNetName -Location $DeploymentLocation
                # Set up all the EndPoints we'll need once we're up and running
                # Note: Web traffic goes through the firewall, so we'll need to set up a HTTP endpoint.
                #       Also, the firewall will be redirecting web traffic to a new IP and Port in a
                #       forwarding rule, so the HTTP endpoint here will have the same public and local
                #       port and the firewall will do the NATing and redirection as declared in the
                #       firewall rule.
                Add-AzureEndpoint -Name "MgmtPort1" -Protocol tcp -PublicPort 801  -LocalPort 801  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "MgmtPort2" -Protocol tcp -PublicPort 807  -LocalPort 807  -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                Add-AzureEndpoint -Name "HTTP"      -Protocol tcp -PublicPort 80   -LocalPort 80   -VM (Get-AzureVM -ServiceName $ServiceName[$i] -Name $VMName[$i]) | Update-AzureVM
                # Note: A SSH endpoint is automatically created on port 22 when the appliance is created.
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
        Write-Host "Configuring the Network Security Group (NSG)" -ForegroundColor Cyan

      # Build the NSG
        Write-Host "Building the NSG" -ForegroundColor Cyan
        New-AzureNetworkSecurityGroup -Name $NSGName -Location $DeploymentLocation -Label "Security group for $VNetName subnets in $DeploymentLocation"

      # Add NSG Rules
        Write-Host "Writing rules into the NSG" -ForegroundColor Cyan
        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internal DNS" -Type Inbound -Priority 100 -Action Allow `
            -SourceAddressPrefix VIRTUAL_NETWORK -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[4] -DestinationPortRange '53' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable RDP to $VNetName VNet" -Type Inbound -Priority 110 -Action Allow `
            -SourceAddressPrefix INTERNET -SourcePortRange '*' `
            -DestinationAddressPrefix VIRTUAL_NETWORK -DestinationPortRange '3389' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable Internet to $($VMName[0])" -Type Inbound -Priority 120 -Action Allow `
            -SourceAddressPrefix Internet -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[0] -DestinationPortRange '*' `
            -Protocol *

        Get-AzureNetworkSecurityGroup -Name $NSGName | Set-AzureNetworkSecurityRule -Name "Enable $($VMName[1]) to $($VMName[2])" -Type Inbound -Priority 130 -Action Allow `
            -SourceAddressPrefix $VMIP[1] -SourcePortRange '*' `
            -DestinationAddressPrefix $VMIP[2] -DestinationPortRange '*' `
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
      # Configure Firewall
      # Install Test Web App (Run Post-Build Script on the IIS Server)
      # Install Backend resource (Run Post-Build Script on the AppVM01)
      Write-Host
      Write-Host "Build Complete!" -ForegroundColor Green
      Write-Host
      Write-Host "Optional Post-script Manual Configuration Steps" -ForegroundColor Gray
      Write-Host " - Configure Firewall" -ForegroundColor Gray
      Write-Host " - Install Test Web App (Run Post-Build Script on the IIS Server)" -ForegroundColor Gray
      Write-Host " - Install Backend resource (Run Post-Build Script on the AppVM01)" -ForegroundColor Gray
      Write-Host


#### <a name="network-config-file"></a><span data-ttu-id="496b4-298">File di configurazione di rete</span><span class="sxs-lookup"><span data-stu-id="496b4-298">Network Config File</span></span>
<span data-ttu-id="496b4-299">Salvare questo file XML con il percorso aggiornato e aggiungere il collegamento a questo file nella variabile $NetworkConfigFile dello script precedente.</span><span class="sxs-lookup"><span data-stu-id="496b4-299">Save this xml file with updated location and add the link to this file to the $NetworkConfigFile variable in the script above.</span></span>

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

#### <a name="sample-application-scripts"></a><span data-ttu-id="496b4-300">Script di applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="496b4-300">Sample Application Scripts</span></span>
<span data-ttu-id="496b4-301">Se si vuole installare un'applicazione di esempio per questo e altri esempi di rete perimetrale, è possibile trovarne una in [Script di applicazione di esempio][SampleApp]</span><span class="sxs-lookup"><span data-stu-id="496b4-301">If you wish to install a sample application for this, and other DMZ Examples, one has been provided at the following link: [Sample Application Script][SampleApp]</span></span>

<!--Image References-->
<span data-ttu-id="496b4-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Rete perimetrale in ingresso con gruppo di sicurezza di rete"</span><span class="sxs-lookup"><span data-stu-id="496b4-302">[1]: ./media/virtual-networks-dmz-nsg-fw-asm/example2design.png "Inbound DMZ with NSG"</span></span>
<span data-ttu-id="496b4-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Icona di Destination NAT"</span><span class="sxs-lookup"><span data-stu-id="496b4-303">[2]: ./media/virtual-networks-dmz-nsg-fw-asm/dstnaticon.png "Destination NAT Icon"</span></span>
<span data-ttu-id="496b4-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Regola del firewall"</span><span class="sxs-lookup"><span data-stu-id="496b4-304">[3]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallrule.png "Firewall Rule"</span></span>
<span data-ttu-id="496b4-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Attivazione delle regole firewall"</span><span class="sxs-lookup"><span data-stu-id="496b4-305">[4]: ./media/virtual-networks-dmz-nsg-fw-asm/firewallruleactivate.png "Firewall Rule Activation"</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
[SampleApp]: ./virtual-networks-sample-app.md
[Example1]: ./virtual-networks-dmz-nsg-asm.md
